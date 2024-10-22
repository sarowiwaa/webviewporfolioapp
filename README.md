WebView Portfolio App
This is an Android app that integrates Ken Sarowiwa's online portfolio (https://sarowiwaa.github.io/myportfolio) into a native Android application using a WebView. The app allows users to browse the portfolio within the app interface, offering basic web browsing features such as back navigation and zoom controls.

Features
Loads Ken Sarowiwa's portfolio directly in the app.
Allows zooming in and out of the web content with pinch-to-zoom gestures.
Supports back navigation within the web pages.
Displays web pages without opening an external browser.
Prerequisites
Android Studio (latest version recommended)
A device or emulator running Android 5.0 (Lollipop) or higher.
How to Use
Clone or Download the Project:
bash
Copy code
git clone https://github.com/your-username/portfolio-webview-app.git
Open the Project in Android Studio.
Run the App on an Android device or emulator.
Code Overview
Main Files
AndroidManifest.xml
Make sure that the app has permission to access the internet:

xml
Copy code
<uses-permission android:name="android.permission.INTERNET" />
activity_main.xml
This layout file contains a simple WebView to display the portfolio website.

xml
Copy code
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <WebView
        android:id="@+id/webView"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</LinearLayout>
MainActivity.java
This Java class is the main activity of the app. It:

Loads the portfolio URL (https://sarowiwaa.github.io/myportfolio) into the WebView.
Enables JavaScript and zoom controls for a better user experience.
Handles back button navigation to move through the web page history.
java
Copy code
package com.example.webviewapp;

import android.os.Bundle;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Find the WebView by its ID
        WebView webView = findViewById(R.id.webView);

        // Enable JavaScript
        webView.getSettings().setJavaScriptEnabled(true);

        // Enable zoom controls
        webView.getSettings().setSupportZoom(true); // Enable zoom
        webView.getSettings().setBuiltInZoomControls(true); // Show built-in zoom controls
        webView.getSettings().setDisplayZoomControls(false); // Hide zoom control buttons

        // Ensure links open in WebView instead of a browser
        webView.setWebViewClient(new WebViewClient());

        // Load Ken Sarowiwa's portfolio
        webView.loadUrl("https://sarowiwaa.github.io/myportfolio");
    }

    // Handling back button to navigate through WebView history
    @Override
    public void onBackPressed() {
        WebView webView = findViewById(R.id.webView);
        if (webView.canGoBack()) {
            webView.goBack(); // Navigate back within the WebView
        } else {
            super.onBackPressed(); // Exit the app if no more pages to go back to
        }
    }
}
How to Customize
To load a different website, replace the URL in the webView.loadUrl("https://sarowiwaa.github.io/myportfolio") line with your desired URL.
You can enable or disable zoom controls by modifying the lines related to setSupportZoom, setBuiltInZoomControls, and setDisplayZoomControls.
License
This project is open-source and available under the MIT License.
