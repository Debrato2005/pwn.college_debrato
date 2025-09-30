# File Globbing
Even just a few levels in, you might already be tired of typing out all these file paths. Luckily, the shell has a solution: globbing! That's what we'll learn in this module.

Before executing commands that you enter, the shell first performs expansions on them, and one of these expansions is globbing. Globbing lets you reference files without typing them all out, or typing out their full paths. Let's dig in!

## 1 Matching with *
The first glob we'll learn is *. When it encounters a * character in any argument, the shell will treat it as a "wildcard" and try to replace that argument with any files that match the pattern. It's easier to show you than explain:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_*
Look: file_a file_b file_c
Of course, though in this case, the glob resulted in multiple arguments, it can just as simply match only one. For example:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: file_*
Look: file_a
When zero files are matched, by default, the shell leaves the glob unchanged:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
The * matches any part of the filename except for / or a leading . character. For example:

hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use globbing to keep the argument you pass to cd to at most four characters! Once you're there, run /challenge/run for the flag!

### Solve
**Flag:** `pwn.college{oQoBvPlA2YMF6H2UZr1SgZZGFVW.dFjM4QDLxATN1czW}`

``` bash
Connected!
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /chal*
You specified the path to 'cd' to in more than 4 characters. Disallowed!
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /cha*
You specified the path to 'cd' to in more than 4 characters. Disallowed!
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{oQoBvPlA2YMF6H2UZr1SgZZGFVW.dFjM4QDLxATN1czW}
hacker@globbing~matching-with-:/challenge$ 

```
`*` matches 0 or more characters, so using that info we must use only 4 character and rest leave upto file globbing when passing args to `cd` in this challenge.

## 2 Matching with ?
Next, let's learn about ?. When it encounters a ? character in any argument, the shell will treat it as a single-character wildcard. This works like *, but only matches one character. For example:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_cc
hacker@dojo:~$ ls
file_a	file_b	file_cc
hacker@dojo:~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:~$ echo Look: file_??
Look: file_cc
Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use the ? character instead of c and l in the argument to cd! Once you're there, run /challenge/run for the flag!

### Solve
**Flag:** `pwn.college{Uekca-NkF0CrMEz55fWqgqjhrkl.dJjM4QDLxATN1czW}`

``` bash
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{Uekca-NkF0CrMEz55fWqgqjhrkl.dJjM4QDLxATN1czW}
hacker@globbing~matching-with-:/challenge$ 

```
`?` matches with exactly 1 character, so using that info we must use ? for c and l in `challenge` and rest leave upto file globbing when passing args to `cd` in this challenge.

## 3 Matching with []
Next, we will cover []. The square brackets are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, or n. For example:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
Try it here! We've placed a bunch of files in /challenge/files. Change your working directory to /challenge/files and run /challenge/run with a single argument that bracket-globs into file_b, file_a, file_s, and file_h!

### Solve
**Flag:** `pwn.college{AwDXLO3xQI9t5y0NPYtXwsb0CL8.dNjM4QDLxATN1czW}`

``` bash
Connected!
hacker@globbing~matching-with-:~$ cd  /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{AwDXLO3xQI9t5y0NPYtXwsb0CL8.dNjM4QDLxATN1czW}
hacker@globbing~matching-with-:/challenge/files$ 

```
`[]` Matches any one character inside brackets, therefore Changing working directory to /challenge/files and run /challenge/run with a single argument that bracket-globs into file_b, file_a, file_s, and file_h.

## 4 Matching paths with [] 
Globbing happens on a path basis, so you can expand entire paths with your globbed arguments. For example:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: /home/hacker/file_[ab]
Look: /home/hacker/file_a /home/hacker/file_b
Now it's your turn. Once more, we've placed a bunch of files in /challenge/files. Starting from your home directory, run /challenge/run with a single argument that bracket-globs into the absolute paths to the file_b, file_a, file_s, and file_h files!

