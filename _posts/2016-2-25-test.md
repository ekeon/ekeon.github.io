---
layout: post
title:  "TwoWayView + RecyclerView"
date:   2016-02-24 4:35
categories: jekyll update
---

<a href="https://github.com/lucasr/twoway-view">twoway-view</a> 란 안드로이드 <a href="http://developer.android.com/intl/ko/reference/android/support/v7/widget/RecyclerView.html">RecyclerView 의 라이브러리 이다.</a>  
기본 RecyclerView 와 사용법은 똑같지만 RecyclerView 를 init 해주는 시점에서 setLayoutManager부분이 기존 RecyclerView 보다 많은 기능을 제공해주기 때문에 일반 RecyclerView를 쓰기보다는 TwoWayView를 사용하기를 추천한다.  

<a href="https://github.com/ekeon/twowayviewExample">예제소스 깃 주소</a>

####gradle : compile 'org.lucasr.twowayview:twowayview:0.1.4'  
  
RecyclerView에 사용할 뷰홀더를 3개 만들었다.  
###holder_one.xml, HolderOne.java
{% highlight xml %}
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:background="@android:color/holo_red_light">

  <Button
      android:text="view holder one"
      android:layout_width="match_parent"
      android:layout_height="100dp"/>
</LinearLayout>
{% endhighlight %}

{% highlight java %}
public class HolderOne extends RecyclerView.ViewHolder {

  public static HolderOne newInstance(Context context) {
    View itemView = LayoutInflater.from(context).inflate(R.layout.holder_one, null);
    return new HolderOne(itemView);
  }

  public HolderOne(View itemView) {
    super(itemView);
    ButterKnife.bind(this, itemView);
  }

}
{% endhighlight %}

###holder_two.xml, HolderTwo.java
{% highlight xml %}
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:background="@android:color/holo_blue_dark">

  <Button
      android:text="view holder two"
      android:layout_width="match_parent"
      android:layout_height="100dp"/>
</LinearLayout>
{% endhighlight %}

{% highlight java %}
public class HolderTwo extends RecyclerView.ViewHolder {

  public static HolderTwo newInstance(Context context) {
    View itemView = LayoutInflater.from(context).inflate(R.layout.holder_two, null);
    return new HolderTwo(itemView);
  }

  public HolderTwo(View itemView) {
    super(itemView);
  }
}
{% endhighlight %}

###holder_three.xml, HolderThree.java
{% highlight xml %}
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:background="@android:color/holo_green_light">

  <Button
      android:text="view holder three"
      android:layout_width="match_parent"
      android:layout_height="100dp"/>
</LinearLayout>
{% endhighlight %}

{% highlight java %}
public class HolderThree extends RecyclerView.ViewHolder {

  public static HolderThree newInstance(Context context) {
    View itemView = LayoutInflater.from(context).inflate(R.layout.holder_three, null);
    return new HolderThree(itemView);
  }

  public HolderThree(View itemView) {
    super(itemView);
  }
}
{% endhighlight %}

###twoWayView Adapter
```java
public class TwoWaySampleAdapter extends TwoWayView.Adapter {

  private final int TYPE_HOLDER_ONE = 0;
  private final int TYPE_HOLDER_TWO = 1;
  private final int TYPE_HOLDER_THREE = 2;

  @Override
  public RecyclerView.ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
    RecyclerView.ViewHolder viewHolder = null;
    Context context = parent.getContext();

    //위에 int 로 지정해놓은 뷰홀더 타입에 인스턴스를 넘겨주고 viewholder을 리턴해줌.
    switch (viewType) {
      case TYPE_HOLDER_ONE:
        viewHolder = HolderOne.newInstance(context);
        break;
      case TYPE_HOLDER_TWO:
        viewHolder = HolderTwo.newInstance(context);
        break;
      case TYPE_HOLDER_THREE:
        viewHolder = HolderThree.newInstance(context);
        break;
    }
    return viewHolder;
  }

  @Override
  public void onBindViewHolder(RecyclerView.ViewHolder holder, int position) {
  //view holder 에 position값이나 data 등을 넘겨줄때 사용해준다.
  }

  @Override
  public int getItemCount() {
    //보통 어댑터를 set해줄때 넘겨주는 array의 size로 카운트를 정해놓지만 간단한 예제이기때문에 고정된 숫자로 넣어두었다.
    //ex) array.size;
    return 13;
  }

  @Override
  public int getItemViewType(int position) {
  //넣고싶은 위치에 분기를 쳐서 타입을 리턴해주면 된다.
    if (position >= 0 && position <= 4) {
     return TYPE_HOLDER_ONE;
    }

    if (position >= 5 && position <= 9) {
      return TYPE_HOLDER_TWO;
    }

    if (position >= 10 && position <= 14) {
      return TYPE_HOLDER_THREE;
    }
    return super.getItemViewType(position);
  }
}
```

###Adapter를 init해줄 Fragment
```java
public class TwoWaySampleFragment extends Fragment {

  @Bind(R.id.twv_test) TwoWayView testRecyclerView;
  TwoWaySampleAdapter twoWaySampleAdapter;

  public static TwoWaySampleFragment newInstance() {
    return new TwoWaySampleFragment();
  }

  @Override
  public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    return inflater.inflate(R.layout.twowayview, container, false);
  }

  @Override
  public void onViewCreated(View view, @Nullable Bundle savedInstanceState) {
    super.onViewCreated(view, savedInstanceState);
    ButterKnife.bind(this, view);
    twoWaySampleAdapter = new TwoWaySampleAdapter();

    testRecyclerView.setLayoutManager(new StaggeredGridLayoutManager(TwoWayLayoutManager.Orientation.VERTICAL, 2, 2));
    testRecyclerView.setAdapter(twoWaySampleAdapter);

    Log.d("TAG", "init");
  }

  @Override
  public void onDestroy() {
    ButterKnife.unbind(this);
    super.onDestroy();
  }

}
```

```java
//넘겨주는 부분 MainActivity.
  @OnClick(R.id.btn_show_twv)
  void onShowTwv() {
    Fragment twoWaySampleFragment = TwoWaySampleFragment.newInstance();
    FragmentManager fragmentManager = getSupportFragmentManager();
    FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction()
            .add(R.id.fl_fragment_layout, twoWaySampleFragment)
            .show(twoWaySampleFragment);

    fragmentTransaction.commit();

  }
```

####참고 예제
{% highlight java %}
public class HolderOne extends RecyclerView.ViewHolder {

  @Bind(R.id.btn_holder_one) Button btnHolderOne;

  public static HolderOne newInstance(Context context) {
    View itemView = LayoutInflater.from(context).inflate(R.layout.holder_one, null);
    return new HolderOne(itemView);
  }

  public HolderOne(View itemView) {
    super(itemView);
    ButterKnife.bind(this, itemView);
  }

  publiv void bind(int position) {
    btnHolderOne.setText("" + position);
  }

}
...
//in adapter

  @Override
  protected void onBindViewHolder(RecyclerView.ViewHolder holder, int position) {
    if (holder instanceof HolderOne) {
      ((HolderOne) holder).bind(postiong);
      return;
    }
  }

  private void onBindChannelResult(SearchResultChannelHolder holder, int position) {
    ChannelModel channelModel = channels.get(position);
    holder.bind(channelModel);
  }
{% endhighlight %}


