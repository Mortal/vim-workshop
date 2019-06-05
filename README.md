Workshop: Practical Efficient Vim
=================================

You've used Vim for a little while, and maybe even used it to write and edit code.

You know that Vim is supposed to make you super-efficient at editing text and code,
but you feel like you're spending a lot of time fighting Vim to make it do what you want.

Let's get better at Vim together!

**Prerequisites:** vimtutor.
In vimtutor you learn about a lot of basic commands that are useful when editing text,
and I am not going to spend too much time going over the basic commands.

**Optional prerequisites:** LaTeX compiler and Python 3 interpreter.
Some of the exercises involve LaTeX and Python code,
which is more fun if you can compile or run the code after editing it.

I'd recommend that you go through vimtutor (type `vimtutor` in your terminal)
before the workshop to freshen up the following commands:

* <kbd>i</kbd> <kbd>A</kbd> <kbd>o</kbd> <kbd>a</kbd> <kbd>A</kbd>
* <kbd>x</kbd>
* <kbd>:q!</kbd> <kbd>:wq</kbd>
* <kbd>h</kbd> <kbd>j</kbd> <kbd>k</kbd> <kbd>l</kbd>

* <kbd>w</kbd> <kbd>e</kbd> <kbd>0</kbd> <kbd>$</kbd>
* <kbd>dw</kbd> <kbd>d$</kbd> <kbd>dd</kbd>
* <kbd>2w</kbd> <kbd>d2w</kbd> <kbd>2dd</kbd>
* <kbd>u</kbd> <kbd>CTRL-R</kbd>

* <kbd>p</kbd>
* <kbd>r</kbd> <kbd>ce</kbd> <kbd>c$</kbd>

* <kbd>gg</kbd> <kbd>G</kbd> <kbd>CTRL-G</kbd>
* <kbd>/</kbd> <kbd>?</kbd> <kbd>n</kbd> <kbd>N</kbd>
* <kbd>CTRL-O</kbd> <kbd>CTRL-I</kbd>
* <kbd>%</kbd>
* <kbd>:%s/old/new/g</kbd>

* <kbd>:!ls</kbd> <kbd>:r</kbd>
* <kbd>:w</kbd>

* <kbd>R</kbd> <kbd>vy</kbd> <kbd>yw</kbd> <kbd>p</kbd>
* <kbd>:set hls</kbd> <kbd>:set nohls</kbd>

Here's a useful cheatsheet from [viemu.com](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html):

![viemu cheatsheet](viemu-cheatsheet.png)


Lesson zero: Choice of keyboard layout
--------------------------------------

If you're working with LaTeX or any kind of programming,
and you don't use the US keyboard layout (shown in the cheatsheet above),
I strongly recommend that you give it a try!

On the US keyboard layout, you get a lot of useful special characters
without having to hold down Shift, Ctrl or Alt:

* <kbd>&#92;</kbd>
* <kbd>[</kbd> <kbd>]</kbd>
* <kbd>'</kbd>
* <kbd>;</kbd>
* <kbd>/</kbd>
* <kbd>=</kbd>

And with just the Shift key you get the following:

* <kbd>|</kbd>
* <kbd>{</kbd> <kbd>}</kbd>
* <kbd>"</kbd>
* <kbd>:</kbd>
* <kbd>?</kbd>
* <kbd>+</kbd>
* <kbd>~</kbd>

This is a lot better than e.g. Danish keyboard layout
where you need the nasty AltGr key to access <kbd>&#92;</kbd> <kbd>{</kbd> <kbd>}</kbd> <kbd>|</kbd> <kbd>~</kbd>.

For entering special characters such as æ ø å ä ö ü etc.,
you can configure a so-called *Compose key* in Linux
so that you can enter e.g. æ by typing <kbd>Compose</kbd> <kbd>a</kbd> <kbd>e</kbd>.


Lesson one: Getting tabular
---------------------------

**Tip: Press <kbd>"+p</kbd> to paste text into Vim that you copied from outside Vim.**

