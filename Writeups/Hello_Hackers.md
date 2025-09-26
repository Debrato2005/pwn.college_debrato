# Hello Hackers

## Intro to commands
In this challenge, you will invoke your first command! When you type a command and hit enter, the command will be invoked, as so:

hacker@dojo:~$ whoami
hacker
hacker@dojo:~$
Here, the user executed the whoami command, which simply prints the username (hacker) to the terminal. When the command terminates, the shell once again displays the prompt, ready for the next command.

In this level, invoke the hello command to get the flag! Keep in mind: commands in Linux are case sensitive: hello is different from HELLO.

### Solve
**Flag:** `pwn.college{MZ2Jotz2yaYCFGGPqfkQH4BddO4.ddjNyUDLxATN1czW}`

It was said to use whoami command and then invoke hello command for the flag.

``` bash
(base) debrato@debratolaptop:~/Desktop/Coding/pwn.college_debrato$ ssh -i ./key hacker@dojo.pwn.college
Connected!
hacker@hello~intro-to-commands:~$ whoami
hacker
hacker@hello~intro-to-commands:~$ hello
Success! Here is your flag:
pwn.college{MZ2Jotz2yaYCFGGPqfkQH4BddO4.ddjNyUDLxATN1czW}
hacker@hello~intro-to-commands:~$ 
```

## Intro to arguments
Let's try something more complicated: a command with arguments, which is what we call additional data passed to the command. When you type a line of text and hit enter, the shell actually parses your input into a command and its arguments. The first word is the command, and the subsequent words are arguments. Observe:

hacker@dojo:~$ echo Hello
Hello
hacker@dojo:~$
In this case, the command was echo, and the argument was Hello. echo is a simple command that "echoes" all of its arguments back out onto the terminal, like you see in the session above.

Let's look at echo with multiple arguments:

hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
hacker@dojo:~$
In this case, the command was echo, and Hello and Hackers! were the two arguments to echo. Simple!

In this challenge, to get the flag, you must run the hello command (NOT the echo command) with a single argument of hackers. Try it now!
### Solve
**Flag:** `pwn.college{45qZFAXk4FyiyxCjJySsuBtj40U.dhjNyUDLxATN1czW}`

It was said to use implement argument with command.

``` bash
Connected!
hacker@hello~intro-to-arguments:~$ echo hacker
hacker
hacker@hello~intro-to-arguments:~$ hello hacker
Please run this command with the argument 'hackers' (rather than 'hacker').
hacker@hello~intro-to-arguments:~$ hello hackers
Success! Here is your flag:
pwn.college{45qZFAXk4FyiyxCjJySsuBtj40U.dhjNyUDLxATN1czW}
hacker@hello~intro-to-arguments:~$
```

## Command History
You're going to type a lot of commands, and typing everything from scratch can be annoying. Luckily, the shell saves a history of every command you invoke.

You can scroll through those saved commands with the up/down arrow keys, and we'll practice that in this challenge. This challenge will inject the flag into your history. Bring up a terminal, hit the up arrow, and grab it! In other challenges, the history will contain the log of the commands you've run, so if you need to run a similar command again, you can use the arrow keys to scroll through and find it!
### Solve
**Flag:** `pwn.college{kfsvF4O1Empa41kDi-u8rAicSj_.QX2MTM3EDLxATN1czW}`

It was said to use arrow keys to get the flag.

``` bash
Connected!
hacker@hello~command-history:~$ the flag is pwn.college{kfsvF4O1Empa41kDi-u8rAicSj_.QX2MTM3EDLxATN1czW}
```
## New Learnings
whoami, commands, arguments, command history

## References 
Linux Luminarium
