#Terminal Multiplexing
## 1 Launching Screen

Let's dive right in!

screen is a program that creates virtual terminals inside your terminal. It's somewhat like having multiple browser tabs, but for your command line!

Starting screen is super simple:

hacker@dojo:~$ screen
That's it! You're now inside a screen session. It looks exactly like a terminal, but there are new capabilities there, waiting to be discovered.

For this challenge, we've hooked things up so that just launching screen will get you the flag. Easy!

NOTE: When you're done with your command line, type exit or press Ctrl-D to leave the screen session. Then screen will terminate and return you to your original shell.

### Solve
Congratulations! You're inside a screen session!
Here's your flag:
pwn.college{Yb-OKFGTbwnh-YojMgbSrAv3HIB.QX1gjM4EDLxATN1czW}
hacker@terminal-multiplexing~launching-screen:~$

## 2 Detaching and Attaching

Now we'll start digging in with the magic of detaching!

Imagine you're working on something important over a remote connection, and your connection drops. With a normal terminal (outside of this awesome dojo environment), everything's gone. With screen, your work keeps running, and you can reattach later!

You can also detach on purpose, which we'll do in this challenge. You detach by pressing Ctrl-A, followed by d (for detach). This leaves your session running in the background while you return to your normal terminal.

hacker@dojo:~$ screen
[doing some work...]
[Press Ctrl-A, then d]
[detached from 12345.pts-0.hostname]
hacker@dojo:~$ 
To reattach, you can use the -r argument to screen:

hacker@dojo:~$ screen -r
For this challenge, you'll need to:

Launch screen
Detach from it.
Run /challenge/run (this will secretly send the flag to your detached session!)
Reattach to see your prize
FUN FACT: Ctrl-A is screen's activation key for all of its shortcuts in its default configuration. All screen functionality is activated by some command combination starting with Ctrl-A.

HINT: Remember: Hold Ctrl and press A, then release both and press d.

HINT: If you see [detached from...], you did it right!

### Solve
Connected!                                                                        
hacker@terminal-multiplexing~detaching-and-attaching:~$ screen
[detached from 166.pts-0.terminal-multiplexing~detaching-and-attaching]
hacker@terminal-multiplexing~detaching-and-attaching:~$ /challenge/run
Found detached screen session: 166.pts-0.terminal-multiplexing~detaching-and-attaching
Sending flag to your screen session...

Flag sent! Now reattach to your screen session with:

  screen -r

You'll find the flag waiting for you there!
hacker@terminal-multiplexing~detaching-and-attaching:~$ screen -r
[screen is terminating]
hacker@terminal-multiplexing~detaching-and-attaching:~$ 
## 3 Finding Sessions

Time for some screen detective work!

If you become an avid screen user, you will inevitably end up with multiple sessions running. How do you find the right one to reattach to?

Well, we can list them:

hacker@dojo:~$ screen -ls
There are screens on:
        23847.mysession   (Detached)
        23851.goodwork    (Detached)
        23855.morework    (Detached)
3 Sockets in /run/screen/S-hacker.
The identifiers of the sessions are the PID of each respective screen process, a dot, and the name of the screen session. To attach to a specific one, you use its name or its PID by giving it as an argument to screen -r.

hacker@dojo:~$ screen -r goodwork
In this challenge, we've created three screen sessions for you. One of them contains the flag. The other two are decoys!

You'll need to check each one until you find it. Don't forget to detach (Ctrl-A d) before trying the next session!

### Solve
Connected!                                                                        
hacker@terminal-multiplexing~finding-sessions:~$ screen -ls
There are screens on:
	175.pts-0.terminal-multiplexing~launching-screen	(Remote or dead)
	144.session_7fcc4116e9a18f85	(Detached)
	147.session_0fc629dd6b28069e	(Detached)
	150.session_2f61cc34af235c49	(Detached)
4 Sockets in /home/hacker/.screen.
hacker@terminal-multiplexing~finding-sessions:~$ screen -r 23847.mysession
There is no screen to be resumed matching 23847.mysession.
hacker@terminal-multiplexing~finding-sessions:~$ screen -r 144.session_7fcc4116e9a18f85
[screen is terminating]
hacker@terminal-multiplexing~finding-sessions:~$ 

