# An example of Virtual Production in Unreal Engine 

This is an example of a Virtual set where live green-screen video of your "talent" (actors) is composited with a 3d virtual set rendered in realtime by Unreal.  Features of the example include:

* A live video camera that is tracked so you can move it (even handheld)
* A tracked object (a cartoon hammer) you can make follow a tracker in the talent's hand
* A marker you can move to anyplace in the level you want the talent to stand.
* A tracked matte that prevents objects outside the green screen area from being seen, even if the camera moves.
* A way to delay the tracking data to keep it in sync with the live video
* A setup using Unreal's "composure" plugin to composite all the layers together.
* Foreground and Background layers in the composite so objects can appear in front of and behind the talent.

To avoid content licensing issues and keep the example small, only Unreal "starter content" from the 3rd person project template is used. In a few minutes you can migrate the assets from this project into any Unreal level you want to use as a virtual set.  See https://github.com/MiloMindbender/UE4VirtualProduction/blob/master/ReadMe_2.md for instructions.  The Unreal "Virtual Studio" example has several TV studio levels that work well with this.

# Documentation is on Youtube

See my youtube channel at https://www.youtube.com/user/GregCorson for documentation, tutorials, demos and tips on Virtual Production. There are also playlists with a lot of Virtual Production and mixed reality videos from other creators.

This may look complicated but you can get some great results from a very simple setup and since everything here runs in real-time, you can even use this setup for livestreaming!

# Hardware Required

The only thing really required to do Virtual Production is an Unreal compatible camera & video capture card or a Webcam.  To use all the features and have a camera you can move, you need some kind of tracking system.  This can be a VR headset and it's controllers or specialized tracking devices.  The example is configured for the hardware and video studio I currently use so if your setup is different you will have to make some changes.

My setup is:
* A 35mm full frame consumer camera with HDMI out on a good tripod
* AJA Kona-HDMI 4 input HDMI capture card
* A Vive Pro VR setup (second generation base stations)
* Several Vive tracking pucks (second generation)
* Standard PC
* NVIDIA 2080 graphics card
* A large fabric green-screen and some lights


