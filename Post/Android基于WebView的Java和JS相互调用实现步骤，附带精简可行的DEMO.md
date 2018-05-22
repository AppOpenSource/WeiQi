

在Android系统中，WebView加载HTML5页面并实现Java和JS的相互调用的实现步骤如下：


1、在AndroidManifest.xml文件中增加访问网络的权限；

2、在布局文件中添加WebView控件标签；

3、在Activity中初始化WebView控件并且通过LoadUrl的方式加载HTML5页面；

4、給WebView设置自定义的客户端，覆盖第三方或者系统默认的打开方式，改用WebView加载自定路径的网页；

5、设置WebView的setJavaScriptEnabled为TRUE（默认为FALSE，不支持JS，可能会导致页面加载不出来）；

6、给WebView对象添加JS接口，通过addJavascriptInterface(obj, XXX)的方式，XXX自定义，在8中使用；

7、添加相应的JS需要调用的Java方法，方法修饰符需要时public的，写成private的话JS无法访问（调用不到），同时给所有需要在JS中调用的对象方法前加上注解       @JavascriptInterface，在API 17即Android4.2.2之后；

8,、在JS中调用Java方法可以通过window.XXX.startFunction()的方式，其中XXX是在6中定义好的；

9、在JS中添加Java需要调用的接口，形如：function updateHtml() {...}；

10、在Java调用JS接口，形如：mWebView.loadUrl("javascript:updateHtml()")；

11、至此，JS和Java的互相调用已经初步实现；

MainActivity.java代码如下：
```java
package com.weiqi.webview;  
  
import android.app.Activity;  
import android.app.AlertDialog;  
import android.content.DialogInterface;  
import android.os.Bundle;  
import android.view.KeyEvent;  
import android.view.View;  
import android.view.Window;  
import android.webkit.JavascriptInterface;  
import android.webkit.WebView;  
import android.webkit.WebViewClient;  
import android.widget.Button;  
  
public class MainActivity extends Activity {  
      
    private WebView mWebView;  
    private Button mButton;  
      
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
          
        requestWindowFeature(Window.FEATURE_NO_TITLE);//去掉标题栏  
        this.setContentView(R.layout.main_activity);  
          
        mButton = (Button) findViewById(R.id.button);  
        mWebView = (WebView) findViewById(R.id.web_view);  
          
        //默认不支持JS，导致部分网页加载不出来  
        mWebView.getSettings().setJavaScriptEnabled(true);  
        mWebView.addJavascriptInterface(this, "update");  
           
        //mWebView.loadUrl("http://baidu.com");//加载云端数据  
        mWebView.loadUrl("file:///android_asset/demo.html");//加载本地数据  
          
        //默认用系统浏览器或者第三方浏览器打开页面，设置后改用WebView打开  
        mWebView.setWebViewClient(new WebViewClient() {  
            @Override  
            public boolean shouldOverrideUrlLoading(WebView view, String url) {  
                return super.shouldOverrideUrlLoading(view, url);  
            }  
        });  
          
        mButton.setOnClickListener(new View.OnClickListener() {  
              
            @Override  
            public void onClick(View v) {  
                mWebView.loadUrl("javascript:updateHtml()");  
            }  
        });  
    }  
      
    @JavascriptInterface  
    public void startFunction() {  
          
        AlertDialog.Builder dialog = new AlertDialog.Builder(this);  
        dialog.setTitle("标题");  
        dialog.setMessage("测试消息");  
          
        dialog.setPositiveButton("确定", new DialogInterface.OnClickListener() {  
            @Override  
            public void onClick(DialogInterface dialog, int which) {  
                dialog.dismiss();  
            }  
        });  
        dialog.create().show();  
    }  
      
    @Override  
    public boolean onKeyDown(int keyCode, KeyEvent event) {  
          
        if ((keyCode == KeyEvent.KEYCODE_BACK) && mWebView.canGoBack()) {  
            mWebView.goBack(); //默认按返回键退出应用，改为回退到上一页  
            return true;  
        }  
          
        return super.onKeyDown(keyCode, event);  
    }  
}
```

HTML页面demo.html代码如下：
```html
<html>  
<head>  
<script type="text/javascript">  
    function updateHtml() {  
        document.getElementById("content").innerHTML = "java调用js更新页面";  
        alert("dialog");  
    }  
</script>  
</head>  
  
<body>  
this is my html <a onClick="window.update.startFunction()" href="";>点击，js调用java中的toast</a>  
<span id="content"></span>  
</body>  
</html>  
```

布局文件main_activity.xml如下：
```xml
<?xml version="1.0" encoding="utf-8"?>  
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    android:orientation="vertical" >  
  
    <WebView  
        android:id="@+id/web_view"  
        android:layout_width="wrap_content"  
        android:layout_height="wrap_content"  
        android:layout_weight="11" />  
  
    <Button  
        android:id="@+id/button"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:layout_weight="1"  
        android:text="调用HTML中的JS方法" />  
  
</LinearLayout>  
```

配置文件AndroidManifest.xml内容如下：
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"  
    package="com.weiqi.webview"  
    android:versionCode="1"  
    android:versionName="1.0" >  
  
    <uses-sdk  
        android:minSdkVersion="8"  
        android:targetSdkVersion="19" />  
  
    <uses-permission android:name="android.permission.INTERNET" />  
  
    <application  
        android:allowBackup="true"  
        android:icon="@drawable/ic_launcher"  
        android:label="@string/app_name"  
        android:theme="@style/AppTheme" >  
        <activity android:name=".MainActivity" >  
            <intent-filter>  
                <action android:name="android.intent.action.MAIN" />  
  
                <category android:name="android.intent.category.LAUNCHER" />  
            </intent-filter>  
        </activity>  
    </application>  
  
</manifest> 
```
