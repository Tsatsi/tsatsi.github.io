---
layout: post
title:  "Why clojure?"
tags:
  - programming
  - clojure
  - philosophy
hero: "assets/img/clojure.png"
overlay: purple
published: true

---
At my current company (Columinate at the time of writing) we write code in clojure and clojurescript. I have often been asked the question "Why clojure?". I hope to answer this question with this blog post and to highlight the pros and cons of opting for clojure.
{: .lead}
<!–-break-–>

Clojure is a pragmatic dynamic language founded by Rich Hickey that endeavours to be a general purpose language that is suitable in areas where Java is suitable. It is opinionated and does not try to cover all the paradigms but instead provides the features needed to solve real-world problems. It allows developers to avoid the costs of maintaining a different infrastructure while leveraging existing libraries.

Rich Hickey wanted a **lisp** for **functional programming** that takes advantage of a well **established platform** and is **designed for concurrency**.

The benefits of the language being a lisp are:
- homoiconicity (code as data and syntantic abstraction)
- minimal syntax
- not constraint by backwards compatibility

Clojure is a functional language with a dynamic emphasis, the benefits of this are:
- Immutable data structures
- First-class functions
- Dynamic polymorphism

The reason for taking advantage of established platforms is to avoid rebuilding the wheel and for this clojure uses the JVM. The JVM has  a proven track record, works across operating systems and is open.

Clojure was build with the following goals in mind:
- Simplicity
- Freedom to focus
- Empowerment

![clojure-goals](../assets/img/clojure-goals.png)


