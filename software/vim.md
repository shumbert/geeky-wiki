# Links
- https://vimawesome.com/
- vimhelp.org
- https://vim.fandom.com/wiki/Vim_Tips_Wiki
- http://vimcasts.org
- https://www.vim.org/
- https://neovim.io/
- https://neovim.io/doc/user/index.html

# Cheatsheet
## Some notes
### File buffers
- Buffers status flags
  - u: unlisted buffer (:ls doesn’t show it but :ls! will show it)
  - % or (mutually exclusive) #: % is the buffer for the current window. # is the buffer to which you would switch with the :edit # command
  - a or (mutually exclusive) h: a indicates an active buffer. That means the buffer is loaded and visible. h indicates a hidden buffer. The hidden buffer exists but is not visible in any window
  - \- or (mutually exclusive) =: - means that a buffer has the modifiable option turned off. The file is read-only. = is a read-only buffer that cannot be made modifiable
  - \+ or (mutually exclusive) x: + indicates a modified buffer. x is a buffer with read errors

### Edition buffers
- The last nine deletions are stored by vi in numbered buffers. The last delete is saved in buffer 1, the second-to-last in buffer 2, and so on. Small deletions, of only parts of lines, are not saved in numbered buffers, however.
- In case you paste content from numbered buffers, using the repeat command (.) will automatically increment the buffer number.

### Text objects selection
- This is a series of commands that can only be used while in Visual mode or after an operator.

## Command-line options
Option | Description
-------|------------
vim +\<n\> \<file\> | Open file at line number n
vim + \<file\> | Open file at last line
vim +/\<pattern\> \<file\> | Open file at first occurrence of pattern
vim -R \<file\> | Open file in read-only mode
vim -r | List swap files
vim -r \<file\> | Recover file
vim -o \<f1\> \<f2\> \<f3\> | Open f1, f2 and f3 using horizontal windows
vim -o 5 \<f1\> \<f2\> \<f3\> | Open vim with 5 horizontal windows, topmost will contain f1, second one will contain f2 and third one will contain f3
vim -O \<f1\> \<f2\> \<f3\> | Open f1, f2 and f3 using vertical windows
vim -p \<f1\> \<f2\> \<f3\> | Open f1, f2 and f3 using tabs
vim scp://\<user\>@\<host\>:\<port\>/\<file\> | Open file on remote host (file is either a filename or a relative path relative to user home directory)
vim scp://\<user\>@\<host\>:\<port\>/\<path\> | Open file on remote host (path is an absolute path)

## Basic commands
### Motion
Command | Description
--------|------------
[\<count\>]h | Move left
[\<count>\]j | Move down
[\<count\>]k | Move up
[\<count\>]l | Move right
[\<count\>]\<ENTER\> | Move to first nonblank character of next line
[\<count\>]+ | Move to first nonblank character of next line
[\<count\>]- | Move to first nonblank character of previous line
[\<count\>]gj | Move down one screen line
[\<count\>]gk | Move up one screen line
[\<count\>]w | Move to the start of next word
[\<count\>]W | Move to the start of next white-space separated word
[\<count\>]b | Move to the start of previous word
[\<count\>]B | Move to the start of previous white-space separated word
[\<count\>]e | Move to the end of next word
[\<count\>]E | Move to the end of next white-space separated word
[\<count\>]ge | Move to the end of previous word
[\<count\>]gE | Move to the end of previous white-space separated word
[\<count\>]$ | Move to the end of the line
^ | Move to the first nonblank character of the line
0 | Move to the very first character of the line
\<count\>\| | Move to column count of current line
[\<count\>]( | Move to beginning of current sentence
[\<count\>]) | Move to beginning of next sentence
[\<count\>]{ | Move to beginning of current paragraph
[\<count\>]} | Move to beginning of next paragraph
gg | Move to beginning of the file
G | Move to the end of the file
\<count\>G | Move to line count
\<count\>% | Move to count percents within the file
% | Move to the matching paren (also works for [] and {} pairs, if the cursor is not on a useful character % will search forward to find one)
`` | Jump back to previous position
‘’ | Jump back to beginning of the line of previous position
[\<count\>]H | Move to first line on the screen (or count lines below top line if provided)
M | Move to middle of the screen
[\<count\>]L | Move to last line on the screen (or count lines above bottom line if provided)
[\<count\>]zt | Move current line (or line count if provided) at the top of the screen
[\<count\>]z\<ENTER\> | Move current line at the top of the screen
[\<count\>]zz | Move current line at the middle of the screen
[\<count\>]z. | Move current line at the middle of the screen
[\<count\>]zb | Move current line at the bottom of the screen
[\<count\>]z- | Move current line at the bottom of the screen
[\<count\>]CTRL-E | Scroll down one line in the file
[\<count\>]CTRL-Y | Scroll up one line in the file
[\<count\>]CTRL-F | Scroll down one screen in the file
[\<count\>]CTRL-B | Scroll up one screen in the file

