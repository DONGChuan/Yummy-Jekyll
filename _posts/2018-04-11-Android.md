---
layout: post
title: Android Toolbar
category: android
tags: [android]
---

Quick note about learning [Training : Adding the App Bar](https://developer.android.com/training/appbar/index.html)

Android introduces a new Toolbar widget. It is a generalization of the Action Bar pattern that gives us much more control and flexibility. ActionBar now is considered a special kind of Toolbar.

Using a Toolbar as an replacement to ActionBar:

1. Greater control to customize its appearance.
2. Fully support to lower android os devices via AppCompact support lib.
3. Continue to use the ActionBar features such as menus, selections, etc. 
4. Use a standalone Toolbar, put it where ever we want in app.

## Add Toolbar

To Add Toolbar:

1. Have [v7 appcompat support library](https://developer.android.com/topic/libraries/support-library/features.html#v7-appcompat)
2. Activity to extend `AppCompatActivity`
3. Update theme to be without actionbar
4. Apply theme to every activity
5. Define toolbar in activity layout
6. Update `onCreate()` to have this toolbar

#### Extend `AppCompatActivity`

{% highlight java %}
public class MyActivity extends AppCompatActivity {
    // ...
}
{% endhighlight %}

#### Update theme

Update theme to NoActionBar to prevent the app from using the native ActionBar class to provide toolbar.

In `res/values/styles.xml`:

{% highlight xml %}
<!-- Theme for activity -->
<style name="AppTheme.NoActionBar">
    <item name="windowActionBar">false</item>
    <item name="windowNoTitle">true</item>
</style>

<!-- Theme for toolbar -->
<style name="AppTheme.AppBarOverlay" parent="ThemeOverlay.AppCompat.Dark.ActionBar" />

<!-- Theme for toolbar popup menu -->
<style name="AppTheme.PopupOverlay" parent="ThemeOverlay.AppCompat.Light" />
{% endhighlight %}

#### Update `AndroidManifest.xml`

Make sure all `<activity>` has the AppTheme.`NoActionBar` theme 

{% highlight xml %}
android:theme="@style/AppTheme.NoActionBar"
{% endhighlight %}

#### Update activity layout

* `android:theme` sets theme for the whole toolbar.
* `app:popupTheme` sets theme for the toolbar overflow menu.

{% highlight xml %}
<android.support.v7.widget.Toolbar
   android:id="@+id/my_toolbar"
   android:layout_width="match_parent"
   android:layout_height="?attr/actionBarSize"
   android:background="?attr/colorPrimary"
   android:elevation="4dp"
   android:theme="@style/ThemeOverlay.AppCompat.ActionBar"
   app:popupTheme="@style/ThemeOverlay.AppCompat.Light"/> 
{% endhighlight %}

> Elevation 4dp is recommanded by [Material Design specification](https://www.google.com/design/spec/what-is-material/elevation-shadows.html#elevation-shadows-shadows) 

#### Update `onCreate()`

{% highlight java %}
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_my);

    Toolbar myToolbar = (Toolbar) findViewById(R.id.my_toolbar);
    setSupportActionBar(myToolbar);
} 
{% endhighlight %}

## Add Action Buttons

To add action buttons:
 
1. Update menu layout xml in `res/menu/` to have this button
2. Update `onOptionsItemSelected()` to add listener

#### Update menu layout xml

Button will appear directly in toolbar or in overflow menu according to:

* `app:showAsAction="ifRoom"` - button will be displayed on toolbar if there is enough room in the toolbar; if not, it will be in overflow menu.
* `app:showAsAction="never"` - Only in the overflow menu.

{% highlight xml %}
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    tools:context="com.example.chuandong.myapplication.MainActivity">

    <!-- in toolbar if there is room -->
    <item
        android:id="@+id/item_a"
        android:icon="@mipmap/ic_launcher"
        android:title="@string/action_settings"
        app:showAsAction="ifRoom"/>

    <!-- in overflow menu -->
    <item
        android:id="@+id/item_b"
        android:orderInCategory="100"
        android:title="@string/action_settings"
        app:showAsAction="never" />

</menu>
{% endhighlight %}

#### Update `onOptionsItemSelected()` to add Listener

{% highlight java %}
@Override
public boolean onOptionsItemSelected(MenuItem item) {

    switch (item.getItemId()) {
        case R.id.item_a:
            // ToDo
            return true;

        case R.id.item_b:
            // ToDo
            return true;

        default:
            // ToDo
            return super.onOptionsItemSelected(item);

    }
}
{% endhighlight %}

### Adding an Up Action

Up button in toolbar is for all activities (except the main one) to **navigate to the parent activity**.

Two steps:

1. Declare a Parent Activity
2. Enable the Up button for an activity

#### Declare a Parent Activity

In `AndroidManifest.xml`:

* For higher than Android 4.1 (API level 16), using `android:parentActivityName`.
* For older version, using `<meta-data>` name-value pair, where name is `android.support.PARENT_ACTIVITY` with value the name of the parent activity.

{% highlight xml %}
<application ... >
    ...

    <!-- The main/home activity (it has no parent activity) -->
    <activity
        android:name="com.example.myfirstapp.MainActivity" ...>
        ...
    </activity>

    <!-- A child of the main activity -->
    <activity
        android:name="com.example.myfirstapp.MyChildActivity"
        android:label="@string/title_activity_child"
        android:parentActivityName="com.example.myfirstapp.MainActivity" >

        <!-- Parent activity meta-data to support 4.0 and lower -->
        <meta-data
            android:name="android.support.PARENT_ACTIVITY"
            android:value="com.example.myfirstapp.MainActivity" />
    </activity>
</application>
{% endhighlight %}

#### Enable Up button

{% highlight java %}
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_my);

    Toolbar myToolbar = (Toolbar) findViewById(R.id.my_toolbar);
    setSupportActionBar(myToolbar);

    // Get a support ActionBar corresponding to this toolbar
    ActionBar actionbar = getSupportActionBar();

    // Enable the Up button
    actionbar.setDisplayHomeAsUpEnabled(true);
} 
{% endhighlight %}

