---
category: 
    - 'fields'
title: "Creating Field Types"
date:  2017-11-18T09:02:51+01:00
weight: 5
url: '/forms/fields/creating/'
---

Creating your own field types is really not that hard to do in Cuisine Forms. In this instance we'll be building a simple dropdown-field in which you'll be able to select certain payment issuers.

To recreate this field, follow these steps:

1. [Registering](#registering)
2. [Extending the base class](#extending-the-base-class)
3. [Setting the notification data](#notifications)


---

## Registering

Field types can be registered using a simple WordPress filter. Here's our example:

```php
//register a field-type:
add_filter( 'cuisine_forms_field_types', function( $types ){

	$types['payment_issuers'] = array(
			'name'	=> 'Payment Dropdown',
			'class' => 'MyPlugin\\IssuerField',
			'icon'	=> 'dashicons-shield'
	);

	return $types;

});

```
Let's see what's happening here:

> **$types** takes a new key - value pair. The key (in this case **payment_issuers** )is the string identifier by which your field will be saved and called again.<br/>
> The array being passed takes three arguments:<br/>
> 1. Name: The label that will be shown in the Forms UI<br/>
> 2. Class: The class that will handle all logic<br/>
> 3. Icon: You can add a [dashicon](https://developer.wordpress.org/resource/dashicons) string here. This is completely optional however.

The class is what will take care of all our logic here. Figuring out what all this logic should be would be a big chore, if you couldn't just extend a base-class within Cuisine Forms...

---

## Extending the base class

Cuisine Forms has it's own Field classes. On the front-end they'll most of the time use [Cuisine Core's field engine](/core/fields/field-types/) to render all field types, but Cuisine Forms needs to be able to make fields and field settings available in a UI on the backend. 

This is the reason we've created custom classes for this, all extending this base class:

`ChefForms\Fields\DefaultField`

This base class will handle most of the stuff like saving, adding setting-panels and all drag & drop functionality. The only thing we need to do is change the functions we want to change. In our case (and in most cases) that'll be covered in this example:

```php
namespace MyPlugin;

use MyPlugin\Api;
use ChefForms\Fields\DefaultField;
use Cuisine\Wrappers\Field;

class IssuerField extends DefaultField{

    /**
     * Method to override to define the input type
     * that handles the value.
     *
     * @return void
     */
    protected function fieldType(){
        $this->type = 'payment_issuers';
    }


    /*=============================================================*/
    /**             FRONTEND                                       */
    /*=============================================================*/


    /**
     * Render this field on the front-end
     * @return [type] [description]
     */
    public function render(){

        $this->setDefaults();
        $this->sanitizeProperties();
        $this->properties['name'] = 'payment_issuers';

        $issuers = Api::getIssuers();

        Field::select(

            $this->properties['name'],
            $this->getLabel(),
            $issuers,
            $this->properties

        )->render();

    }

    /*=============================================================*/
    /**             Backend                                        */
    /*=============================================================*/


   		/**
        * Generate the preview for this field:
        * 
        * @return void
        */
       public function buildPreview( $mainOverview = false ){

        $html = '';

        $html .= '<label class="preview-label">'.$this->getLabel().'</label>';

        $choices = array(
            'Paypal',
            'Creditcard',
            'iDeal'
        );

        $html .= '<select class="preview-select preview-input" disabled">';
        
        foreach( $choices as $choice ){
            $html .= '<option>'.esc_html( $choice ).'</option>';
        }
        
        $html .= '</select>';
              
        //do not display these in the lightbox:
        if( $mainOverview ){

            $html .= $this->getFieldIcon();
            $html .= $this->previewControls();

        }

        echo $html;

    }
}

```

In the example above we extend the <ins>DefaultField<ins> provided by Cuisine Forms. We assign it's <ins>fieldType</ins> (payment_issuers) and then we overwrite two functions. 

Both these functions you'll be overwriting most of the time. Let's get into 'em one by one:

#### render();
The render function is what echoes the eventual output to the frontend for this field. In this case it's a regular select-field which we render using [Cuisine Core's field engine](/core/fields/field-types/), but we populate dynamically using a custom <ins>API</ins> class that I'm not going to cover on this page.

#### buildPreview();
Users appreciate live previews and Cuisine Forms gives it to 'em. Using this function you can generate your own live preview, where you can be as accurate as possible. All we're doing in this example is showing a dropdown field with a few payment issuers.

---

## Tweaks

For the most of your fields; **that's it.**
Yeah, you've read it correctly; that's it. That's what is needed to create a custom field type. Saving will be handled automatically, sorting will be done by Cuisine Forms and reading/writing the field output in notifications will also be done automatically. Although all these things are tweakable, we'll cover these issues elsewhere in the documentation.

There's one issue that you might want to change which is the way that Cuisine Forms displays the user-input in the notification after a form get's submitted.

### Changing the value from an entry
Each field has it's own way to handle the values submitted by the user. This function (already available in the DefaultField class) can be fully overwritten:

```php

    public function getValueFromEntry( $entryItems ){

        $response = [ 'label' => '', 'value' => '' ];

        foreach( $entryItems as $item ){

            if( $this->name == $item['name'] ){

                $response['label'] = $this->label;
                $response['value'] = 'ISSUER_'.strtoupper( str_replace( ' ', '_', $item['value'] ) );

            }

        }
        
        return $response;
    }
```

In the example above we find the right field in the submitted form entry and we return a label and value in an array. Now we can easily use this in other processes and we can render the value in a notification to the user.

### Chaning the notification part
We call this the notification part of a field. It basically returns a way to display the input of this field in the notification to the admin or the user. A password field has the following notification part, for instance:

```php 

public function getNotificationPart( $entryItems ){
    return '';
}
```
Because we wouldn't want to send the password out over e-mail, we chose to remove every mention of the notification part altogether, but you can add anything you'd like in here. Especially mind this step when you chose to completely customize [the notifications template](/forms/notifications/templating/).
