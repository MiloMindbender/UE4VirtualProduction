# Live Monitoring of VIVE trackers and Unreal

This is [TelemetryViewer](http://farrellf.com/TelemetryViewer/) From "Farrellf" or [upgrdman](https://www.youtube.com/user/upgrdman) on YouTube. A JRE (Java Runtime Environment) needs to be installed on your computer to run it.  There is a link to one on his website above.  Videos on how to use the tool are on his YouTube channel with the [latest one here](https://youtu.be/FqfgBnCdrTo)  It's useful for a lot of things, here I am using it to display real-time information from a VIVE tracker.

For monitoring telemetry this is one of the best programs I have found but it has the limitation of only working with one source of data and the exact size and layout of the data has to be known in advance. If you want to be able to record telemetry from a lot of programs and computers all at once, or change what data is sent see "Advanced Telemetry" below.

# What can I get Telemetry from?

I have built two actors for sending telemetry data to TelemetryViewer.  The first is "SingleTelemetrySender" that sends telemetry from ANY single Unreal actor, it works on VivePuck actors or other actors such as a game character or vehicle.

The second is "MultipleTrackerTelemetry", this only works with VivePuck objects but automatically detects and sends telemetry from every VivePuck in your level.
  
VivePuck objects can be setup for VR hand controllers so you can send telemetry from those as well.

All this stuff is in the VPStudioCore/TestAndTelemetry folder of the project.

# What kind of telemetry do I get?

Right now I send X, Y, Z in cm and Roll, Pitch, Yaw in degrees.  There are three versions you can select.  RawTracker is the data with no changes.  RawTrackerNormalized remembers the first position it sees and sends all the following data relative to that.  RawTrackerRelative sends only the change in position from the previous one.  

The different types of telemetry are in a pop-up menu in the "details" window for the telemetry sender actor.

# Getting telemetry from your level

__Important__ only put ONE SingleTelemetrySender or MultipleTrackerTelemetry actor in your level.  If you have both or more than one of either the telemetry will be corrupted. 

## SingleTelemetrySender for one actor

You can see a sample for this in the SingleTelemetrySenderExample level.  To add to your own level just drop the SingleTelemetrySender actor into the level, go to to the world outliner and drag and drop the SingleTelemetrySender on the VivePuck or other actor you want data from.  You can also use the right-click "attach to" menu to attach SingleTelemetrySender to another actor.

If you are running TelemetryViewer on the same computer as unreal, that's it, the defaults will get you started.

## MultipleTrackerTelemetry to send all your trackers

The MultipleTrackerTelemetryExample level shows this.  It sends data for ALL the VivePuck actors in your level.  The default is a maximum of 8, If you have more you will only get telemetry from the first 8, unless you customize your setup.

To use just drop it into your level, use the defaults to get you started.

MultipleTrackerTelemetry will automatically find your VivePuck actors and send data from all of them.  To organize things you need to number your VivePuck actors.  Go into each VivePuck object, under "details" and set "Telemetry Order" to 1, 2, 3 and so on for each VivePuck.

## Running TelemetryViewer

Just double click TelemetryViewer, if it does not launch you may not have a recent JRE (Java Runtime Environment) installed.  See Farrellf's site for more info if you don't know what this is.

Press the "Import" button in the lower left and navigate to the folder you launched TelemetryViewer from.  If you are using SingleTelemetrySender choose SingleTelemetryForOneActor.txt  For MultipleTrackerTelemtry choose MultipleTrackerTelemetryFor8Trackers.txt.

A green bar should appear at the top of the TelemetryViewer screen saying it is ready.  Now press "Play" in Unreal and you should see the graphs start updating.

You can scroll back and forth in time using the scroll wheel of your mouse or zoom in and out by holding down the Ctrl key and turning the scroll wheel.

When you "stop" your unreal app, it takes a few seconds for TelemetryViewer to reset, then you can just re-start unreal and it will reconnect.

# Testing your tracker setup

Sometimes the base stations may not be fully covering your room or there can be reflections of the tracking lasers from shiny objects, windows or monitors.  Or people may walk between the tracker and base station.  This can cause low quality or complete drop-outs of tracking in some parts of the room.

The best way to debug this is to use the MultipleTrackerTelemetryExample map setup to see data from all your trackers.  Then move trackers around the room and watch the screen to see exactily where in the room you have problems.  You may want to set TelemtryType to "Raw Tracker Relative" this will make it easier to see glitches.

To see the amount of noise your tracker receives, put it on a table, the floor or tripod and let it sit.  The wiggling of the charts is the noise.  It's normal to see noise in the X,Y,Z values of about 0.02 (two hundredths of a centemeter).  If yours is worse you might have a problem.

It may make it easier to test if you hookup a webcam to TeletryViewer so you can see where you were in the room when problems happened.

The telemetry sending actors will work in any project with any frame rate.  If you want really detailed and clean data when testing your setup, use one the simple tracker telemetry example maps and set a fixed frame rate of 60 or higher in the project settings.  Try to pick a frame rate your computer can maintain.

# Advanced Telemetry

## Customizing TelemetryViewer charts

You can change around TelemetryViewer's charts and graphs however you like.  The layouts I provide are fairly basic, you can easily change them.  Check out Farrellf's [latest video](https://youtu.be/FqfgBnCdrTo) for tutorials on how to use the program.

TelemetryViewer can also capture video from a webcam or network camera along with the telemetry data, this lets you see what was happening in the room at the time the data was recorded.

## More than 8 VivePucks

To support more than 8 VivePucks you will need to customize TelemetryGrapher.  By pressing the disconnect and connect buttons in the lower left corner you can see a screen with the layout of the message I send.  To make a setup for more than 8 trackers you will need to add more lines to this table, 6 float32's for each additional tracker.  You will also need to change the layout of the screen so it can display more than 8 sets of graphs.

In MultipleTrackerTelemetry's "details" set "maximum pucks" to the number of pucks you setup in TelemetryViewer.  The value of maximum pucks must match your TelemetryViewer setup.

## Custom telemtry

You may want to send telemtry from something else in your level like a lens tracker or a simulated vehicle.  If you take a closer look at my SingleTelemetrySender you can use it as an example of how to send other kinds of data to TelemetryViewer.  For example in a game you could send info on a vehicle's suspension system, where players were in the level...etc

## Telemetry from lots of objects or multiple computers with COSMOS

If you have a complex virtual production setup with multiple cameras, video walls, Ndisplay setups and different tracking systems it's possible to send telemetry from all of them to one place!  This can be really helpful for keeping a complicated system running smoothly and knowing if anything is out of whack. Everything is automatically archived to disk and can be replayed later.

https://cosmosrb.com/ is an advanced telemetry system used by NASA and other aerospace companies.  It's realtime graphs aren't as fast as TelemetryViewer but it can do way more.  Almost any device can send it Telemetry over network, serial and other types of connections.  Any message, any format and one device can send more than one kind of message.

You can build screens to monitor a whole system and automatically check to make sure all the values it's receiving are "in range" so you can have a status board for the whole studio and if anything goes out of spec (like a drop in frame rate), an indicator will light up red to let you know.

Cosmos can also SEND commands to devices, so you can setup screens with buttons and other controlls to turn systems on and off.

It's been well tested in "mission critical" aerospace applications and is pretty much totally bulletproof.  You could build your own telemetry system but it's not going to be as well tested and flexible as this.

It's only real flaw is that visually it's not as "pretty" as telemetry viewer, but if you need an advanced system to monitor the whole studio it's the place to go.

