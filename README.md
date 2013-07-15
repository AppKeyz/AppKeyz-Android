AppKeyz SDK for Android
============

This SDK is designed to allow a developer to easily add either the AppKeyz API by itself, or a suite also containing a "drop-in" authentication module.

This repository is a sample app that demonstrates all API calls as well as the authentication. Authentication module works on Android Device & Tablet in either landscape or potrait.

The AppKeyz SDK requires Android 2.1+

Installation
------------

Installation consists of two different levels of SDK integration. One level contains just the API calls library, and the other also includes the authentication module.

###Installing ONLY the API Library
------
Add AppKeyz.java to your <Application Name>- AndroidManifest.xml file:

```.java
#ifdef __OBJC__
    import "AKUser.java"
    import "AppKeyz.java
    import "AppUtils.java"
    import "AppkeysActivity.java" 
#endif
```

Add the 'AppKeyz' directory into your Eclipse project.

In the AppKeyz.java file, replace the sample token (on line 10) with your app token. The included token is not for production and will only work with this sample app.

```.Java
String APP_TOKEN == "ci48xk6m"; //REPLACE WITH YOUR APP TOKEN
```


### Installing the AppKeyz Suite with authentication module
------

Add AppKeyz.java, AKUser.java, AppUtils.java to your <Application Name>-AndroidManifest.xml file:

```.java
#ifdef __OBJC__
    import "AppUtils.java"
    import "AKUser.java"
    import "AppKeyz.java"
    import "AppkeyzActivity.java"
#endif
```

Add the 'AppKeyz.java','AppUtils.java','AppKeyActivity.jave' directories into your Eclipse project.

In the AppKeyz.java file, replace the sample token (on line 10) with your app token. The included token is not for production and will only work with this sample app.

```.java
String APP_TOKEN == "ci48xk6m"; //REPLACE WITH YOUR APP TOKEN
```

In order to use the authentication module, add this code inside the 'viewDidLoad' method of your first view controller:

''' java
String firstName, lastName, sex, age, email_Id,
String BASE_URL = "https://www.appkeyz.com/mobileapp/appkeyzapi/";`

The 'setRegisterFields' method sets optional registeration fields (Age, Gender and six custom fields). The method is required but can be set as an empty array:


```Java
AppUtils setRegisterFields :String[] arrayWithObjects(null);
```

###Using the AppKeyz API Library only
------

The AppKeyz library is setup as a singleton, so you can call the API from your Activity like so:

```java
paramMap.put("apiaction", "createuser");
  			paramMap.put("apptoken",AppUtils.APP_TOKEN);
				paramMap.put("email", email.getText().toString());
				paramMap.put("password",password.getText().toString());```

You can capture callbacks from the API inside 'consumeResponse':

`java'
case readpurchase:
    switch (rspCode) {
        case 0:
            message = null;
            response paramMap("productsku");
 //String
            response paramMap("purchaseprice"); //float
           
            response  paramMap("purchasedate"); //String 2013-01-01 format
            response paramMap("consumableid");
 //String
            break;
        case 1:
            //Bad Parameters.  Usually means you're missing apiaction or apptoken
            break;
        case 2:
            //This Email does not does exist in our system, please Register or log in using a different email
            break;
        case 4:
            //Invalid Purchase
            break;
    }
    break;
```

####A Note about AlertViews:
In the consumeResponse method, each command has a place for the developer to capture returned values (in the case of rspCode==0) and set AlertView messages. By default, you must set the success message (0). The server returns it's own message for rspCode==1,2,3,4,5 of 100. Feel free to set your own message. You may set 'message' to nil to prevent the AlertView from showing at all.

The sample app shows an example of each API call in AppKeyzActivity.java and the output of each call can be seen in the Eclipse log files.


And subscribe to intent notifications in your Activity. For example:

```java
Intent intent = new Intent();
   intent.setClass(AppKeyzActivity.this, AnotherActivity.class);
   startActivity(intent);
```

More detail can be found about each API call in the wiki article on <a href="https://github.com/AppKeyz/app-keyz-Android/wiki/AppKeyz-API-Library">using the AppKeyz API library</a>. Also a detailed explaination of each API call can be found in the AppKeyz_Client_SDK_v2.0_0504.doc file in the root directory.

#### Note: if you wish to use the AppKeyz login API, you can use the AKUser model, found in the AppKeyzSuite directory, or remove the assignments inside 'consumeUser'.



###Using the AppKeyz Suite
------

The AppKeyz suite works in combination with the AppKeyz API Library mentioned in the above section.

If you follow the setup steps, your activity will present a set of 'login or register' screens that will capture login or register details from the user and register them with the AppKeyz server, then save the details to an AKUser singleton. You may use the stock AKUser model and customize it, or replace with your own user model. Note that you'll need to replace AKUser methods in AppKeyz.java and Loginscreen.java.

The login screen will work for any Android device and CAN rotate to any orientation. However, it is recommended that the screens only be used in one orientation, as the background image will distort when the screen rotates.

#### Note: We've recently added an alertview to popup if a user isn't already registered or logged in, to give the user a chance to login or register before a potential purchase. You may choose whether or not to use it. It can simply be removed from createPurchase.

------
This document &copy; 2013 AppKeyz, Inc.
