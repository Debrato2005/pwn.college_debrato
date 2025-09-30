# Shell Variables
## 1
The Linux command line interface is actually a sophisticated programming language with which you can write actual programs! Because the command line interface is colloquially referred to as a "shell", programs written in this language are referred to as "shell scripts". When you're using the command line, you are basically writing a shell script line by line!

Like most programming languages, the shell supports variables. This module will get you familiar with setting, printing, and using these variables!

## 1 Printing Variables
Let's start with printing variables out. The /challenge/run program will not, and cannot, give you the flag, but that's okay, because the flag has been put into the variable called "FLAG"! Just have your shell print it out!

You can accomplish this using a number of ways, but we'll start with echo. This command just prints stuff. For example:

hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
You can also print out variables with echo, by prepending the variable name with a $. For example, there is a variable, PWD, that always holds the current working directory of the current shell. You print it out as so:

hacker@dojo:~$ echo $PWD
/home/hacker
Now it's your turn. Have your shell print out the FLAG variable and solve this challenge!


### Solve
**Flag:** `pwn.college{MWpG75zTgfP-CNssJXSivt9K3Te.ddTN1QDLxATN1czW}`

``` bash
hacker@variables~printing-variables:~$ /challenge/run
You cannot solve this challenge using /challenge/run.
However, the flag is already in the FLAG variable in your shell.
Print it out!
hacker@variables~printing-variables:~$ cat FLAG
cat: FLAG: No such file or directory
hacker@variables~printing-variables:~$ echo FLAG
FLAG
hacker@variables~printing-variables:~$ cat $FLAG
cat: pwn.college{MWpG75zTgfP-CNssJXSivt9K3Te.ddTN1QDLxATN1czW}: No such file or directory
hacker@variables~printing-variables:~$ 

```
You can also print out variables with echo, by prepending the variable name with a $.

## 2 Setting Variables
Naturally, as well as reading values stored in variables, you can write values to variables. This is done, as with many other languages, using =. To set variable VAR to value 1337, you would use:

hacker@dojo:~$ VAR=1337
Note that there are no spaces around the =! If you put spaces (e.g., VAR = 1337), the shell won't recognize a variable assignment and will, instead, try to run the VAR command (which does not exist).

