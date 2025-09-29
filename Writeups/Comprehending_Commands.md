# Comprehending Commands
This module will expose you to some useful Linux commands that will serve you well for the rest of your journey here! It is FAR from an exhaustive list, and we'll continue to expand this module, but this should be enough to get you started.

So, without further ado, let's learn some commands!


## 1 cat: no the pet, but the command!
One of the most critical Linux commands is cat. cat is most often used for reading out files, like so:

hacker@dojo:~$ cat /challenge/DESCRIPTION.md
One of the most critical Linux commands is `cat`.
`cat` is most often used for reading out files, like so:
cat will concatenate (hence the name) multiple files if provided multiple arguments. For example:

hacker@dojo:~$ cat myfile
This is my file!
hacker@dojo:~$ cat yourfile
This is your file!
hacker@dojo:~$ cat myfile yourfile
This is my file!
This is your file!
hacker@dojo:~$ cat myfile yourfile myfile
This is my file!
This is your file!
This is my file!
Finally, if you give no arguments at all, cat will read from the terminal input and output it. We'll explore that in later challenges...

In this challenge, I will copy the flag to the flag file in your home directory (where your shell starts). Go read it with cat!



### Solve
**Flag:** `pwn.college{gZs-dZTVCtdHqY06KtPof-NUOo6.dFzN1QDLxATN1czW}`

``` 
bash
Connected!
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{gZs-dZTVCtdHqY06KtPof-NUOo6.dFzN1QDLxATN1czW}
hacker@commands~cat-not-the-pet-but-the-command:~$ 
```
Just had to cat the flag file which was in the home dir ie where the shell started.

## 2 catting absolute paths
In the last level, you did cat flag to read the flag out of your home directory! You can, of course, specify cat's arguments as absolute paths:

hacker@dojo:~$ cat /challenge/DESCRIPTION.md
In the last level, you did `cat flag` to read the flag out of your home directory!
You can, of course, specify `cat`'s arguments as absolute paths:
...
In this directory, I will not copy it to your home directory, but I will make it readable. You can read it with cat at its absolute path: /flag.

FUN FACT: /flag is where the flag always lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

### Solve
**Flag:** `pwn.college{kEsNkh58AZdb4PVGaQ3d2TGRDfJ.dlTM5QDLxATN1czW}`

``` 
bash
Connected!
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{kEsNkh58AZdb4PVGaQ3d2TGRDfJ.dlTM5QDLxATN1czW}
hacker@commands~catting-absolute-paths:~$ 
```
Just had to cat the flag file via absolute path which was in the home dir ie where the shell started.

## 3 more catting practice
You can specify all sorts of paths as arguments to commands, and we'll practice some more with cat. In this level, I'll put the flag in some crazy directory, and I will not allow you to change directories with cd, so no cat flag for you. You must retrieve the flag by absolute path, wherever it is.

### Solve
**Flag:** `pwn.college{QtadBccpNNQBiT5Wvn8qRAhH3Mc.dBjM5QDLxATN1czW}`

``` 
bash
Connected!
You cannot use the 'cd' command in this level, and must retrieve the flag by 
absolute path. Plus, I hid the flag in a different directory! You can find it 
in the file /usr/share/gtksourceview-4/flag. Go cat it out **without** cding 
into that directory!
hacker@commands~more-catting-practice:~$ cat /usr/share/gtksourceview-4/flag
pwn.college{QtadBccpNNQBiT5Wvn8qRAhH3Mc.dBjM5QDLxATN1czW}
hacker@commands~more-catting-practice:~$ 


```
Just had to use the absolute path given to invoke to get the flag.

## 4 grepping for a needle in a haystack
Sometimes, the files that you might cat out are too big. Luckily, we have the grep command to search for the contents we need! We'll learn it in this challenge.

There are many ways to grep, and we'll learn one way here:

hacker@dojo:~$ grep SEARCH_STRING /path/to/file
Invoked like this, grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

In this challenge, I've put a hundred thousand lines of text into the /challenge/data.txt file. grep it for the flag!

HINT: The flag always starts with the text pwn.college.

### Solve
**Flag:** `pwn.college{goV0uO1Id9ESvxNb5hKYUoNAppY.ddTM4QDLxATN1czW}`