## Action Views

It is an action providing rich functionality. For example, a search action view allows the user to type their search text in toolbar, without having to change activities or fragments.

1. Add `<item>` in toolbar menu resource
2. Update `onCreateOptionsMenu()` to add event listener

#### Update toolbar menu resource

To add an action view, create an `<item>` element in the toolbar's menu resource. Then add one of the following two attributes to the element:

* `actionViewClass` - The class of a widget that implements the action.
* `actionLayout` - A layout resource describing the action's components.

Set `showAsAction` to either `ifRoom|collapseActionView` or `never|collapseActionView`. 

The `collapseActionView` indicates how to display the widget when the user is not interacting with it: If the widget is on toolbar, the app should display the widget as an icon. If the widget is in the overflow menu, the app should display the widget as a menu item. When the user interacts with the action view, it expands to fill toolbar.

{% highlight xml %}
<item android:id="@+id/action_search"
     android:title="@string/action_search"
     android:icon="@drawable/ic_search"
     app:showAsAction="ifRoom|collapseActionView"
     app:actionViewClass="android.support.v7.widget.SearchView" />
{% endhighlight %}     
     
#### Update `onCreateOptionsMenu()`

Update `onCreateOptionsMenu()` in activity to add event listener

{% highlight java %}
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.main_activity_actions, menu);

    MenuItem searchItem = menu.findItem(R.id.action_search);
    SearchView searchView =
            (SearchView) MenuItemCompat.getActionView(searchItem);

    // Configure the search info and add any event listeners...

    return super.onCreateOptionsMenu(menu);
}
{% endhighlight %}

#### Listener to action view collapse/expanded

If we want to do something when action view collapses/expands:

1. Define and override `OnActionExpandListener`
2. Add this listener to action view item

{% highlight java %}
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.options, menu);
    // ...

    // Define the listener
    OnActionExpandListener expandListener = new OnActionExpandListener() {
        @Override
        public boolean onMenuItemActionCollapse(MenuItem item) {
            // Do something when action item collapses
            return true;  // Return true to collapse action view
        }

        @Override
        public boolean onMenuItemActionExpand(MenuItem item) {
            // Do something when expanded
            return true;  // Return true to expand action view
        }
    };

    // Get the MenuItem for the action item
    MenuItem actionMenuItem = menu.findItem(R.id.myActionItem);

    // Assign the listener to that action item
    MenuItemCompat.setOnActionExpandListener(actionMenuItem, expandListener);

    // Any other things you have to do when creating the options menu…

    return true;
}
{% endhighlight %}

## Action Providers

It is an action with its own customized layout. When user clicks it, the action provider controls the action's behavior in any way we want. For example, the action provider might respond to a click by displaying a menu.

{% highlight xml %}
<item android:id="@+id/action_share"
    android:title="@string/share"
    app:showAsAction="ifRoom"
    app:actionProviderClass="android.support.v7.widget.ShareActionProvider"/>
{% endhighlight %}

To create a custom action provider, see [here](https://developer.android.com/reference/android/support/v4/view/ActionProvider.html). 

To configure a ShareActionProvider, see [here](https://developer.android.com/reference/android/support/v7/widget/ShareActionProvider.html).

## Ref

* [What is the difference between Action Bar and newly introduced Toolbar?](http://stackoverflow.com/questions/27665018/what-is-the-difference-between-action-bar-and-newly-introduced-toolbar)