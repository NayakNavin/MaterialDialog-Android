# Material Dialogs for Android 📱

📱Android Library to implement *animated*, 😍*beautiful*, 🎨*stylish* Material Dialog in android apps easily.

<table style="width:100%">
  <tr>
    <th><b>1. Material Dialog<b></b></th>
    <th>2. Animated Material Dialog</th> 
    <th>3. Bottom Sheet Material Dialog</th>
    <th>4. Animated Bottom Sheet Material Dialog</th>
  </tr>
  <tr>
    <td><img src="GIFs/SimpleMaterialDialog.gif"/></td>
    <td><img src="GIFs/AnimatedMaterialDialog.gif"/></td> 
    <td><img src="GIFs/BottomSheetMaterialDialog.gif"/></td>
    <td><img src="GIFs/AnimatedBottomSheetMaterialDialog.gif"/></td>
  </tr>
</table>


# Table of Contents:
> - [ Introduction ](#introduction)
> - [ Types of Dialog ](#types)
> - [ Implementation ](#implementation)
>    - [ Prerequisite ](#prerequisite)
>    - [ Create Dialog Instance ](#createDialogInstance)
>        - [ Material Dialog ](#createMaterialDialog)
>        - [ Bottom Sheet Material Dialog ](#createBsMaterialDialog)
>    - [ Show Animations ](#showAnims)
>        - [ Using `Resource` File ](#showAnimRes)
>        - [ Using `Asset` File ](#showAnimFile)
>        - [ Getting `LottieAnimationView` ](#getLottieAnimationView)
>    - [ Dialog State Listeners ](#stateCallbacks)
> - [ Credits ](#credits)    

<a name="introduction"></a>
## Introduction
**MaterialDialog** library is built upon Google's Material Design library. This API will be useful to create rich, animated, beautiful dialogs in Android app easily. 
This library implements Airbnb's [*Lottie*](https://github.com/airbnb/lottie-android) library to render After Effects animation in app.
Refer [this](https://airbnb.io/lottie/#/) for Lottie documentation.

<a name="types"></a>
## Types of Dialog
**MaterialDialog** library provides two types of dialog i.e. 

<table style="width:100%">
  <tr>
    <th><b>1. Material Dialog<b></b></th>
    <th>2. Bottom Sheet Material Dialog</th>
  </tr>
  <tr>
    <td>This is basic material dialog which has two material buttons (Same as Android's AlertDialog) as you can see below.</td>
    <td>This is Bottom Sheet material dialog which has two material buttons which is showed from bottom of device as you can see below.</td> 
  </tr>
  <tr>
    <td align="center"><img src="Screenshots/MaterialDialog.png" width="75%"/></td>
    <td align="center"><img src="Screenshots/BottomSheetMaterialDialog.png" width="75%"/></td> 
  </tr>
</table>

<a name="implementation"></a>
## Implementation
Implementation of Material Dialog library is so easy. You can check [/app](/app) directory for demo. Let's have look on basic steps of implementation.
<a name="prerequisite"></a>
### Prerequisite
#### i. Gradle
In `Build.gradle` of app module, include these dependencies. If you want to show animations, include *Lottie* animation library.
```groovy
dependencies {

    // Material Dialog Library
    implementation 'com.shreyaspatil:MaterialDialog:1.0.0'

    // Material Design Library
    implementation 'com.google.android.material:material:1.0.0'

    // Lottie Animation Library
    implementation 'com.airbnb.android:lottie:3.0.6'
}
```
#### ii. Set up Material Theme
Setting Material Theme to app is necessary before implementing Material Dialog library. To set it up, update [`styles.xml`](app\src\main\res\values\styles.xml) of `values` directory in app.
```xml
<resources>
    <style name="AppTheme" parent="Theme.MaterialComponents.Light">
        <!-- Customize your theme here. -->
        ...
    </style>
</resources>
```
These are required prerequisites to implement Material Dialog library.

<a name="createDialogInstance"></a>
### Create Dialog Instance
As there are two types of dialogs in library. Material Dialogs are instantiated as follows.
<a name="createMaterialDialog"></a>
#### i. Material Dialog
`MaterialDialog` class is used to create Material Dialog. Its static `Builder` class is used to instantiate it. After building, to show the dialog, `show()` method of `MaterialDialog` is used.
```java
        MaterialDialog mDialog = new MaterialDialog.Builder(this)
                .setTitle("Delete?")
                .setMessage("Are you sure want to delete this file?")
                .setCancelable(false)
                .setPositiveButton("Delete", R.drawable.ic_delete, new MaterialDialog.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int which) {
                        // Delete Operation
                    }
                })
                .setNegativeButton("Cancel", R.drawable.ic_close, new MaterialDialog.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int which) {
                        dialogInterface.dismiss();
                    }
                })
                .build();

        // Show Dialog
        mDialog.show();
```

<img align="center" src="GIFs/SimpleMaterialDialog.gif" width="300"/>

<a name="createBsMaterialDialog"></a>
#### ii. Bottom Sheet Material Dialog
`BottomSheetMaterialDialog` class is used to create Bottom Sheet Material Dialog. Its static `Builder` class is used to instantiate it. After building, to show the dialog, `show()` method of `BottomSheetMaterialDialog` is used.
```java
        BottomSheetMaterialDialog mBottomSheetDialog = new BottomSheetMaterialDialog.Builder(this)
                .setTitle("Delete?")
                .setMessage("Are you sure want to delete this file?")
                .setCancelable(false)
                .setPositiveButton("Delete", R.drawable.ic_delete, new BottomSheetMaterialDialog.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int which) {
                        Toast.makeText(getApplicationContext(), "Deleted!", Toast.LENGTH_SHORT).show();
                        dialogInterface.dismiss();
                    }
                })
                .setNegativeButton("Cancel", R.drawable.ic_close, new BottomSheetMaterialDialog.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int which) {
                        Toast.makeText(getApplicationContext(), "Cancelled!", Toast.LENGTH_SHORT).show();
                        dialogInterface.dismiss();
                    }
                })
                .build();

        // Show Dialog
        mBottomSheetDialog.show();
```

<img align="center" src="GIFs/BottomSheetMaterialDialog.gif" width="300"/>

<a name="showAnims"></a>
### Show Animations
<table style="width:100%">
  <tr>
    <th>Material Dialog</th> 
    <th>Bottom Sheet Material Dialog</th>
  </tr>
  <tr>
    <td><img src="GIFs/AnimatedMaterialDialog.gif"/></td>
    <td><img src="GIFs/AnimatedBottomSheetMaterialDialog.gif"/></td>
  </tr>
</table>

Animations in this library are implemented using Lottie animation library. You can get free animations files [here](https://lottiefiles.com/). You can find varieties of animation files on [https://lottiefiles.com](https://lottiefiles.com/).
`*.json` file downloaded from *LottieFiles* should be placed in android project. There are two ways to place animation file (`*.json`).

For example, here `delete_anim.json` animation file is used to show file delete animation.
<a name="showAnimRes"></a>
#### i. Using `Resource` File
Downloaded json file should placed in `raw` directory of `res`.

![](Screenshots/ScreenAnimRes.PNG)

In code, `setAnimation()` method of `Builder` is used to set Animation to the dialog.

Prototype :
> setAnimation(int resourceId)

Resource file should be passed to method. e.g. `R.raw.delete_anim`. 
```java
        MaterialButton mDialog = new MaterialDialog.Builder(this)
                // Other Methods to create Dialog........               
                .setAnimation(R.raw.delete_anim)                
                //...
```
<a name="showAnimFile"></a>
#### ii. Using `Asset` File
Downloaded json file should placed in `asset` directory.

![](Screenshots/ScreenAnimAsset.PNG)

In code, `setAnimation()` method of `Builder` is used to set Animation to the dialog.

Prototype:
> setAnimation(String fileName)

**Only** file name ***with extensions*** should passed to method.
```java
        MaterialButton mDialog = new MaterialDialog.Builder(this)
                // Other Methods to create Dialog........               
                .setAnimation("delete_anim.json")               
                //...
```

<a name="getLottieAnimationView"></a>
#### iii. Getting `LottieAnimationView` 
To get `View` of Animation for any operations, there is a method in Material Dialogs which returns `LottieAnimationView` of dialog.
```java
        // Get Animation View
        LottieAnimationView animationView = mDialog.getAnimationView();
        // Do operations on animationView
```

<a name="stateCallbacks"></a>
### Dialog State Listeners 
There are three callback events and listeners for Dialog.

Following are interfaces for implementations:
- `OnShowListener()` - Listens for dialog Show event. Its `onShow()` is invoked when dialog is displayed.
- `OnCancelListener()` - Listens for dialog Cancel event. Its `onCancel()` is invoked when dialog is cancelled.
- `OnDismissListener()` - Listens for dialog Dismiss event. Its `onDismiss()` is dismiss when dialog is dismissed.
```java
       ... 
       mDialog.setOnShowListener(this);
       mDialog.setOnCancelListener(this);
       mDialog.setOnDismissListener(this);
    }
    
    @Override
    public void onShow(DialogInterface dialogInterface) {
        // Dialog is Displayed
    }

    @Override
    public void onCancel(DialogInterface dialogInterface) {
        // Dialog is Cancelled
    }

    @Override
    public void onDismiss(DialogInterface dialogInterface) {
        // Dialog is Dismissed
    }
}
```

<a name="credits"></a>
## Credits
This library is built using following open-source libraries.
- [Material Components for Android](https://github.com/material-components/material-components-android)
- [Lottie for Android](https://github.com/airbnb/lottie-android)

