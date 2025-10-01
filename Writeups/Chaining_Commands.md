#Chaining Commnands
## 1 Chaining with Semicolons

The easiest way to chain commands is ;. In most contexts, ; separates commands in a similar way to how Enter separates lines. So, this:

hacker@dojo:~$ echo COLLEGE > pwn
hacker@dojo:~$ cat pwn
COLLEGE
hacker@dojo:~$
Is roughly the same as this:

hacker@dojo:~$ echo COLLEGE > pwn; cat pwn
COLLEGE
hacker@dojo:~$
Basically, when you hit Enter, your shell executes your typed command and, after that command terminates, gives you the prompt to input another command. The semicolon is analogous, just without the prompt and with you entering both commands before anything is executed.

Give it a try now! In this level, you must run /challenge/pwn and then /challenge/college, chaining them with a semicolon.
### Solve 
debrato@debrato:~$ ssh -i ./key hacker@dojo.pwn.college Connected!
hacker@chaining-chaining-with-semicolons:~$ /challenge/pwn;/challenge/college Yes! You chained /challenge/pwn and /challenge/college! Here is your flag: pwn.college{YKbc7sr7EQxjrzVMxtfRzKape8D.dVTN4QDLXATN1CZW}
hacker@chaining~chaining-with-semicolons:~$

## 2 Building on Success

You learned about exit codes in the Processes module. Now let's use them to chain commands together!

The && operator allows you to run a second command only if the first command succeeds (in Linux convention, this means it exited with code 0). This is called the "AND" operator because both conditions must be true: the first command must succeed AND then the second command will run. That's super useful for complex commandline workflows where certain actions depend on the success of other actions.

Here's the syntax:

hacker@dojo:~$ command1 && command2
This means: "Run command1, and IF it succeeds, then run command2."

Some examples:

hacker@dojo:~$ touch /home/hacker/file && echo "this will run"
success
this will run
hacker@dojo:~$ touch /file && echo "this will NOT run"
touch: cannot touch '/file': Permission denied
hacker@dojo:~$
That second invocation of touch failed because the hacker user does not have write access to /file, so the echo did not run.

In this challenge, you need to chain the programs /challenge/first-success and /challenge/second using the && operator. Try running each command separately first to see what happens (which is that you will not get the flag). But if you chain them with &&, the flag will appear!
### Solve
Connected!                                                                        
hacker@chaining~building-on-success:~$ /challenge/first-success && /challenge/second
Nice chaining! Flag: pwn.college{cW3UDFFNwMCnbQGyh8RjehNTx3v.QXyQzM4EDLxATN1czW}
hacker@chaining~building-on-success:~$ 


## 3 Handling Failure

You just learned about the && operator, which runs the second command only if the first succeeds. Now let's learn about its opposite: the || operator allows you to run a second command only if the first command fails (exits with a non-zero code). This is called the "OR" operator because either the first command succeeds OR the second command will run.

Here's the syntax:

hacker@dojo:~$ command1 || command2
This means: "Run command1, and IF it fails, then run command2."

Some examples:

hacker@dojo:~$ touch /file || echo "touch failed, so this runs"
touch: cannot touch '/file': Permission denied
touch failed, so this runs
hacker@dojo:~$ touch /home/hacker/file || echo "this will NOT run"
hacker@dojo:~$
The || operator is super useful for providing fallback commands or error handling!

In this challenge, you need to chain /challenge/first-failure and /challenge/second using the || operator. Go for it!
### Solve
Connected!
hacker@chaining~handling-failure:~$ /challenge/first-failure || /challenge/second
Nice chaining! Flag: pwn.college{k56CjuzMJb46wp4kK1cG1hOBzqH.QXzQzM4EDLxATN1czW}
hacker@chaining~handling-failure:~$ 


## 4 Your First Shell Script 

As you combine more and more commands to achieve complex effects, the length of the combined prompt quickly gets really annoying to deal with. When this happens, you can put these commands in a file, called a shell script, and run them by executing the file! For example, consider our semicolon technique:

hacker@dojo:~$ echo COLLEGE > pwn; cat pwn
COLLEGE
hacker@dojo:~$
We can create a shell script called pwn.sh (by convention, shell scripts are frequently named with a sh suffix):

echo COLLEGE > pwn
cat pwn
And then we can execute by passing it as an argument to a new instance of our shell (bash)! When a shell is invoked like this, rather than taking commands from the user, it reads commands from the file.

