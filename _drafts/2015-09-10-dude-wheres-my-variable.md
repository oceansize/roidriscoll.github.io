---
layout: post
title: Dude, Where's My Variable?
date: 2015-09-10 11:52:15
---

Today I witnessed a rather heated debate about Ruby, and how it stores a value in a variable. No-one in the group was able to reach a consensus and I thought it would be fun to explore in blog-post form (after a little research!)

### Pass by Reference Vs Pass by Value

Firstly it's important to understand that for the most part, a language associates values with variables in either of the following ways: **passing by reference** or **passing by value**.

To understand this, I turned to Stack Overflow and found this [fantastic post](http://stackoverflow.com/questions/373419/whats-the-difference-between-passing-by-reference-vs-passing-by-value), which I will repost here:

### Say I want to share a web page with you...

#### By Ref(erence)

If I tell you the URL, I'm **passing by reference.** You can use that URL to see the same web page I can see. If that page is changed, we both see the changes. If you delete the URL, all you're doing is _destroying your reference to that page_ - you're not deleting the actual page itself.

#### By Val(ue)

If I print out the page and give you the printout, I'm **passing by value.** Your page is a disconnected copy of the original. You won't see any subsequent changes, and any changes that you make (e.g. scribbling on your printout) will not show up on the original page. _If you destroy the printout, you have actually destroyed your copy of the object_ - but the original web page remains intact.

### Ruby is Pass by Value

Consider the following program:

```
def increment(number)
  number += 1
end

integer = 1
increment(integer)
puts integer
```

## Output: By Ref
```
=> 2
```
In this case, the `number` variable increments the value of `integer` because inside `number` is a _reference_ to a value. In our example, this variable contains the URL, not the site.

## Output: By Val
```
=> 1
```
In this case, the `number` and `integer` variables are independent from one another. The value stored inside each variable is the printout in our web example.

### Still confused?

Let's make sure we definitely get this. Consider the following example:

```
def secret_squirrel(message)
  message << " Iron Man is actually Tony Stark!"
  message << " Spider Man is a student called Peter Parker."
  message << " Batman's secret identity is Bruce Wayne."
  message = "Nothing to see here. Move along."
end
```
What do we anticipate would happen if we did the following:

```
tell_me_secrets = "Psst, what's news?"
secret_squirrel(tell_me_secrets)
puts tell_me_secrets
```
What do we anticipate Ruby will give us if we ask for the contents of `tell_me_secrets`?

If you guessed that a lot of Super Heroes are currently cursing me, this blog and possibly even the Ruby programming language then you're right. And if that was a lucky guess, allow me to explain...

We pass the variable `tell_me_secrets` (which contains a string value) to the method `secret squirrel`. Once inside, `tell_me_secrets`, represented by the variable `message` in the method has the shovel (`<<`) operator applied to it. At this point you might expect that `message` is a copy of `tell_me_secrets` value, but the 

??? both of the standard cloning methods do a shallow copy, so the instance variables of the clone still point to the same objects that the originals did.???

#### Sources:
* Stack Overflow post ["Ruby - Parameters by reference or by value?"](http://stackoverflow.com/questions/22827566/ruby-parameters-by-reference-or-by-value/22827949#22827949)
* Stack Overflow post ["Is Ruby pass by reference or by value?"](http://stackoverflow.com/a/10974116)
