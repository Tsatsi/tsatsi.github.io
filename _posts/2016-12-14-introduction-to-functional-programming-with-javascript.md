---
layout: post
title:  "Introduction to functional programming with javascript part 1"
date:   2016-12-14 00:00:00 +0200
categories: functional programming
hero: "assets/img/functionaljs.png"
overlay: red
published: true
---
After Spending some time reading Dr Frisby Most adequate guide to functional programming I thought I should write a blog to summarize my understanding of the concepts presented especially seeing how foreign some of them were to me. So what is it that we are after when we write programs in a functional way?
{: .lead}
<!–-break-–>
functional programming is governed by general programming principles such as YAGNI(ya ain’t gonna need it), DRY(don’t repeat yourself) and SOLID principles. Functions are treated as first class citizens, that is to say they are treated just like everyone else or other data types. They can be passed as parameters, stored in arrays or assigned as variables.

To understand how functional programming differs from other styles of programming we will go through some examples and see how it helps improve code.

Let’s consider this problem from code wars:
Deoxyribonucleic acid (DNA) is a chemical found in the nucleus of cells and carries the “instructions” for the development and functioning of living organisms.

In DNA strings, symbols “A” and “T” are complements of each other, as  are “C” and “G”.
You have a function which accepts one side of the DNA; you need to get the complementary side.
DNA is never empty or there’s no DNA at all.

To solve this problem one might take this approach:

{% highlight ruby %}
var result = ‘’;
function getDNAStrand(dna) {
    for( var i = 0;    i < dna.length;    i++ ){
        if(dna[i]===“A”){result +=“T”;}
        else if(dna[i]===“T”){result +=“A”;}
        else if(dna[i]===“C”){result +=“G”;}
        else if(dna[i]===“G”){result +=“C”;}
         else {result +=dna[i];}
    }
  return result;
}
{% endhighlight %}


This example uses a lot of if-else statements and mutates the result variable to get to the final answer. The problem with this approach is that it can lead to incorrect results.
The variable result is mutable, should it have changed outside getDNAStrand, we will end up with the wrong results. This means getDNAStrand is impure because given the same input it is possible that the results we will get will be different, It also has undesirable side effects because it mutates the variable result.

Functional programming makes use of pure functions, which are functions that do not have side effects. Given the same input they return the same output. Mutable state and mutable values are unreasonably difficult to keep track of and for this reason, functional programs only maintain immutable values and state.
i.e they rely soley on their arguments

The first move towards getting getDNAStrand to be a pure function would be:

{% highlight ruby %}
function getDNAStrand(dna) {
  var result = ‘’;
    for( var i = 0;    i < dna.length;    i++ ){
        if(dna[i]===“A”){result +=“T”;}
        else if(dna[i]===“T”){result +=“A”;}
        else if(dna[i]===“C”){result +=“G”;}
        else if(dna[i]===“G”){result +=“C”;}
         else {result +=dna[i];}
    }
  return result;
}
{% endhighlight %}

result has been moved into the getDNAStrand function and can only be changed within the function. Given the same input getDNAStrand will return the same output without any observable side effects. But we can take this a step further. Remember functional programs do not have mutable state or values, but result still remains mutable within getDNAStrand.

A more functional approach would look like this:

{% highlight ruby %}
function DNAStrand(dna){
    const complements = {A: ’T’, T: ‘A’, C: ‘G’, G: ‘C’}
    return dna.split(‘’).map( x => complements[x]).join(‘’)
}
{% endhighlight %}

The philosophy of functional programming suggests that side effects are a primary cause of incorrect behavior. But this does not mean we are forbidden to use them but rather, we want to contain them and use them in a controlled way.

Using pure functions enables us to cache inputs using an optimization technique called memoization. Memoisation speeds computer programs by storing expensive function calls and returning the cached results when the same input occurs again.

{% highlight ruby %}
var dnaStrand = memoize(DNAStrand);

dnaStrand(‘AATT’)
//=> TTAA

dnaStrand(‘AATT’) // returns cache from input ‘AATT'
// => TTAA  


var memoize = function(f){
    var cache = {};
    
        return function ( ){
            var arg_str = JSON.stringify(arguments);
            cache[arg_str] = cache[arg_str]  || f.apply(f, arguments);
            return cache[arg_str];
        }
}
{% endhighlight %}
