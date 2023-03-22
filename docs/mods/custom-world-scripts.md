# Custom World Scripts

!!! danger
	We plan to remove the feature in this form. It is just bad in about every way possible. Maybe just drop the page? Undocumented stuff doesn't exist :)

It is also possible to add some custom code, like used at tutorials. It is a bit hacky, but the concept is very simple. This can be very powerful.

For that you need some basics in GDScript, what you will unterstand in 5 minutes, if you have a bit programming experience, it's similar to python. Read [this article](https://docs.godotengine.org/en/stable/getting_started/scripting/gdscript/gdscript_basics.html) for that.

## Adding Script
First of all: The script itself is not scenario specific, but it can check itself, which scenario is currently running.. So let's add a script. Select the 'World' Node with right click, and select 'Add Child Node':

![1](https://raw.githubusercontent.com/Jean28518/Libre-TrainSim/master/Documentation/Images/CustomScripts/1.png)

Now just select 'Node', and select create.

![2](https://raw.githubusercontent.com/Jean28518/Libre-TrainSim/master/Documentation/Images/CustomScripts/2.png)

By double clicking the new node (its at the bottom) you can rename it whatever you want. In the end it should look like this:

![3](https://raw.githubusercontent.com/Jean28518/Libre-TrainSim/master/Documentation/Images/CustomScripts/3.png)

If you want you could add your own complete custom script, but a template is very useful. In the 'File System' tab navigate to `res://addons/Libre_Train_Sim_Editor/Data/Scripts/` rightclick `CustomScenarioTemplate.gd`, and select duplicate. Move then the duplicate to `res://Worlds/YOURWORLD`. In the end it should look like this:

![4](https://raw.githubusercontent.com/Jean28518/Libre-TrainSim/master/Documentation/Images/CustomScripts/4.png)

Now drag and drop your `CustomScript.gd` from the 'FileSystem' tab to your new Script node in the 'Scene' tab: 

![5](https://raw.githubusercontent.com/Jean28518/Libre-TrainSim/master/Documentation/Images/CustomScripts/5.png)

In the end you should see a script symbol next to your new script node. Just click on it, and the editor should open automatically.

![6](https://raw.githubusercontent.com/Jean28518/Libre-TrainSim/master/Documentation/Images/CustomScripts/6.png)

## Editing Script:
For better editing press the fullscreen button of the main window:

![7](https://raw.githubusercontent.com/Jean28518/Libre-TrainSim/master/Documentation/Images/CustomScripts/7.png)

Dont forget to save by pressing `Ctrl + S`.

### Header:
```
extends Node

onready var world = find_parent("World")
onready var player = world.get_node("Players/Player")
```
This code you will find at almost every component of modules from Libre TrainSim. These are the main components. 

- The world node handles such components as chunk system, time, spawning other trains, scenario, etc. Also every single component like rails, trees, trains, signals, stations, etc. can be accessed via it. For example if I want to reference a signal then I write `var signal = world.get_node("Signals/SIGNALNAME")`. For scripting just further one variable is interesting: `world.time`. `world.time[0]` contains the hour, `world.time[1]` contains the minute, `world.time[2]` contains the second.
- The player node is simply the player. It's the train, which the player drives. It drives over rails, handles the ingame HUD, messages, and stores much information like the timetable, speed, doors, ... You can find the player script for looking after variables under `res://addons/Libre_Train_Sim_Editor/Data/Scripts/Player.gd`. Only the first 100 lines should be interesting to you. 

**BUT IT IS HIGHLY RECOMMENDED TO NOT CHANGE ANY OF THESE VARIABLES VIA SCRIPT, IF YOU DON'T NEED TO!** The game couldn't work correctly after it. 

- Some functions from [jTools](https://github.com/Jean28518/Godot-jTools) could be useful too. jTools is already integrated to Libre TrainSim. jAudioManager and jEssentials could be interesting for custom scripts.

### Stuff for specific scenarios
```
var message = ""
var step = 0
var scenario = Root.currentScenario
func _process(delta):
	internal_stuff(delta)


func next_step():
    # ...
    step += 1
    #....

func internal_stuff(delta):
    #....

```
This handles the basic functionality. 

So now let's add a function, which will handle one specific scenario from step to step.
At first we to create a function:
```
func scenario1():
    pass
```
(You can remove `pass`, when you added something to the function). Now you need to call the function in `_process(delta)`:
```
func _process(delta):
    internal_stuff(delta)
    if scenario == "ExactNameOfTheScenario":
        scenario1()
```
Now the function is just called, if the player plays a specific scenario. *(For advanced scripting: Keep in mind, that the function is called every game cylce (about 60 times per second)*

Now because of `internal_stuff()` some magic happens, and the code below will work like written in the comments:
```
func scenario1():
match step:
		0:
			message = "Welcome! Please rise up the pantograph by pressing b"  ## In Beginning of every step, you should define next message. 
			if player.pantograph: # condition, if step 0 is done
				next_step() # move on to next step
		1:
			message = "Great! To close the Doors, press 'o'.\n\nWhith 'i' you can open the left one,\nwith 'p' you open the right door."
			if  not (player.doorRight or player.doorLeft):
				next_step()
		2:
			message = "Last message of custom scenario. Thanks for playing!"
```

So happy coding! 

***

For example here is the code of the mobile tutorial function:

```
func basics_mobile_version():
	match step:
		0:
#			message = "Welcome to Libre TrainSim!\nPlease have in mind that this is an early alpha version, in which many features are missing, and some bugs are possible.\nThe mode is now set to Easy.\n\nLet's start the engines!\nPress 'b' to set up the pantograph and wait a bit.\nAfter 5 sconds you can press 'e' to start the engines!"
			message = TranslationServer.translate("TUTORIAL_4_0")
			player.get_node("HUD/MobileHUD/Pantograph").modulate = Color(1, 0.5, 0, 1)
			if player.pantograph:
				next_step()
		1:
			# message = Press e to start engines
			player.get_node("HUD/MobileHUD/Pantograph").modulate = Color(1, 1, 1, 1)
			player.get_node("HUD/MobileHUD/Engine").modulate = Color(1, 0.5, 0, 1)
			message = TranslationServer.translate("TUTORIAL_4_1")
			if player.engine:
				next_step()
		2:
#			message = Our departure is at 12:00. Let's wait for the depart message in the bottom left corner."
			message = TranslationServer.translate("TUTORIAL_4_2")
			player.get_node("HUD/MobileHUD/Engine").modulate = Color(1, 1, 1, 1)
			player.get_node("HUD/MobileHUD/Camera").modulate = Color(1, 0.5, 0, 1)
			if player.currentStationName == "":
				next_step()
		3:
#			message = "Great! To close the Doors, press 'o'.\n\nWhith 'i' you can open the left one,\nwith 'p' you open the right door."
			message = TranslationServer.translate("TUTORIAL_4_3")
			player.get_node("HUD/MobileHUD/Camera").modulate = Color(1, 1, 1, 1)
			player.get_node("HUD/MobileHUD/DoorClose").modulate = Color(1, 0.5, 0, 1)
			if  not (player.doorRight or player.doorLeft):
				next_step()
		4:
#			message = "Let’s abort! Use the arrow keys to drive. \n\n\tPress the up arrow key to accelerate / release the brakes.\n\tPress the down arrow key to release acceleration / apply the brakes. \n\nHint: You can see your current command at the right tachometer."
			message = TranslationServer.translate("TUTORIAL_4_4")
			player.get_node("HUD/MobileHUD/DoorClose").modulate = Color(1, 1, 1, 1)
			player.get_node("HUD/MobileHUD/Up").modulate = Color(1, 0.5, 0, 1)
			player.get_node("HUD/MobileHUD/Down").modulate = Color(1, 0.5, 0, 1)
			if Math.speedToKmH(player.speed) > 20:
				next_step()

		5:
#			message = "Ahead you see an orange signal. That means that the next signal is going to be red. So make sure, you apply the brakes that you will stand before the red signal.\n\nWith the left arrow key you can easily set acceleration and brakes to zero. Try it, if you have brakes or accleration applied!"
			message = TranslationServer.translate("TUTORIAL_4_5")
			player.get_node("HUD/MobileHUD/Up").modulate = Color(1, 1, 1, 1)
			player.get_node("HUD/MobileHUD/Down").modulate = Color(1, 0.5, 0, 1)
			if Math.speedToKmH(player.speed) == 0 and not player.overrunRedSignal:
				world.get_node("Signals/Signal2").status = 1
				next_step()
		6:
#			message = "Great... \nWait... the signal is now green! Now we need to accelerate very fast.\nTo do this, simply press the right arrow key. It instantly sets the train to max power."
			message = TranslationServer.translate("TUTORIAL_4_6")
			player.get_node("HUD/MobileHUD/Down").modulate = Color(1, 1, 1, 1)
			player.get_node("HUD/MobileHUD/Up").modulate = Color(1, 0.5, 0, 1)
			if player.distanceOnRail > 700 and player.currentRail.name == "Rail":
				next_step()
		7:
			player.get_node("HUD/MobileHUD/Up").modulate = Color(1, 1, 1, 1)
#			message = "The signal in front of you is blinking.. what does this mean?\nIf a signal is blinking, then its announcing a new speed limit, which is lower than your current one.\nNo fear, the blinking signal just announce it, the speed limit will become effective at the signal behind it.\n\nIf e.g. the signal displays a 8, then the speed limit is 80 km/h.\nOrange signs/digits are always announcing limits,\nWhite signs/digits will set the speed limit effective."
			message = TranslationServer.translate("TUTORIAL_4_7")
			if player.currentRail.name == "Rail2":
				next_step()
		8:
#			message = "In 600 meters there will be the next train station. Every station is announced in the left bottom corner, if its 1000m away. Certainly you already saw it.\n\nIt is recommended to brake down to about 70 or 60 km/h, and then brake softly if you are shortly before the train station.\nLets arrive!"
			message = TranslationServer.translate("TUTORIAL_4_8")
			if player.distanceOnRail > 250 and player.currentRail.name == "Rail2":
				next_step()

		9: 
			# message: Hint: If you don't know further on at any time or you just want to enjoy the ride, press 'ctr' + 'a' to activate the autopilot. 
			message = TranslationServer.translate("TUTORIAL_4_9")
			player.get_node("HUD/MobileHUD/Autopilot").modulate = Color(1, 0.5, 0, 1)
			if player.speed == 0 and player.currentStationName == "Tutorialbach" and not player.wholeTrainNotInStation:
				next_step()
			
		10:
#			message = "Great, you arrived securly!\nNow you have to open the doors.\nWith 'i' you can open the left one, with 'p' the right one.\nIn our case we have to open the left one with 'i'."
			message = TranslationServer.translate("TUTORIAL_4_10")
			player.get_node("HUD/MobileHUD/Autopilot").modulate = Color(1, 1, 1, 1)
			player.get_node("HUD/MobileHUD/DoorLeft").modulate = Color(1, 0.5, 0, 1)
			if player.isInStation:
				next_step()
		11:
#			message = "Thank you for playing! You can now exit the game with 'Esc'"
			message = TranslationServer.translate("TUTORIAL_4_11")
			player.get_node("HUD/MobileHUD/DoorLeft").modulate = Color(1, 1, 1, 1)
			player.get_node("HUD/MobileHUD/PauseButton").modulate = Color(1, 0.5, 0, 1)
```

