---
layout: post
title:  "gson + williamChart"
date:   2016-05-12 5:43
categories: jekyll update
---
<p class="lead"> <a href="https://github.com/google/gson">Gson</a> : json convert to java object</p>
<p class="lead"> <a href="https://github.com/diogobernardino/WilliamChart">WilliamChart</a> : android chart library</p>

{% highlight java %}
{
  "dummy": {
    "dummydata": {
      "dummylist": {
        "one": 42.87,
        "two": 42.16,
        "three": 42.45,
        "four": 39.16,
        "five": 37.25,
        "six": 38.02
      },
      "dummycount": 40.32,
      "dummydummy": 0
    }
  }
}
{% endhighlight %}


{% highlight java %}
public class DummyListModel {
  @SerializedName("dummylist")
  private TreeMap<String, Float> dummylist;
  @SerializedName("dummycount")
  private float dummycount;
  @SerializedName("dummydummy")
  private Integer dummydummy;

  public TreeMap<String, Float> getDummyList() {
    return dummyList;
  }

  public void setDummyList(TreeMap<String, Float> dummyList) {
    this.dummyList = dummyList;
  }

  public float getDummyCount() {
    return dummyCount;
  }

  public void setDummyCount(float dummyCount) {
    this.dummyCount = dummyCount;
  }

  public Integer getDummydummy() {
    return dummydummy;
  }

  public void setDummydummy(Integer dummydummy) {
    this.dummydummy = dummydummy;
  }

}
{% endhighlight %}

{% highlight java %}
public class DummyDataModel {
  @SerializedName("dummydata")
  public DummyListModel dummyListModel;

  public void setDummyListModel(DummyListModel dummyListModel) {
    this.dummyListModel = dummyListModel;
  }

  public DummyListModel getDummyListModel() {
    return commentCount;
  }
{% endhighlight %}

{% highlight java %}
public class DummyModel {
  @SerializedName("dummy")
  private DummyDataModel dummydatamodel;

  public DummyData getDummyDataModel() {
    return dummydatamodel;
  }

  public void setDummyDataModel(DummyDataModel dummydatamodel) {
    this.dummydatamodel = dummydatamodel;
  }
}
{% endhighlight %}

```
  private final static String dummyjson = "dummyjson"//예제 json;

  public DummyJsonModel getDummyModel() {
    Gson gson = new Gson();
    DummyJsonModel dummyJsonModel = gson.fromJson(dummyjson, DummyJsonModel.class);

    return dummyJsonModel == null ? null : dummyJsonModel;
}
```
