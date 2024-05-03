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

+ [Emacs](https://www.gnu.org/software/emacs/)

    It's an extensible, customizable, free/libre text editor. At its core is an interpreter for Emacs Lisp, a dialect of the Lisp programming language with extensions to support text editing. Emacs has a lot of crazy features and is definetly a goto for a higher level linux user. To start it:
  > $emacs


**Vim**

  
