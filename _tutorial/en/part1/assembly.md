---
title: Assembly basics
footnotes:
  instr_directive: >-
    Technically, instructions in RGBASM are implemented as directives, more or less transparently outputting them to ROM; but this creates an artificial distinction between the instructions in the source code and those in the final ROM, so it's not worth bringing up right now.
  ld_imm_from: >-
    The curious reader may ask where the value is copied *from*. The answer is simply that the \"immediate\" byte ($00 in this example) is stored in ROM just after the instruction's opcode byte, and it's what gets copied to `a`.
    We will come back to this when we talk about how instructions are encoded later on.
---

Alright, now that we know what the tools *do*, let's see what language RGBASM speaks.
I will take a short slice of the beginning of `hello-world.asm`, so that we agree on the line numbers, and you can get some syntax highlighting even if your editor doesn't support it.

{% highlight nasm linenos %}
INCLUDE "hardware.inc"

SECTION "Header", ROM0[$100]

	di
	jp EntryPoint

	ds $150 - @, 0 ; Make room for the header

SECTION "Code", ROM0

EntryPoint:
	; Kill sound
	ld a, 0
	ldh [rNR52], a
{% endhighlight %}

Let's analyze it.
Note that I will be glossing over a *lot* of RGBASM's functionality; if you're curious to know more, you should wait until parts II and III, or [read the docs](https://rgbds.gbdev.io/docs).

## Comments

We'll start with line 13, which should appear gray above.
Semicolons `;` denote *comments*.
Everything from a semicolon to the end of the line is *ignored* by RGBASM.
As you can see on line 9, comments need not be on an otherwise empty line.

Comments are a staple of every good programming language; they are useful to give context as to what code is doing.
They're the difference between "Pre-heat the oven at 180 °C" and "Pre-heat the oven at 180 °C, any higher and the cake would burn", basically.
In any language, good comments are very useful; in assembly, they play an even more important role, as many common semantic facilities are not available.

## Instructions

Assembly is a very line-based language.
Each line can contain a *directive*, which instructs RGBASM to do something, or an *instruction*<sup>{% include footnote.html id="instr_directive" %}</sup>, which is copied directly into the ROM.

We will talk about directives later, for now let's focus on instructions.
To continue the cake-baking analogy even further, instructions are like steps in a recipe.
The console's processor (<abbr title="Central Processing Unit">CPU</abbr>) executes instructions one at a time, and that... eventually does something!
Like baking a cake, draw a "Hello World" image, or display a Game Boy programming tutorial!
\*wink\* \*wink\*

In the snippet above, lines 1 (`INCLUDE`), 8 (`ds`), and 10 (`SECTION`) are directives, so we will ignore them for the time being.
Instructions have a *mnemonic*, which is a name they are given, and *operands*, which indicate what they should act upon.
For example, in "melt the chocolate and butter in a saucepan", *the whole sentence* would be the instruction, *the verb* "melt" would be the mnemonic, and "chocolate", "butter", and "saucepan" being the operands, i.e. some kind of parameters to the operation.

Let's discuss the most fundamental instruction, **`ld`**.
`ld` stands for "LoaD", and its purpose is simply to copy data from its right operand (["<abbr title="Right-Hand Side">RHS</abbr>"](https://en.wikipedia.org/wiki/Sides_of_an_equation)) into its left operand (["<abbr title="Left-Hand Side">LHS</abbr>"](https://en.wikipedia.org/wiki/Sides_of_an_equation))
For example, take line 14's `ld a, 0`: it copies ("loads") the value 0 into the 8-bit register `a`<sup>{% include footnote.html id="ld_imm_from" %}</sup>.
If you look further, line 58 has `ld a, b`, which causes the value in register `b` to be copied into register `a`.
`ldh` is just like `ld`, but a bit special; for now, just treat it as `ld`.

ℹ️ Due to CPU limitations, not all operand combinations are valid for `ld` and many other instructions; we will talk about this when writing our own code later.

Instruction | Mnemonic | Effect
------------|----------|---------------------
Load        | `ld`     | Copies values around
