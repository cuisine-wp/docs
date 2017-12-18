---
category:
    - columns
title: "Saving column data"
date:  2017-11-20T10:17:50+01:00
weight: 5
url: /sections/columns/saving
---

Okay, great. You've [registered your own column](/sections/columns/creating) and then [extended the DefaultColumn class for your custom functionality](/sections/columns/extending). Now comes the time to save everything.

---

## Automatic saving
First thing's first: you're probably already done with your column. All fields passed along a column are saved automatically once the lightbox (or your custom implementation of it) are closed. All data will be saved under the names you've given to the fields and retrievable with the <ins>getField()</ins> method.

An example:
```php

public function getFields(){
    return [
        Field::text( 
            'testField', 
            __( 'A test field' ), 
            [ 
                'defaultValue' => $this->getField( 'testField' )
            ]
        )
    ];
}

//in your template:
echo $column->getField( 'testField' );
```

We've added one field called <ins>testField</ins> and once the user is done editting the column and closes the lightbox, the data entered in the <ins>testField</ins> textfield gets saved under the name 'testField', so we can retrieve it by using the <ins>getField()</ins> function in your custom column.

---

## Custom sanitization

Now I hear you saying that you need more control over what eventually get's saved! You need to make sure a string entered is actually a string, or a number being entered is higher than zero. I totally get you. Each column can sanitize their input via the <ins>santizeProperties()</ins> function, which get's called right before the data is saved:

```php

    /**
	 * Creates the right values to save
	 * 
	 * @return array
	 */
	public function sanitizeProperties( $props )
	{
        if( isset( $props['testField'] ) ){

            $props['testField'] = (string)$props['testField']; //cast to a string

            if( $props['testField'] == '' ){
                //throw an error if we see an empty string:
                $this->addError( __( 'No empty string allowed for "test field" ' ) );
                unset( $props['testField'] ); // make sure this field doesn't get saved.
            }

        }

		return $props;
    }
```

In this case we're taking our testField and making sure an actual string get's saved. If the string is empty we throw an error using the column's <ins>addError</ins> function, which will parse an error back to the ligthbox of this column. We also unset the testField from the array, making sure we're not saving non-valid data.

---

### Altering the data after sanitization

After sanitizing the data you have another option to alter the data via a WordPress filter. Consider this example:

```php

add_filter( 'cuisine_sections_save_column_properties', function( $properties, $column ){

    if( $column->type == 'my-custom-column' ){
        if( isset( $properties['startDate'] )  ){
            $properties['startDateTimestamp'] = strtotime( $properties['startDate'] );
        }
    }
    return $properties;
}, 100, 2 );
```
The example above first checks if we're trying to save data for our custom column. It then checks if there's a startDate given (always check this, since the field might not have passed sanitization). If it detects a startDate, it creates a new property (for which we haven't created a field) called 'startDateTimestamp', which saves a copy of the startDate as a unix timestamp.

---

### Before and After column saves

These WordPress action hooks run just before and just after a column gets saved, so you can add additional data or save a subset of column data elsewhere (for example in a custom database table.)

Here's an example, where we save timestamp data to a custom table using [Cuisine's Record class](/core/database/adding-updating):

```php

add_action( 'cuisine_sections_after_column_save', function( $column ){

    global $post;
    $timestamp = $column->getField( 'startDateTimestamp' );
    Record::insert( 'column-timestamps', ['post_id' => $post->ID, 'timestamp' => $timestamp ]);

}, 100, 1 );
```

This takes the <ins>startDateTimestamp</ins> property we've created on the fly and adds that (plus the columns post ID) to a custom database table called "column-timestamps".

---

### Custom save operations

If all else fails, you can always overwrite the <ins>saveProperties()</ins> function that's saving the data. This isn't encouraged, however since there might be problems with backwards compatibility late on..
Here's the <ins>saveProperties()</ins> function from <ins>DefaultColumn</ins>:

```php

/**
 * Save the properties of this column
 * 
 * @return bool
 */
public function saveProperties(){
    
    $props = $_POST['properties'];
    $props = $this->sanitizeProperties( $props ); //sanitize
    $props = apply_filters( 'cuisine_sections_save_column_properties', $props, $this ); //then filter

    do_action( 'cuisine_sections_before_column_save', $this );

    $saved = update_post_meta(
        $this->post_id,
        '_column_props_'.$this->fullId,
        $props
    );


    //set the new properties in this class
    $this->properties = $props;

    do_action( 'cuisine_sections_after_column_save', $this );

    return $saved;
}

```
<br/>

All properties for a column get saved in one serialized array, as you can see here. If you feel the need to save data separately, you can do so here by adding to this function.

<br/>


