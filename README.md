Download Link: https://assignmentchef.com/product/solved-openmp-lab
<br>
Introduction

The basic idea is to use <a href="http://openmp.org/wp/">OpenMP</a> to make a program go faster.

<h2>Keep a log</h2>

As usual, keep a log in the file <samp>openmplab.txt</samp> of what you do in the lab so that you can reproduce the results later. This should not merely be a transcript of what you typed: it should be more like a true lab notebook, in which you briefly note down what you did and what happened. The log should help us verify that you’ve done the steps of this assignment, so that we can in principle reproduce them.

<h2>Files</h2>

Your lab handout contains the following files:

<dl>

 <dt>

  <code>func.h</code>

 </dt>

 <dd>

  Header with typedefs and function prototypes.

 </dd>

 <dt>

  <code>func.c</code>

 </dt>

 <dd>

  Primary source file (edit and submit this).

 </dd>

 <dt>

  <code>filter.c</code>

 </dt>

 <dd>

  Filtering function file.

 </dd>

 <dt>

  <code>main.c</code>

 </dt>

 <dd>

  Source file containing main() and initialization code.

 </dd>

 <dt>

  <code>util.h</code>

 </dt>

 <dd>

  util.c Files for utility functions.

 </dd>

 <dt>

  <code>Makefile</code>

 </dt>

 <dd>

  Build script.

 </dd>

 <dt>

  <code>correct.txt</code>

 </dt>

 <dd>

  Correct output data (for default inputs).

 </dd>

 <dt>

  <code>seed.txt</code>

 </dt>

 <dd>

  Input file

 </dd>

</dl>

You should edit only <code>func.c</code>.

<h2>Grading</h2>

Your grade for this assignment will be proportional to the amount of speedup you achieve. For full credit, you must achieve a 3.5× speedup. Extra credit will be awarded for speedup beyond that amount. To get any credit, your code must produce the same output as the original code. In addition, for each memory leak in your code, your overall grade will be reduced by 1%. A memory leak is defined as a region of memory that was allocated but never freed.

<h2>Compiling and Running</h2>

<dl>

 <dt>

  To compile normally:

 </dt>

 <dd>

  <code>make seq</code>

 </dd>

 <dt>

  To compile with OpenMP enabled:

 </dt>

 <dd>

  <code>make omp</code>

 </dd>

 <dt>

  To compile using a different source file:

 </dt>

 <dd>

  <code>make omp SRC=try2.c</code>

 </dd>

 <dt>

  To compile with gprof enabled:

 </dt>

 <dd>

  <code>make seq GPROF=1</code>

 </dd>

 <dt>

  To compile with memory tracing enabled:

 </dt>

 <dd>

  <code>make omp MTRACE=1</code>

 </dd>

 <dt>

  To check that your output is correct:

 </dt>

 <dd>

  <code>make check</code>

 </dd>

 <dt>

  To check for memory leaks after a run:

 </dt>

 <dd>

  <code>make checkmem</code>

 </dd>

 <dt>

  To remove the executable and output files:

 </dt>

 <dd>

  <code>make clean</code>

 </dd>

</dl>

The generated executable is named <code>filter</code>. By default, it will generate a file <code>output.txt</code>. It also outputs the time taken to run the <code>filter</code> function. If your output is not correct, a message will be output saying your output differs from <code>correct.txt</code>. When you add the <code>make</code> operand <code>MTRACE=1</code>, all calls to <code>malloc</code> and <code>free</code> are logged and saved to the file <code>mtrace.out</code>. When you run <code>make checkmem</code>, that file will be analyzed to verify that all allocated memory was eventually freed. This last step requires tools that are available on the SEASnet GNU/Linux servers.

<h2>Code Overview</h2>

The code performs filtering algorithm on a media file. The main function is <code>filter</code>, found in <code>filter.c</code>. It calls six functions <code>func0</code> through <code>func5</code>. Each function consists of a for-loop, and your job is to try to optimize the given code and extract parallelism from each function using OpenMP.

<h2>Profiling</h2>

When optimizing a large program, it is useful to profile it to determine which portions take up the largest portion of the execution time. There is no point in optimizing code that only takes up a small fraction of the overall computations.

<code>gprof</code> is a simple profiling tool which works with GCC to give approximate statistics on how often each function is called. <code>gprof</code> works by interrupting your program at fixed time intervals and noting what function is currently executing. As shown earlier, to compile with <code>gprof</code> support, add <code>GPROF=1</code> to the <code>make</code> command. Then when you run <code>filter</code>, it will produce the file <code>gmon.out</code> containing the raw statistics. To view the statistics in a readable format, run <code>gprof</code> with the name of the executable, e.g., <code>gprof filter</code>.

You can also measure execution time of portions of the program using the <code>get_time</code> and <code>elapsed_time</code> functions. Check how they are used in the <code>main</code> function.

<h2>Submit</h2>

Submit the files <code>func.c</code> and <samp>openmplab.txt</samp>, along with any other files you think useful.

All text files should be ASCII files, with no carriage returns, and with no more than 200 columns per line. For example, the shell command

<pre><samp>expand func.c openmplab.txt |  awk '/r/ || 200 &lt; length'</samp></pre>

should output nothing.