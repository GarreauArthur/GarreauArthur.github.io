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

## The story

I recently start this blog using jekyll, and jekyll requires that the names of
the posts start with the date of creation. Which meamns that I am going to end
up with a lot of files beginning with `2018-`.

So everytime I want to edit a draft, or a post, I need to write the complete
date, before being able to autocomplete the rest of the file.

I asked myself :

> Am I doomed to write the date every single time I need to interact with
> these files ?

## wait a minute

The files' names don't end with the same
