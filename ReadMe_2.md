# How to install in your own project and fix UE/Steam issues in 4.24.1

This is a quick guide that explains how to move the Virtual Production stuff from this sample project into your own.  Also in UE 4.24.1 the steam input system was changed which caused the trackers to stop working.  There is a fix for that here too.  This will be replaced by a video guide soon, but since many people were asking about this I though I would write a quick document.

# How to install my Virtual Production setup in your own Project.

* Go into your target project where you want to install virtual production.
* Go to the plugins section and make sure all these plugins are enabled Aja, Composure and all the media framework plugins
* Go into project settings post processing->alpha channel support and set to linear
* Restart UE, these changes may require a rebuild of a lot of your shaders, so the load may take a bit.

* Now open up my Virtual Production sample project
* Duplicate the level and rename it to something like "EmptyStudio"
* Open EmptyStudio and delete everything in the level except for what is in the "comp elements" folder
* Test to make sure it is still working, video is coming in...etc.
* select EmptyStudio level in the content browser and do asset actions->migrate to the the content folder in your target project

* Open up your target project
* Switch to the EmptyStudio level
* Select everything in the "comp elements" folder and do a copy
* Switch to the level you want to do virtual production in
* Paste into that level
* Select the "talent marker separate" object you just pasted in and move it to wherever in your level you want your live talent to stand
* In Project Settings->maps & modes->game instance set to "globals" which should have come in with the migration
* You may need to go into the "comp camera" and reset the focus target to talent marker separate
* You may need to set Project Settings->engine->general->custom TimeStep to AjaCustomTimeStep

# If you are on UE 4.24.1 with latest Steam

You may find none of your trackers are working.  Here is a work-around, I'm not sure if this is the "right" way to do it but it works for me, I'll update if I find something simpler.

>>>This part not fully complete, need to do it again myself to make sure I haven't missed any steps<<<

* In UE project settings->input bindings, if you don't have ANY bindings here, create an axis mapping with default values.
* in steam's "manage trackers" assign a different "role" to each of your trackers.
* In UE's "steam" menu select manage
* Click on the controller icon and choose the role you assigned to your camera tracker
* Add an action that maps the raw pose to Special_1
* write it out
* Repeat for your second tracker and assign to Special_2
* write that out
* trackers should now be working