Also note that this uses VAR and not $VAR: the $ is only prepended to access variables. In shell terms, this prepending of $ triggers what is called variable expansion, and is, surprisingly, the source of many potential vulnerabilities (if you're interested in that, check out the Art of the Shell dojo when you get comfortable with the command line!).

After setting variables, you can access them using the techniques you've learned previously, such as:

hacker@dojo:~$ echo $VAR
1337
To solve this level, you must set the PWN variable to the value COLLEGE. Be careful: both the names and values of variables are case-sensitive! PWN is not the same as pwn and COLLEGE is not the same as College.

### Solve
**Flag:** `pwn.college{4_8XTqkz48SMTTNuRnPEQHwogfV.dlTN1QDLxATN1czW}`

``` bash
Connected!
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{4_8XTqkz48SMTTNuRnPEQHwogfV.dlTN1QDLxATN1czW}
hacker@variables~setting-variables:~$ 
```
It was just required to set a variable.

## 3 Multi-word variables 
In this level, you will learn about quoting. Spaces have special significance in the shell, and there are places where you can't use them spuriously. Recall our variable setting:

hacker@dojo:~$ VAR=1337
That sets the VAR variable to 1337, but what if you wanted to set it to 1337 SAUCE? You might try the following:

hacker@dojo:~$ VAR=1337 SAUCE
This looks reasonable, but it does not work, for similar reasons to needing to have no spaces around the =. When the shell sees a space, it ends the variable assignment and interprets the next word (SAUCE in this case) as a command. To set VAR to 1337 SAUCE, you need to quote it:

hacker@dojo:~$ VAR="1337 SAUCE"
Here, the shell reads 1337 SAUCE as a single token, and happily sets that value to VAR. In this level, you'll need to set the variable PWN to COLLEGE YEAH. Good luck!

### Solve
**Flag:** ``

``` bash
Connected!
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{UsYU5ZJEn7EQ5qcSZikn-NmOZfD.dBjN1QDLxATN1czW}
hacker@variables~multi-word-variables:~$ 

```
Here the shell needs to read `COLLEGE YEAH`s as a single token.

## 4 Exporting Variables
By default, variables that you set in a shell session are local to that shell process. That is, other commands you run won't inherit them. You can experiment with this by simply invoking another shell process in your own shell, like so:

hacker@dojo:~$ VAR=1337
hacker@dojo:~$ echo "VAR is: $VAR"
VAR is: 1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 
In the output above, the $ prompt is the prompt of sh, a minimal shell implementation that is invoked as a child of the main shell process. And it does not receive the VAR variable!

This makes sense, of course. Your shell variables might have sensitive or weird data, and you don't want it leaking to other programs you run unless it explicitly should. How do you mark that it should? You export your variables. When you export your variables, they are passed into the environment variables of child processes. You'll encounter the concept of environment variables in other challenges, but you'll observe their effects here. Here is an example:

hacker@dojo:~$ VAR=1337
hacker@dojo:~$ export VAR
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
Here, the child shell received the value of VAR and was able to print it out! You can also combine those first two lines.

hacker@dojo:~$ export VAR=1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
In this challenge, you must invoke /challenge/run with the PWN variable exported and set to the value COLLEGE, and the COLLEGE variable set to the value PWN but not exported (e.g., not inherited by /challenge/run). Good luck!

### Solve
**Flag:** `pwn.college{Ik04uxdnspCM6Cfcak2C9Nu0b2g.dJjN1QDLxATN1czW}`

``` bash
Connected!
hacker@variables~exporting-variables:~$ /challenge/run
Incorrect...
You have not exported the PWN variable. This challenge requires you to export 
the PWN variable.
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ PWN=COLLEGE
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run
Incorrect...
You have not exported the PWN variable. This challenge requires you to export 
the PWN variable.
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ export PW
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ export PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great 
job! Here is your flag:
pwn.college{Ik04uxdnspCM6Cfcak2C9Nu0b2g.dJjN1QDLxATN1czW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ 

```
We need to export variable and then run the program.

## 5 Printing Exported variables
There are multiple ways to access variables in bash. echo was just one of them, and we'll now learn at least one more in this challenge.

Try the env command: it'll print out every exported variable set in your shell, and you can look through that output to find the FLAG variable!

### Solve
**Flag:** `pwn.college{Y7tSBteE5rELxWiq0oMpKzs6Phi.dhTN1QDLxATN1czW}`

``` bash
Connected!
hacker@variables~printing-exported-variables:~$ env
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
MANPATH=/run/dojo/share/man:
DOJO_AUTH_TOKEN=f79c7c2bff601d2bf583114d84718d12db03576a877956b202a01c0c19aaa441
HOME=/home/hacker
LANG=C.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=00:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.7z=01;31:*.ace=01;31:*.alz=01;31:*.apk=01;31:*.arc=01;31:*.arj=01;31:*.bz=01;31:*.bz2=01;31:*.cab=01;31:*.cpio=01;31:*.crate=01;31:*.deb=01;31:*.drpm=01;31:*.dwm=01;31:*.dz=01;31:*.ear=01;31:*.egg=01;31:*.esd=01;31:*.gz=01;31:*.jar=01;31:*.lha=01;31:*.lrz=01;31:*.lz=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.lzo=01;31:*.pyz=01;31:*.rar=01;31:*.rpm=01;31:*.rz=01;31:*.sar=01;31:*.swm=01;31:*.t7z=01;31:*.tar=01;31:*.taz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tgz=01;31:*.tlz=01;31:*.txz=01;31:*.tz=01;31:*.tzo=01;31:*.tzst=01;31:*.udeb=01;31:*.war=01;31:*.whl=01;31:*.wim=01;31:*.xz=01;31:*.z=01;31:*.zip=01;31:*.zoo=01;31:*.zst=01;31:*.avif=01;35:*.jpg=01;35:*.jpeg=01;35:*.jxl=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:*~=00;90:*#=00;90:*.bak=00;90:*.crdownload=00;90:*.dpkg-dist=00;90:*.dpkg-new=00;90:*.dpkg-old=00;90:*.dpkg-tmp=00;90:*.old=00;90:*.orig=00;90:*.part=00;90:*.rej=00;90:*.rpmnew=00;90:*.rpmorig=00;90:*.rpmsave=00;90:*.swp=00;90:*.tmp=00;90:*.ucf-dist=00;90:*.ucf-new=00;90:*.ucf-old=00;90:
FLAG=pwn.college{Y7tSBteE5rELxWiq0oMpKzs6Phi.dhTN1QDLxATN1czW}
LESSCLOSE=/usr/bin/lesspipe %s %s
TERMINFO=/run/dojo/share/terminfo
TERM=xterm-256color
LESSOPEN=| /usr/bin/lesspipe %s
SHLVL=2
LC_CTYPE=C.UTF-8
SSL_CERT_FILE=/run/dojo/etc/ssl/certs/ca-bundle.crt
PATH=/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
DEBIAN_FRONTEND=noninteractive
_=/run/dojo/bin/env

```
`env` prints out every exported variable set in your shell.

## 6 Storing command output
In the course of working with the shell, you will often want to store the output of some command into a variable. Luckily, the shell makes this quite easy using something called Command Substitution! Observe:

hacker@dojo:~$ FLAG=$(cat /flag)
hacker@dojo:~$ echo "$FLAG"
pwn.college{blahblahblah}
hacker@dojo:~$
Neat! Now, you practice. Read the output of the /challenge/run command directly into a variable called PWN, and it will contain the flag!

Trivia: You can also use backticks instead of $(): FLAG=`cat /flag` instead of FLAG=$(cat /flag) in the example above. This is an older format, and has some disadvantages (for example, imagine if you wanted to nest command substitutions. How would you do $(cat $(find / -name flag)) with backticks? The official stance of pwn.college is that you should use $(blah) instead of `blah`.


### Solve
**Flag:** ``

``` bash
Connected!
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run command)
Congratulations! You have read the flag into the PWN variable. Now print it out 
and submit it!
hacker@variables~storing-command-output:~$ echo $PWN
pwn.college{siS8Ex5om-qrrd_wN3LreaXyiR_.dVzN0UDLxATN1czW}
hacker@variables~storing-command-output:~$ 
```
Command Substitution is FLAG=$(cat /flag) can also use backticks instead of $(): FLAG=`cat /flag` instead of FLAG=$(cat /flag). Therefore, Read the output of the /challenge/run command directly into a variable called PWN and then read the variable.


## 7 Reading input
We'll start with reading input from the user (you). That's done using the aptly named read builtin, which reads input into a variable!

Here is an example using the -p argument, which lets you specify a prompt (otherwise, it would be hard for you, reading this now, to separate input from output in the example below):

hacker@dojo:~$ read -p "INPUT: " MY_VARIABLE
INPUT: Hello!
hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
You entered: Hello!
Keep in mind, read reads data from your standard input! The first Hello!, above, was inputted rather than outputted. Let's try to be more explicit with that. Here, we annotated the beginning of each line with whether the line represents INPUT from the user or OUTPUT to the user:

 INPUT: hacker@dojo:~$ echo $MY_VARIABLE
OUTPUT:
 INPUT: hacker@dojo:~$ read MY_VARIABLE
 INPUT: Hello!
 INPUT: hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
OUTPUT: You entered: Hello!
In this challenge, your job is to use read to set the PWN variable to the value COLLEGE. Good luck!

### Solve
**Flag:** `pwn.college{U2xMWFoF-lvODo_EQXaMH25OeDp.dhzN1QDLxATN1czW}`

``` bash
Connected!
hacker@variables~reading-input:~$ read -p "Enter value for PWN: " PWN
Enter value for PWN: COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{U2xMWFoF-lvODo_EQXaMH25OeDp.dhzN1QDLxATN1czW}
hacker@variables~reading-input:~$ 

```
Read to set the PWN variable to the value COLLEGE.

## 8 Reading Files
Often, when shell users want to read a file into an environment variable, they do something like:

hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ VAR=$(cat some_file)
hacker@dojo:~$ echo $VAR
test
This works, but it represents what grouchy hackers call a "Useless Use of Cat". That is, running a whole other program just to read the file is a waste. It turns out that you can just use the powers of the shell!

Previously, you read user input into a variable. You've also previously redirected files into command input! Put them together, and you can read files with the shell.

hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ read VAR < some_file
hacker@dojo:~$ echo $VAR
test
What happened there? The example redirects some_file into the standard input of read, and so when read reads into VAR, it reads from the file! Now, use that to read /challenge/read_me into the PWN environment variable, and we'll give you the flag! The /challenge/read_me will keep changing, so you'll need to read it right into the PWN variable with one command!

### Solve
**Flag:** `pwn.college{k8y0VXpiVGMiC65sApPZdBwOI6m.dBjM4QDLxATN1czW}`

``` bash
Connected!
hacker@variables~reading-files:~$ read PWN < /challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{k8y0VXpiVGMiC65sApPZdBwOI6m.dBjM4QDLxATN1czW}
hacker@variables~reading-files:~$ 

```
When shell users want to read a file into an environment variable, they use cat but its useless running a whole other program just to read the file is a waste, its better to use read.

## New Learnings
print out variables with echo, by prepending the variable name with a $, when assigning there are no spaces around the =,$ is only prepended to access variables,VAR="1337 SAUCE",Here, the shell reads 1337 SAUCE as a single token,Think of exporting as “sending this variable along when launching programs.” Local variables are like “private notes” for your shell — invisible to any commands you run, env command, can do env | grep flag, Command Substitution is FLAG=$(cat /flag) can also use backticks instead of $(): FLAG=`cat /flag` instead of FLAG=$(cat /flag), read -p the -p is used to show a prompt to user, read is beter and more efficient to use compared to cat for variables.

## References 
Linux Luminarium 


