---
categories:
- post-types-taxonomies
date: 2015-08-26T09:34:26Z
order: 1
title: Creating Post Types
url: /core/post-types-taxonomies/creating-post-types/
---

Post Types are one of the reasons WordPress can call itself a full-fledged CMS, so creating post types should be damn easy right? Well, regular WordPress gives you a LOT of options when registering a Post Type. When usually you're okay with just passing the slug, the singular label and the plural label. With Cuisine you can do just that, without having to dive into the [codex page](https://codex.wordpress.org/Function_Reference/register_post_type) everytime.


The PostType class is available through [Cuisine's Wrapper System](/core/getting-started/structure), so you can start using it by adding

`use Cuisine\Wrappers\PostType`

to the top of your php-document.

---

### Registering


Here is an example:

{{< highlight php  >}}

PostType::make( 'project', 'Projects', 'Project' )->set();

{{< / highlight >}}  

<br/>

Let's break that down:

>**PostType::make()** is the function we use to prop up our Post Type. **set()** actually registers it with WordPress.<br/><br/>
>
>The parameters passed down to the make-function are, in order of appearence:
>
>*  **slug**
>   The slug represents both the ID and what will be used in urls for this post type.
>
>*  **plural label**
>   Both labels are used in the backend mostly. This is the plural form.
>
>*  **singular label**
>   Two projects, one project.

---

### Fine-grained control

If you still need to get into the nitty-gritty stuff, we've got you covered. The **set()** function at the end of our last example is used for passing additional arguments. Here's an example:

<br/>

{{< highlight php  >}}

$args = array(
	'labels'			 => $labels
	'description'        => __( 'Description.', 'your-plugin-textdomain' ),
	'public'             => true,
	'publicly_queryable' => true,
	'show_ui'            => true,
	'show_in_menu'       => true,
	'query_var'          => true,
	'rewrite'            => array( 'slug' => 'book' ),
	'capability_type'    => 'post',
	'has_archive'        => true,
	'hierarchical'       => false,
	'menu_position'      => null,
	'supports'           => array( 'title', 'editor', 'author', 'thumbnail', 'excerpt', 'comments' )
);


PostType::make( 'project', 'Projects', 'Project' )->set( $args );


{{< / highlight >}}

See the [WordPress Codex](https://codex.wordpress.org/Function_Reference/register_post_type) for more information on which arguments to pass.

The defaults to the arguments taken by the **set()** function are the exact same as regular WordPress with two notable exeptions:

* The labels array gets created with the use of the singular and plural labels you've passed in the **make()** function.

* The rewrite value gets set to the slug you've passed in the **make()** function.



