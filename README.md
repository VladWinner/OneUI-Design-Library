[![](https://img.shields.io/github/v/release/Yanndroid/SamsungOneUi?color=%235555ff)](https://github.com/Yanndroid/SamsungOneUi/releases)
[![](https://img.shields.io/static/v1?label=sample&message=apk&color=yellow)](https://github.com/Yanndroid/SamsungOneUi/raw/master/app/release/app-release.apk)
![](https://img.shields.io/github/last-commit/Yanndroid/SamsungOneUi)
[![](https://img.shields.io/github/issues-raw/Yanndroid/SamsungOneUi?color=%23ff4400)](https://github.com/Yanndroid/SamsungOneUi/issues)
[![](https://img.shields.io/github/issues-pr-raw/Yanndroid/SamsungOneUi?color=%23bb00bb)](https://github.com/Yanndroid/SamsungOneUi/pulls)
[![](https://img.shields.io/github/forks/Yanndroid/SamsungOneUi?color=%2300bbbb)](https://github.com/Yanndroid/SamsungOneUi/network/members)
[![](https://img.shields.io/github/contributors/Yanndroid/SamsungOneUi)](https://github.com/Yanndroid/SamsungOneUi/graphs/contributors)
[![](https://img.shields.io/static/v1?label=telegram&message=Yanndroid&color=blue)](https://t.me/Yanndroid)

# Samsung OneUi Design
A library for Android, which makes your app look like Samsung's OneUI. In this library there is a theme which will apply for each View (see [Progress](#Progress)) in your layout. This library has been tested in AndroidStudio, but should work in other IDEs too. You can try out the latest example [here](https://github.com/Yanndroid/SamsungOneUi/raw/master/app/release/app-release.apk).

Excuse my bad english, feel free to correct it. :)


- [Screenshots](#Screenshots)
- [Installation](#Installation)
- [Usage](#Usage)
  - [DrawerLayout](#DrawerLayout)
  - [ToolbarLayout](#ToolbarLayout)
  - [OptionButton and OptionGroup](#OptionButton-and-OptionGroup)
  - [DrawerDivider](#DrawerDivider)
  - [SplashViewSimple](#SplashViewSimple)
  - [SplashViewAnimated](#SplashViewAnimated)
  - [SwitchBar](#SwitchBar)
  - [SeekBar](#SeekBar)
  - [ProgressBar](#ProgressBar)
  - [Button](#Button)
  - [ColorPickerDialog](#ColorPickerDialog)
  - [Icons](#Icons)
  - [Color theme](#Color-theme)
    - [Entire App](#1.-Entire-App)
    - [Single/Multiple activities](#2.-Single/Multiple-activities)
    - [Via Code](#3.-Via-Code)
  - [App Icon](#App-Icon)
- [Progress](#Progress)


## Screenshots
<img src="readme-resources/screenshots/screenshot_1.png"  width="150"/> <img src="readme-resources/screenshots/screenshot_2.png"  width="150"/> <img src="readme-resources/screenshots/screenshot_3.png"  width="150"/> <img src="readme-resources/screenshots/splash_simple.png"  width="150"/> <img src="readme-resources/screenshots/splash_animated.gif"  width="150"/>
<img src="readme-resources/screenshots/seekbar.gif"  width="300"/>
<img src="readme-resources/screenshots/progressbar.gif"  width="300"/>
<img src="readme-resources/screenshots/switchbar.gif"  width="300"/>


## Installation
### with [Jitpack](https://jitpack.io/#Yanndroid/SamsungOneUi):
1. Add jitpack to build.gradle (Project: ...)
```gradle
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
	}
}
```
2. Add the dependency to build.gradle (Module: ...)
```gradle
dependencies {
	implementation 'com.github.Yanndroid:SamsungOneUi:1.1.3'
    ...
}
```
3. Apply the theme in AndroidManifest.xml
```xml
<application
    ...
    android:theme="@style/SamsungTheme"
    >
    ...
</application>
```


### with Github Packages:
1. Create a [new token](https://github.com/settings/tokens) with ```read:packages``` permission.
2. Add the dependency to build.gradle (Module: ...)
```gradle
repositories {
    maven {
        url = uri("https://maven.pkg.github.com/yanndroid/SamsungOneUi")
            credentials {
                username = "your username"
                password = "your token"
            }
    }
}


dependencies {
    implementation 'de.dlyt.yanndroid:samsung:1.1.3'
    ...
}
```

3. Apply the theme in AndroidManifest.xml
```xml
<application
    ...
    android:theme="@style/SamsungTheme"
    >
    ...
</application>
```

## Usage
### DrawerLayout
"Ready-to-go" DrawerLayout with collapsing toolbar.
```xml
<de.dlyt.yanndroid.samsung.layout.DrawerLayout 
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:drawer_icon="..."
    app:drawer_viewId="@id/viewindrawer"
    app:toolbar_subtitle="..."
    app:toolbar_title="...">

    <View
        android:id="@+id/viewindrawer"
        ... />

    <!--other views-->

</de.dlyt.yanndroid.samsung.layout.DrawerLayout>

```
The view with the ID specified in ```app:drawer_viewId="..."``` will be shown in the drawer and the rest of the children on the main screen.  

```app:toolbar_title="..."``` and ```app:toolbar_subtitle="..."``` are setting the title and subtitle in the toolbar. If nothing is set for the subtitle, the toolbar will adjust the title position to match the space.  

The drawable in ```app:drawer_icon="..."``` is the little icon at the top right in the drawer pane. There are already some stock Samsung [icons](#Icons) included in the library.  

If you want the toolbar collapsing when you scroll the content you should either use a [NestedScrollView](https://developer.android.com/reference/androidx/core/widget/NestedScrollView) as view child or set ```android:nestedScrollingEnabled="true"``` on the view you want the toolbar to collapse on scroll.

#### Methods
Return the toolbar, useful for ```setSupportActionBar()```.
```java
public Toolbar getToolbar()
```
OnClickListener for the DrawerIcon (the icon in the top right corner of the drawer pane).
```java
public void setDrawerIconOnClickListener(OnClickListener listener)
```
Set the title of the toolbar.
```java
public void setToolbarTitle(String title)
```
Set the subtitle of the toolbar.
```java
public void setToolbarSubtitle(String subtitle)
```
Expand or collapse the toolbar with an optional animation.
```java
public void setToolbarExpanded(boolean expanded, boolean animate)
```
Show/hide the badges on the DrawerIcon and NavigationIcon.
```java
public void showIconNotification(boolean navigationIcon, boolean drawerIcon)
```
Open/close the drawer pane with an optional animation.
```java
public void setDrawerOpen(Boolean open, Boolean animate)
```

### ToolbarLayout
Basically the same as [DrawerLayout](#DrawerLayout) but without the drawer.
```xml
<de.dlyt.yanndroid.samsung.layout.ToolbarLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:title="..."
    app:subtitle="..."
    app:navigationIcon="..."
    >

    <!--children-->

</de.dlyt.yanndroid.samsung.layout.ToolbarLayout>
```
```app:navigationIcon="..."``` is the NavigationIcon of the toolbar. There are already some stock Samsung [icons](#Icons) included in the library, like a drawer and back icon.  

Same as the [DrawerLayout](#DrawerLayout) you need to use a [NestedScrollView](https://developer.android.com/reference/androidx/core/widget/NestedScrollView) or ```android:nestedScrollingEnabled="true"```.

#### Methods
Return the toolbar, useful for ```setSupportActionBar()```.
```java
public Toolbar getToolbar()
```
Set the title of the toolbar.
```java
public void setTitle(String title)
```
Set the subtitle of the toolbar.
```java
public void setSubtitle(String subtitle)
```
Expand or collapse the toolbar with an optional animation.
```java
public void setExpanded(boolean expanded, boolean animate)
```
Clicklistener for the NavigationIcon (Back icon).
```java
public void setNavigationOnClickListener(OnClickListener listener)
```
Show/hide the badges on the NavigationIcon.
```java
public void showNavIconNotification(boolean showNotification)
```
Set a drawable for the NavigationIcon.
```java
public void setNavigationIcon(Drawable navigationIcon)
```

### OptionButton and OptionGroup
todo

### DrawerDivider
A divider between to options on the drawer. It's the same divider you can find in almost any Samsung app drawer.

<img src="readme-resources/screenshots/drawerdivider.png"  width="260"/>

```xml
<de.dlyt.yanndroid.samsung.drawer.Divider
    android:layout_width="match_parent"
    android:layout_height="4dp"
    android:layout_marginHorizontal="24dp"
    android:layout_marginVertical="2dp" />
```
Alternatively you could use this, it's easier and all set but less customizable:
```xml
<View style="@style/DrawerDividerStyle" />
```

### SplashViewSimple
Simple Splash view. (I think Samsung removed the splashscreen of their apps since OneUI 3 but in former times it was still there.)

<img src="readme-resources/screenshots/splash_simple.png"  width="150"/>

```xml
<de.dlyt.yanndroid.samsung.layout.SplashViewSimple
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:image="..."
    app:text="..." />
```
```app:image="..."```is the icon and ```app:text="..."``` the text underneath the icon.

#### Methods
```java
public void setImage(Drawable mImage)
```
Sets the icon drawable
```java
public void setText(String mText)
```
Sets the text of the splash textview
```java
public String getText()
```
Returns the text of the splash textview

### SplashViewAnimated
An animated splash screen view like the one in the GalaxyStore.

<img src="readme-resources/screenshots/splash_animated.gif"  width="150"/>

```xml
<de.dlyt.yanndroid.samsung.layout.SplashViewAnimated
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:background_image="..."
    app:foreground_image="..."
    app:text="..." />
```

```app:background_image="..."``` only the background of your icon and ```app:foreground_image="..."``` only the foreground, which will have a shake animation.
```app:text="..."``` will be the text under the icon. It has a very similar font and color as the GalaxyStore splash text.

#### Methods
```java
public void setImage(Drawable foreground, Drawable background)
```
Sets the icon fore- and background
```java
public void setText(String mText)
```
Sets the text of the splash textview
```java
public String getText()
```
Returns the text of the splash textview
```java
public void startSplashAnimation()
```
Starts the shake animation of the foreground
```java
public void clearSplashAnimation()
```
Clears the animation
```java
public void setSplashAnimationListener(Animation.AnimationListener listener)
```
Listener for the splash animation


### SwitchBar
A SwitchBar like in the wifi or bluetooth settings.

<img src="readme-resources/screenshots/switchbar.gif"  width="300"/>

```xml
<de.dlyt.yanndroid.samsung.SwitchBar
    android:layout_width="match_parent"
    android:layout_height="wrap_content" />
```
#### Methods
On and Off text of the Switchbar.
```java
public void setSwitchBarText(int i, int i2)
```
Enable and disable the Switchbar.
```java
public void setEnabled(boolean z)
```
Visibility of the ProgressBar in the Switchbar.
```java
public void setProgressBarVisible(boolean z)
```
Switchbar Listener.
```java
public void addOnSwitchChangeListener(OnSwitchChangeListener onSwitchChangeListener)
```

### SeekBar
A Seekbar like the brightness slider in the QS.

<img src="readme-resources/screenshots/seekbar.gif"  width="300"/>

```xml
<de.dlyt.yanndroid.samsung.SeekBar
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:seslSeekBarMode="expand" />
```
:warning: You might need to set a vertical margin, in case the seekbar thumb is cut of.

If you don't want the expanding seekbar, you can use the default seekbar instead of ```de.dlyt.yanndroid.samsung.SeekBar```, as the style will also apply on the default one.

#### Methods
Set a warning at progress i.
```java
public void setOverlapPointForDualColor(int i)
```
Other methodes are the same as the normal [Seekbar](https://developer.android.com/reference/android/widget/SeekBar).

### ProgressBar
The theme won't apply for the ProgressBar, so you need to set it manually:

<img src="readme-resources/screenshots/progressbar.gif"  width="300"/>

```style="@style/ProgressBarStyle.Horizontal"```  
```style="@style/ProgressBarStyle.Horizontal.Large"```  
```style="@style/ProgressBarStyle.Circle.Large"```  
```style="@style/ProgressBarStyle.Circle"```  
```style="@style/ProgressBarStyle.Circle.Small"```  
```style="@style/ProgressBarStyle.Circle.Title"```

### Button
<img src="readme-resources/screenshots/button.png"  width="300"/>

The first style is applied by default. The other two can be used with ```style="@style/ButtonStyle.Invert"``` and ```style="@style/ButtonStyle.Invert.Secondary"```.

### ColorPickerDialog
A color picker dialog like in Samsung Notes.

<img src="readme-resources/screenshots/colorpicker_1.png"  width="200"/> <img src="readme-resources/screenshots/colorpicker_2.png"  width="200"/>

Create dialog with mode (1 = Spectrum, 2 = Swatches) and fArr (starting color).
```java
public ColorPickerDialog(Context context, int mode, float[] fArr)
public ColorPickerDialog(Context context, float[] fArr)
```
Show the dialog.
```java
public void show()
```
Dismiss the dialog.
```java
public void dismiss()
```
Close the dialog.
```java
public void close()
```
Listener when "Done" is pressed.
```java
public void setColorPickerChangeListener(ColorPickerChangedListener colorPickerChangedListener)
```
Example:
```java
float[] scolor = new float[3];
Color.colorToHSV(Color.parseColor("#0381fe5"), scolor);

ColorPickerDialog mColorPickerDialog = new ColorPickerDialog(this, scolor);
mColorPickerDialog.setColorPickerChangeListener(new ColorPickerDialog.ColorPickerChangedListener() {
    @Override
    public void onColorChanged(int i, float[] fArr) {
        
    }

    @Override
    public void onViewModeChanged(int i) {

    }
});
mColorPickerDialog.show();
```

### Icons
There are also some of the stock icons you can find in Samsung apps included in this library, and I will add more over time. You can use them with ```@drawable/ic_samsung_...``` and ```R.drawable.ic_samsung_...```.

<img src="readme-resources/screenshots/icons.png"  width="350"/>

<details>
<summary>See the icon list</summary>
<p>

```ic_samsung_arrow_down```  
```ic_samsung_arrow_left```  
```ic_samsung_arrow_right```  
```ic_samsung_arrow_up```  
```ic_samsung_attach```  
```ic_samsung_audio```  
```ic_samsung_back```  
```ic_samsung_book```  
```ic_samsung_bookmark```  
```ic_samsung_brush```  
```ic_samsung_camera```  
```ic_samsung_close```  
```ic_samsung_convert```  
```ic_samsung_copy```  
```ic_samsung_delete```  
```ic_samsung_document```  
```ic_samsung_download```  
```ic_samsung_drawer```  
```ic_samsung_edit```  
```ic_samsung_equalizer```  
```ic_samsung_favorite```  
```ic_samsung_group```  
```ic_samsung_help```  
```ic_samsung_image```  
```ic_samsung_image_2```  
```ic_samsung_import```  
```ic_samsung_info```  
```ic_samsung_keyboard```  
```ic_samsung_lock```  
```ic_samsung_mail```  
```ic_samsung_maximize```  
```ic_samsung_minimize```  
```ic_samsung_minus```  
```ic_samsung_more```  
```ic_samsung_move```  
```ic_samsung_mute```  
```ic_samsung_page```  
```ic_samsung_pause```  
```ic_samsung_pdf```  
```ic_samsung_pen```  
```ic_samsung_pen_calligraphy```  
```ic_samsung_pen_calligraphy_brush```  
```ic_samsung_pen_eraser```  
```ic_samsung_pen_fountain```  
```ic_samsung_pen_marker```  
```ic_samsung_pen_marker_round```  
```ic_samsung_pen_pencil```  
```ic_samsung_play```  
```ic_samsung_plus```  
```ic_samsung_rectify```  
```ic_samsung_redo```  
```ic_samsung_remind```  
```ic_samsung_rename```  
```ic_samsung_reorder```  
```ic_samsung_restore```  
```ic_samsung_save```  
```ic_samsung_scan```  
```ic_samsung_search```  
```ic_samsung_selected```  
```ic_samsung_send```  
```ic_samsung_settings```  
```ic_samsung_share```  
```ic_samsung_shuffle```  
```ic_samsung_smart_view```  
```ic_samsung_stop```  
```ic_samsung_tag```  
```ic_samsung_text```  
```ic_samsung_text_2```  
```ic_samsung_time```  
```ic_samsung_undo```  
```ic_samsung_unlock```  
```ic_samsung_voice```  
```ic_samsung_volume```  
```ic_samsung_warning```  
```ic_samsung_web_search.xml```  

</p>
</details>
&nbsp;

### Color theme
The default color of the style is the same blue as Samsung (see [Screenshots](#Screenshots)). But like Samsung has different colors for different apps, you too can use other colors which will apply on the entire App and even on the [App Icon](#App-Icon). In this library there are there are three different ways to do that and all three can be used simultaneously:

#### 1. Entire App
This methode will apply the color theme on the entire app and on the app icon. You need to add these three colors in your ```colors.xml``` :
```xml
<color name="primary_color">...</color>
<color name="secondary_color">...</color>
<color name="primary_dark_color">...</color>
```
These colors should have approximately the same color but with a different brightness. ```secondary_color``` the brightest, then ```primary_color``` and the darkest ```primary_dark_color```.  

Here are some presets (if you want I can make more):
- ![#f3a425](https://via.placeholder.com/12/f3a425/000000?text=+) Yellow like MyFiles App (also used in [FreshHub](https://github.com/Yanndroid/FreshHub)):
```xml
<color name="primary_color">#fff3a425</color>
<color name="secondary_color">#ffffb949</color>
<color name="primary_dark_color">#ffbd7800</color>
```

- ![#008577](https://via.placeholder.com/12/008577/000000?text=+) Dark green like Calendar App:
```xml
<color name="primary_color">#ff008577</color>
<color name="secondary_color">#ff009e7c</color>
<color name="primary_dark_color">#ff00574b</color>
```

- ![#68b31a](https://via.placeholder.com/12/68b31a/000000?text=+) Light green like Calculator App:
```xml
<color name="primary_color">#ff68b31a</color>
<color name="secondary_color">#ff7fa87f</color>
<color name="primary_dark_color">#ff569415</color>
```

- ![#ff034A](https://via.placeholder.com/12/ff034A/000000?text=+) Light red which I personally like:
```xml
<color name="primary_color">#ffff034a</color>
<color name="secondary_color">#ffff3d67</color>
<color name="primary_dark_color">#ffde0043</color>
```

#### 2. Single/Multiple activities
If you want to use different colors for a single (or multiple, but not all) activities, this is also possible. The difference here is that this will only apply for the activities you want. Add the three colors (see [Entire App](#1.-Entire-App)) in a theme in ```themes.xml```:

```xml
<style name="ThemeName" parent="SamsungTheme">
    <item name="colorPrimary">#fff3a425</item>
    <item name="colorSecondary">#ffffb949</item>
    <item name="colorPrimaryDark">#ffbd7800</item>
</style>
```
Then apply it on the activities you want with ```android:theme="@style/ThemeName"``` in ```AndroidManifest.xml```.

#### 3. Via Code
This methode allows you to change the color of your theme dynamicly within your app. It's based on [this idea](https://stackoverflow.com/a/48517223). In your activity onCreate add this line at the top **before** ```setContentView(...)```:
```java
new ThemeColor(this);
```
This will apply the color theme at launch. If you want to chnage the color you can use these functions:
```java
ThemeColor.setColor(Activity activity, int red, int green, int blue)
ThemeColor.setColor(Activity activity, float red, float green, float blue)
ThemeColor.setColor(Activity activity, float[] hsv)
```
The color you apply with these functions will apply on every activity with ```new ThemeColor(this)``` at the top.

### App Icon
The most app icons of Samsung apps are made of one solid color as background and a white icon as forground. Useually there is even a little part/detail of the foreground with a similar color as the background.

<img src="readme-resources/app-icons/settings.png" width="50" height="50" />   <img src="readme-resources/app-icons/notes.png" width="50" height="50" />   <img src="readme-resources/app-icons/messages.png" width="50" height="50" />   <img src="readme-resources/app-icons/camera.png" width="50" height="50" />   <img src="readme-resources/app-icons/calculator.png" width="50" height="50" />   <img src="readme-resources/app-icons/contacts.png" width="50" height="50" />   <img src="readme-resources/app-icons/myfiles.png" width="50" height="50" />

 I would suggest you to use ```@color/primary_color``` for the background color and ```@color/launcher_foreground_detail_color``` for the foreground "detail" color, so [your color theme](#Own-custom-color-theme) applys for the app icon too.  
My sample app icon for example:

<img src="readme-resources/app-icons/sample.png" width="50" height="50" />


## Progress

- [x] Cardview
- [x] Checkbox
- [x] Switch 
- [x] Radiobutton
- [x] Progressbar circle
- [x] Progressbar horizontal
- [x] Seekbar
- [x] Drawer
- [x] Drawer divider
- [x] SeslToggleSwitch
- [x] SeslProgressbar
- [x] SeslSwitchbar
- [x] SeslSeekbar
- [x] Collapsing toolbar
- [x] Rtl
- [x] Color picker dialog *
- [x] Button *
- [x] Spinner *
- [ ] Menu (in progress)
- [ ] Snackbar (in progress)
- [ ] Dialog
- [ ] Bottomsheet
- [ ] Tablayout
- [ ] Viewpager
- [ ] Landscape 
- [ ] Preferences
- [ ] Tooltip
- [ ] (Textview)
- [ ] (Edittext)

*needs improvement

## Special thanks to:
- [leonbcode](https://github.com/leonbcode) for github actions, so this library is always up-to-date.
- [nfauv2001](https://github.com/nfauv2001) for helping me out with my english.