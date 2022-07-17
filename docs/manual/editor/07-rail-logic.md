# Rail Logic

## Basics
Why are signals, train stations, speed limits, and contact points handled in one article? Because technically they are very similar, and work all same. 

***Technical Background***: A signal point registers itself at his attached rail. This attached rails saves all signal points with position, which are attached to it in a list. If a train drives over this rail, the train takes this list with all signal points and checks, from now on, if he drove over a signal point. If he drove over it, and it has the same direction as the train self, the train activates a 'signal' function in itself and that function decides dependent of the type what to do. That works for all types of signals (signals, train stations, speed limits...).  (From version 0.6 the train is more intelligent, and could search in his route for the next signal. That makes for example the autopilot possible).

So what similarities do they all have together?
- The way how the train recognize them
- They are always attached to a rail on a specific rail position, with a specific direction.
- The way how you add them into the world

**How to add a signal point:**
- At first select the rail, on which you want to add the signal point.
- Open in the the FileSystem at the bottom left corner the following path: `res://addons/Libre_Train_Sim_Editor/Data/Modules` Here you see all basic Modules of which Libre TrainSim exists without the Train ;). From here you can drag and drop a module to the 3d view. These signal points you could add:
    - ContactPoint.tscn
    - SpeedLimit.tscn
    - Signal.tscn
    - Station.tscn
    - WarnSpeedLimit.tscn

![1](https://raw.githubusercontent.com/Jean28518/Libre-TrainSim/master/Documentation/Images/Signals/1.png)

- Select the signal in the 3D View, and then you could define in the Inspector the rail position and the direction.

![2](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/Signals/2.png)

- In my case I set it to the following properties. My rail is 135 m long:

![3](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/Signals/3.png)

Great! You now know the basics about signals points. 

## 'Normal Signals':
Since version 0.8 you can create your own visual instances for signals and can specify the path under `Visual Instance Path` of a signal. For creating own visual instances for signals an article will follow.

![4](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/Signals/4.png)

So well, the basic function of a signal is very very easy. Its the status variable: Is the status set to 0, the signal is red, and no train should pass. If the status is set to 1, then its green or orange, and the train can pass the signal. 

With the `Set Pass At ...`  Variables you can define a time, when the signal sets its status to 1. That is very useful at signals at a station. *(This could happen just one time ingame. Generally it is recommended just to use this functions for the "Player" train.)* 

![5](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/Signals/5.png)

In This example the signal is set to status = 1 at 14:30:00 or 02:30:00 pm. 

Also you can define a speed limit in km/h which should be applied, if the train drives over it. If it is set to -1, then this is ignored.

**How can I configure, that the signal shows orange, or a Warn Speed Limit (orange digits)?** That is set automaticly by the signal. *(All trains are configuring at the beginning of the simulation the signals, and "say" them, which signal they will drive over after the signal. From there the signal checks the status and the speed limit "after" the signal it self, and set itself if necessary to orange, or/and shows the orange digits.)*

- Green: Train can pass (Status 1)
- Orange: Train can pass, next signal shows red. (Status 1)
- Red: Train should not pass. (Status 0)

**Block Signal**: If this mode is active, then the signal works 'automaticly'. At default the signal is green. It turns red, when a train drives over, and will turn green again, if the train drives over the signal behind it. (The signal behind it don't have to be a Block Signal necessarily. When a train despawns, the signal will recognize it also). *The only point: THe Block Signal don't recognize, when a train spawns behind it. It only turns red, when a train drives over it.*

## Contact Points:
What does a Contact Point? If a (optional: specific) train drives over it, the contact point activates (optional: after some seconds) a signal, end set it to a defined status and speed. With that feature complex Signal Processes are possible. 

![6](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/Signals/6.png)

- **Affected Signal**: The Signal Name in the scene tree of the Affected Signal.
- **By Specific Train**: If the Contact point should be activated by a specific Train. (Name of it). If every train, who drives over it, should activate this point, that variable has to be empty.
- **New Status**: Self explaining
- **New Speed**: Self explaining
- **Affect Time**: Time in seconds, after it the signal should be set. Set it to `0` if the signal should set immediately.

In the example above the signal called `Signal` will be set to status = 1 with speed 80 5 seconds after any train drove over this contact point.

## Station:
Look to article 'Train Stations' for more details.

## Speed Limit:
First of all: At the moment it is not easy/possible to change the signals look or model. That will be implemented for version 0.8.

Very simple:
If a train drives over it, the speed limit which is set in the variable `Speed` will be applied. It shouldn't/can't be changed Ingame, because it is a static sign ;)

![7](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/Signals/7.png)

## Warn Speed Limit:
First of all: At the moment it is not easy/possible to change the signals look or model. That will be implemented for version 0.8.

That's even simler than the normal Speed Limit. It just announce the player, which speed limit is the next one. *(Normally just set, if the next speed limit is lower than the current one)*.
It doesn't set itself automatically, or has any effect to the trains.

### YouTube Video: [Click here](https://youtu.be/OMS1oaVrfwA)