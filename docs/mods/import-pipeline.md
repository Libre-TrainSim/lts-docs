# Import pipeline

This page introduces the import pipeline for LTS. It'll explain supported content, file strucutre, assets, and licensing.

## Supported content

 1. 3D Objects (from landscape to bins to trains)
 2. Sound files

!!! warning
    Level of Detail is currently not supported out of the box.

!!! tip "Good practices"
    - Prefer glTF as your primary export format.
    - Use as much topology as required and as little as possible. If you are new to 3D modelling search for tutorials and guides that show *game-ready* workflows. A good chunk of videos on YouTube for Blender is made for *offline rendering, eg. film or artwork renders*. If the tutorial uses loop cuts to control the beveling of an edge, it's not probably not game-ready.
    - Use proper scaling. One unit in Blender and Godot is one metre. In Maya, one unit is ten centimetres. The object should have a scale of one in Godot.

## File Structure

Always keep your source assets as close as possible to the scene. If you are importing for use as rail attachments, you need to save the meshes in a dedicated folder.

## Lighting

When using glTF (or FBX by all means) lights can be created in your 3D content creation software. However lighting is not only a realistic component but also an artistic one. You should strive to use as few lights as possible but as many as required.

!!! tip
    Have a look at lighting in games and how lights work to guide attention. These are classic level design problems. As we don't have any level designer right now, you are probably better of researching the topic on your own.

## Materials

For more information take a look [at the offical Godot documentation.](https://docs.godotengine.org/en/3.5/tutorials/3d/spatial_material.html).
You want to use something like Substance Painter, Material Maker, or any other alternative you can find. Good materials go a long way in visual quality.

!!! tip
    You can read more about texel density if you are interested in the proper texture sizes. Also use channel packing to combine AO, roughness, and metallness maps to save VRAM.

## Objects

It's perfectly valid to start with existing objects and modify them to get to a coherent visual style. Please make sure you're complying with licenses.

## Licensing

FOSS lives and breathes through sharable and open content. Thus, please ensure to properly credit the external content you used and share your content under a open license. Have a look at [Choose a license](https://choosealicense.com/) and [Creative Commons](https://creativecommons.org/licenses/) respectively.

If you want to allow anyone do do about anything with your content, then [Creative Commons 0](https://creativecommons.org/share-your-work/public-domain/cc0/) is the right license for you. Most assets in the base game are licensed CC0.

### YouTube-Video: [Click Here](https://youtu.be/qZrul1Gagv8)