hacker@terminal-multiplexing~finding-sessions:~$  echo 'Congratulations! You found the right session!'
Congratulations! You found the right session!
hacker@terminal-multiplexing~finding-sessions:~$  echo pwn.college{0F0gIJqgXfkrxyTShQpdPDOgF9o.QX3gjM4EDLxATN1czW}
pwn.college{0F0gIJqgXfkrxyTShQpdPDOgF9o.QX3gjM4EDLxATN1czW}
hacker@terminal-multiplexing~finding-sessions:~$ 



## 4 Switching Windows

Okay, so far, screen is just a weird sort of terminal-with-a-terminal. But it can be much more!

Inside a single screen session, you can have multiple windows, like your browser has multiple tabs. This can be super handy for organizing different tasks!

These windows are handled with different keyboard shortcuts, all starting with Ctrl-A:

Ctrl-A c - Create a new window
Ctrl-A n - Next window
Ctrl-A p - Previous window
Ctrl-A 0 through Ctrl-A 9 - Jump directly to window 0-9
Ctrl-A " - bring up a selection menu of all of the windows
For this challenge, we've set up a screen session with two windows:

Window 0 has... well, you'll have to switch there to find out!
Window 1 has a welcome message
Attach to the session with screen -r, then use one of the key combinations above to switch to Window 1. Go get that flag!

### Solve
Connected!                                                                        
hacker@terminal-multiplexing~switching-windows:~$ screen -r
[screen is terminating]
hacker@terminal-multiplexing~switching-windows:~$ 

 cat <<MSG
Welcome to the window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-A 0 to switch to window 0!
MSG
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Welcome to the window switching challenge!
> You are currently in window 1.
> The flag is hidden in window 0.
> Use Ctrl-A 0 to switch to window 0!
> MSG
Welcome to the window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-A 0 to switch to window 0!
hacker@terminal-multiplexing~switching-windows:~$
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{QbDllthl5Tu3eTP0K1se5QBb-6u.QX4gjM4EDLxATN1czW}> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{QbDllthl5Tu3eTP0K1se5QBb-6u.QX4gjM4EDLxATN1czW}
hacker@terminal-multiplexing~switching-windows:~$


## 5 Detaching and Attaching(tmux)

Let's try the same thing with tmux!

tmux (terminal multiplexer) is screen's younger, more modern cousin. It does all the same things but with some different key bindings. The biggest difference? Instead of Ctrl-A, tmux uses Ctrl-B as its command prefix.

So to detach from tmux, you press Ctrl-B followed by d.

hacker@dojo:~$ tmux
[doing some work...]
[Press Ctrl-B, then d]
[detached (from session 0)]
hacker@dojo:~$ 
The commands also differ:

tmux ls - List sessions
tmux attach or tmux a - Reattach to session
For this challenge:

Launch tmux
Detach from it.
Run /challenge/run (this will send the flag to your detached session!)
Reattach to see your prize

### Solve

hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$  echo Congratulations, here is your flag: pwn.college{UnAuph19TWmm_tvsFG8EBdptLx0.QX5gjM4EDLxATN1czW}
Congratulations, here is your flag: pwn.college{UnAuph19TWmm_tvsFG8EBdptLx0.QX5gjM4EDLxATN1czW}
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ 


## 6 Switching Windows(tmux)

Let's learn to navigate windows in tmux!

Just like screen, tmux has windows. The key combos are different, but the concept is the same:

Ctrl-B c - Create a new window
Ctrl-B n - Next window
Ctrl-B p - Previous window
Ctrl-B 0 through Ctrl-B 9 - Jump to window 0-9
Ctrl-B w - See a nice window picker
Tmux shows your windows at the bottom in a status bar that looks like:

[0] 0:bash* 1:bash
The * shows your current window, and each entry also shows the process that the window was created to run.

We've created a tmux session with two windows:

Window 0 has the flag!
Window 1 has your warm welcome.
Go get that flag!

### Solve
Connected!                                                                        
hacker@terminal-multiplexing~switching-windows-tmux:~$ tmux attach

hacker@terminal-multiplexing~switching-windows-tmux:~
hacker@terminal-multiplexing~switching-windows-tmux:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{UPf2oRBAUpTYcyxkbxsw2KrfH22.QXwkjM4EDLxATN1czW}> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{UPf2oRBAUpTYcyxkbxsw2KrfH22.QXwkjM4EDLxATN1czW}
hacker@terminal-multiplexing~switching-windows-tmux:~$