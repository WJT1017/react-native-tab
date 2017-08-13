# react-native-tab
RN中的选项卡

Skip to content
This repository

    Pull requests
    Issues
    Marketplace
    Gist

    @WJT1017

25
906

    160

crazycodeboy/react-native-splash-screen
Code
Issues 45
Pull requests 3
Projects 0
Wiki
react-native-splash-screen/README.md
dcee9e1 on 31 May
vjph贾鹏辉 publish v2.1.0
@crazycodeboy
@Jacse
@fenderrex
@haikyuu
237 lines (162 sloc) 7.92 KB
react-native-splash-screen

Download PRs Welcome react-native-splash-screen release 语言 中文 License MIT 原理 解析

A splash screen API for react-native which can programatically hide and show the splash screen. Works on iOS and Android.
Content

    Installation
    Examples
    Getting started
    API
    Contribution
    Changes

Changes

For React Native >= 4.0 use v2.+, for React Native < 4.0 use v1.0.9
Examples

    Examples

react-native-splash-screen-Android react-native-splash-screen-iOS
Installation
First step(Download):

Run npm i react-native-splash-screen --save
Second step(Plugin Installation):
Automatic installation

react-native link react-native-splash-screen or rnpm link react-native-splash-screen
Manual installation

Android:

    In your android/settings.gradle file, make the following additions:

include ':react-native-splash-screen'   
project(':react-native-splash-screen').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-splash-screen/android')

    In your android/app/build.gradle file, add the :react-native-splash-screen project as a compile-time dependency:

...
dependencies {
    ...
    compile project(':react-native-splash-screen')
}

    Update the MainApplication.java file to use react-native-splash-screen via the following changes:

import com.cboy.rn.splashscreen.SplashScreenReactPackage;
public class MainApplication extends Application implements ReactApplication {

    private final ReactNativeHost mReactNativeHost = new ReactNativeHost(this) {
        @Override
        protected boolean getUseDeveloperSupport() {
            return BuildConfig.DEBUG;
        }

        @Override
        protected List<ReactPackage> getPackages() {
            return Arrays.<ReactPackage>asList(
                    new MainReactPackage(),
            new SplashScreenReactPackage()  //here
            );
        }
    };

    @Override
    public ReactNativeHost getReactNativeHost() {
        return mReactNativeHost;
    }
}

iOS:

    In XCode, in the project navigator, right click Libraries ➜ Add Files to [your project's name]

    Go to node_modules ➜ react-native-splash-screen and add SplashScreen.xcodeproj

    In XCode, in the project navigator, select your project. Add libSplashScreen.a to your project's Build Phases ➜ Link Binary With Libraries

    To fix 'SplashScreen.h' file not found, you have to select your project → Build Settings → Search Paths → Header Search Paths to add:

    $(SRCROOT)/../node_modules/react-native-splash-screen/ios

Third step(Plugin Configuration):

Android:

Update the MainActivity.java to use react-native-splash-screen via the following changes:

import android.os.Bundle;
import com.facebook.react.ReactActivity;
import com.cboy.rn.splashscreen.SplashScreen; // here

public class MainActivity extends ReactActivity {
   @Override
    protected void onCreate(Bundle savedInstanceState) {
        SplashScreen.show(this);  // here
        super.onCreate(savedInstanceState);
    }
    // ...other code
}

iOS:

Update AppDelegate.m with the following additions:

#import "AppDelegate.h"
#import "RCTRootView.h"
#import "SplashScreen.h"  // here

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // ...other code

    [SplashScreen show];  // here
    return YES;
}

@end

Getting started

Import react-native-splash-screen in your JS file.

import SplashScreen from 'react-native-splash-screen'
Android:

Create a file called launch_screen.xml in app/src/main/res/layout (create the layout-folder if it doesn't exist). The contents of the file should be the following:

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@drawable/launch_screen">
</LinearLayout>

Customize your launch screen by creating a launch_screen.png-file and placing it in an appropriate drawable-folder. Android automatically scales drawable, so you do not necessarily need to provide images for all phone densities. You can create splash screens in the following folders:

    drawable-ldpi
    drawable-mdpi
    drawable-hdpi
    drawable-xhdpi
    drawable-xxhdpi
    drawable-xxxhdpi

Optional steps：

If you want the splash screen to be transparent, follow these steps.

Open android/app/src/main/res/values/styles.xml and add <item name="android:windowIsTranslucent">true</item> to the file. It should look like this:

<resources>
    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <!-- Customize your theme here. -->
        <!--设置透明背景-->
        <item name="android:windowIsTranslucent">true</item>
    </style>
</resources>

To learn more see examples
iOS

Customize your splash screen via LaunchImage or LaunchScreen.xib,

Learn more to see examples
Usage

Use like so:

import SplashScreen from 'react-native-splash-screen'

export default class WelcomePage extends Component {

    componentDidMount() {
    	// do stuff while splash screen is shown
        // After having done stuff (such as async tasks) hide the splash screen
        SplashScreen.hide();
    }
}

API
Method 	Type 	Optional 	Description
show() 	function 	false 	Open splash screen (Native Method )
hide() 	function 	false 	Close splash screen
Contribution

Issues are welcome. Please add a screenshot of you bug and a code snippet. Quickest way to solve issue is to reproduce it in one of the examples.

Pull requests are welcome. If you want to change the API or do something big it is best to create an issue and discuss it first.

MIT Licensed

    Contact GitHub API Training Shop Blog About 

    © 2017 GitHub, Inc. Terms Privacy Security Status Help 

