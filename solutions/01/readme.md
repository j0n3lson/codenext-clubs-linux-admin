
# Level 1

## <a name='Overview'></a>Overview

In this level, you still have to read a file but with a twist. The file has wierd name which confuses your `cat` command.


## <a name='TableofContents'></a>Table of Contents
<!-- vscode-markdown-toc -->
* [Overview](#Overview)
* [Table of Contents](#TableofContents)
* [Completing the Level Goal](#CompletingtheLevelGoal)
	* [Command Demo: Working with strangely named files](#CommandDemo:Workingwithstrangelynamedfiles)
* [Discussion Points](#DiscussionPoints)
	* [What are `stdin` and `stdout`?](#Whatarestdinandstdout)
		* [Quick! Get your Bathing Suit!](#QuickGetyourBathingSuit)
		* [The standard streams, `stdin`, `stdout` and `stderr`](#Thestandardstreamsstdinstdoutandstderr)
* [Learn More](#LearnMore)
	* [More on `stdin`, `stdout`, and `stderr`](#Moreonstdinstdoutandstderr)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='CompletingtheLevelGoal'></a>Completing the Level Goal

Clicking on the first link the page provides takes you to a Google search
with some useful results (Google is your friend :smiley:). One of the first
post is from
[StackExchange](https://unix.stackexchange.com/questions/16357/usage-of-dash-in-place-of-a-filename).

Specifically:

> Using `-` as a filename to mean `stdin`/`stdout` is a convention that a lot of programs use...When cat sees the string `-` as a filename, it treats it as a synonym for stdin. To get around this, you need to alter the string that cat sees in such a way that it still refers to a file called `-`. The usual way of doing this is to prefix the filename with a path for example:  `./-`,

### <a name='CommandDemo:Workingwithstrangelynamedfiles'></a>Command Demo: Working with strangely named files

![Funny files demo](funnyfiles.gif)

## <a name='DiscussionPoints'></a>Discussion Points

### <a name='Whatarestdinandstdout'></a>What are `stdin` and `stdout`?

#### <a name='QuickGetyourBathingSuit'></a>Quick! Get your Bathing Suit!

To answer this question, you need to go swimming. Specifically, unix-like
systems have a concept of "streams" which programs use to commmunicate:

```

|----------|					 |----------|
| Program1 | <---- Stream ---- > | Program2 |
|----------|					 |----------|
```

This *stream* is actually a *datastream* and programs can put ... *data* in
it to send to another program. The *data* can be anything, but usually it's
text.

#### <a name='Thestandardstreamsstdinstdoutandstderr'></a>The standard streams, `stdin`, `stdout` and `stderr`

Whenever you run a command, the system sets up three standard streams between
the command you just ran and the `shell` (i.e. the terminal). After you hit `enter` on your keyboard, the system runs the command, and connects the `shell` and the command:

```
|----------|					       |----------|
| shell    | stdout <---- Stream ----  |    cat   |
|----------|					 	   |----------|
```

##### How programs talk

Now the `cat` command is running. When it's done *doing the thing*
<sup>TM</sup> it writes it's output to `stdout`. Meanwhile, `shell` (which is
still running) is waiting for the data to arrive, when it does it just
outputs it as normal.

##### How programs talk about errors

Now that you understand `stdout`, the `stderr` stream should be easy to understand. Like `stdout` programs put output into that stream...but unlike `stdout` usually `stderr` just contains error messages.

##### How the `shell` get's keyboard input

The last stream `stdin` is used to get input from other programs. The simplest use-case is getting info from the keyboard. When you type a key, the system actually reads data from the keyboard hardware and then writes that data to the `stdin` stream of the active program, in our case, the `shell`.

```
|------------|		 |------------|			       |----------|
| keyboard   | ----> | Operating  | --- stdin ---> |  shell   |  ---> Your Eyeballz
| (hardware) |	^	 |  System|   | 	 ^	       | 		  |
|------------|  |    |------------|      |         |----------|
		  		|						 |
		   data: 'foo'				  data: 'foo'
```

## <a name='LearnMore'></a>Learn More

### <a name='Moreonstdinstdoutandstderr'></a>More on `stdin`, `stdout`, and `stderr`

* [StackOverflow: Confused about stdin, stdout and stderr?](https://stackoverflow.com/questions/3385201/confused-about-stdin-stdout-and-stderr)
* [How To Geek: What are stdin, stdout, and stderr on Linux?](https://www.howtogeek.com/435903/what-are-stdin-stdout-and-stderr-on-linux/)
* [Youtube: Linux Commans for Beginners](https://www.youtube.com/watch?v=shFMEJJ_fpU)
* [Youtube: A simple explanation of stdin, stdout, and stderr](https://www.youtube.com/watch?v=fVwuiuirzmc)