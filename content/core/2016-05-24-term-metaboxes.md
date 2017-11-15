---
categories:
- admin
date: 2016-05-24T22:32:00Z
order: 4
title: Taxonomy Metaboxes
url: /core/admin/term-metaboxes/
---

Metaboxes for terms and taxonomies have been recently introduced to WordPress. In Cuisine, they work exactly the same as regular metaboxes. A Metabox object can take an array of [field-objects](/core/fields/using-fields) which are validated and saved automatically.

The TermMetabox class is available through [Cuisine's Wrapper System](/core/getting-started/structure), so you can start using it by adding

`use Cuisine\Wrappers\TaxonomyMetabox`

to the top of your php-document.

---


### Creating a TermMetabox

Creating a new metabox with a few custom fields is fairy straightforward. Let's look at an example:

{{< highlight php  >}}

$fields = array(
	Field::text( 'website', 'Customer website' ),
	Field::text( 'address', 'Customer address' )
);

TaxonomyMetabox::make( 'Customer Detauils', 'customer' )->set( $fields );

{{< / highlight >}}  

<br/>

Let's break that down:

>**TaxonomyMetabox::make()** is the function we use to prop up our Term-Metabox. In this case we're creating some custom fields for a customer taxonomy. 
> **set()** actually registers the metabox with WordPress. It takes an array of [Field Objects](/core/fields/using-fields) or can alternatively take a call to a static php function (see the next example).<br/><br/>
>
>The parameters passed down to the make-function are, in order of appearence:
>
>*  **label**
>   The label at the top of our Term-Metabox.
>
>*  **taxonomy**
>   The Taxonomy where our metabox will appear. This can also be an array of taxonomies. 
>
---

### Creating custom TaxonomyMetabox layouts

Instead of passing an array of [Field Objects](/core/fields/using-fields) you can also just call a static function:

{{< highlight php  >}}

TaxonomyMetabox::make( 'Customer Details', 'customer' )->set( '\\MyNameSpace\\MyClass::metabox' );


namespace MyNameSpace;

class MyClass{

	//here's our custom HTML:
	public static function metabox(){

		echo 'Hi from the metabox!';

	}

}

{{< / highlight >}}