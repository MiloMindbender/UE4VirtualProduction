# Unreal Project to test your tracker setup

You may not have noticed it yet, but Vive trackers can jitter a bit as shown [here](https://youtu.be/H6M5PleSJD4). In Virtual Production this is usually not noticed if the camera is moving, but when the camera is stationary you can sometimes see it.

There are a number of things that can interfere with tracker operation, many of which can be easily fixed by changes to the way the room is setup.  This project gives you a way to measure how much jitter you have so you can see if the changes you make improve things.

# Setup

This project assumes you have already got your Vive system working with unreal and tried out some Virtual Production examples.

Assuming you have one tracker setup with it's Role set to "Special_1" you should be ready to use this project.

The tracker must be STATIONARY while the test is running.  On a tripod, the floor, a table or chair are all fine, just don't hand-hold it.

# Run the test and get results

Load up the project and press Play.  After about 20 seconds it will stop on it's own.  Now go to window->developer tools->output.  You will find some messages with a row of numbers that look something like what's below (I shortened it a bit here to make it easier to read)

LogBlueprintUserMessages: [AutoTest_2] --------------------

  | 277.895 | 131.399 | 151.0294 | -148.438 | 88.894 | 170.352 | Average Value (mean)

  | 0.0044  | 0.0057  | 0.0060   | 0.5918   | 0.0130 | 0.5894  | standard deviation (smaller is better)

LogBlueprintUserMessages: [AutoTest_2] --------------------

The first row shows X, Y, Z position in centimeters and Roll, Pitch, Yaw rotation in degrees.  This is where in the room the tracker was when you ran the test.  If you run several tests without moving the tracker, these numbers should be almost the same.

The second row shows how much the values have changed during the test, also called the standard deviation.  The smaller these numbers are, the less jitter you have.

# What is good?

I don't have any guidelines for what these numbers should be, how much jitter is too much will vary depending on your setup and your expectations.  Basically if you are doing Virtual Production and you can see jittering in a stationary camera shot, you want to try to reduce it.

# Reducing Jitter

There is no guaranteed way to reduce jitter but a lot of the things below can help.  Also if you notice large errors like the camera suddenly jumping around or not moving when it should, these fixes may help that too.  Problems may be worse in some parts of the room than others.

* Cover reflective surfaces -- The Vive base stations scan the room with an IR laser, anything that laser light bounces off of can cause confusion for the trackers.  This can include things like glass, mirrors, chrome and any kind of high-gloss surface you can see a reflection in, including polished floors.  Not every surface will reflect enough light to be a problem, try covering them up one-by-one and re-testing to see if the jitter improves.
* Sunlight -- Direct sunlight can be so bright the trackers can't see the lasers anymore.  So avoid sunlight falling right on the tracker.
* Flickering Light -- Any kind of light that flickers (even if you can't see it) can confuse the trackers.  This would include strobe lights, camera flashes, old flourescent lights that have started to flicker or sunlight going in and out between blinds/curtains blown around in the wind.  If you suspect lights, try turning them off and see if tracking gets better, then turn them on one by one to find the one causing trouble.
* Base Station Position -- Changing the position of your base stations may help.  Generally they should be along a wall (not in a corner) and roughly opposite each other if you are using 2 of them.  Head height or higher is usually best, remember to angle them down.
* V1 vs V2 base stations -- The V1 base stations have flat fronts, the V2 ones are curved.  The V2 bases have slightly wider angle tracking, longer range and are more immune to interference.  You can only have 2 of the V1 base stations, the V2 ones allow 4 for larger areas and better coverage.
* Base Station Vibration -- Make sure your base stations are securely mounted so they don't move.  If your building shakes when people walk around or when a large truck drives by, this can cause jitter.  Also check your base stations by touching them when they are in use.  They have spinning parts inside and it is normal to feel some vibration.  If one of the bases seems to vibrate more than another, there could be a hardware problem.

# Shutting off tracking

If you are planning on shooting with a stationary camera, you can eliminate jitter by shutting the trackers off once your camera is where you want it.  Any time you move the camera you will have to turn the trackers on again to get the new position.

I have tried ignoring the trackers when the camera appears to be stationary and automatically starting them when the camera begins to move.  So far this almost always results in a small but objectionable jump when the camera starts moving.

# Filtering

The output of the trackers can also be filtered mathamatically to reduce the jitter using a low pass filter implemented in an Unreal blueprint.  The trick is filtering just enough to remove the jitter while not causing lag when the camera starts moving.  If you come up with a filter that works for you, let me know.

# Report your results

We are still trying to figure out what amount of jitter is normal and what is not, so if you can please send me your results from this project along with a description of your setup.

