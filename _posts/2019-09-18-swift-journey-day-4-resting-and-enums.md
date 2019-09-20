---
layout: post
title:  "Swift - Day 4 : Resting and Enums"
tags:
  - programming
  - ios
  - swift
  
hero: "assets/img/nathan-dumlao-unGA1qBecwg-unsplash.png"
overlay:  blue
published: true

---

Today was a reminder of the importance of taking time to rest. Not having enough sleep finally caught up with me and impeded my productivity during the day. So I'm going to catchup on some sleep but before I do, here's what I've learned about swift's enums.
<!–-break-–>

## Enums

Enumerations in Swift define a common type for a group of related values. Unlike other languages enumerations in Swift don't have to provide a value for each case. The case keyword is used to define new enumeration cases.
{% highlight swift %}  
    enum Direction {
    	case left
    	case right
    	case forward
    	case backward
    }
    // Enum type is inferred
    var characterDirection = Direction.right
    characterDirection = .forward
{% endhighlight %}

An enumeration name has to start with a capital letter as shown above. The type of enum is inferred on initialisation and can be passed a shorter syntax `.forward` once declared.

## Associated value

It is sometimes valuable to store variables or types within  this enums to use later. This is what associated values are used for.
{% highlight swift %}  
    enum ApiError: Error {
    	case requestFailed
    	case responseUnsuccessful(statusCode: Int)
    }
{% endhighlight %}

## Matching enumerations

One of the things I like about swift enumerations is how they are matched. Suppose we have a function that has an Enum as a parameter.
{% highlight swift %}  
    func move(direction:Direction) {
    		switch direction {
    			case .left:
    				print("move left")
    			case .right:
    				print("move right")
    			case .forward:
    				print("move forward")
    			case .backward:
    				print("move backward")
    		}
    }
    
    move(.forward)
{% endhighlight %}

When the function is called and the argument is passed we simply pass it as `.forward` instead of having to pass it as `Direction.forward`.