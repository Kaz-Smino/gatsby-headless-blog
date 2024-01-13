---
title: Using the find Command with -exec Option
date: "2024-01-11T22:40:32.169Z"
description: A guide on how to use the find command with -exec option in Unix-like systems.
---

## Introduction

In Unix-like systems, the `find` command is a powerful tool for searching files and directories. One of its features is the `-exec` option, which allows you to execute a specific command on each item found. This guide will show you how to use the `find` command with `-exec` option.

## TL;DR

The other day, a friend asked me a question about Linux commands that I couldn't answer on the spot. So, I've put together this guide for my own learning and to help others. The goal is to search for directories named "udemy" in the same directory and move all found directories into the "program" directory at the same level.



##### Table Of Contents
 -  [Prerequisites](#anchor1)
 -  [Main Content](#anchor2)
 -  [Further Exploration: Pipe vs. Find -exec](#anchor3)
 -  [Final Thoughts](#anchor4)
 -  [References](#anchor5)

<a id="anchor1"></a>
## Prerequisites
Basic knowledge of Linux commands and the terminal is required to follow this guide.

<a id="anchor2"></a>
## Main Content

```bash
➜  sample_dir ls
➜  sample_dir mkdir program
➜  sample_dir mkdir udemy_01
➜  sample_dir mkdir udemy_02
➜  sample_dir ls
program  udemy_01 udemy_02

➜  sample_dir find . -type d -name "*udemy*" -exec mv {} ./program/ \;
find: ./udemy_01: No such file or directory
mv: ./program/udemy_01 and ./program/udemy_01 are identical
find: ./udemy_02: No such file or directory

➜  sample_dir ls
program

➜  sample_dir cd program
➜  program tree
.
├── udemy_01
└── udemy_02

2 directories, 0 files
```

#### Executed Command

```bash
find . -type d -name "*udemy*" -exec mv {} ./program/ \;
```

#### Explanation of the Executed Command

```bash
find [path]--> Search the specified [path] (for reference)
-type d --> Specify directories as the search target
-name "*udemy*" --> Specify items containing "udemy" in their name as the search target
-exec  --> Execute a specific command on the search target (in this case, the mv command)
mv {} ./program/ --> Move from the source path to the destination path ※ mv {source} {destination}
{} --> Placeholder for files or directories (if it hits in find, its full path is stored) ※ In other words, it becomes like this --> mv {source (full path of the directory that hit)} {destination (./program/)}
\; --> Used at the end of the exec option
```

<a id="anchor3"></a>
#### Further Exploration: Pipe vs. Find -exec

```bash
｜ --> Used to pass the output of one command as input to another command
find -exec --> Used to execute a specific command on each file or directory that find has searched
```
To be honest, when my friend first asked me about Linux commands, I intuitively thought that the pipe command would be used because it combines two or more commands (even though that wasn't actually the case.) So, just in case, I'm making a note of how it differs from the pipe command.

<a id="anchor4"></a>
## Final Thoughts

This has been a great reminder of the importance of regularly using Linux commands. From here on out, I'll continue to learn and share my discoveries. If you have any questions or suggestions, feel free to send a message via [LinkedIn](https://www.linkedin.com/in/kaz-smino-27a20a178).

<a id="anchor5"></a>
## References

I found the following resources helpful while writing this blog post:

- [Linux man pages online](https://man7.org/linux/man-pages/man1/find.1.html#EXAMPLES)
