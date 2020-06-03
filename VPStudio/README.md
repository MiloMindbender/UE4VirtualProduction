# VPStudio Example WORK IN PROGRESS, NOT FULLY FUNCTIONAL

This is a new template for doing Virtual Production.  I won't go into much detail because I'm still working on it.  Please be aware I am actively updating this daily so it may not always be fully functional.

The biggest features of this new studio will be support for multiple cameras and a structure that is easier to understand.

# Currently

Right now the setup is very basic, there is a composite with two camera inputs and code to switch between them.

This is currently setup for an AJA Kona HDMI card with the first 2 inputs at 1080p59.94  It should not be too hard to change it for a different card by modifying the media bundles and composure video plates.  I'm working on making this easier.

To see the results of the composite, make sure that the VPComp output pass is set to "Player Viewport"  if you set it to "none" you will be able to move a camera around the set using the usual Unreal wasd movement keys and the mouse.

Remember for any keyboard commands to work you need to have clicked in the game window with your mouse.

Currently Special_1 and Special_2 trackers drive the two main cameras.  Special_3 drives a third camera that is not connected to a composite.  If you run with VPComp output pass set to "none" you should be able to move around the world with the wasd keys and get to a position where you can see all 3 cameras which will move when you move trackers.

To switch between the two cameras use the 9 and 0 keys.

Camera tracking delay is set individually in each VPCamera object so you can have different delays for different cameras.

There is no garbage matte yet.

This setup is probably inefficient, rendering the CG views for both cameras every frame.  Need to improve this.

All the controls are now in the "VPPlayerController" object.  When the game starts a blueprint finds all the VPCamera and MotionController objects and stores them in an array here.  Another part of the blueprint reads the three motion controller positions and copies them into the cameras.

There is some test code in the level blueprint, it prints some messages but does nothing functional right now, you can delete it or ignore it if you like.

Composure still does not recognize camera components, so it is nessary to create a camera actor.  This is why the player controller handles reading the motion controllers.

# Bugs and Suggestions

Like I said, I'm still working on this.  I welcome suggestions on how to make it simpler or more efficient.  You can use the issues tracker to comment on things.  Remember this is in active development so there will occasionally be bugs, missing features and other problems.