### Solve
**Flag:** `pwn.college{8BcIusB4oZWOcjvsLyKfyU3zJI5.dRjM4QDLxATN1czW}`

``` 
bash
Connected!
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{8BcIusB4oZWOcjvsLyKfyU3zJI5.dRjM4QDLxATN1czW}
hacker@globbing~matching-paths-with-:~$ 
```
A bunch of files in /challenge/files. Starting from your home directory, run /challenge/run with a single argument that bracket-globs into the absolute paths to the file_b, file_a, file_s, and file_h files

## 5 Multiple globs
So far, you've specified one glob at a time, but you can do more! Bash supports the expansion of multiple globs in a single word. For example:

hacker@dojo:~$ cat /*fl*
pwn.college{YEAH}
hacker@dojo:~$
What happens above is that the shell looks for all files in / that start with anything (including nothing), then have an f and an l, and end in anything (including ag, which makes flag).

Now you try it. We put a few happy, but diversely-named files in /challenge/files. Go cd there and run /challenge/run, providing a single argument: a short (3 characters or less) globbed word with two * globs in it that covers every word that contains the letter p.

### Solve
**Flag:** ` pwn.college{ouOh4hWEVFgx1Cctannt6KzNMrO.QXycTO2EDLxATN1czW}`

``` bash
Connected!
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{ouOh4hWEVFgx1Cctannt6KzNMrO.QXycTO2EDLxATN1czW}
hacker@globbing~multiple-globs:/challenge/files$
```
Few files in /challenge/files. Go cd there and run /challenge/run, providing a single argument: a short (3 characters or less) globbed word with two * globs in it that covers every word that contains the letter p. Therefore `*p*` made the most sense.

## 6 Mixing globs
Now, let's put the previous levels together! We put a few happy, but diversely-named files in /challenge/files. Go cd there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to /challenge/run) will match the files "challenging", "educational", and "pwning"!

### Solve
**Flag:** ` `

``` bash
Connected!
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{MDaC0fwq2zps5ZIusUxhEkxYThH.dVjM4QDLxATN1czW}
hacker@globbing~mixing-globs:/challenge/files$ 

```
Few files in /challenge/files. Go cd there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to /challenge/run) will match the files "challenging", "educational", and "pwning". Therefore `[cep]*` made the most sense.

## 7 Exclusionary globbing
Sometimes, you want to filter out files in a glob! Luckily, [] helps you do just this. If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed. For example:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[!ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[^ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
Armed with this knowledge, go forth to /challenge/files and run /challenge/run with all files that don't start with p, w, or n!

NOTE: The ! character has a different special meaning in bash when it's not the first character of a [] glob, so keep that in mind if things stop making sense! ^ does not have this problem, but is also not compatible with older shells.

### Solve
**Flag:** ` pwn.college{sPOjd6mh0v1t1cSIwYHusZzUdZR.dZjM4QDLxATN1czW} `

``` 
bash
Connected!
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{sPOjd6mh0v1t1cSIwYHusZzUdZR.dZjM4QDLxATN1czW}
hacker@globbing~exclusionary-globbing:/challenge/files$ 

```
Go to /challenge/files and run /challenge/run with all files that don't start with p, w, or n. The ! character has a different special meaning in bash when it's not the first character of a [] glob, so keep that in mind if things stop making sense! ^ does not have this problem, but is also not compatible with older shells. Therefore `[!pwn]*` made the most sense.

## 8 Tab completion
As tempting as it might be, using * to shorten what must be typed on the commandline can lead to mistakes. Your glob might expand to unintended files, and you might not spot it until the rm command is already running! No one is safe from this style of error.

A safer alternative when you are trying to specify a specific target is tab completion. If you hit tab in the shell, it'll try to figure out what you're going to type and automatically complete it. Auto-completion is super useful, and this challenge will explore its use in specifying files.

This challenge has copied the flag into /challenge/pwncollege, and you can freely cat that file. But you can't type the filename: we used some serious trickery to make sure that you must tab-complete it. Try it out!

hacker@dojo:~$ ls /challenge
DESCRIPTION.md  pwncollege
hacker@dojo:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@dojo:~$ cat /challenge/pwn<TAB>
pwn.college{HECK YEAH}
hacker@dojo:~$

### Solve
**Flag:** `pwn.college{g3zIssPg6LtjY35oCUlvr_5xivo.QX0QTM3EDLxATN1czW}`

``` 
bash
Connected!
hacker@globbing~tab-completion:~$ /challenge/pwncollege
bash: /challenge/pwncollege: No such file or directory
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege​ 
pwn.college{g3zIssPg6LtjY35oCUlvr_5xivo.QX0QTM3EDLxATN1czW}
hacker@globbing~tab-completion:~$ 

```
Just using tab to complete arguments.

## 9 Multiple options for tab completion
Consider the following situation:

hacker@dojo:~$ ls
flag  flamingo  flowers
hacker@dojo:~$ cat f<TAB>
There are multiple options! What happens?

What happens varies based on the specific shell and its options. By default bash will auto-expand until the first point when there are multiple options (in this case, fl). When you hit tab a second time, it'll print out those options. Other shells and configurations, instead, will cycle through the options.

This challenge has a /challenge/files directory with a bunch of files starting with pwncollege. Tab-complete from /challenge/files/p or so, and make your way to the flag!

### Solve
**Flag:** `pwn.college{EERiKk2IxCLi7CPgeTz73PzpoZq.QX2QTM3EDLxATN1czW}`

``` 
bash
Connected!
hacker@globbing~multiple-options-for-tab-completion:~$ cd /challenge/files/pwncollege-
pwncollege-family      pwncollege-flamingo    pwncollege-hacking
pwncollege-flag        pwncollege-flyswatter  
hacker@globbing~multiple-options-for-tab-completion:~$ cd /challenge/files/pwncollege-fla
pwncollege-flag      pwncollege-flamingo  
hacker@globbing~multiple-options-for-tab-completion:~$ cd /challenge/files/pwncollege-flag
bash: cd: /challenge/files/pwncollege-flag: Not a directory
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-flag
pwn.college{EERiKk2IxCLi7CPgeTz73PzpoZq.QX2QTM3EDLxATN1czW}
hacker@globbing~multiple-options-for-tab-completion:~$ 
```
By default bash will auto-expand until the first point when there are multiple options (in this case, fl). When you hit tab a second time, it'll print out those options. Other shells and configurations, instead, will cycle through the options.

## 10 tab completion on commands
Tab completion is for more than files! You can also tab-complete commands. This level has a command that starts with pwncollege, and it'll give you the flag. Type pwncollege and hit the tab key to auto-complete it!

NOTE: You can auto-complete any command, but be careful: callous auto-completes without double-checking the result can wreak havoc in your shell if you accidentally run the wrong commands!

### Solve
**Flag:** `pwn.college{MBOBXfAPI1NYNtRcy_m_YzPwAzk.QX1QTM3EDLxATN1czW}`

``` 
bash
Connected!
hacker@globbing~tab-completion-on-commands:~$ pwncollege-9496 
Correct! Here is your flag:
pwn.college{MBOBXfAPI1NYNtRcy_m_YzPwAzk.QX1QTM3EDLxATN1czW}
hacker@globbing~tab-completion-on-commands:~$
```
Tab completion of commands.

## New Learnings
echo Look: is just echo with Look: too as args, * matches 0 or more characters, ? matches with exactly 1 character,
The square brackets are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets.
The ! character has a different special meaning in bash when it's not the first character of a [] glob, so keep that in mind if things stop making sense! ^ does not have this problem, but is also not compatible with older shells.

## References 
Linux Luminarium
