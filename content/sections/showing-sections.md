---
category: 
    - getting-started
title: "Showing Sections"
date:  2017-11-18T09:05:38+01:00
weight: 5
url: /sections/getting-started/showing-sections/
---

Cuisine Sections doesn't do stuff automatically when it comes to content. That's because it was written for developers and we know you guys and gals want to be able to put sections wherever you wish. 

You can make it as easy and as hard as you want.

---

## Calling the_sections()

In line with WordPress' default template tags we've added a few of our own. Although it pains us to do so and not work completely OOP, we understand that this fits in a bit more with WordPress' way of working.

To display all sections in the right order you can just call
`the_sections();`<br/>

This echoes all output. You can also fetch the html, for late use with:
`get_sections();`<br/>

Checking to see wether or not a page or post even has sections you can use:
`has_sections();`<br/>

If you have access to a <ins>Section</ins> object, you can also show it's columns with template tags:
`get_columns( $section );`

The <ins>$section</ins> variable in this example needs to be a valid instance of a `ChefSections\SectionTypes`-class. You can check this by seeinf if it implements a <ins>ChefSections\Contracts\Section</ins> interface.

---

## Extending the Walker

All of the template-tag examples above use the <ins>CuisineSections\Front\Walker</ins> class to display sections, columns and section-templates.

This walker can, obviously be completely extended to suit your own needs. The <ins>Walker</ins> class relies heavily on an extended [Cuisine Collection](/core/utilities/collections) called `ChefSections\Collections\SectionCollection`, which you are also free to extend.

Although the walker class is free to be extended, some methods need to be still callable:

#### walk();

The <ins>walk()</ins> method loops through all found sections and displays them, triggering the Sections and Columns <ins>beforeTemplate()</ins> and <ins>afterTemplate()</ins> in the process. These methods add flexibility and provide you with the options to, for example, register custom scripts or add extra html. 

Here's the default <ins>walk()</ins> method, as it appears in the <ins>Walker</ins> class:

```php
public function walk(){

    ob_start();

    foreach( $this->collection->getNonContainered() as $section ){

        $section->beforeTemplate();

            Template::section( $section )->display();

        $section->afterTemplate();
    }

    //reset post-data, to be sure:
    wp_reset_postdata();
    wp_reset_query();


    return apply_filters( 'cuisine_sections_output', ob_get_clean(), $this );
}
```
As you can see the complete output is eventually filterable through <ins>cuisine_sections_output</ins>.

---

### setCollection();

The default <ins>setCollection</ins> method populates a protected <ins>$collection</ins> variable in the <ins>Walker</ins> class. You can change the outcome of this function (which -by default- uses a post-id to get all the sections associated with a post), as long as the output is a version of the <ins>SectionCollection</ins> class.