---
icon: message-pen
---

# Patreon Fund July 2025

{% hint style="info" %}
**Patreon income:** $280 -> £208.77 -> (£50/h rate for mixed skillset) 4 hours of work.\
**Total time:** 20 hours, 31 minutes.\
**Unpaid overtime:** 16 hours, 31 minutes (£50/h) = \~£825.
{% endhint %}

<details>

<summary>18 July 2025</summary>

* BY-GEN - General Preparation
* Starting with updating to Blender 4.5, transferred appdata from 4.4 to 4.5, things seem to work. BY-GEN already transferred, going to remove to we can link it up with the visual studio code project.&#x20;

- Executing Blender and building with VSCode, BY-GEN linked successfully.&#x20;

* Created Anki deck for BY-GEN to track and reinforce personal knowledge in the future and as we make important rediscoveries.&#x20;

- \[Anki] Understanding that BY-GEN (on the interface side) is split into 3 core pillars and 3 extended features:&#x20;
  * Surface Effects&#x20;
  * Mesh Effects&#x20;
  * Volume Effects&#x20;
  * Structured Generation&#x20;
  * Scattering&#x20;
  * Tools&#x20;
  * (Additionally: Info)&#x20;

* Noticing that the generator's lab content pack was installed as it is kept in our private repo for BY-Gen. Should keep it there for testing purposes, but also don't want to share that when migrating content to public repo. Setting drop down options to official to keep the same.&#x20;
  * Saving startup file to test if the drop down choices persist on Blender restart - they don't seem to, but maybe due to rebuilding of addon. Did the same with version not linked to VSCode, still did not persist, so property must be stored in other place.&#x20;
* In folder space for BY-GEN noticing many folders but it's confusing to know which are related to functionality and which are misc. For example dev folder is just notes, it would be useful to clean this up or to store functionality under a subfolder but this will require a rewriting of references.&#x20;
* Moved notes from the dev folder into onenote space for these notes. Then deleted dev folder to simplify folder space.&#x20;
* Noticing a 'tools' folder which contains a blend file for a depth tool, but I don't think this is referenced in any code, rather there for the user to find and access if needed.&#x20;
* Noticing that inside of the init.py file, under register() we refer to each of the core functionality python files and call their sub .register() functions, meaning classes are defined on a file-by-file basis. That is good because it means we can work independently in each file and know things are registered without having to put an extra reference to it in the init file. However properties may still need to be defined at the init level, inside of BGProperties. This is defined under the region 'Global Variables and Properties'. There are many sub regions for each of the different categories of effects. Some of this information should be distilled.&#x20;
* \[Anki] How is class registration for multiple files handled in BY-GEN?&#x20;
  * \[Answer With Image] Every file is referenced and their associated .register() functions are called. This triggers registration for every necessary file. Any new files should also be given a .register() function and added to the list in init.py.&#x20;
* While looking at the register classes in other files, I'm noticing some complexity where not only are classes registered from a list of all classes defined in that file, but there is also a long list of other properties being defined, destroyed and re-registered (specifically in the effects.py file), which I believe are related to window management for the visual asset selection boxes. Just checking to see if this complexity is also present in other sub-files. Nope, it seems all files under a subsidiary folder 'operators' that also contain functionality code have unremarkable register functions, so effects.py seems like a spike in complexity.&#x20;
* \[Anki] Which files has the greatest complexity on account of shepherding many window management properties?&#x20;
  * \[Answer With Image] effects.py has many WindowManager props as it is responsible for managing the user interface for external effect/asset selection. They need to be destroyed and recreated in specific orders to maintain functionality.&#x20;
