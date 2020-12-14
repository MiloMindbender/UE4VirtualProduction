# VPStudio Virtual Production project

VPStudio is my latest project, all the features of my older projects are in here now so please use this one. Feel free to use anything here in your own projects, if you can please credit me, Greg Corson, for helping you out.  Tested on unreal 4.25, not tried on 4.26 yet.

Subscribe to [my youtube channel](https://www.youtube.com/user/GregCorson) for updates, tutorials and demos of virtual production. You can also ask for help on [this discord channel](https://discord.gg/ReEhkhc)or this [facebook group](https://www.facebook.com/groups/virtualproduction)

# What's new in Release 5 (COMING SOON)

For past releases check out the [releases page](https://github.com/MiloMindbender/UE4VirtualProduction/releases)

* Added a way to view tracker data, handy for debugging tracking problems like dropouts or jitter.  This uses a Java program [telemetry viewer](http://farrellf.com/TelemetryViewer/) see the [the author's channel](https://www.youtube.com/channel/UC_vO52hFzjMd2bPQA5AaHhg) for info and tutorials on it.  [This](https://youtu.be/FqfgBnCdrTo) is the most recent one.  You can use telemetry viewer on the same computer you are running Unreal on, or any other machine on your network (including Raspberry Pi 4). I include a copy of v0.7 of telemetry viewer, you need to install a Java [JRE](https://adoptopenjdk.net/) if you don't already have one installed. See the "tracker telemetry" level for an example.

* You can now record stats on your trackers like the standard deviation (a measure of jitter) min/max and other info by attaching a TrackerStats actor to your tracker.  Just add a TrackerStats actor and use the "attach to" function to attach it to a VivePuck actor. You can get stats from multiple trackers, just attach a TrackerStats actor to each one. See the "tracker stats" level for an example of getting stats from 4 trackers.  

* In MeasuringGuides there is a "MeasuringGrid" actor that draws a grid of squares to help you align cameras with a real world object like a checkerboard or cutting mat with a grid on it.  You set the size of the squares in cm and the number of squares horizontal and vertical.  To use just drop into the level.  You can attach it to a VivePuck actor and the grid will go wher ever the Vive Puck goes.  The "Grid Adjustment" node inside the actor lets you rotate or shift the grid.

* In MeasuringGuides there is a "MeasuringGadget" actor.  This uses a second vive tracker to get a quick measurement of your camera rig.  This can save setup time since you don't have to measure and build your own camera rig actor.  To use first setup a VivePuck actor, attach an AutoRig actor to it and a VPCamera actor to the AutoRig.  Then setup another VivePuck actor for doing measurements.  The sample level has a MeasureingGadget and Camera 2 in VPStudio setup for this.  To do a measurement PUT THE LENSCAP ON your camera and hold the vive tracker centered on it, then press V.  It will take 100 samples from both trackers and load the offset into the AutoRig's "Measured" values.  You will still need to figure out your lens's entrance pupil and tweek the rig for that, but this saves a lot of time.

* In CameraRigs there is an AutoRig actor for use with the MeasuringGadget actor.  The "measured" entries in this actor are for your rig measurements.  The "adjust" entries are for making small adjustments, for example if the tracker is slightly twisted or tilted on the rig.  This is usually easier than getting the physical rig exactly right. The "MeasuringGadget" will automatically set the measurements or you can put them in manually.

* The experimental "MeasureMe" actor has been removed and replaced by "MeasuringGadget"

* The old entrance pupil map has been removed, it was just used for filming a tutorial and was way out of date.

* Removed the old tracker and non-rotating tracker as they were out of date.  If you need to make an actor that copies only the position and not rotation from a tracker, see the "plumb line" actor for an example.

# Updating to New Releases

Always keep KEEP BACKUP copies your projects BEFORE you try to update!!!

The github is updated FREQUENTLY. Please use the [latest release from the releases section](https://github.com/MiloMindbender/UE4VirtualProduction/releaseshere) or clone the repository from the latest release tag.  If you just clone the project or download a ZIP from the main page, you may get a work in progress version that is not debugged yet.

If you have customized an older VPStudio for your own hardware I don't know of a good way to update it without wiping out the changes you have made.  Please keep a record of the changes you made so you can apply them to each new release.  If anyone knows of a good way to solve this problem, please let me know.  Sorry but there are so many different setups people might have, I can't make the project plug-and-play with all of them.

I recommend you start with a clean copy of VPStudio, get it running on your hardware and save it.  Don't add or change any content till the sample works for you.  Then save the running VPStudio and don't change it.  To add your own content, make a copy of this running VPStudio and migrate or import your content into it.

# The sample level IS boaring!

A lot of content, even "free" stuff, is licensed so you can use it in your own games and videos but you CAN NOT redistribute it to other people.  So I can't give you all the content used in my demos.  My sample project uses just the content built into Unreal.  See the [use your own sets tutorial](https://youtu.be/trlpmm5gI6U) on my YouTube channel for help on using your own content.  Almost all the demos on my channel were done with Epic "free" content that you can download yourself and use with VPStudio.  Epic releases new free content every month.

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

Right now to switch between "Virtual Production Filming" mode and just inspecting the set has to be done by going to the "VPStudio Comp" actor and setting the output pass to "Player Viewport" for filming or "none" for inspecting.  I haven't been able to find a way to do this with a keyboard key yet.

The way my dual camera setup works is inefficient as it always rendering both camera views.  If you are only using one camera you should delete the composure passes and mattes for camera two and things will be faster.

# Features

* Keyboard, mouse and Vive commands go through Edit->Project Settings->Engine->Input so they can be changed. You can change the keyboard key functions and the speed of movement on this page.  You can also add support for any input device you have by adding it here, this would include things like PC game controllers, joysticks and VR controllers.  

* Multiple cameras and video sources are supported.  This lets you have more than one camera view of your talent and live switch between them.  The project is setup for 2 cameras, adding more requires some blueprint and composure changes but I am working to make this simpler.

* An "inspection camera" gives you a 3rd person view of your level with all the tracking running.  This is useful to see if your cameras and other tracked objects are appearing in the right places and tracking correctly.  This camera can be moved with the mouse and wasd keys.

* Multiple "Talent Markers" are supported.  Position these markers where you want your talent to appear in the level.  When you have more than one you just press a key and your talent, cameras and other tracked objects will teleport to the new location in the level.  This is just a quick cut, no transition effects (like fade in/out) yet.  Add more talent markers just by dragging them into the level and naming them TalentMark1...TalentMark2...etc.

* Tracking and tracker-delay functions are inside the "Tracker" actor.  Each tracker actor can have a different delay.  The output of the tracker automatically connects to any objects "attached-to" it in the world outliner.  The supplied tracker actor is for the Vive but you can make your own to support other tracking systems like optitrack, pan/tilt mechanical trackers or stationary cameras.

* All the control and UI functions are inside the "PlayerController" now.  So everything is in one place and easy to change.

* You can move the talent markers around using keyboard key to get the right placement of them in your level.  This can be done live while the composite is running and you will see the talent moving through the level.

* In the "Measuring Guides" folder there are several objects you can attach to trackers to make lining up the real/virtual parts of your level easier.  This includes a 1M cube, 1M square, a 2M high measuring scale, a plumbline that will always be vertical and some axis arrows.  The AxisGuideWorld will always point to the world X,Y,Z with no rotations.  TalentMarkMan is 193cm tall or about 6'3".

* VPCamera1 and VPCamera2 are setup to be controlled by VIVE trackers set to Special_1 and Special_2.  If you want to use some other controller just change the source in the camera's motion controller component.  For example "left" or "right" if you want to use the hand controllers.

* The setup should still work if you have only one camera.  Just don't use the "switch to camera 2" feature.

* The camera "rig" actors I've provided have variables for making small adjustments to the joints of the rig.  This is to correct for minor tracker rotation issues such as the tracker being slightly rotated on it's 1/4-20 tripod thread or on a ballhead mount you couldn't get exactly straight.  It is meant for very small adjustments of a few degrees at most and is not perfect, but if your tracker is slightly out of alignment using this can bring it back without having to mess with the mount itself.  The ones I included represent my actual camera rigs and only have these adjustments at places that can move.

* There is a garbage matte setup for use with a greenscreen that covers a wall and floor.  If your greenscreen has a different shape, you can model it and add your own mesh for a better fit.  There is a tutorial on my youtube channel that shows how to adjust the garbage matte to match the size of your greenscreen.

* A HUD with guides useful for aligning cameras if your camera doesn't have guides or has no screen.

# Planned (NOT done yet)

* Since you can move the talent markers and inspection camera interactively, I will be adding a way to save their positions between runs of the project.

* Adding or removing cameras requires editing the composure setup and PlayerController blueprints to add more.  I'm working on making this easier to do.  Right now it is setup for 2.

* There is no setup for a "pro video output card", because I don't have one.  See [step 6 here](https://docs.unrealengine.com/en-US/Engine/Composure/QuickStart/index.html) to see where to make the change in composure.  I capture output from my NVIDIA card's HDMI output.

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

# Bugs and Suggestions

I welcome suggestions on how to make this simpler or more efficient.  You can use the github issues tracker or post to my YouTube channel if you find bugs or have feature requests.

