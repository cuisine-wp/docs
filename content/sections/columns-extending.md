---
category:
    - columns
title: "Extending a column"
date:  2017-11-20T10:17:50+01:00
weight: 5
url: /sections/columns/extending
---

Creating your own columns is easier that you might think. It basically requires just three steps:

1. [Registering your column](/sections/columns/registring.html)
2. [Extending the DefaultColumn base-class](/sections/columns/extending.html)
3. [Providing a default column-template](/sections/columns/template.html)

On this page we'll look at extending the default column class

If you're looking for a cut-and-dry solution [you can check out our free starter column](https://github.com/cuisine-wp/starter-column)

---

### An intro to the class we're extending

The DefaultColumn class, located in the `CuisineSections\Columns\DefaultColumn` namespace handles everything for our columns. Front- and backend. So saving column data? DefaultColumn, deciding which fields are in the admin-lightbox? DefaultColumn. Hooking in before or after the template? DefaultColumn. 

---

### The most basic example

The most basic example features no fields to save in the admin, just a column type that's selectable:

```php

namespace MyCustomColumn;

use CuisineSections\Columns\DefaultColumns;

class Column extends DefaultColumn{

	/**
	 * Type of this column
	 *
	 * @type String
	 */
	public $type = 'custom-column';


}

```
<br/>

The `$type` declaration is needed and should be the same as the [key you've registered it with](/sections/columns/creating). But that's it! You now have a custom column. With extending this class you're basically done.

Obviously this isn't a very usefull column, so let's look at adding some custom fields:

---

### Adding custom fields

Using the [Cuisine Field engine](/core/fields/fields), you can easily create the layout of fields for the lightbox:

```php

/**
 * Get the fields for this column
 * This function always needs to be public.
 * 
 * @return array
 */
public function getFields(){

	return array(
		
		Field::text( 
			'title', //variable name
			'',		 //field label
			array(
				'label' 				=> false,
				'placeholder' 			=> 'Titel',
				'defaultValue'			=> $this->getField( 'title' ),
			)
		),
		Field::media( 
			'media', //this needs a unique id 
			'Media', 
			array(
				'label'				=> 'top',
				'defaultValue' 		=> $this->getField( 'media' )
			)
		)
	);

}

```
<br/>

The <ins>getFields()</ins> function gets called by the <ins>DefaultColumn</ins> class, when building the lightbox. This should return an array of <ins>Cuisine Field</ins> objects. An important note here is that we need to feed the <ins>Field</ins> objects with the column's saved values by using <ins>defaultValue<ins>...

We use the column's <ins>getField()</ins> function for this. Notice that the parameter we pass to <ins>$this->getField()</ins> is exactly the same as the first parameter of the <ins>Field</ins> object.

---

### Creating a custom lightbox

You can also create a custom lightbox for your column, if you need another interface or multiple places to put your fields.
The <ins>DefaultColumn</ins> class just has an overwritable function called <ins>buildLightbox()</ins>.

This is the function as defined in the <ins>DefaultColumn</ins>:

```php
/**
 * Build the contents of the lightbox for this column
 * 
 * @return string ( html, echoed )
 */
public function buildLightbox(){

	$fields = array();

	if( method_exists( $this, 'getFields' ) )
		$fields = $this->getFields();

	echo '<div class="main-content">';
	
		foreach( $fields as $field ){

			$field->render();

			if( method_exists( $field, 'renderTemplate' ) )
				echo $field->renderTemplate();

		}

	echo '</div>';
	echo '<div class="side-content">';
		$this->saveButton();

	echo '</div>';
}

```
<br/>
Let's look at this in a little more detail:

1. First it tries to get the fields from the <ins>getField</ins> function. 
2. It loops through all fields, and renders them
3. Inside the loop it looks for possible JS templates to render for a specific fieds using the <ins>renderTemplate()</ins> function. In all base field-classes, this gets taken care of automatically
4. It adds a save button in the side-content.
