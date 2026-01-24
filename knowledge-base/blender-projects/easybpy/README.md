---
icon: file-pen
---

# EasyBPY

#### Installation

Place the easybpy.py module in the ‘modules’ folder of your Blender user preferences. On windows, this will be located in:

* C:\Users\USER\AppData\Roaming\Blender Foundation\Blender\2.91\scripts\modules

If any of the folders do not exist, create them! Blender will look for them when you start the program. Please [watch the introduction video](https://www.youtube.com/watch?v=ybnapDe4-Ts) to see how this works.

**from easybpy import \*** <- Use this line in the text editor or Python console to import the module.

If using EasyBPY in a separate addon, remember to package it inside your addon folder and point to it directly when importing the functions, to prevent conflicts with the user’s installed module:

**from . easybpy import \*** <- Use this line if you are importing inside of a packaged addon (adjust depending on your folder structure).

#### Where To Start?

The best place to start with EasyBPY is the [landing page](https://curtisholt.online/easybpy), where you can get a quick breakdown of the different features.\
Please also consider reading [this blog post](https://curtisholt.online/blog/easybpy) to get a feel for the design philosophy of the project.

Following this, feel free to take a look at my age Examples post to get a feel for how the module can help you:

{% hint style="info" %}
[EasyBPY Usage Examples](easybpy-usage-examples.md)
{% endhint %}

#### What Functions are Available?

The **easybpy.py** file is categorized with regions so all functions are kept in a neat order, open them up and take a look. If you’re concerned about argument contexts, you already know enough to read the code.

> **Tip:** If using Visual Studio Code to open the file, press CTRL+K+0 to collapse all regions, this will help you to navigate the categories of the file faster.
