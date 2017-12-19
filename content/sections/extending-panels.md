---
category:
    - extending
title: "Extending with panels"
date:  2017-11-20T10:17:50+01:00
weight: 5
url: /sections/extending/panels
---

Cuisine Sections allows you to add custom meta-data to each section. We do this with settings panels. These show up as little tooltipped icons next to a sections title:
![A settings panel](/images/settings-panel.png)<br/>

On this page we'll handle the following topics:

1. [Retrieving panel data](#retrieving-panel-data)
2. [Altering existing settings panels](#altering-existing-settings-panels)
3. [Creating new settings panels](#creating-new-settings-panels)
4. [Defining rules for your panel](#defining-rules-for-your-panel)

---

## Retrieving panel data

All panel data gets saved with the field name as it's key. So retrieving data to use in your templates is quite easy:

```php

if( $section->getProperty('hide_container') == false )
    echo '<div class="container">';

```
The example above checks for the default panel data called "hide_container" and echoes a container div in the section's template depending on wether this checkbox was selected. If you're going to use custom panel data, we highly recommend you overwrite the default [templates provided by the plugin and use your own](/sections/templating/introduction)

---

## Altering existing settings panels.

The standard settings-panel in Cuisine Settings has a few tricks up it's sleeve for extending functionality. 


### Changing the fields
You can add or remove regular [Cuisine Core Field Objects](/core/fields/introduction/) via a filter for the default settings panel. The regular panel contains the following three fields:

- Name: text-field. Used for template fetching (required)
- Classes: text-field for entering multiple CSS classes for the frontend
- Hide container: a checkbox to hide the container div.

Adding another field is quite easy:

```php
add_filter( 'cuisine_sections_setting_fields', function( $fields ){

    $alignment = [
        'top center' => 'Top, center',
        'center center' => 'Center, center',
        'bottom center' => 'Bottom, center'
    ];

    //add the fields:
    $fields[] = Field::image( 'background_image', __( 'Background Image' ) );
    $fields[] = Field::select( 'background_align', __( 'Background Align' ), $aligment );

    return $fields;
});
```
The example above adds two fields to the default settings panel allowing the user to pick an image and a way that image is aligned. The idea being that we can use this data in our template to add a background image the user chose.


### Changing the icon or position

To change the default arguments for a panel (like the icon or the position) you can use this filter tied to the default settings panel:

```php
add_filter( 'cuisine_sections_base_panel_args', function( $args ){
    $args['position'] = 10; //set the position at 10 instead of the default -1
    $args['icon'] = 'dashicons-camera'; //replace the default gear with a camera icon
    return $args;
});
```
Currently these are the only settings you'll be able to change in the standard settings panel.

---

## Creating new settings panels

The goal for creating Cuisine and all it's subsequent tools is to unify the way you create your WordPress websites and plugins. This is why creating a Sections' Setting Panel is exactly the same as creating [a Metabox in Cuisine](/core/admin/metaboxes/). All you need is an array of [Cuisine Field objects](/core/fields/introduction/). The example below shows you just how to create a new settings panel. It uses the SettingsPanel class found in [Sections's wrapper system](/core/getting-started/structure/), which you can include as follows:

`use ChefSections\Wrappers\SettingsPanel`

```php

$fields = [
    Field::text( 'test', __( 'Test field' ) ),
    Field::text( 'test2', __( 'Test 2 field' ), [ 'placeholder' => __( 'type something...' ) ] )
];

SettingsPanel::make( 
    'My Settings Panel'
    'my-settings',
    [ 'icon' => 'dashicons-admin-site' ]
)->set( $fields );
```

This example creates a settings panel with two text fields. Let's break the arguments down:

1: the label **My Settings Panel**
This is the title of the panel. It will show up at the top of your panel and as a tooltip on the icon when hovering over the icon.

2: the slug **my-settings**
This is a simple slug to make sure your settings panel is unique.

3: the arguments
This is an array of arguments. In the example above we've chosen to just add an icon (which can be any [dashicon](https://developer.wordpress.org/resource/dashicons) WordPress offers). Possible arguments are:

> **Icon:** can be any valid dashicon or url to an image.<br/>
> **Position:** determine where this panel will sit compared to other settings panels<br/>
> **Rules:** when this panel might show up (and at what section). More on this later.<br/>


---

## Defining rules for your panel

Sometimes you want to restrict the amount of sections a settings panel is for. For example; if you are creating a custom [Container section](/sections/types/containers/) to which you plan to add a slider script, you might want users to select how fast that slider should go and if the slider should contain controls. In that case, you wouldn't want the panel to show up in regular sections, just your custom container type. So consider this example:

```php

$fields = [
    Field::checkbox( 
        'auto_play', 
        __( 'Play automatically (be careful!)' ),
        [ 'defaultValue' => false ]
    ),
    Field::number( 
        'speed', 
        __( 'Slider speed' ), 
        [ 'defaultValue' => 3000 ]
    )
];

SettingsPanel::make(
    __( 'Slider settings' ),
    'slider_settings',
    [ 
        'rules' => [
            'containerType' => 'slider',
            'userRole' => 'administrator'
        ]
    ]

)->set( $fields );
```

In this example we set two fields: an auto-play checkbox and a speed field. Then we create our settings-panel where we add two rules:

- Only show up in the slider container
- Only show up when the user is an administrator, because having control over "auto-play" in sliders is dangerous ;-)

These rules will get checked before the panel gets rendered and if the section isn't a container or isn't of the type 'slider', it won't render. If the logged in user doesn't have the role 'administrator' it won't render as well.


### Available restrictions:
Here's an example with all rules set:

```php

SettingsPanel::make( 
    __( 'My settings panel' ),
    'my-settings-panel',
    [
        'rules' => [
            'sectionTypes' => ['content', 'container'],
            'sectionView' => 'fullwidth',
            'inContainer' => false,
            'containerType' => false,
            'userCap' => 'edit-sections',
            'userRole' => ['administrator', 'editor']
        ]
    ]
)->set( $fields );

```

Here's a break down:

> **sectionType**: Array/String. Can be any of the [registered section types](/sections/types/content)<br/>
> **sectionView**: Array/String. Can be any of the [section views(/sections/extending/views)]<br/>
> **inContainer**: Boolean/String. True/false for all containers. String for a specific container; targets sections inside a container<br/>
> **containerType**: Array/String. Can be any [registered container type](/sections/types/containers)<br/>
> **userCap**: Array/String. Can be any registered WordPress user capability. Applies to the logged-in user.<br/>
> **userRole**: Array/String. Can be any registered WordPress user role. Applies to the logged-in user.

