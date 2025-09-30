# Processes and Jobs
Computers execute software to get stuff done. In modern computing, this software is split into two categories: operating system kernels (about which we will learn much later) and processes, which we will discuss here. When Linux starts up, it launches an init (short for initializer) process that, in turn, launches a bunch of other processes which launch more processes until, eventually, you are looking at your command line shell, which is also a process! The shell, of course, launches processes in response to the commands you enter.

In this module, we will learn to view and interact with processes in a number of exciting ways!

## 1 Listing Processes
First, we will learn to list running processes using the ps command. Depending on whom you ask, ps either stands for "process snapshot" or "process status", and it lists processes. By default, ps just lists the processes running in your terminal, which honestly isn't very useful:

hacker@dojo:~$ `ps
    PID TTY          TIME CMD
    329 pts/0    00:00:00 bash
    349 pts/0    00:00:00 ps
hacker@dojo:~$`
In the above example, we have the shell (bash) and the ps process itself, and that's all that's running on that specific terminal. We also see that each process has a numerical identifier (the Process ID, or PID), which is a number that uniquely identifies every running process in a Linux environment. We also see the terminal on which the commands are running (in this case, the designation pts/0), and the total amount of cpu time that the process has eaten up so far (since these processes are very undemanding, they have yet to eat up even 1 second!).

In the majority of cases, this is all that you'll see with a default ps. To make it useful, we need to pass a few arguments.

As ps is a very old utility, its usage is a bit of a mess. There are two ways to specify arguments.

"Standard" Syntax: in this syntax, you can use -e to list "every" process and -f for a "full format" output, including arguments. These can be combined into a single argument -ef.

"BSD" Syntax: in this syntax, you can use a to list processes for all users, x to list processes that aren't running in a terminal, and u for a "user-readable" output. These can be combined into a single argument aux.

These two methods, ps -ef and ps aux, result in slightly different, but cross-recognizable output.

Let's try it in the dojo:

hacker@dojo:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
hacker         1       0  0 05:34 ?        00:00:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7       1  0 05:34 ?        00:00:00 /bin/sleep 6h
hacker       102       1  1 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server --auth=none -
hacker       138     102 11 05:34 ?        00:00:07 /usr/lib/code-server/lib/node /usr/lib/code-server/out/node/entr
hacker       287     138  0 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       318     138  6 05:34 ?        00:00:03 /usr/lib/code-server/lib/node --dns-result-order=ipv4first /usr/
hacker       554     138  3 05:35 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       571     554  0 05:35 pts/0    00:00:00 /usr/bin/bash --init-file /usr/lib/code-server/lib/vscode/out/vs
hacker       695     571  0 05:35 pts/0    00:00:00 ps -ef
hacker@dojo:~$
You can see here that there are processes running for the initialization of the challenge environment (docker-init), a timeout before the challenge is automatically terminated to preserve computing resources (sleep 6h to timeout after 6 hours), the VSCode environment (several code-server helper processes), the shell (bash), and my ps -ef command. It's basically the same thing with ps aux:

hacker@dojo:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
hacker         1  0.0  0.0   1128     4 ?        Ss   05:34   0:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7  0.0  0.0   2736   580 ?        S    05:34   0:00 /bin/sleep 6h
hacker       102  0.4  0.0 723944 64660 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       138  3.3  0.0 968792 106272 ?       Sl   05:34   0:07 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       287  0.0  0.0 717648 53136 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       318  3.3  0.0 977472 98256 ?        Sl   05:34   0:06 /usr/lib/code-server/lib/node --dns-result-order=
hacker       554  0.4  0.0 650560 55360 ?        Rl   05:35   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       571  0.0  0.0   4600  4032 pts/0    Ss   05:35   0:00 /usr/bin/bash --init-file /usr/lib/code-server/li
hacker      1172  0.0  0.0   5892  2924 pts/0    R+   05:38   0:00 ps aux
hacker@dojo:~$
There are many commonalities between ps -ef and ps aux: both display the user (USER column), the PID, the TTY, the start time of the process (STIME/START), the total utilized CPU time (TIME), and the command (CMD/COMMAND). ps -ef additionally outputs the Parent Process ID (PPID), which is the PID of the process that launched the one in question, while ps aux outputs the percentage of total system CPU and Memory that the process is utilizing. Plus, there's a bunch of other stuff we won't get into right now.

