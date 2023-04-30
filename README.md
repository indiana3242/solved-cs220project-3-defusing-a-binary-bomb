Download Link: https://assignmentchef.com/product/solved-cs220project-3-defusing-a-binary-bomb
<br>
Introduction

The nefarious <em>Dr. Evil </em>has planted a slew of “binary bombs” on our class machines. A binary bomb is a program that consists of a sequence of phases. Each phase expects you to type a particular string on stdin. If you type the correct string, then the phase is <em>defused </em>and the bomb proceeds to the next phase. Otherwise, the bomb <em>explodes </em>by printing “BOOM!!!” and then terminating. The bomb is defused when every phase has been defused.

There are too many bombs for us to deal with, so we are giving each student a bomb to defuse. Your mission, which you have no choice but to accept, is to defuse your bomb before the due date. Good luck, and welcome to the bomb squad!

<h1>Step 1: Get Your Bomb</h1>

You can obtain your bomb by pointing your Web browser at:

http://zdu.binghamton.edu:15213/

[This URL can only be accessed from one of the lab machines.]

This will display a binary bomb request form for you to fill in. Enter your user name or remote.cs and Binghamton University email address and hit the Submit button. The server will build your bomb and return it to your browser in a tar file called bombk.tar, where <em>k </em>is the unique number of your bomb. Note that the tar file will be downloaded directly and there is no success feedback; you should find the downloaded tar file in your Downloads directory.

Save the bombk.tarfile to a (protected) directory in which you plan to do your work, like your ˜/i220X/work directory. Then give the command: tar -xvf bombk.tar. This will create a directory called ./bombk with the following files:

<ul>

 <li>README: Identifies the bomb and its owners.</li>

 <li>bomb: The executable binary bomb.</li>

 <li>c: Source file with the bomb’s main routine and a friendly greeting from Dr. Evil.</li>

</ul>

If for some reason you request multiple bombs, this is not a problem. Choose one bomb to work on and delete the rest.

<h1>Step 2: Defuse Your Bomb</h1>

Your job for this lab is to defuse your bomb.

You must do the assignment on one of the remote.cs machines. In fact, there is a rumor that Dr. Evil really is evil, and the bomb will always blow up if run elsewhere. There are several other tamper-proofing devices built into the bomb as well, or so we hear.

Note that when the bomb requires you to type in an input string, it silently pauses without any prompt.

You can use many tools to help you defuse your bomb. Please look at the hints section for some tips and ideas. The best way is to use objdump to disassemble your binary combined with using your favorite debugger to step through the disassembled binary.

Each time your bomb explodes it notifies the bomblab server, and you lose 1/2 point (up to a max of 20 points) in the final score for the lab. So there are consequences to exploding the bomb. You must be careful!

The bomb requires a 6-phase defusing. However, in this project we will defuse only the first 4 steps. Phase 1 will be worth 19 points and the remaining 3 phases are worth 27 points each. Hence if you correctly defuse all 4 phases but have the bomb go off 4 times, you will obtain a grade of 98.

Although phases get progressively harder to defuse, the expertise you gain as you move from phase to phase should offset this difficulty.

The bomb ignores blank input lines. If you run your bomb with a command line argument, for example,

$ <em>./bomb psol.txt</em>

then it will read the input lines from psol.txt until it reaches EOF (end of file), and then switch over to stdin. In a moment of weakness, Dr. Evil added this feature so you don’t have to keep retyping the solutions to phases you have already defused.

To avoid accidentally detonating the bomb, you will need to learn how to single-step through the assembly code and how to set breakpoints. You will also need to learn how to inspect both the registers and the memory states. One of the nice side-effects of doing the lab is that you will get very good at using a debugger. This is a crucial skill that will pay big dividends the rest of your career.

<h1>Handin</h1>

There is no explicit handin. The bomb will automatically report your progress to us as you work on it. You can keep track of how you are doing by looking at the class scoreboard at:

http://zdu.binghamton.edu:15213/scoreboard

[This URL can only be accessed from one of the lab machines.]

This web page is updated continuously to show the progress for each bomb. Ignore the <em>Score </em>shown on this scoreboard as we are using a different scoring system for this project.

<h2>Hints (Please read this!)</h2>

There are many ways of defusing your bomb. You can examine it in great detail without ever running the program, and figure out exactly what it does. This is a useful technique, but it not always easy to do. You can also run it under a debugger, watch what it does step by step, and use this information to defuse it. This is probably the fastest way of defusing it.

We do make one request, <em>please do not use brute force! </em>You could write a program that will try every possible key to find the right one. But this is no good for several reasons:

<ul>

 <li>You lose 1/2 point (up to a max of 20 points) every time you guess incorrectly and the bomb explodes.</li>

 <li>Every time you guess wrong, a message is sent to the bomblab server. You could very quickly saturate the network with these messages, and cause the system administrators to revoke your computer access.</li>

 <li>We haven’t told you how long the strings are, nor have we told you what characters are in them. Even if you made the (incorrect) assumptions that they all are less than 80 characters long and only contain letters, then you will have 26<sup>80 </sup>guesses for each phase. This will take a very long time to run, and you will not get the answer before the assignment is due.</li>

</ul>

There are many tools which are designed to help you figure out both how programs work, and what is wrong when they don’t work. Here is a list of some of the tools you may find useful in analyzing your bomb, and hints on how to use them.

<ul>

 <li>gdb</li>

</ul>

The GNU debugger, this is a command line debugger tool available on virtually every platform. You can trace through a program line by line, examine memory and registers, look at both the source code and assembly code (we are not giving you the source code for most of your bomb), set breakpoints, set memory watch points, and write scripts. The CS:APP web site http://csapp.cs.cmu.edu/2e/docs/gdbnotes-x86-64.pdf

has a very handy single-page gdb summary that you can print out and use as a reference. Here are some other tips for using gdb.

<ul>

 <li>To keep the bomb from blowing up every time you type in a wrong input, you’ll want to learn how to set breakpoints.</li>

 <li>For online documentation, type “help” at the gdb command prompt, or type “man gdb”, or “info gdb” at a Unix prompt. Some people also like to run gdb under gdb-mode in emacs.</li>

</ul>

<ul>

 <li>objdump -t</li>

</ul>

This will print out the bomb’s symbol table. The symbol table includes the names of all functions and global variables in the bomb, the names of all the functions the bomb calls, and their addresses. You may learn something by looking at the function names!

<ul>

 <li>objdump -d</li>

</ul>

Use this to disassemble all of the code in the bomb. You can also just look at individual functions. Reading the assembler code can tell you how the bomb works.

<ul>

 <li>strings</li>

</ul>

This utility will display the printable strings in your bomb.

Looking for a particular tool? How about documentation? Don’t forget, the commands apropos, man, and info are your friends. In particular, man ascii might come in useful. info gas will give you more than you ever wanted to know about the GNU Assembler. Also, the web may also be a treasure trove of information.

More hints:

<ul>

 <li>Since this is a very popular lab offered by many schools, you are likely to find a lot of help online. Hopefully, this help will not constitute a complete solution, but could get you pointed in the right direction.</li>

 <li>When using gdb, layout asm and layout regs are invaluable. See https://sourceware.org/gdb/onlinedocs/gdb/TUI-Commands.html</li>

</ul>

Note that the TUI is a bit rough around the edges, use the focus command to switch between the windows within your terminal.

<ul>

 <li>Evil has been nice enough to provide correct names for functions in the object file; i.e., the functions do what their names imply. So sscanf()does indeed refer to the standard library function which reads input from a string.</li>

 <li>It is possible to set things up so that it is impossible for the bomb to detonate. Using the debugger, you should be able to see when your bomb is about to detonate and stop or restart the program at that point.</li>

</ul>