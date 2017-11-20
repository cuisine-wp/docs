---
category:
    - templating
title: "Introduction to Templating"
date:  2017-11-20T10:17:50+01:00
weight: 5
url: /sections/templating/introduction
---


Templates in Cuisine Sections are all completely overwritable. That's what makes it such a flexible system. On this page you'll learn how the template-engine works in general and how you can replace individual templates.

---

## Structure

Cuisine Sections does templating like [WooCommerce](https://www.woothemes.com/woocommerce/) does templating. We provide a default template, readily available from the plugin itself, which you can copy and place in your theme. Cuisine Sections will allways check the theme first and see if there are custom templates available. If there aren't any custom templates available Cuisine Sections will default back to the original provided by the plugin itself.

In Cuisine Sections we have five types of templates, that all have their sub-page in these docs:

1. [Sections](/sections/templating/sections/) - A template for a single section
2. [Columns](/sections/templating/columns/) - A template for a single column, output ranges vastly per column-type
3. [Collections](/sections/templating/collections/) - Templates around our collection column. Since these differ per post-type and application, the templating surrounding collections is a bit more complicated than regular columns.
4. [Containers](/sections/templating/containers/) - Templates around section containers.
5. [Elements](sectionssections/templates/elements.html) - Templates for stuff like loaders, and other UI.

All of these are overwritable, however; when there's a new feature in a column we can't guarentee this will work with your overwritten templates. So to keep backwards compatibility at maximum, we also offer a [lot of template filters that will come in handy.](/sections/templating/filters/)

---

## Hierarchy

The default folders where Cuisine Sections will be looking are:
```
/my-theme/sections/
/my-theme/columns/
/my-theme/collections/
/my-theme/elements/
```

But there are filters available for anybody who wants their templates in different directories:

```php
add_filter( 'cuisine_sections_column_template_folder', function( $folder ){
	return 'templates/columns/';
});
```

Each template is overwritable in a certain hierarchy. Column templates are, for instance, prefixed by the section-name or section ID they are in, so you can be extremely specific in which column you'll overwrite.

In the WordPress admin, when logged in as an administrator, you'll find a so called "template snitch" for both sections and columns. This wil tell you exactly in what hierarcy Cuisine Sections will be looking for your custom template.

Here's what to look for:<br/>
![The Template Snitch](/images/snitch.png)<br/>
You will see the dropdown once you mouse over the template icon.




