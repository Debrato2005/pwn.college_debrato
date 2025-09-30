# Data Manipulation
You've learned to pipe data, specify input, and so on. Let's start putting things together! In this module, you'll learn a number of commands for manipulating data that will help you achieve great results on the shell.


## 1 Translating characters
One of the purposes of piping data is to modify it. Many Linux commands will help you modify data in really cool ways. One of these is tr, which translates characters it receives over standard input and prints them to standard output.

In its most basic usage, tr translates the character provided in its first argument to the character provided in its second argument:

hacker@dojo:~$ echo OWN | tr O P
PWN
hacker@dojo:~$
It can also handle multiple characters, with the characters in different positions of the first argument replaced with associated characters in the second argument.

hacker@dojo:~$ echo PWM.COLLAGE | tr MA NE
PWN.COLLEGE
hacker@dojo:~$
Now, you try it! In this level, /challenge/run will print the flag but will swap the casing of all characters (e.g., A will become a and vice-versa). Can you undo it with tr and get the flag?

### Solve
**Flag:** `pwn.college{YiGgnf6deaJ9dP5aRhVNTUWzEQl.QXzETM3EDLxATN1czW}`

``` bash
Connected!
hacker@data~translating-characters:~$ /challenge/run | tr 'a-zA-Z' 'A-Za-z'
yOUR CASE-SWAPPED FLAG:
pwn.college{YiGgnf6deaJ9dP5aRhVNTUWzEQl.QXzETM3EDLxATN1czW}

hacker@data~translating-characters:~$ 

```
tr translates the character provided in its first argument to the character provided in its second argument

## 2 Deleting Characters
tr can also translate characters to nothing (i.e., delete them). This is done via a -d flag and an argument of what characters to delete:

hacker@dojo:~$ echo PAWN | tr -d A
PWN
hacker@dojo:~$
Pretty simple! Now you give it a try. I'll intersperse some decoy characters (specifically: ^ and %) among the flag characters. Use tr -d to remove them!

### Solve
**Flag:** `pwn.college{QdZKnrXbwvh7ali2GNa_51qqo9h.QX0ETM3EDLxATN1czW}`

``` bash
(base) debrato@debratolaptop:~/Desktop/Coding/pwn.college_debrato$ ssh -i ./key hacker@dojo.pwn.college
 Connected!
hacker@data~deleting-characters:~$ /challenge/run | tr -d '^%'           
Your character-stuffed flag:
pwn.college{QdZKnrXbwvh7ali2GNa_51qqo9h.QX0ETM3EDLxATN1czW}
hacker@data~deleting-characters:~$ 

```
tr can also translate characters to nothing (i.e., delete them). This is done via a -d flag and an argument of what characters to delete

## 3 Deleting newlines
A common class of characters to remove is a line separator. This happens when you have a stream of data that you want to turn into a single line for further processing. You can specify newlines almost like any other character, by escaping them:

hacker@dojo:~$ echo "hello_world!" | tr _ "\n"
hello
world!
hacker@dojo:~$
Here, the backslash (\) signifies that the character that follows it is a standin for a character that's hard to input into the shell normally. The newline, of course, is hard to input because when you typically hit Enter, you'll run the command itself. \n is a standin for this newline, and it must be in quotes to prevent the shell interpreter itself from trying to interpret it and pass it to tr instead.

Now, let's combine this with deletion. In this challenge, we'll inject a bunch of newlines into the flag. Delete them with tr's -d flag and the escaped newline specification!

Fun fact! Want to actually replace a backslash (\) character? Because \ is the escape character, you gotta escape it! \\ will be treated as a backslash by tr. This isn't relevant to this challenge, but is a fun fact nonetheless!

### Solve
**Flag:** `pwn.college{Yj7GKMBuT6J6jxrEcKN_8HtdvGw.QX1ETM3EDLxATN1czW}`

