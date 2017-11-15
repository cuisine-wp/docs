---
categories:
- getting-started
date: 2015-08-26T09:33:55Z
order: 2
title: Structure
url: /core/getting-started/structure/
---

Cuisine caries on the event-driven model of WordPress, it's not MVC, so you are completely free to choose your plugin's structure. There are some smart things to take into account, though.

Cuisine is completely namespaced and needs PHP 5.4 as a minimum to operate properly. Everything is Object Oriented and in a propper class. Namespacing largely reflects the folderstructure of the classes:

> Cuisine 
>> Front
>> Route


---


## Wrappers

Regular Cuisine development can make WordPress development look an aweful lot like [Laravel](http://laravel.com/) and that's because of the [Facade Design Patter](https://en.wikipedia.org/wiki/Facade_pattern). 

Cuisine uses wrappers for easy-access to classes and functions. All classes you can use on-the-fly have there own wrapper. To clarify this, look at the next example:

So:
{{< highlight php  >}}

use Cuisine\Wrappers\PostType;

PostType::make( 'project', 'Projects', 'Project' )->set();

{{< / highlight >}}


Actually works the same as the long-form version:
{{< highlight php  >}}

$post_type = new \Cuisine\Utilities\PostType();
$post_type = $post_type->make( 'project', 'Projects', 'Project' );
$post_type->set();

{{< / highlight >}}

---


## EventListeners, Assets & Ajax

The EventListeners, Assets and Ajax classes don't have a wrapper. That's because these class-types fire themselves. They are typically extended by a StaticInstance. Static Instances make fireing this class easy. 

Static Classes where designed for hooking in to WordPress. They don't do any logic themselves though, they just tie WordPress to our neat OOP environment. Here's an example, taken from [Crouton](https://bitbucket.org/chefduweb/crouton), our empty scaffolded plugin:

{{< highlight php  >}}

namespace Crouton\Front;

use \Crouton\Wrappers\StaticInstance;
use \Cuisine\Wrappers\PostType;

class EventListeners extends StaticInstance{

	/**
	 * Init events & vars
	 */
	function __construct(){
		$this->listen();
	}

	/**
	 * Listen for events
	 * 
	 * @return void
	 */
	private function listen(){

		add_action( 'init', function(){
				
			PostType::make( 'project', 'Projects', 'Project' )->set();

		});
	}
}

\Crouton\Front\EventListeners::getInstance();

{{< / highlight >}}

The above example fires itself. Listens to the 'init' hook in WordPress and then triggers the PostType class to create a new PostType instance for us.