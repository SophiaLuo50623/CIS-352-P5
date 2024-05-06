# Discussion and Reflection


The bulk of this project consists of a collection of five
questions. You are to answer these questions after spending some
amount of time looking over the code together to gather answers for
your questions. Try to seriously dig into the project together--it is
of course understood that you may not grasp every detail, but put
forth serious effort to spend several hours reading and discussing the
code, along with anything you have taken from it.

Questions will largely be graded on completion and maturity, but the
instructors do reserve the right to take off for technical
inaccuracies (i.e., if you say something factually wrong).

Each of these (six, five main followed by last) questions should take
roughly at least a paragraph or two. Try to aim for between 1-500
words per question. You may divide up the work, but each of you should
collectively read and agree to each other's answers.

[ Question 1 ]

For this task, you will three new .irv programs. These are ir-virtual? programs in a pseudo-assembly format. Try to compile the program. Here, you should briefly explain the purpose of ir-virtual, especially how it is different than x86: what are the pros and cons of using ir-virtual as a representation? You can get the compiler to to compile ir-virtual files like so:

racket compiler.rkt -v test-programs/sum1.irv

(Also pass in -m for Mac) ir-virtual is useful for showing the order in which the function executes commands Compared to x86 it is much easier to understand as it shows the variables and functions. x86 moreso represents the hardware's understanding of commands and registers. Pros: Shows Variables and functions The coder is able to understand it easier Cons: Cannot track the processes within the memory Can be harder to track errors within the execution

[ Question 2 ]

For this task, you will write three new .ifa programs. Your programs must be correct, in the sense that they are valid. There are a set of starter programs in the test-programs directory now. Your job is to create three new .ifa programs and compile and run each of them. It is very much possible that the compiler will be broken: part of your exercise is identifying if you can find any possible bugs in the compiler.

For each of your exercises, write here what the input and output was from the compiler. Read through each of the phases, by passing in the -v flag to the compiler. For at least one of the programs, explain carefully the relevance of each of the intermediate representations.

For this question, please add your .ifa programs either (a) here or (b) to the repo and write where they are in this file. arith2.ifa - (print (* (* 3249 (- 1 9234)) 100)) if2.ifa - (if (not bop?)(print #f)(print #t)) cond2.ifa (cond [0 (print1)] [(? lit? l)(print 100)] [(+ 5 ((* 10 (+ (- 8 3) -2))))(print (+ 206 832))] [else (print #f)])

[ Question 3 ] 

Describe each of the passes of the compiler in a slight degree of
detail, using specific examples to discuss what each pass does. The
compiler is designed in series of layers, with each higher-level IR
desugaring to a lower-level IR until ultimately arriving at x86-64
assembler. Do you think there are any redundant passes? Do you think
there could be more?

In answering this question, you must use specific examples that you
got from running the compiler and generating an output.

Each pass of the compiler updates the stack pointer, performs assembly commands and prints the final output of the function call. Henceforth, depending on the function, there either were or weren't redundant passes. 

For example, comparing the if0 to the zero and bool0 calls, the if0 appears to contain redundant move calls as it's moving the stack and base pointers up and down the stack. Upon examining the zero and bool0 calls, it appears that they feature a more succinct assembly command sequence. This is evident from the inclusion of a few sub and mov instructions, along with instructions that directly execute the functions' intended purposes.


[ Question 4 ] 

This is a larger project, compared to our previous projects. This
project uses a large combination of idioms: tail recursion, folds,
etc.. Discuss a few programming idioms that you can identify in the
project that we discussed in class this semester. There is no specific
definition of what an idiom is: think carefully about whether you see
any pattern in this code that resonates with you from earlier in the
semester.

Definitions are identified because there a number of racket functions (like symbol?) and built in functions that are defined that are used throughout the ifarith->ifarith-tiny function. One idiom that I can identify is recursion because some of the multi-argument pattern matches recursively calls back ifarith->ifarith-tiny to evaluate ebody. Another idiom that can be identified is pattern matching, since all the different types from the input language that ifarith->ifarrith-tiny pattern matches and translates.

[ Question 5 ] 

In this question, you will play the role of bug finder. I would like
you to be creative, adversarial, and exploratory. Spend an hour or two
looking throughout the code and try to break it. Try to see if you can
identify a buggy program: a program that should work, but does
not. This could either be that the compiler crashes, or it could be
that it produces code which will not assemble. Last, even if the code
assembles and links, its behavior could be incorrect.

To answer this question, I want you to summarize your discussion,
experiences, and findings by adversarily breaking the compiler. If
there is something you think should work (but does not), feel free to
ask me.

Your team will receive a small bonus for being the first team to
report a unique bug (unique determined by me).

in prim-plus.ifa, one of the test cases has a bug where the let* is not defined correctly, as it uses = where it shouldn't be. It should, for example, look like [x 5] instead of [x = 5], or [z (+ x y)] instead of [z = (+ x y)]. Another bug is in the cost.ifa test case where the let* are not written properly. Like before, there is an example where you see [x0 = 5], buti t should be just [x0 5]. We found these through looking over all the test case codes and discussing anything that appeared incorrect, and then we would run the test cases and check if maybe the output was incorrect, or there was an error with the result.

[ High Level Reflection ] 

In roughly 100-500 words, write a summary of your findings in working
on this project: what did you learn, what did you find interesting,
what did you find challenging? As you progress in your career, it will
be increasingly important to have technical conversations about the
nuts and bolts of code, try to use this experience as a way to think
about how you would approach doing group code critique. What would you
do differently next time, what did you learn?

This project taught us the value of group work in the coding industry. When one of us was
stuck, we were all able to share our understanding of the project to further
progress. We also learned how to understand and utilize a compiler properly. While the code
we were given was substantial, we found methods to locate possible bugs. The tests, for 
example, were necessary for understand the goal of the code and the intended output.
Once we had used the tests to find individual problems within the code, we were able to
utilize the x86-64 compiler to find more specifically the problems with the code. In this
sense, it was helpful that we were using the terminal, which almost all of our computer science
classes this term had familiarized us with. Using Github, (which is the industry standard) 
however, posed a problem as many of us were unfamiliar with it. It was notable that each
group member was able to locate different bugs, which  is most likely due to a
different outlook on the code. In a workplace, it would be useful for this skill
to be applied to group code critiques as it allows a diverse set of ideas for locating
bugs and fixing them.
