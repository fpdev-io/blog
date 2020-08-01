---
layout: post
title:  "What is Functional Programming?!"
date:   2020-07-13 23:01:16 +0200
categories: functional programming
author: fp-dev
---

Some time ago I was Java Developer. One day I decided that I'd like to be Scala developer. I didn't have any previous experience with this language.

When I started learning it, it quickly turned out that it's not just a syntax to grab. It was the whole new world of programming with a very different approach. It was Functional Programming.

# What is Functional Programming?

Functional Programming is a programming style with functions. 
{% highlight scala %}   
def func(): Unit = {
    println("hello World!")
}

{% endhighlight %}

## Monad definition in Scala
{% highlight scala %}
    trait Monad[F[_]] {
        def pure[A](value: A): F[A]
        def flatMap[A, B](value: F[A])(func: A => F[B]): F[B]
    }
{% endhighlight %}