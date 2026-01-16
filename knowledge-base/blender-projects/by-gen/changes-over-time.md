---
icon: circle-info
---

# Changes Over Time

### Why So Many Changes?

The BY-GEN addon has undergone many changes over time to keep up with Blender developments. When the addon was first created, huge features like geometry nodes did not exist. Over time, as Blender has changed, the possibilities of the addon have shifted. Various parts of the Blender API are more likely to cause addon-breaking changes that others. As a result of this, experimental features have both been added and removed from BY-GEN across different versions. The change in features may seem arbitrary from user perspectives, but it is largely due to several directions being available for future development, collapsing down into a more certain direction as future updates arrive.

This is why some updates seem to remove more features than they add, with BY-GEN V10 being a good example of this. Many features were removed, and the remaining code was stabilized as the decision was taken to let geometry nodes do the 'heavy-lifting' when it came to importing content into the scene and providing procedural / parametric / generative mesh effects.

### Settling on the Content Pack System

After version 9, a content pack system was added to BY-GEN which was later refined in version 10, building around a philosophy that regular asset libraries and BY-GEN content packs could be one in the same. See [turning-asset-libraries-into-content-packs.md](turning-asset-libraries-into-content-packs.md "mention"). In an earlier stage of the content pack system, an expansion called 'The Generator's Lab' was created to test the possibility of paid packs. During the V10 refinement, several categories of content were removed from BY-GEN (namely structural parametric effects), meaning that some of the content from the expansion pack was no longer accessible. At the time of writing, a decision still needs to be made on whether to adapt the content for BY-GEN post-V10, or whether to convert it into a traditional asset library.

### Compensation for Free Development

I tend to develop tools firstly for myself (to make the tools I wish existed for my own projects and workflows) and then secondly for others. Often times, free projects start as fun experiments - 'axial projects' from which I can learn new skills, which are then made available to others. As people grow fond of free projects (EasyBPY would be another example), these tools are integrated into their workflows which leads to pipeline reliance. People have the image that because a tool has a seemingly professional presentation and level of finish, then it must be a financially supported project.

However, there was no true funding for free projects. Donations did occur, but they are not 'budget-able'. Sustained development cannot reliably occur on sporadic donations.

As a solution to this issue, I redesigned my Patreon as a solution to the demand for free project updates. The income decides the number of hours per month that I will work on free projects for the community, set to an agreed 'wage' (50 GBP per hour at the time of writing this). Therefore, Patreon became the development fund. A secondary reason for doing this was to shift the onus onto the community. Whereas in the past, I would (albeit infrequently) receive ridicule in discussion forums for leaving bugs or issues in free projects, now the responsibility falls on the collective community. If a bug exists, it is not my laziness: I have simply not been paid to fix it, and the community interest in the bug is of a lower-priority than other potential free community projects.

The Patreon wage amount earned every month (along with the overtime and specific notes about what was worked on) is visible to everyone. Essentially, the development process for community projects has been made 'open source', which is a compatible philosophy with the Blender community. Additionally, people are already familiar with the [Blender Development Fund](https://fund.blender.org/), which itself employs the same philosophy. A large number of small donations is more sustainable than a small number of large donations (there is strength in a swarm mentality as it naturally builds redundancy), but having both at the same time is better (the Blender Development Fund is a good example of having smaller user donations with larger corporate grants).

This is all to say that BY-GEN is an example of a project that has been limited by a lack of development in the past, and when work does occur, it tends to happen in sprints to maximize the time investment. As a side effect of this, I have been more inclined to remove features for the sake of making BY-GEN more stable in the long-term, meaning that less corrective development work would be required to keep it working for users in the future, therefore less time would need to be sunk in the tool when new development time was paid for by the community. This would mean that the paid time could be (more likely) spent on more exciting features and content.
