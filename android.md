### Activity xxx has leaked window PhoneWindow$DecorView/PopupWindow$PopupDecorView) that was originally added here  
在Activity的onPause或onDestroy方法中调用PhoneWindow或PopupWindow的dismiss方法，例如：
~~~
@Override
protected void onDestroy() {
    if(mDialog != null) {
        mDialog.dismiss();
    }
    super.onDestroy();
}
~~~
当PhoneWindow或PopupWindow属于自定义View组件时，可以在View的onDetachedFromWindow方法中调用dismiss方法。  

### Assign WRITE_SMS AppOps permission to some special system apps  
自android 4.4(API 19)开始仅允许默认短信应用写短信，系统应用可调用com.android.internal.telephony.SmsApplication类的以下两个方法任一授予写短信权限： 
~~~
private static void assignWriteSmsPermissionToSystemApp(Context context,
        PackageManager packageManager, AppOpsManager appOps, String packageName)

private static void assignWriteSmsPermissionToSystemUid(AppOpsManager appOps, int uid)
~~~
其内部实现和https://stackoverflow.com/questions/27697282/android-kitkat-api-19-how-to-write-messages-in-sms-content-provider-without类似。
