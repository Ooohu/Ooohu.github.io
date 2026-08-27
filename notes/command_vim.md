---
layout: page
title: "VIM"
permalink: /notes/command_vim/
---

# 🐵VIM
`vimdiff <fileA.txt> <fileB.txt>`

🐵 Open 2 files with vertical split:
 `vim -O file1 file2` 

🐵 Open 2 files with horizontal split:
 `vim -o file1 file2` 
 
🐵 Only show lines contains the keyword:
```
:vimgrep <keyword> %
:cwindow
```
🐵 Keep [only two words](https://stackoverflow.com/questions/26376855/vim-formula-to-leave-only-two-first-words-in-each-line) of each line, but only words with more than 2 characters could be saved `%norm EElD`

This is more robust `%s/\v^(\s*\S+\s+\S+).+/\1/`

Keep the first field `%s/\v^(\s*\S+\s+).+/\1/`

🐵 sort numbers & remove duplicated: `sort u`

🐵 Paste without comments: `:set paste`
This will turn off auto indent, so turn it back off `:set nopaste`


Use register:
to save a line `"ayy` and paste from the register `"ap`


