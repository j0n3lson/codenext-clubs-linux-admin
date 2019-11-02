
# Level 9

## <a name='Overview'></a>Overview

Simular to a previous level, the main point of this level is to search for
specific content in a file.

<!--NOTE: Do not edit table of content's. This is auto generated using an vscode-extension. -->
## <a name='TableofContents'></a>Table of Contents
<!-- vscode-markdown-toc -->
* [Overview](#Overview)
* [Table of Contents](#TableofContents)
* [Completing the Level Goal](#CompletingtheLevelGoal)
	* [Command Demo](#CommandDemo)
	* [Command Breakdown](#CommandBreakdown)
* [Learn More](#LearnMore)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='CompletingtheLevelGoal'></a>Completing the Level Goal

The *gotcha* on this level was that not every byte in a file is printable.
Trying to print a non-printable character will result in gibberish (and/or
mess your terminal up). If your terminal got messed up you can use the
`reset` command.

You had to filter the non-printable chracters using `strings` and then search
the resulting text.


### <a name='CommandDemo'></a>Command Demo

![Combining `strings` and `grep` to search file contents](stringsgrep.gif)

### <a name='CommandBreakdown'></a>Command Breakdown

The `grep` command is very very powerful. The general form from the `man grep` page is

```shell
grep PATTERN file1 file2 ...
```

The *PATTERN* here is called a **Regular Expression**. Regular Expressions help us describe a whole class of text using special characters. We won't dive into Regular Expressions since it can be very very confusing for college students, teachers, programers, and hackers alike! 

## <a name='LearnMore'></a>Learn More

* Article: [Regular Expressions, Regular Grammar and Regular Languages](https://www.geeksforgeeks.org/regular-expressions-regular-grammar-and-regular-languages/) (EXTREME GEEK WARNING)
* Video: [Regular Expressions (RegEx) Tutorial #1 - What is RegEx?](https://www.youtube.com/watch?v=r6I-Ahc0HB4)