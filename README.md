Lab 0.5: Navigating between two views
===

Hey guys, in this in-class lab, we are going to work on navigating between two views. We will cover the following:

* The basics of MVC
* The tons of folders in an Android app
* Adding a second activity
* Your homework

The basics of MVC
---


The tons of folders in an Android app
---
You may have notied that the HelloWorld app had a ton of folders (directories). We would like to go over a few of the important ones:

* AndroidManifest.xml: The manifest file describes the fundamental characteristics of the app and defines each of its components. You'll learn about various declarations in this file as you read more training classes.
	* One of the most important elements your manifest should include is the <uses-sdk> element. This declares your app's compatibility with different Android versions using the android:minSdkVersion and android:targetSdkVersion attributes. For your first app, it should look like this:
```
<manifest xmlns:android="http://schemas.android.com/apk/res/android" ... >
    <uses-sdk android:minSdkVersion="8" android:targetSdkVersion="17" />
    ...
</manifest>
```
* main/ 
	* java/: Directory for your app's main source files. By default, it includes an Activity class that runs when your app is launched using the app icon.
	* res/: Contains several sub-directories for app resources. Here are just a few:
		* drawable-hdpi/: Directory for drawable objects (such as bitmaps) that are designed for high-density (hdpi) screens. Other drawable directories contain assets designed for other screen densities.
		* layout/: Directory for files that define your app's user interface.
		* values/: Directory for other various XML files that contain a collection of resources, such as string and color definitions.

Adding a second activity
---
Now we would like to go over how to add a second activity to your HelloWorld app. To start, fork and clone our Lab_0.5 app and open it up in Android Studio.

Open up main --> java --> MainActivity.java. This is the file which acts as your controller. It sohuld look like this:

```
package com.evansimpson.mobpro.lab0;

// imports
import android.os.Bundle;
import android.app.Activity;
import android.view.Menu;

// MainActivity: This is what runs when you open the app
public class MainActivity extends Activity {

	// onCreate method sets the view to activity_main, which is a view found in the layout folder (code found below)
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    // Adds in the menu (the top bar that says Lab0)
    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.main, menu);
        return true;
    }
    
}
```

Pay close attention to the onCreate method, which sets the view to activity_main. This is the logic behind what is displayed when you open the app. 

Open up main --> res --> layout --> activity_main.xml. It should look like this:

```
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingBottom="@dimen/activity_vertical_margin"
    tools:context=".MainActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/hello_world" />

</RelativeLayout>
```

This is where the basic UI elements that you see when you open up the HelloWorld app, such as the text that says "Hello World" are layed-out.

Okay, time to go back to MainActivity.java. Now, we are going to create a second activity. 



__Making the Activities__

1. Click file --> new --> class and name it FirstActivity
2. Copy over the code from MainActivity.java to FirstActivity
3. Change the name in MainActivity to be FirstActivity and change `setContentView(R.layout.activity_main);` to `setContentView(R.layout.activity_first);`
4. Repeat steps 2 and 3 to make another activity called SecondActivity. Now we have two activities, which we will create the ability to navigate between.

__Making the Views__
1. Next, we are going to make the views themselves. Open up the folder (main --> res --> layout) and right click, click new, "new layout resource file" and name it activity_first.xml. Repeat these steps again to make another layout file called activity_second.xml.
2. For the sake of time, we are going to give you the two layout files for this lab. (In the homework, you will work on putting new UI elements into the layout.) Paste the code below into the new layout files that you made. 

activity_first.xml
```
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingBottom="@dimen/activity_vertical_margin"
    tools:context=".FirstActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/activity1" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/button"
        android:id="@+id/button1"
        android:layout_alignParentTop="true"
        android:layout_alignParentRight="true"/>

</RelativeLayout>
```

activity_second.xml
```
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingBottom="@dimen/activity_vertical_margin"
    tools:context=".FirstActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/activity2" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/button"
        android:id="@+id/button2"
        android:layout_alignParentTop="true"
        android:layout_alignParentRight="true"/>

</RelativeLayout>
```

__Adding Strings__

1. Next, look at all the red elements that appeared. This means that the app cannot find the "resource", in this case the string, since it is not declared. Resources are declared in the values folder and can be shared throughout portions of the app. It is worth defining elements like strings in the values folder instead of hardcoding them, as it makes it much easier to change the value of the string later.
2. Open up main --> values --> strings.xml 
3. We need to define a few string values (aka the ones that are highlighted in red on the layouts). Paste the three values below into the strings.xml file.

