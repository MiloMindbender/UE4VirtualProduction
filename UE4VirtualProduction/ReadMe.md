# UE4VirtualProduction Unreal Sample Project

This project is my original virtual production sample, it is a basic virtual set that you can put a live actor ("talent") into.  The full setup allows the camera to move or be handheld.  You can add my virtual production setup into any Unreal map you like.  Below is a video of the map the project comes with, it's based on the Unreal Engine "third person" template to keep it small and easy to download.

[![Virtual Production](http://img.youtube.com/vi/jwS3F9H_LWg/0.jpg)](https://www.youtube.com/watch?v=jwS3F9H_LWg "Virtual Production")

This video shows my setup being used with a more realistic TV studio virtual set.  The only "real" things in this video are me and the chair.  You can get this free set from the Epic Games Unreal "launcher" under the "learn" tab, look for "Virtual Studio" it contains several nice TV studios and a construction set for building your own.  I can't redistribute it here as part of my project due to licensing restrictions.

[![Virtual Production](http://img.youtube.com/vi/a3jh6HootAk/0.jpg)](https://www.youtube.com/watch?v=a3jh6HootAk "Virtual Production")

# Features of this project

* A live video camera that is tracked so you can move it (even handheld)
* A tracked object (a cartoon hammer) you can make follow a tracker in the talent's hand
* A rig you can move to anyplace in the level you want the talent to appear to be standing.
* A tracked 3D matte that prevents objects outside the green screen area from being seen, even if the camera moves.
* A way to delay the tracking data to keep it in sync with the live video
* A setup using Unreal's "composure" plugin to composite all the layers together.
* Foreground and Background layers in the composite so objects can appear in front of and behind the talent.

# Hardware Required

You can do Virtual Production with a lot of different kinds of equipment.  The only really essential thing is a camera and an Unreal compatible video capture device.  It's also possible to use a webcam. If you don't have exactly the same hardware as I use, you will have to make a few changes to the project.  They aren't too difficult and are covered in my video tutorial.  The hardware setup I currently use is:

* A 35mm full frame consumer camera with HDMI out on a good tripod
* AJA Kona-HDMI 4 input HDMI capture card
* A Vive Pro VR setup with two V2 base stations and controllers
* Several Vive tracking pucks (second generation)
* Standard PC
* NVIDIA 2080 graphics card
* A green or blue background to stand in front of

A Vive tracking puck is used to track the camera, you can also use the Vive controler for this, the pucks are just smaller and easier to mount on a camera.

# Getting Started

You can find a lot of tutorials on [my youtube channel](https://www.youtube.com/user/GregCorson) showing how everything works and how to use my setup with your own levels.  There are also some tips on equipment and studio setup.  These videos are the best place to start.

You do need to setup a solid color background to stand in front of.  Bright green works best because it is far from normal skin tones.  Blue is also commonly used.  You can use nearly any color as long as it is not too close to any color your talent is wearing (or their skin).  You can use fabric, paper or a painted wall.  You want something with a matte finish (NOT glossy or shiny) to cut down on reflections or hot spots.  You need to make sure the background and your talent are both evenly lit with as few shadows as possible.  Depending on your setup, natural light can work, cheap light fixtures from a home store or video/photo lights.

# Using your own Unreal Levels

To avoid content licensing issues I only use Unreal "starter content" in this project. In a few minutes you can migrate the assets from this project into any Unreal level you want to use as a virtual set.  See my video [how to migrate to your own project](https://youtu.be/lmCeBpzhge4) for instructions.  There is quite a bit of content available for free from the Unreal marketplace, a lot of it works without changes though some may contain lighting, fog or other effects that you will need to adjust to make them work with the live composites.

# Recording and Streaming

Most any screen recording/streaming software should be able to record the unreal window.  I usually use [OBS: Open Broadcaster Software](https://obsproject.com/) because it is free and easy to use.  You can also livestream the output from unreal directly to the internet for live events.  If you want a higher quality recording that is easier to edit you can use a hardware recorder such as a [Atomos Ninja V](https://www.atomos.com/ninjav) plugged into your graphics card or a video output card.

# Known Issues

This setup doesn't include color correction or removing lens distortion.  This can all be done in Unreal, I just don't do it in this project to keep things simple.

If the color of your live video looks weird or seems to change a lot, you probably have your camera set to "auto white balance".  The big solid green background confuses most cameras.  Use a manual white balance setting, most cameras have several fixed settings and many will let you set white balance by pointing the camera at a white card.

The solid green background can also confuse autofocus on some cameras.  If the focus is wrong or goes in and out, use manual focus or set the camera to face/eye tracking if you have it.

# If your trackers don't work

Sometimes trackers stop working.  You can check by running the virtual production project and clicking on the "comp camera rig" object in the world outliner, if the location/rotation numbers aren't changing then the tracker is not working.  There can be a couple of reasons for this.

* Trackers sometimes shut off if they aren't moved every so often.  This is for power saving when running on batteries but sometimes happens even if the trackers are plugged in.
* If you previously had everything working, but now the trackers are not, your setup may need restarting.  Exit both Steam VR and Unreal, then start them both back up.  If this doesn't work, try a reboot.
* If this is your first time in a new project, you may need to setup tracker "roles" in Steam to make them work.  [This video](https://youtu.be/tyIM6VTtc_w) on my Youtube channel describes how to do this.  This setup is required for Unreal 4.24 or higher used with Vive trackers and Steam versions since about November 2019.

