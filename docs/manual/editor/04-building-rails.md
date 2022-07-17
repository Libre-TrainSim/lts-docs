# Building Rails

## Getting started

!!! danger "Update required"
    This info needs to be updated with ingame info. All the Godot references can go.

Lets assume, you don't have any Track at first. You can add a Track by drag and drop the file located under `res://addons/Libre_Train_Sim_Editor/Data/Modules/Rail.tscn` into the world (from the FileSystem Tab in the bottom left corner). 

**Please make sure that all rails in the World are a direct child/attached to the `Rails` node in the scene. Otherwise they wont work properly.** *(To do that drag and drop the newly added Rail to the `Rails` node in the scene tree)*

![CorrectSceneTree](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/CorrectSceneTree.png)

After that you will see in the Inspector many Variables with them the rail is configured. *You shouldn't change these Script Variables, we will have our own editor for that.* Head over to the Transform Settings of your new Rail. Libre TrainSim just uses the translation and the y Rotation. *Dont rotate your rail over the x or z axis, also never scale it, Libre TrainSim is ignoring them.* Before changing any of these values, you have to activate Manual Moving in the RailBuilder tab, or at the train variables. Now apply the transform of your first rail, like you want it, or just set the translation and rotation to 0. *At the beginning it's recommended to set the translation.y to 0. * Here you can see which transform variables you are allowed to change:

![WhichTranslationVariablesCanIUse](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/WhichTranslationCouldIChange.png)

Congratulations to your first Rail! From now on we will only use the Libre TrainSim RailBuilder to build further Rails. You Can find him at the right top Corner of GoDot, maybe you have to click on the white arrows to select the RailBuilder:

![WhereToFindRailBuilder](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/WhereToFindRailBuilder.png)

## Railbuilder

!!! danger "Update info"
    Needs new screenshots. And a check if the stuff is still valid. Furtheremore Drag and Drop is partly implemented.

Lets see which sections the RailBuilder has:

![SectionsOfRailBuilder](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/SectionsOfRailBuilder.png)

1. Here you can rename the Rail, and delete it, if you want. 
2. Here you can add a new Rail. There are Three Modes:
    - *After Rail*: You simply add a new Rail after your current selected Rail. 
    - *Parallel To*: Adding a Rail, which is parallel to the selected one. For more information look further down of this documentation.
    - *Before Rail*: As 'After Rail' But you add this Rail at the green dot of your Track, the Beginning.
3. That are some only read variables. They show the world rotation of the rail, and the world height. Later this will be important for us
4. Here you can define the Rail Type of a Rail. Just insert the path of the railtype.tscn in it. Example: `res://Resources/Basic/RailTypes/Road.tscn`
5. Here you can define how much curved the Rail is and how long it is. There are three modes which all have two of these variables:
    - *Length*: You can define how long the rail is (Maximum is 1000) (It is measured in meters)
    - *Radius*: Here you can define how sharp the curve of the track is (Radius of the imagined Rail Circle) (It is measured in meters). 
        - 100: very sharp
        - 10000: almost staight
        - 0: straight
    - *Angle*: Here you can define how much the Rail will change its world rotation (It is measured in degrees). That is very helpful for building switches later.
If you don't know which Mode is the best, I personally recommend 'Length - Radius' or 'Length - Angle'. I personally use 'Length - Angle' in the most cases in building rails.
6. Here you can set the slope settings of the tracks. For more information look further down of this documentation. Just ignore this for now
7. Here you can set the tendency settings of the tracks. For more information look further down of this documentation. Just ignore this for now
8. To save and apply the Rail Configuration you have to press 'Update' **But for that there is no undo function!**
9. Here is the rail connector. For more information look further down of this documentation. Just ignore this for now

