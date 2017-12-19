---
category: 
    - 'fields'
title: "Installation"
date:  2017-11-18T09:02:51+01:00
weight: 5
url: '/forms/fields/'
---

Cuisine Forms offers a lot of different field-types out-of-the box.
Here are all available types, along with the way you can create 'em with the [Form Generator](/forms/forms/generating/).

You'll notice that you can just use [Cuisine Core's Field engine](/core/fields/field-types/) and pass those fields to the generator to create your forms from code.

---

## Default fields

#### Text
> A regular text-input.
```php
Field::text( 'name', 'Label', $args )->render();
```

#### Number
> A html5 number-field. Auto-validates 'is-number'
```php
Field::number( 'name', 'Label', $args )->render();
```

#### Email
> A html5 email-field. Auto-validates e-mailadresses
```php
Field::email( 'name', 'Label', $args )->render();
```


#### Textarea
> A multi-lined text input
```php
Field::textarea( 'name', 'Label', $args )->render();
```


#### Checkbox
> Creates a single checkbox. Returns true or false as a string.
```php
Field::checkbox( 'name', 'Label', $args )->render();
```


#### Checkboxes
> Multiple checkboxes. Pass options as the third argument.
```php
$options = array(
	'option-one' => 'Option One', // value - label
	'option-two' => 'Option Two',
	'option-etc' => 'Etc.'
);
Field::checkboxes( 'name', 'Label', $options, $args )->render();
```


#### Radio buttons
> Multiple radio-buttons. Pass options as the third argument.
```php
$options = array(
	'option-one' => 'Option One', // value - label
	'option-two' => 'Option Two',
	'option-etc' => 'Etc.'
);
Field::radio( 'name', 'Label', $options, $args )->render();
```


#### Select box
> A select-dropdown. Pass options as the third argument.
```php
$options = array(
	'option-one' => 'Option One', // value - label
	'option-two' => 'Option Two',
	'option-etc' => 'Etc.'
);
Field::select( 'name', 'Label', $options, $args )->render();
```

---

## Advanced fields

#### Editor
> Adds a wysiwyg editor-field. This isn't the standard WordPress editor though, because that would be a bit 
```php
Field::editor( 'name', 'Label', $args )->render();
```


#### Date
> A date-field using jQuery-ui's datepicker.
```php
Field::date( 'name', 'Label', $args )->render();
```


#### Password
> A regular input-field hiding passwords being entered
```php
Field::password( 'name', 'Label', $args )->render();
```


#### File upload
> A regular file-input field.
```php
Field::file( 'name', 'Label', $args )->render();
```


#### Hidden field
> A hidden field. Ommits the 'Label' parameter.
```php
Field::hidden( 'name', $args )->render();
```


#### Address field
> This is actually three fields in your form: Street, zipcode and city.
```php
Field::address( 'name', 'Label', $args )->render();
```

