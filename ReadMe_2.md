# How to install in your own project and fix UE/Steam issues in 4.24.1

This is a quick guide that explains how to move the Virtual Production stuff from this sample project into your own.  In UE 4.24.1 and SteamVR 1.9.16 the input system was changed and some extra steam setup is required to trackers work.  Also the SteamVR 1.10.1 update currently breaks trackers so until this is fixed you should stay with the SteamVR release build at 1.9.16.  I will be doing a video version of this guide but a number of people were asking about it so I thought I would do a quick description here so they can use it.

# Hardware Required

This template is setup to use 2 VIVE tracking pucks and a 1080P camera attached to an Aja Kona HDMI card.  If you have different hardware some modifications will be needed that you will have to figure out yourself.  I will try to make the project more compatible as time goes by, but for now I only have this hardware to test with.  It should be possible to adapt this project to work with any camera and Unreal compatible video capture device, even webcams.  It should also work with any unreal compatible tracking system.  If you don't want to move the camera while doing a video, you don't even need the trackers, but they do make setup much easer!  

# How to use my Virtual Production template in your own Project.

* Edit your target project where you want to install Virtual Production.
* Go to the plugins section and make sure all these Aja, Composure and all the media framework plugins are enabled.  These must be enabled before you try to do a migrate or some of the assets will fail to work.
* Go into project settings post processing->alpha channel support and set to linear.  If this is not set the compositing may fail or look funny.
* Restart UE, these changes may require a rebuild of your shaders, so the load may take a bit.

* Now edit my Virtual Production sample project
* Open the level "EmptyStudio"
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

# Steam 1.10.1 beta bug

Right now there is a bug in Steam 1.10.1 beta that breaks trackers, they don't work at all.  Till this is fixed please use the release version of steam 1.9.16

# If you are on UE 4.24.1 with latest Steam

The newer versions of Steam require you to assign "roles" to each tracker and setup an input mapping.  This is pretty new so I'm not sure if this is the "right" way to do it but it works for me, I'll update if I find something simpler.

* You need to have at least ONE axis mapping in UE project settings->input bindings or you won't be able to configure the tracker.  If you have nothing here, just create a default axis mapping.  Not sure if this is a bug, but at the moment it is required.
* In steam's "manage trackers" assign a different "role" to each of your trackers such as "camera" and "keyboard"
* In UE's "SteamVR Input" menu select "Launch SteamVr Bindings dashboard"
* Click on the controller icon and choose the role you assigned to your camera tracker
* Add an action that maps the raw pose to Special_1
* Repeat for your second tracker and assign to Special_2
* trackers should now be working

# PLEASE report any problems.

If you run into any problems making this work, please report them as an issue here on github and I'll try to address them.  You may also want to subscribe to my YouTube channel at https://www.youtube.com/user/GregCorson so you won't miss any new tutorials or demos.


