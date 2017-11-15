---
categories:
- post-types-taxonomies
date: 2015-08-26T09:34:34Z
order: 2
title: Creating Taxonomies
url: /core/post-types-taxonomies/creating-taxonomies/
---

Like post types, taxonomies are extremely important to WordPress development. It's so sad that registering a simple taxonomy needs more that one line of code. So, just like [Post Types in Cuisine](/core/post-types-taxonomies/creating-post-types.html), Taxonomies have been made a lot simpeler.

The Taxonomy-class is available through [Cuisine's Wrapper System](/core/getting-started/structure.html), so you can start using it by adding

`use Cuisine\Wrappers\Taxonomy`

to the top of your php-document.


---

###Registering 

Say we have a post type called **project** and we want to add a **Client** taxonomy to it, so we can easily sort our portfolio.. Well, then we just use this one line of code:

{{< highlight php  >}}

Taxonomy::make( 'client', 'project', 'Clients', 'Client' )->set();

{{< / highlight >}}  

<br/>

Let's dive into this a little more:

>**Taxonomy::make()** is the function we use to prop up our taxonomy. **set()** actually registers it with WordPress.<br/><br/>
>
>The parameters passed down to the make-function are, in order of appearence:
>
>*  **slug**
>   The slug represents both the ID and what will be used in urls for this taxonomy.
>
>*  **post type slug**
>   The slug of the post-type we're tying this taxonomy to. This can be an array of post-type slugs as well.
>
>*  **plural label**
>   The plural label for this taxonomy
>
>*  **singular label**
>   The singular label for this taxonomy

---

### Fine-grained control

If you need to pass aditional arguments for this taxonomy, you can do so in the **set()** function: 

<br/>

{{< highlight php  >}}

$args = array(
	'hierarchical'          => false,
	'labels'                => $labels,
	'show_ui'               => true,
	'show_admin_column'     => true,
	'query_var'             => true
);

Taxonomy::make( 'client', 'project', 'Clients', 'Client' )->set( $args );


{{< / highlight >}}