``` 
bash
Connected!
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{goV0uO1Id9ESvxNb5hKYUoNAppY.ddTM4QDLxATN1czW}
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ 
```
Because the flag always starts with the text pwn.college we can directly grep `pwn.college` with the given path.
## 5 comparing files
When looking for changes between similar files, eyeballing them might not be the most efficient approach! This is where the diff command becomes invaluable.

diff compares two files line by line and shows you exactly what's different between them. For example:

hacker@dojo:~$ cat file1
hello
world
hacker@dojo:~$ cat file2
hello
universe
hacker@dojo:~$ diff file1 file2
2c2
< world
---
> universe
The output tells us that line 2 changed (2c2), with world in the first file (<) being replaced by universe in the second file (>).

Sometimes, when new lines are added, you'll see something like:

hacker@dojo:~$ cat old
pwn
hacker@dojo:~$ cat new
pwn
college
hacker@dojo:~$ diff old new
1a2
> college
This tells us that after line 1 in the first file, the second file has an additional line (1a2 means "after line 1 of file1, add line 2 of file2").

Now for your challenge! There are two files in /challenge:

/challenge/decoys_only.txt contains 100 fake flags
/challenge/decoys_and_real.txt contains all 100 fake flags plus the one real flag
Use diff to find what's different between these files and get your flag!

### Solve
**Flag:** `< pwn.college{Q7IQgO0B-N_-71EguufdUjAxLdN.QXzAzM4EDLxATN1czW}`

``` 
bash
Connected!
hacker@commands~comparing-files:~$ diff /challenge/decoys_and_real.txt  /challenge/decoys_only.txt
100d99
< pwn.college{Q7IQgO0B-N_-71EguufdUjAxLdN.QXzAzM4EDLxATN1czW}
hacker@commands~comparing-files:~$ 

```
`diff` command can find out difference between two files.

## 6 listing files
So far, we've told you which files to interact with. But directories can have lots of files (and other directories) inside them, and we won't always be here to tell you their names. You'll need to learn to list their contents using the ls command!

ls will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided. Observe:

hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$
In this challenge, we've named /challenge/run with some random name! List the files in /challenge to find it.

### Solve
**Flag:** `pwn.college{Uu8-iMQ4f_i3ErPCK9sl-tn0ff3.dhjM4QDLxATN1czW}`

``` 
bash
hacker@commands~listing-files:~$ ls /challenge
19528-renamed-run-8168  DESCRIPTION.md
hacker@commands~listing-files:~$ /challenge/19528-renamed-run-8168 
Yahaha, you found me! Here is your flag:
pwn.college{Uu8-iMQ4f_i3ErPCK9sl-tn0ff3.dhjM4QDLxATN1czW}
hacker@commands~listing-files:~$ 

```
`ls` used to list all files in current dir or with given path and then run that file for flag.

## 7 touching files
Of course, you can also create files! There are several ways to do this, but we'll look at a simple command here. You can create a new, blank file by touching it with the touch command:

hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ touch pwnfile
hacker@dojo:/tmp$ ls
pwnfile
hacker@dojo:/tmp$
It's that simple! In this level, please create two files: /tmp/pwn and /tmp/college, and run /challenge/run to get your flag!

### Solve
**Flag:** `pwn.college{QpKqfky-5_RltuPv0l31WvVYpTQ.dBzM4QDLxATN1czW}`

``` 
bash
Connected!
hacker@commands~touching-files:~$ /challenge/run
Uh oh! /tmp/pwn does not exist. Please use the 'touch' command to create it!
hacker@commands~touching-files:~$ touch /tmp/pwn
hacker@commands~touching-files:~$ touch /tmp/college
hacker@commands~touching-files:~$ /challenge/run
Success! Here is your flag:
pwn.college{QpKqfky-5_RltuPv0l31WvVYpTQ.dBzM4QDLxATN1czW}
hacker@commands~touching-files:~$ 

```
THis challenge required me to create two new files using `touch` and then run the program to get the flag.
## 8 removing files
Files are all around you. Like candy wrappers, there'll eventually be too many of them. In this level, we'll learn to clean up!

In Linux, you remove files with the rm command, as so:

hacker@dojo:~$ touch PWN
hacker@dojo:~$ touch COLLEGE
hacker@dojo:~$ ls
COLLEGE     PWN
hacker@dojo:~$ rm PWN
hacker@dojo:~$ ls
COLLEGE
hacker@dojo:~$
Let's practice. This challenge will create a delete_me file in your home directory! Delete it, then run /challenge/check, which will make sure you've deleted it and then give you the flag!

