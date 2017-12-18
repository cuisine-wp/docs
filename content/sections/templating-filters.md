---
category: 
    - templating
title: "Templating Filters"
date:  2017-11-26T14:23:56+01:00
weight: 5
url: /sections/templating/filters
---

Sections knows many filters to make your templating even easier. Here's a list of what we're talking about:

- [Changing basefolders](#changing-base-folders)
- [Before / After action hooks](#before-after-action-hooks)
- [Changing a specific template](#changing-a-specific-template)
- [Changing the template hierarchy](#changing-the-template-hierarchy)
- [Creating a custom section template class](#creating-a-custom-section-template-class)
- [Changing the html output of sections](#changing-the-html-output-of-sections)
- [Changing section css classes](#changing-section-css-classes)

---

### Changing base folders
If you've been reading other parts of the section documentation, you've seen base folders pop up a lot. These folders house the custom template rewrites in your theme. They are, in order of importance:

- /columns
- /collections
- /collections/blocks
- /sections
- /elements

Sections in this case are pretty low down the list because in practice you won't need to change a whole lot of section templates. You can change these base folders (dependent on type) by using the following filter:

`cuisine_sections_{type}_template_base`

where you change {type} to the type you are targetting. Here are some examples:
```php
//change the columns folder to 'custom-column-folder'
add_filter( 'cuisine_sections_column_template_base', function( $baseFolder ){
    return 'custom-column-folder';
});

//change the block base folder to 'post_types/'
add_filter( 'cuisine_sections_block_template_base', function( $baseFolder ){
    return 'post_types';
});
```

---

### Before & After action hooks
These aren't filters; they are action-hooks. Nevertheless, they play a vital role in customizing templates in Cuisine Sections. The templates run before each column and each section.

`cuisine_sections_before_{type}_template`<br/>
`cuisine_sections_after_{type}_template`

In this case {type} should be replaced with 'section' or the type of column. Here are some examples:

```php 
add_action( 'cuisine_sections_before_section_template', function( $object ){
    echo '<h3>Here\'s a section:</h3>'; //adds a title above each section
});
```
The <ins>$object</ins> that get's passed is either the section or the column object we're fetching a template for. So if you wanted to further specify a text, you could use the filter like this:

```php
add_action( 'cuisine_sections_after_content_column_template', function( $object ){
    if( $object->getField( 'title' ) == 'test' )
        echo '<strong>Share if you\'ve enjoyed the read!</strong>'; //adds a text after the column with 'test' as it's title.
});
```

To get the proper column types, see the [Column template hierarchy]('/sections/columns/extending/#column-template-hierarchy).

---

### Changing a specific template
Templates in Sections can be replaced at the absolute last minute, just so you're always sure that what gets pulled in, is the file you've specified. Here's an example:

```php

//load a custom collection template when the object we're loading a template for
//is of the type 'collection'.
add_filter( 'chef_sections_located_template', function( $located, $template ){
    if( $template->type == 'column' && $template->object->type == 'collection' )
        return Url::path('my-plugin/templates/collection-template');
});
```
The value returned in this function needs to be a valid filepath. We recommend using [Cuisine's URL Utility](/cuisine/utilities/url) to fetch the correct path for you.
The <ins>$template</ins> variable that get's provided is an instance of the [Template Class](/sections/templating/class) which can be used to narrow down your selection process.

---

### Changing the template hierarchy
The template hierarchy is there for each column and section. If you ever which to change it's order, or to utterly simplify it, use these filters:

`chef_sections_section_template_hierarchy`<br/>
`chef_sections_column_template_files`

Both of these filters expect an array to be returned. This array can -however- have just one template, if you want that:
```php

add_filter( 'cuisine_sections_column_template_files', function( $hierarchy ){
    return [ 'columns/one-file-fits-all' ]; //this isn't recommended :)
});
```

---

### Creating a custom section template class
Template classes search for and eventually load the sections template files. [Each section type](/sections/types/index) has it's own rules, hence it's own Template class. Here's an overview of the existing classes:

- ContentSectionTemplate ([default section](/sections/types/default) template class)
- ContainerTemplate (for [section containers](/sections/types/containers))
- ReferenceTemplate (for [reference sections](/sections/types/reference))
- DynamicSectionTemplate (see below for explanation)

If you have a custom section type which you wish to connect to a custom template class, you can use the following example code:
```php
add_filter( 'cuisine_sections_section_template_class', function( $class, $section ){
    if( $section->id = 1 && $section->type == 'content' )
        return '\\MyPlugin\\Templates\\SectionTemplate';
});
```

The class in the example above <ins>(MyPlugin\Templates\SectionTemplate)</ins> needs to be an extension of the
<ins>BaseSectionTemplate</ins> like this:

```php
namespace MyPlugin\Templates;

use CuisineSections\Templates\BaseSectionTemplate;

class SectionTemplate extends BaseSectionTemplate{

}
```

#### DynamicSectionTemplate

Dynamic section templates are there to hot-load custom templates for the `get_section()` template tag. This class is, however, fully extendable and requires a path as it's second parameter. You can use this class to on-the-fly load precisely your template. Here's two examples:

```php
//via get_section:
get_section( $postId, $sectionId, '/sections/my-custom/first.php' );

//via the class:
( new DynamicSectionTemplate( $section, '/sections/my-custom/first.php' ) )->display();
```
For more information on the get_section function, please check the [showing sections](/sections/getting-started/showing-sections/) page.

---

### Changing the html output of all sections

All html output for Sections runs through a filter before it gets echoed in a template. With the <ins>cuisine_sections_output</ins> filter you can easily alter this output:

```php

add_filter( 'cuisine_sections_output', function( $html ){
	
	$html .= '<div class="call-to-action">';

		$html .= '<strong>Contact us as soon as possible!</strong>';
		$html .= '<a href="/contact" class="button">Contact us</a>';

	$html .= '</div>';

	return $html;
});

```
<br/>

In the example above, we create a simple call to action to place beneath all sections.

---

### Changing html output of the section-div

You can change the html-output of the section starting div and add your own data-attributes or custom ID...
The section instance gets passed as a second parameter.
Here's an example:

```php
add_filter( 'cuisine_section_opening_div', function( $div, $section ){
	
	if( $someConditional == true )
		$div .= 'data-custom="my-custom-data-attribute"';

	return $div;

});
```

---

### Changing section css classes

Css classes in sections are also filterable. The section instance gets passed as a second parameter:

```php
add_filter( 'cuisine_section_classes', function( $classes, $section ){

	if( $section->getField( 'title' ) == 'My Title' ){

		$classes[] = 'custom-section-class';

	}

	return $classes;
	
});
```
