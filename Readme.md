1º) Criar novo projeto (Empty Activity), minimum API 15 - SDK 28;

2º) Copiar a pasta "assets" dentro da pasta (app/src/main/*) do novo projeto.

3º) Abrir o "build.gradle (Module: app)" e copiar antes de "apply plugin: 'com.android.application'" o seguinte:

buildscript {
    repositories {
    maven { url 'https://plugins.gradle.org/m2/'}
    }
dependencies {
    classpath 'gradle.plugin.com.onesignal:onesignal-gradle-plugin:[0.11.0, 0.99.99]'
    }
}
apply plugin: 'com.onesignal.androidsdk.onesignal-gradle-plugin'

repositories {
maven { url 'https://maven.google.com' }
}


4º) Ainda no "build.gradle", depois de "defaultConfig { applicationId XXX " copiar, alterando o ID do Onesignal:


        manifestPlaceholders = [
                onesignal_app_id: 'XXXXXXXXXXXXXXXX',
                // Project number pulled from dashboard, local value is ignored.
                onesignal_google_project_number: 'REMOTE'
        ]

        minSdkVersion 15
        targetSdkVersion 28
        versionCode XXXXXXXX
        versionName "XXXXXXXXX"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
implementation fileTree(dir: 'libs', include: ['*.jar'])
implementation 'com.android.support:appcompat-v7:28.0.0'
implementation 'com.android.support.constraint:constraint-layout:1.1.3'
testImplementation 'junit:junit:4.12'
androidTestImplementation 'com.android.support.test:runner:1.0.2'
androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'

    implementation 'com.onesignal:OneSignal:[3.9.1, 3.99.99]'

    implementation 'com.google.android.gms:play-services-location:15.0.1'
}


5º) Sempre verificar a "version Code" e a "version Name" nas atualizações.


6º) Dar um "Sync Now" para atualizar as novas dependências.


7º) Abrir o java "MainActivity" e copiar o seguinte à partir do nome do pacote "package XX.XXX.XXXXXX;" :

import android.content.Intent;
import android.graphics.Bitmap;
import android.net.Uri;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.webkit.WebChromeClient;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import android.widget.ProgressBar;

public class MainActivity extends AppCompatActivity {

    private ProgressBar spinner;
    WebView webView;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        webView = (WebView) findViewById(R.id.webView);
        spinner =  findViewById(R.id.progressBar1);
        webView.getSettings().setJavaScriptEnabled(true);
        webView.getSettings().setAppCacheEnabled(true);
        webView.getSettings().setDomStorageEnabled(true);
        webView.getSettings().setAppCacheMaxSize(1024*1024*8);
        webView.getSettings().setAppCachePath("/data/data/"+ getPackageName() +"/cache");
        webView.getSettings().setAllowFileAccess(true);
        webView.getSettings().setAppCacheEnabled(true);
        webView.getSettings().setCacheMode(WebSettings.LOAD_DEFAULT);
        webView.loadUrl("https://pratorapido.com/app/");
        webView.setWebChromeClient(new WebChromeClient());
        webView.setWebViewClient(new WebViewClient(){

            @Override
            public void onPageStarted(WebView webview, String url, Bitmap favicon) {
                webview.setVisibility(webview.INVISIBLE);
            }

            @Override
            public void onPageFinished(WebView view, String url) {

                spinner.setVisibility(View.GONE);

                view.setVisibility(webView.VISIBLE);
                super.onPageFinished(view, url);

            }

            @Override
            public boolean shouldOverrideUrlLoading(WebView view, String url) {
                if( url.startsWith("http://pratorapido.com/") || url.startsWith("https://pratorapido.com/") || url.startsWith("https://www.foodbooking.com/") || url.startsWith("https://www.fbgcdn.com/") ) {
                    return false;
                }

                Intent intent = new Intent(Intent.ACTION_VIEW);
                intent.setData(Uri.parse(url));
                startActivity(intent);
                return true;
            }

            public void onReceivedError(WebView view, int errorCode, String description, String failingUrl) {

                webView.loadUrl("file:///android_asset/error.html");

            }
        });
    }

    @Override
    public void onBackPressed(){

        if (webView.canGoBack()){
            webView.goBack();
        }else {
            finish();
        }
    }
}


8º) Abrir o Layout "activity_main.xml" e copiar (*****carece atualização posterior):

<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical"
android:background="#ffffff"
tools:context=".MainActivity">

    <WebView
        android:id="@+id/webView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/colorBg"

        />

    <ProgressBar
        android:id="@+id/progressBar1"
        android:layout_width="120dp"
        android:layout_height="120dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:indeterminate="true"

        />


</android.support.constraint.ConstraintLayout>

*****Background vai dar como desconhecido.


9º) No value "colors.xml" copiar todo esse conteudo:

<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="colorPrimary">#474747</color>
    <color name="colorPrimaryDark">#000000</color>
    <color name="colorAccent">#787878</color>
    <color name="colorBg">#FFFFFF</color>
</resources>


10º) Adicionar no value "strings.xml" as seguintes strings:

    <string name="logosplash">LogoSplash</string>
    <string name="copyright">Copyright</string>


11º) No value "styles.xml" copiar do AppTheme:

<style name="AppTheme" parent="Theme.AppCompat.NoActionBar">


12º) Copiar para pasta "Drawable" os arquivos de imagem: logoicone192, logosplash512, copyrirght - Não pode salvar nome com letra maiúscula (Max de 512px PNG).


13º) Criar uma "EmptyActivity" chamada "SplashActivity" e copiar (no seu Java) abaixo do nome do pacote, o seguinte:

import android.content.Intent;
import android.os.Handler;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class SplashActivity extends AppCompatActivity {

    private static int SPLASH_TIME_OUT = 4000;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_splash);
        new Handler().postDelayed(new Runnable() {
            @Override
            public void run() {
                Intent homeIntent = new Intent(SplashActivity.this, MainActivity.class);
                startActivity(homeIntent);
                finish();
            }

        },SPLASH_TIME_OUT);

    }
}


14º) Abrir o layout "activity_splash.xml" e copiar o seguinte:

<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#ffffff"
    android:orientation="vertical"
    tools:context=".SplashActivity">

    <ImageView
        android:id="@+id/logosplash"
        android:layout_width="250dp"
        android:layout_height="250dp"
        android:contentDescription="@string/logosplash"
        android:src="@drawable/logosplash512"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:ignore="MissingConstraints" />

    <ImageView
        android:id="@+id/copyright"
        android:layout_width="200dp"
        android:layout_height="80dp"
        android:layout_marginBottom="30dp"
        android:contentDescription="@string/copyright"
        android:src="@drawable/copyright"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        tools:ignore="MissingConstraints" />

</android.support.constraint.ConstraintLayout>


15º) Editar "AndroidManifest.xml" - Copiar permissões logo abaixo do nome do pacote:

    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>


16º) Adicionar icones no "AndroidManifest" nos campos "android:icon" e "android:roundIcon" fazer referencia ao "@drawable/*".


17º) Ainda no Manifest, copiar logo abaixo de "android:theme="@style/AppTheme":

android:name=".ApplicationClass">
        <activity android:name=".SplashActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity android:name=".MainActivity"></activity>
    </application>


18º) Criar a class ".ApplicationClass" e copiar o seguinte logo abaixo do nome do pacote:

import android.app.Application;

import com.onesignal.OneSignal;

public class ApplicationClass extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        // OneSignal Initialization
        OneSignal.startInit(this)
                .inFocusDisplaying(OneSignal.OSInFocusDisplayOption.Notification)
                .unsubscribeWhenNotificationsAreDisabled(true)
                .init();
    }
}


19) Dar um Clean Project e depois um Rebuild Project

20) Gerar APk Assinado

21) Chave "pratorapido" para os apps do site