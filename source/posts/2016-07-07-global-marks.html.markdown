---
title: Global Marks
date: '2016-07-07'
tags: the young person's guide to vim
tagline: In which I continue to refrain from ending all my posts with "Now you're not so ignorant."
---

So <a title="Mark my Words" href="/2016/07/01/mark-my-words.html">last time</a> I talked about how helpful marks are. It's true, they are super helpful, but did you think at any point that marks left something to be desired? READMORE Maybe you'd like them to persist from one vim session to the next. Maybe, instead of having marks be confined to a particular buffer, you'd like to use a single set of marks across all of your files.

<em>I am going to make your dreams come true.</em>

Marks set with a capital letter will behave differently than those set with a lowercase letter in the following ways:

<ul>
	<li>They are global. Each mark will only point to a single location in a single file across your entire filesystem</li>
	<li>They persist betweem vim sessions (by default)</li>
</ul>

So, what are they good for? I use them to quickly open files that exist in only one place. For example, I have the mark <code>V</code> set to the first line of my .vimrc file. I'm sure there are better, more advanced uses, but I am a simple man.

Next time on The Young Person's Guide to Vim, we will look at some of the marks that vim sets for you automatically, as well as the two different ways of jumping to a mark's location.
