---
icon: message-pen
---

# Patreon Fund January 2026

<details>

<summary>2 January 2026</summary>

* Getting Charan set up with GitHub Desktop so we can better sync changes for BY-GEN.
* We have also synchronised references and inspiration content.
* Charan will be converting effects to use bundles and closures now that Blender 5.0+ is available, keeping in mind that when we were experimenting with approaches, bundles and closures were not guaranteed features.
* Creating a branching growth effect for the surface effects, aiming to have at least three effects per pillar of the addon.

\+ 1 hour 33 minutes

</details>

<details>

<summary>3 January 2026</summary>

* Continuing with developing Ivy Growth.
* Experimenting with a deconstructive mesh effect.
* Working on Ivy generation effect.

\+ 2 hour 26 minutes.

</details>

<details>

<summary>4 January 2026</summary>

* Work continued on simulation-like features.
* I am adding effects to the official content pack - volume advection, volume plexus. Waiting for Charan to finish Ivy. Waiting for reaction diffusion.

\+ 35 minutes

</details>

<details>

<summary>6 January 2026</summary>

* Getting reaction diffusion done and light usability checks on the node groups of current effects, adding frames and info where appropriate.
* \+ 50 minutes

</details>

<details>

<summary>8 January 2026</summary>

* Replacing the ivy growth with a simpler version for the base version of V10, holding on to the more complex version.
* Adding reaction diffusion to the official content pack in preparation for V10 release.
* Doing a usability check from empty file, noticed surface growth needs some default parameters changed to make the effect properly visible, and reaction diffusion needs to be applied to the source mesh as it was using a generated icosphere for testing.
* More usability testing.
* In \_\_init\_\_ and effects.py, added debug\_mode property and put into settings panel as a toggle, which we can use to enable debugging output in the console. Hopefully we can use this to let people give us more information when they encounter issues - specifically in regards to directories, as that seems to be the most common issue.
* Hiding weight paint option for applying surface effects, as won't be appropriate in all cases and seems like a point of potential issues as geometry nodes develops into the future.
* Removed old tools panel from panels.py.
* Removed panels.py and ui folder as these were no longer necessary.
* Removed interpreter folder and associated py file as this was no longer necessary.
* Massively trimmed down init file and removed old scatter and generation / modify files as they are no longer necessary. This should reduce the code size and registration time of the addon.
* Removed resources folder with the surface effects blend file as it was not being used.
* Removed geonodes.py module file (which I never continued working on) as it was not being used, but it will still exist in the workspace of previous versions if I want to return to it.
* Removed spatial.py module file as it was not being used.
* Removed randutils.py module file as it was not being used.
* Moved easybpy module to the root addon folder and removed the modules folder since there would have only been the single easybpy file in it anyway.

\+ 2 hour 24 minutes

* Removed BYGEN\_OT\_surface\_effect\_weight\_paint, as we will not be having the weight painting specific import anymore. This means we have a bunch of argument we can remove from the import function.
* Trying to remove unnecessary arguments from the import function, and update the calls from surface, mesh and volume effects to reflect this.

\+ 50 minutes

* Fixed a bug, avoiding applying effects if invalid object types are selected.

\+ 24 minutes

Total: 3 hours 38 minutes

</details>
