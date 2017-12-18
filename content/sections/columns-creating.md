---
category:
    - columns
title: "Creating a column"
date:  2017-11-20T10:17:50+01:00
weight: 5
url: /sections/columns/creating
---

Creating your own columns is easier that you might think. It basically requires just three steps:

1. Registering your column
2. [Extending the DefaultColumn base-class](/sections/columns/extending)
3. [Providing a default column-template](/sections/templating/columns)

And if you're feeling cheeky you can also change the [data of your column as it's being saved](/sections/columns/saving)

On this page we'll look at registering a new column-type.
If you're looking for a cut-and-dry solution [you can check out our free starter column](https://github.com/cuisine-wp/starter-column)

---

## Registering on the right hook

Before we start adding our custom column-type we'll have to make sure that Sections get's loaded. We use the `cuisine_sections_loaded` hook for this:

```php

add_action( 'cuisine_sections_loaded', function(){
		
	//load your event listeners here
	...

});
```

<br/>
In our [Starter Column](https://github.com/cuisine-wp/starter-column) we trigger the <ins>ColumnIgniter</ins> class with the autoloader after this action.

---

## Registering the actual column

Registering the actual column happens via a regular WordPress filter. It takes an array with three parameters and a key.

1. Key: the unique type-string that we'll use to save and fetch your column data.
2. Name: the display name of your column; this needs to be translatable.
3. Class: the class of your column, easiest would be to extend <ins>\CuisineSections\Columns\DefaultColumn</ins> for this.
4. Template: the path to your columns default template file.

Here's an example:

```php

add_filter( 'cuisine_sections_column_types', function( $types ){

	$template = Url::path( 'plugin', 'my-plugin-folder/Assets/template.php' );

	//change the $types[ key ] and the name value:
	$types['my-column'] = array(
		'name'		=> 'My Custom Column',
		'class'		=> 'MyColumn\Column',
		'template'	=> $template
	);

	return $types;
});

```
<br/>

Let's break that down:

First we use the <ins>cuisine_sections_column_types</ins> filter to add a new value to the column $types array.

Inside the filter we use a [utility class in Cuisine Core](/core/utilities/url) to fetch the path of our plugin folder. 
After that we add a <ins>my-column</ins> key to the $types array, with a name, class and template value for our column.

<br/>