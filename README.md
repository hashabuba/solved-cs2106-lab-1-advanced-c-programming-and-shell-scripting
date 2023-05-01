Download Link: https://assignmentchef.com/product/solved-cs2106-lab-1-advanced-c-programming-and-shell-scripting
<br>
There are <strong>seven exercises </strong>in this lab. The main motivation for this lab is to familiarize you with:




<ul>

 <li>using the SoC Compute Cluster,</li>

 <li>some advanced aspects of C programming, compiling and running C programs in Linux, and</li>

 <li>using the shell in Linux.</li>

</ul>




As such, you will need to write a combination of C programs and shell scripts (shell commands) to achieve some simple tasks. The <strong>techniques and shell commands </strong>used in these exercises are quite commonly used in OS related topics, and they will help you in completing the next lab assignments.




<h2>2.1. Exercise 1: Setting up your development environment</h2>




There are many ways to go about doing the development of your lab assignment. This exercise will run through some basic shell commands, as well as some advanced options that may aid you with your development. You should find what set-up works best for you.




Before we begin, make sure you have gone through Section 1.2, especially the part on the SoC Compute Cluster. We will be using our terminal (for Linux or Mac) or command prompt (for Windows) to connect to the remote nodes. We will also be downloading our assignment files using the terminal. You can think of the terminal or command prompt as an interactive program that allows you to type commands to complete some tasks without a graphical interface.




We will now discuss two possible ways to connect to the remote nodes:




<h3>A. Secure Shell (SSH) to xcne0-xcne7 through sunfire</h3>




Secure Shell (SSH) is a network protocol that allows us to work with remote nodes securely. We will first utilize this protocol to access our SoC Compute Cluster nodes.




To reach the SoC Compute Cluster nodes (xcne0-xcne7), we would normally need to perform the <strong>ssh</strong> command twice – once to get access to the sunfire node, then once more from the sunfire node to the xcne node. The steps are as follows:

<ol>

 <li>In your computer’s terminal or command prompt, enter <strong>ssh &lt;your_soc_account_id&gt;@sunfire.comp.nus.edu.sg</strong></li>

</ol>

You will be prompted for your SoC account password. Once entered, you should be looking at the shell of the remote sunfire node, and you will be placed at the home directory of your sunfire account.




<ol start="2">

 <li>To access xcne0 – xcne7, you can type e.g., <strong>ssh xcne6</strong> for xcne6. You will once again be prompted for your password. Once entered, you should now see that you are now in the xcne node.</li>

</ol>




Alternatively, instead of using these two steps, we can us a single ssh command using the -J flag. For example, in your computer’s terminal or command prompt, enter:

<h4>ssh -J &lt;your_soc_account_id&gt;@sunfire.comp.nus.edu.sg &lt;your_soc_account_id&gt;@xcne6</h4>




You will be prompted twice for your SoC account password, once for sunfire, and another for the xcne6 node. Once entered, you should be looking at the shell of the remote xcne6 node, and you will be placed at the home directory of your account.




<h3>B. Secure Shell (SSH) directly to xcne0-xcne7 from the SoC Network</h3>




