---
title: Non-Recursive Macros in Vim
date: '2016-06-25'
tags: the young person's guide to vim
---

Recently, I read a <a href="http://robots.thoughtbot.com/recursive-macros-in-vim">blog post from thoughtbot about recursive macros in vim</a>. As cool as they look, I almost never use them. I have nothing against recursive macros, but I think it's important to note a few other ways to replay a macro multiple times in vim.

Let's look at the problem as presented in the blog post. We have a file that consists of a list of dates like such:

~~~
10/30/2013
11/30/2013
12/30/2013
...
~~~

We want to change the file so that each line contains the date in two formats:

~~~
10/30/2013 : 10-30-2013
11/30/2013 : 11-30-2013
12/30/2013 : 12-30-2013
...
~~~

If that's all that's involved, a recursive macro is a pretty good way to go. But what if our macro doesn't apply to each and every single line in a file? What if, perchance, our consecutive lines of dates were occasionally interrupted by medieval English poetry?

~~~
10/30/2013
11/30/2013
12/30/2013
Sumer is icumen in, lhude sing cuccu!
01/30/2014
02/28/2014
03/30/2014
~~~

Ha ha. How delightfully humorous. Our large list of dates could have multiple lines with comments, or blank lines, or any other number of things that could cause our macro to fail. As soon as a motion fails (in the case of the macro presented in the blog post, this would be the motion <span class="code-sample">F/</span>), the macro will end and we'll have to restart it. If that happens more than a few times, things can get pretty tedious. So what do we do? I'm going to highlight two different ways of running a macro multiple times.

The first is fairly simple. The command to invoke a macro in vim can take a count. If the macro we want to run multiple times is in the q register, we can use <span class="code-sample">&lt;count&gt;@q</span> to run the command <span class="code-sample">&lt;count&gt;</span> number of times. The upside to this technique is that we can control the number of times a macro is run. There are a few downsides, though. We still need to have the macro set itself up to run the next iteration of itself, so we really don't save any work compared to a recursive macro. This method will also abort if it runs into an error like a failed motion, just like recursive macros do. Again, we have just as much work to do after a failed macro as we do with a recursive macro, if not more. Running a macro multiple times by giving it a count is the most common way I use macros because it's easy and quick when I need to use it on just a few lines or a few regions, but for our particular problem, it's less than ideal.

Luckily for us, there is a way we can run the macro exactly once for the entire file no matter how many interruptions there are. Not only that, but we can simplify the macro at the same time. Here is the macro as presented in the original blog post: <span class="code-sample">y$A&lt;Space&gt;:&lt;Space&gt;&lt;Escape&gt;pF/r-;.^j@q</span>. It yanks, puts, and then reformats the date. Our new macro would look the same, except for the last four characters -- moving the cursor to the beginning of the next line and invoking the macro recursively. We don't need them. It's a small simplification, but not totally insignificant, especially if setting ourselves up for the next macro was more involved than just going to the beginning of the next line.

So now we've got a macro that doesn't set itself up for the next iteration. We can only run it one line at a time. So how do we run this on the entire file? Like so: <span class="code-sample">:g/^\d/normal @q</span>. Let's unpack this. The <span class="code-sample">:g</span> command takes a pattern and a command. For every line that matches the pattern, the command is run on that particular line. Our pattern here will match every line that starts with a number. The rest of the command invokes the normal mode command <span class="code-sample">@q</span> -- our macro. Our macro runs on every matched line, and we only needed to do it once.