``` bash
Connected!
hacker@data~deleting-newlines:~$ /challenge/run | tr -d '\n'
Your line-split flag: pwn.college{Yj7GKMBuT6J6jxrEcKN_8HtdvGw.QX1ETM3EDLxATN1czW}
hacker@data~deleting-newlines:~$ 

```
A common class of characters to remove is a line separator. This happens when you have a stream of data that you want to turn into a single line for further processing. You can specify newlines almost like any other character, by escaping them

## 4 Extracting the first lines with head
In your Linux journey, you'll experience situations where you need to grab just the early output of very verbose programs. For this, you'll reach for head! The head command is used to display the first few lines of its input:

hacker@dojo:~$ cat /something/very/long | head
this
is
just
the
first
ten
lines
of
the
file
hacker@dojo:~$
By default, it shows the first 10 lines, but you can control this with the -n option:

hacker@dojo:~$ cat /something/very/long | head -n 2
this
is
hacker@dojo:~$
This challenge's /challenge/pwn outputs a bunch of data, and you'll need to pipe it through head to grab just the first 7 lines and then pipe them onwards to /challenge/college, which will give you the flag if you do this right! Your solution will be a long composite command with two pipes connecting three commands. Good luck!

### Solve
**Flag:** `pwn.college{ovgyGClbm7aGzWQWnywP-CYTRcQ.QX2ETM3EDLxATN1czW}`

``` bash
Connected!
hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n 7 | /challenge/college
Congratulations, you piped the right codes!
pwn.college{ovgyGClbm7aGzWQWnywP-CYTRcQ.QX2ETM3EDLxATN1czW}
hacker@data~extracting-the-first-lines-with-head:~$ 

```
The head command is used to display the first few lines of its input

## 5 Extracting specific sections of text
Sometimes, you want to grab specific columns of data, such as the first column, the third column, or the 42nd column. For this, there's the cut command.

For example, imagine that you have the following data file:

hacker@dojo:~$ cat scores.txt
hacker 78 99 67
root 92 43 89
hacker@dojo:~$
You could use cut to extract specific columns:

hacker@dojo:~$ cut -d " " -f 1 scores.txt
hacker
root
hacker@dojo:~$ cut -d " " -f 2 scores.txt
78
92
hacker@dojo:~$ cut -d " " -f 3 scores.txt
99
43
hacker@dojo:~$
The -d argument specifies the column delimiter (how columns are separated). In this case, it's a space character. Of course, it has to be in quotes here so that the shell knows that the space is an argument rather than a space separating other arguments! The -f argument specifies the field number (which column to extract).

In this challenge, the /challenge/run program will give you a bunch of lines with random numbers and single characters (characters of the flag) as columns. Use cut to extract the flag characters, then pipe them to tr -d "\n" (like the previous level!) to join them together into a single line. Your solution will look something like /challenge/run | cut ??? | tr ???, with the ??? filled out.

### Solve
**Flag:** `pwn.college{ARz70x-nKh3K5o-Wkjy1RefOGsx.QX3ETM3EDLxATN1czW}`

``` bash
Connected!
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run
11018 p
16360 w
12499 n
9755 .
15151 c
11712 o
22595 l
14757 l
350 e
30116 g
32169 e
1790 {
12154 A
32217 R
23933 z
23973 7
8124 0
8935 x
710 -
14665 n
6425 K
29774 h
13311 3
16155 K
7380 5
25110 o
9889 -
19593 W
29555 k
16766 j
26865 y
16566 1
10929 R
21092 e
20216 f
10864 O
16776 G
29843 s
2440 x
23852 .
30240 Q
16934 X
22417 3
1536 E
5010 T
3973 M
27137 3
31808 E
31427 D
6274 L
15688 x
26994 A
31893 T
13381 N
15702 1
25826 c
21735 z
11074 W
1670 }
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d ' ' -f2 | tr -d '\n' 
pwn.college{ARz70x-nKh3K5o-Wkjy1RefOGsx.QX3ETM3EDLxATN1czW}hacker@data~extracting-specific-sections-of-text:~$ 
```
To grab specific columns of data, such as the first column, the third column, or the 42nd column. For this, there's the cut command.