### Solve
**Flag:** `pwn.college{E-wAXBPQxGVrhbrIq43pNVel-Ee.dZTOwUDLxATN1czW}`

``` 
bash
Connected!
hacker@commands~removing-files:~$ /challenge/check
It looks like /home/hacker/delete_me still exists! rm it.
hacker@commands~removing-files:~$ ls
COLLEGE         PWN   data.txt   hello.txt     out.txt
DESCRIPTION.md  a     delete_me  instructions  script.sh
Desktop         asdf  file.txt   myflag        the-flag
MYFLAG          c     file1.txt  not-the-flag  x.sh
hacker@commands~removing-files:~$ rm delete_me 
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{E-wAXBPQxGVrhbrIq43pNVel-Ee.dZTOwUDLxATN1czW}
hacker@commands~removing-files:~$ 


```
Used `rm` command to delete file then ran `/challenge/check` for the flag.

## 9 moving files
You can also move files around with the mv command. The usage is simple:

hacker@dojo:~$ ls
my-file
hacker@dojo:~$ cat my-file
PWN!
hacker@dojo:~$ mv my-file your-file
hacker@dojo:~$ ls
your-file
hacker@dojo:~$ cat your-file
PWN!
hacker@dojo:~$
This challenge wants you to move the /flag file into /tmp/hack-the-planet (do it)! When you're done, run /challenge/check, which will check things out and give the flag to you.

### Solve
**Flag:** `pwn.college{kk9NTyH5kkaX8PC1jh4B9MqFGQb.QX5ETM3EDLxATN1czW}`

``` 
bash
Connected!
hacker@commands~moving-files:~$ /challenge/check
Uh oh! /tmp/hack-the-planet doesn't exist...
hacker@commands~moving-files:~$ ls
COLLEGE         MYFLAG  asdf      file.txt   instructions  out.txt    x.sh
DESCRIPTION.md  PWN     c         file1.txt  myflag        script.sh
Desktop         a       data.txt  hello.txt  not-the-flag  the-flag
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{kk9NTyH5kkaX8PC1jh4B9MqFGQb.QX5ETM3EDLxATN1czW}
hacker@commands~moving-files:~$ 

```
Moved `/flag` to `/tmp/hack-the-planet` using `mv` and ran the check program for the flag. 

## 10 hidden files
Interestingly, ls doesn't list all the files by default. Linux has a convention where files that start with a . don't show up by default in ls and in a few other contexts. To view them with ls, you need to invoke ls with the -a flag, as so:

hacker@dojo:~$ touch pwn
hacker@dojo:~$ touch .college
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
hacker@dojo:~$
Now, it's your turn! Go find the flag, hidden as a dot-prepended file in /.

### Solve
**Flag:** `pwn.college{EiR41yz8IFODwtwBkTgPGqYmIxN.dBTN4QDLxATN1czW}`

``` 
bash
Connected!
hacker@commands~hidden-files:~$ ls -a /
.                      bin        etc    lib64   nix   run   tmp
..                     boot       home   libx32  opt   sbin  usr
.dockerenv             challenge  lib    media   proc  srv   var
.flag-274892722913504  dev        lib32  mnt     root  sys
hacker@commands~hidden-files:~$ cat /.flag-274892722913504 
pwn.college{EiR41yz8IFODwtwBkTgPGqYmIxN.dBTN4QDLxATN1czW}
hacker@commands~hidden-files:~$
```
Had to use 'ls -a` to get hidden files in `/` dir.

## 11 An epic filesystem quest

With your knowledge of cd, ls, and cat, we're ready to play a little game!

We'll start it out in /. Normally:

hacker@dojo:~$ cd /
hacker@dojo:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  dev        flag  lib   lib64  media   opt  root  sbin  sys  usr
That's a lot of contents! One day, you will be quite familiar with them, but already, you might recognize the flag file and the challenge directory.

In this challenge, I have hidden the flag! Here, you will use ls and cat to follow my breadcrumbs and find it! Here's how it'll work:

