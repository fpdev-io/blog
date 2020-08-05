---
layout: post
date:   2020-08-05 07:00:00 +0100
title:  "Functors explained"
categories: functional programming, scala
author: fp_dev
---

When you start writing your code in a more functional way you finally learn about **`Functors`**, **`Monads`** and
**`Applicatives`**.
At first it can be overwhelming but I'll try to explain what's all about and how to better understand these constructs.

In this blogpost we'll define our own **`Functor`**, **`Monad`** and **`Applicative`**.

Let's make some assumptions first:

1. We have three functions:
 - **`A => B`**
 - **`A => F[B]`**
 - **`F[A => B]`**
2. We want to use a function of type **`F[A] => F[B]`**.  

It's obvious that we cannot apply such a function. We need to make some transformations.

**`F[_]`** is a type constructor. If you don't know what type constructors are please go to my
[blogpost](https://fp-dev.io/type-constructors).

Let's define our first Functor. 
# What is Functor?
Informally we can say that **`Functor`** is anything with a **`map`** method.  
So types like **`List`**, **`Option`** or **`Either`** are functors.

{% highlight scala %}
Option(1).map(n => n + 1)
// res0: Option[Int] = Some(2)

List(1, 2, 3).map(n => n + 1)
// res1: List[Int] = List(2, 3, 4)
{% endhighlight %}
Using simple transformations we could define Functor more formally as:

# **`(A => B) => (F[A] => F[B])`**
It's a function that gets a function of type **`A => B`**(which itself is a function :wink:) as parameter and returns another function of type **`F[A] => F[B]`**.
We can look at **`F[A]`** as a box that can hold a value of type **`A`**.  

For instance:
**`Option[Int]`** is a box that can hold a value of type **`Int`**.  

In Scala it would be defined as:
{% highlight scala %}
val opt = Option(10)
// opt: Option[Int] = Some(100) 
{% endhighlight %}

If it's still hard to understand let's define an Option-like container from scratch.
{% highlight scala %}
case class Box[T](value: T)
{% endhighlight %}
We defined a `case class` that has only one property `value of type T`.

Let's put a value into it.
{% highlight scala %}
val boxedInt = Box(100)
{% endhighlight %}

Ok, now we have an instance of `Box` case class and we want to apply some computation to it. Let's say we want to square
the value inside the `Box`
We write a function that gets Int parameter and squares it. 
{% highlight scala %}
def square(x: Int): Int = x * x
{% endhighlight %}
But hmm, how can we apply our **`square`** function into **Box[T]** type if our function is of type **`Int => Int`** but we need
a function **`F[Int] => F[Int]`**?

We quickly come up with a solution: We need another transformation!
So we write:

{% highlight scala %}
def map[A, B](f: A => B): Box[A] => Box[B] = (a: Box[A]) => Box(f(a))
{% endhighlight %}

We've just defined a function that will help us a lot.  
Our **`map`** is a function that takes another function as a parameter and returns a function of type **`Box[A] => Box[B]`**

Let's grab the code together:
{% highlight scala %}
case class Box[T](value: T)

def quare(value: Int) = x * x
def map[A, B](f: A => B): Box[A] => Box[B] = (a: Box[A]) => Box(f(a.value))

val box = Box(100)
val mappedSquare = map(square)
val result = mappedSquare(box)
//result: Box[Int] = Box(10000)

{% endhighlight %}

One more example. With strings this time.

Let's have a string **`"fp-dev.io"`** that we want to uppercase. 

**What we have:**  
A raw function **`.toUpperCase()`**, so **`"fp-dev.io".toUpperCase`** would return **`FP-DEV.IO`**

**What we need:**  
A function **`Box[String] => Box[String]`**

We already have a mapping function so let's use it:

{% highlight scala %}

val box = Box("fp-dev.io")

def toUpperCase(s: String) = s.toUpperCase

val upperCasedString = map(toUpperCase)

val result = upperCasedString(box)

// To make the code shorter we could even write something like this:
val result = map(toUpperCase)(string)
// result: Box[String] = Box(FP-DEV.IO)
{% endhighlight %}

:tada: :tada: :tada: **This way we created the mysterious Functor.** :tada: :tada: :tada:

I already mentioned that **`List`**, **`Option`** and **`Either`** are functors so that
they have their own version of **`map`** implemented. It's implemented inside these structures so the usage is a bit
better. 
{% highlight scala %}
case class Option {
  def map[A, B](f: A => B): Option[B]
}
{% endhighlight %}
The argument on which it operates **`Option[A]`** it takes from inside.  
That's why we use it like:

{% highlight scala %}
val opt = Option("string")

opt.map(s => s.toUpperCase)
// opt: Option[String] = Some(STRING)
{% endhighlight %}
As you can see the usage is much pleasant. 

The same with Lists:
{% highlight scala %}
val list = List(1, 2, 3)

list.map(n => n + 1)
// list: List[Int] = List(2, 3, 4)
{% endhighlight %}
Ok that's all for now. I hope I explained a bit about Functors. In the next blogpost we'll talk about **`Monads`**
:smile::heart:

