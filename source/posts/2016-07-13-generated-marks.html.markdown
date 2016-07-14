---
title: Generated Marks
date: '2016-07-13'
tags: the young person's guide to vim
tagline: This concludes my three part saga "Everything you ever wanted to know about marks, but were too afraid to ask."
---

If you've read my previous posts about marks, you know about the different marks that you can set in vim, but did you know that vim sets all sorts of marks for you? READMORE You can see the entire list of them at <code>:help marks</code>. Two excellent and easy to use/understand examples of generated marks are <code>'&lt;</code> and <code>'&gt;</code>.

These two marks represent the beginning of the area last selected in visual mode and the end of the area last selected in visual mode, respectively. You can treat them along with all other auto-generated marks in vim like any other marks. This means you can use them to define ranges in ex commands, so if the range with these two marks, <code>'&lt;,'&gt;</code> rings a bell, it's because that's the range that is automatically inserted when you run an ex command on a visually selected area. I'm pretty sure that vim also uses these two marks to select the previously selected area in visual mode using <code>gv</code>. Don't quote me on that, though.
