---
layout: post
title:  "Swift - Day 3 : Exception handling"
tags:
  - programming
  - ios
  - swift
  
hero: "assets/img/ricardo-gomez-angel-KmKZV8pso-s-unsplash.png"
overlay:  green
published: true

---

Though there's nothing exceptionally new to me about how Swift deals with exceptions, I do have to say that I prefer it's way of dealing with functions that throw an error. I find them to be easier to read compared to languages like java.
<!–-break-–>

Suppose we have a function `canThrow()` which may throw as shown below.

{% highlight swift %}  
    func canThrow() throws {
    	//Some logic that may result in an error
    }
{% endhighlight %}

What I like about Swift is the way the function is called in a different part of the code that handles/catches the error.
{% highlight swift %}  
    do {
    	try canThrow()
    	someOtherSafeFunction()
    
    } catch SomeError.happened {
    	dealWithIt()
    }
{% endhighlight %}

By having try before the function that could potentially throw an error,it is clear to anyone reading the code where an exception may come from.
