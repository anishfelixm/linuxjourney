**regex \(Regular Expressions\)**

  Regular expressions are a pattern to select specific words. They may have the exact same charachters as the word and maybe some wildcard charachters like "*" -> one or many charachters, "?" -> 0 or 1 charachter, "." -> one charachter, etc. These are used a lot in text editing. Regex are very powerful tool. They are universal among all programming languages. Some other Regex symbols :
|Regex example |Action                                                                                          |
|--------------|------------------------------------------------------------------------------------------------|
|^by           |matches lines that start with "by"                                                              |
|seashore$     |matches lines that send with "seashore"                                                         |
|d\[iou\]g     |matches words that have i, o, u in middle like "dig", "dog", "dug"                              |
|d\[^i\]g      |matches words that have anything in middle except i ie "dag", etc but not "dig"                 |
|d\[a-c\]g     |matches words whose middle charachters range is a to c ie a,b, or c. Brackets are case-sensitive|
|d\[a-zA-Z\]g  |matches words which have any alphabet either lowercase a to z or uppercase A to Z               |
|d\.g          |matches word "d.g". Backslash used for patterns involving special charachters                   |
|four\|4       |matches words "four" or "4"                                                                     |

  Regex in Linux is used along with text editor or with grep.

---

**Text Editors**

  Two of the most popular Text editors in Linux which usually comes with the kernel are **Vim** and **Emacs**.
+ [Vim](https://www.vim.org/) :
  
    Vim is a highly configurable text editor that is very efficient at creating and changing texts of any kind. It is included in Linux kernels as "vi". To launch vim editor for a file named "file.txt" :
  > $vi file.txt
  >
  > //or
  >
  > $vim

+ [Emacs](https://www.gnu.org/software/emacs/)

    It's an extensible, customizable, free/libre text editor. At its core is an interpreter for Emacs Lisp, a dialect of the Lisp programming language with extensions to support text editing. Emacs has a lot of crazy features and is definetly a goto for a higher level linux user. To start it:
  > $emacs


**Vim**

  Vim stands for **V**i\(**IM**proved\) and is just an improved version of vi. It's lightweight and very comfortable to work with. Usually installed by default in Linux. To start it 
> $vim

  Once a Vim file is entered into, to search something within the file "/" or "?" is used with the word. "/" searches for the pattern from top of file to bottom. To move to next occurance of the word, use "n" and to move to previous occurance use "N". "?" searches for the pattern from bottom to top of file ie reverse of "/". So inside the Vim file while it's in command mode *\(since there's visual and insert mode\)* 
> /"hello, world"   //to locate occurance of hello, world in file. Since space is in pattern, use quotes.
>
> /#include   //locates all header files
>
> ?#define   //locates all macros

  There's no mouse activated by default in Vim *\[Can be done by editing "set mouse=a" in .vimrc\]*. So to navigate we use :
  
|Keys            |Action         |
|----------------|---------------|
|h or left arrow |move left by 1 |
|k or up arrow   |move up by 1   |
|j or down arrow |move down by 1 |
|l or right arrow|move right by 1|

  To enter "*insert*" mode from command mode, use :

|Keys|Action                  |
|----|------------------------|
|i   |insert bwfore the cursor|
|O   |insert in previous line |
|o   |insert in next line     |
|a   |append after the cursor |
|A   |append at end of line   |

To go back to command mode, use the "***ESC***" key.

  To do editing of a file in command mode in Vim :

|Key|Action                                            |
|---|--------------------------------------------------|
|d  |to delete the selected or charachter before cursor|
|x  |to cut and also delete selected text              |
|dd |to delete current line                            |
|y  |to yank or copy the selected content              |
|yy |to yank or copy the current line                  |
|p  |to past the copied content before the cursor      |

  To save or exit out of Vim we have to use the following commands :

|cmd|Action                                           |
|---|-------------------------------------------------|
|:w |to write changes to file ie save file            |
|:q |to quit out of vim                               |
|:q!|to quit out of vim without saving changes to file|
|:wq|to save changes and quit vim                     |
|ZZ |exactly same as ":wq"                            |
  
Two other useful command mode tools is :
+ u - undo last action or change
+ ctrl+r - redo last action or change

	There are lot more command options and tools in Vim but these are the essential basic ones.


**Emacs**

	