### Edition
Command | Description
--------|------------
[\<count\>]A | Put Vim in Insert mode after the last character on the line
[\<count\>]a | Put Vim in Insert mode after the character under the cursor
[\<count\>]C | Delete to end of the line and put Vim in Insert mode
[\<count\>]c\<motion\> | Delete and put Vim in Insert mode
[\<count\>]cc | Delete current line and put Vim in Insert mode
[\<count\>]D | Delete to end of the line
[\<count\>]d\<motion\> | Delete
[\<count\>]dd | Delete current line
[\<count\>]I | Put Vim in Insert mode before the first non blank character on the line
[\<count\>]i | Put Vim in Insert mode before the character under the cursor
[\<count\>]J | Join two lines
[\<count\>]O | Create a new empty line above the cursor and put Vim in Insert mode
[\<count\>]o | Create a new empty line below the cursor and put Vim in Insert mode
[\<count\>]P | Paste text before the cursor
[\<count\>]p | Paste text after the cursor
[\<count\>]R | Enter replace mode
[\<count\>]r | Replace character under the cursor
[\<count\>]S | Substitute whole lines (equivalent to cc)
[\<count\>]s | Substitute a single character (equivalent to cl)
[\<count\>]X | Delete character before the cursor
[\<count\>]x | Delete character under the cursor
[\<count\>]Y | Copy current line (equivalent to yy)
[\<count\>]y\<motion\> | Copy
[\<count\>]yy | Copy current line
[\<count\>]~ | Change case of single character
[\<count\>]gu\<motion\> | Put text in lowercase
[\<count\>]guu | Put current line in lowercase
[\<count\>]gU\<motion\> | Put text in uppercase
[\<count\>]gUU | Put current line in uppercase
[\<count\>]. | Repeat the last change
[\<count\>]u | Undo the last edit
U | Undo all changes on the last line that was edited
[\<count\>]CTRL-R | Redo
!\<motion\>\<cmd\> | Filter text from current cursor position to end of motion through external program cmd
!!\<cmd\> | Filter current line through external program cmd
[\<count\>]\<\< | Decrease current line indent
[\<count\>]\>\> | Increase current line indent
CTRL-A | Increment number under cursor
CTRL-X | Decrement number under cursor

### Search
Command | Description
--------|------------
/\<pattern\> | Search forward for pattern
?\<pattern\> | Search backward for pattern
\* | Search forward for the next occurrence of word under cursor
\# | Search backwards for the next occurrence of word under cursor
n | Repeat search in same direction
N | Repeat search in opposite direction
/\<ENTER\> | Repeat search forward
?\<ENTER\> | Repeat search Backward
c/\<pattern\> or c?\<pattern\> | Change until pattern
d/\<pattern\> or d?\<pattern\> | Delete until pattern
y/\<pattern\> or y?\<pattern\> | Copy until pattern
[\<count\>]f\<character\> | Move cursor to next occurrence of character on current line
[\<count\>]F\<character\> | Move cursor to previous occurrence of character on current line
[\<count\>]t\<character\> | Move cursor before next occurrence of character on current line
[\<count\>]T\<character\> | Move cursor after previous occurrence of character on current line
[\<count\>]; | Repeat previous move command in same direction
[\<count\>]’ | Repeat previous move command in opposite direction
cf\<character\> or cF\<character\> or ct\<character\> or cT\<character\> | Change until character
df\<character\> or dF\<character\> or dt\<character\> or dT\<character\> | Delete until character
yf\<character\> or yF\<character\> or yt\<character\> or yT\<character\> | Copy until character

