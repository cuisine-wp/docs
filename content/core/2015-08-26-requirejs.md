---
categories:
- assets
date: 2015-08-26T09:35:49Z
order: 2
title: RequireJS
url: /core/assets/requirejs/
---

**The problem:**<br/>
Cuisine believes in a clean and uncluttered frontend. A big part in this philosophy is how we work with Javascript. In the regular WordPress-way you'd register a script and it's dependencies in one line of php. It then gets added to the code in the documents' \<head\> or after the footer. This means all files get added as loose dependencies and all get loaded seperately. This is a good way to work with plugins where lots of different functionalities need lots of different scripts to actually work.

The big problem in this approach is that it produces a lot of non-asychronious http-request which tend to slow down browser-rendering. This is a real waste... especially if a plugin loads scripts that it doesn't need on the current page.

---

##Enter RequireJS
With RequireJS you can asynchroniously load new scripts for you. This means the browser render time won't be affected and you still get the full flexibility of being able to work with a lot of files and plugins.

Registering scripts for use can be done in either PHP (from where the also can be autoloaded) and Javascript itself. Thats right; you can even load them on-the-fly in Javascript. Consider this example:

{{< highlight javascript  >}}
	
var _element = document.getElementById( "#gallery-nav" );
if( _element ){

	require(['flickity-as-nav-for'], function( Flickity ){

		var _flickityNav = new Flickity({
			asNavFor: '.gallery-main',
			...
		});

	});
}

{{< / highlight >}}
<br/>
In the example set above, we first check if the element **\#gallery-nav** can be found. If that's the case we load a special [Flickity](http://flickity.metafizzy.co/) module, which we send up once the load is complete.


---

##Loading dependencies

In WordPress we register our scripts with the [Script class](/core/assets/script) like so:

> Script::register( 'script_id', '/my-plugin/script_url', true );

The last variable in that functioncall is wether or not to autoload this file at render time. You can read more about it in the [Script class docs](/core/assets/script).

In RequireJS each dependency is stated at the start of a document, like we would in PHP when we use **use namespace\Class**. Here's an example:

{{< highlight javascript  >}}

require( 
	['jquery', 'flickity'], 
	function( $, Flickity ){

		//I can use both jQuery and Flickity here...

	}
);

{{< / highlight >}}
<br/>
As you can see both jQuery and Flickity are loaded as dependencies using the **require()** function.

---

##Things to take into account

RequireJs works with the idea that every module you load returns itself as a Javascript object. That's why you get to use both jQuery and Flickity in the example mentioned above. 

Obviously not every third-party library returns itself so how would we go about using third-party scripts without losing updatability? RequireJS has something for this called the a Shim.

A Shim is basically a wrapper created on-the-fly to deal with non-returning vendor files. Creating one is pretty easy in Cuisine:


{{< highlight php  >}}

Script::shim( 
	'my-wrapper',
	'MyWrapper',
	array(
		'jQuery',
		'backbone'
	)
);

{{< / highlight >}}
<br/>
Let's look at this parameter by parameter shall we?
> 
>* 	**Slug**<br/>
>	The slug of the script we're creating a Wrapper for
>
>*	**Exports**<br/>
>	The name of the variable this shim exports
>
>*	**Dependencies**<br/>
>	All slugs of the dependencies needed

If you like more information on how shims work, I encourage you to [checkout there docs.](http://requirejs.org/docs/api.html#config-shim)

> For more on RequireJS take a look at [their documentation](http://requirejs.org/docs/api)

