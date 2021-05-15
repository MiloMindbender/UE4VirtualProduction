Rassi Engineering Readme

To use this for testing realsense.

1. Setup the media player for your video capture device.  See VPStudioCore/AjaVideoCapture for an example.  Drag the media player actor to someplace in the level where it is not visible.

2. Go into VPMediaPlate actor in world outliner, set the video texture to the one you created in #1 above

3. Setup your livelink source in the livelink window.

4. Go to LiveLinkTracker1 in the world outliner.  Set tracker type to relative tracker and set Live Link Tracker To Use to your livelink source.  Once you do this you should see the tracker with a camera rig attached somewhere in the level.  

5. To get the tracker to appear in the right place you will need to provide a "Relative Tracker Offset" to position the tracker relative to whatever you consider the talent mark on your stage.  In Unreal the talent mark is the white square with an X on it.  You can also add the offset in an external program and just leave the "Relative Tracker Offset" all zeros.

6. Go to VPStudioComp in the world outliner.  In the output section set output 0 to None

7. Press play, click in viewport, press I for inspection mode.  Now you can use the wasd keys and mouse to move the inspection camera and view the virtual version of the studio.  Your tracker should be visible in there.  If it does not appear in the right place the offset is probably wrong.

8. To get a key, you will need to go into the VPMediaPlate and setup the chroma key parameters for your setup.

9. To get a proper composite you need to set the position of the MatteWall to match the green screen in your studio.  This is a garbage matte that removes anything outside your green screen from the video feed so the studio won't show up.

10. To see the finished composite, go into VPStudioComp again and set the output to player viewport.  Now when you press play you will see the results of the composite.

12. Note that the level has several other LiveLinkController and LiveLinkTracker actors in it.  These shouldn't cause any problems, if you want you can remove them from the level.

13. To get proper tracking you will need to go to the AutoRig object and set up the correct offset from your tracker to the entrance pupil of your lens.  Suggest you start by zeroing out all the numbers in there.  If your calibration system generates a tracking offset to the Entrance Pupil you can leave it this way.  If it generates an offset to the tracker, use the Rig Measurements section for the measurements from tracker to camera, the "adjustments" can be used to make small changes to get things to line up properly.  