Anyways! Let's practice. In this level, I have once again renamed /challenge/run to a random filename, and this time made it so that you cannot ls the /challenge directory! But I also launched it, so you can find it in the running process list, figure out the filename, and relaunch it directly for the flag! Good luck!

NOTE: Both ps -ef and ps aux truncate the command listing to the width of your terminal (which is why the examples above line up so nicely on the right side of the screen. If you can't read the whole path to the process, you might need to enlarge your terminal (or redirect the output somewhere to avoid this truncating behavior)! Alternatively, you can pass the w option twice (e.g., ps -efww or ps auxww) to disable the truncation.

### Solve

**Flag:** `pwn.college{sae9zew7jrFH-Q0w-Way536s70D.dhzM4QDLxATN1czW}`

```bash
          Connected!
hacker@processes~listing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 16:04 ?        00:00:00 /sbin/docker-init -- /nix/va
root           7       1  0 16:04 ?        00:00:00 /run/dojo/bin/sleep 6h
root         132       1  0 16:04 ?        00:00:00 /challenge/19204-run-1934
root         135     132  0 16:04 ?        00:00:00 sleep 6h
hacker       137       0  0 16:04 pts/0    00:00:00 /nix/store/0nxvi9r5ymdlr2p24
hacker       143     137  0 16:04 pts/0    00:00:00 /run/dojo/bin/bash --login
hacker       157     143  0 16:04 pts/0    00:00:00 ps -ef
hacker@processes~listing-processes:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.2  0.0   1056   640 ?        Ss   16:04   0:00 /sbin/docker-
root           7  0.1  0.0 231708  2560 ?        S    16:04   0:00 /run/dojo/bin
root         132  0.0  0.0   4132  2560 ?        S    16:04   0:00 /challenge/19
root         135  0.0  0.0   2744  1280 ?        S    16:04   0:00 sleep 6h
hacker       137  0.3  0.0 231576  3520 pts/0    Ss   16:04   0:00 /nix/store/0n
hacker       143  0.0  0.0 231940  4160 pts/0    S    16:04   0:00 /run/dojo/bin
hacker       158  0.0  0.0 233600  3840 pts/0    R+   16:04   0:00 ps aux
hacker@processes~listing-processes:~$ ps auxw
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.0   1056   640 ?        Ss   16:04   0:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/b
root           7  0.0  0.0 231708  2560 ?        S    16:04   0:00 /run/dojo/bin/sleep 6h
root         132  0.0  0.0   4132  2560 ?        S    16:04   0:00 /challenge/19204-run-1934
root         135  0.0  0.0   2744  1280 ?        S    16:04   0:00 sleep 6h
hacker       137  0.1  0.0 231576  3520 pts/0    Ss   16:04   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p37/bin/bash /run/d
hacker       143  0.0  0.0 231940  4160 pts/0    S    16:04   0:00 /run/dojo/bin/bash --login
hacker       159  0.0  0.0 233600  3840 pts/0    R+   16:05   0:00 ps auxw
hacker@processes~listing-processes:~$ /challenge/19204-run-1934
Yahaha, you found me! Here is your flag:
pwn.college{sae9zew7jrFH-Q0w-Way536s70D.dhzM4QDLxATN1czW}
Now I will sleep for a while (so that you could find me with 'ps').

```

ps = process snapshot or process status,ps -e → list all processes ("every"),ps -f → full format (more details),ps with -ef or aux same thing, both are the same thing,ps -ef and ps aux truncate the command listing to the width of your terminal (which is why the examples above line up so nicely on the right side of the screen. If you can't read the whole path to the process, you might need to enlarge your terminal (or redirect the output somewhere to avoid this truncating behavior)! Alternatively, you can pass the w option twice (e.g., ps -efww or ps auxww) to disable the truncation.

---

## 2 Killing Processes

Describe how to terminate processes (`kill`, `kill -9`, `pkill`, `killall`) and when to use different signals.

### Solve

**Flag:** `pwn.college{8Q3SBEZ8py9oBQ801v0406Menlg.dJDN4QDLxATN1czW}`

```bash
Connected!                                                                        
hacker@processes~killing-processes:~$ ps -efww             
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 16:07 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 16:07 ?        00:00:00 /run/dojo/bin/sleep 6h
root         135       1  0 16:07 ?        00:00:00 su -c /challenge/.launcher hacker
hacker       136     135  0 16:07 ?        00:00:00 /challenge/dont_run
hacker       137     136  0 16:07 ?        00:00:00 sleep 6h
hacker       139       0  0 16:07 pts/0    00:00:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p37/bin/bash /run/dojo/bin/ssh-entrypoint
hacker       145     139  0 16:07 pts/0    00:00:00 /run/dojo/bin/bash --login
hacker       159     145  0 16:08 pts/0    00:00:00 ps -efww
hacker@processes~killing-processes:~$ kill 136
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{8Q3SBEZ8py9oBQ801v0406Menlg.dJDN4QDLxATN1czW}
hacker@processes~killing-processes:~$ 

```

find PID then kill PID then run the program.

---

## 3 Interrupting Processes
You've learned how to kill other processes with the kill command, but sometimes you just want to get rid of the process that's clogging up your terminal! Luckily, terminals have a hotkey for this: Ctrl-C (e.g., holding down the Ctrl key and pressing C) sends an "interrupt" to whatever application is waiting on input from the terminal and, typically, this causes the application to cleanly exit.

Try it here! /challenge/run will refuse to give you the flag until you interrupt it. Good luck!

For the very interested, check out this article about terminals and "control codes" (such as Ctrl-C).

### Solve

**Flag:** ``

```bash
# Example
hacker@dojo:~$ /challenge/run
# press Ctrl+C to interrupt
```

---

## 4 Suspending Processes

Cover `Ctrl+Z` to suspend a foreground job and what `Stopped` means in `jobs`/`ps` output.

### Solve

**Flag:** ``

```bash
# Example
hacker@dojo:~$ /challenge/run
# press Ctrl+Z
[1]+  Stopped                 /challenge/run
```

---

## 5 Resuming Processes

Describe `fg` to resume in foreground and `bg` to resume in background. Mention job specifiers like `%1`.

### Solve

**Flag:** ``

```bash
# Example
hacker@dojo:~$ fg %1
```

---

## 6 Killing misbehaving processes

Describe `fg` to resume in foreground and `bg` to resume in background. Mention job specifiers like `%1`.

### Solve

**Flag:** ``

```bash
# Example
hacker@dojo:~$ fg %1
```

---

## 7 Backgrounding Processes

Explain launching with `&`, using `nohup`, and `disown` for persistent background processes.

### Solve

**Flag:** ``

```bash
# Example
hacker@dojo:~$ /challenge/run &
[1] 12345
```

---

## 8 Foregrounding Processes

Discuss bringing background jobs back to the foreground with `fg`, checking `jobs` to see job IDs.

### Solve

**Flag:** ``

```bash
# Example
hacker@dojo:~$ jobs
hacker@dojo:~$ fg %1
```

---

## 9 Starting Backgrounded Processes

Show running commands in background, and differences between starting backgrounded vs. suspending + bg.

### Solve

**Flag:** ``

```bash
# Example
hacker@dojo:~$ /challenge/run &
```

---

## 10 Process Exit Codes

Explain exit codes, `$?`, and how to check the last command's exit status. Mention common conventions (0 success).

### Solve

**Flag:** ``

```bash
# Example
hacker@dojo:~$ false
hacker@dojo:~$ echo $?
1
```

---

## New Learnings
ps = process snapshot or process status,ps -e → list all processes ("every"),ps -f → full format (more details),ps with ef or aux same thing, ps -efww or ps auxww for without truncation

## References
Linux Luminarium


