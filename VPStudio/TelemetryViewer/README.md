# Live Monitoring of VIVE trackers and Unreal

This is [TelemetryViewer](http://farrellf.com/TelemetryViewer/) From "Farrellf" or [upgrdman](https://www.youtube.com/user/upgrdman) on YouTube. A JRE (Java Runtime Environment) needs to be installed on your computer to run it.  There is a link to one on his website above.  Videos on how to use the tool are on his YouTube channel with the [latest one here](https://youtu.be/FqfgBnCdrTo)  It's useful for a lot of things, here I am using it to display real-time transform information from a VIVE tracker or any other actor.

For monitoring telemetry this is one of the best programs I have found but it has the limitation of only working with one source of data and the exact size and layout of the data has to be known in advance. If you want to be able to record telemetry from a lot of programs and computers all at once, or change what data is sent see "Advanced Telemetry" below.

# What can I get Telemetry from and what do I get?

You will get location and rotation in world coordinates from a list of actors.  Coordinates are in centemeters and rotations in degrees.  For VPStudio LiveLinkTracker and MotionControlerTracker actors you will get the "output" transform after any adjustments/delays have been applied.  All other actors will send their root transform. 

You can select to get the raw transform information, a version that's "normalized" by subtracting the first transform seen when the program starts or "relative" data showing the change since the last reading.  The "normalized" and "relative" data help keep the graphs centered on 0.0 so they are easier to compare.  You can put several traces on the same graph without loosing too much precision when the graphs auto-range.

All the blueprints and sample maps for this are in the VPStudioCore/TestAndTelemetry folder in the content browser.

# Getting telemetry from your level

__Important__ only add ONE ActorTransformTelemetry actor to your level or telemetry will be corrupted, it will send telemetry from any number of other actors. Under the "default" parameters can set the type of telemetry, the IP address and port of TelemetryViewer.  The defaults will send to TelemetryViewer running on the same computer as Unreal.  The last thing is the list of actors you want to send telemetry from.  All the actors you want to send telemetry from must be in the same sublevel as the ActorTransformTelemetry actor. This is set with the button in the lower right corner of the editor viewport.

Telemetry Viewer expects to receive telemetry from a fixed numbe of actors, set by the configuration file you load after you start it up.  The data sent by unreal must be the same size as the one Telemetry Viewer expects to receive.  In ActorTransformTelemetry "Max Actors"  sets max number of actors you can send and must match the config file you load in Telemetry Viewer.  You can send information from less than this number of actors but not more.  I've provided Telemetry Viewer config files for 1, 4 and 8 actors.  You can send more but you will have to make your own config file for Telemetry Viewer to do it.

## Running TelemetryViewer

Double click TelemetryViewer, if it does not launch you may not have a recent JRE (Java Runtime Environment) installed.  See  [Farrellf's site](http://farrellf.com/TelemetryViewer/) for more info if you don't know what this is.

Press the "Import" button in the lower left and navigate to the folder you launched TelemetryViewer from.  Select the file for 1, 4 or 8 actors depending on how you have Max Actors setup in ActorTransformTelemetry

A green bar should appear at the top of the TelemetryViewer screen saying it is ready.  Now press "Play" in Unreal and you should see the graphs start updating.

You can scroll back and forth in time using the scroll wheel of your mouse or zoom in and out by holding down the Ctrl key and turning the scroll wheel.  See[the author's youtube site ](https://www.youtube.com/user/upgrdman) for videos on other features.

When you "stop" your unreal app, it takes a few seconds for TelemetryViewer to reset the network connection. If you press play again too soon TelemetryViewer may get out of sync and appear to run very slowly.  To fix this just press stop in unreal, quit TelemetryViewer and restart it.

# Testing your tracker setup

Sometimes the base stations may not be fully covering your room or there can be reflections of the tracking lasers from shiny objects, windows or monitors.  Or people may walk between the tracker and base station.  This can cause low quality or complete drop-outs of tracking in some parts of the room.

The best way to debug this is to use the ActorTransformTelemetry map setup to see data from all your trackers.  Then move them around the room and watch the screen to see exactily where in the room you have problems.  You may want to set TelemtryType to "Raw Tracker Relative" this will make it easier to see glitches.

To see the amount of noise your tracker receives, put it on a table, the floor or tripod and let it sit.  The wiggling of the charts is the noise.  It's normal to see noise in the X,Y,Z values of about 0.02 (two hundredths of a centemeter).  If yours is worse you might have a problem.

VIVE base stations can be very sensitive to vibration, this will show up as jitter in your videos.  To check for this, make sure all your trackers are stationary and let them run till you can see the noise.  Then try doing things like jumping, walking around the room and knocking on walls.  If the vibration is getting into your tracking data it should show up really clearly on the telemetry graphs.

It may make it easier to test if you hookup a webcam to TeletryViewer so you can see where you were in the room when problems happened.

The telemetry sending actors will work in any project with any frame rate.  If you want really detailed and clean data when testing your setup, use one the simple tracker telemetry example maps and set a fixed frame rate of 60 or higher in the project settings.  Try to pick a frame rate your computer can maintain.

# Advanced Telemetry

## Customizing TelemetryViewer charts

You can change around TelemetryViewer's charts and graphs however you like.  The layouts I provide are fairly basic, you can easily change them.  Check out Farrellf's [latest video](https://youtu.be/FqfgBnCdrTo) for tutorials on how to use the program.

TelemetryViewer can also capture video from a webcam or network camera along with the telemetry data, this lets you see what was happening in the room at the time the data was recorded.

## More than 8 VivePucks

To support more than 8 VivePucks you will need to customize TelemetryGrapher.  By pressing the disconnect and connect buttons in the lower left corner you can see a screen with the layout of the message I send.  To make a setup for more than 8 trackers you will need to add more lines to this table, 6 float32's for each additional tracker.  You will also need to change the layout of the screen so it can display more than 8 sets of graphs.

In ActorTransformTelemetry set "maximum pucks" to the number of pucks you setup in TelemetryViewer.  The value of maximum pucks must match your TelemetryViewer setup.

## Custom telemtry

You may want to send telemtry from something else in your level like a lens tracker or a simulated vehicle.  If you take a closer look at my ActorTransformTelemetry you can use it as an example of how to send other kinds of data to TelemetryViewer.  For example in a game you could send info on a vehicle's suspension system, where players were in the level...etc

## Telemetry from lots of objects or multiple computers with COSMOS

If you have a complex virtual production setup with multiple cameras, video walls, Ndisplay setups and different tracking systems it's possible to send telemetry from all of them to one place!  This can be really helpful for keeping a complicated system running smoothly and knowing if anything is out of whack. Everything is automatically archived to disk and can be replayed later.

https://cosmosrb.com/ is an advanced telemetry system used by NASA and other aerospace companies.  It's realtime graphs aren't as fast as TelemetryViewer but it can do way more.  Almost any device can send it Telemetry over network, serial and other types of connections.  Any message, any format and one device can send more than one kind of message.

You can build screens to monitor a whole system and automatically check to make sure all the values it's receiving are "in range" so you can have a status board for the whole studio and if anything goes out of spec (like a drop in frame rate), an indicator will light up red to let you know.

Cosmos can also SEND commands to devices, so you can setup screens with buttons and other controlls to turn systems on and off.

It's been well tested in "mission critical" aerospace applications and is pretty much totally bulletproof.  You could build your own telemetry system but it's not going to be as well tested and flexible as this.

It's only real flaw is that visually it's not as "pretty" as telemetry viewer, but if you need an advanced system to monitor the whole studio it's the place to go.

