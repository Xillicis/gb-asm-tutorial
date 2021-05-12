---
title: Assembly
---

Alright, now that we know what the tools *do*, let's see what language RGBASM speaks.
I will take a short slice of the beginning of `hello-world.asm`, so that we agree on the line numbers, and you can get some syntax highlighting even if your editor doesn't support it.

{% highlight nasm linenos %}
INCLUDE "hardware.inc"

SECTION "Header", ROM0[$100]

	di
	jp EntryPoint

	ds $150 - @, 0

SECTION "Code", ROM0

EntryPoint:
	; Kill sound
	ld a, 0
	ldh [rNR52], a
{% endhighlight %}

Let's analyze it.
Note that I will be glossing over a *lot* of RGBASM's functionality; if you're curious to know more, you should [read the docs](https://rgbds.gbdev.io/docs).

## Comments

We'll start with line 13, which should appear gray above.
Semicolons `;` denote *comments*.
Everything from a semicolon to the end of the line is *ignored* by RGBASM.

Comments are a staple of every good programming language; they are useful to give context as to what code is doing.
They're the difference between "Wash the rice" and "Wash the rice so the onigiris won't break apart", basically.
In any language, good comments are very useful; in assembly, they play an even more important role, as many common semantic facilities are not available.

## Includes

Line 1 *includes* `hardware.inc`.
Including a file has the same effect as if you copy-pasted it, but without having to actually do that.
It allows sharing the same file: if `a.asm` and `b.asm` include `hardware.inc`, you only need to modify `hardware.inc` once, instead of both `a.asm` and `b.asm` if you actually copy-pasted the contents.

## General syntax

Assembly is a very line-based language.
