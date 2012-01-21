---
layout: post
title: AppleScript and Copying
---

{{ page.title }}
================


 <p class='meta'>21 January 2012</p>
Oh my lord! I cannot begin to tell you how much of a pain I have experienced trying to do the most simple task one can do! What I wanted to do was simply to <b>copy a file</b> to a destination while having a window display the status of the transfer (using Finder's copying window). Seeing as how I've had some experience working on a Mac, the obvious choice is Applescript.

I have a local NFS server that has various files I work with and I wanted to be able to see a window of the file copying to the local file system, on Linux the solution was quite simple however on here the solution was a little obfuscated in Applescript. After several hours of tinkering and tweaking I came up with this:

<i>gcopy</i>
<pre>
	#!/bin/bash

	osascript&lt;&lt;EOF
	tell application &quot;Finder&quot;
	  set sfile to (POSIX file &quot;$PWD/$1&quot;)
	  set sdest to (POSIX file &quot;$2&quot;)
	  duplicate file sfile to folder sdest with replacing
	end tell
	EOF
</pre>

Obviously there's room for a LOT of improvement here. I think that with some assistance from my friend Ruby I might be able to make something really nice, unfortunately Applescript doesn't like me one bit! 

The things to watch out for this difference between Posix paths and HFS Paths (which Applescript) understands. <a href="http://whitefiles.org/b1_s/1_free_guides/fg3mo/pgs/v03.htm">Here is a nice tutorial</a> on dealing with folders in Applescript, as well as the POSIX conversion technique I adopted from <a href='http://en.wikibooks.org/wiki/AppleScript_Programming/Aliases_and_paths'>here</a>.