### Patterns
Pattern | Description
--------|------------
. | Match any single character except a newline
\* | Match zero or more (as many as there are) of the single character that immediately precedes it
^ | When used at the start of a regular expression, require that the following regular expression be found at the beginning of the line
$ | When used at the end of a regular expression, require that the preceding regular expression be found at the end of the line
[ ] | Match any one of the characters enclosed between the brackets
~ | Match whatever regular expression was used in the last search
[:alnum:] | POSIX character class for alphanumeric characters
[:alpha:] | POSIX character class for alphabetic characters
[:blank:] | POSIX character class for space and tab characters
[:cntrl:] | POSIX character class for control characters
[:digit:] | POSIX character class for numeric characters
[:graph:] | POSIX character class for printable and visible (nonspace) characters
[:lower:] | POSIX character class for lowercase characters
[:print:] | POSIX character class for printable characters (including whitespace)
[:punct:] | POSIX character class for punctuation characters
[:space:] | POSIX character class for whitespace characters
[:upper:] | POSIX character class for uppercase characters
[:xdigit:] | POSIX character class for hexadecimal digits
\ | Treat the following special character as an ordinary character (characters that need to be escaped are .*[]^%/\?~$)
\\( \\) | Provide grouping for *, \+, and \=, as well as making matched subtexts available in the replacement part of a substitute command (\1, \2, etc.)
\\< \\> | Match characters at the beginning or at the end of a word
\c | Special marker for making a case insensitive pattern (must be at the beginning of the pattern)
\\\| | Alternation
\\+ | Match one or more of the preceding regular expression
\\= | Match zero or one of the preceding regular expression
\\{n,m} | Match n to m of the preceding regular expression, as much as possible
\\{n} | Match n of the preceding regular expression
\\{n,} | Match at least n of the preceding regular expression, as much as possible
\\{,m} | Match 0 to m of the preceding regular expression, as much as possible
\\{} | Match 0 or more of the preceding regular expression, as much as possible (same as *)
\\{-n,m} | Match n to m of the preceding regular expression, as few as possible
\\{-n} | Match n of the preceding regular expression
\\{-n,} | Match at least n of the preceding regular expression, as few as possible
\\{-,m} | Match 0 to m of the preceding regular expression, as few as possible
\i | Match any identifier character, as defined by the isident option
\I | Like \i, but excluding digits
\k | Match any keyword character, as defined by the iskeyword option
\K | Like \k, but excluding digits
\f | Match any filename character, as defined by the isfname option
\F | Like \f, but excluding digits
\p | Match any printable character, as defined by the isprint option
\P | Like \p, but excluding digits
\s | Match a whitespace character (exactly a space or a tab)
\S | Match anything that isn’t a space or a tab
\b | Match Backspace
\e | Match Escape
\r | Match Carriage Return
\t | Match Tab
\\\<n> | Matches the same string that was matched by the first subexpression in \\( and \\)

### Replacement strings
Pattern | Description
--------|------------
\\\<n\> | Replace with the text matched by the nth pattern previously saved in a holding space
\\ | Treat the following special character as an ordinary character
& | Replace with the entire text matched by the search pattern when used in a replacement string
~ | Replace with the replacement text specified in the last substitute command
\u or \l | Change the next character in the replacement string to uppercase or lowercase, respectively
\U or \L and \E or \e | All following characters are converted to uppercase or lowercase until the end of the replacement string or until \e or \E is reached

