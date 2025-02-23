## Rammer's Zettelkasten Spec

This is my implementation of the Zettelkasten note-taking method. I have created a bunch of scripts to manipulate and create zettelkastens. 

## Terminology/Definitions

* Zettelkasten: A directory which serves as your stash of short notes.
* Isosec: A timestamp based on the following format - `YYYYMMDDHHmmSS` (where `M` is month and `m` is minute). An isosec is used for naming files.
* `ZETDIR`: The absolute path of the zettelkasten directory in your machine. I recommend setting this in your shell's profile/rc file.
* `Tag`: A mark or a label which will provide more context to your note.

## Workflow

* The `ZETDIR` is the directory containing all your notes.
* All your notes/entries will exist directly under the `ZETDIR`.
* The first line of a zetentry must be a header with one `#`. This will be the title of your note.
* Try not to write more than 60 words as a general guideline. Always break large notes into multiple small ones and link them.
* For media (images/video/etc), use a folder called `media` under `ZETDIR` where all the media of zettelkasten will be stored. 
	* Media files will be named in the following manner: `ISOSECx{id}.{ext}` where 'x' can be any alphabetical character, `{id}` is just a number, and `{ext}` is the extension. 
	* I first thought that it'll be useful to name these as `ISOSEC-{number}.{ext}` or `ISOSEC_{number}.{ext}` but I realized that hyphens and underscores may be invalid characters in different contexts (such as web links).
* You may optionally choose to create an index. If you do, name it as `README.md`.
* Tags
	* Tags start with `#` and have no space (for example, `#cooking` is a tag, but not `# cooking`). 
	* For the sake of simplicity, tag-names must begin with an alphabetical character and can contain only numbers and alphabets (no hyphens, underscores or any other special characters).
	* Tags must be whitespace-separated from other text (ensure that you use `blah blah #tag` and not `blah blah#tag`).
	* If you wish to use Exuberant Ctags, allocate an entire line for a tag i.e. do not write multiple tags together on the same line.


## Commands

All zet commands error out if `ZETDIR` is unset

1. `zetentry`: Opens a new zet note/entry using the current isosec as the filename. 

2. `zetget`: Takes an isosec as an argument and opens it in your `EDITOR`. Errors out if the given argument is not an isosec. Has an interactive option too "-i" which uses fzf

3. `zethead`: Searches through zet entries on the basis of headings. Can be made interactive using fzf.

4. `zets`: Grep through entire zettelkasten.

5. `zetplace`: Takes an isosec and converts it into a markdown link. Works only in zettelkasten. Errors out if the argument is not an isosec.

6. `zetback`: Takes an isosec and returns entries which link to the given isosec.

7. `zetag`: Zet Tag Generate will use ctags to index tags for easier navigation - WIP

8. `zetlink`: Displays all the links that a zet entry has to other entries

## Helper Commands

1. `zetloc` - Locates a given isosec and returns absolute path of the entry

## Useful optional dependencies

1. rg
2. fzf

## FAQ

* "I use Obsidian, and I can't see the titles of my notes in the graph view" - use the Front Matter Title plugin.

## TODO

* Tag indexing


## vimrc

```vimscript
" Zettelkasten get heading
function Headings()
	set noshelltemp
	read !zethead -i
	set shelltemp
endfunction

" Zet get backlinks to current file
function Backlinks()
	read !zetback %:p -v
endfunction
```
