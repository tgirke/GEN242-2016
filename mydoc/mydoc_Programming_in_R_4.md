---
title: Functions
keywords: 
last_updated: Wed Apr 13 16:38:00 2016
---

## Function Overview

A very useful feature of the R environment is the possibility to expand existing functions and to easily write custom functions. In fact, most of the R software can be viewed as a series of R functions.

__Syntax__ to define function

{% highlight r %}
myfct <- function(arg1, arg2, ...) { 
	function_body 
}
{% endhighlight %}
__Syntax__ to call functions

{% highlight r %}
myfct(arg1=..., arg2=...)
{% endhighlight %}
The value returned by a function is the value of the function body, which is usually an unassigned final expression, _e.g._: `return()`

## Function Syntax Rules
	
__General__

* Functions are defined by 
    1. The assignment with the keyword `function`
    2. The declaration of arguments/variables (`arg1, arg2, ...`) 
    3. The definition of operations (`function_body`) that perform computations on the provided arguments. A function name needs to be assigned to call the function.

__Naming__ 

* Function names can be almost anything. However, the usage of names of existing functions should be avoided.
	
__Arguments__ 

* It is often useful to provide default values for arguments (_e.g._: `arg1=1:10`). This way they don't need to be provided in a function call. The argument list can also be left empty (`myfct <- function() { fct_body }`) when a function is expected to return always the same value(s). The argument `...` can be used to allow one function to pass on argument settings to another.

__Body__

* The actual expressions (commands/operations) are defined in the function body which should be enclosed by braces. The individual commands are separated by semicolons or new lines (preferred).

__Usage__ 

* Functions are called by their name followed by parentheses containing possible argument names. Empty parenthesis after the function name will result in an error message when a function requires certain arguments to be provided by the user. The function name alone will print the definition of a function.

__Scope__

* Variables created inside a function exist only for the life time of a function. Thus, they are not accessible outside of the function. To force variables in functions to exist globally, one can use the double assignment operator: `<<-` 

## Examples

__Define sample function__


{% highlight r %}
myfct <- function(x1, x2=5) { 
	z1 <- x1 / x1
	z2 <- x2 * x2
        myvec <- c(z1, z2) 
        return(myvec)
} 
{% endhighlight %}

__Function usage__


Apply function to values 2 and 5

{% highlight r %}
myfct(x1=2, x2=5) 
{% endhighlight %}

{% highlight txt %}
## [1]  1 25
{% endhighlight %}

Run without argument names

{% highlight r %}
myfct(2, 5) 
{% endhighlight %}

{% highlight txt %}
## [1]  1 25
{% endhighlight %}

Makes use of default value '5'

{% highlight r %}
myfct(x1=2) 
{% endhighlight %}

{% highlight txt %}
## [1]  1 25
{% endhighlight %}
Print function definition (often unintended) 

{% highlight r %}
myfct 
{% endhighlight %}

{% highlight txt %}
## function(x1, x2=5) { 
## 	z1 <- x1 / x1
## 	z2 <- x2 * x2
##         myvec <- c(z1, z2) 
##         return(myvec)
## }
{% endhighlight %}

