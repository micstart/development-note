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
调用com.android.internal.telephony.SmsApplication类的以下两个方法任一即可：  
~~~
private static void assignWriteSmsPermissionToSystemApp(Context context,
        PackageManager packageManager, AppOpsManager appOps, String packageName)

private static void assignWriteSmsPermissionToSystemUid(AppOpsManager appOps, int uid)
~~~

