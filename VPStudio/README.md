# VPStudio Virtual Production sample project

My new Virtual Production project has many new features and is easier to setup. Feel free to use anything you find here in your own projects, please credit me, Greg Corson, for helping you out.

Please subscribe to [my youtube channel](https://www.youtube.com/user/GregCorson) and check it out for tutorials on Virtual Production.  You can also ask me for help on [this discord channel](https://discord.gg/ReEhkhc).

This is an active project and will be seeing new checkins FREQUENTLY.  I suggest you grab the latest release from the releases section here on github and keep a backup copy of it in case I change something that causes you issues.  If you clone the archive you will get the latest version but there might also be bugs or unfinished features.

# The sample level IS boaring!

Content from the Epic Marketplace and many other other places is licensed so you can use it in games and videos but you CAN NOT redistribute the assets.  Unfortunately, all the demos I've done so far have been done with their models so I can't redistribute them to you.  My sample only uses Unreal builtin content to avoid licensing issues and keep the project small.  I've tried to make VPStudio easy to use with your own levels so it shouldn't be too hard to add it to any level you have.

If you are an artist and would like to help by contributing original material under creative commons license, please let me know.

# Setup VPStudio

After you get VPStudio you need to set it up for your hardware.  Do this BEFORE trying to add your own stuff to the level. Right now it is setup for an AJA Kona HDMI video capture card and VIVE trackers.  If you have a BlackMagic DeckLink or other card/webcam you will need to replace the assets found in the Aja folder with ones for your hardware.  I will try to add a webcam setup to this soon.  I don't have any BlackMagic hardware to work with so I can't do a setup for that.  Look at [Unreal Pro Video](https://docs.unrealengine.com/en-US/Engine/ProVideoIO/index.html) for information on setting up BlackMagic and Aja cards and [Using WebCams](https://docs.unrealengine.com/en-US/Engine/MediaFramework/HowTo/UsingWebCams/index.html) for info on webcams.  If you are not using VIVE hardware, you will have to make your own tracker actors.  See VPStudioCore->Trackers folder for examples.

Follow [tutorial 1](https://youtu.be/wWPZjX29asM) and [tutorial 2](https://youtu.be/kRUbUaESw80) to make a rig in Unreal that shows how your camera and tracker are mounted.  There are sample rigs in VPStudio but if they don't match your camera/lens/tracker setup you won't get good alignment of real and virtual objects in your scene.  [Tutorial 3](https://youtu.be/4LjvekNocD4) shows how to setup VIVE controller buttons to control things.  Make sure your VIVE trackers are setup to Special_1, 2, etc. as shown here.

You also need to setup the location of your greenscreen and a few other things.  Tutorials on this for VPStudio are coming, for now you can look at my older tutorials for advice.
 
Once VPStudio is working with your trackers and studio setup, keep this version as a backup and use the Epic launcher "clone" function to create a copy you can add stuff too. 

# Using your own levels

Some Epic Marketplace content has an "add to project" button you can use to add it to your VPStudio project.  To add content from another project, open it and use the editor "migrate" function to move content or whole levels into your VPStudio project.  Doing it this way will make sure all the plugins and other settings needed are properly setup.  You can also migrate the VPStudio content into your own project, but you might miss some important setup if you do.

VPStudio uses sublevels to make adding Virtual Production features to your own level easier.  Start by opening the level you want to do virtual production on.  Go to window->levels to open the levels window.  You will see just "persistent level" which is the one you just opened.  Under Levels, select "default streaming method" and set it to "always loaded".  Then under Levels select "add existing" and browse to VPCoreMap.  When you load this all the Virtual Production actors should appear in your level and be ready to use.

Some levels may do things with lighting that will make them appear too bright or too dark.  For now you're on your own about fixing this, I don't have any good advice (yet).

# Known Problems

Under Edit->Project Settings->Project->Maps & Modes I provide a VPPlayerController that manages all user input and controls everything.  This is required or nothing will work.  If you want to use this project with a level that requires it's own PlayerController you will need to figure out how to combine mine and yours. I also provide a VPGameState and VPGameMode which are currently EMPTY and not required.  Though in the future this may change.  

Every time you recompile a VPCamera asset, Unreal disconnects the cameras from the composure passes.  If you recompile these you will have to go back into VPStudioBackground1 & 2 and the GarbageMatte1 & 2  and set the "camera source" to override and the Target Camera Actor to VPCamera 1 & 2.

Right now to switch between "Virtual Production Filming" mode and just inspecting the set has to be done by going to the "VPStudio Comp" actor and setting the output pass to "Player Viewport" for filming or "none" for inspecting.  I haven't been able to find a way to do this with a keyboard key yet.

The way my dual camera setup works is inefficient and is probably always rendering both camera views.  If you are only using one camera you may want to delete the composure passes for camera 2 to speed things up.

# Latest Revisions

All the release notes have been moved to the releases page on github, please check there for new features and fixes.  From now on I'll be making a release every time I get to a clean and usable spot in development.

Release 2

This release contains some small fixes to make the import/migrate demo work right.

* Set all the chroma key, despil and erode passes to be on by default

* I key was mapped to two functions (inspection camera and hide trackers) remapped so hide trackers is now K key.

* The two AJA media sources should have been part of the core map, moved them there.

# Features

Keep in mind all these are subject to change!  

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

* There is no setup for a "pro video output card", I don't have one to test.  You should be able to do this with minor changes.  See [step 6 here](https://docs.unrealengine.com/en-US/Engine/Composure/QuickStart/index.html) to see where to make the change in composure.  I capture output from my NVIDIA card's HDMI output.

* Eventually I will be find a way to switch between "filming" and "inspecting" with a keyboard key.

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

I'm still working on this.  I welcome suggestions on how to make it simpler or more efficient.  You can use the github issues tracker to comment on things if you like. 

