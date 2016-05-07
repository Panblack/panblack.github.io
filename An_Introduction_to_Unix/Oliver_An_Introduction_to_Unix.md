#Oliver An Introduction to Unix

Everybody Knows How to Use a Computer, but Not Everyone Knows How to Use the Command Line. Yet This is the Gateway to Doing Anything and Everything Sophisticated with a Computer and the Most Natural Starting Place to Learn Programming
by Oliver; Jan. 13, 2014

## Table of Contents
1. Introduction
2. 100 Useful Unix Commands
3. Getting Started: Opening the Terminal
4. The Definitive Guides to Unix, Bash, and the Coreutils
5. The Unix Filestructure
6. The Great Trailing Slash Debate
7. Where Are You? - Your Path and How to Navigate through the Filesystem
8. Gently Wading In - The Top 10 Indispensable Unix Commands
9. ls
10. Single Line Comments in Unix
11. The Primacy of Text Files, Text Editors
12. echo and cat
13. cp, mv, and rm
14. Variables in Unix
15. Escape Sequences
16. Global Variables in Unix
17. The PATH
18. Links
19. What is Scripting?
20. File Suffixes in Unix
21. The Shebang
22. bash
23. chmod
24. ssh
25. Saving to a File; Stdout and Stderr
26. More on Stdout and Stderr; Redirection
27. Conditional Logic
28. File Test Operators; Return or Exit Status
29. Basic Loops
30. Arguments to a Script
31. Multi-Line Comments, Multi-Line Strings in Bash
32. Source and Export
33. Dotfiles (.bashrc and .bash_profile)
34. Working Faster with Readline Functions and Key Bindings
35. More on Key Bindings, the ASCII Table, Control-v
36. Aliases, Functions
37. The Top 20 Indispensable Unix Commands
38. head and tail
39. less and more
40. grep
41. sort
42. history
43. Piping in Unix
44. Command Substitution
45. Process Substitution
46. Interlude - Bell Laboratories 1982 Unix Video
47. Processes and Running Processes in the Background
48. sudo and the Root User
49. awk
50. sed
51. More awk Examples
52. Regular Expressions and Globbing in Bash
53. Command Line Perl and Regex
54. Text Editors Revisited: Vim
55. Example Problems on the Command Line
56. Example Bash Scripts
57. Using the Python Shell to do Math, and More
58. tmux
59. Installing Programs on the Command Line
60. Bash in the Programming Ecosystem (or When Not to Use Bash)
61. Concluding Notes
62. Acknowledgements and Postscript

## Introduction
I took programming in high school, but I never took to it. This, I strongly believe, is because it wasn't taught right—and teaching it right means starting at the beginning, with unix. The reason for this is three-fold: (1) it gives you a deeper sense of how a high-level computer works (which a glossy front, like Windows, conceals); (2) it's the most natural port of entry into all other programming languages; and (3) it's super-useful in its own right. If you don't know unix and start programming, some things will forever remain hazy and mysterious, even if you can't put your finger on exactly what they are. If you already know a lot about computers, the point is moot; if you don't, then by all means start your programming education by learning unix!

A word about terminology here: I'm in the habit of horrendously confusing and misusing all of the precisely defined words "Unix", "Linux", "The Command Line", "The Terminal", "Shell Scripting", and "Bash." Properly speaking, unix is an operating system while linux refers to a closely-related family of unix-based operating systems, which includes commercial and non-commercial distributions [1]. (Unix was not free under its developer, AT&T, which caused the unix-linux schism.) The command line, as Wikipedia says, is:

    ... a means of interacting with a computer program where the user issues commands to the program in the form of successive lines of text (command lines) ... The interface is usually implemented with a command line shell, which is a program that accepts commands as text input and converts commands to appropriate operating system functions.

So what I mean when I proselytize for "unix", is simply that you learn how to punch commands in on the command line. The terminal is your portal into this world. Here's what my mine looks like:

image

There is a suite of commands to become familiar with—The GNU Core Utilities (wiki entry)—and, in the course of learning them, you learn about computers. Unix is a foundational piece of a programming education.

In terms of bang for the buck, it's also an excellent investment. You can gain powerful abilities by learning just a little. My coworker was fresh out of his introductory CS course, when he was given a small task by our boss. He wrote a full-fledged program, reading input streams and doing heavy parsing, and then sent an email to the boss that began, "After 1.5 days of madly absorbing perl syntax, I completed the exercise..." He didn't know how to use the command-line at the time, and now a print-out of that email hangs on his wall as a joke—and as a monument to the power of the terminal.

You can find ringing endorsements for learning the command line from all corners of the internet. For instance, in the excellent course Startup Engineering (Stanford/Coursera) Balaji Srinivasan writes:

    A command line interface (CLI) is a way to control your computer by typing in commands rather than clicking on buttons in a graphical user interface (GUI). Most computer users are only doing basic things like clicking on links, watching movies, and playing video games, and GUIs are fine for such purposes.

    But to do industrial strength programming - to analyze large datasets, ship a webapp, or build a software startup - you will need an intimate familiarity with the CLI. Not only can many daily tasks be done more quickly at the command line, many others can only be done at the command line, especially in non-Windows environments. You can understand this from an information transmission perspective: while a standard keyboard has 50+ keys that can be hit very precisely in quick succession, achieving the same speed in a GUI is impossible as it would require rapidly moving a mouse cursor over a profusion of 50 buttons. It is for this reason that expert computer users prefer command-line and keyboard-driven interfaces.

To provide foreshadowing, here are some things you can do in unix:

    make or rename 100 folders or files en masse
    find all files of a given extension or any file that was created within the last week
    log onto a computer remotely and access its files with ssh
    copy files to your computer directly over the network (no external hard drive necessary!) with rsync
    run a Perl or Python script
    run one of the many programs that are only available on the command line
    see all processes running on your computer or the space occupied by your folders
    see or change the permissions on a file
    parse a text file in any way imaginable (count lines, swap columns, replace words, etc.)
    soundly encrypt your files or communications with gpg2
    run your own web server on the Amazon cloud with nginx

What do all of these have in common? All are hard to do in the GUI, but easy to do on the command line. It would be remiss not to mention that unix is not for everything. In fact, it's not for a lot of things. Knowing which language to use for what is usually a matter of common sense. However, when you start messing about with computers in any serious capacity, you'll bump into unix very quickly—and that's why it's our starting point.

Is this the truth, the whole truth, and nothing but the truth, so help my white ass? I believe it is, but also my trajectory through the world of computing began with unix. So perhaps I instinctively want to push this on other people: do it the way I did it. And, because it occupies a bunch of my neuronal real estate at the moment, I could be considered brainwashed :-)


[1] Still confused about unix vs linux? Refer to the full family tree and these more precise definitions from Wikipedia:
unix: a family of multitasking, multiuser computer operating systems that derive from the original AT&T Unix, developed in the 1970s at the Bell Labs research center by Ken Thompson, Dennis Ritchie, and others
linux: a Unix-like and mostly POSIX-compliant computer operating system assembled under the model of free and open-source software development and distribution [whose] defining component ... is the Linux kernel, an operating system kernel first released [in] 1991 by Linus Torvalds ↑

## 100 Useful Unix Commands
This article is an introduction to unix. It aims to teach the basic principles and neglects to mention many of the utilities that give unix superpowers. To learn about those, see 100 Useful Unix Commands.

## Getting Started: Opening the Terminal
If you have a Mac, navigate to Applications > Utilities and open the application named "Terminal":
image
If you have a PC, abandon all hope, ye who enter here! Just kidding—partially. None of the native Windows shells, such as cmd.exe or PowerShell, are unix-like. Instead, they're marked with hideous deformities that betray their ignoble origin as grandchildren of the MS-DOS command interpreter. If you didn't have a compelling reason until now to quit using PCs, here you are [1]. Typically, my misguided PC friends don't use the command line on their local machines; instead, they have to ssh into some remote server running Linux. (You can do this with an ssh client like PuTTY, Chrome's Terminal Emulator, or MobaXterm, but don't ask me how.) On Macintosh you can start practicing on the command line right away without having to install a Linux distribution [2] (the Mac-flavored unix is called Darwin).

For both Mac and PC users who want a bona fide Linux command line, one easy way to get it is in the cloud with Amazon EC2 via the AWS Free Tier. If you want to go whole hog, you can download and install a Linux distribution—Ubuntu, Mint, Fedora, and CentOs are popular choices—but this is asking a lot of non-hardcore-nerds (less drastically, you could boot Linux off of a USB drive or run it in a virtual box).


[1] I should admit, you can and should get around this by downloading something like Cygwin, whose homepage states: "Get that Linux feeling - on Windows" ↑
[2] However, if you're using Mac OS rather than Linux, note that OS does not come with the GNU coreutils, which are the gold standard. You should download them ↑

## The Definitive Guides to Unix, Bash, and the Coreutils
Before going any further, it's only fair to plug the authoritative guides which, unsurprisingly, can be found right on your command line:

$ man bash
$ info coreutils

