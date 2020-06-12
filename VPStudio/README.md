# READ SO YOU DON"T LOSE WORK! UNREAL 4.25.1 BUG

There is a bug in 4.25.1 that causes an editor crash. If there are mediabundles in the current level and you open a new level the editor may crash and lose everything till the last time you saved.  Epic is working on a fix that should be in 4.25.2  Till the fix is released I will be checking this project in without media bundles in the level to avoid accidental crashes and lost work.

You can still use the level for Virtual Production, just drag the two media bundles from the AJA folder back into the level.  But once you do this DO NOT try to switch levels or Unreal may crash.  Delete the media bundles from the level (NOT from content browser) and you should be able to switch levels again.

# VPStudio is a WORK IN PROGRESS, NOT FULLY FUNCTIONAL

This is my new template for doing Virtual Production.  It should be easier to understand how this template works and it has a number of new features.  I am also trying to make it easier to setup and customize for your hardware and studio.

Things could change on an almost daily basis.  Feel free to look at it and make comments on anything you think could be improved.  Please feel free to use any of the bits and pieces or ideas you find here in your own projects, just please credit me, Greg Corson for whatever stuff you take.

I will be starting a series of tutorial videos on my YouTube site soon.

# Recommendations for Use

Since this is a work in progress, every time you check this out from github there could be significant changes.  For now I recommend you make a UNCHANGED copy of whatever version you are using and save it somewhere.  This way if I make a change that isn't compatible with what you are doing, you will always have your saved version to go back to.

If you are checking out or cloneing the github repository, I would recommend you don't make changes in the directory you checked out.  Make a duplicate, fork or in the unreal launcher, a clone of the project to work on.  This will keep your original checkout clean.

# Use with your own levels

The easiest way to use this Virtual Production template with one of your own levels is to migrate your level into this template.  This will make sure all the plugins and other project settings needed for Virtual Production will already be set for you.  You can also migrate the key parts of this project into your own project, this is a bit more complicated because a number of settings and plugins need to be changed.  The "migration tutorial" on my YouTube channel should still mostly work for this new template.  I will try to update it soon.

# Please remember

If you change some of the blueprints or game modes, things may break. Here are a few important ones.

Under Edit->Project Settings->Project->Maps & Modes I provide a VPPlayerController that manages all user input and controls everything.  This is required or nothing will work.  I also provide a VPGameState and VPGameMode which are currently EMPTY and not required.  Though in the future this may change.

If you change the VPCamera asset blueprints and recompile, Unreal disconnects the cameras from the composure passes.  You will have to go into VPStudioBackground1 & 2 and reset the "camera source" to override and the Target Camera Actor to VPCamera 1 & 2 again.

Right now there is no way to switch between "Virtual Production Filming" mode and just looking around the set mode with a keyboard key.  You have to go to the "VPStudio Comp" item and find the output pass.  Set the output to "none" if you just want to look around, or "player viewport" to see the composite output.

Because of the 4.25.1 bug in unreal, my levels don't contain the AjaMediaBundles.  When you are ready to shoot just drag them from the aja folder into the level and you will be ready to film.

# Features

Keep in mind all these are subject to change!  Remember for keyboard/mouse to work you need to have clicked in the 3d viewport.  To get control of your computer back just hit shift-F1 or ESC to quit.

* To see all the control keys, go to Edit->Project settings and then open Engine->Input

* User commands go through Edit->Project Settings->Engine->Input so they can be easily changed.  Everything is keyboard/mouse now.  You can easily change what keyboard keys do what and the speed of movement and mouse response right on this page.  You can also add support for any input device you have by adding it here, this would include things like PC game controllers, joysticks, VR controllers and so on.  

* Multiple cameras and video sources are supported.  This lets you have more than one camera view of your talent and live switch between them.  Currently the project is setup for 2 cameras, adding more requires some blueprint and composure changes but I am working to make this simpler.

* An "inspection camera" gives you a 3rd person view of your level.  This is useful if you want to see if your cameras and other trackers are pointed in the right direction and moving.  This is a live view so if your tracked cameras move you will see them move.  This camera can also be moved around while the project is running.

* Multiple "Talent Markers" are supported.  You position these markers where you want your talent to appear in the level.  When you have more than one you just press a key and your talent, cameras and other tracked objects will teleport to the new location in the level.  This is just a quick cut, no transition effects (like fade in/out) yet.  Add more talent markers just by dragging them into the level and naming them TalentMark1...TalentMark2...etc.

* All the tracking and tracker-delay functions are now inside the VPCamera actor.  Each camera can have a different delay if necessary.  The old version required two actors and a global to do this, now it's all in VPCamera.

