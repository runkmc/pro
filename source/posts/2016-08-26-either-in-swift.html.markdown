---
title: Either in Swift
date: 2016-08-26
tags: swift, programming, haskell
tagline: You got your Haskell in my Swift! I got my Swift in your Haskell!
---

Let's suppose we have an iOS application that requires users to log in. Here's
a `User` struct:

~~~swift
struct User {
    let name: String
	let occupation: String
	let hometown: String
}
~~~

And here's a simple function that might handle the login process:

~~~swift
func logInUser(username: String, password: String) -> User? {
    // handle login stuff and return a user if successful
}
~~~

We're returning an optional `User` here because the login might fail. The
problem with this is that if we get `nil`, we don't know why we failed. Incorrect
password? Does the user not exist? LOCUSTS?!? WAS IT LOCUSTS?!?! There's no way
to know. Let's try a different approach that might let us know the reason for
any failures. First, let's define a `UserError` that conforms to the `ErrorType` protocol:

~~~swift
struct UserError: ErrorType {
    let errorMessage: String
}
~~~

Now let's try that `logInUser` function again:

~~~swift
func logInUser(username: String, password: String) -> (User?, UserError?) {
    // return a user if successful, and UserError if not
}
~~~

This is better because now we have an object that will let us know the reason
for failure instead of just nil. I'm still not a fan of this
strategy, though. What's to prevent us from returning a `User` *and*
a `UserError`? Or what's to prevent us from returning two nils?
We're assuming that one of these two optionals will always have
a value, and that the other one will always be nil. That's an assumption that
the type system can't enforce.

To fix this, we could throw a `UserError`, or we could steal a page from the Haskell playbook. Haskell has a type
called `Either`. This is sort of like an optional in Swift, but instead of
potentially having a value or being nil, `Either` has one of two potential
values. Here is a definition for us to use in this situation:

~~~swift
enum Either<T, U: ErrorType> {
    case Success(T)
    case Failure(U)
}
~~~

It should be noted that instead of "Success" and "Failure", Haskell labels
these as "Right" and "Left". I've chosen different names here so that they're
easier to read and understand in the example.

Let's try our login function one last time:

~~~swift
func logInUser(username: String, password: String) -> Either<User, UserError> {
// return Either, containing either a User or a UserError
}
~~~

This is better. We've completely eliminated optionals from this process. 
Now, our function has to return either a User or a UserError. It can't return
nil, and it can't return two values. I think it's more readable, as well.
It's clear that this function returns either a `User` or a `UserError`. 

In part two of this series, I'll look at how to efficiently work with an
`Either` value, and how to deal with an array of `Either` values.
