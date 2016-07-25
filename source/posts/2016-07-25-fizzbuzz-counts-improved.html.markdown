---
title: FizzBuzz Counts, Improved
date: '2016-07-25'
tags: programming, scheme
tagline: I took a good thing and made it better. Or worse. Still hard to tell.
---

I improved the fizzbuzz solution in scheme from my <a href="/2016/07/17/fizzbuzz-counts.html">previous post</a>. I mentioned
that if I added a second function inside of the main function, I could avoid
passing in the `n` argument over and over again. I don't know if it's a change
for the better but it's definitely.. uh...  different.

~~~scheme
(define fizzbuzz
  (lambda (m n col)
    (letrec
((F (lambda (m col)
    (cond
      ((> m n) (col 0 0 0))
      ((and (zero? (modulo m 5)) (zero? (modulo m 3)))
       (F (add1 m) (lambda (f b fb)
                      (col f b (add1 fb)))))
      ((zero? (modulo m 5)) (F (add1 m) (lambda (f b fb)
                                   (col f (add1 b) fb))))
      ((zero? (modulo m 3)) (F (add1 m) (lambda (f b fb)
                                   (col (add1 f) b fb))))
      (else (F (add1 m) (lambda (f b fb)
                           (col f b fb))))))))
      (F m col))))
                      
(fizzbuzz 5 15 (lambda (f b fb)
         (cons f (cons b (cons fb '())))))
~~~

It's essentially the same, but the `letrec` lets me simplify things somewhat. That's all.
