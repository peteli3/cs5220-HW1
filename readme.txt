HW1: Building, Queuing, and Profiling

This HW covers three fundamental topics required in this class: compiling code, running code on a cluster, and profiling said code with a profiler. Please post questions on Piazza or come to OH if you find any part of the instructions confusing!

To submit tarball including:

(1) mystery-valentine.txt
(2) makefile
(3) job-mystery.pbs
(4) profile-mystery.out

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
~~~ Manual Compilation of Code ~~
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

C which will be extensively used for almost all, if not all, of our homeworks and projects. C is one of the oldest computer languages, and still very relevant today. For a brief overview of the history of the language, see https://www.codingunit.com/the-history-of-the-c-language

C is a *compiled* language, meaning you use a compiler to translate the C code you've written into an executable program containing machine instructions. Python and Matlab are examples of languages that aren't compiled. Let's start with compilation basics. The GNU C Compiler (gcc) is a standard C compiler. We have provided a mystery-valentine.c function to play with. Compile the code as follows:

gcc -o mystery-valentine mystery-valentine.c

Notice that you get a file named a.out; please submit this file (1) in the tarball. You may run mystery-valentine with the command:

./mystery-valentine

You can also switch compilers. The Intel C Compiler (icc) is another popular compiler we will be using in this class. The principle remains the same, except you have to load the compiler via the module system before using it. The first command loads icc into your system path via the module system, and the second compiles mystery-valentine.c:

module load cs5220
icc -o mystery-valentine mystery-valentine.c

(1) SUBMISSION: In your submission, please include a .txt file containing the output of mystery-valentine named mystery-valentine.txt

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
~ Automatic Compilation of Code ~
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We will include makefiles with almost all our homeworks and projects. A makefile is a useful tool for among other things, compiling code. Let's say we have the canonical "Hello World!" code, aptly titled "Hello.c". Instead of tediously typing out "gcc -option1 -option2 -option2 hello.c", you can simply type 

make hello

This calls the make recipe for hello, which in this case will simply compile hello.c. You can clean up the executable with the command

make clean

(2) SUBMISSION: In your submission, please create a modify the makefile to include a recipe for compiling mystery-valentine.c. 


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
~~~~ Running Code on Cluster ~~~~
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Totient contains a login node and compute nodes. You do not want to run your code on the login node outside very light prototyping and scripting, as it will be shared across the class. Slowing down the login node is generally not a good idea, especially when the instructors can check who is running what! To run an executable named "runme.out" on the login node, recall the simple command:

./runme.out

To run an executable on a compute node, you will need to submit a compute job; this requires a submission script. Typical submission scripts include: number of nodes (or which particular set of nodes) to run the job on, number of threads per node, time limit, etc. We have included a very basic submission script for hello.c named job-hello.pbs. To run hello.c, please compile and submit it as follows:

make hello
qsub job-hello.pbs

The first command compiles hello.c into hello. The second submits job-hello.pbs, which simply executes hello on a random compute node, to the job queue (hence the name "qsub"). You can also run jobs in interactive mode. From the login node, type

lscpu
qsub -I
lscpu

The first command checks the CPU of the login node. The second command starts an interactive shell on a compute node, meaning you get to interface directly with the compute node. Third command verifies this fact: note that the output of the first "lscpu" is different from the output of the second "lscpu". You can use the "qstat" command to check the status of your job. 

(3) SUBMISSION: Please create a job script for mystery-valentine.c named job-mystery.pbs. Verify that it runs correctly on Totient. 

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
~~~~~~ Profiling Your Code ~~~~~~
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the context of this class, profiling code means measuring the number of function calls, timing the execution runtime, and checking particular compiler flags for successful executed. We will be using Intel Vtune for this HW; feel free to use a different profiler in the future (or even to write your own!). To profile with Intel Vtune, run the following

module load cs5220
amplxe-cl -collect advanced-hotspots ./mystery-valentine

This will run a "hotspot" analysis to identify bottlenecks in your code, and store the profiler data in a folder default-ly named "r000ah". You can use this data to generate a number of reports. One example is the command 

amplxe-cl -report hotspots -r r000hs -group-by source-line

If you try generating a report right now, it should be rather empty as mystery-valentine.c is a rather simple program. For more on use of the Vtune tool, please check the following link for useful tips:
https://www.nas.nasa.gov/hecc/support/kb/finding-hotspots-in-your-code-with-the-intel-vtune-command-line-interface_506.html

(4) SUBMISSION: Please run Vtune on mystery-valentine and include the Vtune data folder r000ah in your submission. 

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
~~~~ IMPORTANT LAST THOUGHTS~~~~~
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Scientific Software Club @ Cornell hosts workshops for people in STEM unfamiliar with popular computing tools. Unix and Version Control are two topics that will be covered early on. If any of the concepts discussed in this HW were a bit hard to understand (including but not limited to: logging into Totient, Unix commands, makefiles, etc), we highly recommend you join. Pizza will be provided!

