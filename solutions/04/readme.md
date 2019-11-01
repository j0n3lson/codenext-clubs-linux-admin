
# Level 4 

## <a name='Overview'></a>Overview

The goal of this level is to learn how to read files when the contents of
files. But there's a twist, sometimes reading a file might trip you up. You
should be careful opening/reading files when you don't know what's in them
:).

## <a name='TableofContents'></a>Table of Contents
<!-- vscode-markdown-toc -->
* [Overview](#Overview)
* [Table of Contents](#TableofContents)
* [Completing the Level Goal](#CompletingtheLevelGoal)
	* [(Required) Command Demo](#RequiredCommandDemo)
	* [(Optional) Command Breakdown](#OptionalCommandBreakdown)
	* [Banging on the Pipes](#BangingonthePipes)
* [Discussion Points](#DiscussionPoints)
* [Learn More](#LearnMore)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='CompletingtheLevelGoal'></a>Completing the Level Goal

My solution uses a few different ideas:

* Since we're told that the file is human-readable, I suspect we should look
for *ASCII* files. But how do I figure out the type of a file?
* I'm lazy and don't want to read all the files one at a time. If I can figure out a command that tells me the file type, then I just need to check the file time for each of the files...

### <a name='RequiredCommandDemo'></a>(Required) Command Demo

![File types provide a hint for what might be in a file](filetypes.gif)

### <a name='OptionalCommandBreakdown'></a>(Optional) Command Breakdown

```shell
bandit4@bandit:~/inhere$ find -type f | xargs -II file I
./-file09: data
./-file06: data
./-file01: data
./-file02: data
./-file05: data
./-file03: data
./-file08: data
./-file07: ASCII text
./-file04: data
./-file00: data
```

Here's what each part is doing:

* `find -type f`: This command list *only* files in the directory.
* `|`: Tells the shell to *redirect* the output (`stdout`) of one command to
 the input (`stdin`) of another. The output of the command on the left is used
 as the input of the command on the righthand side of the pipe.
* `xargs -II file I`: The `file` command can tell me the type of a file (see the demo) but it wants it's arguments like `file $THEFILENAME`. I use `xargs` to build the command using the *output* of the `find -type -f` command. The `xargs` command takes a flag `-I` which replaces every occurence of the following character in the command (here' we're replacing the *I* character).

### <a name='BangingonthePipes'></a>Banging on the Pipes

You can pipe (or chain) any number of commands in *nix. Try looking at the
output of each command to see how the whole pipe is built up.

```shell
# This gives you only the files
find -type f 

# This gives you the file types
find -type f | xargs -II file I 

# This gives you onlyl the files with ASCII text in them
find -type f | xargs -II file I | grep "ASCII" 

# This parses out the file name from the description
find -type f | xargs -II file I | grep "ASCII" | cut -d':' -f1 

# And this one combines them all to read the file that contains redable text
find -type f | xargs -II file I | grep "ASCII" | cut -d':' -f1 | xargs -II cat I
```

## <a name='DiscussionPoints'></a>Discussion Points

* Why are pipes so useful?
* What other things can you do with linux pipes?

## <a name='LearnMore'></a>Learn More

* [Piping in Unix or Linux](https://www.geeksforgeeks.org/piping-in-unix-or-linux/)