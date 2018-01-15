---
layout: post
title: "Autocomplete from the end"
comments: true
---

## Quick version

I made a bash script that allows one to autocomplete the name of file starting
from the end ; and to use a command on it.

Example :

	2017-09-02-the-quest-of-artificial-intelligence.md
	2017-10-08-sync-files-between-osx-and-linux.md
	2018-01-05-dynamic-programming.md
	2018-01-14-autocomplete-from-the-end.md

Just type

	end-autocomplete vim end

You can find it here :

<https://gist.github.com/GarreauArthur/caf12287a4316c0d3526c855681ac6a9>

## The story (who cares ?)

I recently start this blog using jekyll, and jekyll requires that the names of
the posts start with the date of creation. Which means that I am going to end
up with a lot of files beginning with `2018-`.

I am a vim user, because I am really cool & it's way better than Emacs (let's
start a war for fun).

So everytime I want to edit a draft, or a post, I need to write the complete
date, before being able to autocomplete the rest of the file.

I asked myself :

> Am I doomed to write the date every single time I need to interact with
> these files ?

## wait a minute

The file names don't end with the same letters, so I can just try to type the
end of the file name and autocomplete it from there.

Ok, let's build a bash script for that.

It's not really hard to understand, so if you're interested by it, you can
clone the [gist](https://gist.github.com/GarreauArthur/caf12287a4316c0d3526c855681ac6a9).

## Just a couple of command

	# a short alias is always better
	alias ea='. /path/end-autocomplete.sh'
	# open the file in vim
	ea vim end
	# print the name of the file
	ea echo end
	# copy the file name in the clipboard
	ea echo end | pbcopy # macOS way
	ea echo end | xclip  # the linux way



