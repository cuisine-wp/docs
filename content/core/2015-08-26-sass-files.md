---
categories:
- assets
date: 2015-08-26T09:36:06Z
order: 1
title: Sass Files
url: /core/assets/sass-files/
---

Cuisine believes that delivering a clean and uncluttered frontend means, amongst other things, unifying and concatinating CSS. If you don't know why that's an important step, [please read Yoast's advice on it](https://yoast.com/reduce-http-requests-wordpress/).

Cuisine, and it's themes do this by leveraging the power of [Sass](http://sass-lang.com/). A tool which makes it easier to write and maintain stylesheets, but also combine 'em.

> In these docs you will mostly find how to register a Sass file with Cuisine.
> It is intended for Cuisine plugin developers, because themes can just 
> create Sass-file on there own.
>
> If you are not yet familiar with working with Sass we encourage you to
> [check out the docs on Sass in our theme section](https://doc.chefduweb.nl/themes/sass).

---

## Including the Sass Class

The Sass class is available through [Cuisine's Wrapper System](/core/getting-started/structure.html), so you can start using it by adding

> **use Cuisine\Wrappers\Sass**

to the top of your php-document.

---

## Registering a Sass file

Registering a Sass file in Cuisine is pretty easy:

{{< highlight php  >}}
	
$url = 'plugin-folder/Assets/sass/';
Sass::register( 'my-sass-file', $url.'_sass', false );

{{< / highlight >}}

<br/>

This function does a few things:

* Checks if this file is already registered with Cuisine
* If that's not the case, copies it to the destined Sass folder (more on this below )
* Updates the Sass registry to make sure this file doesn't get copied on every request.


Okay, so let's see what's going on in the **Sass::register()** function. Let's look at it's parameters in order of appearance:

> 
>* 	**Theme filename**<br/>
>	'my-sass-file' is what the new sass-file on the theme-side will be called.
>	It's also the name Cuisine will save in it's sass-registry
>
>*	**Path**<br/>
>	This is the path to your plugin's "origin" sass-file.  
>
>*	**Auto reload**<br/>
>	Be careful with this boolean: the default is set to false, but once this
>	is set to true, Cuisine will bypass the Sass registry and just keep 
>	copying this file to the theme directory on every request.
>	<br/>This can be handy for development, but it's not meant to be used in
>	a production environment.

---

## Compiling & Theme location of your sass files.

Sass isn't compiled by Cuisine. There are javascript taskrunners or pieces of software available that are infinitely better at this. In the [Sass section on our theme-docs](https://docs.chefduweb.nl/themes/sass) you can find a list of compile options.

By default Cuisine will try and put your plugin's Sass file in the following theme directory:

> **my-theme/assets/src/sass/plugins** 

You can easily change this with a filter:

{{< highlight php  >}}

add_filter( 'cuisine_sass_folder', function(){
	return 'css/sass/plugins/';
});

{{< / highlight >}}

<br/>
In the example Cuisine will place all sass-files that get registered in the following directory:

> **my-theme/css/sass/plugins/**

---

## Refreshing files

Okay, so what if you've made a mistake in your plugins sass file but the file your theme is working with is already registered? How do we make sure the plugin sass file is the latest being used?

The third parameter passed to the **Sass::register()** function can help you in forcing an auto reload ( see the registration section above ). This automatically copies the sass file to the theme directory in __every request__. 

If you'd like a more pragmatic option, you can use the [WP CLI](https://wp-cli.org/) command to refresh all sass files:

> **wp cuisine sass --refresh**

You can find more info on this and other WP CLI commands available in Cuisine in our [WP CLI section](/core/utilities/wp-cli).

If you don't use WP CLI there's a third option to refresh the registry of sass-files in cuisine. Just look up the _registered\_sass\_files_ option in the WordPress options databasetable and delete that record. Now, on a page-refresh, all your sass-files will be renewed.


