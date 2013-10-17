
Grammar:
===

### Verbs
- Indicate what you want to do ie actions you want to take
  - **d** : Delete
  - **c** : Change
  - **v** : visual mode, **V** for visual line mode
  - **y** : Yank (copy)

### Modifiers
- Modifers indicate how you want to take action.
  - **i** : inside
  - **a** : around
  - **t** : till, finds a character and stops just before it
  - **f** : find, finds a character and stop right on top of it
  - **/** : find a string or use a regex (foward-slash)

### Objects/Subjects
- Represents object acted upon.
  - **w** : word
  - **s** : sentence or **)** 
  - **p** : paragraph
  - **b** : block/parentheses
  - **t** : xhtml tags

In vim (language), we can combine `verbs`+`modifiers`+`objects` to perform
efficient actions in vim:

- **diw** : delete inside word (inside means the word you are in)
- **yis** : yank(copy) contents inside sentence
- **cit** : change the contents inside tags
- **ci"** : change inside quotes
- **dat** : delete around tags
- **yt'** : yank(copy) till(before) the **'** character
- **c/<** : Change till the occurance of {
- **vap** : Visually select tags you are in 
- **vi{** : Select function blocks in c-style language


Tips:
===

### Read help for a command

`:help <command>` show help info for a command

### Reload vim config:

* ` :tabedit ~/.vimrc ` and do ` :so % ` where `%` stands for current file
(better yet, make a mapping for it)
* `:tabedit $MYVIMRC` [[src]](http://dailyvim.blogspot.com/2008/11/reload-vimrc.html)

### Edit file in new tab:

`:tabedit file.html`

### Cut and paste(visual mode):

* Position the cursor where you want to begin cutting.
* Press `v` (or upper case `V` if you want to cut whole lines).
* Move the cursor to the end of what you want to cut.
* Press `d`.
* Move to where you would like to paste.
* Press `p` to paste after the cursor, or `P` to paste before.

### Copy using marks:
1. Go to start location and set mark using `ma` where `a` is the marker.
2. Then go to end location and type `y'a` to yank from line containing `a` to
  the end location line(the line from where you rank the yank command).
3. OR to yank to the precise point where mark was set, use `` ` `` instead
  of `'`

### Cut a paragraph:
`{d}` : `{` moves to the start of paragraph,`d` starts deletion and `}` ends
deletion at end of paragraph.

### Change case:
* Enter visual mode
* Select the text
* Use `U` for uppercase or `u` for lower

### Word motion:
* `b` to go to beginning of current or previous word
* `w` to go the beginning of next word
* `e` to go to the end of current or next word
* `:22` - go to line 22

### Tab motion:
* `gt` = next tab
* `gT` = previous tab

### Copy to clipboard:
* `gg"*yG` - Copy whole file to clipboard
* `"*y$` - Copy to the end of the line in clipboard


### Switch files:
* `Ctrl-6` to switch between files
* Press `gf`while cursor on a file path to go to a file
* `:bf` to go back to previous file
* `Ctrl-o` go to previous curson position

### Tabs:
* `t`- opens selected files in tab
* `:tabm n` - moves tab to n-th position(base 0), short for :tabmove
* `:h word-motions` for more


### Join lines:

`2J` to join 2 lines.

### Window management:
* `ctrl+ws` - Split windows
* `ctrl+ww` - switch between windows
* `ctrl+wq` - Quit a window
* `ctrl+wv` - Split windows vertically

### Moving windows around:

Combination `Ctrl+w+` `J`,`K`,`L`,`M` moves the window around. [[src]](http://stackoverflow.com/questions/2586984/how-can-i-swap-positions-of-two-open-files-in-splits-in-vim/2591946#2591946)

### Go to right end of line/quote while in insert mode:

In insert more,`Ctrl-o` immediately followed by `A`
[[src]](http://stackoverflow.com/a/11118130)

### Find and replace a word in vim:
* to replace first occurrence of OLD to NEW on current line `:s/OLD/NEW`
* to replace all occurrence of OLD to NEW on current line `:s/OLD/NEW/g`
* to replace all occurrence of OLD to NEW between two line numbers (# are the line numbers) `:#,#s/OLD/NEW/g`
* to replace every occurrence of OLD to NEW on current file `:%s/OLD/NEW/g`

[[src]](http://linuxwave.blogspot.com/2008/05/replacing-words-in-vi.html)

### Turnoff highlight after a search is done

`:nohl` Turns off highlight of a previous search if using `set hlsearch` in .vimrc

### To search and replace value under the cursor:

`:%s/<c-r><c-w>/new value/g` where `<c-r><c-w>` means to literally type `<ctrl-r><ctrl-w>` to insert the word under the cursor.

### Folds:
* Disable using `:set nofoldenable`
* `za` - toggles
* `zc` - closes
* `zo` - opens
* `zR` - open all
* `zM` - close all
[[src]](http://smartic.us/2009/04/06/code-folding-in-vim/)

### Insert text inside tag:
Place cursor in the line and pres `cit`(change inside tag)

### Select/Paste inside tag:

`vit` (select visually inside tag) **or** `vitp` (select visually inside tag and paste)

### Delete contents inside tag:
`dit` (delete inside tag)

### Delete surrounding tag:
`dst` (delete surrounding tag)
Deletes a tag, leaving behind only surrounding elements

### Delete from current position upto (and including) a character:
`dfx` (delete upto and including `x`, `f` stands for find) where `x` is a character

### Delete until(excluding) a character:
`dtx` (delete till `x`) where `x` is a character

### Delete mistyped word:
`<C-w>` will delete a word just mistyped.[[src]](http://stackoverflow.com/a/1737259)

### Record a macro:

1. Press `q` to start recording.
2. Then press any letter to use as a register for the recording `(say a)`.
3. Type commands you wish to record.
4. Press `q` again to stop recording.
5. Play the recording using `@a`.

### Run a macro on selected line: 

`:5,10norm! @a` which runs the macro stored in register `@a` from line `5` to `10` in normal mode. [[src]] (http://stackoverflow.com/a/390194)

### Run last macro:

`@@`

### Jumping locations:

`Ctrl o` jumps backward to previous cursor location
`Ctrl i` jumps forward to newer cursor location

### Paste over to inner contents:

`vitp` Select content inside tag in visual mode and paste over (replace) earlier content to it.

See `:help text-objects`

### Moving within the screen(viewing area)
- **M** : move to the middle of the screen
- **L** : move to the end of the screen

### Move to matching parentheses:
- `%` : moves to matches parentheses `([{}])`

### Indent code inside parentheses
- `>%` or `<%`

### References
http://stackoverflow.com/questions/1218390/what-is-your-most-productive-shortcut-with-vim/1220118#1220118
http://danielmiessler.com/study/vim/


[Sparkup](https://github.com/rstacruz/sparkup):
===

### Expansion key: 
`<Ctrl-e>`

### Repeat an element n times

`td*n` repeats the tag `n` time
So pressing `td*3` and expansion key will produce:

```html
<td></td>
<td></td>
<td></td>
```

[Surround:](https://github.com/tpope/vim-surround)
===
1. Select the letter, word or line in visual mode.
2. Press `S`
3. Press character to surround with
