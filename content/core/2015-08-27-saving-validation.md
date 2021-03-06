---
categories:
- fields
date: 2015-08-27T16:46:07Z
order: 4
title: Saving & Validation
url: /core/fields/saving-validation/
---

If you use the Cuisine [Metabox API](/core/admin/metaboxes/) or [SettingsPage API](/core/admin/settings-pages), saving and validation will be automatically handled for you, you can see those pages for details on how the variables will be saved. If you're more of a manual person, you'll find this page comes in handy on how to save and validates these fields.

---

## Saving

The Cuisine field generator will output regular html. The name attribute of the field will be the same as the name attribute passed along in the field function:

{{< highlight php  >}}

<label for="211b2e0ca31b24032d930f07c9a98aaa">My Field</label>
<input type="text" id="211b2e0ca31b24032d930f07c9a98aaa" class="field input-field field-my-field type-text" name="my-name">

{{< / highlight >}}


Dependent on the method of the form you've rendered this field in, you can retrieve the value of this field with a simple __$_POST['my-name']__ or __$_GET['my-name']__ call. Here's an example:

{{< highlight php  >}}

class MyFieldLayout {

    //keep the fields in an array
    var $fields = array();

    function __construct(){

        //populate the fields:
        $this->fields = array(
            Field::text( 'test', 'Test Field' ),
            Field::number( 'number', 'Test Number' )
        );

        //hook into the 'save_post' action
        add_action( 'save_post', function( $post_id ){

            //loop through the fields
            foreach( $this->fields as $field ){

                //check if the fields are set, and save 'em
                if( isset( $_POST[ $field->name ] ) && $_POST[ $field->name ] != '' )
                    update_post_meta( $post_id, $field->name, $_POST[ $field->name ] );

            }
        });
    }
}

{{< / highlight >}}


Cuisine's Metaboxes will save field-data in the post-meta table and they will get the value out of the current post if there is one. The same is true for the Settings Pages only Cuisine will save everything in the __options__ table.


---

## Validating

Some fields, like e-mail and number fields will be automatically validated if you have an html5 capable browser. [You can find a list of self-validating inputs over here](http://www.the-art-of-web.com/html/html5-form-validation/). Other forms of validation need javascript to correctly work.

In WordPress admin, this javascript is included and readily available. Fields will be validated automatically if you've passed the validation array when you declared the field:

{{< highlight php  >}}

Field::text( 
    'my-field',
    'My Field',
    array(
        'validation' => array( 'required', 'address' )
    )
);

{{< / highlight >}} 

If you want to validate a general field which wasn't generated by Cuisine, you can do this in two ways. You can add a __data-validate__ attribute to the field, and it will validate automatically in the admin, or you can use the javascript Cuisine validation library. Here are some examples:

**Using the data-attribute:**
{{< highlight php  >}}

<input type="text" name="my-field" data-validate="required,address"/>

{{< / highlight >}}
Note that the validation-options need to be seperated by a comma.
<br/>

**Using the Cuisine validation library**
{{< highlight javascript  >}}


if( CuisineValidate.empty( value ) === false )

if( CuisineValidate.email( value ) === false )

if( CuisineValidate.number( value ) === false )

if( CuisineValidate.has_number( value ) === false )

if( CuisineValidate.json( value ) === false )

if( CuisineValidate.zipcode( value ) === false )

if( CuisineValidate.slug( value ) === false )


{{< / highlight >}}

<br/>

For the above to work, you need to include the Cuisine Validation script using requirejs. The script is already known to Cuisine, so you can just define it at the top of your javascript document, like this:

{{< highlight javascript  >}}

define([

    'cuisine-validate'

], function(){

    // your code here

});

{{< / highlight >}}
[You can read more on how to work with requirejs over here](/core/assets/requirejs).


