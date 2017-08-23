# HW1: Building, Queuing, and Profiling
---


This HW covers two fundamental topics required in this class: compiling code and running code on a cluster. Please post questions on Piazza or come to OH if you find any part of the instructions confusing!

Your submission should include the following files:

1. **mystery-valentine.txt**
2. **makefile**
3. **job-mystery.pbs**


As this is the first homework, we want to make sure you understand how to submit our HWs properly. There are two options for submission: 

* Submit tarball through CMS. This submission method requires you compress your submission directory. For quick instructions, see [here](https://www.mkyong.com/linux/how-to-zip-unzip-tar-in-unix-linux/)
* Submit Git Repository link through CMS. This submission method requires you provide a link to a repository hosted on your personal git account. For instructions, see [here](http://www.cs.cornell.edu/courses/cs5220/2017fa/git-info.html)

As this is the first formal HW, we want to encourage students try both methods of submission, by both submitting a tarball and a Github link on CMS. Students who do so will receive a small amount of extra credit points


## Manual Compilation of Code 


C which will be extensively used for almost all of our HWs and projects. For those needing a introduction or refresh of C, please refer to the C Background section of the [Course Readings Page](http://www.cs.cornell.edu/courses/cs5220/2017fa/readings.html)

C is a *compiled* language, meaning you use a compiler to translate the C code you've written into an executable program containing machine instructions. Python and Matlab are examples of languages that aren't compiled. Let's start with compilation basics. The GNU C Compiler (**gcc**) is a standard C compiler. We have provided code snippet **mystery-valentine.c**. Compile the code as follows:

```
gcc -o mystery-valentine mystery-valentine.c
```

Notice compilation creates a new file named **mystery-valentine**. You may run **mystery-valentine** with the command:

```
./mystery-valentine
```

You may also switch compilers. Different compilers offer different features. The Intel C Compiler (**icc**) is a popular compiler used in this class. The principle remains the same, except you have to load the compiler via the module system before using it. The first command loads **icc** into your system path via the module system, and the second compiles **mystery-valentine.c**:

```
module load cs5220
icc -o mystery-valentine mystery-valentine.c
```

SUBMISSION: In your submission, please include a .txt file containing the output of **mystery-valentine** named **mystery-valentine.txt**


## Automatic Compilation of Code 


We will include makefiles with almost all our homeworks and projects. A makefile is a useful tool for among other things, building and compiling code. Let's say we have the canonical "Hello World!" code, aptly titled **hello.c**. Instead of tediously typing out compiler instructions, you can simply type 

```
make hello
```
This calls the make recipe for hello, which in this case will simply compile **hello.c**. You can clean up the executable with the command

While seeminly trivial for something like **hello.c**, makefiles are necessary for any non-trivial code and can become increasingly complex. We will use makefiles for all programming projects. Note that makefiles are not the only automated method of building code; IDEs for example all use their own proprietary build systems. 
```
make clean
```

SUBMISSION: In your submission, please create a modify the provided **makefile** to include a recipe for compiling **mystery-valentine.c**. 



## Running Code on Cluster 

Totient contains a login node and compute nodes. You do not want to run your code on the login node outside very light prototyping and scripting, as it will be shared across the class. Slowing down the login node is generally not a good idea, especially when the instructors can check who is running what! To run an executable named **runme.out** on the login node, recall the simple command:

```
./runme.out
```

To run an executable on a compute node, you will need to submit a compute job; this requires a submission script. Typical submission scripts include: number of nodes (or which particular set of nodes) to run the job on, number of threads per node, time limit, etc. We have included a very basic submission script for **hello.c** named **job-hello.pbs**. To run **hello.c**, please compile and submit it as follows:

```
make hello
qsub job-hello.pbs
```

The first command, as you should know by now, compiles **hello.c** into **hello**. The second submits **job-hello.pbs**, which simply executes hello on a random compute node, to the job queue (hence the name **qsub**). You can also run jobs in interactive mode. From the login node, type

```
lscpu
qsub -I
lscpu
```

The first command checks the CPU of the login node. The second command starts an interactive shell on a compute node, meaning you get to interface directly with the compute node. Third command verifies this fact: note that the output of the first **lscpu** is different from the output of the second **lscpu**. You can use the **qstat** command to check the status of your job. To leave interactive mode and return to the login node, simply type 

```
exit
```

SUBMISSION: Please create a job script for **mystery-valentine.c** named **job-mystery.pbs**. Verify that it runs correctly on Totient.  



## Important Concluding Thoughts

If any of the concepts discussed in this HW were a bit hard to understand (including but not limited to: logging into Totient, Unix commands, makefiles, etc), don't worry! CS 5220 always enrolls students from a wide range of disciplines; it is not uncommon for this to be many students' first formal Computer Science Class. Throughout the semester, there will be many opportunities for students without a formal CS background to brush up on necessary information. 

We will take this opportunity to list one good resource: the [Scientific Software Club @ Cornell](https://cornell-ssw.github.io/) hosts workshops for people in STEM unfamiliar with popular computing tools. Unix and Version Control are two topics that will be covered early on. These workshops will be announced a bit later in the semester. We highly recommend you attend if you think it may help! Pizza will be provided. 

