---
categories:
- fields
date: 2015-08-27T16:45:33Z
order: 3
title: Available Field Types
url: /core/fields/field-types/
---

Cuisine comes with a lot of field-types build in. Here's a list:


### Textual inputs

> #### Text
> A regular text-input.
> {{< highlight php  >}}
Field::text( 'name', 'Label', $args )->render();
{{< / highlight >}}
>
> <br/>
>
> #### Textarea
> A textarea field.
> **Aditional arguments: ** Row ( pass the amount of rows this textarea needs)
> {{< highlight php  >}}
Field::textarea( 'name', 'Label', $args )->render();
{{< / highlight >}}
>
> <br/>
>
> #### Date
> A date-field using jQuery-ui's datepicker.
> {{< highlight php  >}}
Field::date( 'name', 'Label', $args )->render();
{{< / highlight >}}
>
> <br/>
>
> #### Number
> A html5 number-field. Auto-validates 'is-number'
> {{< highlight php  >}}
Field::number( 'name', 'Label', $args )->render();
{{< / highlight >}}
>
> <br/>
>
> #### Email
> A html5 email-field. Auto-validates e-mailadresses
> {{< highlight php  >}}
Field::email( 'name', 'Label', $args )->render();
{{< / highlight >}}

<br/>

### Choice inputs

> #### Checkbox
> Creates a single checkbox. Returns true or false as a string.
> {{< highlight php  >}}
Field::checkbox( 'name', 'Label', $args )->render();
{{< / highlight >}}
>
> <br/>
>
> #### Checkboxes
> Multiple checkboxes. Pass options as the third argument.
> {{< highlight php  >}}
$options = array(
    'option-one' => 'Option One', // value - label
    'option-two' => 'Option Two',
    'option-etc' => 'Etc.'
);
Field::checkboxes( 'name', 'Label', $options, $args )->render();
{{< / highlight >}}
>
> <br/>
>
> #### Radio buttons
> Multiple radio-buttons. Pass options as the third argument.
> {{< highlight php  >}}
$options = array(
    'option-one' => 'Option One', // value - label
    'option-two' => 'Option Two',
    'option-etc' => 'Etc.'
);
Field::radio( 'name', 'Label', $options, $args )->render();
{{< / highlight >}}
>
> <br/>
>
> #### Select box
> A select-dropdown. Pass options as the third argument.
> {{< highlight php  >}}
$options = array(
    'option-one' => 'Option One', // value - label
    'option-two' => 'Option Two',
    'option-etc' => 'Etc.'
);
Field::select( 'name', 'Label', $options, $args )->render();
{{< / highlight >}}

<br/>


### Special inputs

> #### Image
> Adds a thumbnail of the selected image and a button to edit the image. Opens the WordPress media library and > saves the image's ID, the three default WP-sizes and some meta-information. Currently only works in the > WordPress admin.
> {{< highlight php  >}}
Field::image( 'name', 'Label', $args )->render();
{{< / highlight >}}
>
> <br/>
>
> #### Media
> Adds a gallery where multiple images, videos and other media can be saved. Items can be ordered by drag & drop. This saves the media-item's ID, position and thumb-url.
> {{< highlight php  >}}
Field::media( 'name', 'Label', $args )->render();
{{< / highlight >}}
>
> <br/>
>
> #### Repeater field
> Similar to Advanced custom fields repeater-fields. Creates a layout that can be repeated indefinitely. Takes an array of Field objects as it's third parameter.
> {{< highlight php  >}}

$fields = array(
	Field::text( 'title', 'Title' ),
	Field::date( 'date', 'Date' )
);
Field::repeater( 'name', 'Label', $fields, $args )->render();

{{< / highlight >}}
>
> #### Flex field
> Similar to Advanced custom fields flexible-layout-fields. Creates multiple layouts that can be repeated indefinitely. Takes an array of layouts (which is just an array of Field objects ) as it's third parameter.
> {{< highlight php  >}}

$layouts = array(
    'button' => [
        'layout' => 'button',
        'label' => __( 'Button' ),
        'fields' => [
            Field::text( 'title', __( 'Title' ) ),
            Field::text( 'button_text', __( 'Click here' ) ),	
        ]
    ],
    'textblock' => [
        'layout' => 'textblock',
        'label' => __( 'Tekst block' ),
        'fields' => [
            Field::title( 'title', __( 'Title' ) ),
            Field::editor( 
                'textarea', 
                __( 'Content' )
            )
        ]
    ]
);

Field::flex( 'button_or_text', 'Label', $layouts, $args )->render();

{{< / highlight >}}