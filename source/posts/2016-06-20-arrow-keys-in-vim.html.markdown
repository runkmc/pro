---
title: Arrow Keys in Vim
date: '2016-06-20'
tags: the young person's guide to vim
---

One of the things that someone new to vim learns early on is that the usage of your keyboard's arrow keys to move around is a bad thing. Many of you are nodding your heads in silent agreement with me. If you are not, I would ask that you consider the benefits of using the hjkl keys instead of arrow keys for movement with regards to hand placement and overall speed. (Also consider the efficiency of moving only one character/line at a time. That's an entirely different post, altogether. (cue <em>Airplane!</em> joke))

One frequent bit of advice given to the beginning vim user is to remap the arrow keys in their .vimrc so that they are disabled, like so;

~~~viml
nnoremap <Up> <NOP>
nnoremap <Down> <NOP>
nnoremap <Left> <NOP>
nnoremap <Right> <NOP>
~~~

Of course, these mappings only cover normal mode. For completeness, one would do the same for both visual and insert modes as well.

But once we have finally kicked the habit of using arrow keys for movement, is there something more we could do with them? We are left with perfectly functional keys on our keyboards (provided you have not become so devoted to vim that you have hacked them off with a saw) that we are not using. They are like four little vestigial organs, crying out for a chance to be useful once again.

So let's use them! I wanted to find a set of commands where the individual directions would still have some meaning, so I mapped them to tab related commands;

~~~viml
nnoremap <Left> <C-PageUp>
nnoremap <Right> <C-PageDown>
nnoremap <Up> :tabnew<CR> 
nnoremap <Down> :tabc<CR>
~~~

Up and down now open and close tabs while in normal mode, while left and right cycle between them. I rarely use tabs, so having these mappings helps on those occasions when I do desire them. Of course, this is just one possibility. Perhaps you would like to use arrow keys to switch between windows instead of tabs, or maybe you would like left and right to change indentation while up and down <a href="http://vimcasts.org/episodes/bubbling-text/">bubble text</a>. You could also have different functionality assigned to these keys depending on the mode you are in, as well. Truly, the power is yours.
