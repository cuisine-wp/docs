---
categories:
- admin
date: 2016-05-24T22:32:00Z
order: 4
title: User Metaboxes
url: /core/admin/user-metaboxes/
---

Users have meta-data, just as posts and terms. With User Metaboxes in Cuisine, it's become very easy to create new custom fields for user-profiles.

The User Metabox class is available through [Cuisine's Wrapper System](/getting-started/structure/), so you can start using it by adding

`use Cuisine\Wrappers\UserMetabox`

to the top of your php-document.

---


### Creating a User Metabox

Creating a new metabox with a few custom fields is fairy straightforward. Let's look at an example:

{{< highlight php >}}

$fields = array(
	Field::text( 'twitter-username', 'Twitter Username' ),
	Field::text( 'facebook-username', 'Facebook Username' )
);

UserMetabox::make( 'Social media' )->set( $fields );

{{< / highlight >}}  

<br/>

Let's break that down:

>**UserMetabox::make()** is the function we use to prop up our Metabox. **set()** actually registers it with WordPress. It takes an array of [Field Objects](/fields/using-fields/) or can alternatively take a call to a static php function (see the next example).<br/><br/>
>
>The parameter passed down to the make-function is a label, which will be displayed on the top of your UserMetabox.
>
---

### Creating custom User Metabox layouts

Instead of passing an array of [Field Objects](/fields/using-fields) you can also just call a static function:

{{< highlight php >}}

	UserMetabox::make( 'My Metabox' )->set( '\\MyNameSpace\\MyClass::metabox' );

namespace MyNameSpace;
class MyClass{

	//here's our custom HTML:
	public static function metabox(){

		echo 'Hi from the metabox!';

	}

}

{{< / highlight >}}