(The $ at the beginning of the line represents the terminal's prompt.) These are good references, but overwhelming to serve as a starting point. There are also great resources online:

    The Linux Information Project
    GNU Bash Reference Manual
    The Linux Documentation Project
    SS64 | Command line reference
    Stack Overflow
    Wikipedia

although these guides, too, are exponentially more useful once you have a small foundation to build on.

## The Unix Filestructure
All the files and directories (a fancy word for "folder") on your computer are stored in a hierarchical tree. Picture a tree in your backyard upside-down, so the trunk is on the top. If you proceed downward, you get to big branches, which then give way to smaller branches, and so on. The trunk contains everything in the sense that everything is connected to it. This is the way it looks on the computer, too, and the trunk is called the root directory. In unix it's represented with a slash:
/
The root contains directories, which contain other directories, and so on, just like our tree. To get to any particular file or directory, we need to specify the path, which is a slash-delimited address:
/dir1/dir2/dir3/some_file
Note that a full path always starts with the root, because the root contains everything. As we'll see below, this won't necessarily be the case if we specify the address in a relative way, with respect to our current location in the filesystem.

Let's examine the directory structure on our Macintosh. We'll go to the root directory and look down just one level with the unix command tree. (If we tried to look at the whole thing, we'd print out every file and directory on our computer!) We have:

image

While we're at it, let's also look at the directory /Users/username, which is the specially designated home directory on the Macintosh:

image

One thing we notice right away is that the Desktop, which holds such a revered spot in the GUI, is just another directory—simply the first one we see when we turn on our computer.

If you're on Linux rather than Mac OS, the directory tree might look less like the screenshot above and more like this:

image

The naming of these folders is not intuitive, but you can read about the role of each one here. I've arbitrarily traced out the path to /var/log, a location where some programs store their log files.

If the syntax of a unix path looks familiar, it is. A webpage's URL, with its telltale forward slashes, looks like a unix path with a domain prepended to it. This is not a coincidence! For a simple static website, its structure on the web is determined by its underlying directory structure on the server, so navigating to:
http://www.example.com/abc/xyz
will serve you content in the folder websitepath/abc/xyz on the host's computer (i.e., the one owned by example.com). Modern dynamic websites are more sophisticated than this, but it's neat to reflect that the whole word has learned this unix syntax without knowing it.

To learn more, see the O'Reilly discussion of the unix file structure.

## The Great Trailing Slash Debate
Sometimes you'll see directories written with a trailing slash, as in:
dir1/
This helpfully reminds you that the entity is a directory rather than a file, but on the command line using the more compact dir1 is sufficient. There are a handful of unix commands which behave slightly differently if you leave the trailing slash on, but this sort of extreme pedantry isn't worth worrying about.

## Where Are You? - Your Path and How to Navigate through the Filesystem
When you open up the terminal to browse through your filesystem, run a program, or do anything, you're always somewhere. Where? You start out in the designated home directory when you open up the terminal. The home directory's path is preset by a global variable called HOME. Again, it's /Users/username on a Mac.

As we navigate through the filesystem, there are some conventions. The current working directory (cwd)—whatever directory we happen to be in at the moment—is specified by a dot:
.
Sometimes it's convenient to write this as:
./
which is not to be confused with the root directory:
/
When a program is run in the cwd, you often see the syntax:

$ ./myprogram

which emphasizes that you're executing a program from the current directory. The directory one above the cwd is specified by two dots:
..
With the trailing slash syntax, that's:
../
A tilde is shorthand for the home directory:
~
or:
~/
To see where we are, we can print working directory:

$ pwd

To move around, we can change directory:

$ cd /some/path

By convention, if we leave off the argument and just type:

$ cd

we will go home. To make directory—i.e., create a new folder—we use:

$ mkdir

As an example, suppose we're in our home directory, /Users/username, and want to get one back to /Users. We can do this two ways:

$ cd /Users

or:

$ cd ..

This illustrates the difference between an absolute path and a relative path. In the former case, we specify the complete address, while in the later we give the address with respect to our cwd. We could even accomplish this with:

$ cd /Users/username/..

or maniacally seesawing back and forth:

$ cd /Users/username/../username/..

if our primary goal were obfuscation. This distinction between the two ways to specify a path may seem pedantic, but it's not. Many scripting errors are caused by programs expecting an absolute path and receiving a relative one instead or vice versa. Use relative paths if you can because they're more portable: if the whole directory structure gets moved, they'll still work.

Let's mess around. We know cd with no arguments takes us home, so try the following experiment:

$ echo $HOME      # print the variable HOME
/Users/username
$ cd              # cd is equivalent to cd $HOME
$ pwd             # print working directory shows us where we are
/Users/username

$ unset HOME      # unset HOME erases its value
$ echo $HOME

$ cd /some/path   # cd into /some/path
$ cd              # take us HOME?
$ pwd
/some/path

What happened? We stayed in /some/path rather than returning to /Users/username. The point? There's nothing magical about home—it's merely set by the variable HOME. More about variables soon!

## Gently Wading In - The Top 10 Indispensable Unix Commands
Now that we've dipped one toe into the water, let's make a list of the 10 most important unix commands in the universe:

    pwd
    ls
    cd
    mkdir
    echo
    cat
    cp
    mv
    rm
    man

Every command has a help or manual page, which can be summoned by typing man. To see more information about pwd, for example, we enter:

$ man pwd

But pwd isn't particularly interesting and its man page is barely worth reading. A better example is afforded by one of the most fundamental commands of all, ls, which lists the contents of the cwd or of whatever directories we give it as arguments:

$ man ls

The man pages tend to give TMI (too much information) but the most important point is that commands have flags which usually come in a one-dash-one-letter or two-dashes-one-word flavor:

command -f
command --flag

and the docs will tell us what each option does. You can even try:

$ man man

However, as the old unix joke goes, this won't work:

$ man woman
No manual entry for woman

Below we'll discuss the commands in the top 10 list in more depth.

## ls
Let's go HOME and try out ls with various flags:

$ cd
$ ls
$ ls -1
$ ls -hl
$ ls -al

Some screen shots:

image

image

First, vanilla ls. We see our files—no surprises. And ls -1 merely displays our files in a column. To show the human-readable, long form we stack the -h and -l flags:
ls -hl
This is equivalent to:
ls -h -l
Screenshot:

image

This lists the owner of the file; the group to which he belongs (staff); the date the file was created; and the file size in human-readable form, which means bytes will be rounded to kilobytes, gigabytes, etc. The column on the left shows permissions. If you'll indulge mild hyperbole, this simple command is already revealing secrets that are well-hidden by the GUI and known only to unix users. In unix there are three spheres of permission—user, group, and other/world—as well as three particular types for each sphere—read, write, and execute. Everyone with an account on the computer is a unique user and, although you may not realize it, can be part of various groups, such as a particular lab within a university or team in a company. To see yourself and what groups you belong to, try:

$ whoami
$ groups

A string of dashes displays permission:

---------
rwx------
rwxrwx---
rwxrwxrwx

This means, respectively: no permission for anybody; read, write, execute permission for only the user; rwx permission for the user and anyone in the group; and rwx permission for the user, group, and everybody else. Permission is especially important in a shared computing environment. You should internalize now that two of the most common errors in computing stem from the two P words we've already learned: paths and permissions. The command chmod, which we'll learn later, governs permission.

If you look at the screenshot above, you see a tenth letter prepended to the permission string, e.g.:

drwxrwxrwx

This has nothing to do with permissions and instead tells you about the type of entity in the directory: d stands for directory, l stands for symbolic link, and a plain dash denotes a file.

The -a option in:
ls -al
lists all files in the directory, including dotfiles. These are files that begin with a dot and are hidden in the GUI. They're often system files—more about them later. Screenshot:

image

Note that, in contrast to ls -hl, the file sizes are in pure bytes, which makes them a little hard to read.

A general point about unix commands: they're often robust. For example, with ls you can use an arbitrary number of arguments and it obeys the convention that an asterisk matches anything (this is known as file globbing, and I think of it as the prequel to regular expressions). Take:

$ ls . dir1 .. dir2/*.txt dir3/A*.html

This monstrosity would list anything in the cwd; anything in directory dir1; anything in the directory one above us; anything in directory dir2 that ends with .txt; and anything in directory dir3 that starts with A and ends with .html. You get the point.

Suppose I create some nested directories:

$ mkdir -p squirrel/mouse/fox

(The -p flag is required to make nested directories in a single shot) The directory fox is empty, but if I ask you to list its contents for the sake of argument, how would you do it? Beginners often do it like this:

$ cd squirrel
$ cd mouse
$ cd fox
$ ls

But this takes forever. Instead, list the contents from the current working directory, and—crucially—use bash autocompletion, a huge time saver. To use autocomplete, hit the tab key after you type ls. Bash will show you the directories available (if there are many possible directories, start typing the name, sq..., before you hit tab). In short, do it like this:

$ ls squirrel/mouse/fox/ # use autocomplete to form this path quickly

## Single Line Comments in Unix
Anything prefaced with a # —that's pound-space—is a comment and will not be executed:

$ # This is a comment.
$ # If we put the pound sign in front of a command, it won't do anything:
$ # ls -hl

Suppose you write a line of code on the command line and decided you don't want to execute it. You have two choices. The first is pressing Cntrl-c, which serves as an "abort mission." The second is jumping to the beginning of the line (Cntrl-a) and adding the pound character. This has an advantage over the first method that the line will be saved in bash history (discussed below) and can thus be retrieved and modified later.

In a script, pound-special-character (like #!) is sometimes interpreted (see below), so take note and include a space after # to be safe.

##The Primacy of Text Files, Text Editors
As we get deeper into unix, we'll frequently be using text editors to edit code, and viewing either data or code in text files. When I got my hands on a computer as a child, I remember text editors seemed like the most boring programs in the world (compared to, say, 1992 Prince of Persia). And text files were on the bottom of my food chain. But the years have changed me and now I like nothing better than a clean, unformatted .txt file. It's all you need! If you store your data, your code, your correspondence, your book, or almost anything in .txt files with a systematic structure, they can be parsed on the command line to reveal information from many facets. Here's some advice: do all of your text-related work in a good text editor. Open up clunky Microsoft Word, and you've unwittingly spoken a demonic incantation and summoned the beast. Are these the words of a lone lunatic dispensing hateration? No, because on the command line you can count the words in a text file, search it with grep, input it into a Python program, et cetera. However, a file in Microsoft Word's proprietary and unknown formatting is utterly unusable.

Because text editors are extremely important, some people develop deep relationships with them. My co-worker, who is a Vim aficionado, turned to me not long ago and said, "You know how you should think about editing in Vim? As if you're talking to it." On the terminal, a ubiquitous and simple editor is nano. If you're more advanced, try Vim or Emacs. Not immune to my co-worker's proselytizing, I've converted to Vim. Although it's sprawling and the learning curve can be harsh—Vim is like a programming language in itself—you can do a zillion things with it. There's a section on Vim near the end of this article.

On the GUI, there are many choices: Sublime, Aquamacs, Smultron, etc. I used to use Smultron until I found, unforgivably, that the spacing of documents when you looked at them in the editor and on the terminal was different. I hear good things about Sublime and Aquamacs.

Exercise: Let's try making a text file with nano. Type:

$ nano file.txt

and make the following three-row two-column file:

1	x
4	b
z	9

(It's Cntrl-o to save and Cntrl-x to exit.)

## echo and cat
More essential commands: echo prints the string passed to it as an argument, while cat prints the contents of files passed to it as arguments. For example:

$ echo joe
$ echo "joe"

would both print joe, while:

$ cat file.txt

would print the contents of file.txt. Entering:

$ cat file.txt file2.txt

would print out the contents of both file.txt and file2.txt concatenated together, which is where this command gets its slightly confusing name.

Finally, a couple of nice flags for these commands:

$ echo -n "joe"            # suppress newline
$ echo -e "joe\tjoe\njoe"  # interpret special chars ( \t is tab, \n newline )
$ cat -n file.txt          # print file with line numbers


## cp, mv, and rm
Finishing off our top 10 list we have cp, mv, and rm. The command to make a copy of a file is cp:

$ cp file1 file2
$ cp -R dir1 dir2

The first line would make an identical copy of file1 named file2, while the second would do the same thing for directories. Notice that for directories we use the -R flag (for recursive). The directory and everything inside it are copied.

Question: what would the following do?

$ cp -R dir1 ../../

Answer: it would make a copy of dir1 up two levels from our current working directory.

To rename a file or directory we use mv:

$ mv file1 file2

In a sense, this command also moves files, because we can rename a file into a different path. For example:

$ mv file1 dir1/dir2/file2

would move file1 into dir1/dir2/ and change its name to file2, while:

$ mv file1 dir1/dir2/

would simply move file1 into dir1/dir2/ or, if you like, rename ./file1 as ./dir1/dir2/file1.

Finally, rm removes a file or directory:

$ rm file     # removes a file
$ rm -r dir   # removes a file or directory
$ rm -rf dir  # force removal of a file or directory
	      # (i.e., ignore warnings)

## Variables in Unix
To declare something as a variable use an equals sign, with no spaces. Let's declare a to be a variable:

$ a=3    # This syntax is right (no whitespace)
$ a = 3  # This syntax is wrong (whitespace)
-bash: a: command not found

Once we've declared something as a variable, we need to use $ to access its value (and to let bash know it's a variable). For example:

$ a=3
$ echo a
a
$ echo $a
3

So, with no $ sign, bash thinks we just want to echo the string a. With a $ sign, however, it knows we want to access what the variable a is storing, which is the value 3. Variables in unix are loosely-typed, meaning you don't have to declare something as a string or an integer.

$ a=3          # a can be an integer
$ echo $a
3

$ a=joe	       # or a can be a string
$ echo $a
joe

$ a="joe joe"  # Use quotes if you want a string with spaces
$ echo $a
joe joe

We can declare and echo two variables at the same time, and generally play fast and loose, as we're used to doing on the command line:

$ a=3; b=4
$ echo $a $b
3 4
$ echo $a$b         # mesh variables together as you like
34
$ echo "$a$b"       # use quotes if you like
34
$ echo -e "$a\t$b"  # the -e flag tells echo to interpret \t as a tab
3	4

You should also be aware of how bash treats double vs single quotes. As we've seen, if you want to use a string with spaces, you use double quotes. If you use double quotes, any variable inside them will be expanded, the same as in Perl. If you use single quotes, everything is taken literally and variables are not expanded. Here's an example:

$ var=5
$ joe=hello $var
-bash: 5: command not found

$ joe="hello $var"
$ echo $joe
hello 5

$ joe='hello $var'
$ echo $joe
hello $var

An important note is that often we use variables to store paths in unix. Once we do this, we can use all of our familiar directory commands on the variable:

$ d=dir1/dir2/dir3
$ ls $d
$ cd $d

$ d=..      # this variable stores the directory one above us (relative path)
$ cd $d/..  # cd two directories up

## Escape Sequences
Escape sequences are important in every language. When bash reads $a it interprets it as whatever's stored in the variable a. What if we actually want to echo the string $a? To do this, we use \ as an escape character:

$ a=3
$ echo $a
3
$ echo \$a
$a
$ echo "\$a"  # use quotes if you like
$a

What if we want to echo the slash, too? Then we have to escape the escape character (using the escape character!):

$ echo \\\$a  # escape the slash and the dollar sign
\$a

This really comes down to parsing. The slash helps bash figure out if your text is a plain old string or a variable. It goes without saying that you should avoid special characters in your variable names. In unix we might occasionally fall into a parsing tar-pit trap. To avoid this, and make extra sure bash parses our variable right, we can use the syntax ${a} as in:

$ echo ${a}
3

When could this possibly be an issue? Later, when we discuss scripting, we'll learn that $n, where n is a number, is the nth argument to our script. If you were crazy enough to write a script with 11 arguments, you'd discover that bash interprets a=$11 as a=$1 (the first argument) concatenated with the string 1 while a=${11} properly represents the eleventh argument. This is getting in the weeds, but FYI.

Here's a more practical example:

$ a=3
$ echo $a		# variable a equals 3
3
$ echo $apple		# variable apple is not set

$ echo ${a}pple		# this describes the variable a plus the string "pple"
3pple


## Global Variables in Unix
In general, it is the convention to use capital letters for global variables. We've already learned about one: HOME. We can see all the variables set in our shell by simply typing:

$ set

Some basic variables deserve comment:

    HOME
    PS1
    TMPDIR
    EDITOR
    DISPLAY

HOME, as we've already seen, is the path to our home directory (preset to /Users/username on Macintosh). PS1 sets the shell's prompt. For example:

$ PS1=':-) '

changes our prompt from a dollar-sign into an emoticon, as in:

image

This is amusing, but the PS1 variable is actually important for orienting you on the command line. A good prompt is a descriptive one: it tells you what directory you're in and perhaps your username and the name of the computer. The default prompt should do this but, in case you want to nerd out, you can read about the arcane language required to customize PS1 here. (If you're familiar with git, you can even have your prompt display the branch of the git repository you're on).

On your computer there is a designated temporary directory and its path is stored in TMPDIR. Some commands, such as sort, which we'll learn later, surreptitiously make use of this directory to store intermediate files. At work, we have a shared computer system and occasionally this common directory $TMPDIR will run out of space, causing programs trying to write there to fail. One solution is to simply set TMPDIR to a different path where there's free space. EDITOR sets the default text editor (you can invoke it by pressing Cntrl-x-e). And DISPLAY is a variable related to the X Window System.

Many programs rely on their own agreed-upon global variables. For example, if you're a Perl user, you may know that Perl looks for modules in the directory whose path is stored in PERL5LIB. Python looks for its modules in PYTHONPATH; R looks for packages in R_LIBS; Matlab uses MATLABPATH; awk uses AWKPATH; C++ looks for libraries in LD_LIBRARY_PATH; and so on. These variables don't exist in the shell by default. A program will make a system call and look for the variable. If the user has had the need or foresight to define it, the program can make use of it.


## The PATH
The most important global variable of all is the PATH. This is the PATH, as distinct from a path, a term we've already learned referring to a location in the filesystem. The PATH is a colon-delimited list of directories where unix will look for executable programs when you enter something on command line. If your program is in one of these directories, you can run it from any location by simply entering its name. If the program is not in one of these directories, you can still run it, of course, but you'll have to include its path.

Let's revisit the idea of a command in unix. What's a command? It's nothing more than a program sitting in a directory somewhere. So, if ls is a program [1], where is it? Use the command which to see its path:

$ which ls  # on my work computer
/bin/ls

$ which ls  # on my home Mac
/usr/local/Cellar/coreutils/8.20/libexec/gnubin/ls

For the sake of argument, let's say I download an updated version of the ls command, and then type ls in my terminal. What will happen—will the old ls or the new ls execute? The PATH comes into play here because it also determines priority. When you enter a command, unix will look for it in each directory of the PATH, from first to last, and execute the first instance it finds. For example, if:
PATH=/bin/dir1:/bin/dir2:/bin/dir3
and there's a command named ls in both /bin/dir1 and /bin/dir2, the one in /bin/dir1 will be executed.

Let's see what your PATH looks like. Enter:

$ echo $PATH

For example, here's a screenshot of the default PATH on Ubuntu:

image

To emphasize the point again, all the programs in the directories specified by your PATH are all the programs that you can access on the command line by simply typing their names.

The PATH is not immutable. You can set it to be anything you want, but in practice you'll want to augment, rather than overwrite, it. By default, it contains directories where unix expects executables, like:

    /bin
    /usr/bin
    /usr/local/bin

Let's say you have just written the command /mydir/newcommand. If you're not going to use the command very often, you can invoke it using its full path every time you need it:

$ /mydir/newcommand

However, if you're going to be using it frequently, you can just add /mydir to the PATH and then invoke the command by name:

$ PATH=/mydir:$PATH  # add /mydir to the front of PATH - highest priority
$ PATH=$PATH:/mydir  # add /mydir to the back of PATH - lowest priority
$ newcommand         # now invoking newcommand is this easy

This is a frequent chore in unix. If you download some new program, you will often find yourself updating the PATH to include the directory containing its binaries. How can we avoid having to do this every time we open the terminal for a new session? We'll discuss this below when we learn about .bashrc.

If you want to shoot yourself in the foot, you can vaporize the PATH:

$ unset PATH  # not advisable
$ ls          # now ls is not found
-bash: ls: No such file or directory

but this is not advisable, save as a one-time educational experience.


[1] In fact, if you want to view the source code (written in the C programming language) of ls and other members of the coreutils, you can download it at ftp.gnu.org/gnu/coreutils. E.g., get and untar the latest version as of this writing:

$ wget ftp://ftp.gnu.org/gnu/coreutils/coreutils-8.9.tar.xz
$ tar -xvf coreutils-8.9.tar.xz

or use git:

$ git clone git://git.sv.gnu.org/coreutils

↑


## Links
While we're on the general subject of paths, let's talk about symbolic links. If you've ever used the Make Alias command on a Macintosh (not to be confused with the unix command alias, discussed below), you've already developed intuition for what a link is. Suppose you have a file in one folder and you want that file to exist in another folder simultaneously. You could copy the file, but that would be wasteful. Moreover, if the file changes, you'll have to re-copy it—a huge ball-ache. Links solve this problem. A link to a file is a stand-in for the original file, often used to access the original file from an alternate file path. It's not a copy of the file but, rather, points to the file.

To make a symbolic link, use the command ln:

$ ln -s /path/to/target/file mylink

This produces:

mylink --> /path/to/target/file

in the cwd, as ls -hl will show. Note that removing mylink:

$ rm mylink

does not affect our original file.

If we give the target (or source) path as the sole argument to ln, the name of the link will be the same as the source file's. So:

$ ln -s /path/to/target/file

produces:

file --> /path/to/target/file

Links are incredibly useful for all sorts of reasons—the primary one being, as we've already remarked, if you want a file to exist in multiple locations without having to make extraneous, space-consuming copies. You can make links to directories as well as files. Suppose you add a directory to your PATH that has a particular version of a program in it. If you install a newer version, you'll need to change the PATH to include the new directory. However, if you add a link to your PATH and keep the link always pointing to the most up-to-date directory, you won't need to keep fiddling with your PATH. The scenario could look like this:

$ ls -hl myprogram
current -> version3
version1
version2
version3

(where I'm hiding some of the output in the long listing format.) In contrast to our other examples, the link is in the same directory as the target. Its purpose is to tell us which version, among the many crowding a directory, we should use.

Another good practice is putting links in your home directory to folders you often use. This way, navigating to those folders is easy when you log in. If you make the link:

~/MYLINK --> /some/long/and/complicated/path/to/an/often/used/directory

then you need only type:

$ cd MYLINK

rather than:

$ cd /some/long/and/complicated/path/to/an/often/used/directory

Links are everywhere, so be glad you've made their acquaintance!


## What is Scripting?
By this point, you should be comfortable using basic utilities like echo, cat, mkdir, cd, and ls. Let's enter a series of commands, creating a directory with an empty file inside it, for no particular reason:

$ mkdir tmp
$ cd tmp
$ pwd
/Users/oliver/tmp
$ touch myfile.txt  # the command touch creates an empty file
$ ls
myfile.txt
$ ls myfile_2.txt  # purposely execute a command we know will fail
ls: cannot access myfile_2.txt: No such file or directory

What if we want to repeat the exact same sequence of commands 5 minutes later? Massive bombshell—we can save all of these commands in a file! And then run them whenever we like! Try this:

$ nano myscript.sh

and write the following:

# a first script
mkdir tmp
cd tmp
pwd
touch myfile.txt
ls
ls myfile_2.txt

Gratuitous screenshot:

image

This file is called a script (.sh is a typical suffix for a shell script), and writing it constitutes our first step into the land of bona fide computer programming. In general usage, a script refers to a small program used to perform a niche task. What we've written is a recipe that says:

    create a directory called "tmp"
    go into that directory
    print our current path in the file system
    make a new file called "myfile.txt"
    list the contents of the directory we're in
    specifically list the file "myfile_2.txt" (which doesn't exist)

This script, though silly and useless, teaches us the fundamental fact that all computer programs are ultimately just lists of commands.

Let's run our program! Try:

$ ./myscript.sh
-bash: ./myscript.sh: Permission denied

WTF! It's dysfunctional. What's going on here is that the file permissions are not set properly. In unix, when you create a file, the default permission is not executable. You can think of this as a brake that's been engaged and must be released before we can go (and do something potentially dangerous). First, let's look at the file permissions:

$ ls -hl myscript.sh
-rw-r--r-- 1 oliver staff 75 Oct 12 11:43 myscript.sh

Let's change the permissions with the command chmod and execute the script:

$ chmod u+x myscript.sh  # add executable(x) permission for the user(u) only
$ ls -hl myscript.sh
-rwxr--r-- 1 oliver staff 75 Oct 12 11:43 myscript.sh

$ ./myscript.sh
/Users/oliver/tmp/tmp
myfile.txt
ls: cannot access myfile_2.txt: No such file or directory

Not bad. Did it work? Yes, it did because it's printed stuff out and we see it's created tmp/myfile.txt:

$ ls
myfile.txt  myscript.sh  tmp
$ ls tmp
myfile.txt

An important note is that even though there was a cd in our script, if we type:

$ pwd
/Users/oliver/tmp

we see that we're still in the same directory as we were in when we ran the script. Even though the script entered /Users/oliver/tmp/tmp, and did its bidding, we stay in /Users/oliver/tmp. Scripts always work this way—where they go is independent of where we go.

If you're wondering why anyone would write such a pointless script, you're right—it would be odd if we had occasion to repeat this combination of commands. There are some more realistic examples of scripting below.


## File Suffixes in Unix
As we begin to script it's worth following some file naming conventions. We should use common sense suffixes, like:

    .txt - for text files
    .html - for html files
    .sh - for shell scripts
    .pl - for Perl scripts
    .py - for Python scripts
    .cpp - for c++ code

and so on. Adhering to this organizational practice will enable us to quickly scan our files, and make searching for particular file types easier [1]. As we saw above, commands like ls and find are particularly well-suited to use this kind of information. For example, list all text files in the cwd:

$ ls *.txt

List all text files in the cwd and below (i.e., including child directories):

$ find . -name "*.txt"



[1] An astute reader noted that, for commands—as opposed to, say, html or text files—using suffixes is not the best practice because it violates the principle of encapsulation. The argument is that a user is neither supposed to know nor care about a program's internal implementation details, which the suffix advertises. You can imagine a program that starts out as a shell script called mycommand.sh, is upgraded to Python as mycommand.py, and then is rewritten in C for speed, becoming the binary mycommand. What if other programs depend on mycommand? Then each time mycommand's suffix changes they have to be rewritten—an annoyance. Although I make this sloppy mistake in this article, that doesn't excuse you! Read the full argument

Update: There's a subtlety inherent in this argument that I didn't appreciate the first time around. I'm going to jump ahead of the narrative here, so you may want to skip this for now and revist it later. Suppose you have two identical Python scripts. One is called hello.py and one is simply called hi. Both contain the following code:

#!/usr/bin/env python

def yo():
    print('hello')

In the Python shell, this works:

>>> import hello

but this doesn't:

>>> import hi
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
ImportError: No module named hi

Being able to import scripts in Python is important for all kinds of things, such as making modules, but you can only import something with a .py extension. So how do you get around this if you're not supposed to use file extensions? The sage answers this question as follows:

    The best way to handle this revolves around the core question of whether the file should be a command or a library. Libraries have to have the extension, and commands should not, so making a tiny command wrapper that handles parsing options and then calls the API from the other, imported one is correct.

To elaborate, this considers a command to be something in your PATH, while a library—which could be a runnable script—is not. So, in this example, hello.py would stay the same, as a library not in your PATH:

#!/usr/bin/env python

def yo():
    print('hello')

hi, a command in your PATH, would look like this:

#!/usr/bin/env python

import hello

hello.yo()

Hat tip: Alex
↑


## The Shebang
We've left out one important detail about scripting. How does unix know we want to run a bash script, as opposed to, say, a Perl or Python script? There are two ways to do it. We'll illustrate with two simple scripts, a bash script and a Perl script:

$ cat myscript_1.sh  # a bash script
echo "hello kitty"

$ cat myscript_1.pl  # a Perl script
print "hello kitty\n";

The first way to tell unix which program to use to interpret the script is simply to say so on the command line. For example, we can use bash to execute bash scripts:

$ bash ./myscript_1.sh	# use bash for bash scripts
hello kitty

and perl for Perl scripts:

$ perl ./myscript_1.pl   # use Perl for Perl scripts
hello kitty

But this won't work for a Perl script:

$ ./myscript_1.pl        # this won't work
./myscript_1.pl: line 1: print: command not found

And if we purposefully specify the wrong language, we'll get errors:

$ bash ./myscript_1.pl   # let's purposefully do it backwards
./myscript_1.pl: line 1: print: command not found

$ perl ./myscript_1.sh
String found where operator expected at ./myscript_1.sh line 1,
near "echo "hello kitty""
	(Do you need to predeclare echo?)
syntax error at ./myscript_1.sh line 1, near "echo "hello kitty""
Execution of ./myscript_1.sh aborted due to compilation errors.

The second way to specify the proper interpreter—and the better way, which you should emulate—is to put it in the script itself using a shebang. To do this, let's remind ourselves where bash and perl reside on our system. On my computer, they're here:

$ which perl
/usr/bin/perl

$ which bash
/bin/bash

although perl could be somewhere else on your machine (bash should be in /bin by convention). The shebang specifies the language in which your script is interpreted according to the syntax #! followed by the path to the language. It should be the first line of your script. Note that it's not a comment even though it looks like one. Let's add shebangs to our two scripts:

$ cat myscript_1.sh
#!/bin/bash
echo "hello kitty"

$ cat myscript_1.pl
#!/usr/bin/perl
print "hello kitty\n";

Now we can run them without specifying the interpreter in front:

$ ./myscript_1.sh
hello kitty
$ ./myscript_1.pl
hello kitty

However, there's still a lingering issue and it has to do with portability, an important software principle. What if perl is in a different place on your machine than mine and you copy my scripts and try to run them? The path will be wrong and they won't work. The solution to this issue is courtesy of a neat trick using env. We can amend our script to be:

$ cat myscript_1.pl
#!/usr/bin/env perl
print "hello kitty\n";

Of course, this assumes you have a copy of env in /usr/bin, but this is usually a correct assumption. What env does here is to use whatever your environmental variable for perl is—i.e., the perl that's first in your PATH.

This is a useful practice even if you're not sharing scripts. Suppose you've updated your version of perl and there's a newer copy than /usr/bin/perl. You've appropriately updated your PATH such that the directory containing the updated perl comes before /usr/bin. If you have env in your shebang, you're all set. However, if you've hardwired the old path in your shebang, your script will run on the old perl [1].

The question that the shebang resolves—which program will run your script?—reminds us of a more fundamental distinction between interpreted languages and compiled languages. The former are those like bash, Perl, and Python, where you can cat a script and look inside it. The later, like C++, require compilation, the process whereby code is translated into machine language (the result is sometimes called a binary). This can be done with a command line utility like g++:

$ g++ MyProgram.cpp -o MyProgram

Compiled programs, such as the unix utilities themselves, tend to run faster. Don't try to cat a binary, such as ls, or it will spew out gibberish:

$ cat $( which ls )  # don't do this!



[1] Of course, depending on circumstances, you may very well want to stick with the old version of Perl or whatever's running your program. An update can have unforeseen consequences and this is the motivation for tools like virtualenv (Python), whose docs remind us: "If an application works, any change in its libraries or the versions of those libraries can break the application" ↑


## bash
We've thrown around the term bash a few times but we haven't defined it. To do so, let's examine the special command, sh, which is more primitive than bash and came before it. To quote Wikipedia and the manual page:

    The Bourne shell (sh) is a shell, or command-line interpreter, for computer operating systems. The shell is a command that reads lines from either a file or the terminal, interprets them, and generally executes other commands. It is the program that is running when a user logs into the system ... Commands can be typed directly to the running shell or can be put into a file and the file can be executed directly by the shell

As it describes, sh is special because it's both a command interpreter and a command itself (usually found at /bin/sh). Put differently, you can run myscript as:

$ sh ./myscript

or you can simply type:

$ sh

to start an interactive sh shell. If you're in this shell and run:

$ ./myscript

without specifying an interpreter or using a shebang, your script will be interpreted by sh by default. On most computers, however, the default shell is no longer sh but bash (usually located at /bin/bash). To mash up Wikipedia and the manual page:

    The Bourne-Again SHell (bash) a Unix shell written by Brian Fox for the GNU Project as a free software replacement for the Bourne shell. bash is an sh-compatible command language interpreter that executes commands read from the standard input or from a file ... There are some subtle differences between bash and traditional versions of sh

Like sh, bash is a command you can either invoke on a script or use to start an interactive bash shell. Read more on Stackoverflow: Difference between sh and bash.

Which shell are you using right now? Almost certainly bash, but if you want to double check, there's a neat command given here to display your shell type:

$ ps -p $$

There are more exotic shells, like Z shell and tcsh, but they're beyond the scope of this article.


## chmod
Let's take a closer look at how to use chmod. Remember the three domains:

    u - user
    g - group
    o - other/world

and the three types of permission:

    r - read
    w - write
    x - execute

we can mix and match these how we like, using a plus sign to grant permissions according to the syntax:
chmod entity+permissiontype
or a minus sign to remove permissions:
chmod entity-permissiontype
E.g.:

$ chmod u+x myfile     # make executable for you
$ chmod g+rxw myfile   # add read write execute permissions for the group
$ chmod go-wx myfile   # remove write execute permissions for the group
                       # and for everyone else (excluding you, the user)

You can also use a for "all of the above", as in:

$ chmod a-rwx myfile   # remove all permissions for you, the group,
		       # and the rest of the world

If you find the above syntax cumbersome, there's a numerical shorthand you can use with chmod. The only two I have memorized are 777 and 755:

$ chmod 777 myfile     # grant all permissions (rwxrwxrwx)
$ chmod 755 myfile     # reserve write access for the user,
                       # but grant all other permissions (rwxr-xr-x)

Read more about the numeric code here. In general, it's a good practice to allow your files to be writable by you alone, unless you have a compelling reason to share access to them.


## ssh
In addition to chmod, there's another command it would be remiss not to mention. For many people, the first time they need to go to the command line, rather than the GUI, is to use the Secure Shell (ssh) protocol. Suppose you want to use a computer, but it's not the computer that's in front of you. It's a different computer in some other location—say, at your university, your company, or on the Amazon cloud. ssh is the command that allows you to log into a computer remotely over the network. Once you've sshed into a computer, you're in its shell and can run commands on it just as if it were your personal laptop. To ssh, you need to know the address of the host computer you want to log into, your user name on that computer, and the password [1]. The basic syntax is:
ssh username@host
For example:

$ ssh username@myhost.university.edu

If you're trying to ssh into a private computer and don't know the hostname, use its IP address (username@IP-address).

ssh also allows you to run a command on the remote server without logging in. For instance, to list of the contents of your remote computer's home directory, you could run:

$ ssh username@myhost.university.edu "ls -hl"

Cool, eh? Moreover, if you have ssh access to a machine, you can copy files to or from it with the utility rsync—a great way to move data without an external hard drive.

The file:
~/.ssh/config
determines ssh's behavior and you can create it if it doesn't exist (the dot in the name .ssh confers invisibility—see the discussion about dotfiles below). On your own private computer, you can ssh into selected servers without having to type in a password by updating this configuration file. To do this, generate rsa ssh keys:

$ mkdir -p ~/.ssh
$ cd ~/.ssh
$ ssh-keygen -t rsa -f localkey

This will create two files on your computer, a public key:
~/.ssh/localkey.pub
and a private key:
~/.ssh/localkey
You can share your public key, but do not give anyone your private key! Suppose you want to ssh into myserver.com. Normally, that's:

$ ssh myusername@myserver.com

Instead of doing this, add these lines to your ~/.ssh/config file:

Host Myserver
    HostName myserver.com
    User myusername
    IdentityFile ~/.ssh/localkey

Next, cat your public key and paste it into:
~/.ssh/authorized_keys
on the remote machine (i.e., the myserver.com computer). Now on your local computer, you can ssh into myserver.com without a password:

$ ssh Myserver

You can also use this technique to push to github.com [2], without having to punch your password in each time, by pasting your public key into:
Settings > SSH Keys > Add SSH Key
on GitHub (read the official tutorial).

If this is your first encounter with ssh, you'd be surprised how much of the work of the world is done by ssh. It's worth reading the extensive man page, which gets into matters of computer security and cryptography.


[1] The host also has to enable ssh access. On Macintosh, for example, it's disabled by default, but you can turn it on, as instructed here. For Ubuntu, check out the official docs. ↑
[2] As you get deeper into the game, tracking your scripts and keeping a single, stable version of them becomes crucial. Git, a vast subject for another tutorial, is the neat solution to this problem and the industry standard for version control. On the web GitHub provides free hosting of script repositories and connects to the command line via the git interface ↑


## Saving to a File; Stdout and Stderr
To save to a file in unix, use an angle bracket:

$ echo joe > junk.txt  # save to file
$ cat junk.txt
joe

To append to the end of a pre-existing file, use a double angle bracket:

$ echo joe >> junk.txt  # append to already-existing file
$ cat junk.txt
joe
joe

Returning to our first script, myscript.sh, let's save the output to a file:

$ ./myscript.sh > out.txt
mkdir: cannot create directory ‘tmp’: File exists
ls: cannot access myfile_2.txt: No such file or directory

$ cat out.txt
/Users/oliver/tmp/tmp
myfile.txt

This is interesting: out.txt has its output. However, not everything went into out.txt, because some error messages were echoed to the console. What's going on here is that there are actually two output streams: stdout (standard out) and stderr (standard error). Look at the following figure from Wikipedia:

image
(Image credit: Wikipedia: Standard streams)

Proper output goes into stdout while errors go into stderr. The syntax for saving stderr in unix is 2> as in:

$ # save the output into out.txt and the error into err.txt
$ ./myscript.sh > out.txt 2> err.txt
$ cat out.txt
/Users/oliver/tmp/tmp
myfile.txt
$ cat err.txt
mkdir: cannot create directory ‘tmp’: File exists
ls: cannot access myfile_2.txt: No such file or directory

When you think about it, the fact that output and error are separated is supremely useful. At work, sometimes we parallelize heavily and run 1000 instances of a script. For each instance, the error and output are saved separately. The 758th job, for example, might look like this:
./myjob --instance 758 > out758.o 2> out758.e
(I'm in the habit of using the suffixes .o for output and .e for error.) With this technique we can quickly scan through all 1000 .e files and check if their size is 0. If it is, we know there was no error; if not, we can re-run the failed jobs. Some programs are in the habit of echoing run statistics or other information to stderr. This is an unfortunate practice because it muddies the water and, as in the example above, would make it hard to tell if there was an actual error.

Output vs error is a distinction that many programming languages make. For example, in C++ writing to stdout and stderr is like this:

cout << "some output" << endl;
cerr << "some error" << endl;

In Perl it's:

print STDOUT "some output\n";
print STDERR "some error\n";

In Python it's:

import sys
sys.stdout.write("some output\n")
sys.stderr.write("some error\n")

and so on.


## More on Stdout and Stderr; Redirection
For the sake of completeness, we should note that you can redirect standard error to standard output and vice versa. Let's make sure we get the syntax of all things pertaining to stdout and stderr right:

1>   # save stdout to (plain old > also works)
2>   # save stderr to

as in:

$ ./myscript.sh 1> out.o 2> out.e
$ ./myscript.sh > out.o 2> out.e   # these two lines are identical

What if we want to choose where things will be printed from within our script? Then we can use the following syntax:

&1   # standard out stream
&2   # standard error stream

Let's examine five possible versions of our Hello Kitty script:

#!/bin/bash
# version 1
echo "hello kitty"

#!/bin/bash
# version 2
echo "hello kitty" > somefile.txt

#!/bin/bash
# version 3
echo "hello kitty" > &1

#!/bin/bash
# version 4
echo "hello kitty" > &2

#!/bin/bash
# version 5
echo "hello kitty" > 1

Here's how they work:

    version 1 - echo "hello kitty" to stdout
    version 2 - echo "hello kitty" to the file somefile.txt
    version 3 - same as version 1
    version 4 - echo "hello kitty" to sterr
    version 5 - echo "hello kitty" to the file named 1

This illustrates the point of the ampersand syntax: it distinguishes between the output streams and files named 1 or 2. Let's try running script version 4 as a sanity check to make sure these scripts are working as expected:

$ # output saved to file but error printed to console
$ ./hellokitty.sh > junk.txt
hello kitty

hello kitty is indeed stderr because it's echoed to the console, not saved into junk.txt.

This syntax makes it easy to see how we could, e.g., redirect the standard error to standard output:

$ ./somescript.sh 2> &1  # redirect stderr to stdout

I rarely have occasion to do this and, although it's not something you need in your introductory unix toolkit, it's good to know.


## Conditional Logic
Conditional Logic is a universal feature of programming languages. The basic idea is, if this condition, then do something. It can be made more complex: if this condition, then do something; else if that condition, then do another thing; else (if any other condition), then do yet another thing. Let's see how to implement this in bash:

$ a=joe
$ if [ $a == "joe" ]; then echo hello; fi
hello

or:

$ a=joe
$ if [ $a == "joe" ]; then echo hello; echo hello; echo hello; fi
hello
hello
hello

The structure is:
if [ condition ]; then ... ; fi
Everything between the words then and fi (if backwards in case you didn't notice) will execute if the condition is satisfied. In other languages, this block is often defined by curly brackets: { }. For example, in a Perl script, the same code would be:

#!/usr/bin/env perl

my $a="joe";

if ( $a eq "joe" )
{
    print "hello\n";
    print "hello\n";
    print "hello\n";
}

In bash, if is if, else is else, and else if is elif. In a script it would look like this:

#!/bin/bash

a=joe

if [ $a == "joe" ]; then
    echo hello;
elif [ $a == "doe" ]; then
    echo goodbye;
else
    echo "ni hao";
fi

You can also use a case statement to implement conditional logic. See an example of that here.

Although I said in the intro that unix is the best place to start your computer science education, I have to admit that the syntax for if-then logic is somewhat unwieldy—even unfriendly. Bash is a bad teaching language for conditional logic, arrays, hashes, etc. But that's only because its element is not heavy-duty programming with lots of functions, numerical operations, sophisticated data structures, and logic. Its mastery is over the quick and dirty, manipulating files and directories, and doing system stuff. I still maintain it's the proper starting point because of its wonderful tools, and because knowing its fundamentals is a great asset. Every language has its place in the programming ecosystem. Back in College, I stumbled on a physics book called The Tiger and the Shark: Empirical Roots of Wave-Particle Dualism by Bruce Wheaton. The book had a great epigraph:

    It is like a struggle between a tiger and a shark,
    each is supreme in his own element,
    but helpless in that of the other.
    J.J. Thomson, 1925

In our context, this would read: bash is supreme on the command line, but not inside of a script.


## File Test Operators; Return or Exit Status
File Test Operators and exit status are two completely different topics, but since they both go well with if statements, I'll discuss them here. File Test Operators are things you can stick in an if statement to give you information about a file. Two common problems are (1) checking if your file exists and (2) checking if it's non-zero size: Let's create two files, one empty and one not:

$ touch emptyfile          # create an empty file
$ echo joe > nonemptyfile  # create a non-empty file

The operator -e tests for existence and -s tests for non-zero-ness:

$ file=emptyfile
$ if [ -e $file ]; then echo "exists"; if [ -s $file ]; then echo "non-0"; fi; fi
exists

$ file=nonemptyfile
$ if [ -e $file ]; then echo "exists"; if [ -s $file ]; then echo "non-0"; fi; fi
exists
non-0

Read The Linux Documentation Project's discussion of file test operators here.

Changing the subject altogether, you may be familiar with the idea of a return value in computer science. Functions can return a value upon completion. In unix, commands also have a return value or exit code, queryable with:
$?
This is usually employed to tell the user whether or not the command successfully executed. By convention, successful execution returns 0. For example:

$ echo joe
joe
$ echo $?  # query exit code of previous command
0

Let's see how the exit code can be useful. We'll make a script, test_exitcode.sh, such that:

$ cat test_exitcode.sh
#!/bin/bash
sleep 10

This script just pauses for 10 seconds. First, we'll let it run and then we'll interrupt it using Cntrl-c:

$ ./test_exitcode.sh;  # let it run
$ echo $?
0

$ ./test_exitcode.sh;  # interrupt it
^C
$ echo $?
130

The non-zero exit code tells us that it's failed. Now we'll try the same thing with an if statement:

$ ./test_exitcode.sh
$ if [ $? == 0 ]; then echo "program succeeded"; else echo "program failed"; fi
program succeeded

$ ./test_exitcode.sh;
^C
$ if [ $? == 0 ]; then echo "program succeeded"; else echo "program failed"; fi
program failed

In research, you might run hundreds of command-line programs in parallel. For each instance, there are two key questions: (1) Did it finish? (2) Did it run without error? Checking the exit status is the way to address the second point. You should always check the program you're running to find information about its exit code, since some use different conventions. Read The Linux Documentation Project's discussion of exit status here.

Question: What's going on here?

$ if echo joe; then echo joe; fi
joe
joe

This is yet another example of bash allowing you to stretch syntax like silly putty. In this code snippet,
echo joe
is run, and its successful execution passes a true return code to the if statement. So, the two joes we see echoed to the console are from the statement to be evaluated and the statement inside the conditional. We can also invert this formula, doing something if our command fails:

$ outputdir=nonexistentdir  # set output dir equal to a nonexistent dir
$ if ! cd $outputdir; then echo "couldnt cd into output dir"; fi
-bash: pushd: nonexistentdir: No such file or directory
couldnt cd into output dir

$ mkdir existentdir  # make a test directory
$ outputdir=existentdir
$ if ! cd $outputdir; then echo "couldnt cd into output dir"; fi
$ # no error -  now we're in the directory existentdir

Did you follow that? (! means logical NOT in unix.) The idea is, we try to cd but, if it's unsuccessful, we echo an error message. This is a particularly useful line to include in a script. If the user gives an output directory as an argument and the directory doesn't exist, we exit. If it does exist, we cd into it and it's business as usual:
if ! cd $outputdir; then echo "[error] couldn't cd into output dir"; exit; fi
Without this line, the script will run in whatever directory it's in if cd fails. Once in lab, I was running a script that didn't have this kind of protection. The output directory wasn't found and the script starting making and deleting files in the wrong directory. It was powerfully uncool!

We can implement similar constructions using the && and || operators rather than an if statement. Let's see how this works by making some test files:

$ touch file{1..4}
$ ls
file1  file2  file3  file4

The && operator will chug through a chain of commands and keep on going until one of the commands fails, as in:

$ ( ls file1 ) && ( ls file2 ) && ( ls file3 ) && ( ls file4 )
file1
file2
file3
file4

$ ( ls file1 ) && ( ls file2 ) && ( ls fileX ) && ( ls file4 )
file1
file2
ls: cannot access fileX: No such file or directory

In contrast, the || operator will proceed through the command chain and stop after the first successful one, as in:

$ ( ls file1 ) || ( ls file2 ) || ( ls file3 ) || ( ls file4 )
file1

$ ( ls fileX ) || ( ls fileY ) || ( ls fileZ ) || ( ls file4 )
ls: cannot access fileX: No such file or directory
ls: cannot access fileY: No such file or directory
ls: cannot access fileZ: No such file or directory
file4


## Basic Loops
In programming, loops are a way of performing operations iteratively. Loops come in different flavors, but the for loop and while loop are the most basic. In bash, we can implement a for loop like this:

$ for i in 1 2 3; do echo $i; done
1
2
3

The structure is:
for variable in list; do ... ; done
Put anything you like in the list:

$ for i in 1 2 hello; do echo $i; done
1
2
hello

Many other languages wouldn't let you get away with combining data types in the iterations of a loop, but this is a recurrent bash theme: it's fast; it's loose; it's malleable.

To count from 1 to 10, try:

$ for i in {1..10}; do echo -n "$i "; done; echo
1 2 3 4 5 6 7 8 9 10

But if we can just write:

$ echo {1..10}

why do we need a loop here? Loops really come into their own in bash when—no surprise!—we're dealing with files, paths, and commands. For example, to loop through all of the text files in the cwd, use:

```
$ for i in *.txt; do echo $i; done
```

Although this is nearly the same as:

```
$ ls *.txt
```
the former construction has the advantage that we can stuff as much code as we like in the block between do and done. Let's make a random directory structure like so:

$ mkdir -p myfolder{1..3}/{X,Y}

We can populate it with token files (fodder for our example) via a loop:

```
$ j=0; for i in myfolder*/*; do echo "*** "$i" ***"; touch ${i}/a_${j}.txt ${i}/b_${j}.txt; ((j++)); done
```

In bash, ((j++)) is a way of incrementing j. We echo $i to get some visual feedback as the loop iterates. Now our directory structure looks like this:

image

To practice loops, suppose we want to find any file that begins with b in any subfolder and make a symbolic link to it from the cwd:

```
$ for i in myfolder*/*/b*; do echo "*** "$i" ***"; ln -s $i; done
```

As we learned above, a link is not a copy of a file but, rather, a kind of pointer that allows us to access a file from a path other than the one where it actually resides. Our loop yields the links:

b_0.txt -> myfolder1/X/b_0.txt
b_1.txt -> myfolder1/Y/b_1.txt
b_2.txt -> myfolder2/X/b_2.txt
b_3.txt -> myfolder2/Y/b_3.txt
b_4.txt -> myfolder3/X/b_4.txt
b_5.txt -> myfolder3/Y/b_5.txt

allowing us to access the b files from the cwd.

I can't overstate all the heroic things you can do with loops in bash. Suppose we want to change the extension of any text file that begins with a and resides in an X subfolder from .txt to .html:

```
$ for i in myfolder*/X/a*.txt; do echo "*** "$i" ***"; j=$( echo $i | sed 's|\.txt|\.html|' ); echo $j; mv $i $j; echo; done
```

But I've jumped the gun! This example features three things we haven't learned yet: command substitution, piping, and sed. You should revisit it after reading those sections, but the idea is that the variable j stores a path that looks like our file's but has the extension replaced. And you see that a knowledge of loops is like a stick of dynamite you can use to blow through large numbers of files.

Here's another contrived example with these yet-to-be-discussed techniques:

```
$ for i in $( echo $PATH | tr ":" " " ); do echo "*** "$i" ***"; ls $i | head; echo; done | less
```

Can you guess what this does? It shows the first ten commands in each folder in our PATH—not something you'd likely need to do, but a demonstration of the fluidity of these constructions.

If we want to run a command or script in parallel, we can do that with loops, too. gzip is a utility to compress files, thereby saving hard drive space. To compress all text files in the cwd, in parallel, do:

```
$ for i in *.txt; do { echo $i; gzip $i & }; done
```

But I've gotten ahead of myself again. We'll leave the discussion of this example to the section on processes.

The structure of a while loop is:
while condition; do ... ; done
I use while loops much less than for loops, but here's an example:

$ x=1; while ((x <= 3)); do echo $x; ((x++)); done
1
2
3

The while loop can also take input from a file. Suppose there's a file junk.txt such that:

$ cat junk.txt
1
2
3

You can iterate over this file as such:

$ while read x; do echo $x; done < junk.txt
1
2
3

## Arguments to a Script
Now that we've covered basic control flow, let's return to the subject of scripting. An important question is, how can we pass arguments to our script? Let's make a script called hellokitty.sh:

```
#!/bin/bash

echo hello

Try running it:

$ chmod 755 hellokitty.sh
$ ./hellokitty.sh
hello
```

We can change it to the following:
```
#!/bin/bash

echo hello $1
```

Now:
```
$ ./hellokitty.sh kitty
hello kitty
```

In bash $1 represents the first argument to the script, $2 the second, and so on. If our script is:
```
#!/bin/bash

echo $0
echo hello $1 $4
```

Then:

```
$ ./hellokitty.sh my sweet kitty cat
./hellokitty.sh
hello my cat
```

In most programming languages, arguments passed in on the command line are stored as an array. Bash stores the nth element of this array in the variable $n. $0 is special and refers to the name of the script itself.

For casual scripts this suits us well. However, as you go on to write more involved programs with many options, it becomes impractical to rely on the position of an argument to determine its function in your script. The proper way to do this is using flags that can be deployed in arbitrary order, as in:
command --flag1 1 --flag2 1 --flag3 5
or, in short form:
command -f1 1 -f2 1 -f3 5
You can do this with the command getopts, but it's sometimes easier just to write your own options parser. Here's a sample script called test_args. Although a case statement would be a good way to handle numerous conditions, I'll use an if statement:

#!/bin/bash

helpmessage="This script showcases how to read arguments"

### get arguments
# while input array size greater than zero
while (($# > 0)); do
    if [ "$1" == "-h" -o "$1" == "-help" -o "$1" == "--help" ]; then
        shift;
        echo "$helpmessage"
        exit;
    elif [ "$1" == "-f1" -o "$1" == "--flag1" ]; then
        # store what's passed via flag1 in var1
        shift; var1=$1; shift
    elif [ "$1" == "-f2" -o "$1" == "--flag2" ]; then
        shift; var2=$1; shift
    elif [ "$1" == "-f3" -o "$1" == "--flag3" ]; then
        shift; var3=$1; shift
    # if unknown argument, just shift
    else
        shift
    fi
done

### main
# echo variable if not empty
if [ ! -z $var1 ]; then echo "flag1 passed "$var1; fi
if [ ! -z $var2 ]; then echo "flag2 passed "$var2; fi
if [ ! -z $var3 ]; then echo "flag3 passed "$var3; fi

This has some things we haven't seen yet:

    $# is the size of our input argument array
    shift pops an element off of our array (the same as in Perl)
    exit exits the script
    -o is logical OR in unix
    -z checks if a variable is empty

The code loops through the argument array and keeps popping off elements until the array size is zero, whereupon it exits the loop. For example, one might run this script as:

$ ./test_args --flag1 x -f2 y --flag3 zzz
flag1 passed x
flag2 passed y
flag3 passed zzz

To spell out how this works, the first argument is --flag1. Since this matches one of our checks, we shift. This pops this element out of our array, so the first element, $1, becomes x. This is stored in the variable var1, then there's another shift and $1 becomes -f2, which matches another condition, and so on.

The flags can come in any order:

$ ./test_args --flag3 x --flag1 zzz
flag1 passed zzz
flag3 passed x

$ ./test_args --flag2 asdf
flag2 passed asdf

We're brushing up against the outer limits of bash here. My prejudice is that you usually shouldn't go this far with bash, because its limitations will come sharply into focus if you try to do too-involved scripting. Instead, use a more friendly language. In Perl, for example, the array containing inputs is @ARGV; in Python, it's sys.argv. Let's compare these common scripting languages:


Bash	Perl	Python	Description

$0	$0	sys.argv[0]	Name of Script Itself

$*			String Containing All Input Arguments

("$@")	@ARGV	sys.argv	Array or List Containing All Input Arguments [1]

$1	$ARGV[0]	sys.argv[1]	First Argument

$2	$ARGV[1]	sys.argv[2]	Second Argument


Perl has a Getopt package that is convenient for reading arguments, and Python has an even better one called argparse. Their functionality is infinitely nicer than bash's, so steer clear of bash if you're going for a script with lots of options.


[1] The distinction between $* and $@ is knotty. Dive into these subtleties on Stackoverflow ↑

## Multi-Line Comments, Multi-Line Strings in Bash
Let's continue in the realm of scripting. You can do a multi-line comment in bash with an if statement:

# multi-line comment
if false; then
echo hello
echo hello
echo hello
fi

(Yes, this is a bit of a hack!)

Multi-line strings are handy for many things. For example, if you want a help section for your script, you can do it like this:

cat <<_EOF_

Usage:

$0 --flag1 STRING [--flag2 STRING] [--flag3 STRING]

Required Arguments:

  --flag1 STRING	This argument does this

Options:

  --flag2 STRING	This argument does that
  --flag3 STRING	This argument does another thing

_EOF_

How does this syntax work? Everything between the _EOF_ tags comprises the string and is printed. This is called a Here Document. Read The Linux Documentation Project's discussion of Here Documents here.


## Source and Export
Question: If we create some variables in a script and exit, what happens to those variables? Do they disappear? The answer is, yes, they do. Let's make a script called test_src.sh such that:

$ cat ./test_src.sh
#!/bin/bash

myvariable=54
echo $myvariable

If we run it and then check what happened to the variable on our command line, we get:

$ ./test_src.sh
54
$ echo $myvariable


The variable is undefined. The command source is for solving this problem. If we want the variable to persist, we run:

$ source ./test_src.sh
54
$ echo $myvariable
54

and—voilà!—our variable exists in the shell. An equivalent syntax for sourcing uses a dot:

$ . ./test_src.sh  # this is the same as "source ./test_src.sh"
54

But now observe the following. We'll make a new script, test_src_2.sh, such that:

$ cat ./test_src_2.sh
#!/bin/bash

echo $myvariable

This script is also looking for $myvariable. Running it, we get:

$ ./test_src_2.sh


Nothing! So $myvariable is defined in the shell but, if we run another script, its existence is unknown. Let's amend our original script to add in an export:

$ cat ./test_src.sh
#!/bin/bash

export myvariable=54  # export this variable
echo $myvariable

Now what happens?

$ ./test_src.sh
54
$ ./test_src_2.sh

Still nothing! Why? Because we didn't source test_src.sh. Trying again:

$ source ./test_src.sh
54
$ ./test_src_2.sh
54

So, at last, we see how to do this. If we want access on the shell to a variable which is defined inside a script, we must source that script. If we want other scripts to have access to that variable, we must source plus export.


## Dotfiles (.bashrc and .bash_profile)
Dotfiles are simply files that begin with a dot. We can make a test one as follows:

$ touch .test

Such a file will be invisible in the GUI and you won't see it with vanilla ls either. (This works the same way for directories.) The only way to see it is to use the list all option:
ls -al
or to list it explicitly by name. This is useful for files that you generally want to keep hidden from the user or discourage tinkering with.

Many programs, such as bash, Vim, and Git, are highly configurable. Each uses dotfiles to let the user add functionality, change options, switch key bindings, etc. For example, here are some of the dotfiles files each program employs:

    bash - .bashrc
    vim - .vimrc
    git - .gitconfig

The most famous dotfile in my circle is .bashrc which resides in HOME and configures your bash. Actually, let me retract that: let's say .bash_profile instead of .bashrc (read about the difference here). In any case, the idea is that this dotfile gets executed as soon as you open up the terminal and start a new session. It is therefore ideal for setting your PATH and other variables, adding functions (like this one), creating aliases (discussed below), and doing any other setup related chore. For example, suppose you download a new program into /some/path/to/prog and you want to add it to your PATH. Then in your .bash_profile you'd add:

export PATH=/some/path/to/prog:$PATH

Recalling how export works, this will allow any programs we run on the command line to have access to our amended PATH. Note that we're adding this to the front of our PATH (so, if the program exists in our PATH already, the existing copy will be superseded). Here's an example snippet of my setup file:

PATH=/apps/python/2.7.6/bin:$PATH	# use this version of Python
PATH=/apps/R/3.1.2/bin:$PATH		# use this version of R
PATH=/apps/gcc/4.6.0/bin/:$PATH		# use this version of gcc
export PATH

There is much ado about .bashrc (read .bash_profile) and it inspired one of the greatest unix blog-post titles of all time: Pimp my .bashrc—although this blogger is only playing with his prompt, as it were. As you go on in unix and add things to your .bash_profile, it will evolve into a kind of fingerprint, optimizing bash in your own unique way (and potentially making it difficult for others to use).

If you have multiple computers, you'll want to recycle much of your program configurations on all of them. My co-worker uses a nice system I've adopted where the local and global aspects of setup are separated. For example, if you wanted to use certain aliases across all your computers, you'd put them in a global settings file. However, changes to your PATH might be different on different machines, so you'd store this in a local settings file. Then any time you change computers you can simply copy the global files and get your familiar setup, saving lots of work. A convenient way to accomplish this goal of a unified shell environment across all the systems you work on is to put your dotfiles on a server, like GitHub or Bitbucket, you can access from anywhere. This is exactly what I've done and you can get the up-to-date versions of my dotfiles on GitHub.

Here's a sketch of how this idea works: in HOME make a .dotfiles/bash directory and populate it with your setup files, using a suffix of either local or share:

$ ls -1 .dotfiles/bash/
bash_aliases_local
bash_aliases_share
bash_functions_share
bash_inirun_local
bash_paths_local
bash_settings_local
bash_settings_share
bash_welcome_local
bash_welcome_share

When .bash_profile is called at the startup of your session, it sources all these files:

# the directory where bash configuration files reside
INIT_DIR="${HOME}/.dotfiles/bash"

# to make local configurations, add these files into this directory:
# bash_aliases_local
# bash_paths_local
# bash_settings_local
# bash_welcome_local

# this line, e.g.,  protects the functionality of rsync by only turning on the below if the shell is in interactive mode
# In particular, rsync fails if things are echo-ed to the terminal
[[ "$-" != *i* ]] && return

# bash welcome
if [ -e "${INIT_DIR}/bash_welcome_local" ]; then
	cat ${INIT_DIR}/bash_welcome_local
elif [ -e "${INIT_DIR}/bash_welcome_share" ]; then
	cat ${INIT_DIR}/bash_welcome_share
fi

#--------------------LOCAL------------------------------
# aliases local
if [ -e "${INIT_DIR}/bash_aliases_local" ]; then
	source "${INIT_DIR}/bash_aliases_local"
	echo "bash_aliases_local loaded"
fi

# settings local
if [ -e "${INIT_DIR}/bash_settings_local" ]; then
	source "${INIT_DIR}/bash_settings_local"
	echo "bash_settings_local loaded"
fi

# paths local
if [ -e "${INIT_DIR}/bash_paths_local" ]; then
	source "${INIT_DIR}/bash_paths_local"
	echo "bash_paths_local loaded"
fi

#---------------SHARE-----------------------------
# aliases share
if [ -e "${INIT_DIR}/bash_aliases_share" ]; then
	source "${INIT_DIR}/bash_aliases_share"
	echo "bash_aliases_share loaded"
fi

# settings share
if [ -e "${INIT_DIR}/bash_settings_share" ]; then
	source "${INIT_DIR}/bash_settings_share"
	echo "bash_settings_share loaded"
fi

# functions share
if [ -e "${INIT_DIR}/bash_functions_share" ]; then
	source "${INIT_DIR}/bash_functions_share"
	echo "bash_functions_share loaded"
fi

A word of caution: echoing things in your .bash_profile, as I'm doing here, can be dangerous and break the functionaly of utilities like scp and rsync. However, we protect against this with the cryptic line near the top.

Taking care of bash is the hard part. Other programs are less of a chore because, even if you have different programs in your PATH on your home and work computers, you probably want everything else to behave the same. To accomplish this, just drop all your other configuration files into your .dotfiles repository and link to them from your home directory:

.gitconfig -> .dotfiles/.gitconfig
.vimrc -> .dotfiles/.vimrc


## Working Faster with Readline Functions and Key Bindings
If you've started using the terminal extensively, you might find that things are a bit slow. Perhaps you need some long command you wrote yesterday and you don't want to write the damn thing again. Or, if you want to jump to the end of a line, it's tiresome to move the cursor one character at a time. Failure to immediately solve these problems will push your productivity back into the stone age and you may end up swearing off the terminal as a Rube Goldberg-ian dystopia. So—enter keyboard shortcuts!

The backstory about shortcuts is that there are two massively influential text editors, Emacs and Vim, whose users—to be overdramatic—are divided into two warring camps. Each program has its own conventions for shortcuts, like jumping words with your cursor, and in bash they're Emacs-flavored by default. But you can toggle between either one:

$ set -o emacs  # Set emacs-style key bindings (this is the default)
$ set -o vi     # Set vi-style key bindings

Although I prefer Vim as a text-editor, I use Emacs key bindings on the command line. The reason is that in Vim there are multiple modes (normal mode, insert mode, command mode). If you want to jump to the front of a line, you have to switch from insert mode to normal mode, which breaks up the flow a little. In Emacs there's no such complication. Emacs commands usually start with the Control key or the Meta key (usually Esc). Here are some things you can do:

    Cntrl-a - jump cursor to beginning of line
    Cntrl-e - jump cursor to end of line
    Cntrl-k - delete to end of line
    Cntrl-u - delete to beginning of line
    Cntrl-w - delete back one word
    Cntrl-y - paste (yank) what was deleted with the above shortcuts
    Cntrl-r - reverse-search history for a given word
    Cntrl-c - kill the process running in the foreground; don't execute current line on the command line
    Cntrl-z - suspend the process running in the foreground
    Cntrl-l - clear screen. (this has an advantage over the unix command clear in that it works in the Python, MySQL, and other shells)
    Cntrl-d - end of transmission (in practice, often synonymous with quit - e.g., exiting the Python or MySQL shells)
    Cntrl-s - freeze screen
    Cntrl-q - un-freeze screen

These are supremely useful! I use these numerous times a day. (On the Mac, the first three even work in the Google search bar!) The first bunch of these fall under the umbrella of ReadLine Functions (read GNU's extensive documentation here). There are actually tons more, and you can see them all by entering:

$ bind -P  # show all Readline Functions and their key bindings
$ bind -l  # show all Readline Functions

Four of the most excellent Readline Functions are:

    forward-word - jump cursor forward a word
    backward-word - jump cursor backward a word
    history-search-backward - scroll through your bash history backward
    history-search-forward - scroll through your bash history forward

For the first two—which are absolutely indispensable—you can use the default Emacs way:

    Meta-f - jump forward one word
    Meta-b - jump backward one word

However, reaching for the Esc key is a royal pain in the ass—you have to re-position your hands on the keyboard. This is where key-binding comes into play. Using the command bind, you can map a Readline Function to any key combination you like. Of course, you should be careful not to overwrite pre-existing key bindings that you want to use. I like to map the following keys to these Readline Functions:

    Cntrl-forward-arrow - forward-word
    Cntrl-backward-arrow - backward-word
    up-arrow - history-search-backward
    down-arrow - history-search-forward

In my .bash_profile (or, more accurately, in my global bash settings file) I use:

# make cursor jump over words
bind '"\e[5C": forward-word'    # control+arrow_right
bind '"\e[5D": backward-word'   # control+arrow_left

# make history searchable by entering the beginning of command
# and using up and down keys
bind '"\e[A": history-search-backward'  # arrow_up
bind '"\e[B": history-search-forward'   # arrow_down

(although these may not work universally [1].) How does this cryptic symbology translate into these particular keybindings? There's a neat trick you can use, to be revealed in the next section.

Tip: On Mac, you can move your cursor to any position on the line by holding down Option and clicking your mouse there. I rarely use this, however, because it's faster to make your cursor jump via the keyboard.


[1] If you have trouble getting this to work on OS's terminal, try iTerm2 instead, as described here ↑


## More on Key Bindings, the ASCII Table, Control-v
Before we get to the key binding conundrum, let's review ASCII. This is, simply, a way of mapping every character on your keyboard to a numeric code. As Wikipedia puts it:

    The American Standard Code for Information Interchange (ASCII) is a character-encoding scheme originally based on the English alphabet that encodes 128 specified characters—the numbers 0-9, the letters a-z and A-Z, some basic punctuation symbols, some control codes that originated with Teletype machines, and a blank space—into the 7-bit binary integers.

For example, the character A is mapped to the number 65, while q is 113. Of special interest are the control characters, which are the representations of things that cannot be printed like return or delete. Again from Wikipedia, here is the portion of the ASCII table for these control characters:


Binary	Oct	Dec	Hex	Abbr	[a]	[b]	[c]	Name

000 0000	000	0	00	NUL	␀	^@	\0	Null character

000 0001	001	1	01	SOH	␁	^A		Start of Header

000 0010	002	2	02	STX	␂	^B		Start of Text

000 0011	003	3	03	ETX	␃	^C		End of Text

000 0100	004	4	04	EOT	␄	^D		End of Transmission

000 0101	005	5	05	ENQ	␅	^E		Enquiry

000 0110	006	6	06	ACK	␆	^F		Acknowledgment

000 0111	007	7	07	BEL	␇	^G	\a	Bell

000 1000	010	8	08	BS	␈	^H	\b	Backspace

000 1001	011	9	09	HT	␉	^I	\t	Horizontal Tab

000 1010	012	10	0A	LF	␊	^J	\n	Line feed

000 1011	013	11	0B	VT	␋	^K	\v	Vertical Tab

000 1100	014	12	0C	FF	␌	^L	\f	Form feed

000 1101	015	13	0D	CR	␍	^M	\r	Carriage return

000 1110	016	14	0E	SO	␎	^N		Shift Out

000 1111	017	15	0F	SI	␏	^O		Shift In

001 0000	020	16	10	DLE	␐	^P		Data Link Escape

001 0001	021	17	11	DC1	␑	^Q		Device Control 1 (oft. XON)

001 0010	022	18	12	DC2	␒	^R		Device Control 2

001 0011	023	19	13	DC3	␓	^S		Device Control 3 (oft. XOFF)

001 0100	024	20	14	DC4	␔	^T		Device Control 4

001 0101	025	21	15	NAK	␕	^U		Negative Acknowledgement

001 0110	026	22	16	SYN	␖	^V		Synchronous idle

001 0111	027	23	17	ETB	␗	^W		End of Transmission Block

001 1000	030	24	18	CAN	␘	^X		Cancel

001 1001	031	25	19	EM	␙	^Y		End of Medium

001 1010	032	26	1A	SUB	␚	^Z		Substitute

001 1011	033	27	1B	ESC	␛	^[	\e	Escape

001 1100	034	28	1C	FS	␜	^\		File Separator

001 1101	035	29	1D	GS	␝	^]		Group Separator

001 1110	036	30	1E	RS	␞	^^		Record Separator

001 1111	037	31	1F	US	␟	^_		Unit Separator

111 1111	177	127	7F	DEL	␡	^?		Delete


([a], [b], and [c] refer to different notations—unicode, caret notation, and escape codes.)

So, the punchline: on the terminal you can press Cntrl-v followed by a special key, like up-arrow or delete, to see its key binding. For example, what's the code for the up-arrow key? Press Cntrl-v up-arrow. On my computer the result is:

$ ^[[A

Cntrl-v down-arrow is:

$ ^[[B

while Cntrl-v Cntrl-left-arrow is:

$ ^[[5D

and so on. These may be different on your computer. As the chart above shows us, the ^[ is the terminal's notation for Escape (it can also be represented as 033 or \e). To state the obvious, a sequence of characters following the escape character can take on a life of its own: Esc-f means something different than f. So, after all this effort, we finally get the payoff of understanding how the following lines work:

# make cursor jump over words
bind '"\e[5C": forward-word'    # control+arrow_right
bind '"\e[5D": backward-word'   # control+arrow_left

# make history searchable by entering the beginning of command
# and using up and down keys
bind '"\e[A": history-search-backward'  # arrow_up
bind '"\e[B": history-search-forward'   # arrow_down

If you want to use different key bindings than mine or more functions, go for it, but the important thing is that you make use of the Readline Functions—they will save you loads of time. Remember, you can list their names with bind -l.

Note: On the Mac you can also see and edit some key bindings for the terminal in:
Terminal > Preferences > Settings > Keyboard
Screenshot:

image


## Aliases, Functions
Let's look at another convenience bash offers: the alias command. Aliasing is a way of mapping one word to another. It can reduce your typing burden by making a shorter expression stand for a longer one:
alias c="cat"
This means every time you type a c the terminal is going to read it as cat, so instead of writing:

$ cat file.txt

you just write:

$ c file.txt

Another use of alias is to weld particular flags onto a command, so every time the command is called, the flags go with it automatically, as in:
alias cp="cp -R"
or
alias mkdir="mkdir -p"
Recall the former allows you to copy directories as well as files, and the later allows you to make nested directories. Perhaps you always want to use these options, but this is a tradeoff between convenience and freedom. In general, I prefer to use new words for aliases and not overwrite preexisting bash commands. Here are some aliases I use in my setup file (see the complete list here):

alias c="cat"
alias s="less -S"
alias l="ls -hl"
alias lt="ls -hlt"
alias ll="ls -al"
alias rr="rm -r"
alias r="readlink -m"
alias ct="column -t"
alias ch="chmod -R 755"
alias chh="chmod -R 644"
alias grep="grep --color"
alias yy="rsync -azv --progress"
# remove empty lines with white space
alias noempty="perl -ne '{print if not m/^(\s*)$/}'"
alias awkf="awk -F'\t'"
alias length="awk '{print length}'"

Aliases are a godsend. But they also have their limitations. If you're familiar with git, you know the following commands might go together:

$ git add .
$ git commit -m "some message"
$ git push

If you always want to call them together, you can put them in a function which gets sourced in your setup file. We'll call this function gup for git update:

# stage all changes, commit, then push
gup ()
{
    local mymessage="next update";

    # if $1 not zero length
    if [ ! -z "$1" ]; then
        mymessage=$1
    fi

    git add .
    git commit -m "$mymessage"
    git push
}

A couple of notes about functions in bash: (1) the arguments to a functions are retrieved as $1, $2, etc., just as in a script; (2) if you're making a function in a script, variables are global by default unless you declare them as local. I declared mymessage as a local variable, even though in this case there's no danger I'd confuse it with a global variable of the same name.

This teaches us how to build functions but it's not terribly useful, because because you can git add and git commit in a single step anyway—so this is a lot of overhead merely to call two commands together. The Linux Documentation Project provides a sample .bashrc with the following more interesting function:

```
extract () {
    if [ -f $1 ] ; then
        case $1 in
            *.tar.bz2)   tar xvjf $1    ;;
            *.tar.gz)    tar xvzf $1    ;;
            *.bz2)       bunzip2 $1     ;;
            *.rar)       unrar x $1     ;;
            *.gz)        gunzip $1      ;;
            *.tar)       tar xvf $1     ;;
            *.tbz2)      tar xvjf $1    ;;
            *.tgz)       tar xvzf $1    ;;
            *.zip)       unzip $1       ;;
            *.Z)         uncompress $1  ;;
            *.7z)        7z x $1        ;;
            *)           echo "don't know how to extract '$1'..." ;;
        esac
    else
        echo "'$1' is not a valid file!"
    fi
}
```

There are many ways to compress files in unix, such as zip and bzip2. And the command tar is for archiving—taking a whole directory structure and rolling it up into a single file (sometimes called a tarball). This function serves as a one-size-fits-all command to untar and/or uncompress these many different compression formats. Note that, because there are so many cases, it's better to use a case statement than an if statement.

To use this function, the syntax would simply be:
```
$ extract my_compressed_file.gz

$ extract my_compressed_file.bz2

$ extract my_compressed_tarball.tar.gz
```

## The Top 20 Indispensable Unix Commands
Before going any further, let's learn some more bedrock commands that—according to any unix primer—it would be impossible to get by without knowing:

    pwd
    ls
    cd
    mkdir
    echo
    cat
    cp
    mv
    rm
    man
    head
    tail
    less
    more
    sort
    grep
    which
    chmod
    history
    clear

We've already seen the first 10, along with which and chmod. The easiest new one on the above list is clear, which simply clears your screen. We'll cover the rest below.
head and tail TOP
head and tail print the first or last n lines of a file, where n is 10 by default. For example:

$ head myfile.txt      # print the first 10 lines of the file
$ head -1 myfile.txt   # print the first line of the file
$ head -50 myfile.txt  # print the first 50 lines of the file

$ tail myfile.txt      # print the last 10 lines of the file
$ tail -1 myfile.txt   # print the last line of the file

These are great alternatives to cat, because you usually don't want to spew out a giant file. You only want to peek at it, get a sense of the formatting, or hone in on some specific portion. If you combine head and tail together in the same command chain—we'll see how to do this in the section about unix pipelines—you can get a row of your file by number.

Another thing I like to do with head is look at multiple files simultaneously. For example, whereas cat concatenates files together:

$ cat hello.txt
hello
hello
hello

$ cat kitty.txt
kitty
kitty
kitty

$ cat hello.txt kitty.txt
hello
hello
hello
kitty
kitty
kitty

head will print out the name of the file when it takes multiple arguments, as in:

$ head -2 hello.txt kitty.txt
==> hello.txt <==
hello
hello

==> kitty.txt <==
kitty
kitty

This is useful if you're previewing many files—say doing:

$ head *

less and more TOP
less is, as the manual pages say, "a filter for paging through text one screenful at a time...which allows backward movement in the file as well as forward movement." If you have a big file, vanilla cat is not a suitable command because printing thousands of lines of text to stdout will flood your screen. Instead, use less, the go-to command for viewing files in the terminal:

$ less myfile.txt      # view the file page by page

Type the arrow keys to scroll up and down, Space to page down, and q to exit. Another nice thing about less: it has many Vim-like features you can read about on its man page, and this is not a coincidence. For example, if you want to search for the word apple in your file, you just type slash ( / ) followed by apple.

If you have a file with many columns, it's hard to view in the terminal. A neat less flag to solve this problem is -S:

$ less -S myfile.txt    # allow horizontal scrolling

This enables horizontal scrolling instead of having rows messily wrap onto the next line. This flag works particularly well in combination with the column command, which forces the columns of your file to line up nicely:

cat myfile.txt | column -t | less -S

(this construction will be clearer when we learn about unix pipes below.) column delimits on whitespace by default, so if your fields themselves contain spaces and you want to delimit on tabs, amend it to:

cat myfile.txt | column -s'      ' -t | less -S

(where you make a tab in the terminal by typing Cntrl-v tab). This makes the terminal feel almost like an Excel spreadsheet. Observe how it changes the viewing experience for this file of fake financial data:

image

I included less and more together because I think about them as a pair, but I told a little white lie in calling more indispensable: you really only need to use less, which is an improved version of more. Less is more :-)
grep TOP
Unix has many file processing utilities, and grep and sort are among them. These are tremendously useful commands for gleaning information about files. grep is the terminal's analog of find from ordinary computing (not to be confused with unix find). If you've ever used Safari or Chrome or Microsoft Word, you can find a word with ⌘F (Command-f) on Macintosh. Similarly, grep searches for text in a file and returns the line(s) where it finds a match. For example, if you were searching for the word apple in your file, you'd do:

$ grep apple myfile.txt          # return lines of file with the text apple

grep has many nice flags, such as:

$ grep -n apple myfile.txt       # include the line number
$ grep -i apple myfile.txt       # case insensitive matching
$ grep --color apple myfile.txt  # color the matching text

Also useful are what I call the ABCs of Grep—that's After, Before, Context. Here's what they do:

$ grep -A1 apple myfile.txt	# return lines with the match,
				# as well as 1 after

$ grep -B2 apple myfile.txt	# return lines with the match,
				# as well as 2 before

$ grep -C3 apple myfile.txt	# return lines with the match,
				# as well as 3 before and after.

You can also do an inverse grep with the -v flag. To find lines that don't contain apple, try:

$ grep -v apple myfile.txt	# return lines that don't contain apple

To find any occurrence of apple in any file in some directory, use the recursive flag:

$ grep -R apple mydirectory/	# search for apple in any file in mydirectory

You can exit after, say, finding the first two instances of apple, so you don't waste more time searching:

$ grep -m 2 apple myfile.txt

There are more powerful variants of grep, like egrep, which permits the use of regular expressions (more on these later), as in:

$ egrep "apple|orange" myfile.txt  # return lines with apple OR orange

as well as other fancier grep-like tools, such as ack, available for download. For some reason—perhaps because it's useful in a quick and dirty way and doesn't have any other meanings in English—grep has inspired a peculiar cult following. There are grep t-shirts, grep memes, a grep function in Perl, and—unbelievably—even a whole O'Reilly book devoted to the command:

image
(Image credit: O'Reilly Media)
sort TOP
As you guessed, the command sort sorts files. It has a large man page, but we can learn its basic features by example. Let's suppose we have a file, testsort.txt, such that:

$ cat testsort.txt
vfw	34	awfjo
a	4	2
f	10	10
beb	43	c
f	2	33
f	1	?

Then:

$ sort testsort.txt
a	4	2
beb	43	c
f	1	?
f	10	10
f	2	33
vfw	34	awfjo

What happened? The default behavior of sort is to dictionary sort the rows of a file according to what's in the first column, then second column, and so on. Where the first column has the same value—f in this example—the values of the second column determine the order of the rows. Dictionary sort means that things are sorted as they would be in a dictionary: 1,2,10 gets sorted as 1,10,2. If you want to do a numerical sort, use the -n flag; if you want to sort in reverse order, use the -r flag. You can also sort according to a specific column. The notation for this is:
sort -kn,m
where n and m are numbers which refer to the range column n to column m. In practice, it may be easier to use a single column rather than a range so, for example:
sort -k2,2
means sort by the second column (technically, from column 2 to column 2).

To sort numerically by the second column:

$ sort -k2,2n testsort.txt
f	1	?
f	2	33
a	4	2
f	10	10
vfw	34	awfjo
beb	43	c

As is often the case in unix, we can combine flags as much as we like.

Question: What does this do?

$ sort -k1,1r -k2,2n testsort.txt
vfw	34	awfjo
f	1	?
f	2	33
f	10	10
beb	43	c
a	4	2

Answer: The file has been sorted first by the first column, in reverse dictionary order, and then—where the first column is the same—by the second column in numerical order. You get the point!

Two more notes about sort. Sometimes it is necessary to sort rows uniquely and the flag for this is -u:

$ sort -u testsort.txt               # sort uniquely

To get really in the weeds, another interesting flag is -T:

$ sort -T /my/tmp/dir testsort.txt   # sort using a designated tmp directory

We touched on this briefly in the section about global variables. Behind the curtain, sort does its work by making temporary files, and it needs a place to put those files. By default, this is the directory set by TMPDIR, but if you have a giant file to sort, you might have reason to instruct sort to use another directory and that's what this flag does.
history TOP
Bash is a bit like the NSA in that it's secretly recording everything you do—at least on the command line. But fear not: unless you're doing something super unsavory, you want your history preserved because having access to previous commands you've entered in the shell saves a lot of labor. You can see your history with the command history:

$ history

The easiest way to search the history, as we've seen, is to bind the Readline Function history-search-backward to something convenient, like the up arrow. Then you just press up to scroll backwards through your history. So, if you enter a c, pressing up will step through all the commands you entered that began with c. If you want to find a command that contains the word apple, a useful tool is reverse intelligent search, which is invoked with Cntrl-r:
(reverse-i-search)`':
Although we won't cover unix pipelines until the next section, I can't resist giving you a sneak-preview. An easier way to find any commands you entered containing apple is:

$ history | grep apple

If you wanted to see the last 10 commands you entered, it would be:

$ history | tail

What's going on under the hood is somewhat complicated. Bash actually records your command history in two ways: (1) it stores it in memory—the history list—and (2) it stores it in a file—the history file. There are a slew of global variables that mediate the behavior of history, but some important ones are:

    HISTFILE - the path to the history file
    HISTSIZE - how many commands to store in the history list (memory)
    HISTFILESIZE - how many commands to store in the history file

Typically, HISTFILE is a dotfile residing in HOME:
~/.bash_history
It's important to understand the interplay between the history list and the history file. In the default setup, when you type a command at the prompt it goes into your history list—and is thus revealed via history—but it doesn't get written into your history file until you log out. The next time you log in, the contents of your history file are automatically read into memory (your history list) and are thus searchable in your session. So, what's the difference between the following two commands?

$ history | tail
$ tail ~/.bash_history

The former will show you the last 10 commands you entered in your current session while the later will show you last 10 commands from the previous session. This is all well and good, but let's imagine the following scenario: you're like me and you have 5 or 10 different terminal windows open at the same time. You're constantly switching windows and entering commands, but history-search is such a useful function that you want any command you enter in any one of the 5 windows to be immediately accessible on all the others. We can accomplish this by putting the following lines in our setup dotfile (.bash_profile):

