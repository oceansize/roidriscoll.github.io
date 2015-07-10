---
layout: post
title: "Seeing is Believing"
date: 2014-06-21 10:55:07 +0100
comments: true
categories: gems articles tutorials
---

Since embarking on my programming journey, I have to admit - I have gone a
little gem-crazy. It's just so EASY to type 'gem install the_promise_of_magic'.
I think that's one of the more dangerous aspects of living in the command line.
When I'm considering installing something via the browser, there are a multitude
of clues to help you ascertain whether or not a binary is legit, not least how
polished their site looks.

<!--more-->

There is also a kind of false sense of security that can set in when you've been
a Mac user for your entire adult life, and have not traditionally had much cause
to worry about virus issues etc- so to just type three words into your iTerm and
wait for your latest library to make itself comfortable in your filesystem takes
little effort. This is something I have noticed and am now very mindful of - but
I digress...

This post is really to draw your attention to a frankly wonderful wee gem I
found this week, called 'Seeing Is Believing', developed by [Mr Josh
Cheek](http://joshcheek.com/seeing_is_believing). Based on an existing gem
called [rcodetools](https://rubygems.org/gems/rcodetools), it automagically
places a comment at the end of each line of ruby code containing the evaluation.
Pretty friggin' useful for a beginner. You can see a video of this little beaut
being demonstrated [here](http://vimeo.com/73866851).

So how could this be even better Roi? How about Sublime Text integration? [Ding
Dong!](https://github.com/JoshCheek/sublime-text-2-seeing-is-believing) (Josh
also supports Textmate 1-2 and Vim)

There is one wee-tiny-little catch - if you're new at this stuff, the
documentation is a little bit sparse (I found the whole rvm wrapper thing a bit
mysterious to say the least), so I thought I would do a quick write-up. Now bear
in mind that I work with a ruby version of 2.1.1 on a mac using rvm [Ruby
Version Manager](https://rvm.io/rvm/basics) so I can only tell you what worked
for me, and this is it.

First one must install the gem:
```
gem install seeing_is_believing
```
Then you need to navigate to the following folder:
```
cd ~/Library/Application\ Support/Sublime\ Text\ 2/Packages
```
and inside of that directory, clone this repo:
```
git clone git://github.com/JoshCheek/sublime-text-2-seeing-is-believing.git
SeeingIsBelieving
```
If this is confusing for you, I would recommend researching into how to navigate
your file system using the [command
line](http://learncodethehardway.org/cli/book/cli-crash-course.html) and basic
usage of [Git](https://try.github.io).
Next up, you need to make a wrapper for Sublime (this is the bit that I found
confusing), and for this you need to know which version of ruby you are
currently running. On my setup, I can type `ruby -v` and am rewarded with the
output:
```
ruby 2.1.1p76 (2014-02-24 revision 45161) [x86_64-darwin12.0]
```
I take the section `ruby 2.1.1` and type the following into Terminal:
```
rvm wrapper ruby-2.1.1 sublime
```
Now, at this point you need to run the following command in terminal : `which
sublime_ruby`, which will return a line like this:
`/Users/your-username/.rvm/bin/sublime_ruby`
At this point, you need to open 'SeeingIsBelieving/Seeing Is
Believing.sublime-settings' in Sublime Text and comment out the line
`"RBENV_VERSION": "2.0.0-p0"` and the MOST important part: delete
`"ruby_command": "~/.rbenv/shims/ruby",` and replace with the following:

```
"ruby_command": "~/.rvm/bin/sublime_ruby",
```
where the line `"~/.rvm/bin/sublime_ruby",` matches the line you got when you
typed in `which sublime_ruby` - remember that? ;)

Restart Sublime Text, and enter some ruby code:
```ruby
10.times do |i|
  i * 2
end
```
Now if you hit the pre-defined keyboard shortcut (⌥ + ⌘ + B on OS X) or run the
command:
```
Evaluate Ruby code with Seeing Is Believing
```
from your command pallete (⌘ + ⇧ + P), you should see the following output:
```
10.times do |i|
  i * 2          # => 0, 2, 4, 6, 8, 10, 12, 14, 16, 18
end              # => 10
```
To remove the comments, run `Remove Seeing Is Believing annotations` or press (⌥
+ ⌘ + V on OS X). And you are back to the original.

Well there you have it - instant win! I strongly suggest that you take the time
to watch Josh's video (and browse the documention I linked to earlier) - I have
directly referenced a lot of the material for this article and I cannot
recommend this enough as a tool to get your head around what ruby is doing when
it evaluates your code.

Happy coding! ^_^