Here's a small LaTeX document.
Copy it into Vim by selecting it in your web browser, pressing <kbd>CTRL-C</kbd>,
opening Vim, and typing <kbd>"+p</kbd>.

```
\documentclass{memoir}
\usepackage[utf8]{inputenc}
\begin{document}
I år består festudvalget af følgende FU'er:\par
\begin{tabular}{lll}
\hline
Navn & Menneskenavn & Email \\
\hline

\hline
\end{tabular}
\end{document}
```

**Tip: Press <kbd>:w (FILENAME)</kbd> to save a new file.**

Next, type <kbd>:w fu.tex</kbd> to save the document.
Optionally compile it with pdflatex.

Go to <https://TAAGEKAMMERET.dk/bestfu/> in your web browser,
scroll to the bottom and copy the table with ten rows.

**Tip: Press <kbd>}</kbd> to go to the next blank line. Press <kbd>{</kbd> to go to the previous blank line.**

In `fu.tex`, press <kbd>}</kbd> to navigate to the blank line
and paste the copied table with <kbd>"+p</kbd>.

You should obtain something like:

```
\documentclass{memoir}
\usepackage[utf8]{inputenc}
\begin{document}
I år består festudvalget af følgende FU'er:\par
\begin{tabular}{lll}
\hline
Navn & Menneskenavn & Email \\
\hline
FUNA 	Znguvnf Xnaartnneq Avryfra 	SHNA@TAAGEKAMMERET.dk
FURN 	Yvaarn Frurfgrq Fxnsgr 	SHRN@TAAGEKAMMERET.dk
FURF 	Wraf Gebyyr 	SHRF@TAAGEKAMMERET.dk
FUSB 	Zbegra Uhyoæx Sbt 	SHSB@TAAGEKAMMERET.dk
FUVO 	Fbsvr Orueznaa 	SHVO@TAAGEKAMMERET.dk
FUAØ 	Xngevar Uøubyg Xnfcrefra 	SHABR@TAAGEKAMMERET.dk
FUEN 	Znevn Nfxubyz Avryfra 	SHEN@TAAGEKAMMERET.dk
FUEB 	Serqrevx Naqrefra 	SHEB@TAAGEKAMMERET.dk
FUHS 	Nyoreg Serhq Novyqtnneq 	SHHS@TAAGEKAMMERET.dk
FULB 	Znwn Qloobr 	SHLB@TAAGEKAMMERET.dk
\hline
\end{tabular}
\end{document}
```

That's not a proper LaTeX table. Let's do something about that.

**Tip: Press <kbd>f(TAB)</kbd> to jump to the next TAB character.** (works with any single character; tab is simply an example)

**Tip: Press <kbd>s</kbd> to delete a character and go to insert mode.**

**Tip: Press <kbd>;</kbd> to repeat the last <kbd>f</kbd> command.**

**Tip: Press <kbd>.</kbd> to repeat the last text manipulation command.**

Navigate to the first line you inserted and type <kbd>f</kbd><kbd>(TAB)</kbd><kbd>s</kbd><kbd>&amp;(SPACE)(ESC)</kbd><kbd>;</kbd><kbd>.</kbd><kbd>A</kbd><kbd>(SPACE)\\(ESC)</kbd>

That was quick! But we still have 9 more lines to go. You could press <kbd>(RETURN)</kbd> to go to the beginning of the next line and repeat the above key presses, but that would be tedious.

**Tip: Press <kbd>q(LETTER)</kbd> to record a series of keystrokes. End the recording with <kbd>q</kbd>.** This is known as *recording a macro*.

**Tip: Press <kbd>@(LETTER)</kbd> to execute a series of keystrokes. Press <kbd>@@</kbd> to re-execute the last executed series.** This is known as *replaying a macro*.

Go to the beginning of the next line, press <kbd>qq</kbd>, redo the keystrokes you entered for the first line, go to the beginning of the next (i.e. third) line, and press <kbd>q</kbd>.

