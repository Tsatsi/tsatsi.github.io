---
layout: post
title:  "Swift - Day 2 : Constants, variables & types"
tags:
  - programming
  - ios
  - swift
  
hero: "assets/img/sonny-ravesteijn-xyxjKdpUg4I-unsplash.png"
overlay: red
published: true

---
Understanding how a language handles data is essential to using it in practice. So I thought this would be the best place for me to start. Swift uses variables and constants to store values of a particular type. Values stored in constants can't be changed whereas variables can be changed or mutated.
<!–-break-–>

Type annotations can be used for clarity when declaring variables. However, this is not necessary if a variable has an initial value because Swift uses **Type Inference** to determine what type a variable or constant is based on the assigned value.
{% highlight swift %}  
    //exampleConstant cannot be changed
    let exampleConstant = 30 //exampleConstant will be inferred as a type Integer
    //exampleVariableInferred value is inferred but can only be changed to inferred type
    let exampleVariableInferred = "This should should accept text"
    //exampleVariable can be changed var exampleVariable:Int //exampleVariable is annotated as an Integer and will only store this type
{% endhighlight %}

# Type Safety

One of the benefits of a **type safe** language  like swift is that you cannot assign the wrong type of values by mistake. In the code snippet above Type inference ensures that `exampleVariableInferred` can only be assigned values of type String.

# Type conversions

Most of swift's types are what you would expect from a typed language. Although it has different integer types(`UInt8, UInt16`) using the general-purpose `Int` type should be enough for most cases. Casting or type conversions can be done as shown in the code snippet below.

{% highlight swift %}  
    let numberInString = "2"
    let integerFromString = Int(numberInString)
    let doubleNumber = 0.05
    let results = Double(integerFromString!) + doubleNumber
    let resultsAsString = String(results)
{% endhighlight %}

# What stood out

What stood out for me when first learning about this topic were type aliases, tuples and optionals. I've used tuples before in python but type aliases and optionals were new to me.

## Type alias

This enables defining a type with an alternative name. I haven't thought of a good use case for this yet, but I found it interesting that this is possible. If you have a background in C or C++ this is probably not new to you.

`typealias MyType = String`

## Tuples

This are values grouped into a compound values similar to a list and can be of mixture of any type. Here is a good example from Swift's documentation.

{% highlight swift %}  
    let http404Error = (404, "Not found")
    // http404Error is of type (Int, String), and equals (404, "Not Found")
{% endhighlight %}

## Optionals

In my opinion optionals take **null safety** to a new level. They are used in cases where a value may be nil. An optional either has a value or doesn't. In  order to get an optional's value you unwrap it and this is where the null safety is. By unwrapping you have to consider what would happen if the expected result is null. What's also great is how optionals can be inferred from the initialisation of values that may be null.

{% highlight swift %}  
    let enteredAge = "30"
    //age is inferred as an optional
    let age = Int(enteredAge)
    //middle is declared as an optional type String
    var middleName:String?
    let enteredAge = "30"
    //age is inferred as an optional
    let age = Int(enteredAge)
    //middle is declared as an optional type String
    var middleName:String?
{% endhighlight %}

In the case above `age` is an optional because it is possible that the conversion of the `enteredAge` to an Int may fail. It is also possible to declare a variable as an optional using type annotations. In the above middleName is set to nil.

### Optional binding

This is used to check if an optional contains a value and if it does to take that value and use it as a variable or constant. The first example would be written as shown below with optional binding.

{% highlight swift %}  
    let numberInString = "2"
    let doubleNumber = 0.05

    if let integerFromString = Int(numberInString) {
        let results = Double(integerFromString) + doubleNumber
        print(results)
    }
{% endhighlight %}

It is worth noting that `integerFromString` will only be available within the scope of the if let statement in the example above. Constants and variables created with optional binding are only available within the body of the if statement.

### Implicitly unwrapping optionals

Sometimes it is clear from the programs structure that an optional will have a value. In such cases it is best to implicitly unwrap the optional using the exclamation mark (!). This was  done in the first code snippet where `numberInString` was implicitly unwrapped then converted to an Int.

{% highlight swift %}  
    //unwrapping on assignment with type annotation
    let exampleUnwrapOne:String! = "some string"
    let someOptional:String? = "optional text"
    //implicitly unwrapping some optional
    let someStringVal = someOptional!
{% endhighlight %}

# Conclusion

Swift has an interesting way of dealing with types and ensuring type safety. I can pickup some similarities to it and languages such as typescript with the way it annotates it's types and the use of tuples to languages like python. There are unique features that I first encountered with it like optionals. It's a very interesting language and I look forward to the next 28 days of building and sharing about it.