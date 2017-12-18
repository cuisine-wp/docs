---
category: 
    - types
title: "Blueprint sections"
date:  2017-11-26T14:23:56+01:00
weight: 5
url: /sections/types/blueprints
---

Blueprint sections are pre-created sections that are used (and filled with content) later. You can create a blueprint in the WordPress admin and going to Section Templates -> Add new. Here you can create a new post with your blueprint section. This section can be used in two ways. 

1. As a blueprint: meaning content can later be changed.
2. As a [reference](/sections/types/references): meaning you can load this section everywhere, but the content will always be the same as the way you've created it here.

--- 

The blueprint doesn't have it's own default classes, because it gets used to quickly build new structured [content sections](/sections/types/content). Therefor it doesn't need to have it's own UI or template classes. What it does need is it's personal admin handler and a simple base-class:
these makes sure that, whenever you load a blueprint; it get's turned into a regular content section.

Base class: <ins>\CuisineSections\SectionTypes\Blueprint</ins><br/>
Admin handler class: <ins>ChefSections\Admin\Handlers\SectionBlueprintHandler</ins>.

If the original section is -for instance- a container; the newly created blueprint will also be of the container type. It will also add all the containered sections you might have added.

