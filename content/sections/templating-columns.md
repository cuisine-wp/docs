---
title: "Columns"
categories:
    - templates
url: /sections/templates/columns/
---

Column templates are the most important templates in Cuisine Sections. You'll probably be changing these the most. Columns are also one of the trickier ones to get, since each column-type requires it's own template.

If you haven't yet, [read up on Cuisine Sections template structure & hierarchy](/sections/templates/introduction). They'll help you immensly along the way

---

### Defaults, Overwrites and Filters

The default column templates that Sections provide are all easily stylable. [Most of them are also filterable](/sections/filters/column.html). But since our column templates will be as backwards compatible as possible, you can go ahead and create your custom templates in your theme. We promise not to create the same situations as WooCommerce where you need to update every template you overwrite with every release. 

Still; if we're talking a minor change that can be done using a filter, please choose the filter option as this will likely save you hassle in the future.

---

### Default templates

In Cuisine Sections, all templates can be found in the plugin folder under the following path:

> ** /cuisine-sections/Templates/ **

Each default column will have it's own template file in /columns. Once you open a default template file, notice that every php call to the column happends with the `$column` variable.

This variable will always be available in your templates and it's an instance of the [Column class](/sections/columns/extending.html).

---

### Column template hierarchy

You'll be able to find which files you need to create in your theme by using the [Template Snitch](/sections/templates/introduction.html) explained in the introduction. The template snitch will always follow this hierarchy:

1. /my-theme/columns/{section_name}-{column id}.php
2. /my-theme/columns/{section_name}-{column type}.php
3. /my-theme/columns/{column type}.php

Sections will first be looking at a template for the column with the current ID AND in the current section (you'll be able to alter section-names as an Administrator, [see the Section Template docs](/sections/templates/sections.html)). So in that case it doesn't really matter if you've selected a content column or a video column; the template will always be the same.

Then it'll check the column type inside your named section. This means that if you have two content columns inside a section called `intro`, both columns will respond to the following template:
`/my-theme/columns/intro-content.php`

If this file cannot be found it'll be looking for a general column type template. If all of your video-columns need a custom class, or would like the video title to be removed for instance, you can create
`/my-theme/columns/video.php` and all video-columns will use that file.

---

### Using the Column Class in your template

The column class has a couple of methods you can use in the template to fetch certain column data. Here are some basics, while looking at the template for the video column:

```php
<div itemprop="video" class="column video">

	<?php if( $column->getField( 'title' ) ):?>
		<h2 itemprop="name"><?php echo esc_html( $column->getField( 'title' ) );?></h2>
	<?php endif;?>

	<div class="video-wrapper">
	<?php 

	$still = $column->getField( 'still' );
	if( $still && $still['full'] != '' ){

		$url = $still['full'];

		if( isset( $still['large'] ) && $still['large'] != '' )
			$url = $still['large'];

		echo '<div itemprop="video" style="background-image:url(';
		echo esc_url( $url ).')"'' class="video-still">';
		echo '</div>';

	}

	echo wp_oembed_get( $column->getField( 'url' ) );

	?>
	</div>	
</div>
```

<br/>
In the template above we do a few things. We'll break them down part by part down here:

<br/>

> <ins>if( $column->getField('title') )</ins>

The `getField();` method in a column takes the name of a certain column field, in this case the title. If a title is set, it will return that title, but (much like Advanced Custom Fields) if the title isn't set, it will return false. So <ins>getField()</ins> can be used to fetch and check for column fields.

<br/>

> <ins>$column->getField( 'still' );</ins>

The <ins>still</ins> property of a video column comes from a cuisine image-field, called with <ins>Field::image( 'still' );</ins>. An image field will always store an array of image sizes and an image ID. So the field <ins>still</ins> returns an array, which we then check for certain sizes.

<br/>

The output of each column really depends on the <ins>Field</ins> object applied to it. [You can check out our documentation on creating your own Column type if the default columns don't cut it](/sections/columns/registring.html).

<br/>
