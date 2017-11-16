---
title: "Adding sections to your post-types"
categories: 
    - getting-started
url: /sections/getting-started/adding-section-post-types/
---

Adding sections to a custom post-type is quite easy and happends with a filter.
Say you have a post-type called "portfolio", the correct code would be:

```php
//add sections to portfolio
add_filter( 'cuisine_sections_post_types', function( $types ){

	$types[] = 'portfolio';
	return $types;

});
```

---

### Reviving the WordPress Editor for Pages

By default Cuisine Sections will remove the WordPress wysiwyg editor for pages. If you wish to undo this, use this filter:

```php
add_filter( 'cuisine_sections_remove_editor', function( $types ){
		
	unset( $types['page'] );
	return $types;

});
```

---

### Disabeling Cuisine Sections on a per-post basis

To exclude certain posts or pages from a Sections layout, you can add that post's ID to another filter:

```php
add_filter( 'cuisine_sections_dont_load', function( $ids ){
	
	$ids[] = '2'; //exclude sections for the Sample Page
	return $ids;

});
```



