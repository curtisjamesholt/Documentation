---
icon: circle-info
---

# Debugging in BY-GEN

BY-GEN V10+ comes with a few debugging features which are described below.

### Debug Mode

In the Settings panel in the 3D view interface, you may see a checkbox for 'Debug Mode'. When this is ticked, every time you import an effect / logic library using BY-GEN, important information will be sent to the system console.

<figure><img src="../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

If you are unsure of where to read the system console, this will vary by operating system.\
On Windows, you can simply go to Window - Toggle System Console from inside of Blender.\
On Mac and Linux, you may need to run Blender from the command line to see the console feed.\
See the [Blender documentation](https://docs.blender.org/manual/en/latest/advanced/command_line/) for more information on running Blender from the console.

### Output to Log

For people that are unsure about finding the console to read the output, ticking 'Debug Mode' will make a second option appear in the settings panel, which is 'Output to Log'.

If this is ticked, the console output will be duplicated and sent to a text file called log.txt in the root directory of the addon. This will be at roughly the following location (remember the directory will change depending on the user layout for your system):

```
Linux:
$HOME/.config/blender/5.0/scripts/addons/BY-GEN/log.txt

macOS:
/Users/$USER/Library/Application Support/Blender/5.0/scripts/addons/BY-GEN/log.txt

Windows:
%USERPROFILE%\AppData\Roaming\Blender Foundation\Blender\5.0\scripts\addons\BY-GEN\log.txt
```

If you are having trouble finding this location, another shortcut is to press the 'Local Content Packs' button in the settings panel and move one folder up, which should take you to the root directory of BY-GEN.

### What Does the Log Show?

Let's take a look at an example of a debug/log output after applying a logic library to an object.

{% hint style="info" %}
Note: With subsequent versions of BY-GEN, the specific information shown in the log may change.
{% endhint %}

```
Timestamp: 2026-01-11 14:05:21
DEBUG: Blender version: 5.0.1
DEBUG: BY-GEN version: 10.0.0
DEBUG: OS:Windows10
DEBUG: Architecture:AMD64
DEBUG: Object name: Cube
DEBUG: Using import method (S). Directory seen to exist. Effect seen to start with (S).
DEBUG: name is: (S) Surface Distribution
DEBUG: Directory is: C:\Users\curti\AppData\Roaming\Blender Foundation\Blender\5.0\scripts\addons\BY-GEN\content_packs\Official\Official.blend
DEBUG: Does .blend file exist: True
DEBUG: tree_directory is: C:\Users\curti\AppData\Roaming\Blender Foundation\Blender\5.0\scripts\addons\BY-GEN\content_packs\Official\Official.blend\NodeTree\
DEBUG: End path separator DETECTED
DEBUG: Final appending string is: C:\Users\curti\AppData\Roaming\Blender Foundation\Blender\5.0\scripts\addons\BY-GEN\content_packs\Official\Official.blend\NodeTree\(S) Surface Distribution
```

Notice that the log contains general information about the user's system (operating system and architecture) as well as the version of Blender and BY-GEN being used. It would be prudent for the user to make a note of the version of BY-GEN being used.

Separately, information on the directory structure of the effect being imported is also provided. This is often a source of issues, especially if the directory structure is not appropriate for the operating system, or if there are naming parity issues within the content pack structure. Check the '[Creating Content Packs](turning-asset-libraries-into-content-packs.md)' page for more information on the naming parity requirements for BY-GEN.
