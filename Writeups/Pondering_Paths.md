# Pondering Paths
This module will teach you the basics of Linux file paths!

The Linux filesystem is a "tree". That is, it has a root (written as /). The root of the filesystem is a directory, and every directory can contain other directories and files. You refer to files and directories by their path. A path from the root of the filesystem starts with / (that is, the root of the filesystem), and describes the set of directories that must be descended into to find the file. Every piece of the path is demarcated with another /.

Armed with this knowledge, go forth and tackle the challenges below.


## 1 The Root
Alright, so the filesystem starts at /. Under that, there are a whole mess of other directories, configuration files, programs, and, most importantly, flags. In this level, we've added a program right in /, called pwn, that will give you the flag. All you need to do for this level is to invoke this program!

You can invoke a program by providing its path on the command line. In this case, you'll be giving the exact path, starting from /, so the path would be /pwn. This style of path, one that starts with the root directory, is referred to as an "absolute path".

### Solve
**Flag:** `pwn.college{IRcGaNEurjbISsUktFiBaRqMLMS.dhzN5QDLxATN1czW}`

``` 
bash
(base) debrato@debratolaptop:~/Desktop/Coding/pwn.college_debrato$ ssh -i ./key hacker@dojo.pwn.college
Connected!
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{IRcGaNEurjbISsUktFiBaRqMLMS.dhzN5QDLxATN1czW}
hacker@paths~the-root:~$ 
```
Just had to use the absolute path oto invoke to get the flag.

## 2 Program and absolute paths
Let's explore a slightly more complicated path! Except for in the previous level, challenges in pwn.college are in the challenge directory and the challenge directory is, in turn, right in the root directory (/). The path to the challenge directory is, thus, /challenge. The name of the challenge program in this level is run, and it lives in the /challenge directory. Thus, the path to the run challenge program is /challenge/run.

This challenge again requires you to execute it by invoking its absolute path. You'll want to execute the run file that is in the challenge directory that is, in turn, in the / directory. If you invoke the challenge correctly, it will give you the flag. Good luck!



### Solve
**Flag:** `pwn.college{8ur2RbeQFT8HGTSsLpcGId4Zf-d.dVDN1QDLxATN1czW}`

``` 
bash
Connected!
hacker@paths~program-and-absolute-paths:~$  /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{8ur2RbeQFT8HGTSsLpcGId4Zf-d.dVDN1QDLxATN1czW}
hacker@paths~program-and-absolute-paths:~$ 
```
I had to use absolute path here where tehre was a `/challenge` directory and had to run the program named run.

## 3 Position thyself
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ~ was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

### Solve
**Flag:** `pwn.college{QZxiS6S0JblIPywaA2xRej4JmZe.dZDN1QDLxATN1czW}`

``` 
bash
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /usr/share/build-essential directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-thy-self:~$ cd /usr/share/build-essential/
hacker@paths~position-thy-self:/usr/share/build-essential$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{QZxiS6S0JblIPywaA2xRej4JmZe.dZDN1QDLxATN1czW}
hacker@paths~position-thy-self:/usr/share/build-essential$ 
```
I had to run `/chalenge/run` then I got the directory where I had to go and rerun that program to get the flag.

## 4 Position elsewhere
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ~ was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

### Solve
**Flag:** `pwn.college{MFAgPN9AxIQSdEg9c_Kc8SbKujf.ddDN1QDLxATN1czW}`


``` 
bash
Connected!
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /proc/131/fd directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-elsewhere:~$ cd /proc/1
1/   125/ 131/ 
hacker@paths~position-elsewhere:~$ cd /proc/131/fd
hacker@paths~position-elsewhere:/proc/131/fd$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{MFAgPN9AxIQSdEg9c_Kc8SbKujf.ddDN1QDLxATN1czW}
hacker@paths~position-elsewhere:/proc/131/fd$ 
```
Like the previous challenge, had to run `/chalenge/run` then I got the directory where I had to go and rerun that program to get the flag.

## 5 Position yet elsewhere
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ~ was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

### Solve
**Flag:** `pwn.college{UGnvYCVlTE66omssoDbhoc3l1Vm.dhDN1QDLxATN1czW}`


