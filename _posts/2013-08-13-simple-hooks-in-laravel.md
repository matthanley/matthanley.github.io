---

layout:			default
title:  		Simple Hooks in Laravel 3
type:			post
navigation: 	false

date:   		2013-08-13
excerpt: 		Delay function calls in Laravel
gradient: 		5
image: 			header-3.jpg
details:		false

author: 		Matt Hanley
bio: 			"Yup, <i>that</i> guy."
twitter: 		"https://twitter.com/_matthanley"

---

### The Scenario

Building a laravel project with dynamically loaded bundles, I found myself with the need to delay execution of a function until all bundles were loaded (in this particular example, building the navigation for a bundle which changes depending on the features of other loaded bundles). WordPress uses Hooks to accomplish this: we register a function with the hook, and it's executed when the hook is called.

### The Solution

An _incredibly_ simple solution: the Hook class.

Simply paste the below into application/libraries/hook.php

{% highlight php %}
<?php

class Hook {

	/*
		Written by Matt Hanley. Copyright 2013. www.mjh.mx
		Usage:

		Hook::name(); // Run the hook

		Hook::name(function() { // Add a function by closure
			doSomething();
		}, (array) $parameters);

		Hook::name('functionName', (array) $parameters); // Add a reference to a function

	*/

	private static $hooks = array();

	public static function __callStatic($method, $parameters)
	{
		if (count($parameters)) {
			// We're adding a method
			$function = array_shift($parameters);
			$parameters = count($parameters) ? $parameters[0] : array();
			static::addHook($method, $function, $parameters);
		} else {
			// We're calling a hook. Run it.
			return static::run($method);
		}
	}

	private static function addHook($name, $function, $parameters) {
		// init
		Log::hook('Adding: '.$name);
		if (!isset(self::$hooks[$name])) {
			self::$hooks[$name] = array();
		}
		self::$hooks[$name][] = array($function, $parameters);
		Log::hook('Added '.$name);
	}

	private static function run($name) {
		// Run hook $name
		Log::hook('Running '.$name);
		if (!is_array(self::$hooks)) {
			Log::hook('&gt;&gt; Failed. No hooks defined!');
		} elseif (array_key_exists($name, self::$hooks)) {
			foreach (self::$hooks[$name] as $hook) {
				if (is_callable($hook[0])) {
					call_user_func_array($hook[0], $hook[1]);
				}
			}
			return true;
		} else {
			Log::hook('Hook '.$name.' not defined!');
		}
		return false;
	}

}
{% endhighlight %}

### Usage

Easy -

Call a hook called `hookname`:

{% highlight php %}
Hook::hookname();
{% endhighlight %}

Add a predefined function `functionname` with an array of parameters to run on the `hookname` hook:

{% highlight php %}
Hook::hookname('functionname', array('parameter1',$parameter2));
{% endhighlight %}

Add a closure to be run on the `hookname` hook:

{% highlight php %}
Hook::hookname(function($text) {
  echo $text;
}, array('Hello World!'));
{% endhighlight %}

Note that this is not necessarily Laravel-specific. To use in any PHP application, simply remove all of the `Log::` lines in the above and make sure you load the class before you try calling it.