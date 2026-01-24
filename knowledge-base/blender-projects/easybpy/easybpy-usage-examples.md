---
icon: circle-info
---

# EasyBPY Usage Examples

Here are a few examples and use-cases of using EasyBPY to improve your workflow. Feel free to try these out inside of the text editor window in Blender. You can run the scripts by going to Text - Run Script or by pressing Alt+P while hovering over the editor.

#### Removing all materials from every object and cleaning the file of unwanted data.

* Line one imports all functions from the EasyBPY module.
* Line two selects all objects in the scene (with mesh content).
* Line three begins a loop. **so()** is a small convenience function which returns a list of all selected objects. You don’t have to use this, an alternative would be to use **selected\_objects()**, but using the convenience function just keeps things neat.
* Line four removes all materials from the provided object ‘o’, however this function does not have to receive an object reference as an argument, it can also receive a string, list of object references, or a list of string names for objects. This is part of the multi-purpose argument philosophy of EasyBPY.
* Line five clears the file of unwanted data, this is the equivalent of going to File -> Cleanup -> Unused Data Blocks.

<figure><img src="../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

#### Adding a subsurf modifier to a cube with different coding styles.

This is an important example to show how some of Blender’s API functionality is implicit - when you create a primitive, it is selected by default. Traditionally, using **bpy.ops** does not return a reference to the newly-created object, but in EasyBPY it does. Because the cube in this case is selected by default, calling **add\_subsurf()** will perform the action on the cube automatically, however as you can see in the second example, passing a direct reference to the object can override this implicit behavior. You can also grab a reference to the modifier from the function, meaning you can start adjusting values, like **sub.levels**, immediately.

<figure><img src="../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

#### Linking textures to emission nodes for objects following a certain naming convention.

This script was used in the production of my ‘[Best Way to Learn Motion Graphics](https://www.youtube.com/watch?v=hVEIfXon51A)’ video. I would import images using the import images as planes addon (pre-packaged with Blender). The images needed to have emissive shaders but the import settings were not working for the addon, so I needed to write a quick script to fix this as it would be too much effort to do it manually.

More than this, I also wanted to set the images to a consistent scale, however I did not want all objects in the scene to be re-scaled. That is why the script looks for objects without ‘X’ in the name before adjusting their size. It was a quick way I could make objects exempt from the change.

See how EasyBPY simplifies the process of getting, creating, linking and deleting nodes with: **get\_nodes**, **create\_node**, **create\_link** and **delete\_node**.

<figure><img src="../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>
