---
title: Applying Android Vibration
categories: tutorial
tags: java android
author: Dai Tianle
image: "/assets/img/2019-02-23-Applying-Android-Vibration.png"
---

# Vibration in andoird

Vibration is an important part of software development in andoird, it acts as a machine-response to certain user action. Noramlly we apply vibration in such circumstances

  - Typing repsonse (soft keyboard)
  - Action response (simulated key)
  - Notification 

# Getting Started

- In andoird studio we use vibrator to control the vibration.
- Before we start, we need to specify the permission to vibrator.
 
    **Open your andoird.xml and let's add in this.**
```java
   <uses-permission android:name="android.permission.VIBRATE"/>
```
--------------------- 
### Method 1

The first method is common and simple to use, that is to vibrate for certain amount of time.
```java
import android.os.Vibrator;
import android.app.Service;

public class MainActivity extends Activity {
	Vibrator vibrator;    // create vibrator
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		
		vibrator=(Vibrator)getSystemService(Service.VIBRATOR_SERVICE); 
		// link to service
		vibrator.vibrate(2000); // vibrate for 2000 milisecond
	}
}
```
As we can see from the last line of the code, we have asked the vibrator to vibrate for 2000 miliseconds.
**But after we try this on our phone, there is one more issue, the viration is too strong!**

--------------------- 
### Method 2

Indeed, 
```java
    vibrator.vibrate(2000);
```
It only controls the time of one vibration but not the strength of the vibration.
Thus, we need a second method -- vibrate in **pattern**

Let's see what Google officially define this

#### Vibrate with a given pattern.
>Pass in an array of ints that are the durations for which to turn on or off the vibrator in milliseconds. The first value indicates the number of milliseconds to wait before turning the vibrator on. The next value indicates the number of milliseconds for which to keep the vibrator on before turning it off. Subsequent values alternate between durations in milliseconds to turn the vibrator off or to turn the vibrator on.

>To cause the pattern to repeat, pass the index into the pattern array at which to start the repeat, or -1 to disable repeating.

In this case we want to
- Vibrate a phone for 400 ms then pause for 200 ms
- And again vibrate for 400 ms then our pattern becomes : {400, 200, 400};
- Vibrator treats first element of an array as a delay in ms. It would start vibrating a device after array[0] ms.
- If you don’t want any initial delay then your array becomes :
 {0, 400, 200, 400};

```java
private void customVibratePatternNoRepeat() {
    // 0 : Start without a delay
    // 400 : Vibrate for 400 milliseconds
    // 200 : Pause for 200 milliseconds
    // 400 : Vibrate for 400 milliseconds
    long[] mVibratePattern = new long[]{0, 400, 200, 400};

    // -1 : Do not repeat this pattern
    // pass 0 if you want to repeat this pattern from 0th index
    vibrator.vibrate(mVibratePattern, -1);
}
```
By passing -1 to the vibrate() we are asking to play it just once. If we want to repeat this pattern we can just pass 0.
```java
// 0 : Repeat this pattern from 0th element.
vibrator.vibrate(mVibratePattern, 0);
```
To cancel vibration at any time call :
```java
vibrator.cancel()
```
If we want to Repeat vibration pattern from specific index?
Consider this example of the vibration pattern:
```java
long[] mVibratePattern = new long[]{0,400,800,600,800,800,800,1000};
```
Here :
- FirstElement 0 : Initial delay 0 ms
- SecondElement 400 : Vibrate for 400 ms
- ThirdElement 800 : Pause for 800 ms
- FourthElement 600 : Vibrate for 600 ms
- FifthElement 800 : Pause for 800 ms
- SixthElement 800 : Vibrate for 800 ms
- SeventElement 800 : Pause for 800 ms
- EightElement 1000 : Vibrate for 1000 ms

we are increasing vibrate time by 200 ms. Suppose we want to repeat vibration from 600 onwards for which we will pass index position of 600 to vibrate() So for repeating vibration from specific index it becomes :
```java
// 3 : Repeat this pattern from 3rd element of an array
vibrator.vibrate(mVibratePattern, 3);
```

--------------------- 
### And some more...

The pattern of vibration is easy and useful in customising vibration pattern according to needs.
Here are some useful examples:
```java
//Vibrator pattern for feedback about a long screen/key press
long[] mVibratePattern1 = new long[]{0, 1, 20, 21};

//Vibrator pattern for feedback about touching a virtual key
long[] mVibratePattern2 = new long[]{0, 10, 20, 30};

//Vibrator pattern for a very short but reliable vibration for soft keyboard tap
long[] mVibratePattern3 = new long[]{40};

//Vibrator pattern for feedback about booting with safe mode disabled
long[] mVibratePattern4 = new long[]{0, 1, 20, 21,500,600};
```

**Thanks for reading~ HOOYAH!**
References:

*Google  [https://developer.android.com/reference/android/os/Vibrator](https://developer.android.com/reference/android/os/Vibrator)*

*ProAndroiddev   [https://proandroiddev.com/using-vibrate-in-android-b0e3ef5d5e07](https://proandroiddev.com/using-vibrate-in-android-b0e3ef5d5e07)*
	
	