Finding it tedious to have to enter your password twice? You can <strong>ssh</strong> directly into the xcne remote node <strong>if you are connected to the</strong> <strong>SoC VPN </strong><a href="https://dochub.comp.nus.edu.sg/cf/guides/network/vpn">(</a><a href="https://dochub.comp.nus.edu.sg/cf/guides/network/vpn">https://dochub.comp.nus.edu.sg/cf/guides/network/vpn</a><a href="https://dochub.comp.nus.edu.sg/cf/guides/network/vpn">)</a>!




To do so, simply enter the command (using xcne6 as an example):

<h4>ssh &lt;your_soc_account_id&gt;@xcne6.comp.nus.edu.sg</h4>




For those interested in further optimizing the developer experience for yourself, you can read up on hostnames and <strong>SSH keys</strong>, to eliminate the need to retype the long host addresses and your SoC account password respectively.




<h5>C. Basic Commands in the Terminal</h5>




Once you are connected to the remote shell, you can navigate around. To do so in the shell, you need to be familiar with basic commands such as:




<ul>

 <li><strong>pwd</strong>: print current working directory</li>

 <li><strong>cd</strong>: change directory</li>

 <li><strong>ls</strong>: list files in current directory</li>

</ul>




You can also type <strong>man &lt;command&gt;</strong> on the terminal to view the user manual of the command and read more about it.

<strong> </strong>

<h5>D. Development Set-Up</h5>




When programming your assignments, you have a few options. You may choose to:




<ol>

 <li>code directly on the remote node (xcne0-7),</li>

 <li>work locally using the virtual machine image provided, or</li>

 <li>use your own Ubuntu set-up.</li>

</ol>




For coding directly on the remote node, you can choose to either:




<ol>

 <li>use terminal-based text editors like Vim, which might seem less userfriendly, or</li>

 <li>set up remote development using SSH with your favorite code editor for a smoother development experience. For example, Visual Studio Code provides a SSH extension that lets you modify files on the xcne0-7 remote nodes as if you were editing a local file</li>

</ol>

<a href="https://code.visualstudio.com/docs/remote/ssh">(</a><a href="https://code.visualstudio.com/docs/remote/ssh">https://code.visualstudio.com/docs/remote/ssh</a><a href="https://code.visualstudio.com/docs/remote/ssh">)</a>.




Please <strong>do not</strong> develop on the sunfire remote node, as it is not running the same OS as the xcne0-7 nodes.




<h3>E. File Transfer</h3>

<strong> </strong>

Once you set up your development environment, you can download the lab1 files using the terminal of your development environment. For example, if you are using the virtual machine image, this will be the terminal of the instance. You will need to first fetch the zip files from a download link. You can use either <strong>wget</strong> or <strong>curl</strong> to do so. Use <strong>man</strong> / <strong>help</strong> to find out how to use <strong>wget</strong> or <strong>curl</strong>.




Download link:

<a href="https://www.comp.nus.edu.sg/%7Eccris/cs2106_ay2122s1/lab1.tar.gz">https://www.comp.nus.edu.sg/~ccris/cs2106_ay2122s1/lab1.tar.gz</a>




Once the files are downloaded, follow the instructions in Section 1.3 to unpack the files for lab1.




To transfer your code to and from the remote nodes, you can either use the <strong>sftp</strong> command, which uses the secure file transfer protocol to transfer your files onto the node. Use <strong>man</strong> to find out how to use <strong>sftp</strong>.




For those coding directly on the remote node, we also <strong>strongly recommend</strong> keeping a copy of the code locally, just in case anything unexpected happens to your data on the remote nodes. Once again, you can either use the <strong>sftp</strong> command to transfer files from the remote node to local or use a <strong>private git repository</strong>.

<h2>2.2. Exercise 2: Circular Linked List in C [Lab Demo Exercise]</h2>




<strong>Exercise 2 </strong>requires you to implement in C some functionalities for a circular linked list. Circular linked lists are commonly used in the Linux Kernel, such as for process and memory management. This exercise allows you to become more familiar with C syntax and appreciate the challenge behind implementing different parts of the operating system.




For this exercise, we represent a node in our circular linked list as follows (in node.h):




<strong>typedef struct NODE </strong>

<strong>{ </strong>

<strong>      int data;  struct NODE *next; } node; </strong>




The list representation looks like this:




<strong>typedef struct </strong>

<strong>{ </strong>

<h3>      node *head; } list;</h3>




Initially, the list will be empty.







Upon inserting the first node with data equals 1, we will have a circular linked list where the first node’s next pointer points back to itself.










Thereafter, every insertion will expand this circular linked list:













You need to implement five functions shown below to work with the circular linked list:




<table width="546">

 <tbody>

  <tr>

   <td width="546">void insert_node_at(list *lst, int index, int data)</td>

  </tr>

  <tr>

   <td width="546">This function inserts a new node that contains <strong>data</strong> at <strong>index </strong>of <strong>lst</strong> counting from the head (index starts from 0). You should use <strong>malloc</strong> to allocate memory to create the new node. Assume that <strong>index</strong> is between 0 and length of the list, both inclusive.</td>

  </tr>

 </tbody>

</table>




<table width="546">

 <tbody>

  <tr>

   <td width="546">void delete_node_at(list *lst, int index)</td>

  </tr>

  <tr>

   <td width="546">This function deletes the node at <strong>index </strong>of <strong>lst</strong> counting from the head (index starts from 0). You should use <strong>free</strong> to delete memory allocated. Assume that <strong>index</strong> is between 0 inclusive and the length of the list exclusive. If the head node is deleted, the next node at index 1 (before deletion) should be the next head, if such a node exists. If no next node exists, the head of <strong>lst</strong> should be set to <strong>NULL</strong>.</td>

  </tr>

 </tbody>

</table>




<table width="546">

 <tbody>

  <tr>

   <td width="546">void rotate_list(list *lst, int offset)</td>

  </tr>

  <tr>

   <td width="546">This function rotates the entire list by <strong>offset</strong> number of nodes. Using the example diagram before, a rotation of offset 1 will result in a list with head pointer to the second node, i.e., the node with data 2 right after the original head node. Assume that <strong>offset</strong> is non-negative. You should not be reallocating or modifying the data of the nodes for this rotation.</td>

  </tr>

 </tbody>

</table>




<table width="546">

 <tbody>

  <tr>

   <td width="546">void reverse_list(list *lst)</td>

  </tr>

  <tr>

   <td width="546">This function reverses the order of the nodes in <strong>lst</strong>. The head pointer of <strong>lst </strong>should also now point to the original “tail” node, i.e., the node that had a next pointer to the original head. You should not be reallocating memory for the nodes or modifying the data of the nodes, but instead <strong>modify the pointers</strong> for this reversal. You may use additional memory to store temporary data during the operation, though it is not necessary.</td>

  </tr>

 </tbody>

</table>




<table width="546">

 <tbody>

  <tr>

   <td width="546">void reset_list(list *lst)</td>

  </tr>

  <tr>

   <td width="546">This function deletes all nodes in <strong>lst</strong> and resets its head to <strong>NULL</strong>.</td>

  </tr>

 </tbody>

</table>




The folder structure of <strong>ex2</strong> is as follows:




<table width="546">

 <tbody>

  <tr>

   <td width="546"><strong>/ex2 </strong></td>

  </tr>

  <tr>

   <td width="546">node.h <strong>(not to be modified) </strong>ex2.c <strong>(not to be modified) </strong>node.c*.in / *.out (files used for testing)Makefile <strong>(not to be modified)</strong></td>

  </tr>

 </tbody>

</table>




You should <strong>only</strong> modify <strong>node.c</strong> for this exercise. Please take note that changes to any other file will be overwritten when we run the grading script.




After you have finished implementation, use the following command to compile your code:

<strong> </strong>

<h3>$ gcc -std=c99 -Wall -Wextra node.c ex2.c -o ex2</h3>




This will produce the executable <strong>ex2</strong> by running gcc compiler with c99 standard, enabling warnings, and creating an output ex2. You may use <strong>-Werror</strong> option in gcc to make all warnings into errors. We will not penalize marks for having warnings, but we may use them to aid us in finding bugs in your programs.




You can use the sample test case we have provided to test your code.




<h3>$ ./ex2 &lt; sample.in | diff sample.out –</h3>

(Note the <strong>–</strong> at the end!)




The above bash command passes the <strong>sample.in</strong> input file into the test runner and compares the output against the expected. Details about how this command runs follow:




<ul>

 <li>The bash spawns two processes. The first process runs ex2 and the second process runs diff.</li>

 <li>We used <strong>input redirection (</strong><strong>&lt;)</strong> to replace the standard input (stdin) with the file in for the first process (running ex2)</li>

 <li>We have made use of a <strong>pipe (</strong><strong>|)</strong> to pass the output from the first process (running the command <strong>./ex2 &lt; sample.in)</strong> into the input of the second process running (running the command <strong>diff sample.out –</strong>). The <strong>–</strong> sign stands for the second input file being replaced with standard input (here, with the output produced by ex2).</li>

</ul>




Apart from <strong>sample.in</strong>, we have two more test cases to help verify your program. To get the demo exercise grade for this lab, you have to show your lab TA that you are familiar with basic bash syntax and have a working circular linked list that works for all test cases.




Also, take note that the runner will call <strong>reset_list</strong> to delete all nodes in the list before it terminates the program. The only file that needs changes is <strong>node.c</strong>.




Refer below for an explanation of the sample input. The input file uses a specific numbering scheme to refer to the five functions defined above:




<table width="546">

 <tbody>

  <tr>

   <td width="546"><strong>sample.in</strong></td>

  </tr>

  <tr>

   <td width="546">1 0 1        // insert_node_at(lst, 0, 1)0                   // print_list(lst)1                   0 3        // insert_node_at(lst, 0, 3)01 1 2</td>

  </tr>

 </tbody>

</table>

0

1 0 100

0

<ul>

 <li>4 200</li>

</ul>

0

<ul>

 <li>1 // delete_node_at(lst, 1)</li>

</ul>

0

<ul>

 <li>2 // rotate_list(lst, 2)</li>

</ul>

0

<ul>

 <li>// reverse_list(lst)</li>

</ul>

0

<ul>

 <li>// reset_list(lst)</li>

</ul>

0

1 0 1000

0




<table width="546">

 <tbody>

  <tr>

   <td width="546"><strong>sample.out</strong></td>

  </tr>

  <tr>

   <td width="546">[ 1 ][ 3 1 ][ 3 2 1 ][ 100 3 2 1 ][ 100 3 2 1 200 ][ 100 2 1 200 ][ 1 200 100 2 ][ 2 100 200 1 ][ ][ 1000 ]</td>

  </tr>

 </tbody>

</table>




We defined specific macros for each of the functions:




#define PRINT_LIST 0

#define INSERT_AT 1

#define DELETE_AT 2

#define ROTATE_LIST 3

#define REVERSE_LIST 4

#define RESET_LIST 5




The function <strong>print_list</strong> has already been written for you within the runner ex2.c. Feel free to look at the <strong>ex2.c</strong> to understand how the runner works.  Understanding how the runner works will help greatly when doing the next exercise.




<h2>2.3. Exercise 3: Function Pointers</h2>




This exercise extends the functionalities of the circular linked list implementation by applying several operations on its nodes. These operations are added by making use of function pointers in C.




<h2>Function Pointer Overview</h2>




You can refer to <a href="https://en.cppreference.com/w/c/language/pointer#Pointers_to_functions">this link</a> for more information on function pointers. Unlike normal pointer, which points to memory location for <strong>data storage, </strong>a function pointer <strong>points to a piece of code (function)</strong>. By dereferencing a function pointer, we <strong>invoke the function </strong>that is referred by that pointer. This technique is commonly used in <strong>system call / interrupt handlers</strong>.




In C, it is possible to define a <strong>function pointer</strong> to refer to a function. For example:




<h3>void (*fptr) (int);</h3>




To understand this declaration (check out this rather <a href="https://cdecl.org/?q=void+%28*fptr%29+%28int%29%3B">handy website</a><a href="https://cdecl.org/?q=void+%28*fptr%29+%28int%29%3B">)</a>, imagine if you replace <strong>(*fptr)</strong> as <strong>F</strong>, then you have:

<strong> </strong>

<h3>void F (int);</h3>




So, <strong>F</strong> is “a function that takes an integer as input and returns nothing (void)”. Now, since <strong>(*fptr)</strong> is <strong>F</strong>, <strong>fptr</strong> is “<strong>a pointer to</strong> a function that takes an integer as input and returns nothing (void)”.




Let’s use the function pointers to define and use a group of functions that can <strong>map</strong> different operations to the circular linked list from exercise 2.




Exercise 3 is an extension of exercise 2. For this exercise, you must write the test runner ex3.c and node.c. The runner




<ul>

 <li><strong>reads the input file provided as a command line argument</strong> (reading from a file can be done using any library. We recommend using stdio (fopen, fclose, fread). Make sure that you gracefully handle an invalid file name.), and</li>

 <li><strong>applies the operations listed in the input file</strong> on the circular linked list.</li>

</ul>

The macros corresponding to the functions that can be applied on the list are:

#define SUM_LIST 0

#define INSERT_AT 1

#define DELETE_AT 2

#define ROTATE_LIST 3

#define REVERSE_LIST 4

#define RESET_LIST 5

#define MAP 6

INSERT, DELETE and LIST operations are similar with exercise 2 (no changes are needed). We have added <strong>MAP</strong> and replaced <strong>PRINT_LIST</strong> with <strong>SUM_LIST</strong>.

<strong>SUM_LIST </strong>function definition is provided in node.h. This function sums the data of all nodes in the list and prints out (at standard output) the sum.

In addition to the functionalities from exercise 2, we define a map function:




<table width="553">

 <tbody>

  <tr>

   <td width="553">void map(list *lst, int (*func) (int))</td>

  </tr>

  <tr>

   <td width="553">This function updates <strong>lst</strong> by applying <strong>func</strong> to the <strong>data</strong> element of every node</td>

  </tr>

 </tbody>

</table>

The <strong>map</strong> function (MAP) uses function pointers. You need to implement this function by applying the function func on each element of the circular linked list.

<strong>MAP</strong> can be used to apply five operations on the list. Indices for these operations are given below:

<table width="216">

 <tbody>

  <tr>

   <td width="23">0</td>

   <td width="193"><strong>add_one </strong></td>

  </tr>

  <tr>

   <td width="23">1</td>

   <td width="193"><strong>add_two</strong></td>

  </tr>

  <tr>

   <td width="23">2</td>

   <td width="193"><strong>multiply_five</strong></td>

  </tr>

  <tr>

   <td width="23">3</td>

   <td width="193"><strong>square</strong></td>

  </tr>

  <tr>

   <td width="23">4</td>

   <td width="193"><strong>cube </strong></td>

  </tr>

 </tbody>

</table>




The implementation for these functions is provided in file functions.c. The runner ex3.c simply calls the right function based on the index given in the input file.




To apply the five MAP operations, you will need to initialize an array of function pointers with indices 0 to 4. This array has already been declared in function_pointers.h, but not initialized. Use the index from the input file to call the corresponding map function. This array of function pointers is:




<h3>• named func_list,</h3>

<ul>

 <li>has been declared in h file, and</li>

 <li><strong>will need to be initialized in </strong><strong>c</strong>. You may choose to use <strong>update_functions</strong> (defined in function_pointers.h and implemented in function_pointers.c) to help you with the initialization. update_functions is called in the main function of ex3.c (please do not modify this call).</li>

</ul>










The runner should be easily extensible to allow for new operations for the map function <strong>without changing the implementation of </strong><strong>ex3.c and </strong><strong>node.c</strong>.

Adding or removing a new MAP operation should be done by modifying only the array of function pointers in function_pointers.c and its declaration in function_pointers.h.




For this exercise the file structure is as follows:




<table width="546">

 <tbody>

  <tr>

   <td width="546"><strong>/ex3 </strong></td>

  </tr>

  <tr>

   <td width="546">Makefile <strong>(not to be modified)</strong> node.h <strong>(not to be modified)</strong> ex3.c <strong> </strong>node.cfunction_pointers.cfunction_pointers.h <strong>(not to be modified) </strong>functions.c <strong>(not to be modified)</strong> functions.h <strong>(not to be modified)</strong>*.in / *.out (files used for testing)</td>

  </tr>

 </tbody>

</table>




As explained earlier, we provide the functions used by <strong>MAP</strong> in <strong>functions.c</strong> and <strong>functions.h</strong>. These files should not be modified.




Use the Makefile provided to compile your code:

<h3>$ make</h3>




Command make uses the instructions found in the Makefile to compile your code. You can also run <strong>make clean</strong> to clean up the executable. Note that you must either call <strong>gcc</strong> or <strong>make</strong> to compile your code (there is no need to call both of them, in sequence).




Test your ex3 as follows:

<h3>$ ./ex3 sample.in &gt; res.out</h3>

<strong>$ diff res.out sample.out</strong> (to compare your output with the given output)




Apart from the sample, we have provided two more test cases for testing. Do take note that getting the right answer for these files will not guarantee full marks for this exercise (see <strong>exercise 4</strong>). Please test your code rigorously on your own. Other test cases will be used during grading.




Your runner should also free any memory it allocates and reset the list before the program terminates.







A sample input and output are shown below:




<table width="546">

 <tbody>

  <tr>

   <td width="546"><strong>sample.in: </strong><strong> </strong></td>

  </tr>

  <tr>

   <td width="546">1 0 1        // first three same as ex21 0 31 1 20            // sums list and prints it6 0          // runs map on list with add_one function06 3          // runs map on list with square function06 4          // runs map on list with cube function0</td>

  </tr>

 </tbody>

</table>




<table width="546">

 <tbody>

  <tr>

   <td width="546"><strong>sample.out:</strong></td>

  </tr>

  <tr>

   <td width="546">69294889</td>

  </tr>

 </tbody>

</table>




When we pass <strong>sample.in</strong> to our program, it should output at standard output (console) the result of any <strong>SUM_LIST</strong> instruction found. This is why the <strong>sample.out</strong> file has 4 numbers (4 <strong>SUM_LIST</strong> instructions in our input file).




Some things to take note of for this exercise:




<ul>

 <li>input will always be valid (there is no need to do input validation on runner)</li>

 <li>the sum of list will be smaller than 2<sup>63</sup> – 1 and larger than -2<sup>63</sup> for any test cases we use (notice we use <strong>long</strong> data type for the function definition)</li>

</ul>







<h2>2.4. Exercise 4: Checking for Memory Errors</h2>




In this exercise, we introduce <strong>valgrind</strong>, a tool commonly used to identify and fix any kind of memory errors (memory leak detection / out of bound array access etc.). You might use <strong>valgrind</strong> for future lab assignments.




We want you to try using <strong>valgrind</strong> on the executable from <strong>ex2</strong> and <strong>ex3</strong>. You used <strong>malloc</strong> or <strong>free</strong> a couple of times in the code and there is a possibility of memory leaks occurring if any resource obtained dynamically is not freed.




To use valgrind, <strong>cd</strong> into <strong>ex2</strong> directory and run the below command:

<h3>  $ valgrind ./ex2 sample.in &gt; res.out</h3>

You should see output like this:

<table width="546">

 <tbody>

  <tr>

   <td width="546"><strong>Sample Output</strong></td>

  </tr>

  <tr>

   <td width="546">==3368== Memcheck, a memory error detector==3368== Copyright (C) 2002-2015, and GNU GPL’d, by Julian Seward et al.==3368== Using Valgrind-3.11.0 and LibVEX; rerun with -h for copyright info==3368== Command: ./ex2 &lt; sample.in==3368====3368====3368== HEAP SUMMARY:==3368==     in use at exit: 0 bytes in 0 blocks==3368==   total heap usage: 7 allocs, 7 frees, 8,824 bytes allocated ==3368====3368== All heap blocks were freed — no leaks are possible==3368====3368== For counts of detected and suppressed errors, rerun with: -v==3368== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)</td>

  </tr>

 </tbody>

</table>




As you can see, <strong>valgrind</strong> has done the hard work of checking for any potential memory leaks for us! Suppose our <strong>ex3</strong> had some memory leaks. <strong>valgrind</strong> detects memory problems and shows how to rerun to see additional details.  When running on the sample input, you might see output as follows:

<table width="546">

 <tbody>

  <tr>

   <td width="546"><strong>Sample Output</strong></td>

  </tr>

  <tr>

   <td width="546">==3388== Memcheck, a memory error detector==3388== Copyright (C) 2002-2015, and GNU GPL’d, by Julian Seward et al.==3388== Using Valgrind-3.11.0 and LibVEX; rerun with -h for copyright info==3388== Command: ./ex3 sample.in==3388====3388====3388== HEAP SUMMARY:==3388==     in use at exit: 8 bytes in 1 blocks==3388==   total heap usage: 7 allocs, 6 frees, 8,824 bytes allocated ==3388====3388== LEAK SUMMARY:==3388==    definitely lost: 8 bytes in 1 blocks ==3388==    indirectly lost: 0 bytes in 0 blocks==3388==      possibly lost: 0 bytes in 0 blocks==3388==    still reachable: 0 bytes in 0 blocks==3388==         suppressed: 0 bytes in 0 blocks==3388== Rerun with –leak-check=full to see details of leaked memory ==3388====3388== For counts of detected and suppressed errors, rerun with: -v==3388== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)</td>

  </tr>

 </tbody>

