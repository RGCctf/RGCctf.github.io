---
layout: post
title: Writeup for n00b15CTF
categories: [CTF, practice,tips]
tags: [CTF,tips, writeup]
fullview: true
---

[Source](http://jaybosamiya.blogspot.be/2015/01/writeup-for-n00b15ctf.html "Permalink to Jay's Blog: Writeup for n00b15CTF")

# Jay's Blog: Writeup for n00b15CTF

This is a collection of hints for all the problems in the recently conducted Capture The Flag (CTF) contest conducted by SDSLabs as a way to get n00bs (beginners) to have a taste of the beautiful world of hacking. It was a pretty fun contest even though it was quite easy.

###  Test

  
Use a SHA256 tool. My favourite is to just search for "SHA256 STRING_TO_BE_SHA256" on my default search engine (www.duckduckgo.com)

###  Location-51

  
There is a redirect occuring here from http://hack.bckdr.in/LOCATION-51/index.html to http://hack.bckdr.in/LOCATION-51/trap.html Stop this redirect, and read the source of index.html The javascript there gives away the flag

###  Hidden flag - Easy

  
Using the file linux command, we find out that it is an ELF binary, but running it gives nothing. However, running strings on it gives away the flag.

###  Search

  
The zip file contains a .txt file which does not seem normal text, so we run a file on it. This says that it is jpeg, so change it to .jpg and open it. It is a QR code. Decode this using some online tool (just search for "QR code decode online" for a large number of free tools) and get a link. The link has the flag.

###  Lost

  
The message says Console, so open up console in Firefox. The message then tells you to POST data to a link. Going to this link directly does nothing, but sending it any random POST data (using HackBar addon in Firefox for example) gives the flag.

###  Hidden flag - Medium

  
Analyzing the file with IDA Pro shows that there is a function called print_flags() which is not called inside main(). Running this function should print the flag. We can do this by attaching gdb to the binary, breaking the execution and running the print_flags() function.

###  Clutter

  
Extracting the file and analyzing with Wireshark shows that there is too much to work with. But exporting all the files and then running strings on it would probably work. However, filtering this is a pain, so I just ran a grep for flag and the answer will be visible near a pastebin title.

###  No - Signal

  
Use GIMP or Photoshop to add the images. The flag should be obvious then.

###  Sound

  
Slow down and reverse the sound wave using Audacity. Listen to it and it should be obvious what the flag is.

###  Sequel

  
Looking at the code, it seems like a SQL injection can be done here. Downloading the database.sdb file and rewriting the source code to start throwing data from database, you realize that there is no user sdslabs in the database. This makes it obvious that you need to add the user. The following username virtually that: ' UNION SELECT 'sdslabs','sdslabs','sdslabs','sdslabs','0c4ea8f5b344600f78516334254e9e085f2225a42a0bb18fa8bd774589f1ca19' UNION SELECT * FROM users WHERE '0'='1. Note that this query will not work directly, the password will have to be set accordingly.

###  Undisputed

  
The file is a ext4 filesystem (use file command if you don't trust the extension). Mount this in linux using the mount command (read man mount to know how) and then open the file inside to see the flag.

Did you find any other cool/new ways of solving any of these tasks? If so, leave a comment below.  