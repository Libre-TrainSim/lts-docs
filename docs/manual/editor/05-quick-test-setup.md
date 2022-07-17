# Quick and dirty track testing

If you built some track, you definitively want to test your track out. We will do this very fast. For more details look in the chapters how scenarios and the world is set up.

1. Select `Configuration` next to the RailBuilder Tab (Maybe you have to use white arrows at the end of the tab list)

2. Fill in the World Config, its completely irrelevant, what you insert there. After that press `Save World Config`.

3. Select `All Chunks` and click `Unload and Save Chunks`. After that your world should be empty. **Everytime you changed/added a rail, or changed something in `Buildings`, `Flora` or `TrackObjects` and want to test out your track, you have to unload and save chunks before.** After testing you could load all Chunks again.

![3](https://raw.githubusercontent.com/Jean28518/Libre-TrainSim/8d93d211a1c0bb1f6efeae8acc3806b3979361c0/Documentation/Images/TestingTrack/dirty_world_configuration.png)

4. Switch to the `Scenarios` tab. 

5. Create here a new scenario by writing something in (1) and then press `New` (2).

6. Press at `Save General` and at `Save current Signal Data to scenario` **Every time you changed something important for your Scenario in `Signals`, you have to save the current Data to the scenario** If you don't have any Signals yet, you can ignore this. But `Save current Signal Data to Scenario` You should press even so.

![4](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TestingTrack/4.png)

7. Head over to `Trains` write 'Player' in the text field, and click on new. 

8. Insert the name of the Rail, the train will start. at `Start Rail`. Also you can define the Direction of the Train at the Start Rail. 

9. If you want, that the train drives a specific route over your world, you can insert the names of the rails he should definitely pass into the `Route` field. Seperate the Rails with a blank (` `). That field can be completely empty too. This is completely optional.

![HowToAddARoute](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/HowToMakeConfigureARoute.png)

10. Press in the End `Save Train`

![5](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TestingTrack/5.png)

11. Click at the play icon in the top right corner, and select your track from the Main Menu. 

![6](https://github.com/Jean28518/Libre-TrainSim/blob/master/Documentation/Images/TestingTrack/6.png)

12. By pressing `Ctrl` + `Y` you can toggle debug mode. with it you can drive very fast. Have fun at testing!

***

## YouTube Video: [Click here](https://youtu.be/RmR11yhq1D8) 