</table>




This exercise is not graded but take note that we will deduct marks if there are memory errors in either <strong>ex2</strong> or <strong>ex3</strong> (even if the expected output is correct).

<h2>2.5. Exercise 5: Shell scripting to find out more about our system</h2>




In the next two exercises, we will write some shell scripts! A shell script is a list of commands designed to be run by the Linux shell. Earlier when we talked about <strong>cd</strong> and <strong>pwd</strong>, commands you can use in the terminal (shell). You can think of a shell script as running a sequence of these commands. For this lab, we will be focusing on the <strong>bash</strong> shell.




Exercise 5 requires you to write a simple shell script to learn more about your operating system and system. Use the man pages and online search to find out about <strong>bash</strong>.




A simple <strong>bash</strong> shell script that prints the current working directory is as follows:




<table width="546">

 <tbody>

  <tr>

   <td width="546"><strong>check_dir.sh</strong></td>

  </tr>

  <tr>

   <td width="546">#!/bin/bash dir=$(pwd)echo Current directory: $dir</td>

  </tr>

 </tbody>

</table>




The first line of the script is known as an <em>interpreter directive</em>, and it starts with the magic sequence <strong>#!</strong> known as a shebang. The directive is parsed by the kernel and instructs the kernel to run the script using the given program, in this case <strong>/bin/bash</strong>. This directive can also be used for other shells (e.g., <strong>zsh</strong>, <strong>fish</strong>) and for other scripting languages (e.g., Python).




