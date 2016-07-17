---
title: Fizzbuzz Counts
date: '2016-07-17'
tags: programming, ruby, scheme
tagline: Time for some pop. Watch out for the fizz!
---

I forget where I saw it, but I recently saw a variation of the <a href="http://en.wikipedia.org/wiki/Fizz_buzz">FizzBuzz problem</a> wherein instead of printing numbers and substituting 'fizz', 'buzz', and 'fizz buzz' where appropriate, the goal is to return the number of times those words would be printed for any given range of numbers. The version I saw created an additional twist by demanding the range between the numbers given be in the tens or hundreds of millions, but I thought it would be an interesting learning exercise for me to try to solve this problem in both ruby and scheme, only with more modest demands. I used the range of whole numbers from 5 to 15 in each example. The result should be three fizzes, two buzzes, and one fizzbuzz.

First, the ruby version. It's pretty straightforward, and only took a few minutes:

~~~ruby
fb = {fizz: 0, buzz: 0, fizzbuzz: 0}

(5..15).each do |n|
  if n % 5 == 0 and n % 3 == 0
    fb[:fizzbuzz] += 1
  elsif i % 5 == 0
    fb[:buzz] += 1
  elsif i % 3 == 0
    fb[:fizz] += 1
  end
end
~~~

The ruby version starts with a hash with three keys, one for each word we are tracking. We iterate through each number in a given range, check to see if it is a multiple of 5 or 3 or both, and then we increment the corresponding number in the preexisting hash. Like I said, pretty straightforward. Now for the scheme version:

~~~scheme
(define fizzbuzz
  (lambda (m n col)
    (cond
      ((> m n) (col 0 0 0))
      ((and (zero? (modulo m 5)) (zero? (modulo m 3)))
       (fizzbuzz (add1 m) n (lambda (f b fb)
                      (col f b (add1 fb)))))
      ((zero? (modulo m 5)) (fizzbuzz (add1 m) n (lambda (f b fb)
                                   (col f (add1 b) fb))))
      ((zero? (modulo m 3)) (fizzbuzz (add1 m) n (lambda (f b fb)
                                   (col (add1 f) b fb))))
      (else (fizzbuzz (add1 m) n (lambda (f b fb)
                           (col f b fb)))))))
                      
(fizzbuzz 5 15 (lambda (f b fb)
         (cons f (cons b (cons fb '())))))
~~~

There are simpler and shorter ways to do this in scheme, but I wanted a solution that was inspired by chapter 8 of <em>The Little Schemer</em>. The function `fizzbuzz` takes three arguments: a starting number, an ending number, and a function that itself takes three arguments. These arguments will be three numbers, each representing the number occurrences of fizz, buzz, and fizzbuzz, respectively. You could do whatever you wanted to with these numbers. In the example, I just return them as a list.

If I wanted to simplify this, I could create a second function within
`fizzbuzz` that would only take the current number and the function as
arguments, avoiding having to pass `n` as a parameter every single time.
There's a few other things I could do as well, but as I said, this holds pretty
well to the example in chapter 8 of *The Little Schemer.*
