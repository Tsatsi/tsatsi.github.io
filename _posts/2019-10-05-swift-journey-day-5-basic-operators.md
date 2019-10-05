---
layout: post
title:  "Swift - Day 6 : Basic operators"
tags:
  - programming
  - ios
  - swift
  
hero: "assets/img/clem-onojeghuo-H-82Nbe8m7o-unsplash.png"
overlay:  red
published: true

---

Swift's operators are mostly similar to that of common programming languages, but there were a few that stood out for me which I thought I should write about today.
<!–-break-–>

## Nil-Coalescing Operator

The simplicity of this operator really stood to me and it is one that I suspect I will be using a lot considering that Swift uses optionals which often require checking whether a value is a nil or not. The Nil-coalescing operator does this in a much cleaner way.

Instead of checking and assigning a default value like below
{% highlight swift %}  
    myOptional ! = nil ? myOptional! : alternativeValue
{% endhighlight %}

Nil coalescing has a cleaner way which is
{% highlight swift %}  
    myOptional ?? alternativeValue
{% endhighlight %}

## Range Operators

Range operators are common in other languages, I'm writing about them because I tend to mix them up, but I'm certain this will improve the more I use them.

### Closed Range operator

`(a...b)` This defines a range that runs from **a** to **b**, and includes both **a** and **b**.
{% highlight swift %}  
    for index in 1..3 {
    	print("\(index) times 10 is \(index * 10) "
    }
    
    //1 times 10 is 10
    //2 times 10 is 20
    //3 times 10 is 30
{% endhighlight %}

### Half-open range operator

`(a..<b)` This defines a range that starts and includes **a** but doesn't include **b** that's why it's said to be half open.
{% highlight swift %}  
    let rugbyGroups = ["pool-a", "pool-b", "pool-c", "pool-d"]
    let count = rugbyGroups.count
    
    for i in 0..<count {
    	print("Pool \(i + 1) is called \(rugbyGroups[i])")
    }
    
    //Pool 1 is called pool-a
    //Pool 2 is called pool-b
    //Pool 3 is called pool-c
    //Pool 4 is called pool-d
{% endhighlight %}

### One-Sided Ranges

`(a...)` defines a range that starts from **a** and continues as far as possible and `(...b)` defines a range that starts as far as possible until **b.** This is called a one-sided range because the range has a value on one side.
{% highlight swift %}  
    for group in rugbyGroups[2...] {
    	print(group)
    }
    //pool-c
    //pool-d
{% endhighlight %}

`(..<b)` defines a range that starts from as far as possible and ends at **b** but without including it. This is a half-open one-side operator.
{% highlight swift %}  
    for group in rugbyGroups[..<2] {
    	print(group)
    }
    //pool-a
    //pool-b
{% endhighlight %}

## Conclusion

Most of the operators in Swift work similar to how operators work in languages like Java and C#, this are a few that stood out for me when learning Basic operators in swift.
