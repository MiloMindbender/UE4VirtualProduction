# How to use the Virtual Production sample with your own Unreal projects.

This is a quick guide that explains how to move the Virtual Production setup from this sample project into your own.  I will be doing a video version of this guide but a number of people were asking about it so I thought I would do a quick description here so they can use it right now.

# BEFORE you migrate.

Before you try and migrate my setup to your own project, I suggest you try to get my project to work with your video setup.  This includes getting the garbage matte setup and making sure whatever video source you are using is working.  It is probably easier to do this in my project because it is very small and simple.  I am using an AJA Kona-HDMI card, if you are using a different card or webcam you definately want to get that setup first.  Then when you migrate everything over to your project the settings will already be correct for your video and hardware.

# How to migrate my Virtual Production template to your own Project.

The most important thing when migrating these assets to your own project is to make sure all the required Unreal plugins are installed and enabled in YOUR project BEFORE you do it.  If these are not installed in YOUR project FIRST some of the assets will fail to migrate or may not work correctly when you try to use them.

* In the Unreal Editor, open your target project where you want to install Virtual Production.
* Go to the plugins section and make sure all the AJA (or whatever plugin you use for YOUR video), Composure and media framework plugins are enabled.
* Go into project settings post processing->alpha channel support and set to linear.  If this is not set composure compositing of the different layers may fail or look funny.
* Restart UE, these changes may require a rebuild of your shaders, so the load may take a bit.  Unreal Editor may appear to "hang" during loading if you have a lot of shaders.  If you are worried, check the task manager on your computer, you should see a lot of "shader compiler worker" tasks starting up and finishing, this means Unreal is working on recompiling shaders.

* Now edit my Virtual Production sample project
* The next 2 staps make sure that if you have already modified my project to work with your setup, all the green screen and composure changes you have made will get migrated.
* Open the example level and select everything in the "comp elements" folder and right click and "copy".  
* Open the level "EmptyStudio" and paste.
* select the EmptyStudio level in the content browser and do asset actions->migrate to the the content folder in your target project
* you will also need to migrate the "ajagenlock" asset over to the same location.

* Open up your target project
* Switch to the EmptyStudio level
* Select everything in the "comp elements" folder and do a copy
* Switch to the level you want to do virtual production in
* Paste into that level
* Select the "talent marker separate" object you just pasted in and move it to wherever in your level you want your live talent to stand
* In Project Settings->maps & modes set game instance to "globals" which should have come in with the migration
* You may need to go into the "comp camera" and reset the focus target to talent marker separate
* You may need to set Project Settings->engine->general->custom TimeStep to ajagenlock

When you are done with all of this, things should work but may not look quite right.  You will probably need to adjust the camera settings, lighting and chromakey colors as described in my YouTube tutorial.

# Unreal Engine 4.24 or higher

Unreal engine 4.24 started using a newer Steam input mapping system that requires you to assign "roles" to each tracker and setup an input mapping.  The main readme describes how to do this .  There is one potential problem, your project needs to have at least ONE axis mapping in UE project settings->input bindings or you won't be able to configure the tracker.  If you have nothing here, just create a dummy axis mapping.  Not sure if this is a bug, but at the moment it is required.

# PLEASE report any problems.

If you run into any problems making this work, please report them as an issue here on github and I'll try to address them.  You may also want to subscribe to [my youtube channel](https://www.youtube.com/user/GregCorson) so you won't miss any new tutorials or demos.