hacker@dojo:~$ ls
hacker@dojo:~$ bash pwn.sh
COLLEGE
hacker@dojo:~$ ls
pwn
hacker@dojo:~$
You can see that the shell script executed both commands, creating and printing the pwn file.

Now, it's your turn! Same as last level, run /challenge/pwn and then /challenge/college, but this time in a shell script called x.sh, then run it with bash!

NOTE: We haven't yet talked about Linux's amazing array of competent command line file editors. For now, feel free to use the Text Editor application in Desktop mode (Applications->Accessories->Text Editor) or the default editor in the VSCode Workspace!


### Solve

debrato@debrato:~$ ssh -i ./key hacker@dojo.pwn.college Connected!
hacker@chaining-your-first-shell-script:~$ vim x.sh hacker@chaining-your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag: pwn.college{Ud6IgPa8HiJWfYMSOvf7J0iYY9X.dFzN4QDLXATN1CZW}
hacker@chaining-your-first-shell-script:~$

## 5 Redirecting Script Output

Let's try something a bit trickier! You've piped output between programs with |, but so far, this has just been between one command's output and a different command's input. But what if you wanted to send the output of several programs to one command? There are a few ways to do this, and we'll explore a simple one here: redirecting output from your script!

As far as the shell is concerned, your script is just another command. That means you can redirect its input and output just like you did for commands in the Piping module! For example, you can write it to a file:

hacker@dojo:~$ cat script.sh
echo PWN
echo COLLEGE
hacker@dojo:~$ bash script.sh > output
hacker@dojo:~$ cat output
PWN
COLLEGE
hacker@dojo:~$
All of the various redirection methods work: > for stdout, 2> for stderr, < for stdin, >> and 2>> for append-mode redirection, >& for redirecting to other file descriptors, and | for piping to another command.

In this level, we will practice piping (|) from your script to another program. Like before, you need to create a script that calls the /challenge/pwn command followed by the /challenge/college command, and pipe the output of the script into a single invocation of the /challenge/solve command!
### Solve
debrato@debrato:~$ ssh -i ./key hacker@dojo.pwn.college Connected!
hacker@chaining~redirecting-script-output:~$ vim x.sh
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{YNgQJnXdU06CIyLfwE3FMRMVгWN.dhTM5QDLXATN1CZW}
hacker@chaining~redirecting-script-output:~$	

## 6 Executable Shell Scripts

You have written your first shell script, but calling it via bash script.sh is a pain. Why do you need that bash?

When you invoke bash script.sh, you are, of course launching the bash command with the script.sh argument. This tells bash to read its commands from script.sh instead of standard input, and thus your shell script is executed.

It turns out that you can avoid the need to manually invoke bash. If your shell script file is executable (recall File Permissions), you can simply invoke it via its relative or absolute path! For example, if you create script.sh in your home directory and make it executable, you can invoke it via /home/hacker/script.sh or ~/script.sh or (if your working directory is /home/hacker) ./script.sh.

Try that here! Make a shellscript that will invoke /challenge/solve, make it executable, and run it without explicitly invoking bash!
### Solve
debrato@debrato:~$ ssh -i ./key hacker@dojo.pwn.college Connected!
hacker@chaining-executable-shell-scripts:~$ vim script.sh
hacker@chaining~executable-shell-scripts:~$ chmod ugo+rwx script.sh hacker@chaining~executable-shell-scripts:~$ ./script.sh Congratulations on your shell script execution! Your flag: pwn.college{kZaDiIXt-rfLbiJm1LpYLXQMhvT.dRzNyUDLXATN1CZW}
hacker@chaining~executable-shell-scripts:~$

## 7 Understanding Shebangs

You're well on your way to your new life as a shell scripter! However, so far, your shellscripts can only be launched from the shell. Things worked great in the previous level (because you were invoking your script from the bash shell), but they won't work if your script was being invoked by, say, a program written in Python (or any other language).

