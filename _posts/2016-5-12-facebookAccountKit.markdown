---
layout: post
title:  "FB-Account-Kit"
date:   2016-05-12 5:43
categories: jekyll update
---
<a href="https://developers.facebook.com/docs/accountkit/android"><h2>FacebookAccountKit</h2></a>

1.처음 페이스북 앱을 등록하는것이라면 Skip and Create App ID 를 클릭해준다.
![Fbaccount1](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/facebookAccount1.png)
2.현재 사용하고 있는 앱이 있다면 앱을 클릭해주고 오른쪽 상단에 Skip Quick Start 를 눌러주면된다
![Fbaccount2](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/facebookAccount2.png)
3.등록하고나면 아래의 화면이 뜨게된다
![Fbaccount3](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/facebookAccount3.png)
4.아래처럼 그래들을 등록

```xml
repositories {
  jcenter()
}

dependencies {
  compile 'com.facebook.android:account-kit-sdk:4.+'
}
```

5.AndroidManifest를 아래처럼  3번째 사진에 있는 ACCOUNT_KIT_CLIENT_TOKEN, appid strings 에 등록해준다.

```xml
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.RECEIVE_SMS" />
  <uses-permission android:name="android.permission.READ_PHONE_STATE" />
  <uses-permission android:name="android.permission.GET_ACCOUNTS" />

  <application
   android:theme="@style/AppTheme">
  ...생략

    <activity
    android:name="com.facebook.accountkit.ui.AccountKitActivity"
    android:theme="@style/AppLoginTheme"
    tools:replace="android:theme"/>

  <meta-data android:name="com.facebook.sdk.ApplicationId"
             android:value="@string/app_id" />
  <meta-data android:name="com.facebook.accountkit.ClientToken"
             android:value="@string/ACCOUNT_KIT_CLIENT_TOKEN" />
  <meta-data android:name="com.facebook.accountkit.ApplicationName"
             android:value="@string/app_name" />
   </application>

```

6.MainActivity 소스 이다 바인드에 버터나이프 라이브러리를 사용함.

```java
public class MainActivity extends AppCompatActivity {

  private static final String TAG = "TAG";

  @OnClick(R.id.btn_email)
  void onEmail() {
    Log.d(TAG, "btnemailclick");
    onLoginPhoneOrEmail(LoginType.EMAIL);
  }

  @OnClick(R.id.btn_phone)
  void onPhone() {
    Log.d(TAG,"btnphoneclick");
    onLoginPhoneOrEmail(LoginType.PHONE);
  }


  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    AccountKit.initialize(getApplicationContext());
    setContentView(R.layout.activity_main);
    ButterKnife.bind(this);

    AccessToken accessToken = AccountKit.getCurrentAccessToken();

    if (accessToken != null) {
      //Handle Returning User
      goToMyLoggedInActivity();
      Log.d(TAG, "onCreate: !null " + accessToken);
    } else {
      //Handle new or logged out user
      Log.d(TAG, "onCreate: null " + accessToken);
    }
  }

  public static int APP_REQUEST_CODE = 99;

  public void onLoginPhoneOrEmail(LoginType loginType) {
    final Intent intent = new Intent(this, AccountKitActivity.class);
    AccountKitConfiguration.AccountKitConfigurationBuilder configurationBuilder =
            new AccountKitConfiguration.AccountKitConfigurationBuilder(
                    loginType,
                    AccountKitActivity.ResponseType.CODE); // or .ResponseType.TOKEN
    // ... perform additional configuration ...
    intent.putExtra(
            AccountKitActivity.ACCOUNT_KIT_ACTIVITY_CONFIGURATION,
            configurationBuilder.build());
    startActivityForResult(intent, APP_REQUEST_CODE);
  }

  @Override
  protected void onActivityResult(
          final int requestCode,
          final int resultCode,
          final Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (requestCode == APP_REQUEST_CODE) { // confirm that this response matches your request
      AccountKitLoginResult loginResult = data.getParcelableExtra(AccountKitLoginResult.RESULT_KEY);
      String toastMessage;
      if (loginResult.getError() != null) {
        toastMessage = loginResult.getError().getErrorType().getMessage();
        showErrorActivity(loginResult.getError());
      } else if (loginResult.wasCancelled()) {
        toastMessage = "Login Cancelled";
      } else {
        if (loginResult.getAccessToken() != null) {
          toastMessage = "Success:" + loginResult.getAccessToken().getAccountId();
        } else {
          toastMessage = String.format("Success:%s...",
                  loginResult.getAuthorizationCode().substring(0,10));
        }

        // If you have an authorization code, retrieve it from
        // loginResult.getAuthorizationCode()
        // and pass it to your server and exchange it for an access token.

        // Success! Start your next activity...
        goToMyLoggedInActivity();
      }

      // Surface the result to your user in an appropriate way.
      Toast.makeText(this, toastMessage, Toast.LENGTH_LONG).show();
    }
  }

  private void showErrorActivity(AccountKitError error) {
    Log.d("TAG", "showErrorActivity: " + error.toString());
  }

  private void goToMyLoggedInActivity(){
    final Intent intent = new Intent(this, SuccessActivity.class);
    this.startActivity(intent);
  }
}
```

7. xml Theme.AccountKit 이 없다고 익셉션이 뜨는경우
style.xml 에 아래코드를 추가해준다 

```xml
    <style name="AppLoginTheme" parent="Theme.AccountKit" />
```