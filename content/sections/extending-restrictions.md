---
category:
    - extending
title: "Restricting views and column types"
date:  2017-11-20T10:17:50+01:00
weight: 5
url: /sections/extending/restrictions/
---

The interface of Sections is already as cleaned up as we can make it. By restricting the possibilities of a user to a minimum, we reduce the learning-curve and the possibilities for errors. Further restrictions, however, are completely possible. Even on a section-by-section basis. 

---

## Restricting view types.

Apart from [creating your own section view-types](/sections/extending/views/), you can also restrict the views that a user can use. Using the following filter:

`cuisine_sections_default_allowed_views`

you are able to completely control which views are allowed where. Consider this example:

```php

add_filter( 'cuisine_sections_default_allowed_views', function( $allowed, $section ){

    if( $section->view == 'content' && User::hasRole( 'administrator' ) == false ){
        unset( $allowed['three-columns'] );
        unset( $allowed['four-columns'] );
    }

    return $allowed;
}, 100, 2 );
```

This example removes two default view-types (namely the three-column and the four-column view) when the user doesn't have the role 'administrator' and we're dealing with a regular content section. In this filter the second parameter is the <ins>$section</ins> object.

---

## Restricting column types

Sometimes you don't want your user to be able to add columns of a certain type. If, for instance, you have an 'add to cart' column, like our Cart plugin does. You'd want to restrict it to the product post-type, since pages and other post types aren't really welcome in your cart :).
Well, using the following filter:

`cuisine_sections_default_allowed_columns`

you are able to do just that. Let's look at an example:

```php

add_filter( 'cuisine_sections_default_allowed_columns', function( $allowed, $column, $section ){

    $postId = $column->post_id;
    $postType = get_post_type( $postId );

    if( $postType !== 'product' && $section->position !== 1 ){
        unset( $allowed['add-to-cart'] );
    }

    return $allowed;
}, 100, 3 );
```
In this example we do exactly what we've mentioned before: we check if the post-type of this column's post is "product". If that isn't the case; the 'add-to-cart' column isn't allowed as a valid choice. 

In this example we also check if we're dealing with the very first section on the page. Meaning that we want to restrict the "add to cart" column to the first section of a product, because we want the add-to-cart button to be easy to find for our customers. 