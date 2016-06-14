---
layout: post
title:  "Android DeelLink"
date:   2016-01-15 4:38
categories: jekyll update
---

아래처럼 설정해줌.

{% highlight xml %}
<activity
  android:name=".MainActivty"
  android:screenOrientation="portrait"
  android:label="@string/app_name">

  <intent-filter>
    <action android:name="android.intent.action.MAIN"/>

    <category android:name="android.intent.category.LAUNCHER"/>
  </intent-filter>
</activity>

<activity
    android:name=".DeepLinkActivity"
    android:screenOrientation="portrait"
    android:label="@string/app_name">

  <intent-filter>
    <action android:name="android.intent.action.VIEW"/>
    <category android:name="android.intent.category.DEFAULT"/>
    <category android:name="android.intent.category.BROWSABLE"/>

    <!--android-app://com.ekeon.deeplink/ekeon/main-->
    <data android:scheme="ekeon"
          android:host="main"/>
  </intent-filter>
</activity>
{% endhighlight %}

<a href="https://developers.google.com/app-indexing/android/test?hl=ko">DeepLinkTest</a> 들어가서 android-app://{package}/{scheme}/{host}/{path} 형식으로 넣어준다.
##ex) android-app://com.ekeon.deeplink/ekeon/main

{% highlight java %}

public class DeepLinkActivity{

  @Override
  protected void onCreate() {
    Intent intent = getIntent();

    Intent goHomeActivity = new Intent(this, HomeActivity.class);
    startActivity(goHomeActivity); // 핸들링 해주면된다
  }
}
{% endhighlight %}