# append history to history file as you type in commands
shopt -s histappend
export PROMPT_COMMAND='history -a'

How does this bit of magic work? Here's what the histappend option does, to quote from the man page of shopt:

    If set, the history list is appended to the history file when the shell exits, rather than overwriting the history file.
    shopt -s histappend
    To append every line to history individually set:
    PROMPT_COMMAND='history -a'
    With these two settings, a new shell will get the history lines from all previous shells instead of the default 'last window closed'>history (the history file is named by the value of the HISTFILE variable)

Let's break this down. shopt stands for "shell options" and is for enabling and disabling various miscellaneous options. The
history -a
part will "Append the new history lines (history lines entered since the beginning of the current Bash session) to the history file" (as the man page says). And the global variable PROMPT_COMMAND is a rather funny one that executes whatever code is stored in it right before each printing of the prompt. Put these together and you're immediately updating the ~/.bash_history file with every command instead of waiting for this to happen at logout. Since every shell can contribute in real time, you can run multiple shells in parallel and have access to a common history on all of them—a good situation.

What if you are engaged in unsavory behavior and want to cover your tracks? You can clear your history as follows:

$ history -c  # clear the history list in memory

However, this only deletes what's in memory. If you really want to be careful, you had better check your history file, .bash_history, and delete any offending portions. Or just wipe the whole thing:

$ echo > ~/.bash_history

You can read more about history on gnu.org.

A wise man once said, "Those who don't know history are destined to [re-type] it." Often it's necessary to retrace your footsteps or repeat some commands. In particular, if you're doing research, you'll be juggling lots of scripts and files and how you produced a file can quickly become mysterious. To deal with this, I like to selectively keep shell commands worth remembering in a "notes" file. If you looked on my computer, you'd see notes files scattered everywhere. You might protest: but these are in your history, aren't they? Yes, they are, but the history is gradually erased; it's clogged with trivial commands like ls and cd; and it doesn't have information about where the command was run. A month from now, your ~/.bash_history is unlikely to have that long command you desperately need to remember, but your curated notes file will.

To make this easy I use the following alias:

alias n="history | tail -2 | head -1 | tr -s ' ' | cut -d' ' -f3- | awk '{print \"# \"\$0}' >> notes"

which—you know the refrain!—will be easier to understand after we learn pipes. To use this, just type n (for notesappend) after a command:

$ ./long_hard-to-remember_command --with_lots --of_flags > poorly_named_file
$ n

Now a notes file has been created (or appended to) in our cwd and we can look at it:

$ cat notes
# ./long_hard-to-remember_command --with_lots --of_flags > poorly_named_file

I use notesappend almost as much as I use the regular unix utilities.
Piping in Unix TOP
Piping is, without a shred of exaggeration, one of the greatest things in unix. To pipe in unix is to string commands together such that the output of the previous one becomes the input of the next one. It's the cat's meow! The beauty of piping is that commands become modular components—building blocks you can snap together a million different ways. A vertical line ( | ) is the syntactic connector:

$ cat file.txt | sort | less

Let's parse this: instead of going to stdout, the output of cat goes into sort, and the output of sort, in turn, goes into less, whose output finally lands on our screen. This is perfect when you have a big file you want to view page by page, but you want to see it sorted. Remember that there are two streams, stdout and stderr. With piping, only the stdout stream gets passed through the pipeline; the stderr—we hope there isn't any—hits our screen right away. There's a nice figure from Wikipedia summarizing this:

image
(Image credit: Wikipedia: Pipeline (Unix))

It's been hard to get this far without mentioning pipes and you saw we were starting to break down in the section about about loops as well as history:

$ history | tail        # show the last 10 lines of history
$ history | grep apple  # find commands in history containing "apple"

because there's no other simple way to do these things. I also mentioned that we'd learn how to print, say, the 37th line of a file using pipes. In unix there's always more than one way to skin a cat, so here are two:

$ cat -n file.txt | head -37 | tail -1  # print row 37
$ cat -n file.txt | awk 'NR==37'        # print row 37

