# Tracking using LiveLink, Motion Controlers and custom methods

There are several ways of getting camera and object tracking data into Unreal.  As of release 4.26 probably the best and easiest way is to use LiveLink as it provides a single way to manage the timing of all the data coming in and keeping it synced up so your virtual and real objects move smoothly.

The main examples in VPStudio use LiveLink and were tested with Steam.  There will be an "OtherTrackerExamples" folder with some maps that use other methods.

# How my tracker actors work

All my tracker actors are similar.  You drag them into a level, configure them to hook up to your tracking device and then use the world outliner's "attach to" function to attach other actors to them.  Any actor you attach will follow the motion of your tracking device with no more setup.  When you create a tracker actor, zero out it's location and rotation.  Do the same to any actor you "attach to" the tracker actor.

# LiveLink trackers

LiveLink is a communications protocol Unreal uses to get tracking and other data in real time.  It's biggest advantage is that it works live in the editor so you can see your trackers moving without having to press "Play".  This makes it much easier to setup, calibrate and test out your studio setup. It has built in support for delaying and syncing up data from multiple sources and supports timecode. No complicated blueprints are needed to do this, it's all built in.

If you are using Steam, virtually any tracker, headset or hand controller should work with Unreal once you turn on the "LiveLinkXR" plugin.  Devices that support OpenXR should also work.  Other devices might require installing a LiveLink plugin which is available for many trackers, motion capture systems and other devices.  Once the plugin is installed, all your LiveLink devices are managed through the LiveLink window in the unreal editor.

In VPStudio, to use LiveLink tracking data just drag a LiveLinkTracker actor into the level.  Select it and in the "details/default" section use the "tracker type" pop-up to set the type of tracker and the "live link tracker to use" menu to select which tracking source.

# MotionController Trackers

Unreal has an older system that supports most VR headsets, hand controllers and trackers that work with games written for Unreal Engine.  This brings in the data to a component that you put inside an actor.  Hopefully you will not need to use this as most VR devices will be supported through Steam, LiveLink or their own custom plugins.  It's kept as an example and contains blueprint code that you can use when building your own tracking setup to delay tracking data.

To make them easier to use I built the "MotionControllerTracker" actor which works similar to my "LiveLinkTracker" actor.  I only recommend using this if your device does NOT support LiveLink, Steam or OpenXR.  The MotionControllerTracker requires a bit more configuration.  For Steam devices you usually need to setup bindings in Steam's tools, define the "role" of each tracker and then setup the motion controller component to attach to that role.  This can be kind of complicated to get right, it's covered in my older video tutorials.  You also have to set how many frames to delay the tracking data to keep it synced up.

# Custom Trackers

Some trackers or motion capture devices may have their own custom ways of bringing in tracking data, usually through some kind of plugin.  I don't have any of these devices so I can't be of too much help here.  You can use the MotionControllerTracker actor as an example of what you need to do to handle custom tracking data.