``` 
bash
Connected!
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /etc/apt/sources.list.d directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-yet-elsewhere:~$ cd /etc/ap
apache2/    apparmor.d/ apport/     apt/        
hacker@paths~position-yet-elsewhere:~$ cd /etc/apt/sources.list
sources.list    sources.list.d/ 
hacker@paths~position-yet-elsewhere:~$ cd /etc/apt/sources.list.d
hacker@paths~position-yet-elsewhere:/etc/apt/sources.list.d$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{UGnvYCVlTE66omssoDbhoc3l1Vm.dhDN1QDLxATN1czW}
hacker@paths~position-yet-elsewhere:/etc/apt/sources.list.d$ 
```
Like the previous challenge, had to run `/chalenge/run` then I got the directory where I had to go and rerun that program to get the flag.


## 6 Implicit Relative Paths from /
Now you're familiar with the concept of referring to absolute paths and changing directories. If you put in absolute paths everywhere, then it really doesn't matter what directory you are in, as you likely found out in the previous three challenges.

However, the current working directory does matter for relative paths.

A relative path is any path that does not start at root (i.e., it does not start with /).
A relative path is interpreted relative to your current working directory (cwd).
Your cwd is the directory that your prompt is currently located at.
This means how you specify a particular file, depends on where the terminal prompt is located.

Imagine we want to access some file located at /tmp/a/b/my_file.

If my cwd is /, then a relative path to the file is tmp/a/b/my_file.
If my cwd is /tmp, then a relative path to the file is a/b/my_file.
If my cwd is /tmp/a/b/c, then a relative path to the file is ../my_file. The .. refers to the parent directory.
Let's try it here! You'll need to run /challenge/run using a relative path while having a current working directory of /. For this level, I'll give you a hint. Your relative path starts with the letter c 😊

### Solve
**Flag:** `pwn.college{sS9h_0ehLArascu86Otf90rLRHf.dlDN1QDLxATN1czW}`


``` 
bash
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{sS9h_0ehLArascu86Otf90rLRHf.dlDN1QDLxATN1czW}
hacker@paths~implicit-relative-paths-from-:/$ 

```
They already mentioned relative path so no `/` required but ned to cd into it and starts with c so it must have been challenge so it was `challenge/run`.

## 7 Explicit relative paths from /
Previously, your relative path was "naked": it directly specified the directory to descend into from the current directory. In this level, we're going to explore more explicit relative paths.

In most operating systems, including Linux, every directory has two implicit entries that you can reference in paths: . and ... The first, ., refers right to the same directory, so the following absolute paths are all identical to each other:

/challenge
/challenge/.
/challenge/./././././././././
/./././challenge/././
The following relative paths are also all identical to each other:

challenge
./challenge
./././challenge
challenge/.
Of course, if your current working directory is /, the above relative paths are equivalent to the above absolute paths.

This challenge will get you using . in your relative paths. Get ready!

### Solve
**Flag:** `pwn.college{IEz_wp4xYrVVsPG5pQgjn2_hDqL.dBTN1QDLxATN1czW}`


``` 
bash
hacker@paths~explicit-relative-paths-from-:~$ cd /
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{IEz_wp4xYrVVsPG5pQgjn2_hDqL.dBTN1QDLxATN1czW}
hacker@paths~explicit-relative-paths-from-:/$ 

```
They already mentioned relative path so no `/` required but ned to cd into it and invoke using current directory so `./challenge/run`.

## 8 Implicit Relative path
In this level, we'll practice referring to paths using . a bit more. This challenge will need you to run it from the /challenge directory. Here, things get slightly tricky.

Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path. Consider the following:

hacker@dojo:~$ cd /challenge
hacker@dojo:/challenge$ run
This will not invoke /challenge/run. This is actually a safety measure: if Linux searched the current directory for programs every time you entered a naked path, you could accidentally execute programs in your current directory that happened to have the same names as core system utilities! As a result, the above commands will yield the following error:

bash: run: command not found
We'll explore the mechanisms behind this concept later, but in this challenge, we'll learn how to explicitly use relative paths to launch run in this scenario. The way to do this is to tell Linux that you explicitly want to execute a program in the current directory, using . like in the previous levels. Give it a try now!

