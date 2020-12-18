# VPStudio Virtual Production project for Unreal 4.25

VPStudio is my latest project, all the features of my older projects are in here now so please use this one. Feel free to use anything here in your own projects, if you can please credit me, Greg Corson, for helping you out.  This is probably the last release for Unreal 4.25, the next will move to 4.26 which has a lot of useful new features.

Subscribe to [my youtube channel](https://www.youtube.com/user/GregCorson) for updates, tutorials and demos of virtual production. You can also ask for help on [this discord channel](https://discord.gg/ReEhkhc)or this [facebook group](https://www.facebook.com/groups/virtualproduction)

# What's new in Release 5 (COMING SOON) [older releases here](https://github.com/MiloMindbender/UE4VirtualProduction/releases)

* A lot of renaming and reorganizing into folders to make the example easier to understand and change.  A lot of obsolete and test content was removed too.

* You may get a prompt asking you to install "TCP Socket Plugin", free on Unreal Marketplace from SpartanTools.  If you don't install it, everything but telemetry will still work.

* ViveTracker actor was renamed "Tracker".  Now it works with Vive Tracker Pucks and Hand Controllers, displaying the right 3d model with tracking delay applied. There are some new settings in the tracker details, described below.

* ViveTracker's "Tracker Type" setting controls which tracker model is displayed.  It also adjusts the transform to have what most people consider the right "up" and "front" orientation for the type of tracker.  You can update this to support more types of trackers or different transform adjustments.

* If ViveTracker's "Tracker is Lockable" setting is checked the tracker can be turned off or "locked down" at any time by pressing a key.  If you are shooting with stationary cameras you can have everything unlocked while you setup your camera positions, then lock them to prevent any tracking jitter.  Don't check this for trackers attached to things you want to move during the shoot, like a hand-held camera or other object.

* ViveTracker's "Telemetry Order" is used for sending your tracking info to a program outside of Unreal for monitoring.

* The "MotionStats" actor is for testing trackers. Add a MotionStats actor to the level and use the "attach to" function to attach it to a tracker.  Make sure the tracker is stationary, then press "play". MotionStats will record movement for a bit and then print out the average, minimum, maximum, spread and standard deviation values for X, Y, Z, Roll, Pitch and Yaw of the actor, these will appear on the screen and in Window->Developer Tools->Output Log.  Standard deviation is a measure of how much "jitter" the tracker has, lower is better.  If you want to test multiple trackers all at once, just create and attach a MotionStats actor to each one of them.  You can set the number of frames to record (1000 is the default, 15-40 seconds depending on frame rate).  MotionStats will work when attached to any actor but is mostly useful for testing trackers.

* There a system for sending tracker and other information (Telemetry) to another program that graphs it in real time.  This is useful for detecting and troubleshooting problems with tracking.  See the VPStudio/TelemetryViewer folder for more detailed documentation on this and the SingleTlemetrySender and MultipleTrackerTelemetry actors.

* The SingleTelemetrySender actor will send real-time X,Y,Z,Roll,Pitch,Yaw data to TelemetryViewer.  Add to your level and drop or "attach" it to the actor you want telemetry from.  Only create ONE of these or your telemetry may be corrupted.  See the SingleTelemetrySenderExample level for a sample.

* The MultipleTrackerTelemetry actor will find all your Tracker actors and send their telemtry to TelemetryViewer at once.  Only create one of these.  See the MultipleTrackerTelemetryExample level for a sample.

* The ExperimentalTelemetryTracker is not useful for you, it's for testing some ideas on filtering tracker data.

* The "MeasuringGrid" actor draws a grid of squares to help you align cameras with a real world object like a checkerboard or cutting mat with a grid on it.  In the details set the size of the squares in cm and the number of squares horizontal and vertical.  To use just drop into the level.  You can attach it to a VivePuck actor and the grid will go wherever the Vive Puck goes.  The "Grid Adjustment" node inside the actor lets you rotate or shift the grid.  There are some checkboxes to turn drawing of the grid and the axis guide on and off.

* The "AutoRig" actor is a generic camera rig you can quickly setup to work with most camera rigs.  The "measured" settings should be set to the measurements of your rig, then the "adjust" elements can be used to make fine adjustments if you find the measurements to be slightly off.  This also works with "MeasuringGadget" to automatically measure your rig.

* The "MeasuringGadget" actor uses a second vive tracker to measure your camera rig and apply it's settings to an AutoRig.  This lets you setup your rig very quickly.  I will put a link to a video tutorial here when it's ready.

* The "LaserPointer" actor projects a laser beam forward till it hits something.  To use, just attach it to a tracker actor.  The blueprint for this actor finds a lot of information about the actor it hits. You could add to the blueprint functions to select, change the target actor or turn the laser beam on and off.  You can set the maximum length of the beam in details.

* The experimental "MeasureMe" actor has been removed and replaced by "MeasuringGadget"

* The "Laser" actor was removed and replaced with "LaserPointer" which works better.

* The old entrance pupil map has been removed, it was just used for filming a tutorial and was way out of date.

* Removed the old tracker and non-rotating tracker as they were out of date.  If you need to make an actor that copies only the position and not rotation from a tracker, see the "plumb line" actor for an example.

# Updating to New Releases

Always BACKUP your old VPStudio and other projects before trying to update them!

I don't use the number.number.number style of version numbering.  All my releases are numbered with integers starting at 1, the largest release number will be the latest one.  Changes may be large or small, check the release notes for details.

The main branch of github is updated FREQUENTLY, cloning or downloading a ZIP from the main github page may get you unfinished and untested code.  Please use the [latest release from the releases section](https://github.com/MiloMindbender/UE4VirtualProduction/releaseshere) or clone the repository from the latest release tag.

VPStudio has to be customized for your hardware, so it's important to keep track of the changes you had to make for it to work on your setup.  Usually these are small and can be quickly copied over to the new VPStudio.

I recommend you start with a clean copy of VPStudio, get it running on your hardware and save it.  Don't add or change anything but what you need to do to get it running.  Save this and don't change it.  To use it with your own content, make a copy of your working VPStudio and copy your own content to it. 

# The sample level IS boaring!

A lot of content, even "free" stuff, is licensed so you can use it in your own games and videos but you CAN NOT redistribute it to other people.  So I can't give you all the content used in my demos.  My sample project uses just content built into Unreal.  See the [use your own sets tutorial](https://youtu.be/trlpmm5gI6U) on my YouTube channel for help on using your own content.  Almost all the demos on my channel were done with Epic "free" content that you can download yourself and use with VPStudio.  Epic releases new free content every month.

If you are an artist and would like to help by contributing a better sample level under creative commons license, please let me know.

# Setup VPStudio

Right now VPStudio is setup for an AJA Kona HDMI video capture card and VIVE trackers.  If you have a BlackMagic DeckLink or other card/webcam you will need to replace the assets found in the Aja folder with ones for your hardware.  Look at [Unreal Pro Video](https://docs.unrealengine.com/en-US/Engine/ProVideoIO/index.html) for how to set up different BlackMagic and Aja cards. [Using WebCams](https://docs.unrealengine.com/en-US/Engine/MediaFramework/HowTo/UsingWebCams/index.html) shows how to use most USB webcams.  If you are not using VIVE hardware, you will have to make your own tracker actors.  See VPStudioCore->Trackers folder for examples.

Follow [tutorial 1](https://youtu.be/wWPZjX29asM) and [tutorial 2](https://youtu.be/kRUbUaESw80) to make a rig in Unreal that shows how your camera and tracker are mounted.  There are sample rigs in VPStudio but if they don't match your camera/lens/tracker setup you won't get good alignment of real and virtual objects in your scene.  [Tutorial 3](https://youtu.be/4LjvekNocD4) shows how to setup VIVE controller buttons to control things.  Make sure your VIVE trackers are setup to Special_1, 2, etc. as shown here. [Tutorial 4](https://youtu.be/UGHjwZ6J13E) shows how to setup the studio and fine tune your camera and tracker alignment [totorial 5](https://youtu.be/trlpmm5gI6U) shows how to add your own sets and assets to a copy of VPStudio.
 
# Using your own levels

[Tutorial 5](https://youtu.be/trlpmm5gI6U) shows how to add your own sets and assets to a copy of VPStudio.
 
You make a copy of a working VPStudio project and then "migrate" your level into it.  Once you have your level migrated, you use the "levels" window in the editor to add VPStudioCore as a sublevel and you are ready to go, see the tutorial for more details.

Some levels may do things with lighting that make them appear too bright or too dark.  For now you're on your own about fixing this, I don't have any good advice (yet).

# Known Problems

Under Edit->Project Settings->Project->Maps & Modes I provide a VPPlayerController that manages all user input and controls everything.  This is required or nothing will work.  If you want to use this project with a level that requires it's own PlayerController you will need to figure out how to combine mine and yours. I also provide a VPGameState and VPGameMode which are currently EMPTY and not required.  Though in the future this may change.  

Every time you recompile a VPCamera asset, Unreal disconnects the cameras from the composure passes.  If you recompile these you will have to go back into VPStudioBackground 1 & 2 and the GarbageMatte 1 & 2  and set the "camera source" to override and the Target Camera Actor to VPCamera 1 & 2.

Switching between "Virtual Production Filming" mode and just inspecting the set has to be done by going to the "VPStudio Comp" actor and setting the output pass to "Player Viewport" for filming or "none" for inspecting.  I haven't been able to find a way to do this with a keyboard key yet.

My dual camera system is always rendering both camera views.  If you are having trouble hitting the frame rate you want, go into Window->Composure Compositing and turn off any composure passes you aren't using.  If you only have one camera turn off everything numbered "2".  Depending on what you are filming, you may not need to render all the foreground, background and garbage matte passes either.

# Features

* All commands go through Edit->Project Settings->Engine->Input so they can be changed. You can change the keyboard keys assigned to functions and the speed of movement on this page.  A function can be mapped to almost any input device you have including PC game controllers, joysticks and VR controllers.  

* Multiple cameras and video sources are supported.  This lets you have more than one camera view of your talent and live switch between them.  The project is setup for 2 cameras, adding more requires some blueprint and composure changes but I am working to make this simpler.

* An "inspection camera" gives you a 3rd person view of your level with all the tracking running.  This is useful to see if your cameras and other tracked objects are appearing in the right places and tracking correctly.  This camera can be moved with the mouse and wasd keys.

* Multiple "Talent Marker" are supported.  Position one where you want your talent to appear in the level.  If you have more than one you just press a key and your talent, cameras and other tracked objects will teleport to the next location in the level.  

* Tracking and tracker-delay functions are inside the "Tracker" actor.  Each tracker actor can have a different delay.  The output of the tracker automatically connects to any objects "attached-to" it in the world outliner.  The supplied tracker actor is for the Vive but you can make your own to support other tracking systems like optitrack, pan/tilt mechanical trackers...etc

* You can move the talent markers around using keyboard key to get the right placement of them in your level.  This can be done live while the composite is running and you will see the talent moving through the level.

* There are a number of measuring and setup guides to help you measure your real world studio and align it with your virtual set.  This includes a plumbline that always points straight down, "axis guide world" which is always lined up with the world and some tools to automatically measure your camera rig.  TalentMarkMan is 193cm tall or about 6'3", you can rescale it to match the size of your talent.

* The "rig" your camera and trackers are mounted to can be modeled in the system to exactly match your real-world rig.  This includes things like multiple joints that could be moved by a tracker or might need to be "tweaked" if the rig is slightly out of alignment.  A few samples of different rigs are provided.

* There is a garbage matte setup for use with a greenscreen that covers a wall and floor.  If your greenscreen has a different shape, you can model it and add your own mesh for a better fit.  There is a tutorial on my youtube channel that shows how to adjust the garbage matte to match the size of your greenscreen.

* A HUD with guides useful for aligning cameras if your camera doesn't have guides or has no screen.

* You can turn tracking of stationary objects on and off to avoid seeing the jitter that some trackers have when sitting still.


# Keyboard Keys

For the keyboard/mouse/vive tracker commands to work you need to have clicked in the player viewport or PIE window.  To get control back just hit shift-F1 or ESC to quit.

These are what the keyboard keys currently do, if you want to change them go to Edit->Project Settings->Engine->Input.

Right now switching between "Virtual Production Filming" mode and  inspecting the set has to be done by going to the "VPStudio Comp" actor and setting the output pass to "Player Viewport" for filming or "none" for inspecting.  

When you first press PLAY you will either be looking at the composure composite or in inspection mode.  All the movement keys will be setup to move the inspection camera so you don't accidentally move anything else while you are filming.

Depending on what mode you are in, you can move talent markers or the inspection camera around.  Use the standard Unreal W, S, D, A keys for forward, back right and left movemtnt.  E and C moves up and down.  Use the mouse to look around (pan tilt).

To change to Virtual Production camera one, press 1 or left-click the right hand vive controller trackpad.  For camera two, use 2 or click right on the trackpad.

The N key or Vive controller trigger teleports you to the next TalentMark.  You can have as many of these as you want, just drag them into the level and number them 1, 2, 3 and so on.  When you press this key all your tracked objects & cameras will jump to the next mark and your talent will appear in that spot.

The M key switches between VPCamera "raw" views.  This gives you a view from each of your cameras but without any live composite, you will only see the CG part.  (only works when VPStudioComp output is set to NONE)

The I key switches to the inspection camera.  This is just a free floating camera that lets you look around the level while all the cameras and tracked objects are running so you can see if they are working and in the right places. (only works when VPStudioComp output is set to NONE)

The T key toggles between moving the inspection camera and moving the talent marks.

y, u, p, o and k keys will toggle visibility of TalentMark, MeasuringGuide, CameraModel, CameraRig and Tracker actors

When VPStudioComp output is set to "player viewport" you will see the full composite output of live cameras and the CG background.  The 1 and 2 keys switch between VPCamera1 and VPCamera2

Press b or click the right VIVE controller trackpad down to take a screenshot.  This is the same as typing "shot" into the editor command window.

The H key brings up the hud with camera alignment guides.

The L key locks down all the trackers you have set to be "lockable"

# Bugs and Suggestions

I welcome suggestions on how to make this simpler or more efficient.  You can use the github issues tracker or post to my YouTube channel if you find bugs or have feature requests.