(In awk, which we'll learn about below, NR is a special variable which refers to the row number.) Another command you can use in your pipelines is tee. Consider the following. We have a file text.txt such that:

$ cat test.txt
1	c
3	c
2	t
1	c

Then:

$ cat test.txt | sort -u | tee tmp.txt | wc -l
3

$ cat tmp.txt
1	c
2	t
3	c

tee, in rough analogy with a plumber's tee fitting, allows us to save a file in the middle of the pipeline and keep going. In this case, the output of sort is both saved as tmp.txt and passed through the pipe to wc -l, which counts the lines of the file.

Using pipes expands the number of things you can do in the shell exponentially. The following are some miscellaneous examples of command pipelines.

Print the number of unique elements in the second column of a file:

$ cat file.txt | cut -f2 | sort -u | wc -l

Number the fields in a tab-delimited header and display them as a column:

$ head -1 file.txt | tr "\t" "\n" | nl -b a

Find the key-binding for history-search-backward:

$ bind -P | grep history-search-backward

Display columns 2 through 4 of a file for rows such that the first column equals 1.

$ cat file.txt | awk '$1==1' | cut -f2-4

Find all the commands in your history with pipes:

$ history | grep "|" | less

In the previous section, I talked about my homemade alias n for notesappend. To flesh out this code snippet, the last command in history is the one we just typed:

$ history | tail -1
 1022  history | tail -1

We want one before the last:

$ echo Hello
Hello
$ history | tail -2 | head -1
 1023  echo Hello

The next part is subtle:

$ history | tail -2 | head -1 | tr -s ' '
 1023 echo Hello

The -s flag in tr stands for squeeze-repeats and the point of this is that there can be a varying number of space characters in the whitespace. Since we're going to cut on space as the delimiter, we have to make sure this doesn't trip us up. With this out of the way, we simply cut on space and use awk to put a pound sign in front of the command, so it's read as a comment:

$ history | tail -2 | head -1 | tr -s ' ' | cut -d' ' -f3- | awk '{print "# "$0}'
# echo Hello

One can always write a script to do something but some unix programmers like to rely on pipes to create long (sometimes unreadable) chains of commands, all the while staying on the same line. This is called a one-liner. I've witnessed some epic ones in my day!
Command Substitution TOP
Command substitution is another powerful technique that allows you to run a command on the fly and use its output as an argument for another command or store it in a variable. Let's look at the later case first. It's sometimes useful to store the current working directory in a variable. With command substitution, you can do it like this:

$ d=$( pwd )

$ d=`pwd`

These are two different syntaxes for doing the same thing. You should use the first one, because it's much cleaner and nicer (if you're a Perl user, you'll recognize the second one, which Perl shares). To take another example, suppose you want to store the length of your file in a variable:

$ len=$( cat file.txt | wc -l )

We can also nest command substitutions. In a script you often want to use a variable to store the directory in which the script itself resides. There might be other scripts in this directory you want your script to execute, even if the script cds into another location. To pull this out, use the line:

# save scripts directory in the variable d
d=$( dirname $( readlink -m $0 ) )

Recall that in a unix script $0 refers to the script itself. The readlink command is a fancy way of getting the absolute path of our script and dirname gets the directory part of the path. Neat, eh?

Let's look at the first thing we said command substitution could do, using the output of a command as an argument. To head all files with extension .txt in a directory, the command is:

$ head *.txt

We could be unnecessarily verbose and do this with command substitution as:

$ head $( ls *.txt )
$ head $( find . -maxdepth 1 -name "*.txt" )

You would never use these in practice, because there's a simpler way to do it. However, more often than not, command substitution is the shortcut. Let's say you want to look at myscript.pl and it's in your PATH but you can remember where it's located. Then you could use:

$ cat $( which myscript.pl )

Command substitution is also very useful in loops. For example, seq prints a sequence of numbers, so:

$ for i in $( seq 1 3 ); do echo $i; done
1
2
3

Question: What do the following do?

$ for i in $( cat file.txt | cut -f3 | sort -u ); do echo $i; done

$ for i in $( ls *.txt | grep -v apple ); do echo $i; done

Answer: The first loops through all unique elements of the third column of file.txt. Here, it just echoes it, but you could do anything. The second loops through all .txt files in the cwd that do not contain the word apple. Note that we're combining command substitution with pipes!

After a long road, we're finally in a better position to understand the code we discussed above to change file suffixes. To recap, if we make three text files:

$ touch {1..3}.txt

We can change their extension from .txt to .html like so:

$ for i in {1..3}.txt; do j=$( echo $i | sed 's|\.txt|\.html|' ); cmd="mv $i $j"; echo "Run command: $cmd"; echo $cmd | bash; done

This line features a trick: saving a command in a variable, cmd, allows us to echo it—showing the user what will be run—and then execute it by piping it into bash.

We can get as wacky as we like. For the first three directories in our PATH, the following tells us how many things are in each and how big each is:

$ for i in $( echo $PATH | tr ":" "\n" | head -3 ); do echo "*** "$i" ***"; echo "This folder has "$( ls $i | wc -l )" elements and is "$( du -sh $i | cut -f1 )" large"; echo; done
*** /usr/local/sbin ***
This folder has 0 elements and is 4.0K large

*** /usr/local/bin ***
This folder has 7 elements and is 32K large

*** /usr/sbin ***
This folder has 130 elements and is 8.6M large

Process Substitution TOP
Wikipedia nails the definition of Process substitution:

    ... process substitution is a form of inter-process communication that allows the input or output of a command to appear as a file. The command is substituted in-line, where a file name would normally occur, by the command shell. This allows programs that normally only accept files to directly read from or write to another program.

Let's take an example. Suppose the first line of your file is a header line, and you want to look at the tail of the file, but you also want to print the header. In that case, you could use:

$ cat <( head -1 file.txt ) <( tail file.txt )

cat expects files as arguments, but we're getting around that with process substitution. Whatever's in the block:
<( )
is treated as a file. Maybe this looks trivial to you, and you argue that you could do this just as well using:

$ head -1 file.txt; tail file.txt

You are correct. But what if you wanted to pipe all of this into another command (like column -t, which prints your file arranged into pretty columns)? Then you'd have to do it like this:

$ cat <( head -1 file.txt ) <( tail file.txt ) | column -t

So, is this the only way to do this? As long as I'm arguing with myself, I reiterate that bash is so elastic there's always another way to do something. Any ideas? Here's one answer:

$ { head -1 file.txt; tail file.txt; } | column -t

Curly brackets create code blocks in bash, as in many other languages. In this case, the code in the curly brackets is executed first and everything is piped, together, into column -t.

How would you print the second column in a file twice? One way would be with awk, which we'll cover below:

$ cat test.txt | awk '{print $2"\t"$2}'

However, you could also do this with process substitution:

$ paste <( cat test.txt | cut -f2 ) <( cat test.txt | cut -f2 )

although the first choice is clearly better.

Sometimes you want to sort a file, but you don't want the sorting to scramble your file header. Here's how to sort on, say, the first column without touching your header:

$ cat <( head -1 temp.txt ) <( cat temp.txt | sed '1d' | sort -k1,1n )

As a final example, suppose you have a simple script, test_script, which counts the lines in a file and echoes some text:

#!/bin/bash

myfile=$1

len=$( cat $myfile | wc -l )

echo "Your file is $len lines long."

The first argument is a file you pass in to the script—say, it's 1.txt—so you could run it like this:

$ ./test_script 1.txt
Your file is 11 lines long.

But what if you've zipped all your files to save space:

$ gzip 1.txt

The program can't handle zipped input, but unzipping your files just to run them in this program is a pain. Process substitution to the rescue!

$ ./test_script <( gunzip --stdout 1.txt.gz )
Your file is 11 lines long.

This gets at the marrow of what process substitution is really good at—avoiding the creation of temporary files.

If unix were a video game, piping would be level one, command substitution level two, and process substitution level three. Once you've gotten comfortable with all three, you've beaten at least one part of this game. Congratulations!
Interlude - Bell Laboratories 1982 Unix Video TOP
Now it's time for a fun and educational interlude. In 1982, Bell Labs AT&T produced a video touting the merits of unix. It features funky turtlenecks and futuristic, yet dated, geometrical figures doing an odd dance number. I don't recognize some of the unix commands they use. Yet, to me the funniest thing about this video is how relevant many of the principles in it still are (once you get past the part about telephone switchboards). Check it out:

(Video credit: YouTube: UNIX: Making Computers Easier To Use -- AT&T Archives film from 1982, Bell Laboratories)
Processes and Running Processes in the Background TOP
Processes are a deep subject intertwined with topics like memory usage, threads, scheduling, and parallelization. My understanding of this stuff—which encroaches on the domain of operating systems—is narrow, but here are the basics from a unix-eye-view. The command ps displays information about your processes:

$ ps     # show process info
$ ps -f  # show verbose process info

What if you have a program that takes some time to run? You run the program on the command line but, while it's running, your hands are tied. You can't do any more computing until it's finished. Or can you? You can—by running your program in the background. Let's look at the command sleep which pauses for an amount of time specified in seconds. To run things in the background, use an ampersand:

$ sleep 60 &
[1] 6846
$ sleep 30 &
[2] 6847

The numbers printed are the PIDs or process IDs, which are unique identifiers for every process running on our computer. Look at our processes:

$ ps -f
  UID   PID  PPID   C STIME   TTY           TIME CMD
  501  5166  5165   0 Wed12PM ttys008    0:00.20 -bash
  501  6846  5166   0 10:57PM ttys008    0:00.01 sleep 60
  501  6847  5166   0 10:57PM ttys008    0:00.00 sleep 30

The header is almost self-explanatory, but what's TTY? Wikipedia tells us that this is an anachronistic name for the terminal that derives from TeleTYpewriter. Observe that bash itself is a process which is running. We also see that this particular bash—PID of 5166—is the parent process of both of our sleep commands (PPID stands for parent process ID). Like directories, processes are hierarchical. Every directory, except for the root directory, has a parent directory and so every process, except for the first process—init in unix or launchd on the Mac—has a parent process. Just as tree shows us the directory hierarchy, pstree shows us the process hierarchy:

$ pstree
-+= 00001 root /sbin/launchd
 |-+= 00132 oliver /sbin/launchd
 | |-+= 00252 oliver /Applications/Utilities/Terminal.app/Contents/MacOS/Terminal
 | | \-+= 05165 root login -pf oliver
 | |   \-+= 05166 oliver -bash
 | |     |--= 06846 oliver sleep 30
 | |     |--= 06847 oliver sleep 60
 | |     \-+= 06848 oliver pstree
 | |       \--- 06849 root ps -axwwo user,pid,ppid,pgid,command

This command actually shows every single process on the computer, but I've cheated a bit and cut out everything but the processes we're looking at. We can see the parent-child relationships: sleep and pstree are children of bash, which is a child of login, which is a child of Terminal, and so on. With vanilla ps, every process we saw began in a terminal—that's why it had a TTY ID. However, we're probably running Safari or Chrome. How do we see these processes as well as the myriad others running on our system? To see all processes, not just those spawned by terminals, use the -A flag:

$ ps -A   # show all process info
$ ps -fA  # show all process info (verbose)

Returning to our example with sleep, we can see the jobs we're currently running with the command jobs:

$ jobs
[1]-  Running                 sleep 60 &
[2]+  Running                 sleep 30 &

What if we run our sleep job in the foreground, but it's holding things up and we want to move it to the background? Cntrl-z will pause or stop a job and the commands bg and fg set it running in either the background or the foreground.

$ sleep 60  # pause job with control-z
^Z
[1]+  Stopped                 sleep 60
$ jobs      # see jobs
[1]+  Stopped                 sleep 60
$ bg        # set running in background
[1]+ sleep 60 &
$ jobs      # see jobs
[1]+  Running                 sleep 60 &
$ fg        # bring job from background to foreground
sleep 60

We can also kill a job:

$ sleep 60 &
[1] 7161
$ jobs
[1]+  Running                 sleep 60 &
$ kill %1
$
[1]+  Terminated: 15          sleep 60

In this notation %n refers to the nth job. Recall we can also kill a job in the foreground with Cntrl-c. More generally, if we didn't submit the command ourselves, we can kill any process on our computer using the PID. Suppose we want to kill the terminal in which we are working. Let's grep for it:

$ ps -Af | grep Terminal
  501   252   132   0 11:02PM ??         0:01.66 /Applications/Utilities/Terminal.app/Contents/MacOS/Terminal
  501  1653  1532   0 12:09AM ttys000    0:00.00 grep Terminal

We see that this particular process happens to have a PID of 252. grep returned any process with the word Terminal, including the grep itself. We can be more precise with awk and see the header, too:

$ ps -Af | awk 'NR==1 || $2==252'
  UID   PID  PPID   C STIME   TTY           TIME CMD
  501   252   132   0 11:02PM ??         0:01.89 /Applications/Utilities/Terminal.app/Contents/MacOS/Terminal

(that's print the first row OR anything with the 2nd field equal to 252.) Now let's kill it:

$ kill 252

poof!—our terminal is gone.

Running stuff in the background is useful, especially if you have a time-consuming program. If you're scripting a lot, you'll often find yourself running something like this:

$ script.py > out.o 2> out.e &

i.e., running something in the background and saving both the output and error.

Two other commands that come to mind are time, which times how long your script takes to run, and nohup ("no hang up"), which allows your script to run even if you quit the terminal:

$ time script.py > out.o 2> out.e &
$ nohup script.py > out.o 2> out.e &

As we mentioned above, you can also set multiple jobs to run in the background, in parallel, from a loop:

$ for i in 1 2 3; do { echo "***"$i; sleep 60 & } done

(Of course, you'd want to run something more useful than sleep!) If you're lucky enough to work on a large computer cluster shared by many users—some of whom may be running memory- and time-intensive programs—then scheduling different users' jobs is a daily fact of life. At work we use a queuing system called the Sun Grid Engine to solve this problem. I wrote a short SGE wiki here.

To get a dynamic view of your processes, loads of other information, and sort them in different ways, use top:

$ top

Here's a screenshot of htop—a souped-up version of top—running on Ubuntu:

image

htop can show us a traditional top output split-screened with a process tree. We see various users—root (discussed next), ubuntu, and www-data—and we see various processes, including init which has a PID of 1. htop also shows us the percent usage of each of our cores—here there's only one and we're using just 0.7%. Can you guess what this computer might be doing? I'm using it to host a website, as nginx, a popular web server, gives away. To echo a point made at the beginning of this article, this is one of the zillion doors basic command line competence opens.
sudo and the Root User TOP
sudo and the Root User sounds like one of Aesop's Fables, but the moralist never considered file permissions and system administration a worthy subject. We saw above that, if you're unsure of your user name, the command whoami tells you who you're logged in as. If you list the files in the root directory:

$ ls -hl /

you'll notice that these files do not belong to you but, rather, have been created by another user named root. Did you know you were sharing your computer with somebody else? You're not exactly, but there is another account on your computer for the root user who has, as far as the computer's concerned, all the power (read Wikipedia's discussion about the superuser here). It's good that you're not the root user by default because it protects you from yourself. You don't have permission to catastrophically delete an important system file.

If you want to run a command as the superuser, you can use sudo. For example, you'll have trouble if you try to make a directory called junk in the root directory:

$ mkdir /junk
mkdir: cannot create directory ‘/junk’: Permission denied

However, if you invoke this command as the root user, you can do it:

$ sudo mkdir /junk

provided you type in the password. Because root—not your user—owns this file, you also need sudo to remove this directory:

$ sudo rmdir /junk

If you want to experience life as the root user, try:

$ sudo -i

Here's what this looks like on my computer:

$ whoami	# check my user name
oliver
$ sudo -i	# simulate login as root
Password:
$ whoami	# check user name now
root
$ exit		# logout of root account
logout
$ whoami	# check user name again
oliver

Obviously, you should be cautious with sudo. When might using it be appropriate? The most common use case is when you have to install a program, which might want to write into a directory root owns, like /usr/bin, or access system files. I discuss installing new software below. You can also do terrible things with sudo, such as gut your whole computer with a command so unspeakable I cannot utter it in syntactically viable form. That's sudo are em dash are eff forward slash—it lives in infamy in an Urban Dictionary entry.
awk TOP
awk and sed are command line utilities which are themselves programming languages built for text processing. As such, they're vast subjects as these huge manuals—GNU Awk Guide, Bruce Barnett's Awk Guide, GNU Sed Guide—attest. Both of these languages are almost antiques which have been pushed into obsolescence by Perl and Python. For anything serious, you probably don't want to use them. However, their syntax makes them useful for simple parsing or text manipulation problems that crop up on the command line. Writing a simple line of awk can be faster and less hassle than hauling out Perl or Python.

The key point about awk is, it works line by line. A typical awk construction is:
cat file.txt | awk '{ some code }'
Awk executes its code once every line. Let's say we have a file, test.txt, such that:

$ cat test.txt
1	c
3	c
2	t
1	c

In awk, $1 is the notation for the first field, $2 is for second field, and so on. The whole line is $0. For example:

$ cat test.txt | awk '{print}'     # print full line
1	c
3	c
2	t
1	c

$ cat test.txt | awk '{print $0}'  # print full line
1	c
3	c
2	t
1	c

$ cat test.txt | awk '{print $1}'  # print column 1
1
3
2
1

$ cat test.txt | awk '{print $2}'  # print column 2
c
c
t
c

There are two exceptions to the execute code per line rule: anything in a BEGIN block gets executed before the file is read and anything in an END block gets executed after it's read. If you define variables in awk they're global and persist rather than being cleared every line. For example, we can concatenate the elements of the first column with an @ delimiter using the variable x:

$ cat test.txt | awk 'BEGIN{x=""}{x=x"@"$1; print x}'
@1
@1@3
@1@3@2
@1@3@2@1

$ cat test.txt | awk 'BEGIN{x=""}{x=x"@"$1}END{print x}'
@1@3@2@1

Or we can sum up all values in the first column:

$ cat test.txt | awk '{x+=$1}END{print x}'  # x+=$1 is the same as x=x+$1
7

Awk has a bunch of built-in variables which are handy: NR is the row number; NF is the total number of fields; and OFS is the output delimiter. There are many more you can read about here. Continuing with our very contrived examples, let's see how these can help us:

$ cat test.txt | awk '{print $1"\t"$2}'        # write tab explicitly
1	c
3	c
2	t
1	c

$ cat test.txt | awk '{OFS="\t"; print $1,$2}' # set output field separator to tab
1	c
3	c
2	t
1	c

Setting OFS spares us having to type a "\t" every time we want to print a tab. We can just use a comma instead. Look at the following three examples:

$ cat test.txt | awk '{OFS="\t"; print $1,$2}'        # print file as is
1	c
3	c
2	t
1	c

$ cat test.txt | awk '{OFS="\t"; print NR,$1,$2}'     # print row num
1	1	c
2	3	c
3	2	t
4	1	c

$ cat test.txt | awk '{OFS="\t"; print NR,NF,$1,$2}'  # print row & field num
1	2	1	c
2	2	3	c
3	2	2	t
4	2	1	c

So the first command prints the file as it is. The second command prints the file with the row number added in front. And the third prints the file with the row number in the first column and the number of fields in the second—in our case always two. Although these are purely pedagogical examples, these variables can do a lot for you. For example, if you wanted to print the 3rd row of your file, you could use:

$ cat test.txt | awk '{if (NR==3) {print $0}}'  # print the 3rd row of your file
2       t

$ cat test.txt | awk '{if (NR==3) {print}}'     # same thing, more compact syntax
2       t

$ cat test.txt | awk 'NR==3'                    # same thing, most compact syntax
2       t

Sometimes you have a file and you want to check if every row has the same number of columns. Then use:

$ cat test.txt | awk '{print NF}' | sort -u
2

In awk $NF refers to the contents of the last field:

$ cat test.txt | awk '{print $NF}'
c
c
t
c

An important point is that by default awk delimits on white-space, not tabs (unlike, say, the command cut). White space means any combination of spaces and tabs. You can tell awk to delimit on anything you like by using the -F flag. For instance, let's look at the following situation:

$ echo "a b" | awk '{print $1}'
a

$ echo "a b" | awk -F"\t" '{print $1}'
a b

When we feed a space b into awk, $1 refers to the first field, a. However, if we explicitly tell awk to delimit on tabs, then $1 refers to a b because it occurs before a tab.

You can also use shell variables inside your awk by importing them with the -v flag:

$ x=hello
$ cat test.txt | awk -v var=$x '{ print var"\t"$0 }'
hello	1       c
hello	3       c
hello	2       t
hello	1       c

And you can write to multiple files from inside awk:

$ cat test.txt | awk '{if ($1==1) {print > "file1.txt"} else {print > "file2.txt"}}'

$ cat file1.txt
1       c
1       c

$ cat file2.txt
3       c
2       t

Question: In the following case, how would you print the row numbers such that the first field equals the second field?

$ echo -e "a\ta\na\tc\na\tz\na\ta"
a	a
a	c
a	z
a	a

Here's the answer:

$ echo -e "a\ta\na\tc\na\tz\na\ta" | awk '$1==$2{print NR}'
1
4

The take-home lesson is, you can do tons with awk, but you don't want to do too much. Anything that you can do crisply on one, or a few, lines is awk-able. I'll do some more involved examples below so you can get a better sense of awk scripting.
sed TOP
Sed, like awk, is a full-fledged language that is convenient to use in a very limited sphere (GNU Sed Guide). I only use it for two things: (1) replacing text, and (2) deleting lines. Sed is often mentioned in the same breath as regular expressions (discussed below) although, like the rest of the world, I'd use Perl and Python when it comes to that. Nevertheless, let's see what sed can do.

Sometimes the first line of a text file is a header and you want to remove it. Suppose we have a file, test_header.txt, such that:

$ cat test_header.txt
This is a header
1	asdf
2	asdf
2	asdf

Then:

$ cat test_header.txt | sed '1d'    # delete the first line
1	asdf
2	asdf
2	asdf

To remove the first 3 lines:

$ cat test_header.txt | sed '1,3d'  # delete lines 1-3
2	asdf

1,3 is sed's notation for the range 1 to 3. We can't do much more without entering regular expression territory. One sed construction is:
/pattern/d
where d stands for delete if the pattern is matched. If we have a file, test_comment.txt, such that:

$ cat test_comment.txt
1	asdf
# This is a comment
2	asdf
# This is a comment
2	asdf

We can remove lines beginning with # like so:

$ cat test_comment.txt | sed '/^#/d'
1	asdf
2	asdf
2	asdf

Another construction is:
s/A/B/
where s stands for substitute. So this means replace A with B. By default, this only works for the first occurrence of A, but if you put a g at the end, for group, all As are replaced:
s/A/B/g
For example, the following replaces the first occurrence of kitty with X:

$ echo "hello kitty. goodbye kitty" | sed 's/kitty/X/'
hello X. goodbye kitty

Using a vertical bar ( | ) as a separator, instead of a slash, is okay:

$ echo "hello kitty. goodbye kitty" | sed 's|kitty|X|'
hello X. goodbye kitty

To replace all occurrences of kitty with X, we can do:

$ echo "hello kitty. goodbye kitty" | sed 's/kitty/X/g'
hello X. goodbye X

This is such a useful ability that all text editors allow you to perform find-and-replace as well. By replacing some text with nothing, you can also use this as a delete:

$ echo "hello kitty. goodbye kitty" | sed 's|kitty||'
hello . goodbye kitty

$ echo "hello kitty. goodbye kitty" | sed 's|kitty||g'
hello . goodbye

Sed is especially good when you're trying to rename batches of files or directories on the command line. I often have occasion to use it in for loops. This example of changing file extensions should be very familiar by now:

$ touch file{1..3}.txt
$ for i in file{1..3}.txt; do j=$( echo $i | sed 's|.txt|.html|'); mv $i $j; done
$ ls
file1.html  file2.html	file3.html

More awk Examples TOP
Let's do some in depth examples with awk. This section gets into gory details so, if you're just here to learn the standard command line, you can skip it with impunity.

Example 1
Suppose we have some files that start with the prefix myfile and we want to concatenate them together. However, in the resulting file, we want the first column to be the name of the file from which that row originated. We can accomplish this as follows:

$ for i in myfile*; do echo "*** "$i" ***"; cat $i | awk -v x=${i} '{print x"\t"$0}' >> files.concat.txt; done

Example 2
Suppose we have a text file of URLs, test_markup.txt:

$ cat test_markup.txt
https://www.google.com
http://www.nytimes.com
http://en.wikipedia.org/wiki/Main_Page

and we want to convert them into HTML links. This is easy with awk:

$ cat test_markup.txt | awk '{print "<a href=\""$1"\">"$1"</a><br>"}'
<a href="https://www.google.com">https://www.google.com</a><br>
<a href="http://www.nytimes.com">http://www.nytimes.com</a><br>
<a href="http://www.wikipedia.org">http://www.wikipedia.org</a><br>

Notice that we've escaped the quote character with a slash where necessary.

Example 3
Here's an example from work: the other day I ran multiple instances of a script and had 500 input and output files. I wanted to check that the number of unique elements in the first column of each corresponding input and output file was the same. Here was my one-liner:

$ for i in {1..500}; do a=$( cat input${i}.txt | cut -f1 | sort -u | wc -l ); b=$( cat output${i}.txt | cut -f1 | sort -u | wc -l ); echo -e $i"\t"$a"\t"$b; done | awk '$2!=$3'

Let's make this more readable:

$ for i in {1..500}; do
      a=$( cat input${i}.txt | cut -f1 | sort -u | wc -l );
      b=$( cat output${i}.txt | cut -f1 | sort -u | wc -l );
      echo -e $i"\t"$a"\t"$b;
  done | awk '$2!=$3'	# print if col2 not equal to col3

So, any time these numbers disagreed, awk printed the line.

Example 4
Now let's take a detour into the world of bioinformatics, a field in which studying sequencing data is one of the chief pursuits. (Because bioinformatics relies on numerous different standard, parsable file formats, it's perhaps the best Petri dish ever created for learning bash, Perl, Python, awk, and sed.) For this example, all you need to know is that a fasta file is one type of file format in which sequencing data is stored. In fasta format, every sequence has an ID line, which begins with > followed by some sequence, which is allowed to span multiple lines. For DNA, the sequence is comprised of the letters A C T G (also called base pairs or nucleotides). A fasta file of two genes could look like this:

$ cat myfasta.fa
>GeneA
ATGCTGAAAGGTCGTAGGATTCGTAG
>GeneB
ATGAACGTAA

(if genes were this small) Suppose we want to create a file with ID vs length. In this example, it would be:

$ cat myfasta.fa | awk '{if ($1 ~ />/) {printf $1"\t"} else {print length}}' | sed 's|>||'
GeneA	26
GeneB	10

Note that length is a keyword in awk.

Another common chore is filtering a fasta file. Sometimes we want to ignore small sequences—say, anything 20 or fewer nucleotides—because either we don't believe they're real or because we'll have trouble aligning them. This is simply:

$ cat myfasta.fa | awk '{if ($0 ~ />/) {id=$0} else if (length > 20) {print id; print}}'
>GeneA
ATGCTGAAAGGTCGTAGGATTCGTAG

To be 100% accurate, the sequence portions of a fasta file can spill over onto more than one line and the above examples don't account for this. We can handle this by first piping our fasta file into:

$ cat myfasta.fa | awk 'BEGIN{f=0}{if ($0~/^>/) {if (f) printf "\n"; print $0; f=1} else printf $0}END{printf "\n"}'

and then piping the result into what we have above.

Here is a more difficult problem. When the sequencing machine does its magic, sometimes it can't make a call what the base is, so instead of writing A C T or G it uses the character N to denote an unknown. Suppose you have a fasta file—perhaps the sequences are thousands of base pairs long—and you want to know where the coordinates of these stretches of Ns are. As a test case, let's look at the following miniature fasta file:

$ cat test.fa
>a
ACTGNNNAGGTNNNA
>b
NNACTGNNNAGGTNN

In the long tradition of one-liners, here's what I wrote to solve this problem:

$ cat test.fa | awk 'BEGIN{flag=0}{if ($0 ~ />/) {if (flag==1) {print nstart"\t"nend;}; print; pos=0; flag=0} else {for (i=1; i<=length; i++) { pos++; c=substr($0,i,1); if (c=="N" && flag==0) {nstart=pos; nend=pos; flag=1;} else if (c=="N") {nend=pos} else if (c!="N" && flag==1) {print nstart"\t"nend; flag=0}}}}END{if (flag==1) {print nstart"\t"nend;}}'

Got that? Probably not, because the strength of one-liners has never been readability. Let's expand this line so we can see what it's doing:

$ cat test.fa | awk 'BEGIN{flag=0} {
  if ($0 ~ />/) # ID line
  {
      if (flag==1) {print nstart"\t"nend;};
      # print ID, set position to 0, flag to 0
      print;
      pos=0;
      flag=0;
  }
  else # sequence line
  {
      # loop thro sequence
      for (i=1; i<=length; i++)
      {
          # increment position
          pos++;
          # grab the i-th letter
          c=substr($0,i,1);

          # set position if char == N
          # flag will raise hi if we hit an N char
          if (c=="N" && flag==0) { nstart=pos; nend=pos; flag=1; }
          else if (c=="N") { nend=pos }
          else if (c!="N" && flag==1) { print nstart"\t"nend; flag=0; }
      } # for loop
  }}END{if (flag==1) {print nstart"\t"nend;}}'