![1](https://raw.githubusercontent.com/Jean28518/Libre-TrainSim/master/Documentation/Images/BuildingRails/1.png)

Also the function 'Manual Moving in Editor' exists. If activated, you can move the rail in the editor via the gizmos. So when deactivated you can't move the rail accidentally.

## Basics in Rail Building:
- Every Rail has a start and an end point. The green one is the start point, the red one the end point. ![SimpleRail](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/SimpleRail.png)
- You can select a rail by clicking on the start or end point of a rail. For now I did't found any good way to hide the gizmo of GoDot, so sometimes it is a bit annoying selecting another rail. Make sure you have the "Select Mode" enabled (Hotkey: "Q") Sometimes it changes if you press e, r or t.
- The path finding for trains later goes over position searching. Also it will compare the rotations of the Rail. But both detections are having some tolerance, so a track which isn't to 100% perfect connected to a rail is also detected as connected. Here are some examples:
    -  These Rails are well connected, the train will drive perfectly over it: ![WellConnected](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/WellConnected.png)
    - These Rails are very messy connected, but the train should drive over it as well: ![NotWellConnectedButTrainWillDetectIt](https://raw.githubusercontent.com/Jean28518/Libre-TrainSim/master/Documentation/Images/BuildingRails/2.png)
    - The Position of both rails is perfect, but the rotation is too different. The train wont drive over this: ![NotConnected1](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/NotConnected1.png)
    - The rotation of both rails is perfect, but the distance between them is to wide. So the train won't drive over this as well: ![NotConnected2](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/NotConnected2.png)
- **Is there any other 'Connection' between the rails except the same location and rotation?** No, theres no further magic. The Route for all trains is gonna be calculated at every start of the game based on the location and rotation. 
- **So how do switches work technically?** Libre TrainSim doesn't have real switches. Sure you can imagine how to build simple switches: Just by adding another Rail to the end of a rail. So in the end two or even more rails are "connected" to the end of a rail. Two define which direction of the switch a train should drive you tell him in his Route settings, which continuing rail he should take. If you dont "tell" it him, it simply takes the first one, he finds. But no fear, we will come to this later.
- **My slope or tend doesn't match to the "connected" rail will that be a problem for Libre TrainSim?** No, it only uses rotation and location for rail finding. 

Now you should be able to build a one way line witch curves. But lets get to some interesting points, the switches.

## Switches - How to build:
### Basic Switch:
- Determine where your switch should start. In my case it starts at an end point of a rail
- I select the rail, and in the rail builder I select `After Rail` and `New Rail`. Now you should end up something like this:

![BasicSwitch1](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/BasicSwitch1.png)

- Now select the first Rail, and add a new Rail after it again, change the Radius or Angle, and update it.

![BasicSwitch2](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/BasicSwitch2.png)

*Congratulations! You builded your first switch!

### Advanced Switch (splitting oneway to double way):
- Start with a simple rail, add a rail after it, and adjust the length of it. (It will later be the length of the whole curve) For Example: 150m.
- After that add a rail to the newly created Rail again. You sould noe end up like this:

 ![AdvancedSwitch1_1](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedSwitch1_1.png)

- Select the third rail (newest) and add a parallel Rail to it, set the distance for ecample to 4.5
- Select the new one, end press at the Rail Connector under Second Rail `Select` and choose `Beginning`
- Select the very first rail, end press at the Rail Connector under First Rail `Select` and choose `End`
- In the end select `Connect`

 ![AdvancedSwitch1_2](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedSwitch1_2.png)

- The result should look like this:

 ![AdvancedSwitch1_3](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedSwitch1_3.png)


### Advanced Switch (In a Curve):
- Start with a simple Rail, add a Rail after it, and set that for example to Angle: 10, Length: 100, add another Rail After it, and add a parallel Rail Whith the distance of -4.5 to it. In the End it should look like this:

![AdvancedSwitch2_1](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedSwitch2_1.png)

- Select the first Rail, add a rail after it, set the new rails angle to the same as the other switch leg. In my case 10. And reduce the length as much as a straight line could be layed between the new leg and the other parallel rail. A bit trial and error. In my case length 45 looks good:

![AdvancedSwitch2_2](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedSwitch2_2.png)

- In the end just connect the both rails with the Rail Connector. (as in the switch above described) And we get a nice curvy switch. **Attention: The Rail connector only works, if the rotation at the start end at the end are the same!!** In our case the end rotation of the first rail is 10, and the beginning rotation of the second one is 10. So it works perfectly:

![AdvancedSwitch2_3](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedSwitch2_3.png)

### Advances Switch: Cross
You wont learn anything new in here, but its good to know.

- Start with a simple Rail, add 3 rails with the same distance (example 50) after it, and in the end the "end" rail, which could be as long as you want. After it ad some parallel rails (example distance 4.5) as shown below:

![AdvancedSwitch3_1](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedSwitch3_1.png)

- Connect with the rail connector follwing rails: 1 and 2, 3 and 4.

![AdvancedSwitch3_2](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedSwitch3_2.png)

- In the End connect 5 and 6 via the rail connector. You can now delete some Rails, if you want.

![AdvancedSwitch3_3](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedSwitch3_3.png)

## Slope:
You also are able to rise and fall rails. In the slope settings you can edit the slope of the rail at start and at end. Unlike other Train Simulators the slope is also calculated with circle functions, so the transition of an slope is very very soft. *(Except the slope change is very very low, then because of floats the slope isn't soft anymore. But you won't need it I guess)*

![Slope1](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/Slope1.png)

Slope is also applied at parallel rails, and could be combined with tendency

But that circle calculation of smooth slope brings problems with it: You cant control very good which height a rail reaches. *(Okay, theoretically we could, but for that you would need a big complex like the normal curves are handled in rails. with radius, rotation, length, angle, and much more. But that would be overpowered at this moment)* So let me show you an example, how you could control that at least a bit:

Add an Rail with length of 50, and set the start slope to 0, the end slope to 7. Add a rail after it and set its length to 200. If you see, the End Hight of the Rail is now 15.74646. We want to come to almost exact 20 meters height, so I add another rail after it, and set its end slope to 0. Then I reduce the length until the end height of almost 20 meters is reached. Thats trial and error In my case its about length = 122. In the end our track will look like this (Just ignore the right one, I only added it for better orientation)

![Slope2](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/Slope2.png)

**Attention**: It is not recommended to build any switches or better formulated: Only parallel rails are supporting simultaneous slope. Also the rail connector doesn't support slopes too at the moment. Theoretically it is all possible but that's gonna be very messy at the moment.

## Tendency:
If a train drives curves, then tracks are tended normally that the train could drive with higher speed.
Libre TrainSim does support this almost simple. 

### Simple Tendency:
We have an start tend and an end tend value. Just define them how you want, you should get the expected results.
For example define a track as length 200, angle 10, start tend 4 and end tend 4. Great: 

![Tendency1](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/Tendency1.png)

Also different values are no problem, just try it out.

### Advanced Tendency:
You could define some more "tendency points" at one track. Lets assume you have the following track:

![AdvancedTendency1](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedTendency1.png)

What could we do if we want to have tendency in our curve, but wont affect the straight rails? For that we can define some additional tendency points which can be defined at the tendency settings too. If almost one of these points position is -1 then they are deactivated. Lets define the tend points like in the image below shown:

![AdvancedTendency2](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedTendency2.png) 

Why the start tend and end tend don't have any position, is obvious. Lets define tend 1 point. The curve is 100 m long, so lets set the tend point position to 20 (20 m). Thus tend 2 point position should be at 80.
Lets set define the points such in the following image:

![AdvancedTendency3](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedTendency3.png) 

And we have a wonderful result:

![AdvancedTendency4](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/AdvancedTendency4.png) 

**Automatic Tendency**: If you want nice tendency very fast, you could activate automatic tendency. Then the two inner tendency settings are calculated automatically. I am using this setting all the time.

![Automatic Tendency](https://raw.githubusercontent.com/Jean28518/Libre-TrainSim/master/Documentation/Images/BuildingRails/automatic_tendency.png)

## Parallel Rails
Maybe you used it already in building some switches. And maybe its complete easy for you how they work, but let me explain to you: If you create a parallel rail then this new rail is very special. It is attached to the "old" rail, and gets his all information from the "parent" rail. You just could adjust the parallel distance to it. That makes it very easy for building parallel tracks, and makes Libre TrainSim very powerful, but it also has it's special characteristics: 
- If its "parent" rail is deleted, or even the name is changed, then the parallel rail becomes useless, because its "born" to be completely dependent to its parent rail.
- Also the parallel status of this rail can't be changed. 
- *(But in game it is for trains and all other modules a wholesome rail, but rather still depends internally to the parent rail)*

## Rail Connector
Probably you learned about it while creating some switches.
But here are all important notes about it:

**Which Rails could I connect?**
- The rails shouldn't be disanced more than 1000m. 
- The rails should have the same rotation at the relevant ends. 
- The rails should have the same height
- The relevant rails shouldn't have any slope at the specific ends

**How to connect two rails**:
![RailConnector1](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/RailConnector1.png)
1. Select the first rail
2. Press in the rail connector at the fist rail `Select`
3. Choose at the first rail `End` because, we want to connect here the red point (=End) of the rail.
4. Choose the second rail
5. Press in the rail connector at the second rail `Select`
6. Choose at the second rail `Beginning` because, we want to connect here the green point (=Beginning) of the rail.
7. Click Connect. Let the magic happen!

![RailConnector2](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/BuildingRails/RailConnector2.png)

Hint: The rails which where added are completely wholesome, and can be treated as normal rails.

---

Now - That's everything you need to know. If you have any other tips for building rails, or think, there is something missing in the documentation just open a github issue. If you get stuck or just need something more input, watch this video ### TO BE INSERTED ###. In this video almost a whole track was built. And explained how it where done.

***

## YouTube Video: [Click Here](https://youtu.be/p0ycRpTUvfM)