Following this, we just have a variable that takes in the return value of the <strong>pwd</strong> command, and we print it out using <strong>echo</strong>.




To run the above script, use the following commands:

<h3>$ chmod +x ./check_dir.sh $ ./check_dir.sh</h3>

<strong> </strong>

The first command helps to change the file permissions to make the script executable. The second command runs the script. You should be able to see your current directory being printed onto the screen.




The output of the script you are supposed to write for this exercise should look as follows:




<table width="546">

 <tbody>

  <tr>

   <td width="546"><strong>Sample Expected Output</strong></td>

  </tr>

  <tr>

   <td width="546">Hostname: xcne6Machine Hardware: Linux x86_64Max User Processes: 1541954User Processes: 9User With Most Processes: rootMemory Free (%): 64.6353Swap Free (%): 99.6441</td>

  </tr>

 </tbody>

</table>




The actual values differ based on the system you are using. We have provided in <strong>ex5</strong> folder a skeleton <strong>bash</strong> script <strong>check_system.sh</strong> that you can use to start work on this. You do not have to install anything else on your system to get the above information.




To get you started, here are some helpful commands that may be of use to you:




<h3>– sort – awk – pipe in shell (|)</h3>




As always, do check the man pages to find out more about these commands. You will need to discover the other commands on your own to complete this exercise.




