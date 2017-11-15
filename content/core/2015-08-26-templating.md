---
categories:
- post-types-taxonomies
date: 2015-08-26T09:34:47Z
order: 4
title: Templating
url: /core/post-types-taxonomies/templating/
---

Templating in Cuisine means routing a certain post-type to a template-file. Therefor it's done by the routing class. You can also use the routing class to route to a specific URL. 

On this page we'll be looking into routing to a template. If you're looking to route your post type to a certain URL [check out the page on URL-routing](/core/post-types-taxonomies/routing.html).

The Route-class is available through [Cuisine's Wrapper System](/core/getting-started/structure.html), so you can start using it by adding

`use Cuisine\Wrappers\Route`

to the top of your php-document.

---

### The Cuisine Template Engine

Cuisine changes the default template hierachy and makes it a bit simpeler. It looks for the following files, in order of priority:

For singular posts and pages:

1. **{post_type}-{slug}.php** ( page-about-us.php )
2. **{post_type}.php** ( page.php )
3. **detail.php**

And for overview pages:

1. **{plural post-type label}.php** ( projects.php )
2. **overview.php** 


<br/>

####Location of template files

> **Very Important:** Cuisine looks for templates in your theme's /templates folder. You can change this using the **cuisine_template_location** filter. 
>
> See below for an example.


{{< highlight php  >}}
	
add_filter( 'cuisine_template_location', function( $location ){
	
	return 'my-template-folder/'; //this needs a trailing slash

});

{{< / highlight >}}

<br/>

**We recommend using Cuisine with it's empty starter-theme Carte Blanche**. It features a clear and Cuisine-ready folder structure. Out-of-the-box support for RequireJS and the Sass-asset pipeline and more good stuff you'll be happy about. [To learn more about using Cuisine and Carte Blanche together check our documentation page about it](/core/theme/carte-blanche.html).

<br/>

### Routing to a Template

Routing post types to templates is done by using the WordPress [template_include filter](https://codex.wordpress.org/Plugin_API/Filter_Reference/template_include). This is considered best practise over using the [template_redirect hook](https://codex.wordpress.org/Plugin_API/Action_Reference/template_redirect). All your registered templates will first be tested on existence and after that follow the regular WordPress theme hierarchy.


So, following our example of [the project-post type](/core/post-types-taxonomies/creating-post-types.html), we'll create a route for our post type **project**. We'll want the overview page to be named __/our-work__ and an single project can route to __/project/project-name__.

<br/>

{{< highlight php  >}}

Route::url( 'project', 'our-work.php', 'project.php' );

{{< / highlight >}}

<br/>

That's it. Here's the breakdown for the example above:

>The parameters passed down to the make-function are, in order of appearence:
>
>*  **post type slug**
>   The slug of the post-type we're routing this template to.
>
>*  **overview template-name**
>   Name of the template file for an archive or overview
>
>*  **singular slug** (optional)
>   Name of the template file for a single post page.