Your first clue is in /. Head on over there.
Look around with ls. There'll be a file named HINT or CLUE or something along those lines!
cat that file to read the clue!
Depending on what the clue says, head on over to the next directory (or don't!).
Follow the clues to the flag!
Good luck!

### Solve
**Flag:** `It is: pwn.college{grUZEfPbAiElainHZV4QInU8a19.dljM4QDLxATN1czW}`

``` 
bash
Connected!
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
SECRET  challenge  flag  lib32   media  opt   run   sys  var
bin     dev        home  lib64   mnt    proc  sbin  tmp
boot    etc        lib   libx32  nix    root  srv   usr
hacker@commands~an-epic-filesystem-quest:/$ cat SECRET 
Lucky listing!
The next clue is in: /usr/share/racket/pkgs/htdp-lib/2htdp
hacker@commands~an-epic-filesystem-quest:/$ cat /usr/share/racket/pkgs/htdp-lib/2htdp/
cat: /usr/share/racket/pkgs/htdp-lib/2htdp/: Is a directory
hacker@commands~an-epic-filesystem-quest:/$ cd /usr/share/racket/pkgs/htdp-lib/2htdp/
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/htdp-lib/2htdp$ ls
NUGGET           image.rkt   planetcute      universe-request.txt
abstraction.rkt  info.rkt    planetcute.rkt  universe-syntax-parse.rkt
batch-io.rkt     itunes.rkt  private         universe.rkt
compiled         langs.txt   uchat           web-io.rkt
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/htdp-lib/2htdp$ ls -a
.                compiled    planetcute            universe-syntax-parse.rkt
..               image.rkt   planetcute.rkt        universe.rkt
NUGGET           info.rkt    private               web-io.rkt
abstraction.rkt  itunes.rkt  uchat
batch-io.rkt     langs.txt   universe-request.txt
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/htdp-lib/2htdp$ cat NUGGET 
Tubular find!
The next clue is in: /usr/local/lib/python3.8/dist-packages/networkx/algorithms/minors/tests/__pycache__

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/htdp-lib/2htdp$ cd /usr/local/lib/python3.8/dist-packages/networkx/algorithms/minors/tests/__pycache__
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/networkx/algorithms/minors/tests/__pycache__$ ls -a
.  ..  INFO  test_contraction.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/networkx/algorithms/minors/tests/__pycache__$ cat INFO 
Great sleuthing!
The next clue is in: /opt/linux/linux-5.4/arch/arm64/boot/dts/actions

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/networkx/algorithms/minors/tests/__pycache__$ ^C
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/networkx/algorithms/minors/tests/__pycache__$ ls -a /opt/linux/linux-5.4/arch/arm64/boot/dts/actions
.   LEAD-TRAPPED  s700-cubieboard7.dts  s900-bubblegum-96.dts
..  Makefile      s700.dtsi             s900.dtsi
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/networkx/algorithms/minors/tests/__pycache__$ cat -a /opt/linux/linux-5.4/arch/arm64/boot/dts/actions/LEAD-TRAPPED 
cat: invalid option -- 'a'
Try 'cat --help' for more information.
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/networkx/algorithms/minors/tests/__pycache__$ cat /opt/linux/linux-5.4/arch/arm64/boot/dts/actions/LEAD-TRAPPED 
Lucky listing!
The next clue is in: /opt/linux/linux-5.4/arch/arm/mach-highbank

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/networkx/algorithms/minors/tests/__pycache__$ cd /opt/linux/linux-5.4/arch/arm/mach-highbank
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/arm/mach-highbank$ ls -a
.   DOSSIER  Makefile  highbank.c  smc.S      system.c
..  Kconfig  core.h    pm.c        sysregs.h
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/arm/mach-highbank$ cat Makefile 
# SPDX-License-Identifier: GPL-2.0-only
obj-y					:= highbank.o system.o smc.o

obj-$(CONFIG_PM_SLEEP)			+= pm.o
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/arm/mach-highbank$ cat DOSSIER 
Great sleuthing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/selenium/webdriver/safari/__pycache__

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/arm/mach-highbank$ ls -a /usr/local/lib/python3.8/dist-packages/selenium/webdriver/safari/__pycache__
.        __init__.cpython-38.pyc     remote_connection.cpython-38.pyc
..       options.cpython-38.pyc      service.cpython-38.pyc
.TEASER  permissions.cpython-38.pyc  webdriver.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/arm/mach-highbank$ cat /usr/local/lib/python3.8/dist-packages/selenium/webdriver/safari/__pycache__/.TEASER
Tubular find!
The next clue is in: /usr/lib/python3/dist-packages/sage/combinat/ncsf_qsym/__pycache__

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/arm/mach-highbank$ ls /usr/lib/python3/dist-packages/sage/combinat/ncsf_qsym/__pycache__
CUE-TRAPPED                   generic_basis_code.cpython-38.pyc
__init__.cpython-38.pyc       ncsf.cpython-38.pyc
all.cpython-38.pyc            qsym.cpython-38.pyc
combinatorics.cpython-38.pyc  tutorial.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/arm/mach-highbank$ cat /usr/lib/python3/dist-packages/sage/combinat/ncsf_qsym/__pycache__/CUE-TRAPPED 
Great sleuthing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/jedi/third_party/typeshed/stdlib/3.9

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/arm/mach-highbank$ ls -a /usr/local/lib/python3.8/dist-packages/jedi/third_party/typeshed/stdlib/3.9
.  ..  .DISPATCH  graphlib.pyi  zoneinfo
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/arm/mach-highbank$ cat /usr/local/lib/python3.8/dist-packages/jedi/third_party/typeshed/stdlib/3.9/.DISPATCH 
Yahaha, you found me!
The next clue is in: /usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/STIX/IntegralsUpSm
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/arm/mach-highbank$ cd /usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/STIX/IntegralsUpSm
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/STIX/IntegralsUpSm$ LS 
bash: LS: command not found
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/STIX/IntegralsUpSm$ ls
Bold  Regular  SPOILER
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/STIX/IntegralsUpSm$ cat SPOILER 
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{grUZEfPbAiElainHZV4QInU8a19.dljM4QDLxATN1czW}
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/STIX/IntegralsUpSm$ 

```
This challenge was lengthy, repeating the concepts, key concept in that accessing the file without cd was using ls with the given absolute path and then cat with the given absolute path with the file.

## 12 making directories
We can create files. How about directories? You make directories using the mkdir command. Then you can stick files in there!

Watch:

hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ mkdir my_directory
hacker@dojo:/tmp$ ls
my_directory
hacker@dojo:/tmp$ cd my_directory
hacker@dojo:/tmp/my_directory$ touch my_file
hacker@dojo:/tmp/my_directory$ ls
my_file
hacker@dojo:/tmp/my_directory$ ls /tmp/my_directory/my_file
/tmp/my_directory/my_file
hacker@dojo:/tmp/my_directory$
Now, go forth and create a /tmp/pwn directory and make a college file in it! Then run /challenge/run, which will check your solution and give you the flag!

### Solve
**Flag:** `pwn.college{gt97Z-KM98llZeLrRY6Up4rlbge.dFzM4QDLxATN1czW}`

``` 
bash
Connected!
hacker@commands~making-directories:~$ /challenge/run 
Uh oh! /tmp/pwn does not exist as a directory. Please use the 'mkdir' command 
to create it!
hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ cd /tmp/pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ /challenge/run 
Success! Here is your flag:
pwn.college{gt97Z-KM98llZeLrRY6Up4rlbge.dFzM4QDLxATN1czW}
hacker@commands~making-directories:/tmp/pwn$ 

```
Created a new directory with a file using `mkdir and touch` .

## 13 finding files
So now we know how to list, read, and create files. But how do we find them? We use the find command!

The find command takes optional arguments describing the search criteria and the search location. If you don't specify a search criteria, find matches every file. If you don't specify a search location, find uses the current working directory (.). For example:

hacker@dojo:~$ mkdir my_directory
hacker@dojo:~$ mkdir my_directory/my_subdirectory
hacker@dojo:~$ touch my_directory/my_file
hacker@dojo:~$ touch my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find
.
./my_directory
./my_directory/my_subdirectory
./my_directory/my_subdirectory/my_subfile
./my_directory/my_file
hacker@dojo:~$
And when specifying the search location:

hacker@dojo:~$ find my_directory/my_subdirectory
my_directory/my_subdirectory
my_directory/my_subdirectory/my_subfile
hacker@dojo:~$
And, of course, we can specify the criteria! For example, here, we filter by name:

hacker@dojo:~$ find -name my_subfile
./my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find -name my_subdirectory
./my_directory/my_subdirectory
hacker@dojo:~$
You can search the whole filesystem if you want!

hacker@dojo:~$ find / -name hacker
/home/hacker
hacker@dojo:~$
Now it's your turn. I've hidden the flag in a random directory on the filesystem. It's still called flag. Go find it!

Several notes. First, there are other files named flag on the filesystem. Don't panic if the first one you try doesn't have the actual flag in it. Second, there're plenty of places in the filesystem that are not accessible to a normal user. These will cause find to generate errors, but you can ignore those; we won't hide the flag there! Finally, find can take a while; be patient!

### Solve
**Flag:** `pwn.college{sJUbcZBvb8i6w0dWu-TPZnuHp2p.dJzM4QDLxATN1czW}`

``` 
bash
Connected!
hacker@commands~finding-files:~$ find / -name
find: missing argument to `-name'
hacker@commands~finding-files:~$ find / -name flag
find: ‘/root’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
find: ‘/tmp/tmp.4mK6TfTSUV’: Permission denied
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/share/racket/pkgs/gui-lib/scribble/flag
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/log/private’: Permission denied
find: ‘/var/log/apache2’: Permission denied
find: ‘/var/log/mysql’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/mysql-keyring’: Permission denied
find: ‘/var/lib/php/sessions’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/mysql-files’: Permission denied
find: ‘/var/lib/mysql’: Permission denied
find: ‘/run/mysqld’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/proc/tty/driver’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/7/task/7/fd’: Permission denied
find: ‘/proc/7/task/7/fdinfo’: Permission denied
find: ‘/proc/7/task/7/ns’: Permission denied
find: ‘/proc/7/fd’: Permission denied
find: ‘/proc/7/map_files’: Permission denied
find: ‘/proc/7/fdinfo’: Permission denied
find: ‘/proc/7/ns’: Permission denied
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
/nix/store/7ns27apnvn4qj4q5c82x0z1lzixrz47p-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/5z3sjp9r463i3siif58hq5wj5jmy5m98-python3.12-pwntools-4.13.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/5n5lp1m8gilgrsriv1f2z0jdjk50ypcn-rizin-0.7.3/share/rizin/flag
/nix/store/h88mxp2mbgyj06vypwmqpy05idhwimnp-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/s8b49lb0pqwvw0c6kgjbxdwxcv2bp0x4-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/bnlabj2vsbljhp597ir29l51nrqhm89w-rizin-0.7.4/share/rizin/flag
/nix/store/1hyxipvwpdpcxw90l5pq1nvd6s6jdi5m-python3.12-pwntools-4.14.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag
hacker@commands~finding-files:~$ cat /opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
cat: /opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /nix/store/5z3sjp9r463i3siif58hq5wj5jmy5m98-python3.12-pwntools-4.13.1/lib/python3.12/site-packages/pwnlib/flag
cat: /nix/store/5z3sjp9r463i3siif58hq5wj5jmy5m98-python3.12-pwntools-4.13.1/lib/python3.12/site-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /nix/store/5n5lp1m8gilgrsriv1f2z0jdjk50ypcn-rizin-0.7.3/share/rizin/flag
cat: /nix/store/5n5lp1m8gilgrsriv1f2z0jdjk50ypcn-rizin-0.7.3/share/rizin/flag: Is a directory
hacker@commands~finding-files:~$ cat /nix/store/5n5lp1m8gilgrsriv1f2z0jdjk50ypcn-rizin-0.7.3/share/rizin/flag
cat: /nix/store/5n5lp1m8gilgrsriv1f2z0jdjk50ypcn-rizin-0.7.3/share/rizin/flag: Is a directory
hacker@commands~finding-files:~$ cat /nix/store/h88mxp2mbgyj06vypwmqpy05idhwimnp-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
cat: /nix/store/h88mxp2mbgyj06vypwmqpy05idhwimnp-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /nix/store/s8b49lb0pqwvw0c6kgjbxdwxcv2bp0x4-radare2-5.9.8/share/radare2/5.9.8/flag
cat: /nix/store/s8b49lb0pqwvw0c6kgjbxdwxcv2bp0x4-radare2-5.9.8/share/radare2/5.9.8/flag: Is a directory
hacker@commands~finding-files:~$ cat /nix/store/bnlabj2vsbljhp597ir29l51nrqhm89w-rizin-0.7.4/share/rizin/flag
cat: /nix/store/bnlabj2vsbljhp597ir29l51nrqhm89w-rizin-0.7.4/share/rizin/flag: Is a directory
hacker@commands~finding-files:~$ cat /nix/store/1hyxipvwpdpcxw90l5pq1nvd6s6jdi5m-python3.12-pwntools-4.14.1/lib/python3.12/site-packages/pwnlib/flag
cat: /nix/store/1hyxipvwpdpcxw90l5pq1nvd6s6jdi5m-python3.12-pwntools-4.14.1/lib/python3.12/site-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag
cat: /nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /usr/local/lib/python3.8/dist-packages/pwnlib/flag
cat: /usr/local/lib/python3.8/dist-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /usr/share/racket/pkgs/gui-lib/scribble/flag
pwn.college{sJUbcZBvb8i6w0dWu-TPZnuHp2p.dJzM4QDLxATN1czW}
hacker@commands~finding-files:~$ 
```
Used `find / -name flag` to search flag in `/` dir then `cat` into all of the output tediously.

## 14 linking files
If you use Linux (or computers) for any reasonable length of time to do any real work, you will eventually run into some variant of the following situation: you want two programs to access the same data, but the programs expect that data to be in two different locations. Luckily, Linux provides a solution to this quandary: links.

Links come in two flavors: hard and soft (also known as symbolic) links. We'll differentiate the two with an analogy:

A hard link is when you address your apartment using multiple addresses that all lead directly to the same place (e.g., Apt 2 vs Unit 2).
A soft link is when you move apartments and have the postal service automatically forward your mail from your old place to your new place.
In a filesystem, a file is, conceptually, an address at which the contents of that file live. A hard link is an alternate address that indexes that data --- accesses to the hard link and accesses to the original file are completely identical, in that they immediately yield the necessary data. A soft/symbolic link, instead, contains the original file name. When you access the symbolic link, Linux will realize that it is a symbolic link, read the original file name, and then (typically) automatically access that file. In most cases, both situations result in accessing the original data, but the mechanisms are different.

Hard links sound simpler to most people (case in point, I explained it in one sentence above, versus two for soft links), but they have various downsides and implementation gotchas that make soft/symbolic links, by far, the more popular alternative.

In this challenge, we will learn about symbolic links (also known as symlinks). Symbolic links are created with the ln command with the -s argument, like so:

hacker@dojo:~$ cat /tmp/myfile
This is my file!
hacker@dojo:~$ ln -s /tmp/myfile /home/hacker/ourfile
hacker@dojo:~$ cat ~/ourfile
This is my file!
hacker@dojo:~$
You can see that accessing the symlink results in getting the original file contents! Also, you can see the usage of ln -s. Note that the original file path comes before the link path in the command!

A symlink can be identified as such with a few methods. For example, the file command, which takes a filename and tells you what type of file it is, will recognize symlinks:

hacker@dojo:~$ file /tmp/myfile
/tmp/myfile: ASCII text
hacker@dojo:~$ file ~/ourfile
/home/hacker/ourfile: symbolic link to /tmp/myfile
hacker@dojo:~$
Okay, now you try it! In this level the flag is, as always, in /flag, but /challenge/catflag will instead read out /home/hacker/not-the-flag. Use the symlink, and fool it into giving you the flag!



### Solve
**Flag:** `pwn.college{E7BD_gqjx3ERBoc3-QzpEZMX0Ck.dlTM1UDLxATN1czW}`

``` 
bash
hacker@commands~linking-files:~$ ln -s /flag /home/hacker/not-the-flag
ln: failed to create symbolic link '/home/hacker/not-the-flag': File exists
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
pwn.college{E7BD_gqjx3ERBoc3-QzpEZMX0Ck.dlTM1UDLxATN1czW}
hacker@commands~linking-files:~$ file /home/hacker/not-the-flag
/home/hacker/not-the-flag: symbolic link to /flag
hacker@commands~linking-files:~$ 
 

```
Had to create symlink using `ln -s` then runt the challenge whichi by default read the symlink and then it gave the flag.


## New Learnings
cat- used to read out files and also concatenates,grep,diff,ls,touch,rm,mv, find / -name,ln -s,file command tells type of file

## References 
Linux Luminarium
