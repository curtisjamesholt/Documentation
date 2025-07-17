---
description: >-
  This page contains a walkthrough explaining the process of installing Python
  addons for Blender.
icon: python
---

# Installing Python Addons for Blender

#### **Installing**

To install any addon, you have two main approaches:

1. Click the ‘install’ button in the addons section of the User Preferences, navigate to the downloaded **.zip file**, and then select it for installing.
2. Manually move the Python addon files into the local directory specified below (and then activate them in the user preferences).

Once the files are in the correct place, then Blender should be able to find them.

* If you installed the addon with method 1, then the addon should appear in the list right away.
* If you installed the addon with method 2, then the addon should appear after Blender has been started, following the installation of files.

#### **Preparation**

1. Make sure you are using a version of Blender that is supported by the addon.(The addon developer should provide this information).
2. Make sure you have the latest version of [Python](https://www.python.org/downloads/) installed on your computer.(External features have a heavy reliance on the Python language).

#### **Downloading**

The addon developer will either provide a link to a [.zip](https://www.7-zip.org/download.html) file, a single Python file. or an uncompressed folder that contains a collection of files (including .py and/or .pyc files).

#### **Where Addons Are Kept**

Blender will detect Python extension files from the [local data path](https://docs.blender.org/manual/en/2.80/advanced/blender_directory_layout.html).

Windows:

* %USERPROFILE%\AppData\Roaming\Blender Foundation\Blender\2.80\Example:C:\Users\\{USER}\AppData\Roaming\Blender Foundation\Blender\2.80\scripts\addons

macOS:

* /Users/$USER/Library/Application Support/Blender/2.80

Linux:

* $HOME/.config/blender/2,80

On Blender’s startup, it will read the appropriate addon/script folder for Python extensions. You will be able to browse these by going to:

* Edit -> User Preferences

In the User Preferences, there will be a section for ‘Add-ons’.This section of the User Preferences contains a list of all the extensions available with the installed build of Blender.Some useful extensions come pre-packaged with the software. You can choose to show user-made addons by using the ‘Community’ filter.

Once you have installed the new addon, it will appear in the list. You can find it easily by using the search bar.

#### **Common Issues**

There are a number of common issues that people might encounter when trying to install Python addons in Blender. I have tried to list as many as possible below:

* **Classes cannot be imported.**
  * **Issue:** This usually occurs when a previous version of an addon has been removed and a new version of the same addon is being installed using the ‘install’ button straight afterwards. The issue occurs because current versions of Blender do not re-load the addons after one has been removed from the User Preferences. This means that the classes of the previous addon are still registered with the opened instance of Blender.
  * **Solution:** Remove the previous version of the addon, restart Blender, and then install the addon using the ‘install’ button in the User Preferences.
* **Computer username preventing addons from installing.**
  * **Issue:** It has been reported that users whose name contains non-standard characters, or characters from other alphabets such a Cyrillic, may encounter trouble when installing Python addons.
  * For now, there is no simple solution other then completely re-naming the user on the computer, including within all relevant directories. This issue will require further investigation.
* **Install button not doing anything after selecting addon.**
  * **Issue:** It has been reported that the ‘install’ button in the User Preferences may not properly install the addon after an appropriate zip file (or Python file) has been selected.
  * **Solution:** A few users have reported that after manually installing Python on their computer, the ‘install’ button started properly installing the addons in Blender.
* **Version mismatch.**
  * **Issue:** General functionality does not work, or Blender throws unexpected errors when trying to activate the addon.
  * **Solution:** It is possible that the problem is due to incompatible versions. As Blender is updated, changes may be made to the Blender API that can break older version of addons. See if the addon creator has provided any version information to help solve this issue. As a general rule-of-thumb, always try to make sure you are using the most recent stable version of Blender.
