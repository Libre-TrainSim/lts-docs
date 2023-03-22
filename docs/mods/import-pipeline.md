# Import pipeline

!!! note "Docs merging note"
    Needs revisit. The info given here is partly false.

First of all: Which types of own content is currently supported?
- Any type of landscape object without animations, without lights
- Trains (head to "Trains" Article)

For now LOD Objects aren't supported

## For what do you need to pay attention?
- The best/only type of static 3D Object File Format you should use .obj
- For animated objects (e.g. passengers) .gltf format was used. (with separate materials)
- Try to reuse Materials! Under res://Resources/Basic/Materials/ you find many pre-configured Materials. The good aspect at them: They will be updated with newer versions, and will look nicer over the time. If you use your own materials, they won't be updated unless you will update your materials.
- Of course you should pay attention to the vertex count of your object. 
- It is highly recommended to use the metrics in the 3D Creation Programm too. Try to use real scales. -> That will it make much more easier.

## File Structure:
Save .obj files to `res://Resources/YourTrackName/Objects/`, .blend files to `res://Resources/YourTrackName/Objects/`.

Resources you use for a train, you should save directly in the "Train Folder". For more details read the Train Article.

## Lighting
Lighting is a big problem in Godot/Libre TrainSim, because the engine currently can only handle 8 Light sources for an object / Track Object. So try to use as few lights as possible! Importing lights from 3D Software is not tested. It is highly recommended to light your world separately from the objects with the lights of godot.

**How to add lights:**
Make sure the `Buildings` Node is selected, and press `Ctrl a` or the plus at the top of the item list. Then Search for "light". OmniLights are very recommended. Spotlights are okay too, but in the most cases you wont need them. 

![1](https://github.com/Libre-TrainSim/Libre-TrainSim/blob/master/Documentation/Images/ImportingSelfMadeObjects/1.png)

*Make sure, that these lights will be direct childs of the `Buildings` Node. Currently there comes no automatism with it, which looks after it.*

## Materials:
There are many Materials in the `Basics` folder. Try to reuse them as much as you can -> better performance ;). If you want to modify/add another material, you should create your own material and save it to `res://Resources/YourTrackName/Materials/`. For more information look [here](https://docs.godotengine.org/en/stable/tutorials/3d/spatial_material.html).

## Reusing Objects:
At most times it saves a lot time if you start modelling an object by modifying a existing similar object. Feel free to use .blend files, textures, and materials of the `Basic` folder any time. If you want to reuse some content of other authors, look to the LICENSE file in the authors folder, and check if you could do it. (Or just ask them ;) )

If you want to contribute to the `Basics` folder, just open a new issue on github or do a 

## Licensing:
Please add a `LICENSE` file to your author folder. Recommended Licenses for your content is: https://creativecommons.org/licenses/

If you want to allow that anyone can do anything with your content, then [CC0](https://creativecommons.org/share-your-work/public-domain/cc0/) is the right license for you. For example the `Basics` folder has this license.

### YouTube-Video: [Click Here](https://youtu.be/qZrul1Gagv8)