```
<string name="activity1">Click the button to go to activity 2</string>
<string name="activity2">Click the button to go back to activity 1</string>
<string name="button">Navigate</string>
 ```
 
As you can see, these three values are the text shown in activity1, activity2, and on the button that allows you to navigate between views.


 __Adding Navigation between Activities___

 1. Now lets hook up the button so that it can navigate between the FirstActivity and SecondActivity. To do this, open up FirstActivity.java and check out the onCreate method.
 2. Now, if you've ever seen Java before, you know that buttons have listeners. Listeners are essentially a way to process events. Aka, to setup a button to do something, you attach a listener to the button, called an setOnClickListener(), which tells the app that something should happen when the button is clicked. Inside the Listener, you define an onClick() method, which deifnes what happens when the button is clicked. In our case, we want to click the button to switch to SecondActivity.
 3. in FirstActivity.java, inside the onCreate() method, under `setContentView(R.layout.activity_first);` add:

 ```
 Button b = (Button) findViewById(R.id.button1); // creates a button b and attaching it to the UI element called button1 on the view
        b.setOnClickListener(new View.OnClickListener() { // creates and sets an onClickListener for the button b
            @Override
            public void onClick(View view) { // creates the onClick method for the listener, which controls what is done when the button is clicked
                Intent i = new Intent(getApplicationContext(), SecondActivity.class); // creates a new intent i, which is how Android passes information between activities, and defines this intent as a way to navigate to the SecondActivity
                startActivity(i); // tells Android to make the intent active
            }
        });
```

4. Take a minute to check out this code (commented) 
5. Repeat step 3 for SecondActivity.java, only change button1 to button2 and SecondActivity.class to FirstActivity.class

__Appending Activities to the Android Manifest__

1. We are almost done. The last step is to make sure that the Android manifest includes all of the activities, so that the app knows they exist.
2. Change `android:name="com.evansimpson.mobpro.lab0.MainActivity"` to `android:name="com.evansimpson.mobpro.lab0.FirstActivity"` so that FirstActivity.java appears when you launch the app
3. Add in SecondActivity.java by appending a new <activity> tag inside the <application> tag. Your manifest should look like this:

```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.evansimpson.mobpro.lab0"
    android:versionCode="1"
    android:versionName="1.0" >

    <uses-sdk
        android:minSdkVersion="7"
        android:targetSdkVersion="16" />

    <application
        android:allowBackup="true"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme" >
        <activity
            android:name="com.evansimpson.mobpro.lab0.FirstActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity
            android:name="com.evansimpson.mobpro.lab0.SecondActivity">

        </activity>
    </application>

</manifest>
```

__Time to build your app__

1. Now hit Build --> Make Project on the toolbar -- don't worry if errors come up, we will fix them
2. Next, hit Run --> FirstActivity on the toolbar (you can also hit the play button on the top nav)
3. Play with your next app! And grab us to help you troubleshoot.

Homework
---

For homework, we are going to ask you guys to create a simple to do list. You can find the example demo here (insert link).

To break this down into more detail, the specs are:
* 1 Activity / View
* 1 Text field with a character limit of 10 characters
* A button to add a new task
* Labels for the tasks (which you made in the layouts above, they say "Click the button to go back to activity 1")
* Delete buttons to delete the tasks that you have added

Some useful hints. First of all, you know most of this stuff, since we just covered it. Look back at what we did for reference.
* The add button and delete buttons will need an onClickListener. The add button will add a new label to the view and the delete buttons will delete labels from the views
* Check out the [layouts tutorial, especially the list views portion](http://developer.android.com/guide/topics/ui/layout/listview.html) since a to-do list can be done with a listview
* The text field can be added via xml using a textfield item. You can google for the syntax. Here is a place to get you started.

```
<EditText android:id="@+id/edit_message"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:hint="@string/edit_message" />
```

Check out [the Android tutorial site](http://developer.android.com/training/basics/firstapp/building-ui.html#TextInput) for more info on text fields

Tim, Evan, and Juliana will be in SF from Thursday - Sunday, which is why we are giving you guys a challenging homework assignment. Google for answers first, then email us, text us, find us in EH. Along with our usual office hours, we will set up another time to either hold Google hangout office hours or have office hours on Sunday night.

