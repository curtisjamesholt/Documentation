---
icon: circle-info
---

# BY-GEN Layout for Distribution

This page is a note to anyone developing the BY-GEN addon. Prior to distribution, make sure to remove:

* .pyc files (and folders).
* VSCode files and/or folders.
* Git related files and/or folders.

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Though the naming conventions have changed over time, it is usual to simply name the containing folder:

```
BY-GEN {VERSION}
```

It is good practice (though not always followed) to not include periods ('.') in the names of addon zip files, as this has been reported to cause some issues (although in 99% of cases it seems to be fine).

Remember that the structure of the addon should look like this:

```
BY-GEN {VERSION} (as a zip file)
    BY-GEN {VERSION} (as a folder within the zip file)
        content_packs (folder)
            Official (folder)
                    thumbnails_mesh_effects (folder)
                    thumbnails_surface_effects (folder)
                    thumbnails_volume_effects (folder)
                    Official.blend
        __init__.py
        effects.py
        easybpy.py
        changelog.txt
        license.txt
```

{% hint style="info" %}
There may be additional thumbnail folders in future versions of BY-GEN representing new categories of logic.
{% endhint %}