### Solve
**Flag:** `pwn.college{YmOb4w_GeBmZqVygUylXFltT8K6.dFTN1QDLxATN1czW}`


``` 
bash
Connected!
hacker@paths~implicit-relative-path:~$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ run
bash: run: command not found
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{YmOb4w_GeBmZqVygUylXFltT8K6.dFTN1QDLxATN1czW}
hacker@paths~implicit-relative-path:/challenge$ 
```
We need to invoke using current directory `/challenge' using `./`, to invoke program `run` we need path if we go inside directory and write its name it gives error `bash:command not found` so we invoke it with its path `./run`.

## 8 Home sweet Home
Every user has a home directory, typically under /home in the filesystem. In the dojo, you are the hacker user, and your home directory is /home/hacker. The home directory is typically where users store most of their personal files. As you make your way through pwn.college, this is where you'll store most of your solutions.

Typically, your shell session will start with your home directory as your current working directory. Consider the initial prompt:

hacker@dojo:~$
The ~ in this prompt is the current working directory, with ~ being shorthand for /home/hacker. Bash provides and uses this shorthand because, again, most of your time will be spent in your home directory. Thus, whenever bash sees ~ provided as the start of an argument in a way consistent with a path, it will expand it to your home directory. Consider:

hacker@dojo:~$ echo LOOK: ~
LOOK: /home/hacker
hacker@dojo:~$ cd /
hacker@dojo:/$ cd ~
hacker@dojo:~$ cd ~/asdf
hacker@dojo:~/asdf$ cd ~/asdf
hacker@dojo:~/asdf$ cd ~
hacker@dojo:~$ cd /home/hacker/asdf
hacker@dojo:~/asdf$
Note that the expansion of ~ is an absolute path, and only the leading ~ is expanded. This means, for example, that ~/~ will be expanded to /home/hacker/~ rather than /home/hacker/home/hacker.

Fun fact: cd will use your home directory as the default destination:

hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ cd
hacker@dojo:~$
Now it's your turn to play! In this challenge, /challenge/run will write a copy of the flag to any file you specify as an argument on the commandline, with these constraints:

Your argument must be an absolute path.
The path must be inside your home directory.
Before expansion, your argument must be three characters or less.
Again, you must specify your path as an argument to /challenge/run as so:

hacker@dojo:~$ /challenge/run YOUR_PATH_HERE

### Solve
**Flag:** ``


``` 
bash
Connected!
hacker@paths~home-sweet-home:~$ ~
bash: /home/hacker: Is a directory
hacker@paths~home-sweet-home:~$ ls
COLLEGE         MYFLAG  asdf      file.txt   instructions  out.txt    x.sh
DESCRIPTION.md  PWN     c         file1.txt  myflag        script.sh
Desktop         a       data.txt  hello.txt  not-the-flag  the-flag
hacker@paths~home-sweet-home:~$ cat MYFLAG 
hacker@paths~home-sweet-home:~$ cat myflag 

[FLAG] Here is your flag:
[FLAG] pwn.college{Y6wsfwtE8dZlAxFrdY-ICtTwPo8.ddjN1QDLxATN1czW}

hacker@paths~home-sweet-home:~$ cat instructions 
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will check that error output is redirected to a specific file path : instructions
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!

[TEST] You should have redirected my stderr to instructions. Checking...

[PASS] The file at the other end of my stderr looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@paths~home-sweet-home:~$ /challenge/run ~/flag
The argument you provided must not have been longer than 3 characters (it's 
currently 6 characters long)!
hacker@paths~home-sweet-home:~$ /challenge/run ~/a
Writing the file to /home/hacker/a!
... and reading it back to you:
pwn.college{ES27AZlBeYU1tT0__U_bQt1BKzw.dNzM4QDLxATN1czW}
hacker@paths~home-sweet-home:~$ 
```
I initially used `ls`  and cat to get the flag directly, but later followed what the instructions said t use `/challenge/run` with a path from home dir as an argument.

## New Learnings
root /, absolute path, relative path, invoke using current directory using `./`, to invoke program we need path if we go inside directory and write its name it gives erro `bash:command not found`.

## References 
Linux Luminarium