### Visual mode
Command | Description
--------|------------
v | Start visual mode
V | Start visual mode on whole lines
CTRL-V | Start visual block mode
gv | Start visual mode with the previous selected area
o | Move cursor to the other end of the selection
\> | Shift text to the right
\< | Shift text to the left
I | (visual block only) Insert text on each line, just left of the visual block
A | (visual block only) Append text on each line, just right of the visual block (special case: if $ has been use to expand block till end of line, text will be inserted at the end of each line)
c | (visual block only) Delete text from left edge of the block to the end of line then put Vim in Insert mode. Text will be added to the end of each line
: | (visual block only) Will go to Ex command mode with pre-filled address :'<,'> which matches boundary of the visual block

## More advanced stuff
### Text object Selection
Command | Description
--------|------------
iw | A word
aw | A word and white space that follows
is | A sentence
as | A sentence and white space that follows
ip | A paragraph
ap | A paragraph and white space that follows
i[ or i] | A [] block, not including [ and ]
a[ or a] | A [] block, including [ and ]
i( or i) or ib | A () block, not including ( and )
a( or a) or ab | A () block, including ( and )
i< or i> | A <> block, not including < and >
a< or a> | A <> block, including < and >
it | A tag block, not including <aaa> and </aaa>
at | A tag block, including <aaa> and </aaa>
i{ or i} or iB | A {} block, not including { and }
a{ or a} or aB | A {} block, including { and }
i" | A "" quoted string, not including the quotes
a" | A "" quoted string, including the quotes
i' | A '' quoted string, not including the quotes
a' | A '' quoted string, including the quotes
i` | A `` quoted string, not including the quotes
a` | A `` quoted string, including the quotes

### Insertion mode commands
Command | Description
--------|------------
\<Left\> | Move left
\<Down\> | Move down
\<Up\> | Move up
\<Right\> | Move right
CTRL-<Home\> | To start of the file
\<PageUp\> | A whole screenful up
\<Home\> | To start of line
SHIFT-\<Left\> | One word left
CTRL-\<Left\> | One word left
SHIFT-\<Right\> | One word right
CTRL-\<Right\> | One word right
\<End\> | To end of the line
\<PageDown\> | A whole screenful down
CTRL-\<End\> | To end of the file
\<Del\> | Delete character under the cursor
\<Backspace\> | Delete character before the cursor
CTRL-@ | Insert text from previous insertion and exit Insert mode
CTRL-A | Insert text from previous insertion
CTRL-E | Insert character below the cursor
CTRL-N | Word completion based on next match
CTRL-O \<cmd\> | Execute command cmd from normal mode
CTRL-P | Word completion based on previous match
CTRL-R \<reg\> | Insert content of register reg
CTRL-U | Delete line before the cursor (except indent)
CTRL-W | Delete word before the cursor
CTRL-Y | Insert character above the cursor

