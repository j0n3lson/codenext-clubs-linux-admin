
# Level 5

## <a name='Overview'></a>Overview

This level is pretty straighforward...if you *read* the manual. There a many
ways to solve this level using one or more command (and pipes) but reading
the manual and looking for command flags will save you a lot of time in the
future.

## <a name='TableofContents'></a>Table of Contents
<!-- vscode-markdown-toc -->
* [Overview](#Overview)
* [Table of Contents](#TableofContents)
* [Completing the Level Goal](#CompletingtheLevelGoal)
	* [Command Demo](#CommandDemo)
	* [Command Breakdown](#CommandBreakdown)
* [Linux File Permissions](#LinuxFilePermissions)
* [Discussion Points](#DiscussionPoints)
* [Learn More](#LearnMore)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='CompletingtheLevelGoal'></a>Completing the Level Goal

This is trivial so I'll just provide the commands. What each flag does is left as an excercies for the reader.


### <a name='CommandDemo'></a>Command Demo

There's just way too many files to check them all by hand:

```shell
# There's 180 files in...
bandit5@bandit:~/inhere$ find ./* -type f | wc -l
180
bandit5@bandit:~/inhere$ 

# In 20 directories:
bandit5@bandit:~/inhere$ find ./* -type d | wc -l
20
bandit5@bandit:~/inhere$
```

You might be tempted to use pipes from the last level (it's reasonable). But
the `find` command is much more powerful! Here's my solution:

```shell
find ./* -type f -size 1033c \! -perm /u=x -exec cat '{}' \;
```

### <a name='CommandBreakdown'></a>Command Breakdown

According to the directions we needed to find a file that matches:

* __human-readable__: I didn't actually explcitly test for this, although I could have.
* __1033 bytes in size__: The `type f -size 1033c` flags are used for this
* __not executable__: The `\! -perm /u=x` flags do that. The `!` tells the `find` command to report files that do not match the criteria given by the `perms` flag. The `perm` flag is saying *look for any file for which the **user** has the **execute** permission (more on file permssions laster).

## <a name='LinuxFilePermissions'></a>Linux File Permissions

Back on level 3 you saw the `ls -la` long form and a breakdown of the output in the [Breakdown of the ls-l output](https://github.com/j0n3lson/codenext-clubs-linux-admin/tree/master/solutions/03#breakdown-of-the-ls--l-output) section.

One of the columns was the *File Permissions* column. Turns out that every file/folder on *nix has a permission that says who can do what with the file:

[![Linux File Permissions video](https://img.youtube.com/vi/D-VqgvBMV7g/0.jpg)](https://www.youtube.com/watch?v=D-VqgvBMV7g)

## <a name='DiscussionPoints'></a>Discussion Points

* What does the `-exec cat '{}' \;` part of the command do? (Hint: Read `man
find` specifically the documentation on `-exec`)
* In the `ls -la` output how can you tell if an entry is a file vs a directory?
* In the `ls -la` output identify the user's permssion? The groups permssion?

## <a name='LearnMore'></a>Learn More

* MUST READ: [File Permissions in Linux/Unix with Example](https://www.guru99.com/file-permissions.html)