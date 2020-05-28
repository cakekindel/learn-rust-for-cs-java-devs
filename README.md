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