### Buffers, tabs & windows
Command | Description
--------|------------
:bad[d] \<file\> | Add file to list
:ba[ll] | Edit all args and buffers
:bd[elete] \<n\> | Delete buffer n
:bf[irst] | Move to first buffer
:bl[ast] | Move to last buffer
:bN[ext] \<n\> | Go to nth previous buffer in buffer list
:bn[ext] \<n\> | Go to nth next buffer in buffer list
:bp[revious] \<n\> | Go to nth previous buffer in buffer list
:bufdo \<cmd\> | Execute cmd on all buffers (including hidden buffers)
:b[uffer] \<n\> | Edit buffer n
:buffers | List buffers
:bun[load] | Unload buffer from memory
:clo[se] | Close current window
:files | List buffers
:hid[e] | Quit current window and hide the buffer if no other window references it
:ls | List buffers
:new | Split the current window horizontally and open the new window on a new file
:on[ly] | Close all windows except the current one
:qa[ll] | Close all windows and quit Vim
:sb[all] | Edit all args and buffers in new windows
:sbf[irst] | Edit first buffer in a new window
:sbl[ast] | Edit last buffer in a new window
:sbN[ext] \<n\> | Edit nth previous buffer in new window
:sbn[ext] \<n\> | Edit nth next buffer in new window
:sbp[revious] \<n\> | Edit nth previous buffer in new window
:sb[uffer] \<n\> | Edit buffer n in a new window
:sp[lit] | Split the current window horizontally and show the same buffer in both windows
:sp \<file\> | Split the current window horizontally and open file in new window
:sun[hide] | Edit all loaded buffers in new windows
:tab split | Open a new tab with current file
:tabc[lose] | Close current tab
:tabe[dit] \<file\> | Open file in a new tab
:tabnew | Open a new tab with an empty file
:tabo[nly] | Close all tabs except current one
:un[hide] | Edit all loaded buffers
:vne[w] | Split the current window vertically and open the new window on a new file
:vs[plit] | Split the current window vertically and show the same buffer in both windows
:vs \<file\> | Split the current window vertically and open file in new window
:wa[ll] | Write changes in all windows
:windo \<cmd\> | Execute cmd on all windows
:wn[ext] | Save current file and move to next file in a sequence of files
:wp[revious] | Save current file and move to previous file in a sequence of files
CTRL-W = | Try to resive all windows to equal size
CTRL-W + | Increase the current window height by one line
CTRL-W - | Decrease the current window height by one line
CTRL-W \> | Increase the current window width by one character
CTRL-W \< | Decrease the current window width by one character
CTRL-W H | Move current window to the far left
CTRL-W J | Move current window to the bottom
CTRL-W K | Move current window to the top
CTRL-W L | Move current window to the far right
CTRL-W R | Rotate windows to the left or to the top
CTRL-W W | Cycle through windows going above or to the left
CTRL-W b | Move cursor to the bottom rightmost window
CTRL-W c | Close current window
CTRL-W h | Move cursor to the window on the left
CTRL-W j | Move cursor to the window below
CTRL-W k | Move cursor to the window above
CTRL-W l | Move cursor to the window on the right
CTRL-W n | Split the current window horizontally and open the new window on a new file
CTRL-W o | Close all windows except the current one
CTRL-W p | Move cursor to the previous (last accessed) window
CTRL-W q | Quit current window
CTRL-W r | Rotate windows to the right or to the bottom
CTRL-W s | Split the current window horizontally and show the same buffer in both windows
CTRL-W t | Move cursor to the top leftmost window
CTRL-W v | Split the current window vertically and show the same buffer in both windows
CTRL-W w | Cycle through windows going below or to the right
gt | Go to next tab
gT | Go to previous tab