Now press <kbd>@q</kbd>. If all went well, this should redo for the third line what you did for the second line, and put your cursor at the beginning of the fourth line. If something doesn't look right, maybe you didn't record the macro completely right; try recording it again.

Now press <kbd>7@@</kbd> to run the macro seven more times.

In this case, we knew there are 10 lines in total, so it was easy to calculate the correct number of repeats in our head (i.e. 7).

However, sometimes there's a lot of lines, more than we can quickly count.
For these cases there's another way to run a macro on a set of lines.

Press <kbd>u</kbd> to undo what you did.

**Tip: Press <kbd>V</kbd> to start selecting lines.** This is known as *Visual Line* mode.

**Tip: Press <kbd>:norm @q</kbd> while in Visual Line mode to replay macro <kbd>q</kbd> on the selected lines.**
Note that Vim inserts `'<,'>` in-between `:` and `norm`; this is intended, so don't delete it!

Move the cursor to the first line that needs to be processed, press <kbd>V</kbd>,
move the cursor to the last line, and press <kbd>:norm @q</kbd>.
If all went well, this should replay the macro on each selected line -- no line counting needed on your part!

In this case, the lines that we needed to run the macro on were contiguous.
Sometimes, we want to run a macro on all lines that match a specific pattern instead.

**Tip: Press <kbd>:g/(PATTERN)/norm @q</kbd> to replay macro <kbd>q</kbd> on all lines that contain `(PATTERN)`.**

Undo the previous macro replays with <kbd>u</kbd>.
This time, without going into Visual Line mode,
press <kbd>:g/(TAB)/norm @q</kbd>.
Vim should display the tab character as `^I` - this is intended and is simply the way Vim displays tab characters.
If all went well, this should replay the macro on every line that contains a tab character.

You should now have a file containing something like:

```
\documentclass{memoir}
\usepackage[utf8]{inputenc}
\begin{document}
I år består festudvalget af følgende FU'er:\par
\begin{tabular}{lll}
\hline
Navn & Menneskenavn & Email \\
\hline
FUNA & Znguvnf Xnaartnneq Avryfra & SHNA@TAAGEKAMMERET.dk \\
FURN & Yvaarn Frurfgrq Fxnsgr & SHRN@TAAGEKAMMERET.dk \\
FURF & Wraf Gebyyr & SHRF@TAAGEKAMMERET.dk \\
FUSB & Zbegra Uhyoæx Sbt & SHSB@TAAGEKAMMERET.dk \\
FUVO & Fbsvr Orueznaa & SHVO@TAAGEKAMMERET.dk \\
FUAØ & Xngevar Uøubyg Xnfcrefra & SHABR@TAAGEKAMMERET.dk \\
FUEN & Znevn Nfxubyz Avryfra & SHEN@TAAGEKAMMERET.dk \\
FUEB & Serqrevx Naqrefra & SHEB@TAAGEKAMMERET.dk \\
FUHS & Nyoreg Serhq Novyqtnneq & SHHS@TAAGEKAMMERET.dk \\
FULB & Znwn Qloobr & SHLB@TAAGEKAMMERET.dk \\
\hline
\end{tabular}
\end{document}
```

**Exercise:** Add `\newcommand{\furow}[3]{#1 & #2 & #3 \\}`
and use what you have learned to convert each row
into an invocation of the `\furow` LaTeX command.

Lesson two: Parselmouth
-----------------------

Copy the following Python code and save it as `fu.py`:

```
import re
import urllib.request

with urllib.request.urlopen('https://TAAGEKAMMERET.dk/bestfu/') as request:
    html = request.read().decode('utf-8')

for row in re.finditer('<tr>.*?</tr>', html, re.S):
    name, human_name = re.findall(r'<td>(.*?)</td>', row.group())
    if not name.startswith('FU'):
        continue
    email, = re.findall('mailto:([^"]*)', row.group())
    print('%s & %s & %s \\\\' % (name, human_name, email))
```

