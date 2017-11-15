---
categories:
- fields
date: 2015-08-27T16:44:38Z
order: 2
title: Using Custom Fields
url: /core/fields/using-fields/
---

You can use the fields anywhere. These classes just return HTML. Creating a new field is quite easy:

{{< highlight php  >}}

	Field::text( 'my-name', 'My Label' )->render();

{{< / highlight >}}

The example above will put out the following HTML:

{{< highlight html  >}}

	<div class="field-wrapper text">

		<label for="211b2e0ca31b24032d930f07c9a98aaa">My Label</label>
		<input type="text" id="211b2e0ca31b24032d930f07c9a98aaa" class="field input-field field-my-name type-text" name="my-name">

</div>

{{< / highlight >}}

As you can see we put every field in it's own wrapper. The field's ID get generated from the name, label and type, so will always be unique. 

---

## Additional arguments

As you might imagine, a name and label are hardly enough information for a field and you'll probably need to provide it with some more information, like which placeholder to use or what the default value will be. We've added this as an optional argument. 

{{< highlight php  >}}

	$args = array(
		'label'			=> 		'top',                      //options: top, left or false
		'placeholder'	=> 		'My placeholder',
		'defaultValue'	=>		'My Default Value',
		'required'		=>		true                        //is this a required field?
		'validation'	=>		array( 'not-empty' )        //More on this at Saving & Validation.
		'class'			=>		array( 'my-custom-class' )  //Additional classes you'd like to pass
);

Field::text( 'my-name', 'My Label', $args )->render();


{{< / highlight >}}


The html-output to this field is quite a bit different:

{{< highlight html  >}}

	<div class="field-wrapper text label-top my-custom-class">

		<label for="...">My Label</label>
		<input type="text" id="..." class="field input-field field-my-name type-text" name="my-name" placeholder="My placeholder" value="My Default Value" data-validate="required,not-empty">

</div>

{{< / highlight >}}

---

## Multiple-choice fields

In regular fields the arguments-array is the third argument passed to the **Field::function()**, but in multiple-choice fields (like select-boxes, checkboxes and radio-buttons) the argument is fourth. Another example:

{{< highlight php  >}}


//the options array is in this case just a list of key -> value pairs.
$options = array(
	'option-one' => 'Option One', // value - label
	'option-two' => 'Option Two',
	'option-etc' => 'Etc.'
);

Field::select( 'my-name', 'My Label', $options, $args )->render();


{{< / highlight >}}