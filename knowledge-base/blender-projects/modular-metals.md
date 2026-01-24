---
description: ( This is an old wiki page migrated from the official website. )
icon: medal
---

# Modular Metals

#### Introduction

Modular Metals is a collection of 100% procedural node groups and presets for building metal materials in Blender. This collection has been designed for the Cycles rendering engine, however some components may work in EEVEE with some adjustment.

Please start off by watching the [introductory video](https://www.youtube.com/watch?v=nuaui_H-J8s).

#### Modularity

The modular part of the name comes from the fact that the procedural materials are built of smaller, independently-useful **node groups**. Layer by layer these groups are combined in progressively more complex ways to produce more interesting and visually-distinct styles, inspired by various metallic surfaces in real life. Naturally, this also means that the more complex the material, the longer the computation time will take when rendering, so of course you will need to make your own judgement for how much rendering time you want to sacrifice for visual results. I think it makes sense to call these smaller modular groups ‘**Builder Nodes**’. Take a look at a few below.\
(Of course keep in mind that as updates are made, the parameters of node groups will likely change).

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

#### A Simple Example

On the original landing page, I provided this example of creating a nice simple metallic effect by combining the Faded Metal and Subtle Imperfections builder nodes.

The main outputs that have been focused on with the product are ‘**Color**’, ‘**Roughness**’ and ‘**Normal**’. Roughness gets the most love because when dealing with metallic materials, this is the value that produces the most distinct visual variety and is essential for **surface imperfections**. In a lot of cases, the color can be swapped out for alternate values to make it look like a different metal. To help with this, I have included a node group with common colors for different metal types.

When creating the package, I found that using the **Glossy BSDF** shader produced more accurate results than the **Principled BSDF** shader, so most default parameters were calibrated for specifically that.

Passing the object output from the **Texture Coordinate** node will generally provide the best results for wrapping a procedure result around an object but keep in mind that every scene and object is different and the coordinate data you use will change depending on that.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

#### Texture Baking

When dealing with complex procedural materials, the important question comes to mind: can we have these amazing looking results for only a fraction of the computation time? The answer is of course yes but you will lose control over properties and sacrifice ‘infinite’ detail for pixel rasterization. You can bake the results down into basic texture maps and use these as traditional materials. Alternatively they can be exported to other rendering software or game engines. I created a quick video showing how to do this, but since making this video more developments have been made in the Blender baking space.

{% embed url="https://www.youtube.com/watch?v=DAAGKr6wCRA" %}

#### Bystedt's Baking Tool

Check out the baking tool by Daniel Bystedt. I haven’t had a chance to personally test this with the package yet but I assume it would be a viable replacement for the original method which had some weird quirks in regards to making sure the right nodes were actively selected (otherwise the results would come out black).

{% embed url="https://www.youtube.com/watch?v=T4GVVQjPi1Q" %}

#### Copper and Iron - The Two Kings

Two main branches of study that were focused on when making the package were **copper** and **iron**, both of which have an interesting ageing process which would commonly be called **oxidation**, but though that term is appropriate for iron, the process of developing **copper carbonate** producing the cyan/green **verdigris** effect is a bit more complex.

There are several node groups included increasing in complexity which eventually lead up to a simulated ageing effect which can be adjusted with a simple ‘age’ slider. From least to most complex, these node groups are as follows:

**Copper**

* Corroded Copper
* Smart Corroded Copper
* Master Copper
* Complex Copper

**Iron**

* Rust
* Smart Rust
* Master Iron
* Complex Iron

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

#### The Mega Shader

If you know much about my creative attitude, you’ll know that I love having artistic control and breaking the rules of realism. So once I was happy with these two branches, I tried to combine everything in a final **Mega Shader**, which would combine the most complex groups to produce the most interesting visual variety. At such a high level of complexity, I cannot recommend using this for any animation work unless you bake things down or have a super beefy machine, however for those that are mad enough to use it, this shader is probably (maybe even secretly) one of the most versatile things I have ever made. Below I will show you the basic structure of the Mega Shader as well as two of my favourite presets (Regal and Stone).

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

I started with trying to make metal and ended up with a well-rounded hard surface material. ‘**Hard surface**’ in this case not specifically meaning metal sci-fi looking things, as the community has come to know it, but hard surface literally in terms of surfaces that are hard by physical property - **metal**, **stone** and **ceramic**. By using the **Mega Shader** as a base for a range of patterns I’m fairly confident that it could be adapted to achieve most types of hard surface visuals, but of course the main downside is that it’s very wasteful and ridiculously **inefficient**, which seems to be a common theme in my work. If anything though, the mega shader serves as a good learning project and demonstrated to me the power of **abstraction** in creative design. I would probably get a slap from other members of the **BlenderNest** crew because ‘layers of abstraction’ is a term I use far too often when discussing projects, but it’s a core principle that translates so perfectly from programmatical logic into artistic design. I don’t know if there are any other philosophical or logical principles that marry the technical and creative spaces as well as abstraction.

#### The Takeaway

So if there’s anything to take away from this project, it’s a functional result of an exploration in modular design and abstraction, in an attempt to see if realistic results can be achieved (in particular with simulating the age of metals), while maintaining the desire to keep artistic control so that in the future those results can be adapted to various other artistic projects.

#### The Lessons for Future Modular Projects

One of the main learning points about this project was the question of how granular node groups should be in their design when building up effects for the larger presets. Should we have as many nodes as possible to provide the most creative control (negating any kind of repetition inside of separate node groups), or should we instead allow some repetition to reduce the overall number of constituent node groups to achieve the same results? That’s a bit of a horrible sentence, put simply, more node groups that to smaller things, or fewer node groups that do larger things but will inevitably have some overlap with other groups (repetition). The answer is usually the same with all projects: it should be a balance of both things. I don’t think I struck the right balance with version one of Modular Metals because the node groups feel a bit too tangled for my liking and I believe Blender struggled with the computation order in a few places by just not outputting the results of certain nested node groups. Strictly speaking, I don’t think Blender is capable of supporting this kind of design in larger scales (at least not yet), so a less granular approach is preferred. Regardless, the project was fun and provided more territory for development and expansion into the future. Feel free to pick it up if you are interested in using it for your own cool projects or just want to see how I pieces it together.
