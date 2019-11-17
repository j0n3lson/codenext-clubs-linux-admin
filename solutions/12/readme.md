
# Level 12

## <a name='Overview'></a>Overview

In this level you get introduced to file compression utilities. These
utilities take files and make them smaller using compression algorithms.

<!--NOTE: Do not edit table of content's. This is auto generated using an vscode-extension. -->
## <a name='TableofContents'></a>Table of Contents
<!-- vscode-markdown-toc -->
* [Overview](#Overview)
* [Table of Contents](#TableofContents)
* [Completing the Level Goal](#CompletingtheLevelGoal)
	* [The Basic Approach](#TheBasicApproach)
	* [A Better Approach](#ABetterApproach)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='CompletingtheLevelGoal'></a>Completing the Level Goal

### <a name='TheBasicApproach'></a>The Basic Approach

After reverting the hexdump, you have to use the `file` utility to see what
kind of file we have. Here's an example file:

```shell
bandit12@bandit:/tmp/jntry12$ file out.gz
out.gz: gzip compressed data, was "data2.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix
bandit12@bandit:/tmp/jntry12$ 
```

The output tells you that the file is `gzip compressed data` which is a hint
at which utility to use, in this case `gunzip`. To beat the level, you have
to use `file` to identify the next utility to use. A complete list of
commands is given below.

```shell
# This changes the hexdump into the original file.
# We use the "&&" to ensure the command are run
# in sequence. Without "&&" a command that writes
# the file may finish slighly after the command that
# reads the file.

xxd -revert data.txt out.gz &&
gunzip out.gz &&

# Bunzip expects the file to have a .bz extension.
mv out out.bz &&
bunzip2 out.bz &&

# Gunzip expects the file to have a .gz extension.
mv out out.gz &&
gunzip out.gz &&
mv out out.tar && 
tar -xf out.tar &&
tar -xf data5.bin &&
mv data6.bin data.bz &&
bunzip2 data.bz &&
tar -xf data &&
mv data8.bin data8.gz &&
gunzip data8.gz &&
# Read the file.
cat data8
```

### <a name='ABetterApproach'></a>A Better Approach

One of the drawbacks of the first approach is that you have to keep track of
the file name. As you've seen `bunzip` and `gunzip` have some expectations
about the file's extension. As a result we have to rename the files using the
`mv` command so the files have the right extension.

Fortunately *nix has the concept of Pipes, which you learned about in a
previous level. The `|` character let's us send the output of one file to the
input of another command. We can use this to our advantage:

```shell
bandit12@bandit:/tmp/jntry12$ 
xxd -r data.txt | gunzip | bunzip2 | gunzip | tar -xf - -O | tar -xf - -O | bunzip2 | tar -xf - -O | gunzip
The password is $NOOOOOP> 
bandit12@bandit:/tmp/jntry12$ 
```
*Note: The `\` are used so that we can continue on the next line for readability.

This approach is a little cleaner since we never actually have to write out a
file. This is important because, in some cases you might not want to write a file (or maybe you can't). Of course the only drawback is that we actually had to know the sequence of commands we needed to run. But what if we didn't know anything about the file?
