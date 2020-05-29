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

Believe it or not, you already know this! If you're familiar with a ternary
statement, you can reason about `if / else` statements as being the **statement**
based conditional idiom, while ternary statements are the **expression-based**
conditional idiom.

Imagine if **both** methods in the following code snippet were OK with the
C# compiler, and semantically equivalent:

```cs
public class Game
{
    private bool canMove = true;
    
    public void GetSpacesToMove_Ternary()
    {
        return this.canMove ? new Dice().Roll() : 0;
    }

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

If you're wondering "why would you make this change? We already have ternary statements,
and this is _more_ verbose!", with some syntactic changes to `if` statements, you
could argue that ternary statements are wholly unnecessary:

```cs
// ternary
this.canMove ? new Dice().Roll() : 0

// vs our tersified if statements:
if this.canMove { new Dice().Roll() } else { 0 }
```

You don't have to prefer the expression-based terse if statements, but now you're familiar with
the semantics of Rust's conditional statements.

This is important, because if everything resolves to a value,
then you can make the `return` statements **optional** if the last line in a function
body is an expression.

```cs
public int Roll()
{
    var random = new Random();

    random.Next(1, 6)
}

// real C# equivalent:
public int Roll()
{
    var random = new Random();

    return random.Next(1, 6);
}
```

You don't have to love this language feature, but in a world where everything
is an expression, you'll probably come across **function bodies** that
end with an expression rather than a return statement.

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

What if enums supported each member, or _Variant_, having different types?

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

When handling this `Coin` enum, one might use the
pattern-matching features in C# 8 like so:

```cs
public int AppraiseCoin(Coin coin)
{
    return coin switch
    {
        Coin.Quarter => /* algorithm to appraise quarters? */,
        // <snip>
    };
}
```

What if the types contained in enums did not have to be constant values?

**What if** "instances" of enum variants could have a `struct` contained within?

Let's say you're dealing with IP Addresses and want to have a strongly-typed
differentiation between IPV4 addresses & IPV6:
```cs
public enum IpAddress
{
    V4(string),
    V6(string),
}
```

In this example, if one had a variable of type `IpAddress`,
the variable contains a string that represents the full IP address.

This allows one to use patterns like this:
```cs
public class TcpHelper
{
    public TcpConnection Connect(IpAddress addr)
    {
        return addr switch
        {
            IpAddress.V4(addrV4) => ConnectIpV4(addrV4),
            IpAddress.V6(addrV6) => ConnectIpV6(addrV6),
        }
    }

    private TcpConnection ConnectIpV4(string addrRaw);
    private TcpConnection ConnectIpV6(string addrRaw);
}
```

Contrast this with a vanilla C# implementation:
```cs
public class TcpHelper
{
    public TcpConnection Connect(IpAddress addr)
    {
        if (IsIpV4(addr))
        {
            return ConnectIpV4(addr);
        }
        else if (IsIpV6(addr))
        {
            return ConnectIpV6(addr);
        }
    }

    private bool IsIpV4(string addrRaw) { /* <snip> */ } 
    private bool IsIpV6(string addrRaw) { /* <snip> */ } 
}
```

A couple things to note here:
- Readers of this code, or recievers of `string addr` have no hints at the type level
    that the given string is an Ip Address v4, v6, or even an Ip Address at all.

- By using Enums this way, if a hypothetical IPV8 was introduced, **all code**
    pattern-matching over IpAddress _immediately_ breaks, telling the maintainers
    all the places where the new case is not considered.


