---
title: I am ErrorType
date: 2016-07-28
tags: programming, swift
tagline: A Zelda reference. How delightful! Tune in next time when I use Portal to explain continuations.
---

I'm going to be talking about Swift's `ErrorType` in the next few posts, and 
I thought I'd talk a little more about it since the built in documentation on
it is... lacking. It's an empty protocol! What good is that? Well, it turns out
that anything that conforms to `ErrorType` can be thrown as an error. Let's
take a look at what that means, and what you can do with it.

First, here is a enum that conforms to ErrorType, along with a function that
could potentially throw an instance of it:

~~~swift
enum ShieldsError: ErrorType {
    case WrongPrefixCode
    case ShieldsAlreadyDown
}

func lowerReliantShields(prefixCode: Int) throws -> Bool {
    guard prefixCode == 16309 else {
        throw ShieldsError.WrongPrefixCode
    }    
    ...
}
~~~

If we try to use this function like any other, Xcode will complain that we're
not handling a potential error, and Xcode would be right. When a function is
capable of throwing an error, you need to be prepared to catch it. There are
a few ways you can do this. The first is with a `do-catch` statement:

~~~swift
var shieldsLowered: Bool

do { 
    shieldsLowered = try lowerReliantSheilds(19004)
} catch ShieldsError.ShieldsAlreadyDown {
    print("Shields already down!")
} catch ShieldsError.WrongPrefixCode {
    print("You entered the wrong code!")
}
~~~

In this `do-catch` statement, we go through each of the possible errors that
`lowerReliantShields` could throw, and we handle the different errors one by
one. This
example has `print` statements, but you could do anything in there. `do-catch`
is useful when you need to know what type of error was thrown.

If you don't care what type of error is thrown, you can use `try` outside of
a `do-catch` statement. `try` has two forms, `try?` and `try!`. Let's look at
them one at a time.

`try?` returns an optional. If your function was successful, the optional will
contain the return value. If it throws an error, the optional will be nil. 

~~~swift
guard let shieldsLowered = try? lowerReliantShields(16309) else {
    // handle error here
}
~~~

`try!` is similar to `try?` except that instead of returning an optional,
`try!` will cause a runtime error if an error is thrown. Apple recommends using
`try!` when you know an error won't be thrown, and uses the example of loading
an image that is shipped with an application. While assuming files will be where
you put them is probably safe, I am a cautious person. For example, I would
normally agree with the statement "All calendar months have at least 28 days."
If you are using OSX, Linux, or any *nix system, run `cal 9 1752` in your
terminal to see how safe that assumption is.

The one situation that I think warrants using `try!` is that if an error is
thrown, something so terrible happened that you want to crash immediately. I do this
when setting up Core Data within an application. If I cannot find the data
model file, then something is seriously wrong, and I would like to abandon ship
as soon as possible.
