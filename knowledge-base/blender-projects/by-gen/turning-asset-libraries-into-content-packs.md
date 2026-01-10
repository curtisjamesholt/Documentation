---
description: >-
  This page describes how to convert traditional asset libraries (containing
  geometry nodes content) into content packs compatible with BY-GEN V10+.
icon: circle-info
---

# Turning Asset Libraries into Content Packs

A few conditions have to be met for an asset library to be understood by BY-GEN. They are described below.

#### Step 1 - Uniform Folder and Naming Convention

Your asset library needs to exist within its own self-contained folder. For example, the standard content pack that comes with BY-GEN is called 'Official'. Inside of the 'content\_packs' folder in the root directory of the addon, you will see the 'Official' folder. Inside of this folder is 'Official.blend'.

Therefore, if youre content pack was called 'MyContent', you would need to create a folder called 'MyContent' which includes a blend file containing your assets named 'MyContent.blend'.

#### Step 2 - Elevating Thumbnails for BY-GEN

Instead of directly reading content inside of the blend file, BY-GEN will look for folders that exist \*inside\* of the content pack folder, which have very specific names. These are:

* thumbnails\_surface\_effects
* thumbnails\_mesh\_effects
* thumbnails\_volume\_effects

You will notice that these reflect the main pillars of content in BY-GEN, where each of the categories has a drop-down list within the user interface in the 3D view.

For each of the effects (geometry nodes trees) you want to make available to the user, you must create an associated thumbnail and place it in one of these folders. As you may have figured out, if you wanted an effect to appear in the 'Surface Effects' category, you must create a thumbnail for it in the 'thumbnails\_surface\_effects' folder.

{% hint style="danger" %}
But wait, how does BY-GEN know which geometry nodes tree to associate with each thumbnail?!
{% endhint %}

The names of the thumbnail images you create MUST be identical to the name of the geometry nodes tree you want the user to import.

Let's rewind for a second to explain this:

If your content pack is named 'MyContent', you must have a file named 'MyContent.blend'. \
If that file has a geometry nodes tree called '(S) My Effect', you must create a thumbnail named '(S) My Effect.png' (or whatever image file format you choose to use).
