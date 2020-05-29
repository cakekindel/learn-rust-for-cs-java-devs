# C# to Rust
learn Rust by transforming C# into Rust, step by step

This is a thought piece that is meant to be read top-to-bottom in order,
and is a "what if" exercise, changing the core values of C# to those of
Rust, with the end goal of arriving at the Rust language.

## Table of Contents
- [Why this guide exists](#why-this-guide-exists)
    - [If this guide helped you](#if-this-guide-helped-you)
    - [If this guide is missing something](#if-this-guide-is-missing-something)
- [Language Values](#language-values)
    - [List of values](#list-of-values)
    - [C# or Java](#cs-or-java)
    - [Rust](#rust)
    - [How to interpret](#how-to-interpret)
- [Expression orientation](#expression-orientation)

## Why this guide exists
As someone who was at one point only comfortable
in languages and ecosystems heavily geared towards OOP,
Rust can be very difficult to appreciate and fully understand.

Rust is an incredibly powerful, and very unique
programming language that can have a very steep learning curve.

So, let's contextualize it by experimenting with
language design!

### If this guide helped you
please consider doing one or more of the following
- star this repo
- file an issue to say thanks
- share this with other rust-curious individuals

### If this guide is missing something
please [file an issue](https://www.github.com/cakekindel/cs-to-rust/issues/new)!

## Language Values
It's important that we understand the **motivation** for the changes to come.

This section is intended to outline the **core values** of the two languages,
with the intent of pointing out the virtues that each is unwilling to compromise on.

You don't have to agree with every decision that is made, but please make an
effort to understand & internalize the core values of both languages.

### List of values
Here is a very rough list of programming language core values,
shamelessly ripped from [bcantrill](https://github.com/bcantrill)'s
[awesome 2018 talk on Rust](https://www.youtube.com/watch?v=2wZ1pCpJUIM),
and programming values in general.

| | | |
|---|---|---|
|Approachability|Integrity|Robust|
|Availability|Maintainability|Safety|
|Compatibility|Measurability|Security|
|Composability|Operability|Simplicity|
|Debuggability|Performance|Stability|
|Expressiveness|Portability|Thoroughness|
|Extensibility|Resiliency|Transparency|
|Interoperability|Rigor|Velocity|

### CS or Java

| | | |
|---|---|---|
|✅Approachability|Integrity|Robust|
|Availability|Maintainability|Safety|
|✅Compatibility|Measurability|Security|
|Composability|Operability|Simplicity|
|✅Debuggability|✅Performance|Stability|
|Expressiveness|✅Portability|Thoroughness|
|Extensibility|Resiliency|Transparency|
|✅Interoperability|Rigor|✅Velocity|

### Rust
| | | |
|---|---|---|
|Approachability|✅Integrity|✅Robust|
|Availability|Maintainability|✅Safety|
|Compatibility|Measurability|✅Security|
|✅Composability|Operability|Simplicity|
|Debuggability|✅Performance|Stability|
|✅Expressiveness|Portability|Thoroughness|
|✅Extensibility|Resiliency|Transparency|
|✅Interoperability|✅Rigor|Velocity|

### How to interpret
C# / Java values being approachable, classical (in the C-influenced, OOP imperative sense),
and performant. The two languages are geared towards moving quickly with a moderate amount
of type safety.

Rust is to C# / Java as C# / Java is to Python. Rust introduces some rules of significant
complexity to guarantee memory & thread safety at compile time. This means that in exchange
for some cognitive load & extra development time, you are rewarded with an extremely fast
program that is most likely going to work exactly as you expect it to.

## Expression Oriented
In Java & C#, the _statements_ in a code block do not resolve to values.

For example:
```cs
public class Dice
{
    public void Roll()
    {
        var random = new Random();
        int diceVal = random.Next(1, 6);

        return diceVal;
    }
}
```

In our example, `new Random()` is a C# _expression_ that resolves to an instance
of the `Random` class. `var random = new Random()` however is a _statement_ that
does not resolve to a value, not even `void`. In this language, there is a rough
tacit rule that each line in your program's code is an instructional step,
not an expression that resolves to a value.

```cs
public class Game
{
    private bool canMove = true;

    // This code is OK
    public void GetSpacesToMove_Ternary()
    {
        return this.canMove ? new Dice().Roll() : 0;
    }

    // This code does not compile
    public void GetSpacesToMove_IfStatements()
    {
        return if (this.canMove)
        {
            new Dice().Roll();
        }
        else
        {
            0;
        }
    }

    // <snip>
}
```

## Enums
The Rust `enum` idiom, and the C# `enum` idiom are _very_ different.

Given a C#-style enum like this:
```cs
public enum Coin
{
    Quarter = 1,
    Nickel = 2,
    Dime = 3
}
```

It may be helpful to think of an "instance" of this `Coin` enum as `1` OR `2` OR `3`.

Following this, imagine you could have a C# enum that could contain a reference type:

```cs
public enum Coin
{
    Quarter = "Quarter",
    Nickel = "Nickel",
    Dime = "Dime",
}
```

What if enums supported each _Variant_ having different types?

```cs
public enum Coin
{
    Quarter = 0.25, // float
    Nickel = 0.05, // float
    Dollar = 1, // int
    Hapenny = 0.005, // float
    Default = null // always null
}
```

Now this `Coin` enum means "0.25 or 0.05 or null or 1"

TODO: the rest
