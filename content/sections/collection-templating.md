---
category:
    - templating
title: "Collection Templating"
date:  2017-11-20T10:17:50+01:00
weight: 5
url: /sections/templating/collections/
---

**Fair warning:** This might be a bit complicated. We have two types of collections in Sections. One is a collection of section; it's a helper object which can sort and fetch sections for us. But in this case we're talking about a <ins>Collection Column</ins>. 

---

## Collection Column

Templating a Collection Column works just like [templating a regular column](/sections/templating/columns/). With a few differences: 

#### 1. A collection column uses a lot more logic
Loops in WordPress can get pretty complex. Especially when you add stuff like pagination, multiple rows of blocks, etc. So a collection-column template currently contains more logic then one would expect in a template. This makes it harder to extend when we also need to take backwards compatibility into account. If you can, also [try and use a filter](/sections/templating/filters/#collections) to solve your problem.

#### 2. It contains element-templates
Collections usually contain other templates. One of those template-types is a block, which we'll get to later. For now; also note that there will be seperate "element"-type templates for Pagination or the Autoloader. [You can read up on these templates over at the "Templating Elements" page](/sections/templating/elements/)


#### 3. It contains blocks.
Post type blocks are the templates that get loaded when we create a collection column. The collection will query a certain post-type (or multiple post-types) and loop through them. 
With each iteration it will load a post-type block, dependant on which post-type is currently in the loop.

---

## The post-type block template

A post type block will usually consist of a link, title, post thumbnail, post date and an excerpt. You can obviously make this as big as you would want. The point being that a single blog post on a single url probably will look vastly different than that post in an overview. 

The hierarchy for these templates looks like this:

> Section > Collection-column > Post-type block

A post type block template will always look at your theme like this:

<ins>/my-theme/collections/blocks/{post_type slug}.php</ins>

So if you're creating a block for a regular post, do so like this:

<ins>/my-theme/blocks/post.php</ins>
```php
<a href="<?php the_permalink();?>" class="post">
	<h2><?php the_title();?></h2>
	<?php the_post_thumbnail();?>	
</a>
```
This example creates a link per post and displays the post's title and thumbnail.