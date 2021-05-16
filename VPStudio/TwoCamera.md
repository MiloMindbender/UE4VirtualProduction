# One Camera or Two Cameras

In this release of VPStudio I made the default setup one camera instead of two.  Not very many people were using the two camera setup so the extra overhead was just making it hard on people trying to learn.

# Problems with Two Cameras

The two camera setup worked fine but was slow, this was because it was always rendering the 3d views for both cameras whether they were being used or not.  So far I haven't found an automatic way to shut down the rendering of the camera that's not on the screen.  If you know of a way, please share it.

# How to use two cameras

In VPStudio there is the "main map" that contains your virtial set and a submap that contains all the Virtual Production stuff.  You can see this in the Windows->Levels menu in Unreal.  The default setup starts up with a 1 camera submap.  You should be able to use the two camera setup by going into the Levels menu, removing the 1 camera setup and adding the two camera sublevel.

# How 2 camera works

You would think that having 2 cameras would the same as one, just needing a way to "switch" between cameras.  Unfortunately unreal doesn't seem to offer this.  So the way the two camera setup works is to have a complete composure compositing setup for each camera. These come together in the top level of the composure stack.  At that point the blueprints switch which of the two composure setups will be shown as the main camera.  Unfortunately this means both views are always rendering so it doubles the rendering time for your level.  I haven't found a way to shut down the one that isn't visible.

# Alternatives for multiple cameras

One alternative to my 2 camera support is to use a different computer for each camera.  This lets each computer concentrate on generating just one view.  You can switch between views by hooking each computer to a video switcher.  While this sounds fairly simple it can get complicated, how complicated depends on your particular setup.