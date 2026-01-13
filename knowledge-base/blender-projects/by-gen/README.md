---
icon: biohazard
---

# BY-GEN

<figure><img src="../../../.gitbook/assets/BY-GEN 10 Cover JPG.jpg" alt=""><figcaption></figcaption></figure>

### Introduction

BY-GEN (V10 and onwards) is a usability addon designed to simplify the artistic workflow of using geometry nodes for procedural and generative effects.

The workflow is simple:

* Select one or more objects.
* Select a 'logic library' from one of the major categories (surface, mesh, volume).
* Apply the effect to the selected object/s.

Depending on the logic library selected, one or more geometry nodes modifiers will be added to the target object/s.&#x20;

{% hint style="danger" %}
**Note:** BY-GEN V10 has been built for Blender 5.0+
{% endhint %}

***

### Import Methods

The exact method of importing the content will also depend on the naming convention used. For example, geometry nodes effects that start with '(S)' are considered 'simple' effects, meaning only a single geometry nodes modifier needs to be constructed on the selected object. Alternatively, '(Ts)' effects import a template object from the content pack file and migrate the entire modifier stack to the originally-selected object, automatically assigning object references to the target object. This is a heavier procedure and will only be appropriate for specific workflows.

***

### Content Pack and Asset Libraries

Content packs can be added to BY-GEN via the 'content\_packs' folder in the addon's root directory. They can also act as Asset Libraries, provided the geometry nodes trees have been flagged as assets in the blend file. The node trees within the official content pack that comes with the BY-GEN addon have already been marked as assets, meaning you can optionally assign it as an asset library within your user preferences.

{% hint style="info" %}
Learn more about [Asset Libraries](https://docs.blender.org/manual/en/latest/files/asset_libraries/introduction.html) in the official Blender documentation.
{% endhint %}

See the following page for more information on creating content packs (or making asset libraries compatible with the BY-GEN content pack system):

{% hint style="info" %}
[Creating Content Packs (Including From Asset Libraries)](turning-asset-libraries-into-content-packs.md)
{% endhint %}

***

### Debugging

BY-GEN V10+ allows for debugging information to be exposed to the console or written to a text log, which should simplify the process of identifying issues. See the linked page for more information:

{% hint style="info" %}
[Debugging in BY-GEN](debugging-in-by-gen.md)
{% endhint %}

***

### For Developers

Below is some information specific to developers of the BY-GEN addon (or anyone making alternate versions of the addon).

{% hint style="info" %}
[Can I Sell Content Packs for BY-GEN?](can-i-sell-content-packs-for-by-gen.md)
{% endhint %}

{% hint style="info" %}
[BY-GEN Layout for Distribution](by-gen-layout-for-distribution.md)
{% endhint %}
