---
categories:
- admin
date: 2015-08-26T09:35:14Z
order: 3
title: Settings Pages
url: /core/admin/settings-pages/
---

Creating settings pages can be an annoying task in WordPress. With Cuisine it's actually pretty similair to [creating Metaboxes](/core/admin/metaboxes.html).

Settings Page builders in Cuisine can take an array of [field-objects](/core/fields/using-fields.html) which are validated and saved automatically.

The SettingsPage class is available through [Cuisine's Wrapper System](/core/getting-started/structure.html), so you can start using it by adding

`use Cuisine\Wrappers\SettingsPage`

to the top of your php-document.

---


### Creating a Settings Page

Creating a new settings page with a few custom fields is fairly straightforward. Let's look at an example:

{{< highlight php  >}}

$args = array(
	'parent'		=> 'my-post-type',
	'menu_title'	=> 'My Settingspage'
);

$fields = array(

	Field::text( 'name', 'Label' ),
	Field::text( 'name-2', 'Label' )

);

SettingsPage::make( 
	
	'My Settingspage', 
	'my-options'

)->set( $fields );

{{< / highlight >}}  

<br/>

Let's break that down:

>**SettingsPage::make()** is the function we use to create our settings page. **set()** actually registers it with WordPress. It takes an array of [Field Objects](/core/fields/using-fields.html) or can alternatively take a call to a static php function or an array of setting-page tabs (see the next examples).<br/><br/>
>
>The parameters passed down to the make-function are, in order of appearence:
>
>*  **title**<br/>
>   The title of the settings page
>
>*  **slug**<br/>
>	Under which option-name do the settings need to be saved


---

### Using tabs

Cuisine comes with a handy feature to break your settings-page up in tabs. Each tab can take [Field Objects](/fields/using-fields/) just like the settings-page class. You won't have to specify anything else, Cuisine's setting-page system just knows it's dealing with tab-objects instead of fields.

For this you need to load in the SettingsTab wrapper, available here:
`use Cuisine\Wrappers\SettingsTab`

Let's look at an example:

{{< highlight php >}}

//define the fields in seperate arrays:
$firstFields = [ 
    Field::text( 'test', __( 'Testing field' ) ), 
    Field::media( 'media-lib', __( 'Media Library' ) )
];

$secondField = [ 
    Field::checkbox( 'check', __( 'Checkbox field' ) )
    Field::editor( 'editor_field', __( 'Type text here' ) )
];

//create the tabs, passing along the fields:
$tabs = [
    SettingsTab::make( __( 'The label for my tab' ), $firstFields ),
    SettingsTab::make( __( 'The label for my second tab' ), $secondFields )
];

//create the settings page:
SettingsPage::make( 
    'My Settingspage', 
    'my-options'
)->set( $tabs ); //use the $tabs array instead of an array of fields.

{{< / highlight >}}


---

### Creating custom Settings Page layouts

Instead of passing an array of [Field Objects](/core/fields/using-fields.html) you can also just call a static function:

{{< highlight php  >}}

SettingsPage::make( 
	'My Settingspage', 
	'my-options'
)->set( '\\MyNameSpace\\MyClass::settings' );

namespace MyNameSpace;
class MyClass{

	//here's our custom HTML:
	public static function settings(){

		echo 'Hi from the settingspage!';

	}

}

{{< / highlight >}}


---

### Fine-grained control

Using a third argument in the **make()** function we can add a little bit of direction to our settings page. It assumes the best location in the WordPress admin menu of our settings page is as a child to the general Settings tab. Though you might want to switch positions, for instance.

Let's take a look at a few extra options:
<br/>

{{< highlight php  >}}

$args = array(
	'parent'		=> 'tools.php',
	'menu_title'	=> 'My Settingspage',
	'capability'	=> 'manage_options'
);


SettingsPage::make( 
	
	'My Settingspage', 
	'my-options',
	$args

)->set( $fields );

{{< / highlight >}}

Here's a breakdown of the **$args** array:

>*  **parent**
>	The position in the WordPress admin menu. Can handle the wanted admin-url
>	of the parent or a post-type. defaults to general-options.php.
>	In the example above we've placed it underneath the "Extra" menu-item.
>
>*  **menu_title**
>	The title to display in the menu. Defaults to the title passed as the 
>	first argument of **make()**
>
>*	**capability**
>	What the current user needs as capability to actually see, edit and
>	save the options. See [the WordPress codex](https://codex.wordpress.org/Roles_and_Capabilities) for more information.