* All the control and UI functions are inside the "PlayerController" now.  So everything is in one place and easy to change.

* You can move the talent markers around using keyboard key to get the right placement of them in your level.  This can be done live while the composite is running and you will see the talent moving through the level.

* I've added several sample tracked objects as examples.  These can be handy for measuring things in your studio for setup or setting up a basic AR tracked object.

* VPCamera1 and VPCamera2 are setup to be controlled by VIVE trackers set to Special_1 and Special_2.  If you want to use some other controller just change the source in the camera's motion controller component.  For example "left" or "right" if you want to use the hand controllers.

* The setup should work as-is if you have less than 2 cameras (even none) you should not have to change anything.

* I have temporarily added a "fix tracker rotation" to VPCamera, these should normally be set to zero.  This is to correct for minor tracker rotation issues such as the tracker being slightly rotated on it's 1/4-20 tripod thread or on a ballhead mount you couldn't get exactly straight.  It is meant for very small adjustments of a few degrees at most and is not perfect, but if your tracker is slightly out of alignment using this can bring it back without having to mess with the mount itself.

* There is a garbage matte setup for use with a greenscreen that covers a wall and floor.  If your greenscreen has a different shape, you can model it and add your own mesh for a better fit.

# Planned (NOT done yet)

* Since you can move the talent markers and inspection camera interactively, I will be adding a way to save their positions between runs of the project.

* The composure setup currently does 2 cameras and requires editing of both the composure setup and PlayerController blueprints to add more.  I'm trying to figure out a way to make this easier or automatic.

* Currently the cameras and trackers are rendered as 3d objects all the time.  I will be adding a button to turn them on and off so they won't appear in the shot.  For now you can tick the "hidden in game" box on each object if you want to make it invisible.

* It is setup for an AJA Kona HDMI video input card right now.  You can change this to support a different card or webcam.  I am working on a way to distribute setups for multiple types of cards and cameras to make it easier to configure it for whatever setup you have.

* There is no setup for a "pro video output card" because I don't have one to test.  You should be able to do this with minor changes.  See step 6 in this https://docs.unrealengine.com/en-US/Engine/Composure/QuickStart/index.html to see where to make the change in composure.  I currently capture output from my NVIDIA card's HDMI output.

* I have not figured out how to switch between Composure and other cameras outputting to the PlayerViewport.  Till I figure this out you need to do the switch manually by going into the composure output pass and changing the output between PlayerViewport and NONE.

* The composure setup may be rendering both camera views even though only one is visible.  I need to do some profiling work to make sure the views you CAN'T see are not stealing any rendering or CPU time.

* Working on improving the setup of the camera and tracker rig so it will be easier to get alignment exactly right.  This will probably involve you creating a SIMPLE model of your rig with the correct measurements and pivots in the right places.

# Keyboard Keys

For any of the controls to work you need to click in the viewport where this project is running.  To get normal mouse control back press shift-F1

These are what the keyboard keys currently do, if you need to change them go to Edit->Project Settings->Engine->Input.

Right now there is no way to switch between "Virtual Production Filming" mode and just looking around the set mode with a keyboard key.  You have to go to the "VPStudio Comp" item and find the output pass.  Set the output to "none" if you just want to look around, or "player viewport" to see the composite output.

When you first press PLAY you either be looking at the composure composite or in inspection mode.  All the movement keys will be setup to move the inspection camera so you don't accidentally move anything else while you are filming.

Depending on what mode you are in, you can move talent markers or the inspection camera around.  Use the standard Unreal W, S, D, A keys for forward, back right and left movemtnt.  E and C moves up and down.  Use the mouse to look around (pan tilt).

The N key teleports you to the next TalentMark.  You can have as many of these as you want, just drag them into the level and number them 1, 2, 3 and so on.  When you press this key all your tracked objects & cameras will jump to the next mark and your talent will appear in that spot.

The M key switches between VPCamera "raw" views.  This gives you a view from each of your cameras but without any live composite, you will only see the CG part.  (only works when VPStudioComp output is set to NONE)

The I key switches to the inspection camera.  This is just a free floating camera that lets you look around the level while all the cameras and tracked objects are running so you can see if they are working and in the right places. (only works when VPStudioComp output is set to NONE)

The T key toggles between moving the inspection camera and moving the talent marks.  

When VPStudioComp output is set to "player viewport" you will see the full composite output of live cameras and the CG background.  The 1 and 2 keys switch between VPCamera1 and VPCamera2

# Bugs and Suggestions

Like I said, I'm still working on this.  I welcome suggestions on how to make it simpler or more efficient.  You can use the github issues tracker to comment on things if you like.  Remember this is in active development so there will occasionally be bugs, missing features and other problems.

