---
layout: post
title: Android processing Hello World works but Geo-location example from Rapid Android Development failed initially because of permissions and sketch location and now it works!
---

## Pontifications
* After upgrading to the API level for Android 7.1.1 on the Pixel XL, the [Hello World works from the Android processing getting started tutorial](http://android.processing.org/tutorials/getting_started/index.html)! Code:

```processing

void setup() {
  fullScreen();
  noStroke();
  fill(0);
}

void draw() {
  background(204);
  if (mousePressed) {
    if (mouseX < width/2) {
      rect(0, 0, width/2, height); // Left
    } else {
      rect(width/2, 0, width/2, height); // Right
    }
  }
}
```
* But the Geo-location example from [Android Processing aka Rapid Android Development](https://www.mobileprocessing.org/) doesn't work. First I got ```Lost connection with device while installing - Try again```! I fixed that by moving the code to the default sketches folder but then I got ```Caused by: android.system.ErrnoException: android_getaddrinfo failed: EACCES (Permission denied)``` so I added Internet and access fine locations permissions and it worked! Code: 

```Java
/**
 * <p>Ketai Sensor Library for Android: http://ketai.org</p>
 *
 * <p>KetaiLocation Features:
 * <ul>
 * <li>Uses GPS location data (latitude, longitude, altitude (if available)</li>
 * <li>Updates if location changes by 1 meter, or every 10 seconds</li>
 * <li>If unavailable, defaults to system provider (cell tower or WiFi network location)</li>
 * </ul>
 * More information:
 * http://developer.android.com/reference/android/location/Location.html</p>
 * <p>Updated: 2012-01-20 Daniel Sauter/j.duran</p>
 */

import ketai.sensors.*; 
double longitude, latitude, altitude, accuracy;
KetaiLocation location;  //(1)
Location otherDevice;  //(2)
KetaiSensor sensor;
String serverMessage = "";
String myName = "myNexusID";  //(3)
String deviceTracked = "myNexusID";  //(4)
String serverURL = "http://ketaiLibrary.org/rapidAndroidDevelopment/location.php"; //(5)
float compass;

void setup() {
  otherDevice = new Location("yourNexus");
  sensor = new KetaiSensor(this);
  sensor.start();
  location = new KetaiLocation(this);
  orientation(PORTRAIT);
  textAlign(CENTER, CENTER);
  textSize(72);
}

void draw() {
  background(78, 93, 75);
  float bearing = location.getLocation().bearingTo(otherDevice);
  float distance = location.getLocation().distanceTo(otherDevice);
  if (mousePressed) {
    if (location.getProvider() == "none")
      text("Location data is unavailable. \n" +
        "Please check your location settings.", 0, 0, width, height);
    else
      text("Location data:\n" + 
        "Latitude: " + latitude + "\n" + 
        "Longitude: " + longitude + "\n" + 
        "Altitude: " + altitude + "\n" +
        "Accuracy: " + accuracy + "\n" +
        "Distance to Other Device: "+ nf(distance, 0, 2) + " m\n" + 
        "Provider: " + location.getProvider()+ "\n" + 
        "Last Server Message: " + serverMessage, 20, 0, width, height );
  }
  else {
    translate(width/2, height/2);
    rotate(radians(bearing) - radians(compass));
    stroke(255);
    triangle(-width/4, 0, width/4, 0, 0, -width/2);
    text((int)distance + " m", 0, 60);
    text(nf(distance*0.000621, 0, 2) + " miles", 0, 140);
  }
}

void onLocationEvent(Location _location)  //(6)
{
  // Print out the location object
  println("onLocation event: " + _location.toString());
  longitude = _location.getLongitude();
  latitude = _location.getLatitude();
  altitude = _location.getAltitude();
  accuracy = _location.getAccuracy();
  updateMyLocation();
}

void updateMyLocation()
{
  if (myName != "")
  {
    String url = serverURL+"?update="+myName+
      "&location="+latitude+","+longitude+","+altitude;  //(7)
    String result[] = loadStrings(url);  //(8)
    if (result.length > 0)
      serverMessage = result[0];
  }
}

void mousePressed()
{
  if (deviceTracked != "")
  {
    String url = serverURL + "?get="+deviceTracked;  //(9)
    String result[] = loadStrings(url);
    for (int i=0; i < result.length; i++)
      println(result[i]);
    serverMessage = result[0];
    // Let's update our target device location
    String[] parameters = split(result[0], ",");
    if (parameters.length == 3)  //(10)
    {
      otherDevice = new Location(deviceTracked);
      otherDevice.setLatitude(Double.parseDouble(parameters[0]));
      otherDevice.setLongitude(Double.parseDouble(parameters[1]));
      otherDevice.setAltitude(Double.parseDouble(parameters[2]));
    }
  }
  updateMyLocation(); //(11)
}

void onOrientationEvent(float x, float y, float z, long time, int accuracy)
{ 
  compass = x;  
  // Angle between magnetic north and device y-axis, around z-axis.
  // Range: 0 to 359 degrees
  // 0=North, 90=East, 180=South, 270=West
}
```
