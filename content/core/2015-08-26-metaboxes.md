---
categories:
- admin
date: 2015-08-26T09:35:03Z
order: 2
title: Metaboxes
url: /core/admin/metaboxes/
---

Custom metaboxes are one of the things that make WordPress great. In Cuisine, the Metabox object can take an array of [field-objects](/core/fields/using-fields) which are validated and saved automatically.

The Metabox class is available through [Cuisine's Wrapper System](/core/getting-started/structure), so you can start using it by adding

`use Cuisine\Wrappers\Metabox`

to the top of your php-document.

---


### Creating a Metabox

Creating a new metabox with a few custom fields is fairly straightforward. Let's look at an example:

{{< highlight php  >}}

$fields = array(

	Field::text( 'name', 'Label' ),
	Field::text( 'name-2', 'Label' )

);

Metabox::make( 'My metabox', 'post' )->set( $fields );

{{< / highlight >}}  

<br/>

Let's break that down:

>**Metabox::make()** is the function we use to prop up our Metabox. **set()** actually registers it with WordPress. It takes an array of [Field Objects](/core/fields/using-fields) or can alternatively take a call to a static php function (see the next example).<br/><br/>
>
>The parameters passed down to the make-function are, in order of appearence:
>
>*  **label**
>   The label at the top of our Metabox.
>
>*  **post_type**
>   The Post Type where our metabox will appear. This can also be an array of post-types. 
>
---

### Creating custom Metabox layouts

Instead of passing an array of [Field Objects](/core/fields/using-fields) you can also just call a static function:

{{< highlight php  >}}

	Metabox::make( 'My Metabox', 'post' )->set( '\\MyNameSpace\\MyClass::metabox' );

namespace MyNameSpace;
class MyClass{

	//here's our custom HTML:
	public static function metabox(){

		echo 'Hi from the metabox!';

	}

}

{{< / highlight >}}


---

### Fine-grained control

If you still need to get into the nitty-gritty stuff we've got you covered. There is a third parameter to the **make()** function you can pass. Here's an example:

<br/>

{{< highlight php  >}}

$options = array(
	'context'			 => 'side'
	'priority'        	 => 'default'
);


Metabox::make( 'My metabox', 'post', $options )->set( $fields );


{{< / highlight >}}

See the [WordPress Codex](https://codex.wordpress.org/Function_Reference/add_meta_box) for more information on which arguments to pass.

