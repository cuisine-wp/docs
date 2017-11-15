---
categories:
- fields
date: 2015-08-27T16:46:26Z
order: 5
title: Creating your own field types
url: /core/fields/creating-your-own-field-types/
---

Fields in Cuisine are completely modular. You can easily create your own field-type. We'll add an address field in this article, which is a collection of multiple small input-fields.

---

## Registering your field

Registering your new field-type happens via a WordPress filter. You just need to pass a slug, name and class and you're all set. Here's an example:


{{< highlight php  >}}

add_filter( 'cuisine_field_types', function( $types ){

	$types['address'] = array(
				'name'		=> 'AddressField',
				'class'		=> 'MyPlugin\Fields\AddressField'
	);

	return $types;

});

{{< / highlight >}}


The class also needs the namespace if you're using that. The slug needs to be a unique key in the __$types__ array. This will also be the string you'll need for actually invoking your field. After registering, you can use the following code to add your field to metaboxes, settings pages or your own system:

{{< highlight php  >}}

	Field::address( 'my-address-field', 'My Address Field' );

{{< / highlight >}}


You'll notice the function we reference in the __Field__ class is the same as the key we've passed to the __types__ array. The other parameters you pass along are (usually) the same as other fields. In the next section we'll look at creating the actual class that runs the field.


---

## Extending the DefaultField class

The DefaultField class lives in the **Cuisine\Fields** namespace. So extending this is quite easy:

{{< highlight php  >}}

namespace MyPlugin\Fields

use Cuisine\Fields\DefaultField;

class AddressField extends DefaultField{
	
	/**
	 * Method to override to define the input type
	 * that handles the value.
	 *
	 * @return void
	 */
	protected function fieldType(){
	    $this->type = 'address';
	}


}

{{< / highlight >}} 


The only real function needed after extending is the __fieldType()__, which returns the same string as the key you've set in the __$types__ array. Of course this doesn't do much. Your field is registered, and you can call it, but right now it just outputs a regular text field because it extends the DefaultField class. We can start creating our address-fields now and we need to overwrite a few more functions to do it. Consider this example;

<br/>

{{< highlight php  >}}

use Cuisine\Wrappers\Field;

class AddressField extends DefaultField{
	
	...

	/**
	 * Build the html
	 *
	 * @return String;
	 */
	public function render(){

		$html = '<div class="address-field field-wrapper">';

			$html .= $this->getLabel();

			$html .= $this->build();

		$html .= '</div>';
		
		echo $html;
	}


	/**
	 * Get the sub fields for the address
	 *
	 * @return html
	 */
	public function build(){

		$subFields = $this->getSubFields();

		$html = '';

		foreach( $subFields as $subField ){

			$html .= $subField->build();

		}

		return $html;
	}


	/**
	 * Get the sub fields for the address-field
	 *
	 * @return array
	 */
	private function getSubFields(){

		return array(

			Field::text( 
				'street', 
				'Street & Number',
				array(
					'validation' => 'address'
				)
			),

			Field::text(
				'zip',
				'Zipcode',
				array(
					'validation' => 'zipcode'
				)

			), 

			Field::text(
				'city',
				'City',
				array(
					'validation' => 'not-empty'
				)
			)

		);

	}


{{< / highlight >}}


The example above overwrites two functions; the **render()** and the **build()** function. In the DefaultField class the **render()** function echoes the **build()** function and wraps it's contents up in a __field-wrapper__ div. It also adds the field label.

The build-function in both this class and the DefaultField class return the html for the field. In the case of our AddressField class, we're populating it with three new Field instances, defined in the **getSubFields()** function. We use the **build()** function of each of those sub-fields to get the right html, but you can easily create your own output here.



---

## Extending the ChoiceField class

Extending multiple-choice fields like checkboxes, radio-buttons and select dropdowns can be done by using the ChoiceField class. This is an extention of the DefaultField class described above, but adds the feature to create, edit and sort options for that field. It works the same as the default class, but you get acces to an extra array of options. So if we want to wrap all options in custom html, we can do something like this:


{{< highlight php  >}}

	use Cuisine\Fields\ChoiceField;


	class MyChoiceField extends ChoiceField{


	    /**
	     * Method to override to define the input type
	     * that handles the value.
	     *
	     * @return void
	     */
	    protected function fieldType(){
	        $this->type = 'mychoicefield';
	    }



	    /**
	     * Build the html
	     *
	     * @return String;
	     */
	    public function build(){

	        $html = '';
	        $choices = $this->getChoices();
	        $choices = $this->parseChoices( $choices );

	        foreach( $choices as $choice ){

	            $html .= $this->buildChoice( $choice );

	        }

	        return $html;
	    }


	    /**
	     * Return html for a single choice
	     * 
	     * @param  array/string $choice
	     * @return string HTML
	     */
	    public function buildChoice( $choice ){

	        $html = '';

	        //set choice variables:
	        $id = 'subfield-'.$this->id.'-'.$choice['id'];
	        $value = $choice['key'];
	        $label = ( isset( $choice['label'] ) ? $choice['label'] : false );

	        $html .= '<span class="subfield">';

	        	$html .= 'Label: '.( $label ? $label : '' ).'<br/>';

	        	$html .= 'Value: '.$value.'<br/>';

	        	$html .= 'Selected?: '.( in_array( $value, $this->properties['defaultValue'] ) ? 'true' : 'false' ).'<br/>';

	        $html .= '</span>';

	        return $html;

	    }

{{< / highlight >}}

<br/>

In the example above, we create a simple span for each of the choices with it's label, value and whether it's selected or not. 