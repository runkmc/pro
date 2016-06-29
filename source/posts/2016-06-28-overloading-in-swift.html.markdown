---
title: Overloading in Swift
date: 2016-06-28
tags: programming, swift
---

You can overload functions in Swift. Let's try it! READMORE

~~~swift
func myFunction(item:String) -> String {
    return "Here is that string: \(item)"
}

func myFunction(item:Int) -> String {
    return "And here is that integer: \(item)"
}

myFunction("Hi there")   \\ "Here is that string: Hi there"
myFunction(4)            \\ "And here is that integer: 4" 
~~~

Neat! Swift knows which version of the function we want based solely on the type of the parameter we pass in. We can even write two versions of this function that take the same type of parameter (or parameters) as long as they have different return types. 

~~~swift
func yesterday(date:NSDate) -> String {
    let formatter = NSDateFormatter()
    formatter.dateFormat = "MM-dd-yyyy"
    return formatter.stringFromDate(date)
}

func yesterday(date:NSDate) -> NSDate? {
    let components = NSDateComponents()
    let calendar = NSCalendar.currentCalendar()
    components.day = -1
    return calendar.dateByAddingComponents(components, toDate: date, options: [])
}

let today = NSDate()
let date = yesterday(today)
~~~

Wait! We got an error on that last line! Xcode is complaining about an "Ambiguous use
of 'yesterday'". This is because Xcode can't tell which version of our function
we want. There's not enough information there. We need to supply the type we
are expecting like so:

~~~swift
let date: NSDate? = yesterday(today)
~~~

Now `date` holds an object of type NSDate?.  We can safely use functions that
differ only in return type in places where one of those types are expected as
well. Observe:

~~~swift
func stringSmasher(toSmash:String) -> String {
    return "SMASH \(toSmash)"
}

stringSmasher(yesterday(today))
~~~

That last line will return the string "SMASH 12-06-2015". I'm not specifying
the return type of `yesterday` anywhere, but since Swift wants a string in that
spot, it knows to just go ahead and use the version that returns a string.

Thanks, Swift!
