This is [TelemetryViewer](http://farrellf.com/TelemetryViewer/) From "Farrellf" or [upgrdman](https://www.youtube.com/user/upgrdman) on YouTube. A JRE (Java Runtime Environment) needs to be installed on your computer to run it.  There is a link to one on his website above.  Videos on how to use the tool are on his YouTube channel with the [latest one here](https://youtu.be/FqfgBnCdrTo)  It's useful for a lot of things, here I am using it to display real-time information from a VIVE tracker.

The data goes directly out of an actor in Unreal to this program through the network.  You can run it on the same machine as unreal or a different computer.  It also runs on Raspberry PI 4 (not older models)

When you start the program, "import" the setup file called Tracker Data.txt and you will be setup to receive data from the first "telemetry type" options in my TrackerTelemetryTCP actor.  The remaining options are just for my testing work and not useful for other people to try.

I am using this setup to filter out tracker jitter which happens to be harder to do than you would think.