>a
5       7
12      14
>b
1       2
7       9
14      15

Looks like we got the ranges right! Let's talk through this.

In the case we're on an ID line, we reset our position variable and our flag. The flag is a boolean (meaning it will be either 1, hi, or 0, low) which we're going to set hi every time we see an N. This plays out in the following way: once we hit a sequence line, we're going to loop over every single character. If the character is an N and the flag is low—meaning the previous character was not an N—then we record this position, pos, as being both the start and end of an N streak: nstart=pos and nend=pos. If the character is an N and the flag is hi, it means the previous character was an N—hence, we're in the middle of a streak of Ns—so the start position is whatever it was when we saw the first N and we just have to update the end position. If the character is not an N but the flag is hi, it means the previous character was an N and we just finished going through a streak, so we'll print the range of the streak and set the flag low to signify we're no longer in a streak.

There's one more subtlety: what if the sequence line ends on an N character? Then we won't end up printing it because our logic only prints things the next time we see a non-N. To solve this issue, we add a line in the if (line == ID line) block to check if our flag is hi. If it is, we print the last-seen range before clearing the variables. And there's an even more subtle point: what if the last line of our file ends on an N? In this case, that fix won't work because we won't be hitting any more ID lines. To solve this, we use the END{ } block: if the flag is hi and we're done reading the file, we'll print the last-seen range. In this example, our fasta file was small and we could eyeball the N ranges but, with a monster file, we'd need to trust our awk rather than our eyes.

Example 5
Here's a final example, leaving the world of bioinformatics. Suppose you want to add numbers above each column at the top of a text file. If your file looks like this:

hello	kitty	kitty
hello	kitty	kitty

then the goal is to make it look like this:

1	2	3
hello	kitty	kitty
hello	kitty	kitty

Easy, right? It's actually not trivial because a long word in one of the columns is going to make it so you can't simply print the numbers separated by tabs if you want them to line up with the columns. To get the spacing right, you might need more than one tab in some cases. So, let's awk it:

$ cat file.txt | awk -F"\t" '{if (NR==1) { for (i=1; i<=NF; i++) {printf i; for (j=1; j<=int(length($i)/8); j++) {printf "\t"}; if (i==NF) {printf "\n"} else {printf "\t"}}; print $0 } else {print $0}}'

Let's make this readable:

$ cat file.txt | awk -F"\t" '{
  if (NR==1)  # if first line
  {
      # loop thro the number of fields
      for (i=1; i<=NF; i++)
      {
          # print number with no tab or newline
          printf i;

          # use the fact a tab is 8 characters
          # print extra tabs for long words
          for (j=1; j<=int(length($i)/8); j++) { printf "\t" };

          # if last field, print newline; otherwise, print tab
          if (i==NF) { printf "\n" } else { printf "\t" }
      };

      # print first line
      print $0
  }
  else  # if not first line, simply print
  {
      print $0
  }}'

What's going on? First, we're going to use the first row only (NR==1) and any other row is printed as is. To number the columns, we iterate through the number of tab-delimited fields, NF. There's a word in the i-th field, and we add int(length($i)/8) extra tabs. This is because we need an new tab every eight characters: if the word is 6 letters long, we don't need any extra tabs, but if it's 12 letters we need one. Then for every field we add one tab unless we're on the last field (i==NF), in which case we add a newline. Finally, we print the first line as is.
Regular Expressions and Globbing in Bash TOP
Regular Expressions (regex for short) are a way of describing patterns in text—and once you've gone to the trouble of describing a pattern, you can write code to match it, extract some piece of it, or parse it in just about any way you like. Regex come up in so many walks of programming that it's critically important to understand the basics, even if you're not a guru.

What do the following have in common?

tttxc234
wer1
asfwaffffffff2342525

All follow the pattern: some number of letter characters followed by some number of numerical characters. You could use a regex to test if a string matches this pattern or to grab the numerical part of any text that fits this pattern.

What do the following have in common?

xd2@joe.com
carlos_danger@gmail.com
hellokitty@yahoo.com

all follow the pattern: string of non-@ characters followed by one @ followed by a string of non-@ characters. You can imagine that a form on the internet which requires an email address uses a regex to verify that it follows this pattern.

Bash can do regex—read about it on The Linux Documentation Project—but don't waste much time with it. The syntax is hairy and Perl and Python were born for this, so use them (as we'll discuss next). However, bash is good at something whose orbit isn't too far from regex and which we've already seen a lot of: globbing. By now, you're very familiar with the asterisk ( * ) as a wildcard:

$ touch A1f A2a A3c A4d A5a B5x	# create files
$ ls				# list everything
A1f  A2a  A3c  A4d  A5a  B5x
$ ls A{2..5}*			# list files beginning with A2 through A5
A2a  A3c  A4d  A5a

And you know from above that these constructions are handy in loops. In the next section, to confuse you, we'll see that asterisk means something different in the regex context.
Command Line Perl and Regex TOP
We've met the scripting language Perl already. Although it's falling out of favor these days—and it's definitely better to invest your time in Python if you're a beginning programmer (IMHO:)—Perl has always had a good reputation for regex. For us on the command line, it has another selling point: Perl fits easily into unix pipelines. You can make Perl run on the command line and execute code line by line using the flags -ne:
cat file.txt | perl -ne '{ some code }'
This makes Perl behave just like awk—and it obeys some of the same conventions, such as using the BEGIN and END keywords. You can read more about Perl's command line options here and in even gorier detail here, but let's see how to use it. Suppose you have a text file and you want to format it as an HTML table:

$ cat test_table.txt
x	y	z
1	2	3
a	b	c

Doing this by hand would be pure torture. Let's do it with a one-liner on the command line:

$ cat test_table.txt | perl -ne 'BEGIN{print "<table border=\"1\">\n";}{chomp($_); my @line=split("\t",$_); print "<tr>"; foreach my $elt (@line) { print "<td>$elt</td>"; } print "</tr>\n";}END{print "</table>\n";}'i

Expanding this for readability:

$ cat test_table.txt | perl -ne 'BEGIN{print "<table border=\"1\">\n";}{
      chomp($_);
      my @line=split("\t",$_);
      print "<tr>";
      foreach my $elt (@line) { print "<td>$elt</td>"; }
      print "</tr>\n";
  }END{print "</table>\n";}'
<table border="1">
<tr><td>x</td><td>y</td><td>z</td></tr>
<tr><td>1</td><td>2</td><td>3</td></tr>
<tr><td>a</td><td>b</td><td>c</td></tr>
</table>

All we're doing here is embedding each line in a table row (tr) tag, and each field in a table data (td) tag, plus printing table tags at the beginning and end of the file.

If we have to deal with nontrivial regex on the command line, we'll be glad we're using Perl, not bash or awk. Somewhere off the internet, I stole this regex cheat sheet:


Syntax	Equivalent Syntax	What It Represents

\d	[0-9]	Any digit

\D	[^0-9]	Any character not a digit

\w	[0-9a-zA-Z_]	Any "word character"

\W	[^0-9a-zA-Z_]	Any character not a word character

\s	[ \t\n\r\f]	whitespace (space, tab, newline, carriage return,
form feed)

\S	[^ \t\n\r\f]	Any non-whitespace character

.		Any character except newline


If we think of the above as nouns, we can think of the following as adjectives:


Quantifiers, etc.	What It Means

*	Match 0 or more times

+	Match 1 or more times

?	Match 1 or 0 times

{n}	Match exactly n times

{n,}	Match at least n times

{n,m}	Match at least n but not more than m times

^	Match at the beginning of a line

$	Match at the end of a line


To get a feeling for how to use these, let's take an example file such that:

$ cat test.txt
889
tttxc234
wer1
CAT
asfwaffffffff2342525

Everything obeys the pattern non-digit string digit string except for 889, just digits, and CAT, just non-digits. Look at the following:

$ cat test.txt | perl -ne '{chomp($_); if ($_ =~ m/(\d*)/) {print $_,"\n";}}'
889
tttxc234
wer1
CAT
asfwaffffffff2342525

In Perl, the syntax:
some value =~ m/regular expression/
tests for a match against a regular expression. Referring to our cheat sheet, the above command prints every row because every row has at least 0 digits. Let's change the asterisk to a plus sign:

$ cat test.txt | perl -ne '{chomp($_); if ($_ =~ m/(\d+)/) {print $_,"\n";}}'
889
tttxc234
wer1
asfwaffffffff2342525

This prints everything with at least 1 digit, which is every row except CAT. Let's invert this and print the rows with non-digits:

$ cat test.txt | perl -ne '{chomp($_); if ($_ =~ m/(\D+)/) {print $_,"\n";}}'
tttxc234
wer1
CAT
asfwaffffffff2342525

This prints everything with at least 1 non-digit, which is every row except 889. We can try to match a more specific pattern:

$ cat test.txt | perl -ne '{chomp($_); if ($_ =~ m/(\d+)(\D+)/) {print $_,"\n";}}'
$

This prints everything with the pattern at least 1 digit, at least 1 non-digit, which no rows follow. What about this?

$ cat test.txt | perl -ne '{chomp($_); if ($_ =~ m/(\D+)(\d+)/) {print $_,"\n";}}'
tttxc234
wer1
asfwaffffffff2342525

It prints everything with the pattern at least 1 non-digit, at least 1 digit, which three rows follow.

We can also grab pieces of our regular expression as follows:

$ cat test.txt | perl -ne '{chomp($_); if ($_ =~ m/(\D+)(\d+)/) {print $1,"\n";}}'
tttxc
wer
asfwaffffffff

$ cat test.txt | perl -ne '{chomp($_); if ($_ =~ m/(\D+)(\d+)/) {print $2,"\n";}}'
234
1
2342525

$1 refers to the piece in the first ( ), $2 the second, and so on.

Let's take another example, the one with emails. You have a file such that:

$ cat mail.txt
xd2@joe.com
malformed.hotmail.com
malformed@@hotmail.com
carlos_danger@gmail.com
hellokitty@yahoo.com

Then to get the strings that are appropriately formatted as emails, we could do the following:

$ cat mail.txt | perl -ne '{chomp($_); if ($_ =~ m/(\w+)@(\w+)/) {print $_,"\n";}}'
xd2@joe.com
carlos_danger@gmail.com
hellokitty@yahoo.com

$ cat mail.txt | perl -ne '{chomp($_); if ($_ =~ m/(\w+)\@{1}(\w+)/) {print $_,"\n";}}'
xd2@joe.com
carlos_danger@gmail.com
hellokitty@yahoo.com

These do the same thing, but we're being a little more explicit in the second case. Escaping the @ sign with a slash isn't a bad idea because in Perl @ can denote an array. If we wanted to grab lines with two @s, the syntax would be:

$ cat mail.txt | perl -ne '{chomp($_); if ($_ =~ m/(\w+)\@{2}(\w+)/) {print $_,"\n";}}'
malformed@@hotmail.com

Question: What would this do?

$ cat mail.txt | perl -ne '{chomp($_); if ( $_ =~ m/(\w+)(\@+)(\w+)/) {print $2,"\n";}}'

Answer:

$ cat mail.txt | perl -ne '{chomp($_); if ( $_ =~ m/(\w+)(\@+)(\w+)/) {print $2,"\n";}}'
@
@@
@
@

Aside from doing matching and extracting pieces of patterns with regex, you can also do substitutions, use variables and logic, and more. Read more about Perl regex here and read about Python regex here. I wrote a short (unpolished) Perl Wiki which also has some more examples here.
Text Editors Revisited: Vim TOP
By now, you've accepted the command line into your heart. But something's still holding you back, slowing you down, sabotaging your true potential—keeping you from becoming the man or woman you want to be. This invisible drag on your abilities is the lack of a good text editor. We touched on the subject of text editors before but, now that you're a more advanced user, you've probably realized that you spend at least half of your time in the terminal editing code or text. For serious business, nano is woefully inadequate. The solution is to use either Vim, the subject of this section, or Emacs.

Borrowing a bit from my Vim wiki, Vim is a powerful text editor that allows you to do almost anything you can dream up in a text file. It has so many commands, you can almost think of it as a text editor-cum-programming language. One of the nicest things about Vim is that it's always available in your terminal. If you use a GUI text editor, like Sublime or Aquamacs, then every time you switch computers, you have to make sure you've installed the program. If you've ssh-ed into a remote server and you're trying to edit a file with one of these GUI text editors, then you have to locally mount the server to edit the file—another headache. If these two reasons aren't compelling enough to switch to Vim, it's also a good editor in its own right.

The downside is that Vim isn't the easiest thing to learn, and it sometimes seems geared towards those with a love of the technical. But there is an extensive user manual, a Tips Wiki, and vim.org, which admirably states:

    The most useful software is sometimes rendered useless by poor or altogether missing documentation. Vim refuses to succumb to death by underdocumentation.

(The manual weighs in at over 250 pages—mission accomplished!) Vim is such a big subject that the goal of this section will simply be to get your feet wet and set you pointing in the right direction.

Here's a random snippet of the utility wc's source code (written in C) edited in Vim:

image

The yellow numbers on the left are line numbers, not part of the document. What about the word INSERT you see at the bottom? The first lesson of Vim is that it has modes. In insert mode, you write text into your document, just as in any other editor. But in normal mode, where you start when you open Vim, you issue commands to the editor. To leave normal mode and enter insert mode, you have various choices, including:

i	enter insert mode
I	enter insert mode at the beginning of the line
a	enter insert mode one character after the cursor
A	enter insert mode at the end of the line
o	create new line (below cursor), enter insert mode at the beginning of it
O	create new line (above cursor), enter insert mode at the beginning of it

To get back into normal mode, use:

Ctrl-c	return to normal mode
Esc	return to normal mode

