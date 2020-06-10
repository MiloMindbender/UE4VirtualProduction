# READ SO YOU DON"T LOSE WORK! UNREAL 4.25.1 BUG

There is a bug in 4.25.1 that causes an editor crash. If there are mediabundles in the current level and and you open a new level the editor will crash and lose everything till the last save.  Epic is working on a fix that should be in 4.25.2  Till the fix is released I will be checking this project in without media bundles in the level to avoid accidental crashes and lost work.

You can still use the level for Virtual Production, just drag the two media bundles from the AJA folder back into the level.  But once you do this DO NOT try to switch levels or it will Unreal will crash.  Delete the media bundles from the level (NOT from content browser) and you should be able to switch levels again.

# VPStudio is a WORK IN PROGRESS, NOT FULLY FUNCTIONAL

This is my new template for doing Virtual Production.  The goal of this template is to make it easier for people to understand how it works.  I am also trying to make it easier to setup and customize for your hardware and studio as well as including some virtual camera rigs that may be useful.

Just remember, I'm still working on this and things could change on an almost daily basis.  So feel free to look at it and make comments on things you think need to be added or changed...but don't expect it to be stable for day-to-day production use YET!  Please feel free to use any of the bits and pieces or ideas you find here in your own projects, just please credit me, Greg Corson for whatever stuff you take.

There will be a full tutorial video on my YouTube channel for this, but not till the main features are done and stable.

# Features

Keep in mind all these are subject to change!  Remember for keyboard/mouse to work you need to have clicked in the 3d viewport.  To get control of your computer back just hit shift-F1 or ESC to quit.

* All user commands go through the Engine->Input system so they can be easily changed.  Right now keyboard and mouse is used but you can easily add support in Engine->Input for any kind of controller device that Unreal supports.  This includes buttons on VR controllers, joysticks and PC game controllers.  You can also change which keyboard keys control which functions.

* To see/change all the control keys, go to Edit->Project settings and then open Engine->Input

* Multiple cameras and video sources are supported.  This lets you have more than one camera view of your talent and live switch between them.  Currently the project is setup for 2 cameras, adding more requires some blueprint and composure changes but I am working to make this simpler.

* There is an "inspection camera" to give you a 3rd person view of what is going on in Unreal.  This is useful if you want to see if your cameras and other trackers are pointed in the right direction and moving.  This is a live view so if your tracked cameras move you will see them move.  This camera can also be moved around while the project is running.

* Multiple "Talent Markers" are supported.  You position these markers where you want your talent to appear in the level.  Setting up more than one lets you press a key and teleport your talent to a new spot in the level.  All the cameras and other objects will follow.  This is just a quick cut, no transition effects (like fade in/out) yet.  You can add more talent markers just by dragging them into the level and naming them TalentMark1...TalentMark2...etc.

* All the tracking and tracker-delay functions are now inside the VPCamera actor.  Each camera can have a different delay if necessary.  The old version required two actors and a global to do this, now it's all in VPCamera.

* All the control and UI functions are inside the "PlayerController" now.  So everything is in one place and easy to change.

* You can move the talent markers around using keyboard key to get the right placement of them in your level.  This can be done live while the composite is running and you will see the talent moving through the level.

* I've added several sample tracked objects as examples.  These can be handy for measuring things in your studio for setup or setting up a basic AR tracked object.

* VPCamera1 and VPCamera2 are setup to be controlled by VIVE trackers set to Special_1 and Special_2.  If you want to use some other controller just change the source in the camera's motion controller component.  For example "left" or "right" if you want to use the hand controllers.

* The setup should work as-is if you have less than 2 cameras (even none) you should not have to change anything.


# Planned (NOT done yet)

* Since you can move the talent markers and inspection camera interactively, I will be adding a way to save their positions between runs of the project.

* The composure setup currently does 2 cameras and requires editing of both the composure setup and PlayerController blueprints to add more.  I'm trying to figure out a way to make this easier or automatic.

* Currently the cameras and trackers are rendered as 3d objects all the time.  I will be adding a button to turn them on and off so they won't appear in the shot.  For now you can tick the "hidden in game" box on each object to make it invisible.

* The garbage matte isn't done yet.

* It is setup for an AJA Kona HDMI video input card right now.  You can change this to support a different card or webcam.  I am working on a setup so I can distribute setups for multiple types of cards and cameras to make it easier to configure it for whatever setup you have.

* There is no setup for a "pro video output card" because I don't have one to test.  You should be able to do this with minor changes.  See step 6 in this https://docs.unrealengine.com/en-US/Engine/Composure/QuickStart/index.html to see where to make the change in composure.  I currently capture output from my NVIDIA card's HDMI output.

* I have not figured out how to switch between Composure and other cameras outputting to the PlayerViewport.  Till I figure this out you need to do the switch manually by going into the composure output pass and changing the output between PlayerViewport and NONE.

* The composure setup may be rendering both camera views even though only one is visible.  I need to do some profiling work to make sure the views you CAN'T see are not stealing any rendering or CPU time.


# Bugs and Suggestions

Like I said, I'm still working on this.  I welcome suggestions on how to make it simpler or more efficient.  You can use the github issues tracker to comment on things if you like.  Remember this is in active development so there will occasionally be bugs, missing features and other problems.

