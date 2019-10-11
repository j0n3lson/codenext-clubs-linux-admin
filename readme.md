# Welcome

## What you'll Need

1. Your laptop
2. A GitHub account

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

## Working with Github

We'll store all of our files on Github both so you get more experience with
Git and so I can give you feedback. In order to do that, you need to fork my
repo. After every class, we'll save all our work on Github for later.

TIP: Check out this [video](https://www.youtube.com/watch?v=f5grYMXbAV0) on
forking

TIP: Check out this [video](https://www.youtube.com/watch?v=-zvHQXnBO6c) on
synching your changes to my Git repository.

## Connecting

The Bandit landing page has all the details on how to login. This section is
just for quick reference.

If you're not logged in, you need to use port `2220`

`ssh $USERNAME@banditlabs.overthewire.org -p $PORT`

Once logged in, you can ssh to any level you know the password for:

`ssh $USERNAME@localhost`

Try to answer the following questions:

1. What is the `ssh` command used for?
2. What is the `-p` flag used for?
3. What is `localhost`?
4. Once you are logged into a level, why don't you have to give the `-p` flag to log into another level?

# HAPPY HACKING!!!
