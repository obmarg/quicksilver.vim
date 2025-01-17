Quicksilver
===========

Quicksilver is a VIM plugin whose purpose is to quicken the process of
opening files from inside VIM.

The original version of this plugin can be found at
https://github.com/Bogdanp/quicksilver.vim

This is a fork by Grambo which:
* Adds support for running under python 2.5
* Adds support for more than basic functionality on windows
* Allows automatic filtering out of certain files from the list (see Settings)
* Fixes a bug with entering directories with spaces in them

# Preview

[Video](http://www.youtube.com/watch?v=RDsey4YqpHs)

![Screenshot](http://farm4.static.flickr.com/3383/5804126014_072806d823_z.jpg)

# Installation

Use [pathogen][1] and clone this repo into your ~/.vim/bundle directory.

# Settings

The `g:QSFilter` setting enables filtering out of certain files from 
the quicksilver list.  It matches based on simple filepattern matching, 
with entries seperated by a semi-colon.

For example, to exclude `.pyc` and `.o` files:
```let g:QSFilter="*.pyc;*.o"```

The `g:QSFilterByMime` option allows more automated filtering of files.
It filters out files from the quicksilver list based on their mimetype.  
Only files with a text/* type (or directories) will be displayed.
This option is not perfect, as it will currently also filter out files
for which the mime type can not be detected, which may also be text

To Enable:
```let g:QSFilterByMime = 1```

# Usage

By default, `\q` will activate the Quicksilver buffer and switch to
insert mode. Typing any key will update the list of suggestions and
pressing `CR` will open the first item in the suggestion list. Use `C-c`
to quickly close the buffer.

You may cycle through the suggestion list using `Tab` and `S-Tab`. `CR`
will open the current suggestion (first item in the list).

If there is only one item in the suggestion list, pressing `Tab` will
open that item.

Pressing `CR` when there is no pattern will go up a directory.

`C-w` clears the entire pattern. If there is no pattern, it will go up a
directory.

`C-t` toggles between if pattern and filename case should be ignored or
not.

`C-f` turns on `fuzzy matching`. Fuzzy matching will match any filename
that contains every character in the given pattern, no matter the order
of the characters. For example: the pattern `foo` will match `foo`, as
well as `oof`, `ofo` and `foob`.

`C-n` turns on `normal matching`. Normal matching will match any
filename that contains the exact phrase within it. For example: the
pattern `foo` will match `foo` and `foob` but not `ofo` or `oof`.

If you prefer fuzzy matching and would like Quicksilver to default to it
instead of normal matching then you can add `let g:QSMatchFn = 'fuzzy'`
to your `.vimrc`.

If a file with the given pattern does not exist then a new file will be
opened for editing with the given pattern as its filename. If a pattern
ends in `/`, quicksilver will create a new folder, change its CWD to
that folder and remain in insert mode expecting a file name.

Patterns that start or end in a wildcard (`*`) are treated as glob
patterns. For example, the pattern `*.md` will open all the files that
have the extension `.md` in the CWD.

# Requirements

* VIM 7.0+ compiled with +python
* Python 2.5+

[1]: http://github.com/tpope/vim-pathogen
