# READ SO YOU DON"T LOSE WORK! UNREAL 4.25.1 BUG

A bug in 4.25.1 can cause an editor crash. If there are mediabundles in the current level and you open a new level the editor may crash.  Epic says the fix will be in 4.25.2  If you notice any crashes while switching levels, just delete the media bundles from the level you are switching FROM and it should work.

# VPStudio is a WORK IN PROGRESS and may change in major ways without notice

My new Virtual Production project is easier to setup and customize for your studio and it has many new features.  

It will change almost daily.  Please take a look at it and make comments on anything you think could be improved.  Feel free to use anything you find here in your own projects, just please credit me, Greg Corson, for whatever you use.

A series of tutorials on this project are on [my youtube channel](https://www.youtube.com/user/GregCorson).

# What a boaring level!

The included level is very basic because of content licensing.  Content from the Epic Marketplace and many other online stores allows you to use it in games and videos, but you CAN NOT distribute as part of an open Unreal project.  This sample only uses content built into Unreal, so no licensing issues and it keeps the project small.  I'm working with artists to make a few virtual production sets we can give away, but they are not done yet.  If you are an artist would like to help by contributing original material under creative commons license, please let me know.

You CAN buy or use content from the Epic's Unreal marketplace in your own work, but YOU have to get it from Epic yourself, their licensing will not allow me to host the content here.

# Recommendations for Use

Every time you check this out from github there could be big changes.  I recommend you keep an UNCHANGED copy as a backup.  If I make a change that isn't compatible with what you are doing, you will have your saved version to go back to.

If you are checking out or cloneing the github repository, I recommend you don't make changes in the directory you checked out.  Make a duplicate, fork or in the unreal launcher, a clone of the project to work on.  That way if I make a change and you check it out, it won't overwrite work you've done.

# Use with your own levels

To use this project with your own levels, migrate your level into this project.  This will make sure all the plugins and other project settings needed for Virtual Production will already be set for you.  You can also migrate this project into your own project, this is a bit more complicated because you will have to change a lot of plugin and editor settings before migrating or it will fail.  The "migration tutorial" on my YouTube channel should still work for this new template.

# Known Problems

Under Edit->Project Settings->Project->Maps & Modes I provide a VPPlayerController that manages all user input and controls everything.  This is required or nothing will work.  If you want to use this project with a level that requires it's own PlayerController you will need to figure out how to combine mine and yours. I also provide a VPGameState and VPGameMode which are currently EMPTY and not required.  Though in the future this may change.  

Every time you recompile the VPCamera asset, Unreal disconnects the cameras from the composure passes.  If you recompile these you will have to go back into VPStudioBackground1 & 2 and the garbage matte passes and set the "camera source" to override and the Target Camera Actor to VPCamera 1 & 2 again.

Right now there is no way to switch between "Virtual Production Filming" mode and just looking around the set mode with a keyboard key.  You have to go to the "VPStudio Comp" item and find the output pass.  Set the output to "none" if you just want to look around, or "player viewport" to see the composite output.

# Latest Revisions

7/17/2020

This includes some new stuff I added to film the mad scientist lab demo.

The right hand vive controller can now be used to control some of the demo functions.  Clicking left or right trackpad will select camera 1 or 2.  Pulling the trigger moves to the next talent mark.  Clicking down on the trackpad or pressing B on the keyboard will take s screenshot (this is useful for checking the key, focus...etc if you are working by yourself).

I've put some materials on things like the floor and the spheres/cones/cubes in the scene.  This makes it easier to see all the objects.  The green screen object is now green.

The talent mark texture now has an arrow showing which way the talent should be facing.

7/5/2020

After testing with a different virtual set, realized all the stage elements (inspection camera, color reference...etc) should be attached to TalentMark1.  If you migrate a new map into this template it makes it easier to get everything to the right position, you just move the talent mark.

6/28/2020

Major refactoring of the tracker and camera rig system to remove some unnecessary rotations and transforms.  This was because vive trackers are setup so that their "front" or X axis when they are flat on the table is pointing up.  This caused any mesh or other object connected to them to be pointing the wrong way.  The tracker objects in VPStudio have had a 270 degree Y axis rotation added to their output to fix this.  Now when the tracker is setting flat on a table, up is the Z axis same in unreal.  The "front" positive X axis points in the direction opposite the USB plug.  If you used one of my earlier examples to build your own camera rig, you probably have this 270 degree rotation as the first node in your rig, this is no longer needed, you can set the rotations to zeros.

Added measuring and alignment tools.  Actors that can be attached to a tracker or placed in the world for reference.  Attach AxisGuide to anything to see it's local coordinates. AxisGuideWorld will always show the world x/y/z no matter what it is attached to or how it is rotated. There are two 1m objects you can use as references when aligning the camera with the virtual world.  These are examples, you should find a real world box and a square of material some fixed size and make your own versions of these references in that size.  Then you can compare the real world object and CG objects in a composite to see if they line up.  Both of my objects have the origin at top-center so if you attach them to a tracker object in unreal and set a Vive tracker on the real world object the CG reference object will appear in the same place.  There is also an actor called PlumbLine which will always draw a vertical line no matter what it is attached to.  If you hang a real plumb line from a vive tracker, the two vertical lines should match.  An axis guide attached to CameraRig will show the entrance pupil component (where the camera would be attached).  If you attach one to the tracker it will show the output of the tracker with any delay included.

The camera models have been adjusted so their origin is at the entrance pupil of the lens.  The A7R4 has a 24-70 F2.8 G-Master zoom attached with the entrance pupil set for it set to 24mm.  The UNCS3CA is setup for a 16-35 F2.8 G-Master with the zoom set to 16mm.  Note that camera models are just for reference when building camera rigs and setting up the studio.  They don't have anything to do with the alignment of the composite cameras so their measurements don't have to be exact.

There are 3 pre-built camera rigs, these represent the hardware used to attach your tracker to your camera and must have correct measurements.  One end of the rig is the point where the tracker attaches, the other is where the entrance pupil of your lens is.  You can make your own rigs however you like.  I have found it is helpful to put joints wherever your real-world rig can rotate or twist (like at a tripod screw or ballhead) and set them up as I have so you can make small adjustments easily.  If the real-world rig is out of alignment by as little as a degree it will be noticable, these adjustments let you correct that without having to fight to get the real-world rig parts perfectly aligned.  My rigs include the mesh of the vive tracker, this is just to make it more clear how the rigs are built, when you build your own you can leave the tracker mesh out.

Added a two-sided white material with a red X going through the center.  These are useful when making alignment objects.  It's also used on the greenscreen model to make it visible from both sides.

Added meshes for a Sony A7R4 camera and a VIVE tracker, these are not precise models but are fairly accurate.  Both models didn't come with the origin where it should be.  To have them appear in the right places, the Vive model needs to have it's origin at the tripod screw and the A7R4 needs it at the entrance pupil location of the lens.

Added TalentMarkMan with the unreal mannequin standing on it as a size reference.  This man is 193cm tall or around 6'3".  I suggest you rescale this to match your your talent's height so it will be a good size reference when putting the talent mark in a level.

Added VivePuckNoRotate which outputs a tracker position without any rotation.

The "entrance pupil" map was used in filming of the tutorials but at the moment is probably not useful for anyone.

There is a "laser pointer" actor.  It contains a motion controller you can hook to any tracking device, by default it is hooked to the right vive controller.  This actor will have a red laser coming from the tracker and stopping on the first object it hits.  Not really useful yet, but it is fun and can be used to point out objects in a virtual set if you are doing a tutorial.  Inside the blueprint it returns the actor the beam hit.

Added keys to toggle visibility of TalentMark, MeasuringGuide, CameraModel, CameraRig and Tracker actors.  Sometimes these are visible when filming so you want to turn them on and off easily.  Current default is ON.

6/19/2020

While recording the demo I noticed a few small errors and fixed them, mainly the garbage mattes were not attached to cameras, so they were not tracking.  There was also a small error in the A7R rig where the tilt axis was rotating the wrong way.

6/14/2020

Completely revised the tracking and camera system.  The system is similar to the built-in unreal "camera rig crane" but is implemented in blueprints instead of C++ code.  It is broken into several actors.  There is a tracker which handles the motion controllers (and any delay), one or more "rigs" that represent the structure attaching the tracker to the camera, the VPCamera which is the CineCameraActor and another actor with a model of the camera.  This change allows for multiple types of "tracker" actor such as Optitrack or a mechanical tracker.  It also allows multiple rigs to attach the tracker to the camera such as a hot-shoe mount or a ball head.  The rigs allow for the tracker to be setup in most any position and can have degrees of freedom which can be adjusted to account for something such as a ball head that is not perfectly aligned.  The default has the tracker, rig and camera models all visible but they can be easily turned off or set to be "hidden in game".  

Do not touch any transform nodes in a rig while it is running, this will detach the rig from the tracker and stop it from working.  Each rig is made mostly of solid parts, any place in the rig that can move will have a variable in details for adjusting it to correct for small alignment errors.

Both maps were updated to use the new camera components.  The virtual camera map is using the "sample" camera rig right now, if you are using this map you will want to make a rig that matches your camera.

The rig system could also be used to represent a fixed tripod with tracked joints, a crane/jib or something like a robot with a camera on the end of the arm.

# Features

Keep in mind all these are subject to change!  For the keyboard/mouse to work you need to have clicked in the 3d viewport.  To get control back just hit shift-F1 or ESC to quit.

* To see all the control keys, go to Edit->Project settings and then open Engine->Input

* User commands go through Edit->Project Settings->Engine->Input so they can be easily changed. You can change what keyboard keys do what and the speed of movement and mouse response on this page.  You can also add support for any input device you have by adding it here, this would include things like PC game controllers, joysticks and VR controllers.  

* Multiple cameras and video sources are supported.  This lets you have more than one camera view of your talent and live switch between them.  The project is setup for 2 cameras, adding more requires some blueprint and composure changes but I am working to make this simpler.

* An "inspection camera" gives you a 3rd person view of your level.  This is useful if you want to see if your cameras and other trackers are pointed in the right direction and moving.  This is a live view so if your tracked cameras move you will see them move.  This camera can also be moved around while the project is running.

* Multiple "Talent Markers" are supported.  You position these markers where you want your talent to appear in the level.  When you have more than one you just press a key and your talent, cameras and other tracked objects will teleport to the new location in the level.  This is just a quick cut, no transition effects (like fade in/out) yet.  Add more talent markers just by dragging them into the level and naming them TalentMark1...TalentMark2...etc.

* All the tracking and tracker-delay functions are now inside the "Tracker" actor.  Each tracker actor can have a different delay.  The output of the tracker automatically connects to any objects "attached-to" it in the world outliner.  The supplied tracker actor is for the Vive but you can make your own to support other tracking systems like optitrack, pan/tilt mechanical trackers or stationary cameras.

* All the control and UI functions are inside the "PlayerController" now.  So everything is in one place and easy to change.

* You can move the talent markers around using keyboard key to get the right placement of them in your level.  This can be done live while the composite is running and you will see the talent moving through the level.

* I've added several sample tracked objects as examples.  These can be handy for measuring things in your studio for setup or setting up a basic AR tracked object.

* VPCamera1 and VPCamera2 are setup to be controlled by VIVE trackers set to Special_1 and Special_2.  If you want to use some other controller just change the source in the camera's motion controller component.  For example "left" or "right" if you want to use the hand controllers.

* The setup should still work if you have only one camera.  Just don't use the "switch to camera 2" feature.

* The camera "rig" actors I've provided have variables for making small adjustments to the joints of the rig.  This is to correct for minor tracker rotation issues such as the tracker being slightly rotated on it's 1/4-20 tripod thread or on a ballhead mount you couldn't get exactly straight.  It is meant for very small adjustments of a few degrees at most and is not perfect, but if your tracker is slightly out of alignment using this can bring it back without having to mess with the mount itself.  The ones I included represent my actual camera rigs and only have these adjustments at places that can move.

* There is a garbage matte setup for use with a greenscreen that covers a wall and floor.  If your greenscreen has a different shape, you can model it and add your own mesh for a better fit.  There is a tutorial on my youtube channel that shows how to adjust the garbage matte to match the size of your greenscreen.

# Planned (NOT done yet)

* Since you can move the talent markers and inspection camera interactively, I will be adding a way to save their positions between runs of the project.

* The composure setup currently does 2 cameras and requires editing of both the composure setup and PlayerController blueprints to add more.  I'm trying to figure out a way to make this easier or automatic.

* It is setup for an AJA Kona HDMI video input card right now.  You can change this to support a different card or webcam.  I am working on a way to distribute setups for multiple types of cards and cameras to make it easier to configure it for whatever setup you have.

* There is no setup for a "pro video output card" because I don't have one to test.  You should be able to do this with minor changes.  See step 6 in this https://docs.unrealengine.com/en-US/Engine/Composure/QuickStart/index.html to see where to make the change in composure.  I currently capture output from my NVIDIA card's HDMI output.

* I have not figured out how to switch between Composure and other cameras outputting to the PlayerViewport.  Till I figure this out you need to do the switch manually by going into the composure output pass and changing the output between PlayerViewport and NONE.

* The composure setup may be rendering both camera views even though only one is visible.  I need to do some profiling work to make sure the views you CAN'T see are not stealing any rendering or CPU time.

# Keyboard Keys

For keyboard or Vive controller buttons to work the player viewport or PIE window needs to have focus.  Just click in it, your mouse cursor will disappear, to get mouse control back press shift-F1

These are what the keyboard keys currently do, if you want to change them go to Edit->Project Settings->Engine->Input.

Right now there is no way to switch between "Virtual Production Filming" mode and just looking around the set mode with a keyboard key.  You have to go to the "VPStudio Comp" item and find the output pass.  Set the output to "none" if you just want to look around, or "player viewport" to see the composite output.

When you first press PLAY you will either be looking at the composure composite or in inspection mode.  All the movement keys will be setup to move the inspection camera so you don't accidentally move anything else while you are filming.

Depending on what mode you are in, you can move talent markers or the inspection camera around.  Use the standard Unreal W, S, D, A keys for forward, back right and left movemtnt.  E and C moves up and down.  Use the mouse to look around (pan tilt).

To change to Virtual Production camera one, press 1 or left-click the right hand vive controller trackpad.  For camera two, use 2 or click right on the trackpad.

The N key or Vive controller trigger teleports you to the next TalentMark.  You can have as many of these as you want, just drag them into the level and number them 1, 2, 3 and so on.  When you press this key all your tracked objects & cameras will jump to the next mark and your talent will appear in that spot.

The M key switches between VPCamera "raw" views.  This gives you a view from each of your cameras but without any live composite, you will only see the CG part.  (only works when VPStudioComp output is set to NONE)

The I key switches to the inspection camera.  This is just a free floating camera that lets you look around the level while all the cameras and tracked objects are running so you can see if they are working and in the right places. (only works when VPStudioComp output is set to NONE)

The T key toggles between moving the inspection camera and moving the talent marks.

y, u, p, o and i keys will toggle visibility of TalentMark, MeasuringGuide, CameraModel, CameraRig and Tracker actors

When VPStudioComp output is set to "player viewport" you will see the full composite output of live cameras and the CG background.  The 1 and 2 keys switch between VPCamera1 and VPCamera2

Press b or click the right VIVE controller trackpad down to take a screenshot.  This is the same as typing "shot" into the editor command window.

# Other Notes

The large cone, cube and sphere are all 1 meter tall.  The center of the sphere is about 1.5 meters off the ground or about 5 feet high.  TalentMarkMan is 193cm tall or about 6'3".

# Bugs and Suggestions

Like I said, I'm still working on this.  I welcome suggestions on how to make it simpler or more efficient.  You can use the github issues tracker to comment on things if you like.  Remember this is in active development so there will occasionally be bugs, missing features and other problems.

