---
layout: post
title:  "Monads are easy"
# date:   2020-07-20 23:00 +0200
categories: functional programming, scala
author: fp-dev
---

Monads are seen as a kind of structure that sounds horrible.

## Monad definition in Scala
{% highlight scala %}
    trait Monad[F[_]] {
        def pure[A](value: A): F[A]
        def flatMap[A, B](value: F[A])(func: A => F[B]): F[B]
    }
{% endhighlight %}
