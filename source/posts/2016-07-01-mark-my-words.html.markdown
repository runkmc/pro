---
title: Mark my Words
date: '2016-07-01'
tags: the young person's guide to vim
---
I am going to write three posts about marks in vim in a row without mentioning Marky Mark and the Funky Bunch once. I am a model of self-restraint. READMORE

Hello there, friend. Do you ever find yourself scrolling through your own code, trying to find something you just saw a moment ago? Do you ever forget the name of that variable that just scrolled out of sight? Do you ever lie awake at night, wondering if all consciousness is the product of a single mind, oscillating at such a speed as to seemingly inhabit multiple bodies at once?

If so, you're in luck! I can help you with those first two problems!

The solution to this problem in vim is to use marks. You can set a mark in normal mode by typing `m` followed by any lowercase letter (`ma` to set the mark a). You can then return to this mark by typing either a backtick followed by the letter of the mark (<code>`a</code>) or an apostrophe followed be the letter of the mark (`'a`). I'll go over the difference between those two options in a future post. There are some other things you should know about these marks:

<ul>
	<li>They are local&mdash;that is, the mark exists within only one file at a time</li>
	<li>Since they are local, you can use the same letter to mark places in different files. Mark <code>a</code> in file.rb is a different mark than mark <code>a</code> in file_spec.rb, for example</li>
	<li>They do not persist between vim sessions (by default)</li>
</ul>

So next time you find yourself jumping around a file again and again, consider the lowly mark! As for that third problem, you're on your own.
