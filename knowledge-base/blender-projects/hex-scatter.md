---
description: This page contains information about the Hex Scatter tool for Blender.
icon: hexagon
---

# Hex Scatter

### What is it?

**Hex Scatter** is a collection of node groups designed to help you scatter texture content around objects, using a variety of techniques such as **hexagonal cell distribution**, **height blending**, **triplanar / biplanar mapping**, **random rotation /scale**, and **normal correction**.

_Note: Made for 4.2. If using older versions, you may need to manually set the displacement to 'Displacement and Bump' in the material settings._

<a href="https://curtisjamesholt.gumroad.com/l/hexscatter" class="button primary" data-icon="dollar-sign">Get it on Gumroad</a>

<a href="https://superhivemarket.com/products/hex-scatter" class="button primary" data-icon="dollar-sign">Get it on Superhive</a>

### **Learning Material**

<details>

<summary>Announcement</summary>

[Our New Blender Nodes are Finally Here](https://youtu.be/Sfj-jiJvl_I)

</details>

<details>

<summary>Community Helper Addon</summary>

[There's a New Blender Addon?](https://youtu.be/FQkjQH6VOFw)

</details>

<details>

<summary>Experiments</summary>

[Hex Scatter for Blender - Putting it to the Test](https://youtu.be/t4fcDJ7iKx8)

</details>

### **Height Blending**

A collection of blending options are available across two main categories: **Image** (where a single texture is scattered) and **Material** (where multiple texture maps are scattered at the same time to compose a more complex material, such as for a PBR workflow).

The most powerful technique involved in this process is '**height blending**', which requires the inclusion of a greyscale height map to guide the process. Below, you can see a comparison between **traditional dithering**, and the more advanced **height blending** method, which provides a far more convincing result when displacement is applied via adaptive subdivision.

<figure><img src="../../.gitbook/assets/Dither vs Height Blending.gif" alt=""><figcaption></figcaption></figure>

A comparison between the regular dithering blending method, and the more advanced height blending, showing how the neighbor regions are much more convincing on the height version when displacement is used. (Material not included.)

### **Normal Correction**

A common oversight for multi-map texture scattering is **normal correction**. When applying random rotations to normal maps, the data needs to be adjusted to compensate for the change in direction. **Our hex scatter nodes do this automatically.** Below, you can see a comparison of a material without normal correction, and then again with normal correction applied.

<figure><img src="../../.gitbook/assets/Normal Correction.gif" alt=""><figcaption></figcaption></figure>

A comparison between randomly rotated cells without normal correction, then with normal correction applied. (Material not included.)

### **No Need for UV Mapping or Seamless Textures**

Textures used by the node group **do not need to be seamless**, thanks to creative blending modes that recycle pixels from neighboring cells, combined with optional randomized rotation and scale values, giving the illusion of an **infinite, seamless material**.

**UV mapping is not required** either, as texture content is wrapped around any object through the use of **triplanar** or **biplanar** mapping. Consideration has also been made to prevent these projections from creating mirrored areas of detail when rotations are randomized - another common oversight.

**Important notes:**

* Not all texture content is appropriate for this kind of scattering. Surfaces that are structurally precise and predictable, such as bricks or tiles, may be less appropriate for hex scattering, triplanar / biplanar projection or height blending.\
  **Materials which are structurally ambiguous, and semi-random by nature, such as clay, rock surfaces, skin, fabrics, ceramics, etc. will be very appropriate for hex scattering.**
* The **Hex Scatter nodes do not create texture maps**, such as normal, height, roughness, etc. To make use of the full Material/PBR workflow, you will need to create your own maps.

As a starter example, a single set of four texture maps is included in the blend file by default, representing a hand-made clay material.

<figure><img src="../../.gitbook/assets/included textures.jpg" alt=""><figcaption></figcaption></figure>

### **Triplanar vs Biplanar Projection**

Biplanar projection typically required fewer image samples than triplanar projection to achieve almost identical results. Both options are available for you in this package. In the following example, you can see a comparison between the two methods, where the only visible different is a small amount of 'pinching' in the biplanar example on the right.

<figure><img src="../../.gitbook/assets/Triplanar vs Biplanar.gif" alt=""><figcaption></figcaption></figure>

### **Convenience Python Scripts**

As these nodes are slightly more complicated to set up than regular materials, **a couple of convenience Python scripts have been included in the main file to help you create new materials**, along with an embedded readme file to explain the process.

<figure><img src="../../.gitbook/assets/python scripts.jpg" alt=""><figcaption></figcaption></figure>

### **Why It Exists**

These node groups were created when [Curtis](https://www.youtube.com/@CurtisHolt) commissioned Kris to create a more powerful random scattering node to help with his sampling projects, which often involve taking image sources from real life and turning them into convincing digital materials. These tools were created to be used in future products by Curtis, but due to popular demand, they have been made available here as a standalone package, so people can use them to create new materials for their own use (please see the license section below regarding commercial usage).

### **Studio-Friendly License**

This product is governed by a custom ‘**Studio-Friendly License**’, which is a **non-aggressive, royalty free, unlimited seat license**, giving extended rights under different pricing tiers to independents and studios. Read more about the license here: [https://curtisholt.online/studio-friendly-license](https://curtisholt.online/studio-friendly-license).

**For a quick breakdown:**

* An **Independent** purchase gives independent customers full reign to use the content for an unlimited number of projects, both commercial (including freelance) and non-commercial.
* A **Studio** purchase allows a studio to use the content **for one project** with **no seat limit** (for example, one purchase per client project).
* A **Studio (Unlimited)** purchase gives a studio the right to use the content for an **unlimited number of projects** with **no seat limit**.

As a reminder for all tiers: **Commercial usage does not include the right to resell or relicense the product.** **You are not allowed to redistribute the content in other packages**, except for specific circumstances, such as compiled entertainment products (see the license page for more details).
