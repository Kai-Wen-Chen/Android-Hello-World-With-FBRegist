# Hello-World-With-FBRegist
FB登入功能with login button

1.至build.gradle(Module.app)
1-1.在dependencies{...}前 加入repositories{ mavenCentral() }
1-2.在dependencies內加入compile 'com.facebook.android:facebook-android-sdk:4.+'

2.至Manifest
2-1.加入<uses-permission android:name="android.permission.INTERNET"/> 取得網路
2-2.在<application ... />內加入<meta-data android:name="com.facebook.sdk.ApplicationId" android:value= "465068090367579" />
    此為加入該APP的ID
    2-2-1.APP的ID需去FB申請
    2-2-2.申請時需要自己開發環境的hash key
      2-2-2-1.安裝openssl至與keystore相同地方的資料夾
      2-2-2-2.於該資料夾用cmd 指令: keytool -exportcert -alias androiddebugkey -keystore %HOMEPATH%\.android\debug.keystore | openssl sha1 -binary | openssl base64 (Windows專用) 即可取得hash key
2-3.在<application ... />內加入<activity android:name="com.facebook.FacebookActivity"
            android:configChanges=
                "keyboard|keyboardHidden|screenLayout|screenSize|orientation"
            android:theme="@android:style/Theme.Translucent.NoTitleBar"
            android:label="@string/app_name" />
    此為取得登入畫面的相關控制(即登入的"活動")

3.至string.xml
3-1.加入<string name="facebook_app_id">465068090367579</string>同樣是加入APP的ID

4.至activity_main.xml
4-1.加入<com.facebook.login.widget.LoginButton
        android:id="@+id/login_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="30dp"
        android:layout_marginBottom="30dp" />
    此為定義FB的登入按鈕

5.至MainActivity
5-1.如程式碼顯示，先初始化FB的SDK，當申請登入發送後(按下登入按鈕)，由CallbackManager負責之間的管理
5-2.如果登入成功後，記錄accessToken(當前存取狀態)
5-3.用GraphRequest來定義你想要獲得的FB資料(如姓名、網頁連結、ID等)，資料以JSON的形式傳回