**[Aside:** Press <kbd>:filetype</kbd> to see your current filetype settings.
Vim should respond with `filetype detection:ON  plugin:ON  indent:ON`.
If it does not, you need to add `filetype indent plugin on` to the file `~/.vimrc`.
This ensures that Vim automatically indents e.g. Python code correctly.
Close Vim and reopen fu.py after editing your vimrc file.
**---End aside]**

**Hint: Press <kbd>CTRL-P</kbd> while in Insert mode to complete the word at the cursor using other words in the current file.**

Navigate to the `for`-line and press <kbd>O</kbd>
to open a new line above, type <kbd>print("TA</kbd><kbd>CTRL-P</kbd><kbd>s FUer:")</kbd>.
This should yield the line `print("TAAGEKAMMERETs FUer:")`.

**Hint: While completing in Insert mode, use <kbd>CTRL-N</kbd> and <kbd>CTRL-P</kbd>
to navigate the suggestions.
When you are satisfied with the completed word,
press <kbd>(ESCAPE)</kbd> or continue typing to close the completion popup.**

**Hint: Press <kbd>CTRL-X</kbd><kbd>CTRL-L</kbd> while in Insert mode
to complete the line at the cursor using other lines in the current file.**

**Hint: Press <kbd>CTRL-W</kbd> while in Insert mode
to erase the last word you inserted.**

Go to the second `import`-line and press <kbd>o</kbd>
to open a new line above and type
<kbd>im</kbd><kbd>CTRL-X</kbd><kbd>CTRL-L</kbd><kbd>CTRL-W</kbd><kbd>parse</kbd>.
This should yield the line `import urllib.parse`. Delete it again with <kbd>dd</kbd>.

Remember to use these two completion commands (token completion and line completion)
-- they will save you **a lot** of typing in the long run!

But now for something more interesting: *code refactoring*.

The `with`-line is a bit long, don't you think?
We should extract the URL as a variable, i.e. change it to this:

```
url = 'https://TAAGEKAMMERET.dk/bestfu/'
with urllib.request.urlopen(url) as request:
    html = request.read().decode('utf-8')
```

