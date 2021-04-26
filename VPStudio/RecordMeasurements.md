# Measurements README

The new RecordMeasurements actor gives you a way to measure the position of things in your studio using a VIVE controller.  The blueprints can be modified to support other devices for measuring as well.  They are fairly simple so take a look if you use something other than vive.

This is a new feature and is still kind of rough, please try it out and send me suggestions on how to make it better.  Right now I am not sure how to make it work in "editor" it only works after pressing play.  If you know how to fix this let me know.

# General

This is not really designed for precise measurements, but is very handy for getting a number of basic measurements when you are trying to setup things like the green screen position, the floor or the positions of mattes for things like tabletops or doors.  You take measurements by holding a vive controller or tracker at the spot you want to measure and pressing a key or button on the controller. It only measures positions, not rotation.

To use the measurement system you have to do a little setup, then press "play". As each measurement is taken it will appear on-screen and a marker will appear in the 3d world with the measurements next to it.  When you stop play, all the measurements will be written to the output log.  The measurements are recorded in a form like (X=-405.085236,Y=272.884674,Z=-0.000031) that is compatible with unreal cut/paste.  Select the whole measurement (including paranthesis) and copy, you can then paste all three values into an unreal actor by right clicking on "location" and selecting paste.

For VIVE tracking pucks, the measurement is made to the base of the tripod screw on the puck.  For VIVE controllers the measuring point is about halfway between the top button and the edge of the ring on the front of the controller.  To get a better idea of where these points are you can drag a "thinaxis" actor into your level and attach it to the tracker actor.  The 3 lines it draws will cross at the measuring or zero point on the tracker.

# Setup to measure

Decide which tracker you want to use to measure, this can be a controller or a tracking puck.  Create either a LiveLinkTracker or MotionControllerTracker in your level for this.  Now drag the RecordMeasurements actor into the level and use "attach to" to attach it to the tracker you just made.  This is setup to take a measurement when you press 0 (zero) on your keyboard or click the trigger on the left VIVE controller.  These settings can be changed in the blueprint or project settings->Inputs page.

# Measuring

Press play, move the tracker to the spot you want to measure and press 0 on the keyboard or click the trigger on the left hand VIVE controller.  You should see a measurement appear on the screen for about 2 seconds, a marker will also appear in the 3d world with the measurement next to it.  No need to write these down, when you end play all the measurements will print to the output log.

