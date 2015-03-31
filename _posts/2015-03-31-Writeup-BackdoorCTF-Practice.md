---
layout: post
title: BackdoorCTF Practice
categories: [CTF, practice, tips]
tags: [CTF, practice, tips]
fullview: true
---


## Path

- `dig -t ns flag.bckdr.in`


## Layers

- `624870365a446f764c32527a59587076636d746d4c6e466c5a7938786355524f626d307a51673d3d`
- hex2ascii
- `bHp6ZDovL2RzYXpvcmtmLnFlZy8xcURObm0zQg==`
- base64 decode
- `lzzd://dsazorkf.qeg/1qDNnm3`
- keyed ceasar cypher, swap alphabet characters until you have a valid domain name

## Lost Found

- the git repository includes an commit object located in lost-found
- `git cat-file -p f7cee847b02a589cd3d0fa4e2c32cf9a0ccd94a6`
- this file points to a tree object, that in turn points to a blob named `flag.txt`

# Redirection

- the page includes a form that posts to handle.php
- `curl http://hack.bckdr.in/REDIRECT/handle.php -I`
- handle.php generates a 302 redirect, hiding the request body
- `curl -d "password=foo" http://hack.bckdr.in/REDIRECT/handle.php`

# Search

- search.txt does not seem to be a text file
- `file search.txt`
- this shows us it's a an image with a qr code

# Hidden Flag - Easy

- `strings hide_easy`
- this includes the flag