### Diffing
Command | Description
--------|------------
vimdiff \<f1\> \<f2\> | Start Vim in diff mode on f1 and f2
:diffsplit \<file\> | Start diff mode on currently edited file and file
:vert[ical] diffsplit \<file\> | Start diff mode on currently edited file and file (using vertical split)
zo | Open a fold
zc | Close a fold
]c | Jump to next change
[c | Jump to previous change
dp | "diff put": put the text of the current window in the other window
do | "diff obtain": get the text from the other window
:diffu[pdate] | Update highlighting after removing differences

### Browser
Command | Description
--------|------------
:e[dit] . | Start browser in current directory
CTRL-O | Go back to browser after editing a file
i | Control listing style (thin, long, wide, and tree).
o | Horizontally split window and display file
P | Edit in the previous window
p | Use the preview-window
r | Reverse the sorting order
s | Change the way the files are sorted; one may sort on name, modification time, or size
t | Open file in a new tab
v | Vertically split window and display file
/\<pattern\> | Search forward for pattern in the list of files/directories
?\<pattern\> | Search backward for pattern in the list of files/directories

### Misc
Command | Description
--------|------------
q: | Open command-line window
\<CTRL\>-G | Show where you are in a file
\<CTRL\>-L | Redraw screen
\<CTRL\>-^ | Switch back to previous file
\<Insert\> | Switch between Insert and Replace mode
"\<letter\>\<cmd\> | Store text resulting from cmd (delete, change or yank operator) in named buffer letter
"\<LETTER\>\<cmd\> | Append text resulting from cmd (delete, change or yank operator) in named buffer letter
"\<letter\>p | Paste content of named buffer letter
"\<number\>p | Paste content of numbered buffer number
q\<letter\> | Start recording a macro and store it in named buffer letter
q\<LETTER\> | Append new actions on an macro in named buffer letter
q | When recording a macro, stop recording the macro
@\<letter\> | Execute macro from named buffer letter
@@ | Repeat execution of last macro
m\<letter\> | Mark current position with letter
‘\<letter\> | Move the cursor to the first character of the line marked by letter
“\<letter\> | Move the cursor to the character marked by letter
ZZ | Save and quit
. | Repeat last edition command
& | Repeat last substitution command
[\<count\>]!!\<cmd\> | Filter count lines (starting at current line) through cmd

## The Ex
### Line addresses
Command | Description
--------|------------
:\<n\>\<cmd\> | Apply cmd to line n
:\<n\>,\<m\>\<cmd\> | Apply cmd from line n to line m
:.\<cmd\> | Apply cmd to current line
:.,$\<cmd\> | Apply cmd from current line to end of file
:20,.\<cmd\> | Apply cmd from line 20 to current line
:%\<cmd\> | Apply cmd to all lines
:.+3,$-2\<cmd\> | Apply cmd on range that starts three lines below the cursor and ends two lines before the last line in the file
:.,+20\<cmd\> | Apply cmd from current line to 20 lines further in the file (when using + or -, . can be omitted)
:-,+\<cmd\> | Apply cmd to current line, line above current line and line below current line
:/\<pattern\>/\<cmd\> | Apply cmd to next line containing pattern
:/\<pattern\>/+\<cmd\> | Apply cmd to line below the next line containing pattern
:/\<pattern1\>/,/\<pattern2\>/\<cmd\> | Apply cmd from the first line containing pattern1 to the first line containing pattern2
:.,/\<pattern\>/\<cmd\> | Apply cmd from current line to firstline containing pattern
:\<cmd\>0 | The number 0 stands for the top of the file (imaginary line 0). It allows you to move or copy lines to the very start of a file, before the first line of existing text.
:/\<pattern\>/;+5\<cmd\> | When you use a semicolon instead of a comma, the first line address is recalculated as the current line. In this example cmd will be applied to the first line containing pattern and the five lines that follow.

### Commands
Command | Description
--------|------------
^V | Escape keys interpreted by ex (for instance \<ENTER\>, \<ESC\>, \<BACKSPACE\> and \<DELETE\>)
% | Current filename (for instance to backup current file, use :w %.bak)
\# | Alternate filename (for instance to go back to previous file, use :e #)
:\<cmd1\> \| \<cmd2\> | Pipe symbol is an Ex command separator
:!\<cmd\> | Open a shell and execute cmd
:\<address\>!\<cmd\> | Filter lines identified by address through cmd
:\<address\> | Move to line identified by address
:ab[breviate] \<abbr\> \<phrase\> | Define abbreviation to expand abbr into phrase when entering text in Insert mode
:ab | List currently defined abbreviations
:argdo \<cmd\> | Execute cmd on all files in the argument list
:ar[gs] | Show list of files when editing multiple files
:ar \<f1\> \<f2\> \<f3\> | Close current files and open files f1, f2 and f3
:cd \<dir\> | Change current directory to dir
:[\<source address\>]co[py]\<target address\> | Copy lines to target address 
:[\<address\>]d[elete] | Delete lines
:e[dit] \<file\> | Close current file and open file
:e! | Discard all changes and go back to last saved version of file
:fir[st] | Move to first file in a sequence of files
:[\<address\>]g[lobal]/\<pattern\>/\<cmd\> | Find lines matching pattern and executes cmd there
:[\<address\>]g!/\<pattern\>/\<cmd\> | Find lines not matching pattern and executes cmd there
:hid[e] edit \<file\> | Hide current buffer and open file
:[\<source address\>]m[ove]\<target address\> | Move lines to target address 
:la[st] | Move to last file in a sequence of files
:map \<string\> \<sequence\> | Map string to sequence of editing commands (character in g, K, q, ^A, ^K, ^O, ^W, ^X, _, *, \, and =)
:map | List currently defined mappings
:n[ext] | Edit next file in a sequence of files
:prev[ious] | Edit previous file in a sequence of files
:[\<address\>]pu[t] \<letter\> | Put content from named buffer letter
:pw[d] | Show current directory
:q[uit] | Quit
:[\<address\>]r[ead] \<file\> | Insert content of file below the last line number of this range or below cursor if range not provided. Special case: range 0 will insert file before the first line
:[\<address\>]r !\<cmd\> | Insert output of external program cmd
:[\<address\>]s[ubstitute]/\<pattern\>/\<replacement\>/\<flags\> | Replace pattern with replacement
:sav[eas] \<file\> | Save current file to f and edit f
:sh[ell] | Open a shell
:tabd[o] \<cmd\> | Execute cmd on all tabs
:una[bbreviate] \<abbr\> | Remove abbreviation for abbr
:unm[ap] \<string\> | Remove mapping for string
:[\<address\>]v[global]/\<pattern\>/\<cmd\> | Find lines not matching pattern and executes cmd there
:[\<address\>]w[rite] | Write buffer to file
:[\<address\>]w \<file\> | Write buffer to file
:[\<address\>]w \>\> \<file\> | Append buffer to file
:[\<address\>]w !\<cmd\> | Send current buffer to standard input of external program cmd
:wq | Write buffer to file and quit
:x[it] | Write buffer to file (only if modified) and quit
:[\<address\>]ya[nk] \<letter\> | Yank into named buffer letter

### Options
Command | Shortcut | Description
--------|----------|------------
:set \<option\>? |  | Show current value of option
:set autoindent | :set ai | Turn on auto indent mode
:set cmdheight | :set ch | Set the command line height
:set equalalways | :set ea | Resize windows equally after splitting or closing a window
:set ignorecase | :set ic | Make searches case-insensitive
:set incsearch | :set is | Enable incremental search
:set list | | List mode: Show tabs as CTRL-I is displayed, display $ after end of line
:set mouse=a | | Enable the use of mouse
:set number | :set nu | Display a line number in front of every line
:set shiftwidth=\<count\> | :set sw | Set default shift to count spaces
:set winheight=\<count\> | :set | wh Define the minimal window height when a window becomes active
:set winminheight=\<count\> | :set wmh | Define the minimum window height
:set winminwidth=\<count\> | :set wmv | Define the minimum window width
:set winwidth=\<count\> | :set wiw | Define the minimal window width when a window becomes active
:set wrapscan | :set ws | Wrap search

### Some useful combinations
Command | Description
--------|------------
:map g I/* ^[A */^[ | Assign g to sequence of instructions which puts C-style comments around the line (note the escaped \<ESC\>, you have to type \<CTRL\>-V\<ESC\>)
:96,99!sort | Pass lines 96 through 99 through the sort filter and replace those lines with the output of sort
:%!sort | Sort file
:e! | Return to the last saved version of the file
:230,$w \<newfile\> | Save only part of currently edited file into newfile
:230,$w \>\> \<newfile\> | Append part of currently edited file into newfile
50i*\<Esc\> | Insert 50 * characters
C | Replace characters from current cursor position to end of the line
\<count\>cc | Change entire line
ct. | Change to end of sentence, leaving the period
ddp | Swap two lines
ea | Append text at the end of a word
S | Change entire line
xp | Swap two letters
ZZ | Save and quit
