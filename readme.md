# Welcome

## What you'll Need

1. Your laptop
2. Curiosity
3. Patience

## Overview

There are 34 levels to the [Bandit](http://overthewire.org/wargames/bandit/)
game. Each level has a specific task to complete. For most earlier levels,
you might have to read a file stored on the computer somewhere. For later
levels, the tasks might involve connecting to a port on a server (I'll
explain what those things are as we go). When you complete the task, you get
the password for the next level. You then login to the next level using the
password.

Note: Every week I'll post solutions before class to the Git repo and we'll review
the previous week's solutions together in class.

## How to play

## Rulez

1. Don't share level passwords or solutions! If someone gives you the
password, ask *how* they solved the problem instead. Try to understand their
approach.

2. I will only provide solutions for non-trivial levels. I reserve the right
to forget how to do stuff :)

3. Document your work. Keep a readme.txt with all your solutions and notes.
This makes it easier to share your thought process (and solution!).

4. Challenge yourself: Are there other solutions out there? Compare your
solution to your lab mate!

## Connecting

The Bandit landing page has all the details on how to login. This section is
just for quick reference.

If you're not logged in, you need to use port `2220`

`ssh $USERNAME@banditlabs.overthewire.org -p $PORT`

Once logged in, you can ssh to any level you know the password for:

`ssh $USERNAME@localhost`

# HAPPY HACKING!!!
