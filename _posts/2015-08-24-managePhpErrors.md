---
title: "Handle PHP errors"
layout: post
---

# Manage php errors

## DISCLAIMER

This document is only a small useful collection of codes and articles to help PHP error handling.

from [http://www.theodo.fr/blog/2014/04/manage-php-errors-and-exceptions-in-your-project/](http://www.theodo.fr/blog/2014/04/manage-php-errors-and-exceptions-in-your-project/)


## When does “error” occur?

Despite the introduction of exceptions, errors are still here and continue to appear (I don’t mean that exceptions should replace errors)… Try something like this:

	//lang php

	$foo = [bar];
	echo $foo;

Notice that quotes are missing in the array key: I should have written ['bar']. This produces the following error:

	PHP Notice:  Array to string conversion[…]

Common errors include:

* parsing errors: missing parenthesis, braces, semi-column…
* type conversion errors
* memory allocation errors

Generally errors occur at the language level like when the syntax is wrong, some actions over variables are invalid.

## Error reporting level

Depending on the gravity of the error, your code can continue to run until the end or will stop. You can configure error reporting in PHP to ignore minor errors but I would recommend you to report as many errors as possible while developing. To configure the error reporting level you will use constants and bitwise operators which are not easy to apprehend. For example, to remove the notice from the previous piece of code you would do the following:

	//lang php

	error_reporting(E_ALL & ~E_NOTICE); // or simply error_reporting(~E_NOTICE);
	$foo = ["bar"];
	echo $foo;

If you want to know what your current error reporting value is, use the error_reporting() function without any arguments.

## Trigger errors manually

Errors can also be manually raised. For example, if you want to deprecate a function and warn the developer that this function will be removed in the next release, then you would do something like this:

	//lang php

	/**
	 * Returns the addition of to integer
	 *
	 * @deprecated This function will be removed in the release 0.2, you should use the add function instead
	 * @param integer $a
	 * @param integer $b
	 * @return integer
	 */
	function calculate($a, $b)
	{
	    trigger_error("This function will be removed in the release 0.2, you should use the add function instead" ,E_USER_DEPRECATED);

	    return add($a, $b);
	}

	/**
	 * @param integer $a
	 * @param integer $b
	 * @return integer
	 */
	function add($a, $b)
	{
	    return $a  $b;
	}

As you can see the function add($a, $b) has been added, for more clarity I guess. So the calculate($a, $b) triggers an error E_DEPRECATED, which, with the default PHP configuration, does not stop the execution of the script, and calls the add() function.

When the script calls the calculate function, the deprecation message is displayed:

	PHP Deprecated:  This function will be removed in the release 0.2, you should use the add function instead

## Handling errors

By default errors will be output right after it has been triggered or after the execution of the script. However, you can catch it and do things by defining and registering an error handler.

	set_error_handler(function ($errno, $errstr, $errfile, $errline, $errcontext) {
	    echo "\n Have a nice day\n";

	    exit(1);
	});
	echo calculate(2, 3);
	exit(0);

In this example we reuse the previous calculate function that triggers a E_USER_DEPRECATED error. We set the closure as the error handler that will be called whenever an error occurs.
As you have already guessed this closure will print “Have a nice day” and exit with the code 1, meaning that the script ended with a problem.

	benjamin@comp : ~/ $ php error-test.php

	Have a nice day


### catch fatal error

[source](http://stackoverflow.com/questions/277224/how-do-i-catch-a-php-fatal-error)

	register_shutdown_function('shutdownFunction');

	function shutDownFunction() {
	    $error = error_get_last();
	    // fatal error, E_ERROR === 1
	    if ($error['type'] === E_ERROR) {
	        //do your stuff
	    }
	}
