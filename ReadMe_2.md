# How to use the Virtual Production sample with your own Unreal projects.

This is a quick guide that explains how to move the Virtual Production setup from this sample project into your own.  I will be doing a video version of this guide but a number of people were asking about it so I thought I would do a quick description here so they can use it right now.

# BEFORE you start!

To start, get my project working with your setup.  This means getting your trackers working, setting up the offsets in the CompCameraRig, getting your live video coming in and setting up the garbage matte to match your greenscreen.  This will be easier to do in my project because it is very small, simple and loads quickly.  Once you have my project running on your hardware configuration the Virtual Production assets can be migrated to a project of your own and they will already be setup to work on your hardware.

Check out tutorials on [my youtube channel](https://www.youtube.com/user/GregCorson) for help.  Particularly this one 
[![Virtual Production](http://img.youtube.com/vi/mwS2VfO3-UI/0.jpg)](https://youtu.be/mwS2VfO3-UI "Virtual Production Tutorial") 

# Step 1 -- BACK UP your target project

This is REALLY IMPORTANT, just in case there is some problem during the migration, you want to have a backup of your project so you can recover.  I just go into my unreal projects folder and drag a copy of it to some other location.

# Step 2 -- Prepare your target project

Your project MUST have all the unreal plugins installed and some settings properly set before you do the migrate.  If these things are not setup right, when you do the migration some assets may not come over, be incorrectly configured or the Unreal Editor may crash.  

* In the Unreal Editor, open your target project where you want to install Virtual Production.
* During this step Unreal may ask you to reset the editor, hold off doing this till all the things in this step are done, it will save you time.
* Go to Edit->Plugins
* Make sure the video plugin for your hardware is enabled (for me this is AJA Media Player, if you don't have an AJA card it may be something different).
* Go to the compositing section of plugins, make sure composure and lens distortion are enabled
* Go to the media section and turn on media framework and media I/O framework
* Go to the media players section and turn on any players you will use, at minimum you want the Media Foundation Media Player and WMF media player.
* Go to the Movie Players section and turn on Windows Movie Player.
* Go to the Virtual Production section and turn on Virtual Production Utilities.
* Close up the plugins window and go to Edit->Project Settings
* Go to Engine->Rendering->PostProcessing->enable alpha channel support... and set to Linear Color Space Only
* Go to Engine->Input->Bindings Some of the VIVE Tracker setup software won't work right unless there is at least one axis mapping here.  If you already have some, you are good, if not just press the plus next to "Axis Mappings" to make one.  You don't have to configure it.
* Now you can close the windows and restart the Unreal Editor.  These changes may cause Unreal to rebuild all your project's shaders which can take some time if you have a complex project.  The editor may appear to be stuck on it's loading page.  If you are concerned, check your task manager, if you see a lot of "shader compiler worker" tasks starting and stoping with all your CPU cores running full speed, then shaders are rebuilding.  Just wait, when it's done the editor will open back up.

# Step 3 -- Prepare my Virtual Productin project for migration

If you have already done a migration from my project and have since made changes to the "ThirdPersonExampleMap", you may have an "EmptyStudio" map with copies of older assets in it.  Before you go ahead you may want to delete the old "EmptyStudio" map so you won't accidently migrate obsolete assets.

* Edit my Virtual Production sample project
* In the Content Browser, go to Content->VPStuff and create a level called "EmptyStudio" 

# Step 4 -- Migrate the assets

In this step you move just the assets you want to migrage into an empty map and then migrate them. 

* In the ThirdPersonExampleMap, go to the World Outliner and select everything in the Comp Elements folder.
* If you WANT to migrate the second mannequin that appears in the foreground, select ThirdPersonCharacter also, I usually don't migrate him, leaving the foreground layer empty to add stuff to later.
* Do a "copy" load the EmptyStudio map and paste.
* In the Content Browser, go to Content->VPStuff
* Select EmptyStudio
* Also select ajagenlock or whatever custom timestep asset you created for your video hardware.
* Right click and choose asset actions->migrate
* A window will appear showing everything that will be migrated.  You may want to check this to make sure everything is there and nothing you don't want is on the list.
* Continue and you will get a file dialog to specify where you want to migrate to, select the content folder of your target project.
* You may get some warnings, usually about source control, review this list to make sure there are not serious errors.

# Step 5 -- Setup of your project

* Open up your target project
* The EmptyStudio level
* Select everything in the "comp elements" folder and do a copy
* Switch to the level you want to do virtual production in
* Paste into that level
* Select the "talent marker separate" object you just pasted in and move it to wherever in your level you want your live talent to stand
* In Project Settings->maps & modes set game instance to "globals"
* In Project Settings->engine->general->custom TimeStep you need to set whatever your custom timestep asset was, for me it's ajagenlock, if you use different hardware it will probably be something else, or you may not have one.  This is the asset that locks the unreal framerate to the framerate of your video source.

# Step 6 -- Final Adjustments

Now when you press play, everything should work like it did in my sample project.  You may need to adjust some things in your target project, below is a list of what to check if things don't look right.

* Atmospheric fog off
* Set camera focus target set to talent marker

# PLEASE report any problems.

If you run into any problems making this work, please report them as an issue here on github and I'll try to address them.  You may also want to subscribe to [my youtube channel](https://www.youtube.com/user/GregCorson) so you won't miss any new tutorials or demos.


