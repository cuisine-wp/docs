---
category: 
    - types
title: "Reference sections"
date:  2017-11-26T14:23:56+01:00
weight: 5
url: /sections/types/references
---

Reference sections are pre-created sections that are meant to be created once and then mentioned everywhere.
They are perfect for regulary returning stuff like call to actions. 

You can create a reference in the WordPress admin and going to Section Templates -> Add new. 
Here you can create a new post with your reference section. This section can be used in two ways:

1. As a [blueprint](/sections/types/blueprints): meaning content can later be changed.
2. As a reference: meaning you can load this section everywhere, but the content will always be the same as the way you've created it here.

--- 

References have their own default classes, because they don't really work in the regular Section flow (since they belong to a different post, officially ).

Base class: <ins>\CuisineSections\SectionTypes\Reference</ins><br/>
Template class: <ins>\CuisineSections\Templates\ReferenceTemplate</ins><br/> 
Collection class: <ins>\CuisineSections\Collections\SectionCollection</ins><br/>

Admin logic: <ins>\CuisineSections\Admin\Handlers\SectionBlueprintHandler</ins><br/>
Admin ui: <ins>\CuisineSections\Admin\Ui\Sections\ReferenceSectionUI</ins><br/>

The outlier in this is the template class. Referencese have a different [template hierarchy](/sections/templating/sections) than regular sections.