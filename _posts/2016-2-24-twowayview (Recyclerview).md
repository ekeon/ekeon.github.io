---
layout: post
title:  "TwoWayView + RecyclerView"
date:   2016-02-24 4:35
categories: jekyll update
---

<a href="https://github.com/lucasr/twoway-view">twoway-view</a> 란 안드로이드 <a href="http://developer.android.com/intl/ko/reference/android/support/v7/widget/RecyclerView.html">RecyclerView 의 라이브러리 이다.
기본 RecyclerView 와 사용법은 똑같지만 RecyclerView 를 init 해주는 시점에서 setLayoutManager부분이 기존 RecyclerView 보다 많은 기능을 제공해주기 때문에 일반 RecyclerView를 쓰기보다는 TwoWayView를 사용하기를 추천한다.

##gradle : compile 'org.lucasr.twowayview:twowayview:0.1.4'

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

{% endhighlight %}