When a program is invoked in Linux, the Linux kernel first inspects the file to determine how it should be run. This does NOT use the extension (which is why you don't have to name your shell scripts with a .sh extension, or your Python scripts with a .py extension, or so on). Rather, Linux looks at the first few bytes of the file for this information.

There are a bunch of different types of programs, but if the program file starts with the characters #! (often termed a "shebang"), Linux treats the file as an interpreted program, and the contents of the rest of the line as the path to the interpreter. It then invokes the interpreter with the path to the program file as its only argument.

Consider this shell script:

#!/bin/bash

echo "Hello Hackers!"
This can be executed as:

hacker@dojo:~$ chmod a+x script.sh
hacker@dojo:~$ ./script.sh
Hello Hackers!
hacker@dojo:~$
When ./script.sh was executed, Linux opened the file, read the first line, extracted /bin/bash as the interpreter, and executed /bin/bash ./script.sh to launch the script!

Note, the shebang line must be the VERY FIRST line of the file - no blank lines or spaces before it!

For this challenge, create a script at /home/hacker/solve.sh that has a proper shebang and outputs "hack the planet". Remember to make it executable, then run /challenge/run to verify your script works correctly!

FUN FACT: Common shebangs you might see:

#!/bin/bash for bash scripts
#!/usr/bin/python3 for Python scripts
#!/bin/sh for POSIX shell scripts --- this is a more primitive predecessor to bash with fewer features, but more compatibility to non-Linux systems!

### Solve
Connected!
hacker@chaining~understanding-shebangs:~$ cat > /home/hacker/solve.sh <<'EOF'
> echo "hack the planet"
> EOF
hacker@chaining~understanding-shebangs:~$ chmod +x /home/hacker/solve.sh
hacker@chaining~understanding-shebangs:~$ /challenge/run
Error: /home/hacker/solve.sh doesn't start with a proper shebang!
The first line should be: #!/bin/bash
There's no shebang at all in your script.
hacker@chaining~understanding-shebangs:~$ # Overwrite solve.sh with a clean shebang-first script
printf '%s\n' '#!/bin/bash' 'echo "hack the planet"' > /home/hacker/solve.sh

# Ensure no CRLF endings (if any) and make it executable
sed -i 's/\r$//' /home/hacker/solve.sh
chmod +x /home/hacker/solve.sh

# Verify the first line and run the challenge checker
echo "First line of file:"
head -n 1 /home/hacker/solve.sh
echo "--- Running verifier ---"
First line of file:
#!/bin/bash
--- Running verifier ---
hacker@chaining~understanding-shebangs:~$ /challenge/run
Testing your script...
Perfect! Your flag:
Flag: pwn.college{MqhpXd6RaTo9Ov7-B7-PjkmS0Ve.QX5MzM4EDLxATN1czW}

hacker@chaining~understanding-shebangs:~$ ^C


## 8 Scripting with Arguments

You've learned how to make shell scripts, but so far they've just been lists of commands. Scripts become much more powerful when they can accept arguments! This might look like:

hacker@dojo:~$ bash myscript.sh hello world
The script can access these arguments using special variables:

$1 contains the first argument ("hello")
$2 contains the second argument ("world")
$3 would contain the third argument (if there had been one)
...and so on
Here's a simple example:

hacker@dojo:~$ cat myscript.sh
#!/bin/bash
echo "First argument: $1"
echo "Second argument: $2"
hacker@dojo:~$ bash myscript.sh hello world
First argument: hello
Second argument: world
hacker@dojo:~$
For this challenge, you need to write a script at /home/hacker/solve.sh that:

Takes two arguments
Outputs them in REVERSE order (second argument first, then the first argument)
For example:

hacker@dojo:~$ bash /home/hacker/solve.sh pwn college
college pwn
hacker@dojo:~$
Once your script works correctly, run /challenge/run to get your flag!

### Solve
Connected!
hacker@chaining~scripting-with-arguments:~$ # create the script with the shebang as the very first line
printf '%s\n' '#!/bin/bash' 'echo "$2 $1"' > /home/hacker/solve.sh

# strip any stray CRLFs and make executable
sed -i 's/\r$//' /home/hacker/solve.sh
chmod +x /home/hacker/solve.sh

# quick manual test (you should see "college pwn")
/home/hacker/solve.sh pwn college
college pwn
hacker@chaining~scripting-with-arguments:~$ /challenge/run
Correct! Your script properly reversed the arguments.
Here's your flag:
pwn.college{oR4eMiuS3fkKZ1TXGHNs53Ncci0.QX1MzM4EDLxATN1czW}
hacker@chaining~scripting-with-arguments:~$ 

## 9 Scripting with Conditionals

Now that you can use arguments in scripts, let's make them smarter with conditional logic!

In bash, you can use if statements to make decisions:

if [ "$1" == "ping" ]
then
    echo "pong"
fi
The above, in English, is if the first argument is "ping", print out "pong". The syntax is somewhat unforgiving for a few reasons. First, you must have spaces after if (if you're used to a language like C, this is different), after [, and before ]. Second, if, then, and fi must all be on different lines (or separated by semicolons); you can't lump them into the same statement. It's also a bit weird: instead of endif or end or something like that, the terminator of the if statement is fi (if backwards). Just something you have to remember.

For this challenge, write a script at /home/hacker/solve.sh that:

Takes one argument
If the argument is "pwn", output "college"
For any other input, output nothing
Example:

hacker@dojo:~$ bash /home/hacker/solve.sh pwn
college
hacker@dojo:~$ bash /home/hacker/solve.sh foo
hacker@dojo:~$
Once your script works correctly, run /challenge/run to get your flag!

NOTE: Interested in what else you can check in a condition, other than string equality? Read all about it with help test!

### Solve
Connected!
hacker@chaining~scripting-with-conditionals:~$ # create the script (shebang MUST be the very first line)
printf '%s\n' '#!/bin/bash' 'if [ "$1" = "pwn" ]; then' '  echo "college"' 'fi' > /home/hacker/solve.sh

# remove any Windows CRLFs just in case, make executable
sed -i 's/\r$//' /home/hacker/solve.sh
chmod +x /home/hacker/solve.sh

# quick tests:
echo "should print 'college':"
/home/hacker/solve.sh pwn

echo "should print nothing (blank line follows):"
/home/hacker/solve.sh foo
should print 'college':
college
should print nothing (blank line follows):
hacker@chaining~scripting-with-conditionals:~$ /challenge/run
Correct! Your script properly handles all the conditions.
Here's your flag:
pwn.college{cs7W5e6wuNOcOxeJs1cif_GhaAO.QX2MzM4EDLxATN1czW}
hacker@chaining~scripting-with-conditionals:~$ 


## 10 Scripting with Default Cases

Your if statements so far have handled specific cases, but what about everything else? That's where else comes in!

The else clause executes when the if condition is false:

if [ "$1" == "hello" ]
then
    echo "Hi there!"
else
    echo "I don't understand"
fi
Note that the else doesn't have a condition --- it catches everything that didn't match previously. It also doesn't have a then statement. Finally, the fi goes after the else block to denote the end of the whole complex statement! It is also optional: you didn't have it in the previous level, and you only need it if the logic you're trying to achieve demands it.

Here's a practical example:

if [ "$1" == "start" ]
then
    echo "Starting the service..."
else
    echo "Unknown command. Use 'start' to begin."
fi
For this challenge, write a script at /home/hacker/solve.sh that:

Takes one argument
If the argument is "pwn", output "college"
For any other input, output "nope"
Example:

hacker@dojo:~$ bash /home/hacker/solve.sh pwn
college
hacker@dojo:~$ bash /home/hacker/solve.sh hack
nope
hacker@dojo:~$ bash /home/hacker/solve.sh anything
nope
hacker@dojo:~$
Once your script works correctly, run /challenge/run to get your flag!

### Solve
Connected!
hacker@chaining~scripting-with-default-cases:~$ # create the script (shebang must be the VERY first line)
printf '%s\n' '#!/bin/bash' 'if [ "$1" = "pwn" ]; then' '  echo "college"' 'else' '  echo "nope"' 'fi' > /home/hacker/solve.sh

# ensure no Windows CRLFs and make executable
sed -i 's/\r$//' /home/hacker/solve.sh
chmod +x /home/hacker/solve.sh

# quick tests (expected: "college" then "nope")
echo "---- test with 'pwn' ----"
/home/hacker/solve.sh pwn
echo "---- test with 'hack' ----"
/home/hacker/solve.sh hack
---- test with 'pwn' ----
college
---- test with 'hack' ----
nope
hacker@chaining~scripting-with-default-cases:~$ /challenge/run
Correct! Your script properly handles the if/else conditions.
Here's your flag:
pwn.college{4EocGrPZzh47zWECB4oTwj4MTDe.QX3MzM4EDLxATN1czW}
hacker@chaining~scripting-with-default-cases:~$ 


## 11 Scripitng with Multiple Conditions

You've learned how to use a single if statement to check a condition. But what if you need to check multiple conditions? You can use elif (short for else if):

if [ "$1" == "one" ]
then
    echo "1"
elif [ "$1" == "two" ]
then
    echo "2"
elif [ "$1" == "three" ]
then
    echo "3"
else
    echo "unknown"
fi
Note that you do need a then after the elif, just like the if. As before the else at the end catches everything that didn't match.

For this challenge, write a script at /home/hacker/solve.sh that:

Takes one argument
If the argument is "hack", output "the planet"
If the argument is "pwn", output "college"
If the argument is "learn", output "linux"
For any other input, output "unknown"
Example:

hacker@dojo:~$ bash /home/hacker/solve.sh hack
the planet
hacker@dojo:~$ bash /home/hacker/solve.sh pwn
college
hacker@dojo:~$ bash /home/hacker/solve.sh learn
linux
hacker@dojo:~$ bash /home/hacker/solve.sh foo
unknown
hacker@dojo:~$
Once your script works correctly, run /challenge/run to get your flag!

NOTE: As you're creating your script, make sure to follow the spacing closely in the examples. Unlike many other languages, bash requires the [ and the ] to be separated from other characters by spaces, otherwise it cannot parse the condition.

### Solve
hacker@chaining~scripting-with-multiple-conditions:~$ # create the script with shebang as the VERY first line
printf '%s\n' '#!/bin/bash' \
'if [ "$1" = "hack" ]; then' \
'  echo "the planet"' \
'elif [ "$1" = "pwn" ]; then' \
'  echo "college"' \
'elif [ "$1" = "learn" ]; then' \
'  echo "linux"' \
'else' \
'  echo "unknown"' \
'fi' > /home/hacker/solve.sh

# ensure no CRLFs and make executable
sed -i 's/\r$//' /home/hacker/solve.sh
chmod +x /home/hacker/solve.sh

# quick tests (expected outputs shown in comments)
echo "---- test: hack ----"
/home/hacker/solve.sh hack    # the planet

echo "---- test: pwn ----"
/home/hacker/solve.sh pwn     # college

echo "---- test: learn ----"
/home/hacker/solve.sh learn   # linux

echo "---- test: foo ----"
/home/hacker/solve.sh foo     # unknown
---- test: hack ----
the planet
---- test: pwn ----
college
---- test: learn ----
linux
---- test: foo ----
unknown
hacker@chaining~scripting-with-multiple-conditions:~$ /challenge/run
Correct! Your script properly handles all the conditions with elif.
Here's your flag:
pwn.college{AHumNGZ13LfkKRbOLqcXYkOJBpo.QX4MzM4EDLxATN1czW}
hacker@chaining~scripting-with-multiple-conditions:~$ 



## 12 Reading Shell Scripts

You're not the only one who writes shell scripts! They are very handy for doing simple "system-level" tasks, and are a common tool that developers and sysadmins reach for. In fact, a surprising fraction of the programs on a typical Linux machine are shell scripts.

In this level, we will learn to read shell scripts. /challenge/run is a shell script that requires you to put in a secret password, but that password is hardcoded into the script iself! Read the script (using, say, cat), figure out the password, and get the flag!

NOTE: Feel free to try to read the code of other challenges as well! Reading code is a critical strategy in learning new skills, because you can see how certain functionality was implemented and reuse those strategies in your own scripts. But watch out: some program files are machine code, and will not be readable to humans. You can use the file command to differentiate, but almost all the challenges in the Linux Luminarium are implemented as shell scripts and are safe to cat out.

### Solve

(base) aryan@aryan:~$ ssh hacker@dojo.pwn.college
hacker@dojo.pwn.college: Permission denied (publickey).
(base) aryan@aryan:~$ ssh -i ./key hacker@dojo.pwn.college
Connected!                                                                        
hacker@chaining~reading-shell-scripts:~$ file /challenge/run
ls -l /challenge/run
/challenge/run: setuid a /opt/pwn.college/bash script, ASCII text executable
-rwsr-xr-x 1 root root 198 Aug 24 19:04 /challenge/run
hacker@chaining~reading-shell-scripts:~$ less /challenge/run
hacker@chaining~reading-shell-scripts:~$ echo 'hack the PLANET' | /challenge/run
CORRECT! Your flag:
pwn.college{cld4NRk9_qVon_YE18sSs4nZ5vd.QXyADO4EDLxATN1czW}
hacker@chaining~reading-shell-scripts:~$