**Tip: Press <kbd>ci(</kbd> to delete the <kbd>i</kbd>nsides of a set of parentheses and switch to Insert mode.**

**Tip: Press <kbd>O</kbd> to <kbd>O</kbd>pen a line above the current line.**

**Tip: Press <kbd>CTRL-A</kbd> while in Insert mode to insert the same text as you inserted the last time you were in Insert mode.**

**Tip: Press <kbd>p</kbd> to put the text you last deleted.**

Here's how I would do it:

1. Navigate to the `(` character in the `with`-line -- remember the <kbd>f(</kbd> command?
2. Press <kbd>ci(</kbd><kbd>url</kbd><kbd>(ESCAPE)</kbd> to replace the contents of the parentheses with the variable name `url`
3. Press <kbd>O</kbd><kbd>CTRL-A</kbd><kbd>(SPACE)=(SPACE)</kbd><kbd>(ESCAPE)</kbd> to insert `url = `.
4. Press <kbd>p</kbd> to insert the URL you deleted using in step 2.

**Exercise:** Record step 3 and 4 in a macro to save you a couple keystrokes in the rest of this lesson.

**Tip: Press <kbd>ct,</kbd> to delete everything <kbd>t</kbd>ill the next comma.**

Let's use a macro to extract some more variables in this Python program.

Navigate to the first `'` in the `for`-line with <kbd>f'</kbd>.
Then use <kbd>ct,</kbd> to delete the first argument (i.e. `'<tr>.*?</tr>'`)
and type <kbd>pattern</kbd><kbd>(ESCAPE)</kbd>.

Then repeat steps 3 and 4 above (or replay the macro you just recorded).

**Tip: Press <kbd>c%</kbd> to delete everything from the cursor until the
parenthesis matching the first parenthesis to the right.**

The motion <kbd>%</kbd> moves the cursor to the parenthesis matching the one under the cursor.
However, if there is no parenthesis under the cursor, Vim first searches to the right
in the line for the first open or close parenthesis, and then moves to the matching one.

This is very useful when you want to affect a function call such as
`re.findall(r'<td>(.*?)</td>', row.group())`:
First move the cursor to the "r" in "re.findall", and then press <kbd>%</kbd>
to jump to the end of the function call.

**Exercise:** Extract `mo.group()` to a variable using <kbd>c%</kbd> and your macro.

**Tip: Press <kbd>:nnoremap (COMMAND) (COMMANDS)</kbd> to remap (COMMAND) to (COMMANDS).**

If you like this trick, create a mapping for it!
Personally, I use <kbd>&#92;</kbd><kbd>r</kbd> as a shortcut for steps 3 and 4.
Press <kbd>:nnoremap &#92;r O&lt;C-A&gt; = &lt;Esc&gt;p</kbd>, and then try replacing some argument with a variable name and pressing <kbd>&#92;r</kbd>.

**Tip: Press <kbd>:nnoremap &lt;buffer&gt; (COMMAND) (COMMANDS)</kbd> to create a mapping that only applies in the current file.**

**Put <kbd>au FileType python (COMMAND)</kbd> in your vimrc to run a command whenever you open a Python file.**

If you want to use this trick in all Python files, add the following to your `~/.vimrc`:

```
au FileType python noremap <buffer> \r O<C-A> = <Esc>p
```

Of course, this works for languages other than Python too.
If you're unsure what to put after `au FileType` for a given type of file,
open a file of the given type and type <kbd>:set ft</kbd>,
and Vim will respond with the filetype of the currently-open file.

**Exercise:** Create a mapping for <kbd>&#92;r</kbd> in your vimrc that works for LaTeX instead of Python.
I.e. when you replace `M_{\odot}` with `\sunmass` in a LaTeX file and press <kbd>&#92;r</kbd>,
Vim should insert `\newcommand{\sunmass}{M_{\odot}}` on a new line above.


Lesson three: Spell-checking
----------------------------

**Hint: <kbd>:set spell spelllang=en&#95;us</kbd> to enable American English spell-checking for the current file.**

**Hint: <kbd>:set spellfile=(SPELLFILE)</kbd> to use the extra words in (SPELLFILE) when spell-checking.**

**Hint: <kbd>]s</kbd> and <kbd>[s</kbd> navigate to the next and previous misspelled word in the open file.**

**Hint: <kbd>zg</kbd> saves the word under the cursor as "good" in (SPELLFILE). <kbd>zw</kbd> saves it as "wrong" in (SPELLFILE). <kbd>zuw</kbd> and <kbd>zug</kbd> are used to <kbd>u</kbd>ndo <kbd>zg</kbd> and <kbd>zw</kbd>.**

**Hint: <kbd>au BufRead (PATH)/&#42;.tex (COMMAND)</kbd> to run (COMMAND) whenever you open a .tex-file inside (PATH).**

**Hint: Add <kbd>let g:tex&#95;comment&#95;nospell=1</kbd> in your vimrc to disable spell-checking inside LaTeX comments.**

In my vimrc, I have the following lines to enable spell-checking for my thesis:

```
let g:tex_comment_nospell=1
au BufRead /home/rav/work/thesis/*.tex
	\ setlocal spell spelllang=en_us spellfile=
	\/home/rav/work/thesis/spell.txt.utf8.add
```


TODO Lesson four: Creating and editing multiple files
-----------------------------------------------------

<https://TAAGEKAMMERET.dk/galleri/2018>

Make links with CTRL-X

Use gf to open link

Use CTRL-O to go back

Use CTRL-W s to split window

CTRL-W CTRL-W to switch between windows

Manipulate HTML and write result to a new file

Record a macro to do it

Manipulate all files with :args :set autowrite :argdo

Look at differences with vimdiff or :windo :diffthis
