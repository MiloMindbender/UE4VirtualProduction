# Tracking using LiveLink, Motion Controlers and custom methods

There are several ways of getting camera and object tracking data into Unreal.  As of release 4.26 the best and easiest way is to use LiveLink as it provides a single way to manage the timing of all the data coming in from your tracking devices.  Use my LiveLinkTracker actor for them.  Some devices, like older VR headsets, may only appear in unreal as MotionController objects, so I have MotionControllerTracker actors to handle those.  Other devices may have custom plugins.  See the sections below for info on how all this works.

# Relative and Absolute tracking

Absolute trackers like VIVE, Optitrack and others provide tracking measured from a fixed point in the room.  VIVE is an example of this.  Once the system is set up, a tracker set on a specific spot in the room will always return the same value.  To set the point with VIVE you should place your VIVE headset on the floor facing away from the camera, towards the green screen.  Then do a "room setup Standing" in Steam VR.  In the regular VPStudio setup, this spot in your room will corrispond to the position of "Talent Mark 1" in VPStudio.

Relative trackers like Intel Realsense measure their position from whatever location they were in when you turn them on.  To get these to match up with the coordinates in VPStudio you need to provide an offset from a fixed point in the room.  Some of these types of trackers have a procedure for doing this, with others you have to measure the offset using a tape measure and enter it manually.

# How my tracker actors work

All my tracker actors are similar.  You drag them into a level, configure them to hook up to a tracking device and then use the world outliner's "attach to" function to attach other actors to them.  Any actor you attach will follow the motion of your tracking device with no more setup.  When you create a tracker actor, zero out it's location and rotation.  Do the same to any actor you "attach to" the tracker actor.

If your tracker requires an offset to align it with VPStudio's coordinate system the tracker actor has a place to enter that.

# LiveLinkTracker

LiveLink is a communications protocol Unreal uses to get tracking and other data in real time.  It's biggest advantage is that it works live in the editor so you can see your trackers moving without having to press "Play".  This makes it much easier to setup, calibrate and test out your studio setup. It has built in support for delaying and syncing up data from multiple sources and supports timecode. No complicated blueprints are needed to do this, it's all built in.

You need to go into settings->plugins and turn on the LiveLinkXR plugin to use livelink tracking.  After doing this just about any tracker type supported by Steam will work.  For devices that don't work through steam you will have to install a LiveLink plugin for them, check with the manufacturer of your tracking device for how to get one.

All your LiveLink devices are managed through the LiveLink window in the unreal editor.  Before you try to connect to your devices, make sure they are all turned on and running.  To connect to them use the green +Source button in that window.  Once you have connected all your devices you can save a preset to make this easier next time.  In the LiveLink window all your devices should show up with a green dot next to them.  As long as the dot is green you are getting good tracking, if it turns yellow the tracking data has stopped.

In VPStudio, to use LiveLink tracking data just drag a LiveLinkTracker actor into the level.  Select it and in the "details/default" section use the "tracker type" pop-up to set the type of tracker and the "live link tracker to use" menu to select which tracking source.  If the tracker requires a relative offset you need to enter that too.

By default, a VIVE tracking puck is setup so the logo on the top is UP or Z, the USB port is the "back" or negative x.  The VIVE controller is setup so the X axis is in line with the handle with positive X towards the ring on the tracker and UP is the side with the touch pad on it.

# MotionController Trackers

Unreal has an older system that supports most VR headsets, hand controllers and trackers that work with games written for Unreal Engine.  This brings in the data to a component that you put inside an actor.  Hopefully you will not need to use this as most VR devices will be supported through Steam, LiveLink or their own custom plugins.  It's kept as an example and contains blueprint code that you can use when building your own tracking setup to delay tracking data.

To make them easier to use I built the "MotionControllerTracker" actor which works similar to my "LiveLinkTracker" actor.  I only recommend using this if your device does NOT support LiveLink, Steam or OpenXR.  The MotionControllerTracker requires a bit more configuration.  For Steam devices you usually need to setup bindings in Steam's tools, define the "role" of each tracker and then setup the motion controller component to attach to that role.  This can be kind of complicated to get right, it's covered in my older video tutorials.

# Custom Trackers

Some trackers or motion capture devices may have their own custom ways of bringing in tracking data, usually through some kind of plugin.  I don't have any of these devices so I can't be of too much help here.  You can use the MotionControllerTracker actor as an example of what you need to do to handle custom tracking data.

# Tracking delay

In Unreal, every sort of tracking and video has some delay before it gets to your computer.  Usually the tracking data comes in several frames ahead of the video, so it must be delayed so it matches the video.  If you have studio setup with TimeCode going to everything, this is automatic, but few people have this.  For setups like VIVE you adjust the delays manually.  For LiveLink this is set in seconds in either the LiveLink window or TimedDataManager window.  For MotionControllerTrackers it is set in frames in the MotionControllerTracker actor.

There will be a video soon showing how to measure and set up delay as it's kind of hard to describe.  Basically you suddenly move the camera and watch to see if the CG or the video objects start moving first.  Then you adjust the tracking delay till they both move at the same time.





