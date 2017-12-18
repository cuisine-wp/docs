---
category: 
    - types
title: "Content Sections"
date:  2017-11-26T14:23:56+01:00
weight: 5
url: /sections/types/content
---

Content sections are the default section types. The types you create by clicking or dragging the "Add new Section" button in the WordPress Admin. Usually when we're talking about sections we'll be mentioning the default content sections.

---

## Classes

There are some classes associated with default content sections which are:

Base class: <ins>\CuisineSections\SectionTypes\ContentSections</ins><br/>
Template class: <ins>\CuisineSections\Templates\ContentSectionTemplate</ins><br/> 
Collection class: <ins>\CuisineSections\Collections\SectionCollection</ins><br/>

Admin logic: <ins>\CuisineSections\Admin\Handlers\SectionHandler</ins><br/>
Admin ui: <ins>\CuisineSections\Admin\Ui\Sections\BaseSectionUI</ins><br/>

---


### Base Class:
Deals with all the properties of a default section. Among these properties you'll find stuff like the chosen view, the position on the page and the associated columns. The ContentSection class extends the BaseSection class. 

---

### Template Class:

The template class makes sure the right template files get loaded in the front-end for this section. You can find more [information about template classes for sections here](/sections/templating/class)

---

### Collection class:
This is the collection of sections for a regular page or other post-type. The base class is a single item in the collection class. The SectionCollection simply contains all sections tied to a specific post-type. 

---

### Admin logic:
Saving, editting and sorting the sections on a specific page all happen in the SectionHandler. 

---

### Admin UI
The basic UI of a content section.

---

## The attributes API.
A section has, like we've discussed above, different attributes like the ID, template name or columns. Each section type has different attributes. Which is why you can overrule them if you're ever extending the class by using the following code:

```php
/**
 * Returns all public attributes
 * 
 * @return array
    */
public function getAttributes()
{
    $attributes = parent::getAttributes();
    $containerAttributes = [
        'sections',
        'container-type'
    ];

    return array_merge( $attributes, $containerAttributes );
}
```
This function adds two new attributes to the container section-type; sections and the container-type. From now on these values will be available in the section template and other places.