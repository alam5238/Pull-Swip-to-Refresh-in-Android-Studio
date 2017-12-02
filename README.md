# Pull-Swip-to-Refresh-in-Android-Studio
Pull-down or swip to Refresh of WebView widget.

##Follow these Step::
---

***Step 1:***
Create a Project first in Android Studio.

***Step 2:***
Add internet permission in `Android Manifest.xml` file

```
<uses-permission android:name="android.permission.INTERNET"/>
```

***Step 3:***
Now add below code in your `activity_main.xml` file in this location - `res/layout/activity_main.xml` 

```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:background="@android:color/holo_green_light"
    android:layout_height="match_parent" 
    android:layout_width="match_parent"
    tools:context="com.nastecltd.cal.splashgif.MainActivity" >

    <android.support.v4.widget.SwipeRefreshLayout
        android:id="@+id/swip"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <WebView
            android:id="@+id/webView"
            android:layout_width="match_parent"
            android:layout_height="match_parent" >

        </WebView>

    </android.support.v4.widget.SwipeRefreshLayout>


</RelativeLayout>

```
***Step 4:***
Now create Global veriables `webView and swip` in `MainActivity.java` and create constractor `swip` and set refresh listner.

```
    private WebView webView;
    SwipeRefreshLayout swip;
```

```
protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        swip = (SwipeRefreshLayout)findViewById(R.id.swip);
        swip.setOnRefreshListener(new SwipeRefreshLayout.OnRefreshListener(){

            @Override
            public void onRefresh(){

                loadWeb();
            }

        });

        loadWeb();




    }
```

***Step 5:***
Now Create a Methord `loadWeb()` in `MainActivity.java` class.

```
public void loadWeb(){

        webView = (WebView)findViewById(R.id.webView);
        webView.getSettings().setJavaScriptEnabled(true);
        webView.getSettings().setAppCacheEnabled(true);
        webView.loadUrl("http://yourWebAddress.com");
        swip.setRefreshing(true);
        webView.setWebViewClient(new WebViewClient(){

            @Override
            public void onReceivedError(WebView view, int errorCode, String description,String fallinUrl) {
                webView.loadUrl("file:///android_asset/www/error.html");
            }

            @Override
            public void onPageFinished(WebView view, String url) {

                swip.setRefreshing(false);
            }
        });



    }
```
Here in `onRecivedError()` method `webView.loadUrl()` called the web address when WebView faild load any web page or somthing error else. `file:///android_asset/www/error.html` called android offline error page in assets folder.


***Step 6:***
Build, Run and Enjoy!!


Follow on Web :: 


