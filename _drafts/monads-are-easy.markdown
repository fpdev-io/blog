---
layout: post
title:  "Monads are easy"
# date:   2020-07-20 23:00 +0200
categories: functional programming, scala
author: fp_dev
---

Monads are seen as a kind of structure that sounds horrible for a newbie in a function progamming world.
But don't be scared, I'll try to explain everything.

When you start coding your software in a functional way you quickly come across Monads.

Their older colleages try to explain what Monads are and say:
>Monads are Monoids in the category of endofunctors.

What does it even mean?!

Of course the definition is correct but this explanation doesn't help with understanding Monads. 

# So what is Monad?

## Monad definition in Scala
{% highlight scala %}
    trait Monad[F[_]] {
        def pure[A](value: A): F[A]
        def flatMap[A, B](value: F[A])(func: A => F[B]): F[B]
    }
{% endhighlight %}