If you type a colon ( : ) in normal mode, you enter command mode (technically called command-line mode, but not to be confused with the unix command line) where you can enter syntactically more complex commands at the prompt. Delete the colon to return to normal mode. If you type a v in normal mode, you toggle visual mode, in which you can highlight text. For this section, I'll assume you're in normal mode (when this is not quite true, I'll use the notation :somecommand instead of saying, more ponderously, go into command-line mode and enter somecommand).

To save and/or quit, use:
:w	save
:q	quit
:wq	save and quit
:q!	quit without saving

Some basic commands to navigate through your file are:

gg	jump to top of file
G	jump to bottom of file
Cntrl-u	move up a chunk
Cntrl-d	move down a chunk
W	jump cursor forward on whitespace
w	jump cursor forward on special characters
B	jump cursor backward on whitespace
b	jump cursor backward on special characters
27gg	go to line 27
:27	go to line 27

Here are some basic copying (or "yanking") and pasting commands:

dd	delete line (and store in default register)
yy	copy or yank line (into default register)
d0	delete everything from cursor to beginning of line (into default register)
d$	delete everything from cursor to end of line (into default register)
p	paste (from default register) after cursor
P	paste (from default register) before cursor

To undo or redo the previous command, use:

u	undo
Cntrl-r	redo

To find text in Vim, type a slash ( / ) followed by what you're searching for. To step through each instance of what you found, it's:

n	find next instance
N	find prev instance

This completes the whirlwind tour. Consider yourself officially weaned off of nano. For further reading, I put together a quick and dirty Vim wiki here.
Example Problems on the Command Line TOP
Pulling together everything we've learned, let's look at some examples of working on the command line. As usual, we'll meet some new commands as we go.

Problem 1
Question: How do we print the most recently modified (or created) file in the cwd?

Answer: ls has a -t flag, which sorts "by time modified (most recently modified first)", so the solution is simply:

$ ls -t | head -1

Problem 2
Question: How do we print the number of unique elements in column 3 (delimiting on tab) of a text file? For example, suppose tmp.txt is:

$ cat tmp.txt
1       aa      3
1       34      z
1       f       32
2       3r      z
2       d       cc
3       d       34
x       e       cc
x       1       z

Answer: We can accomplish this with a simple pipeline using the -u flag of sort to sort column 3 uniquely:

$ cat tmp.txt | cut -f3 | sort -u | wc -l
5

Problem 3
Question: How do we print only the odd-numbered rows of a file? For example, suppose tmp.txt is:

$ cat tmp.txt
aaa
bbb
ccc
ddd
eee
fff
ggg
hhh
iii
jjj

Hint: Use awk.

Answer: Let's explicitly list the row number as well as the row number mod 2:

$ cat tmp.txt | awk '{print NR"\t"NR%2"\t"$0}'
1       1       aaa
2       0       bbb
3       1       ccc
4       0       ddd
5       1       eee
6       0       fff
7       1       ggg
8       0       hhh
9       1       iii
10      0       jjj

Now the solution is obvious:

$ cat tmp.txt | awk 'NR%2==1'
aaa
ccc
eee
ggg
iii

Problem 4
Question: Given two files, how do you find the rows that are only in one of them? For example, suppose file1.txt is:

$ cat file1.txt
1
200
324
95
10
a b c

and file2.txt is:

$ cat file2.txt
3
1
200
324
95

Every row in the first file is somewhere in the second file except for the rows with 10 and a b c.

Hint: Use uniq.

Answer: To find the rows that are unique to the first file, try:

$ cat file1.txt file2.txt file2.txt | sort | uniq -u
10
a b c

Every row in file2.txt is duplicated because we cat the file twice. And every row file1.txt and file2.txt share will appear at least 3 times. Then we pipe this into uniq -u which will output only unique rows for a sorted file.

Problem 5
My friend, Albert, gave me this elegant example. Here are the first 300 bases of chromosome 17 of the human genome (build GRCh37) in a file chr17_300bp.fa:

>17 dna:chromosome chromosome:GRCh37:17:1:81195210:1 REF
AAGCTTCTCACCCTGTTCCTGCATAGATAATTGCATGACAATTGCCTTGTCCCTGCTGAA
TGTGCTCTGGGGTCTCTGGGGTCTCACCCACGACCAACTCCCTGGGCCTGGCACCAGGGA
GCTTAACAAACATCTGTCCAGCGAATACCTGCATCCCTAGAAGTGAAGCCACCGCCCAAA
GACACGCCCATGTCCAGCTTAACCTGCATCCCTAGAAGTGAAGGCACCGCCCAAAGACAC
GCCCATGTCCAGCTTATTCTGCCCAGTTCCTCTCCAGAAAGGCTGCATGGTTGACACACA

Question: How would you count the number of As, Ts, Cs, and Gs in this sequence?

Hint: Use fold.

Answer: We can discard the identifier line with a grep -v ">". The command fold restricts the number of characters printed per line, allowing us to turn a row into a column, as in:

$ cat chr17_300bp.fa | grep -v ">" | fold -w 1 | head
A
A
G
C
T
T
C
T
C
A

Now we can sort this file, so all the A, T, C, and G rows go together, and then count them with uniq -c:

$ cat chr17_300bp.fa  | grep -v ">" | fold -w 1 | sort | uniq -c
     73 A
    100 C
     63 G
     64 T

Problem 6
Changing a text file from one format into another is a common scripting chore. Suppose you have a file, example_data.txt, that looks like this:

,height,weight,salary,age
1,106,111,111300,62
2,124,91,79740,40
3,127,176,15500,46

Question: How would you change its format into this:

1       height  106
2       height  124
3       height  127
1       weight  111
2       weight  91
3       weight  176
1       salary  111300
2       salary  79740
3       salary  15500
1       age     62
2       age     40
3       age     46

?
These two different styles are sometimes called wide format data and narrow (or long) format data. (If you're familiar with the language R, the package reshape2 can toggle between these two formats).

Hint: download GNU datamash.

Answer: Taking this step by step, let's cut everything after the first comma-delimited field:

$ cat example_data.txt | cut -d"," -f2-
height,weight,salary,age
106,111,111300,62
124,91,79740,40
127,176,15500,46

Commas are hard to work with, so let's use a tab delimiter:

$ cat example_data.txt | cut -d"," -f2- | sed 's|,|\t|g'
height  weight  salary  age
106     111     111300  62
124     91      79740   40
127     176     15500   46

Now we're going to transpose the data to make it easier to work with—one of the many great things GNU datamash does:

$ cat example_data.txt | cut -d"," -f2- | sed 's|,|\t|g' | datamash transpose
height  106     124     127
weight  111     91      176
salary  111300  79740   15500
age     62      40      46

Finally, we'll throw in a line of awk to finish the job:
awk '{for (i = 2; i <= NF; i++){print i-1"\t"$1"\t"$i}}'
This loops from the second field to the last field and prints a row for each iteration of the loop. Scroll horizontally to see the one-liner:

$ cat example_data.txt | cut -d"," -f2- | sed 's|,|\t|g' | datamash transpose | awk '{for (i = 2; i <= NF; i++){print i-1"\t"$1"\t"$i}}'
1       height  106
2       height  124
3       height  127
1       weight  111
2       weight  91
3       weight  176
1       salary  111300
2       salary  79740
3       salary  15500
1       age     62
2       age     40
3       age     46

If this seems a little messy, it is, and that's a cue to switch to a more powerful parsing language. Let's revisit this example when we discuss the Python shell below, so we can see how Python cuts through it like a knife through butter.

Problem 7
You should avoid using spaces in file names on the command line, because it can cause all sorts of annoyances. Use an underscore or dash instead.

Question: How many files and directories on your computer have spaces in their names?

Answer: To count every single file or directory on our computer, the command is:

$ sudo find / | wc -l
98912

(I'm testing this on Ubuntu Server 14.04 LTS.) How many have a space in their names?

$ sudo find / | grep " " | wc -l
304

Correct? Not quite, because this overcounts, as in:

$ sudo find / | grep " " | head -5
/sys/bus/pnp/drivers/i8042 aux
/sys/bus/pnp/drivers/i8042 aux/bind
/sys/bus/pnp/drivers/i8042 aux/00:06
/sys/bus/pnp/drivers/i8042 aux/uevent
/sys/bus/pnp/drivers/i8042 aux/unbind

But we just want to count the directory or file the first time we see it, not recursively count all the non-space-containing children of a space-containing parent. We can do this as follows:

$ sudo find / | grep " " | awk -F"/" '$NF ~ / /' | wc -l
70

This works by telling awk to print only the lines such that the last field (delimiting on slash) has a space in it. Here's an even simpler solution, via Albert:

$ sudo find / -name "* *" | wc -l
70

Conclusion: only 0.07% of files and directories follow the poor naming convention of using a space.
Example Bash Scripts TOP
When one-liners fail, it's time to script. When we were introduced to scripting above, we didn't have many tools in our toolkit. Now that we do, let's consider some example bash scripts—picking our battles for things bash can do more cleanly than Python or Perl.

Example 1
We've already seen the construction:

$ cat $( which myscript )

which allows us to look at a script in our PATH without having to remember its exact location. The following example is courtesy of my friend, Albert, who packaged this up into a script called catwhich:

#!/bin/bash

# cat a file in your path

file=$(which $1 2>/dev/null)

if [[ -f $file ]]; then
    cat $file
else
    echo "file \"$1\" does not exist!"
fi

The -f file test operator, says The Linux Documentation Project, checks if the "file is a regular file (not a directory or device file)." The path /dev/null, where any potential error from which gets routed, is a special unix path that acts like a black hole—saving anything in there makes it disappear. Functionally, it just suppresses any error because we don't care what it is.

There's a nearly identical version for vim, vimwhich:

#!/bin/bash

# vim a file in your path

file=$(which $1 2>/dev/null)
if [[ -f $file ]]; then
    vim $file
else
    echo "file \"$1\" does not exist!"
fi

Example 2
In lab we often run scripts in parallel. Each instance of a script will produce two log files, one containing the stdout of the script and and one containing the stderr of the script. We sometimes use a convention of printing a [start] at the beginning of the stdout and an [end] at the finish. This is one way of enabling us to check if the job finished. An output log file might look like this:

[start]

Some output ...

[end]

Here's a script, checkerror, that loops through all of the stdout log files (I assume they have the extension .o) in a directory and checks for these start and end tags:

#!/bin/bash

# 1st arg is logs directory
logs=$1

# example: ./checkerror project/logs
tot=0   # number of files scanned

# loop thro .o files in logs directory
for i in ${logs}/*.o*; do

    # get file name
    filename=$( basename $i );

    # check for [start] and [end] tags
    if ! grep "\[start\]" $i > /dev/null; then
        echo -e "\n[error] no start tag: "${filename};
    elif ! grep "\[end\]" $i > /dev/null; then
        echo -e "\n[error] no end tag: "${filename};
    else
        # print a dot for each error-free file
        echo -n "."
    fi
    # increment total
    ((tot++))
done

echo -e "\n[summary] $tot files scanned"

We're again making use of /dev/null because we don't want grep to return the lines it finds—we just want to know if it's successful. We haven't encountered basename before. This simply gets the name of a file from a path, so we don't output the whole file path.

Example 3
The last example is one I wrote to test if the (bioinformatics) programs bwa, blastn, and bedtools are in the user's PATH:

#!/bin/bash

echo "[checking dependencies]"

# define dependencies
dependencies="bwa blastn bedtools"

for i in $dependencies; do
    if ! which $i > /dev/null; then
        echo "[error] $i not found"
        exit
    fi
done

If, for example, you're transferring a program with dependencies to somebody, this double-checks that they have all of the dependencies installed and accessible in their PATH. It works using the command which, which throws a bad exit code if its argument isn't found in the PATH. These lines might be something you'd see at the beginning of a script rather than a complete script in their own right.
Using the Python Shell to do Math, and More TOP
I'm a new convert to Python and that's why I've leaned on Perl in some of the examples. However, these days it seems inescapable that Perl is the past and Python is the future. Python has many awesome features and one is the ability to run a Python shell simply by entering:

$ python

You can do a million things with this shell, but it's certainly the easiest way to do mathematics in the terminal. (Another convenient way is using the R shell, but you have to install R first.) For example:

$ python  # open the Python shell
>>> 234+234
468
>>> import math
>>> math.log(234,3)
4.96564727304425
>>> math.log(234,2)
7.870364719583405
>>> math.pow(2,8)
256.0
>>> math.cos(3.141)
-0.9999998243808664
>>> math.sin(3.141)
0.0005926535550994539

You can read more about Python's math module here. If you want to do more sophisticated mathematics, you can install the NumPy package.

The Python command line is great not just for math but for many tasks where bash feels clumsy. Remember our parsing example above where we had a a file, example_data.txt:

,height,weight,salary,age
1,106,111,111300,62
2,124,91,79740,40
3,127,176,15500,46

and we wanted to transform it into this:

1       height  106
2       height  124
3       height  127
1       weight  111
2       weight  91
3       weight  176
1       salary  111300
2       salary  79740
3       salary  15500
1       age     62
2       age     40
3       age     46

If you don't know Python, skip this section. If you do, how can you do it in the Python shell? Let's start by opening the file and reading its contents:

>>> with open('example_data.txt', "r") as f: contents = f.read()

Examine our variable contents:

>>> contents
',height,weight,salary,age\n1,106,111,111300,62\n2,124,91,79740,40\n3,127,176,15500,46\n'

Let's convert this string into a list, by splitting on the newline character:

>>> contents.split('\n')
[',height,weight,salary,age', '1,106,111,111300,62', '2,124,91,79740,40', '3,127,176,15500,46', '']

Now lop off the empty field at the end:

>>> contents.split('\n')[:-1]
[',height,weight,salary,age', '1,106,111,111300,62', '2,124,91,79740,40', '3,127,176,15500,46']

Use list comprehension to split the elements of this list on the comma character:

>>> [x.split(',') for x in contents.split('\n')[:-1]]
[['', 'height', 'weight', 'salary', 'age'], ['1', '106', '111', '111300', '62'], ['2', '124', '91', '79740', '40'], ['3', '127', '176', '15500', '46']]

Now let's use a trick that if A is a list of lists, you can perform a matrix transpose with zip(*A):

>>> zip(*[x.split(',') for x in contents.split('\n')[:-1]])
[('', '1', '2', '3'), ('height', '106', '124', '127'), ('weight', '111', '91', '176'), ('salary', '111300', '79740', '15500'), ('age', '62', '40', '46')]

Let's loop through this list:

>>> for j in zip(*[x.split(',') for x in contents.split('\n')[:-1]])[1:]: print(j)
('height', '106', '124', '127')
('weight', '111', '91', '176')
('salary', '111300', '79740', '15500')
('age', '62', '40', '46')

We can transform any given tuple as follows:

>>> k = ('height', '106', '124', '127')
>>> [str(y+1) + '\t' + k[0] + '\t' + z for y,z in enumerate(k[1:])]
['1\theight\t106', '2\theight\t124', '3\theight\t127']

This is using list comprehension to meld the first element of the tuple, height, to each subsequent element and add a numerical index, as well. Let's apply this to each tuple in our list, and join everything with a newline to finish the job:

>>> for j in zip(*[x.split(',') for x in contents.split('\n')[:-1]])[1:]:
...  print('\n'.join([str(y+1) + '\t' + j[0] + '\t' + z for y,z in enumerate(j[1:])]))
1       height  106
2       height  124
3       height  127
1       weight  111
2       weight  91
3       weight  176
1       salary  111300
2       salary  79740
3       salary  15500
1       age     62
2       age     40
3       age     46

Whew - done!

I put together a small (unpolished) Python Wiki here.
tmux TOP
There's one last tool I strongly recommend you make into a habit. Imagine the following scenario: you're working in the terminal and you accidentally close the window or quit or it crashes. If you were logged in somewhere, you'll have to log in again. If you were in the middle of running a program, you'll have to start it again [1]. While your commands should be saved in history, if there was output on the screen you wanted to refer back to, it's lost forever. This is where tmux comes in. Regardless of whether or not you quit the terminal, your sessions are persistent processes that you can always access until the computer is shut off. You can get your exact terminal session back again: you're still logged in wherever you were and, moreover, you can see everything you typed in this window by simply scrolling up. If you happened to be running a program, no worries—it will still be going. For this reason, it's a good idea to make using tmux (or its old-school cousin, screen) a habit every time you're on the terminal, if only as insurance. tmux also allows you to access multiple terminal "windows" within the same terminal, err, window and more.

Let's get the terminology straight. In tmux there are:

    sessions
    windows
    panes

Sessions are groupings of tmux windows. For most purposes, you only need one session. Within each session, we can have multiple "windows" which you see as tabs on the bottom of your screen (i.e., they're virtual windows, not the kind you'd create on a Mac by typing ⌘N). You can further subdivide windows into panes, although this can get hairy fast. Here's an example of a tmux session containing four windows (the tabs on the bottom), where the active window contains 3 panes:

image

I'm showing off by logging into three different computers—home, work, and Amazon.

In tmux, every command starts with a sequence of keys I'll refer to as Leader. The leader sequence is Cntrl-b by default but I like to remap it to Cntrl-f [2]. Here are the basics. To start a new tmux session, enter:

$ tmux

To get out of the tmux universe, detach from your current session using Leader d. To list your sessions, type:

$ tmux ls
0: 4 windows (created Fri Sep 12 16:52:30 2014) [177x37]

This says we have one grouping of 4 virtual windows whose session id is 0. To attach to a session, use:

$ tmux attach			# attach to the first session
$ tmux attach -t 0		# attach to a session by id

To kill a session, use:

$ tmux kill-session -t 0	# kill a session by id

Here's a small list of commands you can invoke within tmux:

<Leader> c	Create a new window
<Leader> x	Kill the current window
<Leader> n	Go to the next window
<Leader> p	Go to the previous window
<Leader> l	Go to the last-seen window
<Leader> 0-9	Go to a window numbered 0-9
<Leader> w	List windows
<Leader> s	Toggle between sessions
<Leader> d	Detach the session
<Leader> ,	Set a window's title

See a longer list of commands here. tmux is amazing—I went from newbie to cheerleader in about 30 seconds!

Note: tmux does not come with your computer by default—you'll have to download it (see the the next section).


[1] You could circumvent this with nohup, which makes a program persist even if the terminal quits ↑
[2] You can rebind the Leader using the configuration file ~/.tmux.conf ↑
Installing Programs on the Command Line TOP
In the course of this article, we've made passing references to programs like htop, pstree, nginx, and tmux. Perhaps you have these on your computer but, if not, how do you get them? You can usually go to a program's webpage, download the source code, and build it on your computer (google the mantra ./configure; make; make install). However, you'll probably discover that your system has some crucial deficiency. Something's out of date, plus the program you're trying to install requires all these other programs which you don't have. You've entered what I call dependency hell, which has a way of sending you to obscure corners of the internet to scour chat rooms for mysterious lore.

When possible, avoid this approach and instead use a package manager, which takes care of installing a program—and all of its dependencies—for you. Which package manager you use depends on which operating system you're running. For Macintosh, it's impossible to live without brew, whose homepage calls it, "The missing package manager for OS X." For Linux, it depends on your distribution's lineage: Ubuntu has apt-get; Fedora has yum; and so on. All of these package managers can search for packages—i.e., see what's out there—as well as install them.

Let's use the program gpg2 (The GNU Privacy Guard), a famous data encryption tool which implements the OpenPGP standard, to see what this process looks like. First, let's search:

$ brew search gpg2			# Mac
$ yum search gpg2			# Fedora
$ apt-cache search gpg2			# Ubuntu

Installing it might look like this:

$ brew install gpg2			# Mac
$ sudo yum install gnupg2.x86_64	# Fedora
$ sudo apt-get install gpgv2		# Ubuntu

The exact details may vary on your computer but, in any case, now you're ready to wax dangerous and do some Snowden-style hacking! (He reportedly used this tool.) I have a quick gpg2 primer here.
Bash in the Programming Ecosystem (or When Not to Use Bash) TOP
All programming languages are the same. This statement is simultaneously true and not true. In the programming landscape, bash occupies a unique place. We've seen it's definitely not for heavy-duty coding. Using basic data structures, like arrays or hashes, or doing any kind of math is unpleasant in bash. Look at the horrible syntax for floating-point arithmetic (via Wikipedia):
result=$(echo "scale=2; 5 * 7 /3;" | bc)
Bash's strength is system stuff, like manipulating files and directories. If you do write a bash script, it's often a wrapper—the glue which ties a bunch of programs together and bends them to your purpose. Many people would argue that you should seldom write a script in bash. Confine bash to the command line and use a modern scripting language if you want to script. Python and Perl can do more, have much friendlier syntax, and make it easy to call system commands.

However, if you're new to programming, start with unix because it will get you acquainted with important principles like input and output streams, permissions, processes, etc. faster than anything else. Furthermore, much of the material we covered above is not bash-specific. Perl is, in many ways, an extension of bash and it shares a lot of the same syntax—for file test operators, system calls with backticks, here documents, and more.
Concluding Notes TOP
As you get deeper and deeper into unix, you may be getting the feeling that the GUI is just a painted facade—or that you're peering behind the clockface into the gears. This is true! If you think of your computer as a tool, you can do a lot more with it using unix. And given that millions of people spend half their lives in front of a computer, there are few downsides to having a greater mastery over this tool. Even if you're not doing something technical, technical questions have a way of insinuating themselves into the picture. This manual has been more about the principles of unix and hasn't introduced many of the most useful unix utilities. To learn about them, there's a reference at 100 Useful Unix Commands.

So how do you go about learning unix? Just as reading a detailed book about violin won't transform you into a violinist, this article is of limited utility and defers to the terminal itself as the best teacher. You have to pay your dues and experience counts for a lot because there's so much to learn (I'm already a few years in and I learn things almost daily). Start using it and crash headfirst into problems. There's no substitute for having somebody to bother who knows it better than you do. Failing that, there's always Stackoverflow and the rest of the internet, which has become the greatest computer science manual ever compiled. In programming, I'm always surprised how much more a couple years of work taught me than a couple years of class, and perhaps this speaks volumes about the merits of apprenticeship versus classroom instruction.

Unix—with its power, elegance, and scope—is a modern marvel. If you know it and your friends don't, it's a bit like having been exposed to some awesome book or song that they haven't discovered yet. To see all the commands at your fingertips, type tab tab on the command line (there are over 2200 on my Mac!). Or do some reading for pleasure in:

$ man bash
$ info coreutils

to remind yourself what you're working with. I bet you didn't think anything this cool came out of the 70s! :D
Acknowledgements and Postscript TOP
I am graciously indebted to the following people, who contributed in ways big and small to this article:

Albert Lee
Vladimir Trifonov
Alex North-Keys
Guido Jansen

Postscript, March 2015
I don't like remembering syntax and I forget what I've learned quickly. Thus this article started out as a memory aid—miscellaneous command line-alia for which I wanted a reference done in my own particular way, prejudices included. Its waistline expanded to its present (large) girth and it got a little play on the internet in early 2015. If I hadn't appreciated the importance of editors and fact-checkers, I do now—as the editing of this page was nerve-wrackingly crowded-sourced in real time. I've since corrected many of the errors people pointed out as well as polished and added sections, and the article is better for it.

If you've read this far, you know that this article is not, speaking in rigid literals, an introduction to unix. It's not about the nitty-gritty of how operating system kernels work. And it's not even about UNIX®, which is still a trademark—"the worldwide Single UNIX Specification integrating X/Open Company's XPG4, IEEE's POSIX Standards and ISO C" (say what!?), according to the official website. These days UNIX® refers to a detailed specification rather than software. This article, in contrast, is about command line basics. But it's not about all command lines, which would include rubbish like Windows Powershell. It's about unix-like command lines—i.e., command lines descended from the ancestral unix progenitor:

image
(Image credit: Wikipedia: Unix-like)

This is what I mean when I use "unix" as a colloquial shorthand. However, to begin the article by embroiling readers in these quagmires of terminology would turn them away in the first paragraph.

There were other comments but the funniest one came from my dad:

    P.S. I see 2 keys at bottom of my keyboard that say, "command." Is this what all the fuss is about? I'm afraid if I touched them the computer would blow up like a roadside bomb!

More comments, corrections, or suggestions? Let me know!
Advertising

image


image


image


© 2016 Oliver
image
