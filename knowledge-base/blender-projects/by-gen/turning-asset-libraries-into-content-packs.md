---
description: >-
  This page describes how to convert traditional asset libraries (containing
  geometry nodes content) into content packs compatible with BY-GEN V10+.
icon: circle-info
---

# Turning Asset Libraries into Content Packs

{% hint style="warning" %}
This page is under development.
{% endhint %}

A few conditions have to be met for an asset library to be understood by BY-GEN. They are described below.

### Step 1 - Uniform Folder and Naming Convention

Your asset library needs to exist within its own self-contained folder. For example, the standard content pack that comes with BY-GEN is called 'Official'. Inside of the 'content\_packs' folder in the root directory of the addon, you will see the 'Official' folder. Inside of this folder is 'Official.blend'.

Therefore, if youre content pack was called 'MyContent', you would need to create a folder called 'MyContent' which includes a blend file containing your assets named 'MyContent.blend'.

### Step 2 - Give the Geometry Nodes Trees a Proper Prefix

The names of the geometry nodes effect are extremely important for BY-GEN to understand what method should be used to apply them to the user's selected object/s.

For most cases, the '(S)' prefix is appropriate, as this represents the 'Simple' method, which simply imports a single node tree from the content pack file, creates a geometry nodes modifier on the object, and assigns the imported node tree.

Therefore, if your geometry nodes tree is named 'My Effect', you should rename it to '(S) My Effect'.

There are other import methods available, represented by alternative prefixes, but they will not be described here.

### Step 3 - Flagging Content Via Thumbnails

Instead of directly reading content inside of the blend file, BY-GEN will look for folders that exist \*inside\* of the content pack folder (consequently, next to the content pack .blend file), which have very specific names. These are:

* thumbnails\_surface\_effects
* thumbnails\_mesh\_effects
* thumbnails\_volume\_effects

You will notice that these reflect the main pillars of content in BY-GEN, where each of the categories has a drop-down list within the user interface in the 3D view.

For each of the effects (geometry nodes trees) you want to make available to the user, you must create an associated thumbnail and place it in one of these folders. As you may have figured out, if you wanted an effect to appear in the 'Surface Effects' category, you must create a thumbnail for it inside of the 'thumbnails\_surface\_effects' folder.

{% hint style="danger" %}
**But wait! How does BY-GEN know which geometry nodes tree to associate with each thumbnail?**\
The names of the thumbnail images you create **MUST** be identical to the name of the geometry nodes tree you want the user to import.
{% endhint %}

Let's back up for a second to explain this:

If your content pack is named '_MyContent_', you must have a file named '_MyContent.blend_'. \
If that file has a geometry nodes tree called '_(S) My Effect_' (following the prefix naming convention), you must create a thumbnail named '_(S) My Effect.jpg_' (or whatever image file format you choose to use).

If you are unsure what image file format to use for your thumbnails, keep it simple:

* JPG if you don't need the thumbnail to have a transparent background.
* PNG if you need your thumbnail to have a transparent background.

{% hint style="warning" %}
In fact, I'm not even sure if the BY-GEN effect selection supports transparent backgrounds, so I will need to test that. You're getting documentation hot off the press, folks. 😅
{% endhint %}

### Step 4 - (Optional) Associate Objects to Effects

This step is optional (depending on the import method) but highly recommended. For the sake of simplicity, you will likely be rendering thumbnails for your effects from _within_ your content pack file.&#x20;

I tend to have a template object in the scene for each effect, which I can enable and disable on demand to re-render thumbnails. This saves me from having to re-assign geometry nodes trees to the object every time I want to make a change. I also create collections which clearly identify which effects are for the Surface, Mesh and Volume categories.

This inner-file organization is not necessary for BY-GEN to find the content, however it is good organizational practice.

However, despite this step being listed as 'optional', it is **necessary** to have a template object if you are using a more advanced import method, such as (Ts) or (Tr), as BY-GEN will import this object prior to reassigning object targets.

This is another reason why I believe it is good practice to have a unique object in your content pack file for each effect. If you wanted to expand into more advanced workflows in the future, it is more convenient.
