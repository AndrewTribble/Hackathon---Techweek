ReadMe for Affdex SDK for Android
Version 2.0

SDK Operating modes
===================
The Affdex SDK for Android has the following operating modes:

- Camera mode:  the SDK turns on the camera and collects images.  
  See the "AffdexMe" sample app for an example of this mode.
- Video file:  provide to the SDK a path to a video file.
- Pushed Frame mode:  provide to the SDK individual frames of video and their
  timestamps.
- Photo mode:  provide a discrete image to the SDK (unrelated to any other
  image).

Camera mode has a default frame rate of 5 frames/second. You can adjust the
frame rate with CameraDetector.setMaxProcessRate().

Android minimum SDK version
===========================
Apps built with this SDK will be able to run on any device running JellyBean
(Android API 16) and above. Apps should declare android:minSdkVersion to be 16
or higher. 

Apps must be compiled with Android compiler 17 or above, that is, 
android:targetSdkVersion must be 17 or higher. 

Supported devices
=================
The Affdex Android SDK is designed to work on most Android devices that meet
the minimum SDK version(API 16).

Here are some specific devices that have known issues:

Nexus 4 - using the camera from any app, including the stock camera app, may
reboot the phone. See https://code.google.com/p/android/issues/detail?id=67113

Samsung Galaxy S2 - may fail to process video files.  The SDK can successfully
process in camera mode, with static images, or pushing individual frames
(using processImage()). 

Contact
=======
Email: sdk@affectiva.com
Web: www.affdex.com/mobile-sdk 

Licensing
=========
Please see http://www.affectiva.com/sdk-trial-license-agreement/ for applicable
Affectiva license terms.

In addition, please see NOTICE.txt for information on 3rd party components
and their licensing.

2.0 Release Notes
=================
The 2.0 SDK release adds several new metrics, which are now categorized as emotions,  
expressions, and measurements.

Measurements, such as Yaw, Roll, and Pitch, are enabled by default. Emotions and expressions  
must be enabled through
a call to Detector.setDetectxxx(), just as in version 1.x of the SDK.

The mechanism through which metric values are retrieved has changed slightly. Metrics are still  
retrieved through the Face object
returned in onImageResults(). However, for better organization, the retrieval methods are  
divided among inner class of the Face object:

-To retrieve an emotion score call Face.emotions.getxxx() (e.g. Face.emotions.getJoy() )
-To retrieve an expression score call Face.expressions.getxxx() (e.g. Face.expressions.getSmile 
() )
-To retrieve a measurement score call Face.measurements.getxxx() (e.g.  
Face.measurements.getInterocularDistance() )
-To retrieve an orientation measurement score call Face.measurements.orientation.getxxx() (e.g.  
Face.measurements.orientation.getYaw() )

See the Android SDK Developer Guide for examples.

Bug fixes:
-VideoFileDetector running on Lollipop may have previously failed to detect a face on videos  
that were not oriented correctly. This has been fixed.
-Although the VideoFileDetector object should always have been initialized and run on a separate  
thread, the documentation did not state this. This has been fixed.

1.2 Release Notes
===============================
The following bugs have been fixed in version 1.2 of the SDK:

1) Previously, the CameraDetector object would throw an exception and
stop processing if CameraDetector.start() was called after any call to
CameraDetector.stop(). This has been corrected. (Bug #3580)

2) Previously, the CameraDetector object would fail to recognize faces
if the back camera of a device was used. This has been corrected.

New features of the SDK include:

1) If a non-null SurfaceView is passed into a CameraDetector object, the
SurfaceView will be resized to match the aspect ratio of the camera images.
The SurfaceView is resized to fit as much of its parent ViewGroup as possible.

2) CameraDetector now offers a CameraSurfaceViewListener interface, which will
fire an event when the size of the SurfaceView has been adjusted.

3) CameraDetector, FrameDetector, and VideoDetector now have a .reset() method
which will reset the baselines used to determine emotions and expressions.

1.1 Release Notes
===============================
If you implemented an integration using the 1.0 release, you will need
to make the following changes/additions to your implementation:

1) Change the way you construct your Detector class. There are now 4 Detector
subclasses, one for each "mode" of use.  See the Developer Guide for more
information.

2) Change the way you enable or disable the expressions you want to detect.
There are now separate setter methods in Detector for each expression type.

3) Update the signature of your onImageResults callback - expression scores
and face points are now returned via a List<Face> instead of a List<Metric>, 
and the timestamp argument has changed from double to float.

4) Update the way you retrieve expression scores or face points in your
onImageResults callback.  The Face object in the provided list has getter 
methods for the individual expression scores and for retrieving the face 
points.  Note that in this release, there will be zero or one Face in the
list (if there are multiple faces in the frame, the SDK will locate and
track the largest face).

5) If you previously called Detector.setReturnFacePoints, remove that
call.  This method has been removed; the SDK now returns face points
automatically.


Copyright (c) 2014 Affectiva, Inc. All rights reserved.









 