Once you have figured out the commands that you might need, you can run them in the terminal to test them and copy them into the <strong>bash</strong> script once they give the output you desire.







<h2>2.6. Exercise 6: Know your syscalls</h2>




For this exercise, we will be writing another shell script to help us list the system calls done by a C program. A system call allows a user program to request services that are provided by the operating system. To find out what system calls are made by a program, we use a tool known as <strong>strace</strong>.




Within the <strong>ex6</strong> folder, you may find a sample C program <strong>pid_checker.c</strong> that prints its own process ID and its parent’s process ID. We have also given a <strong>bash</strong> script skeleton <strong>check_syscalls.sh</strong> for you to update.




You need to complete the <strong>bash</strong> script to obtain a report on the system calls made by the program and the time spent in each call.




The expected output has the following format (values might differ, depending on the program that you are running):




<table width="546">

 <tbody>

  <tr>

   <td width="546"><strong>Expected Output</strong></td>

  </tr>

  <tr>

   <td width="546">Printing system call reportProcess ID: 94510Parent Process ID: 11815% time     seconds  usecs/call     calls    errors syscall—— ———– ———– ——— ——— —————-   0.00    0.000000           0         1           read0.00    0.000000           0         2           write   0.00    0.000000           0         2           open0.00    0.000000           0         2           close0.00    0.000000           0         3           fstat0.00    0.000000           0         7           mmap0.00    0.000000           0         4           mprotect0.00    0.000000           0         1           munmap0.00    0.000000           0         3           brk0.00    0.000000           0         3         3 access   0.00    0.000000           0         1           getpid0.00    0.000000           0         1           execve0.00    0.000000           0         1           arch_prctl—— ———– ———– ——— ——— —————-100.00    0.000000                    31         3 total</td>

  </tr>

 </tbody>

</table>




Again, reading the Linux manual for <strong>strace</strong> should allow you to do this exercise rather quickly.







<h2>2.7. Exercise 7: Check your archive before submission</h2>




The script checks the following:




<ol>

 <li>The name or the archive you provide matches the naming convention mentioned in Section 3</li>

 <li>Your zip file can be unarchived, and the folder structure follows the structure presented in Section 3</li>

 <li>All files for each exercise with the required names are present</li>

 <li>Each exercise can be compiled and/or executed.</li>

 <li>The output your exercise produces using our sample input matches the expected output.</li>

</ol>




Once you have the zip file, you will be able to check it by doing:




<h3>$ chmod +x ./check_zip.sh $ ./check_zip.sh E0123456.zip (replace with your zip file name)</h3>

<strong> </strong>