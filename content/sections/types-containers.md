---
category: 
    - types
title: "Container Sections"
date:  2017-11-26T14:23:56+01:00
weight: 5
url: /sections/types/containers
---

Container sections simply contain other sections. The standard section container in Cuisine Sections is a grouped container. This does nothing more than contain multiple sections. However; there are seperate plugins that allow you to turn your containers into tab-interfaces, sliders and other fun stuff. The defining factor in this is the container 'view' parameter.

It uses [the same class system as a regular Section](/sections/types/content), with the difference that the base class isn't an extension of BaseSectionClass, but an extension of the \CuisineSections\SectionTypes\Container class.

--- 

## Adding your own container types

Registering a container type happens through a filter. We'll look at an example and then dive into it further:

```php
add_filter( 'chef_sections_containers', function( $data ){
    $data[ 'slider' ] = [
        'label' => 'Section slider',
        'view' => 'slider',
        'class' => '\My-Plugin\Containers\SectionSlider'
    ];
    return $data;
});
```

in the example above we're registering a slider section container. It's label (for picking it out in the UI) is "Section Slider" and the class it refers to is <ins>\My-Plugin\Containers\SectionSlider</ins>.

This class is an extension of the \CuisineSections\SectionTypes\Container class. 
This class works with [the same exact attributes api](sections/types/content/#the-attributes-api) as the regular content section, but just adds the <ins>sections</ins> attribute, which is an instance of the <ins>InContainerCollection</ins>; a collection of all sections in this current container. It also makes sure that the columns collection of each container is absolutely empty.

---

## Classes

Base class: <ins>\CuisineSections\SectionTypes\Container</ins><br/>
Template class: <ins>\CuisineSections\Templates\ContainerTemplate</ins><br/> 
Collection class: <ins>\CuisineSections\Collections\InContainerCollection</ins><br/>

Admin logic: <ins>\CuisineSections\Admin\Handlers\ContainerHandler</ins><br/>
Admin ui: <ins>\CuisineSections\Admin\Ui\Sections\ContainerSectionUI</ins><br/>

---
