# Station Setup

Lets build a train station. You already should have builded your rails. This is, how we gonna start:

![1](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/1.png)

*We will only discuss the relevant points about doing a Train Station. After this article you are ready to test out your track with the train stations and getting a first feeling how your track will be in the end, and if it will make fun*

## Platform:

My train station will be 135 m long, and there will be a platform in the middle. Lets build our first Objects to the track. For that you have to open the tab `Rail Attachments` next to the Track Builder Tab, and select a rail. It will look like this:

![2](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/2.png)

Lets add a new Track Object by typing in the field e.g. `Platform` and by pressing the `New` button. In the end select your newly added entry. In the end it will look like this:

![3](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/3.png)

You now need to specify a .obj file for your object. Select `Pick`and select `Platform-1_double.obj` in `res://Resources/Basic` for example. Alternatively you can paste your path `res://Resources/Basic/Platform-1_double.obj` to the text field. *(Of course you can later select your own custom object. But for that read the article about adding your own content to Libre TrainSim)*

Now select the Tab `Position` and make sure `Assign WholeRail` is activated. Then your platform will be set over the whole rail. Alternatively you can define a specific position. Now click on `Save`.

Select the tab `Object Positioning` and adjust the values like below:

![4](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/4.png)

Press `Save` and `Ùpdate`. If everything goes right, then you should see a crappy looking platform.

![5](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/5.png)

That's because we didn't set the Materials properly. Under `Object` you can add Materials. Click on `Add` under Materials and select `pick` and select following Materials. They should have the same order. 

![6](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/6.png)

If you accidently added more Materials than in this case 3, just leave them empty, Libre TrainSim will recognize that. In the end it will look like this:

![7](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/7.png)

Now add platforms on the other train stations too. To copy a TrackObject just select `Copy` under the list, select another rail, and select `Paste`. (Of course you can later change the platforms, and detail your platforms better.

## Adding Train Station Logic:
Now we need to say to Libre TrainSim where a Train Station is. For that navigate in the `FileSystem` tab at the left bottom corner to `res://addons/Libre_Train_Sim_Editor/Data/Modules/`. *(You can also search for `Station` in the FileSystem, that's faster.)* Select the rail, where you want to assign the train station. Now drag and drop `Station.tscn` to the 3D View. 

![8](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/8.png)

Now select the new blue sphere, and select the Inspector on the right screen. Here you can define the Station Length, Position, and much more. After that select `Update`. Also it is recommended to rename the train station. In this Example the settings are:

![9](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/9.png)

Now repeat this at every wail, which whether ai trains or the player should halt at a station.
For the other rail (on which the trains will halt at the other direction) the settings look like this:

![10](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/10.png)

**Attention**: Please keep in mind, that you shouldn't order any nodes in the Scene Tree. Every Rail should be a direct child of `Rails`, every signal, train station, speed limit... should be a direct child of `Signals`, and so on. ;) 

![11](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/11.png)

## Creating Simple Timetable for testing route:
**Make sure you followed the article 'Testing Your Track') properly, or this will not work**
You now should have defined every train station node. Lets create a timetable for our player train, that Libre TrainSim knows, on which station and when the train should halt.
Select the `Configuration` Tab, select or create a new scenario, select `Trains`, and then select or create a train called `Player` 
It should now look similar to this:

![12](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/12.png)

Fill in the route, (like in the article 'Testing Your Track' described), and add timetable entrys. It should be self explaining. 
- Under `Node Name` insert the name of the station node, which we defined above.
- Under `Station Name` insert the name of the station how it is called ingame
- Arrival Time and Departure Time are self explaining. For just testing you could leave them at 0. 
- Minimal Halt Time: How long the train should halt at a minimum. (Unit: Seconds)
- StopType is self explaining too.

In the end my timetable looks like this:

![13](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TrainStations/13.png)

Make sure you select `Save Train` in the End

Now you could test it out! (Press ctrl a in the train to activate the autopilot to get a neutral reference. How this track is driven in the end. 

If your train does not hold at a station, you wanted:
- Is the Node Name written in the Time table correctly?
- Is the Train Station placed in the correct direction?  (Check Forward Property at the Train Station Node)
- Is the halt type correctly set in the timetable?

***

### YouTube Video: [Click here](https://youtu.be/yOFAHt3I9D8)