* Noticing the changelog file, looks a bit cluttered in the root directory but think we will leave it there because it will be an important one in the end.&#x20;
* I'm also noticing under a modules folder that we were creating other modules alongside easybpy, in particular: a module for simplifying and interacting with geometry nodes. Surely this is something that could be merged with easybpy but I suppose it depends on if there are any specific requirements for it to stay separate, other than references needing to be re-written in the current codebase.&#x20;
* I am also noticing code for the old modifier stack interpreter tool which I believe is sitting unused. We can keep it there in a specific subfolder.&#x20;
* I'm noticing the content\_packs folder and seeing that each pack has subfolders with specific names for thumbnails. I remember now that these thumbnail files indicate the existence of an associated effect in the file. They all need to share a naming convention. I will open up one of the content packs now and take a look.&#x20;
* I see that the name of the thumbnail '(S) Distribute Points in Volume' is associated with a geometry nodes tree name '(S) Distribute Points in Volume) which is assigned to a Volume Effect Cube object. This is only a single geometry node and I wonder if that's what the (S) stood for (single or simple). &#x20;
* I see that the volume effect cube has nothing to do with the geometry nodes effect, as it is stored in a rendering - volume effects collection which we were clearly using for rendering the effects out, rather than creating them. This will be worth making a note of as we are bumping into many different kinds of self-invented conventions here, so we will need a way to remember and write them down. They were likely mentioned on video, but I would be surprised if I never wrote them down, but then again I was never that good at keeping track of behind the scenes decisions for posterity.&#x20;
* I'm noticing that each of the geometry nodes effects in the official content pack have been flagged with fake users for obvious reasons.&#x20;
* I'm seeing that when applying the cross mesh effect to the volume cube, nothing is showing and I have to assign the 'Cross Mesh' collection to the collection info input in the geo nodes tree manually. I will try to apply it in a simple file using the by-gen addon to try and remember the application process.&#x20;
* It did apply correctly, so it seems as though the collection is assigned in the application process. If so, that's a bit annoying to preview for render tests behind the scenes. We will really need to write out some kind of flow chart to help outline the process.&#x20;
* Before adding more to anki, just want to understand the application process so we can see what is actually happening.&#x20;
* I can see under BYGEN\_OT\_volume\_effect\_import that there are cases with some commented notes explaining the difference between (S) and non-(S) type effects and how they have different methods of import.&#x20;
  * (S) type effects have no collection to import so they can go straight into the importing of the geo nodes tree and assigning it to the selected object/s.&#x20;
  * Non-(S) type effects have a collection to import. Apparently the collection needs to be imported before assigning the geometry nodes tree (is that still the case, or can the collection be dragged with the geo nodes tree on import now - I suppose it's not really an asset as such, at least not when it was created. I wonder if it can be recoded to not require separate import of the collection. I suppose if it works for now, then there's no sense in trying to change it as that will likely cause large issues we are not ready to debug.&#x20;
* Noticing there are lots of finite things to remember such as what kind of data types certain variables are in the import process, that's something we can add to anki.&#x20;
* Yes, I can see at line 1417 colinfo = getnode\_nodes, "Collection Info"), after that the imported collection is assigned to the node, meaning that the collections are attached after import. I wonder how we can simplify this for ease of working with the effect in the content pack file, or maybe we can create a helper script to preview the effects. Regardless, we are putting together a better picture of a mental flow chart that we could describe for reinforcement later.&#x20;
*   I'm pretty sure there was another category of effect for geometry nodes beyond S and non-S, so I'm going to have a quick look through files to see if I can find it.&#x20;

    * In this micro investigation, I'm noticing that Mesh Effects (compared to Surface Effects and Volume Effects) is organized differently in the code. After checking the interface, this is represented by Mesh Effects having several submenus that the other categories do not. The subcategories are Parametric, Structural, Displacement and Helper Tools (naturally for extra operators, not effects).&#x20;
    * \[Anki] Which of the core 3 pillars of BY-GEN has additional sub-categories?&#x20;
      * \[Answer With Image] Mesh Effects, which contains Parametric, Structural and Displacement subcategories (at version 9.1.1)&#x20;
    * I'm checking the content for the official content pack subfolder of the project and noticing that instead of the hierarchy being organized from the 3 pillars (parent to child, where mesh effects would have subfolders of displacement, parametric and structural), they are instead all contained at the root of the content pack. The folders are listed as such:&#x20;
      * Thumbnails\_mesh\_displacement&#x20;
      * Thumbnails\_mesh\_parametric&#x20;
      * Thumbnails\_mesh\_structural&#x20;
      * Thumbnails\_surface\_effects&#x20;
      * Thumbnails\_volume\_effects&#x20;
    * \[Anki] What are the common subfolders that would be present in a content pack containing assets for all of the main pillars of content (remembering surface, mesh and volume)?&#x20;
      * \[Answer With Image] List the bullet points above.&#x20;
    * I'm also seeing a region in the mesh effects section of effects.py called 'Mesh Legacy' - I'm unsure what this is but I'd guess it's the old panel from older versions of BY-Gen before the addition of the more visual preset selection interface (I likely kept it in case the custom asset system didn't work and I needed to revert).&#x20;
    * \[ Time: 1 hour passed ]&#x20;
    * I'm going to look inside of the parametric, structural and displacement sections to see if there are any unique behaviours for these compared to the simpler surface and volume effects sections.&#x20;
    * Under 'Parametric' there are 5 areas of code, two are functions and three are classes, two of which are operators for importing (regular and template) and the other is for the panel definition. I will look under the regular import function before the template import (as there may be added complexity).&#x20;
    * After expanding the BYGEN\_OT\_mesh\_parametric\_import class, I have found what I am looking for (from my vague memory), an expanded case with limited commenting for effects that begin with (G). The comments state the following: \
      "Complex geo nodes stacks which require extra base referencing." \
      I really could have done a better job at explaining that. What follows after that is code with various comments on the procedure for successive lines, but no overview explanation of what the process is actually for. In my memory, I remember that either this or another feature was for auto assigning the object reference to multiple geometry nodes effects  if certain conditions were met (for example if 'target' was the name of a certain input, but that might be incorrect). This is something we need to elucidate to create accurate documentation and clear out understanding for making future effects and improving the functionality in the future.&#x20;
    * I'm now going to read the code and try to bullet point the process for (G) preset imports:&#x20;
      * Get the selected object .&#x20;
      * Copy the selected object&#x20;
      * Select the new object.&#x20;
      * Append the template object (even though this is not the template import function, I remember we are using objects to store entire stacks of modifiers and geometry nodes trees \[quite smart, really], so we import the object as a whole which acts as a trojan horse to bring in all of the effects).&#x20;
      * Select only the object we want to apply things to. (the commenting at 685 is confusing).&#x20;
      * At 687, we \*also\* select the newly imported object with all of the modifiers and geo nodes we want to use.&#x20;
      * Call bpy.ops.object.make\_links\_data(type='modifiers') to copy the entire stack from the imported object to the selected object.&#x20;
      * Then select only the originally selected object again.&#x20;
      * Now, loop through all of the new modifiers on our selected object and assign self references (geometry nodes effects that need to reference the selected object).&#x20;
        * For ever modifier&#x20;
          * If it's a node type&#x20;
            * Get all of the nodes.&#x20;
            * Get nodes of the type 'group input'. (This confuses me as I would have thought the object reference might have needed to be made at the modifier stack level, but I guess this is where the object reference is made (the object input is accessible from the modifier stack).&#x20;
            * For every 'group input'.&#x20;
              * If the name in lowercase is 'object'&#x20;
                * Get the identifier (Oh, I see, there is a text based ID for each of the geometry nodes inputs at the modifier stack level, and what we're doing is a bit of 'forensics' inside of the node group inputs to find out which of the inputs actually \*is\* the object reference.)&#x20;
            * Then take the captured identifier and assign the base object with: \
              m\[id] = base, where 'm' is the modifier itself.&#x20;
      * Then do a hacky trick to refresh the viewport by hiding and unhiding the object because updating the view layer alone is not sufficient.&#x20;
      * Then delete the imported template object (the trojan horse that carries the modifiers and geo nodes). People will never know it existed and yet we are left with all of the relevant data.&#x20;
      * (Looking back, I'm quite impressed at myself because that's actually a smart combination of using bpy.ops to speed up the process by letting it manage the importing of multiple types of data (objects, mesh, modifiers, geo nodes, etc.) and then doing some manual work to make our own data links afterwards, especially the 'forensics' to discover the secret ID of the object input. This is quite a lot of information in one go so we should take some time to Anki the process.&#x20;
    * Looking back at that mini-investigation, I'm taken aback by both the complexity and intuitiveness of finding a solution.&#x20;
      1. Using bpy.ops to 'trojan horse' a large amount of data into the blend file (modifiers and geometry nodes).&#x20;
      2. Copy all of the modifier and geometry nodes data to the originally selected object.&#x20;
      3. Do some node forensics to discover the secret object target ID string (such as 'Input\_3') by assessing the actual group input node in the node tree of each modifier.&#x20;
      4. Assign the originally selected object as the target using the newly discovered ID.&#x20;
      5. Noticing that Blender view layer update is flawed so doing a hacky workaround of hiding and unhiding the object we're working on to force a correct update.&#x20;

    (We should Anki this information as this process for the (G) type geometry nodes effects is important. Also elevate this process for mentioning to public on next update.&#x20;
* Something important I've noticed is that there is a lack of parity between the import classes of different pillars, specifically; where I can see (G) type imports in the parametric mesh effects, I cannot see that case being handled in the volume effects, and I'm wondering why. \
  Fundamentally, all imports manage the same types of data, the main difference between pillars is categorical purpose as highted by the user interface, so I'm considering created a new central function to manage imports that handles all geo nodes effects types and accepts arguments that direct it to specific types of categories. Then, without deleting the previous classes, just point them to the new class, so we keep all of the import functionality central in one place which is easier to modify and expand upon, while also keeping the pillars separated on a user experience level.&#x20;
* I'm also taking a look at other mesh effect types, such as structural, and noticing its import mode is much more simple, on account of it being a multi-object effect. I think it might be a good idea to not only have a central import function but also a type for each effect rather than keep things ambiguous, e.g. ( S ) for simple ( C ) for collection ( T ) for target, etc. This would require fundamental renaming and restructuring for template content packs, but it might be worth it for future development and community extensibility. It would also be easier to demonstrate to people and explain in documentation.&#x20;
* Created a new region in effects.py for work on this central import function - #region V10 WIP.&#x20;
* To start with, I have created the shell of a function as def import\_content, but I am looking at the necessary input variables across different import classes currently available to see which kinds of arguments I need to include for the full suite of functionality. This will likely require a lot of testing.&#x20;
* Need to make a note:&#x20;
  * Volume Effects:&#x20;
    * Directory&#x20;
    * Colpath&#x20;
    * Colname&#x20;
    * Treepath&#x20;
    * Treename&#x20;
  * Mesh Effects - Displacement&#x20;
    * Directory&#x20;
    * Treepath&#x20;
    * Treename&#x20;
  * Mesh Effects - Structural&#x20;
    * Directory&#x20;
    * Colpath (unused)&#x20;
    * Colname (unused)&#x20;
    * Treepath&#x20;
    * Treename&#x20;
  * Mesh Effects - Parametric&#x20;
    * Directory&#x20;
    * Objpath&#x20;
    * Objname&#x20;
  * Surface Effects&#x20;
    * Directory&#x20;
    * Colpath&#x20;
    * Colname&#x20;
    * Treepath&#x20;
    * Treename&#x20;
  * Surface Effects - Weight Paint&#x20;
    * Directory&#x20;
    * Colpath&#x20;
    * Colname&#x20;
    * Treepath&#x20;
    * Treename&#x20;
  * All different variables&#x20;
    * Directory&#x20;
    * Colpath&#x20;
    * Colname&#x20;
    * Objpath&#x20;
    * Objname&#x20;
    * Treepath&#x20;
    * Treename&#x20;
* It occurs to me after looking at this list that surface effects also support a weight paint mode that I nearly forgot about - it seems there is always a use case exception to a universal function.&#x20;
* From the looks of it, the weight import functions are mostly the same but look to see if a particular geo nodes tree just so happens to have an input with the name 'weight', so we could just do a boolean toggle to look for that.&#x20;
* Now, for our new function, we should look through each of the pre-existing import classes and add their functionality to this, using the passed function arguments, and place a line of code to call the function (maybe leave it commented out before we swap it with the currently active functionality.&#x20;
* It occurs to me that there may be important subtleties between the different importing methods, but I believe all of them can be unified, however it may take a certain kind of cognitive approach. It might be beneficial to do some kind of direct comparison between the lines of code, maybe color or number coding them in some kind of canvas to see how similar they are. It's hard to do in just a code editor, so I might take some time to break it down in affinity designer.&#x20;
* \[ Time: 2 hours passed ]&#x20;
* Each of the import classes have been laid out on an image canvas, now I am reading and comparing.&#x20;
* It occurs to me while comparing that we could (in theory) just throw all of the code classes into this one function and separate them by cases, but that would defeat the point of trying to condense things.&#x20;
* So far discovered:&#x20;
  * Mesh Effects - Displacement is identical to Volume effects (S) case with the exception of differently named variables. These displacement effects could be renamed to use the (S) convention and therefore would be able to use the same code, so that (in theory) can be condensed. They also both use arguments treename and treepath.&#x20;
  * Mesh Effects - Structural is identical to mesh effects displacement, which is also identical to the (S) case of volume effects. Therefore ME-Displacement and ME-Structural can both be condensed into the same kind of case, if their geo nodes trees are renamed, and we take the volume effects cases as a starting point for our new function.&#x20;
  * Mesh Effects - Structural template is different from the other cases as it is just a complete template object import followed by a look at the modifiers for subsurf to enable.&#x20;
  * Interestingly (and maybe confusingly), mesh effects - parametric template importer is different from the structural template importer, in that it also looks for (G) types. However the non-G-type case is the same as the structural template. So it looks like we will need to add a (G) (or T if renamed) case exception to the template case.&#x20;
  * I'm understanding that there is deeper complexity in the mesh effects - parametric import class, a hidden deviation in the (G) type effects where with G, a separate object is kept hidden after being imported to act as the host of the effect, whereas without G, the modifier stack is attached to the originally selected object, so it is itself the host. In both cases, node checks are done to find any required target assignments in modifier inputs. I suppose if none exist with the name of object, then nothing happens. In theory, this else case (which I will nickname the target self method), can also act perfectly as a regular effect import for copying the modifier stack of an object from another file to the current file on the selected object. Now we just need to see how the surface effects fit into this plan.&#x20;
    * So far, I have the following ideas for geometry node effect / application types:&#x20;
      * (S) For simple geometry node single effects.&#x20;
      * (C) For geometry node single effects which also require the importing of a collection asset that will also be assigned in the node tree.&#x20;
      * (Tr) Target remote - for objects with multi-effect modifier stacks which require a separate object to host (the original object will be hidden). Node checks are done to auto-assign 'object' inputs to the now hidden, remote, original object.&#x20;
      * (Ts) Target self - for objects with multi-effect modifier stacks in which the entire modifier stack is kept on the self, and references self. Node checks are done to auto-assign 'object' inputs to the self object.&#x20;
  * On a quick surface glance of the surface effects, I can see the use of (S), which might suggest parity with the earlier volume effects import of (S), but I expect there is more complex functionality. I see a case for creating and assigning an ambient occlusion group, which is clearly not required for the volume effect, but it seems dependent on there being a group input called ( c ) ambient occlusion.&#x20;
    * I'm now thinking that for things like this (input and node activated features), maybe they should be kept as independent of specific cases, as it may be suitable to let people 'summon' features like this simply by leaving the right kind of trail in their input design or specific nodes in the tree. Maybe that's too much to think about for now - the priority is to condense the importing into one function.&#x20;
  * \[ Time: 3 hours passed ]&#x20;
  * Nearly completed planning, just looking at surface effects weight paint case, and noticing this one is geared entirely for single object application given the integration of weight painting the selected object. This is not completely compatible with all of the other code as the other cases support multiple objects. However, one thing learnt from easybpy is we can pretend a list is only a single object, or force it to be, so it might be worth adding an argument called 'single' to our new function, and if True then we make the objs list only contain the active object.&#x20;
  * I'm also noticing a chunk of code specifically for setting up the weight painting which will likely require another specific argument, so adding that to the speculative function argument list now.&#x20;
  * After testing the interface in Blender, I can also see that weight painting is broken, so after moving everything to the new function, we will likely still need to fix that.&#x20;
  * I'm going to include a quick image to show how the different code cases for each type of import method are being compared.&#x20;

<figure><img src="../../.gitbook/assets/map.jpg" alt=""><figcaption></figcaption></figure>

* I think there is enough information now to start drafting out a version of the unified function, even if the code is not complete (portions will likely be pseudocode until it is refined).&#x20;
* I have copied over the original code from the volume effects import class as the starting point for creating the new unified function, just like how I started mapping with the same class above.&#x20;
* Basic code from mesh effects - parametric template has also been copied over to the unified function where appropriate in a template considering case. Changes will still need to be made to the naming conventions. I will try to get all of the basic original code into general place before refining and making it actually work.&#x20;
* Code from mesh effects - parametric has also been added with the speculative Tr and Ts case versions (still referred to as (G) at the moment).&#x20;
* Now all original code has been put into the speculative unified function, it is ready for refinement, a whole lot of checking, and then testing. We also need to completely re-structure the previous presets and template content to follow the new naming conventions. That could be quite a lot of work. We are now coming up to the four hour mark, which is all the patrons have paid for, so now I need to decide whether to carry on in my own time. It might be worth communicating the updates to people so far, but ideally not leaving it too long before continuing.&#x20;
* Thankfully there are backups in the form of gumroad, blender market and github, since we will be making large sweeping changes. I think now might be a good idea to start updating all of the content in the official pack to reflect the new naming conventions. We will also need to update the names of the thumbnails too, I imagine. To focus, I have the following main priorities:&#x20;

- [x] &#x20;Update naming convention for all content.&#x20;
  * [x] Collection names for surface effects with collections.&#x20;
  * [x] &#x20;Geometry node tree names.&#x20;
  * [x] &#x20;Thumbnail names.&#x20;
- [ ] &#x20;Link old classes to new universal function.&#x20;
- [ ] &#x20;Do import / application tests and debug.&#x20;

* \[ Time: 4 hours passed ]&#x20;
* Added a note in the helper text document in the official content pack that the text will need to be updated to reflect version 10 changes.&#x20;
* Changed the collection names of the original surface effects.&#x20;
* Added a File Data workspace in the official content pack to make it easier to access the different data types, mostly for renaming.&#x20;
* Surface effect geometry node trees have also been renamed, now going to look at the thumbnail files for the surface effects specifically.&#x20;
* Thumbnail file names have also been changed and when refreshing the content in the by-gen surface effects panel, I can see those name changes reflected. Before I do any code based testing, I need to also update the conventions for the other content stored in the official file.&#x20;
* Now looking at Mesh Effects – Parametric presets and using the map created earlier to realize that they are (Ts) based effects, meaning target self – to copy modifier stacks from the original source objects to the target of the current file.&#x20;
* The names of the objects have been updated for the parametric effects from the official content pack, now going to do the thumbnail files.&#x20;
* The thumbnail names have been updated and are now reflected in the BY-GEN interface. I do not believe any geometry node trees are required to have any name changes for this kind of effect as it is copied over as an object whole.&#x20;
* Now for mesh effects – structural. According to the map, these should be (S) types, however they can also be imported as a template.&#x20;
* Deciding to try and give the geometry node tree, the object name and the thumbnail file names the (S) prefix and hope that's fine.&#x20;
* Now for the volume effects, these can either be (S) or (C) types according to the map, but each of the originals are (C) type as they use collection content. Actually, looking again, two of them already have the (S) prefix, so there was a mix of types. So we just need to rename the others.&#x20;
* Looks like the volume effects are now done as well. It's now 1am and I should stop soon. The next step is to replace the code in the old import classes with a reference to the new function. Maybe it would be a good idea to not delete the old code immediately, just disable and hide it in a collapsible region.&#x20;
* \[ Ending work for day, 18/07/25, 4 hours and 26 minutes ]&#x20;



</details>

<details>

<summary>19 July 2025</summary>

Deciding to do some 'unpaid overtime' on BY-GEN to keep up with this function update subproject.

\- Firstly, going to do a quick read-through of the function just to see if things make sense in the new order. Also noting that variable names need to be changed as they are currently a mix from all different source locations. Note, I have also recorded a video explaining the work done yesterday with the patreon wage to keep people in the loop.

* So, I can see that wm.volume\_effects is something used and set up prior to importing, but that's something that we expect to be passed into the new function arguments. One of the arguments we've already prepared is 'name', which I think we expected wm.# references to be passed to, so that's what we'll do. Any wm.effect references will be replaced with 'name'.
* Check that we're updating references in the following sections:

Preparation Section

Template

(S)

(C)

(Tr)

(Ts)

* Wondering about where the content pack directory is provided, and realizing that it will be passed as a part of the function arguments.
* I'm noticing there are lots of extra properties to consider, things like bytool.ve\_unique\_collection, these may or may not need to be passed as arguments as well. It's going to take a while to cover all of these bases.
* In the (S) section, I see naming conventions like volume\_tree, I think these should be changed to something more general like 'imported\_tree'. Checking (S), (C), (Tr), (Ts). Those are done.
* Now want to check for references to bytool properties and see what can be done about them. I'm noticing that the 'make collection unique' checkbox is present in both the surface effects and volume effects sections of the interface, but I can only find it present in the volume effects section of our code, meaning we might be missing it for the surface effects.
* I see, when creating the map, we assumed the volume effect one would be renamed to encompass functionality for both the volume effects and surface effects, so bytool.ve\_unique\_collection will become a new general check that is used by both. With that in mind, we could add a boolen argument unique\_collection to the function and use that.\
  Just added that now.
* Now I'm just going to do a quick check for indentation and conditions. I'm clearly taking a long time to check this code and re-read it even though I know it's going to immediately throw up errors. I just want to be methodical about it. I should also note to changeover the previous importing classes so they call this new function with the correct arguments. Just going to make a note of those now. I said before, but I'm also going to not delete the original import code, just comment it out in case I need to swap it back.
* Surface effects (Done) - included bytool.se\_unique\_collection
* Surface effect weight paint (Done) - included bytool.se\_unique\_collection
* Mesh effects parametric (Done)
* Mesh effects parametric template (Done)
* Mesh effects structural (Done)
* Mesh effects structural template (Done)
* Mesh effects displacement (Done)
* Volume effects (Done) - included bytool.ve\_unique\_collection
* I'm remember while looking at these classes that this new function will need to be moved higher up the file so it can be interpreted before being called. I'm going to move that now.
* It has now been moved above the surface effects region.

\[ Time: 1 extra hour has passed from today's session. ]

* Now all of the original classes are making calls to the new function, and I'm aware that it will not work at this state. The integration is very clean in regards to writing out the function argument, and I need to be prepared to write effective debugging checks to understand what's happening.
* I'm wondering if it might be time to tackle the first set of errors. I have reloaded the addon and it completed the reload successfully.
* I have temporarily removed the generator's lab content pack from the by-gen workspace and moved it to a temp folder just to keep things simple during this phase of testing.
* Immediately, 1014 missing argument name, classic. Looks like I forgot to include the name argument, so we'll need to go back through and grab that.
* \[ 1 hour 26 minutes ]



</details>

<details>

<summary>20 July 2025</summary>

* Going to continue with testing today, and the first point of action is to include the name property in all of the new function calls. I can see that name is also redundant in a lot of cases, for example the colname and treename arguments are identical in several cases, but I'm less concerned with optimizing redundant references at the moment, and more so want to try and get it working first.

- Surface effects (Done)
- Surface effect weight paint (Done)
- Mesh effects parametric (Done)
- Mesh effects parametric template (Done)
- Mesh effects structural (Done)
- Mesh effects structural template (Done)
- Mesh effects displacement (Done)

* The name argument has been added to all of the new references, now time to re-test. The effect I'm trying to import is the (Ts) Destructor effect. An error has ocurred:

- 1016 – import\_content -> 81, scene = context.scene. Context is not defined. Looks like another rookie error, let's see why context is not defined here. Think I just missed a few essential lines at the start of the function.
- I see and remember that context is usually passed to each of the classes automatically, maybe we can try passing it as an argument as well. That will require updating all function call references again. For now maybe let's do it just for 1016 where we are testing.

* Wow, I added it and something actually happened – an effect was imported onto the object. Wasn't expecting any degree of success that quickly. With that in mind, let's add the context argument to the other functions before we forget.
* I have several ideas for how to fundamentally redesign the official content pack effects to be more useful for a wide degree of workflows going forward as well, but don't want to jump too far ahead yet.
* Surface effects (Done)
* Surface effect weight paint (Done)
* Mesh effects parametric (Done)
* Mesh effects parametric template (Done)
* Mesh effects structural (Done)
* Mesh effects structural template (Done)
* Mesh effects displacement (Done)

- Now that the context arguments have been added to all of the new function calls, we'll get back to testing and bring up some new errors. We'll descend into deeper testing when it gets harder to find errors, such is the way of things.
- Interestingly, that destructor effect looks different now, but I can't think of any reason why that would have changed from what we've done. I can see that a displacement texture has also been generated as a part of the import process (unless it was already on the effect), because I don't think we generate displacement images anymore like the older version of the addon.
- I applied the (Ts) Hard Surface Faceting effect which seems to work fine.
- (Ts) Hard Padding also works, we are still in the mesh effects – parametric section. Maybe we can move to being more methodical. It would also be nice to knock out the weight painting issue as well, but we can do that when we move over to the surface effects area.

* Destructor (Done) works but the first subdiv ruins the effect. Maybe that should be reduced. Suppose it doesn’t matter much if we completely redesign the official effects. This makes us think we should be a bit more structured and standardized about the kind of meshes we expect people to use. A subsurf could be added at the end of the destructor as well, if we keep and redesign it.
* Face Ripper (Done) This could be recycled as it may be appropriate for a geometry nodes focused mesh surface disruption effect. Seems quite good for generalising.
* Point Cloud (Done)
* Hard Padding (Done)
* Hard Surface Faceting (Done)
* Hard Surface Frame (Done) (Planar)
* Hard Surface Skin (Done) (Edge) (people don't know what type of base mesh an effect is suitable for, maybe we can think about some kind of thumbnail notation in case an effect is suitable for some kind of manifold mesh, or something like a simple plane, or edge shell.)
* Metal Shell (Done)
* Organic Shell (Done)
* Pixelate (Done), but values are off, start frame should be about 300 ish.

- That's all of the parametric effects, they seem to import properly despite design inadequacies, which are things we can easily address without code.
- Tested applying the barnacle surface effect (without weight painting) and it imported fine, even assigning the collection imported, again surprised it worked without error. I am interested in removing 'style' from future effects.
- \[ Time: 1 hour passed ]

* Thinking about when doing future effects, we want to look for different distributions of point, but also different 'angles' and behaviors with their normal directions. Maybe those could be put into node groups. So we need to think about layers of control. Maybe the user selects a distribution 'method' and inside of those node trees are shared node groups controlling other things like angles. Or maybe we go to a higher abstraction where we have more complex effects, but dsitribution and rotation are controlled by node groups. Will need to think about it. Maybe along that vein, any node groups we create for the official content pack – that blend file can also double up as an asset library – so users could in theory add the content pack file as an asset library (maybe we can have a button to do this via code), although there might be some differences between operating systems).
* Elevating some of these notes for future consideration.
* Now let's see if we can fix the weight painting. Also just backed up our work folder to local production SSD because it would have been a pain to lose all this now. Maybe we can backup to the private repo soon as well, when we are confident things still properly work on the new function, and then we can also do cleanups for the redundant code.

- 629 import\_content -> 254 bpy.ops.object.geometry\_nodes\_input\_attribute\_toggle(prop\_path=id\_prop\_path, modifier\_name=geomod.name)\
  in ops, 109, op\_call(self.idname\_py(), kw)\
  Converting py args to operator properties:: keyword "prop\_path" unrecognized.
- Looks like we'll have to put a few debug notices in to see what's happening with prop\_path.
- I'm looking at the line and reading prop\_path=id\_prop\_path.
- Id\_prop\_path is previously defined as "\[\\""+id+"\_use\_attribute\\"]"

* I believe this is some kind of boolean for the geometry node inputs, naturally a lot has changed with the geometry nodes interface since then. Probably for the best, as it seemed poorly designed to start with.
* I'm going to do a bit of scouting around with the interactive Python console in Blender to see what the inputs for geometry nodes trees look like now.
* Okay, it looks like the prop\_path argument in the bpy.ops that toggles attributes has changed to input\_name. So let's swap that over first and see if we happen to have the correct input name still plugged in.
* When testing now, it seems to apply the effect but does not toggle the attribute, so the parameter might be wrong, but when I manually press the button, the effect does change to weight paint and my previous painting attempt shows results, so we see the vertex link is applied.
* I added a debug print and saw that input\_name was being passed Input\_3\_use\_attribute, then it only needs Input\_3.
* I changed it to only pass the id (Input\_3 in this case), and tested again, and now it seems to work. So that might have fixed the issue. Just need to do more testing. And remember, it is based on vertex weights, meaning it won't paint everywhere.
* With more testing, it seems to have been fixed, but going to make a note that when painting, the points for distribution seem to be regenerated for each new position, which looks a bit strange and isn't conducive to fine artistic control.
* Moving on, I'm thinking it might be good to share this version of BY-GEN with people before we do wide reaching changes to the content packs, but also note that we need to update the generator's lab content as well to make it compatible. People may want to still use these effects with 4.5+ so it would be good to give them a functional version before things change even further.
* We still have other categories of effects to test though, so should get on with that first.

\[ Time: 1 hour 35 ]

\+ 2 hours for updating easybpy and holt tools, did not log details. Notably, updating eaysbpt for holt tools fixed unpacking and organization, and node group input setting default updated.

\[ Time: 3 hour 35 minutes ]

* Had a quick check of multiple selected objects before trying weight paint mode, and it only applied to one even though I don't think we've implemented single application properly yet.
* If this is stable, we can move on to cleaning the code, a bit more testing, and then modifying the generator's lab with the updated conventiont to make it compatible.
* Renamed Guilded to (Ts) Guilded, but when applying there is an error appearing with selection. Weirdly after restarting Blender with VS Code and trying again, it works now.
* Weird, if it comes back we will re-investigate. Until then, let's update the conventions for the rest of the generator's lab content. The (G) content will be renamed as (Tr).
* Noticing that the import template isn't working properly as it's not bringing in the right object.
* Looking at the template section of our new function, I can see we still left a (G) condition in there, so it's time to replace it.

- That seems to have fixed the template importing.

* Bumped into an error when trying to weight paint a simple mode (S) instead of collection mode (C), realized we only fixed one of the weight painting cases and not the other.
* I think the generator's lab content is pretty much up to date with the conventions now.\
  Now before we move onto packaging this version of BY-GEN, we should do some large scale cleanups of the code.
* Trying to import the template of a official structural effect and getting an error, looks like we've got more to test and fix. But when applying the effect to selected, it does bring the content in.
* Discovered that template was set to False in the new function argument under the structural section.
* \[ Time total for today: 4 hours 33 minutes ]

</details>

<details>

<summary>21 July 2025</summary>

* Node group getter/setter in holt tools now also works for world nodes and geometry nodes.

- Fixed 'backup generation' result in BY-GEN'
- \[Time + 32 mins]
- At the moment, just hunting for extra bugs in this current version of by-gen and making notes for functionality to remove once we do the jump to version 10, after making this stable. Currently bumping into a bug relating to the generation of ambient occlusion maps.
- I can see that the way vertex color groups has been managed has changed, they are now considered color attributes. They are added with bpy.ops.geometry.color\_attribute\_add(name="Color"). That will replace bpy.ops.mesh.vertex\_color\_add(), but we need to look at the process for accessing that data afterwards.
- Also editing public notice video on the side letting people know about the new updates to free tools (and modular workspaces). Now exporting and encoding that before preparing the admin and uploading prior to release.
- I'm getting some success finding the color attributes by using o.data.attributes\[0], which returns a reference to the Color attribute created.
- Pre-uploading the public notice video.
- Video now prepared for release, likely tomorrow, now continuing with trying to fix the lingering 9.2.1 BY-GEN bugs prior to making available online, but also need to remember to upload the new version of the generator's lab content pack at the same time with the right version notice.
- First set of errors for the ambient occlusion vertex color generation operation have been resolved, next set now.
- Actually, going to make an executive decision to remove this operation from the interface, because it was originally only needed for an experimental grunge geo nodes pack that isn't present, and we don't need it for version 10. Rather than get frustrated on the fixing process, just going to remove it from access. It's contained under helper tools under the surface effects panel.

* This has now been removed from the interface, now moving on.

- Now going to do some cleanup before defining this as BY-GEN 9.2.1.
- Preparing zip files for BY-GEN 9.2.1 and The Generator's Lab for BY-GEN 9.2.1, considering them as 'release candidates'.
- Tried manual install and now the generator's lab content isn't being brought in, okay I think it's because we had period characters in the name of the folder.

* Fixed this, and now I think they are ready for uploading.

- \[Time + 1 hour 17 minutes ]
- Files for both BY-GEN and The Generator's Lab have been uploaded to Gumroad and Superhive, now need to replace the code on the public BY-GEN repository.
- Restructuring the official website web page for BY-GEN to simplify it and add a notice for a large refactoring for version 10.
- Just pushed BY-GEN v9.2.1 to both the private development and public repo.
- Going to do a local backup of both projects onto the production SSD, and then we should be in the clear to start doing the large V10 refactor that we seem to be quite excited about.

* That backup is now done.

- Making some notes on the kind of base effects we want after the refactor.
- I'm looking at the mesh effects section and wondering if we really need them split into parametric and structural sections for 10+.
- Created a folder in the official content pack thumbnails\_mesh\_effects, to see if we can start making the separate modes redundant.

* Hiding registration for the parametric and structural panels.
* Also deleting the ambient occlusion pre-operation code.

- Doing many destructive changes, removing classes, will discover errors as they arise, trying to knock mesh effects back into only one section.
- We are bumping into many points of failure as due to destructive changes in case, there are many places where references need to be made when setting up a content management system like this, it will take time to work through them all.
- We're at a point now where the mesh effects panel does look quite independent, however nothing is showing in the field, but that's understandable since we haven't put anything in the associated thumbnails folder. Maybe I will copy something over from one of the other official content folders just to see if it brings in the content.

* Testing, and I can see that it does. The next step is putting in a button to actually apply the effect to selected.
* Now we have the button appearing as the solo 'mesh' effect import class is registered, but when trying to apply the effect, there is an error. I know this effect is not specifically for this category, but I believe the import process should still work.
* The error says that we cannot use current file as a library but I'm not sure where it thinks we're passing the current file anywhere.
* I think it's because nothing is being passed in objname.
* Now when passing colpath and colname in the obj arguments, trying to apply gives an object selection out of range error.
* Okay there might have been something subtle about the arguments we provided, because after looking back at the old parametric import class and copying the argument layout from that to the new mesh effect function call, it now seems to work.

- We can continue simplifying the interface and removing unnecessary code now.
- \[Time + 1 hour 55 minutes ]
- I'm now going to look at trying to remove unnecessary classes. I also notice that we have a tickbox for 'make collection unique' under the mesh selector now, so I just want to quickly check that we have a unique property for that, so it doesn't accidentally use the property from the volume effects.

* Yep, just checked and it looks like we also created a unique property in BGProperties so the mesh effects have their own selection for making the imported collections unique.

- \[Time + 14 minutes ]

</details>

<details>

<summary>23 July 2025</summary>

* Worked on other projects (Modular Workspaces and Holt Tools) over the last few days but didn't log time as mixed free and paid, now getting back to BY-GEN V10 refactor.
* Firstly, I want to simplify the interface, so I'm going to hide the helper tool sections and maybe trim off the extra buttons next to the content pack drop downs that aren't required.
* While working on that, I will also hide the structured generation and scattering panels - I'd rather focus on a small set of high quality features.
* Changed metadata version to 10, Blender version to 4.5.
* I'm noticing that there are a lot of bloat classes and old files that we can probably remove to simplify. Maybe see how much we can condense into fewer files as well. A good opportunity to make everything nicer to keep track of and work with.
* Disconnected and removed menus.py, which was responsible for shift + a menus that we won't need anymore.
* Managed to remove and hide structured generation and scattering and deleted associated generation files attached to those.
* Also removed the tools panel, but that one could come back in the future if needed. Added comment notes next to the classes we have commented out from registration noting that they were removed for V10.
* Saw that we had a panel in the properties editor, so removed registration for those classes as well, will try to delete the code now.
* Simplifying the info panel to have just one button link to my website.

- Changed the icon for the link button to a python icon.

* Changed the icon for the volume effects panel to be the newer outliner volume icon (at least I think it's newer).
* Changed the icon for the mesh effects panel to be the newer outliner mesh icon.
* Changed the icon for the surface effects panel to be the outliner surface icon.
* Simplified the panels even further by removing 'effects' from the titles of each panel as it seemed redundant and repetitive.
* Changed every 'apply to selected' button text to just 'apply'.
* Created a new settings panel to hold all general settings, underneath the other panels, want to move the 'make collection unique' checkbox to it and make it singular so it applies to all imported effects.
  * Will need to define new property for the general version. (Done)

- Then will need to look for references to all individual versions and replace with the new general version. The previous versions we can search for are:

* Se\_unique\_collection (References Done, Property Deleted)
* Me\_unique\_collection (References Done, Property Deleted)
* Mp\_unique\_collection (References Done, Property Deleted)
* Ms\_unique\_collection (References Done, Property Deleted)
* Ve\_unique\_collection (References Done, Property Deleted)

- There is a lot of cleanup still to do in the properties - lots of them that are no longer relevant.
- Now all of the collection unique interface references and calls have been replaced with the general version, now need to put together the settings panel and move the single checkbox there to keep things simple.

* That is now done, so now we can remove the checkboxes from the original panel elements.

- This is now done, things are looking neater, and I'm noticing a lot of excess classes in the code we can probably remove now.

* Removed all references and classes for the mesh effects subtypes - parametric, structural, displacement, to keep with the concept of a simplified BY-GEN V10.
* Deleted all classes in the mesh helper tools section and removed registration references.
* Getting some errors now but that was bound to happen when modifying properties relating to all this asset refreshing.

- I think I've gotten it working now. When registering the addon for the first time, if the properties weren't completely in order, then it would not successfully register all of the rest leading to lingering issues when continuing to use features of the addon in the same open instance of Blender.

* What this means is we have now simplified effects.py down into just surface, mesh and volume classes, along with settings and the new function we created for handling all types of imports. We must be pretty much ready to start working on the content side of things, but there are still the lingering buttons next to the content pack drop downs for each panel.
* \[ Time + 1 hour 10 minutes ]
* Maybe we should also add a button to the content packs directory in the settings panel.

- That has now been added, so we can remove it from the other panels.

* \[ Time + 13 minutes ]

</details>

<details>

<summary>24 July 2025</summary>

* Going to carry on with the cleanup of the smaller panel buttons.

- Specifically removing the smaller button to open the local content packs, as well as the website link button, but leaving the refresh one (even though it's better for Blender to be restarted after installing content packs for the addon.

* Those extra buttons have been commented out now, and I quite like how the panels look, so it might be time to start working on the graphics and abstraction node group planning for the differential effect categories in each pillar.
* Working on a conceptual thumbnail for volume effects - distribution.
* Conceptual thumbnail for mesh effects - deformation has also been created, but it's just a placeholder.
* While working on conceptual thumbnails, refamiliarizing with geometry nodes, manipulating points in relation to geometry, etc.
* It's taking a while to figure out to geometry nodes effects. Of course, when it comes to making the content for real, I will be consulting with geo nodes experts.
* \[ Time + 1 hour 21 minutes ]

</details>

<details>

<summary>29 July 25</summary>

* Continuing work on distribution for surface effects.
* Overwriting official content pack file with the thumbnail test file, making good headway with setting up surface distribution category, but the variables / attributes are confusing.
* Consulting with Charan on making variables for distribution simpler.
* Too many things to note, Charan is runnig through many possibilities with us.
* Noise distributions, proximities, etc.
* Charan passed work back, I can compress it in terms of user design.
* \[ Time +1 hour 56 minutes ]

</details>

<details>

<summary>30 July 25</summary>

* Posting a visual experiment from last night's work to socials, a good confidence boost for being able to demonstrate fun interactive visuals for people when the logic library for the addon has expanded.

- [https://x.com/curtisjamesholt/status/1950506006154301797](https://x.com/curtisjamesholt/status/1950506006154301797)
- Inspired by this new artwork, I'm thinking of taking that lighting / material setup and using it for the thumbnail defaults. Keep changing my mind about that, but I want it to feel right for people.
- Now I need to focus on simplifying the parameters, giving them names to make them more understandable for users, separating the logic sections into more modular units, etc.
- Separated the node areas for the distribution logic so far into easy to identify frames, ready for potential node grouping.
- Charan has also shown me more changed relating to capturing effects within the inside of a mesh hull. I'm continuing to simplify the logic into node groups on my end, so asking him if we can merge.
- Discussing extra changes with Charan who has been contributing more work, discussing differential normal inputs.
- \[ Time + 1 hour 28 minutes ]

</details>

