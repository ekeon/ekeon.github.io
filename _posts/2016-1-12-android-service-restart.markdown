---
layout: post
title:  "Android Service Restart!"
date:   2016-01-12 3:53
categories: jekyll update
---

### PersistentService.java

    {.java}
    public class PersistentService extends Service {

        @Override
        public void onCreate() {
                Log.d("PersistentService", "onCreate");
                unregisterRestartAlarm(); // 만들어질때 알람 해제해줌.
                super.onCreate();
        }

        @Override
        public void onDestroy() {
                Log.d("PersistentService","onDestroy");

                registerRestartAlarm();  // 서비스 종료될때 알람등록해줌.
                super.onDestroy();
        }

        public void registerRestartAlarm() {
                Intent intent = new Intent(PersistentService.this, RestartService.class);
                intent.setAction("ACTION.RESTART.PersistentService");

                PendingIntent sender = PendingIntent.getBroadcast(PersistentService.this, 0, intent, 0);

                long firstTime = SystemClock.elapsedRealtime();
                firstTime += 1000 * 10;

                AlarmManager am = (AlarmManager)getSystemService(ALARM_SERVICE);
                am.setRepeating(AlarmManager.ELAPSED_REALTIME_WAKEUP, firstTime * 10, 1000, sender);
        }

        public void unregisterRestartAlarm() {
                Intent intent = new Intent(PersistentService.this, RestartService.class);
                intent.setAction("ACTION.RESTART.PersistentService");

                PendingIntent sender = PendingIntent.getBroadcast(PersistentService.this, 0, intent, 0);

                AlarmManager am = (AlarmManager)getSystemService(ALARM_SERVICE);
                am.cancel(sender);
        }

        @Override
        public IBinder onBind(Intent intent) {
                Log.d("TAG", "RESTART SERVICE"); // Service 를 extend 받을시 필수
                return null;
        }
    }

### RestartService.java
    
    {.java}
    public class RestartService extends BroadcastReceiver{

	    @Override
	    public void onReceive(Context context, Intent intent) {
	        Log.d("RestartService", "RestartService called! :" + intent.getAction());

	        if(intent.getAction().equals("ACTION.RESTART.PERSISTENTSERVICE")){
	            Log.d("RestartService", "ACTION_RESTART_PERSISTENTSERVICE");
	            Intent i = new Intent(context, PersistentService.class);
	            context.startService(i);
	        }

	        if (intent.getAction().equals(Intent.ACTION_BOOT_COMPLETED)) {
	            Log.d("RestartService", "ACTION_BOOT_COMPLETED");
	            Intent i = new Intent(context, PersistentService.class);
	            context.startService(i);
	        }
	    }
    }

###  MainActivity.java
    
    {.java}
    BroadcastReceiver receiver = new RestartService();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Intent intentMyService = new Intent(this, PersistentService.class);
        receiver = new RestartService();

        try{
            IntentFilter mainFilter = new IntentFilter("com.ekeon.clipboardtest.restart");
            registerReceiver(receiver, mainFilter);
            startService(intentMyService);
        }
        catch (Exception e) {
            Log.d("RestartService",e.getMessage()+"");
        }
    }

    @Override
    protected void onDestroy() {
        unregisterReceiver(receiver);
        super.onDestroy();
    }

### AndroidManifest.xml
    
    {.xml}
    <?xml version="1.0" encoding="utf-8"?>
    <manifest
        package="com.ekeon.clipboardtest"
        xmlns:android="http://schemas.android.com/apk/res/android">
    
      <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
    
      <application
          android:allowBackup="true"
          android:icon="@mipmap/ic_launcher"
          android:label="@string/app_name"
          android:supportsRtl="true"
          android:theme="@style/AppTheme">
    
        <activity android:name=".MainActivity">
          <intent-filter>
            <action android:name="android.intent.action.MAIN"/>
            <category android:name="android.intent.category.LAUNCHER"/>
          </intent-filter>
        </activity>
    
        <service
            android:name=".PersistentService"
            android:enabled="true"
            android:process=":remote">
          <intent-filter>
            <action android:name="com.ekeon.clipboardtest.restart"/>
          </intent-filter>
        </service>
    
        <receiver
            android:name=".RestartService"
            android:enabled="true"
            android:exported="false"
            android:label="RestartService"
            android:process=":remote">
          <intent-filter>
            <action android:name="ACTION.RESTART.PersistentService"/>
            <action android:name="android.intent.action.BOOT_COMPLETED"/>
          </intent-filter>
    
        </receiver>
      </application>
    
    </manifest>