## 6 Sorting data
Files (or output lines of commands) aren't always in the order you need them! The sort command helps you organize data. It reads lines from input (or files) and outputs them in sorted order:

hacker@dojo:~$ cat names.txt
  hack
  the
  planet
  with
  pwn
  college
hacker@dojo:~$ sort names.txt
  college
  hack
  planet
  pwn
  the
  with
hacker@dojo:~$
By default, sort orders lines alphabetically. Arguments can change this:

-r: reverse order (Z to A)
-n: numeric sort (for numbers)
-u: unique lines only (remove duplicates)
-R: random order!
In this challenge, there's a file at /challenge/flags.txt containing 100 fake flags, with the real flag mixed among them. When sorted alphabetically, the real flag will be at the end (we made sure of this when generating fake flags). Go get it!

### Solve
**Flag:** ``

``` bash
Connected!
hacker@data~sorting-data:~$ sort -r /challenge/flags.txt
pwn.college{wIVrjnmE64k1k1bZ80R4J4Wgifg.QXwQzM4EDLxATN1czW}
pwn.college{wIVrjnmE64k1k1bZ80R4J4Wgifg.QXwQzM4EDLxATN1czW}
pwn.college{wIVrjnmE64k1k1bZ80R4J3Wgifg.QXwQzM4EDKxATN1czW}
pwn.college{wIVrjnmE64k0k1bZ80R4J4Wgifg.QXwQzM4EDLxATN1czW}
pwn.college{wIVrjnmE64k0k1bZ80R4I4Vgifg.QXwQzM4EDLxATN1bzW}
pwn.college{wIVrjnmE64k0k1bZ80R3J4Wgifg.PXvPzM4EDKxATN1bzW}
pwn.college{wIVrjnmE64k0k1bZ70R3J4Wgifg.QXwQzM4EDLxATN1bzW}
pwn.college{wIVrjnmE54k1k1bZ80R4J4Wgifg.QXwQzM4ECLxATN1czW}
pwn.college{wIVrjnmE54k1k1bZ80R4J4Wgifg.PXwQzM4EDLxATN1czW}
pwn.college{wIVrjnmE54k1k1bZ80R4J4Vgifg.QXwQyM4EDLxATN1bzW}
pwn.college{wIVrjnmD64k1k1bZ80R4J4Wgifg.QXwQzM4EDLxATN1czW}
pwn.college{wIVrjnlE64k1k1bZ80R4J4Wgifg.QXwPzM4EDLxATN1czW}
pwn.college{wIVrjmmE63k1j0bZ80R4J4Wgiff.PXwPzM4EDLwATN1czW}
pwn.college{wIVqjnmE64k1k1bZ80R4J4Wgifg.QXwQzM4EDLxATM1czW}
pwn.college{wIVqjnmE64k1k0bZ80Q4J4Wgifg.QWwQzM4EDLwATN1czV}
pwn.college{wIUrjnmD64k0k1bZ70R4J4Wgifg.QXwQzM3EDLxATN1czW}
pwn.college{wHVrjnmE64k1k0bZ80R4J4Wgifg.QXwQzM4EDLxATN1czW}
pwn.college{wHVqjnmE64j1k1bZ80R4J4Wgifg.QXwQzM4EDLxATN1czW}
pwn.college{vIVqjnmE64k1k1bZ80R4J4Wghfg.QWwQzL4EDLxATN1czW}
pwn.college{vIVqinmE63k1k0aZ80R4J4Vfifg.QXwPzM3ECLwATN0cyV}
pwn.collegd{wIVrjnmE64k1k1bZ80R4J4Wgifg.QXwQzM4EDLxATN1czW}
pwn.collegd{wIVrjmmE64k1k1bY80Q4J4Wgieg.QXwQzM4EDLxATN1czW}
pwn.collegd{wIVrinmD64k1k0bY80R4J4Wgifg.QXwQzM4EDKxASN0bzV}
pwn.collegd{wIUrjnmE63k1k1bZ80R4J4Wghfg.QWwQzM4ECLxATN1bzW}
pwn.collegd{wIUqjnmE64k1j1bZ80R4J4Vgheg.QXwQzM3ECLxATN1czV}
pwn.collegd{vHUrjmmE54j1k1aZ70R3J4Vgiff.QXwQyM3EDLxASM1czW}
pwn.collefe{wIVrjnmE64k1j1bY70R4J4Wgieg.QWvQzL3ECLxATN1czW}
pwn.colldge{wIVqinlD54j0j0bZ80Q3I4Vfifg.PXwPzM3DDLxASM1czW}
pwn.colldge{vIVqinmE64k1j1aZ80R3J4Wgifg.QXwQzM4EDLxATN1cyW}
pwn.colkege{wHVrjnmE64k1k1bZ70R4J4Wgifg.QXwQzM4ECLxATM1czW}
pwn.colkege{vIVrjnmE64k1k1bZ80R4J4Wghfg.QXwQzM4EDLwATN1cyV}
pwn.colkege{vIVrjnmD64k0k1bZ80R4J3Wgifg.QWwQzM4ECLxATM0cyW}
pwn.colkdge{wHVrjnmE64j1k1bY80Q4J4Wghfg.QWwQzM3DDLxATN0bzW}
pwn.colkdge{wHVqjmlE63k0k1bZ80R4J4Wgiff.PXvQzL3DDLxATN1czV}
pwn.coklefd{wHVqinlD64j0j1bY70Q4I3Wgheg.QXwQyM4EDLxATN1bzW}
pwn.cokkefe{vIVqinmE64k1k1bZ80R3J4Wgifg.PXwQzM4DDLwATN1czV}
pwn.cnllefe{wIVrinmE64k1k0bZ80R3J4Wgifg.QXwPzM4EDLwATN1czW}
pwn.cnllefd{wIVrjnmE64j1j1bZ70Q4J4Wfifg.QXvQyM3DCLxATN1bzW}
pwn.cnllefd{wIVqjmmE64k0k1bY80R4J4Wgifg.QXwQzM4EDKxATN1czW}
pwn.cnlldge{wHVrjnmE63k0k1bZ70R4J4Wgifg.QXwQzM4DDLxATN1czW}
pwn.cnlkege{wIVrinmE63k1k1bZ80R4J4Wgheg.QXwPzM4DDLxATN1cyV}
pwn.cnklege{wIVrjnmE64k1k1bZ80R4J4Vgifg.PXwQzM4EDLxATM1czW}
pwn.cnklegd{wHUqjnmD64k1j1bZ80R3J3Wgiff.QWvQzL3EDLwASN1czW}
pwn.bollege{wIVrjnlE64k1k1bZ80R4J4Wgifg.QXwQzM4EDLxATN0czW}
pwn.bollege{wIVrjnlE63k1j1aZ80R4J4Wghfg.QWwQzM4EDKxATN1czW}
pwn.bollege{vIUrjnmE64k0k0bZ80R4J4Wgieg.PXwQzM4EDLxATN1cyW}
pwn.bolkege{wIVqjnlE64k1k0bY80Q4J3Vgifg.QWwQyM4EDLxATM1czW}
pwn.bolkdge{wIVrinlE64k1k1bZ70R4J3Vgifg.PXwQzL4ECKxATN1bzW}
pwn.bolkdfd{wIVrjnmE64j1j1bZ70Q3I4Wgifg.QXwPzM4ECKwASN1cyW}
pwn.bnllege{wIVrjnlE64k1k1bY80R3I3Wgheg.PXwQzL4ECLwATM1czW}
pwn.bnllege{wIUrjnlD64k1k1bZ80R4I3Wfiff.QWwQzL4DDLwATN1czW}
pwn.bnllefd{wHVrimmD54k1k1bZ80R4I4Wghfg.PWvQyM3EDLxATN1czV}
pwn.bnllefd{vIVrjnmE64k0j1bZ70R4J4Wgifg.QXwQzM3DCLxATN1cyW}
pwn.bnkkege{wIVqinlD64k0k0bZ80R3I3Vgieg.QXvPyL4ECLxATN1czW}
pwm.colkege{wIVrjnmE64k1k1bZ80R3J4Wgifg.QXwQzM4DDLxATN0czW}
pwm.coklefe{vIVrinmD54k1k1aZ80Q4J4Vgiff.PWwPzL4DDLxASN1byW}
pwm.cokkdfe{vIVrimmE53j0j1bY80R4I4Wghff.QWwQzM4EDLwATN0czW}
pwm.cnllege{wIVrjnmE63k1k1bZ80R4J4Wgifg.QXwQzM3DDLxATM1bzV}
pwm.bolldge{wIVrjnmD64j1k1aZ80Q4I4Wgifg.QXwQzL3DDLwATN0czW}
pwm.boklege{wIUrjnmE64k0k1bZ80R4J3Wfifg.QXwQyL3DDLxASN1czW}
pvn.college{wIVrinmE64k1k1aZ70R4J4Wgifg.QXwQzM3EDLxATM1czW}
pvn.college{wHVrjmmE64k1j0bZ80R3J4Wgieg.QXwQzM4ECLxATN0czW}
pvn.collegd{wIVqjnlE54k0k0bZ80R4J4Vgifg.PXwQzL4EDLxASN1byW}
pvn.colldge{wIUqimmE64k0j1bZ80R4I4Wgheg.QXwQyM4EDKxATN1cyW}
pvn.colkege{wIVrimmE64k1k0bZ80R4J4Wfifg.QXwQyL3ECLxATN1bzW}
pvn.colkege{wIUqinmE63k0k0aZ80R4J4Wgieg.PXwQyM4EDLxASN0cyW}
pvn.colkdfd{wIVrjmlE64k0k1bZ80Q4J4Wgifg.PXwPzM4EDLxASN1czV}
pvn.cnkkefe{wHVrjnmE54k0k1aZ80R4J3Wgifg.QXwPzM4EDLxASM1cyW}
pvn.bolldfe{wIUrjnlD64j1j0bZ70R3I3Wfhfg.QXwQzM3EDKwASN1czV}
pvn.bnlkdfe{wIVrjmmE64k1k1bY80R4J4Wgifg.QXwQzM4EDLxATN1bzW}
pvm.colldge{wHUqinmD53j0k0bZ80R4I3Vgieg.PWwQyM4EDLxASM1czW}
pvm.colldfe{wHVrjnlE64j0k1bY70Q4I3Wgiff.QWvQzM4EDKxASM1bzV}
pvm.cokldfd{wHVrjnmE63k1k1bY80R3I4Wghfg.PXwQzM4DCLwATM0czV}
pvm.cokkdfe{vIUrjnmE64k0k1bZ80R4J3Vgiff.QXwQzL4EDKwASN1cyV}
pvm.bolldge{wIVrjnmE64k0k0bZ80R4J4Vgifg.QXwQzM4ECLwATN1czW}
own.college{wIVrjnmE64k1k1bZ80R4J4Wgifg.QXwQzM4EDLxATN1czW}
own.college{wIVrimmE64j1k1aY80R3I4Vfifg.QXvQyM4ECLxATN1bzW}
own.college{wHVrjnmE64k1k1bY80R4J4Wfifg.QXvQzM4DDLxATN1czW}
own.college{wHUrjnmE64k0k1bZ80R4J4Wgifg.QXwQzM4ECLwATN1cyW}
own.colldge{wIVrjnmE54k1k1bZ80R4J4Wgiff.QXwQzM4DDLxATN1czW}
own.colkefe{vIUrjnmE54k1k1bZ80R4J4Wgifg.QXwQzL4ECLxATN1czW}
own.coklegd{wHUrjnmD54j1k1aZ80R4J4Wgieg.QXwPyM4DDLwASN0cyW}
own.cokldge{wIUrjnmE53j1k0bY80Q3J4Wgifg.PWwQzM3EDLwATN1cyW}
own.cnllege{wIUrjnlD54j0k0aZ70Q4I3Wgief.QXvQzL4ECLxATN1cyV}
own.cnllege{wHVrinlD64k1k1aZ80R4J4Wgiff.QXvQzM4EDKxATN0czW}
own.cnllegd{wIUrinmE54j1k1bY80R4J3Vgief.QXwQyM4ECKxASN1czW}
own.cnlldge{wIVrjmmE64j1k0aY70R4J4Wghfg.PXwPyM4EDLxATN0bzW}
own.cnlldfd{wIVrimmE64k1k1bY70R3J4Wgifg.QXwPzM4DDLwATN1czW}
own.cnlkege{vIVrinmE53j1k0aZ70R4J3Wghfg.QWwPzL3EDLwASN0bzW}
own.bolkdge{wIUqinmE63k0k1bZ80R4J3Wghff.PXwPzL4EDKxATN1bzW}
own.bnllege{wIVrjnmE64k1k1bY80R4J4Vghfg.QWwQzM4EDKxATN1czW}
own.bnlldge{vIVrjmmE64k1k1bZ80Q4J4Wghfg.QWwQzM4ECLwATN1czW}
own.bnkkegd{wHUrjnmE64k1j1bZ70R4I4Wfheg.QXvQzM4EDLxASM1czW}
owm.cnkkege{wIVqinmE54k1k1bZ80Q4J4Wgiff.PXwQyL4EDLxATN1czV}
owm.bnllege{vIVqjnmD63k1k1aZ80R4J4Wfifg.QXvQzL4EDLxASM1byV}
ovn.collegd{wHVrjnmE64k1k1bY80R3J4Wfieg.PXvQyM4ECLwATM0czW}
ovn.collegd{vHUrjnmE64j1k0aZ80Q4J4Wfiff.PXwQzM4DCLxATN1czV}
ovn.colkegd{wIUqinmD64j0k1bZ70R4I4Wgifg.QXvQzM4ECLxATN1czW}
ovn.cnlkefd{wIUqinmD54j1k1bZ70R4J3Vgief.PXwQyM4EDKxASN1czW}
ovn.bollege{wIVqjnmE64k0k1bZ80R3J4Wgifg.QXvPzM4DDKwATN1czW}
ovn.bollegd{wIUrjnmE64k0k0bZ80R4J4Vfieg.QXwQzM3EDLwATN0czV}
hacker@data~sorting-data:~$ 
```
The sort command helps you organize data. It reads lines from input (or files) and outputs them in sorted order

## New Learnings
tr translates the character provided in its first argument to the character provided in its second arguments, tr  can also translate characters to nothing (i.e., delete them). This is done via a -d flag and an argument of what characters to delete , tr _ "\n" to delete line, head -n 3 The head command is used to display the first few lines of its input, to grab specific columns of data, such as the first column, the third column, or the 42nd column. For this, there's the cut command -d argument specifies the column delimiter (how columns are separated). In this case, it's a space character. Of course, it has to be in quotes here so that the shell knows that the space is an argument rather than a space separating other arguments! The -f argument specifies the field number (which column to extract), The sort command helps you organize data. It reads lines from input (or files) and outputs them in sorted order


## References 
Linux Luminarium 


