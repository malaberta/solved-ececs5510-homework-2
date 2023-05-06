Download Link: https://assignmentchef.com/product/solved-ece_cs5510-homework-2
<br>
<strong>Part I: Problems </strong>

<ol>

 <li>Consider the Bakery Algorithm, in which both the safety (mutually exclusive) and liveness (guarantees progress and bounded-waiting) properties hold. The proof for these properties depends on the following assumption: any process will stay in the critical section only for a finite amount of time. Suppose a process crashes while inside its critical section (for example, the program does a division that causes an uncaught division by zero exception in that thread), while other processes are still running:

  <ol>

   <li>Does this violate the safety property of the solution?</li>

   <li>Does this violate the liveness property?</li>

   <li>Does this violate the bounded waiting part of liveness?</li>

  </ol></li>

</ol>




For each of the questions above, provide a very brief explanation for your answer.

<ol start="2">

 <li>The Peterson’s mutual exclusion algorithm, which ensures no starvation, is presented in Figure 1. Consider the algorithms in Figures 2 and 3. Either prove or refute the following claims about the algorithms in Figures 2 and 3.

  <ol>

   <li>Algorithm provides mutual exclusion</li>

   <li>Algorithm provides deadlock freedom</li>

   <li>Algorithm provides starvation freedom</li>

  </ol></li>

</ol>

<h1>Figure 1</h1>

<h1>Figure 2</h1>

<h1>Figure 3</h1>

<ol start="3">

 <li> A solution to the mutual exclusion problem has been proposed in Figure 4. The line numbers are on the right. Does this solution satisfy the safety and liveness properties of the mutual exclusion problem? Give an informal proof or a violating adversary schedule for each of these properties.</li>

</ol>




<h1>Figure 4</h1>

<ol start="4">

 <li> The following algorithm (Fig. 5) is for two threads 1 and 2, and it makes use of two registers: x which can hold three values (0, 1, and 2); and y which can hold two values (0 and 1). Both threads can read and write registers x and y. The symbol i is used to designate the thread-id, and can be 1 or 2.</li>

</ol>




<h1>Figure 5</h1>

<ol>

 <li>Show that it satisfies mutual exclusion and deadlock-freedom for two threads.</li>

 <li>Does it satisfy starvation-freedom for two threads?</li>

 <li>Does it satisfy deadlock-freedom for three threads? That is, i can be 1, 2 or 3.</li>

 <li>Does it satisfy mutual exclusion for three threads? That is, i can be 1, 2 or 3.</li>

</ol>

For each question, you should either sketch a proof, or display an execution where it fails.

<ol start="5">

 <li>[7 Points] Consider the proposed algorithm to the mutual exclusion problem for two threads in Figure 6.</li>

 <li>Prove or dispute the safety and liveness properties of the algorithm.</li>

 <li>If the turn variable was initialized to -1, how will this affect the algorithm’s correctness properties?</li>

 <li>How does this algorithm compare to the Peterson’s algorithm. Discuss the differences in design choices that impact the safety and liveness properties of the algorithms. Is one better than the other?</li>

</ol>

<table width="267">

 <tbody>

  <tr>

   <td width="267">01: var flag: array [0..1] of boolean; 02: turn: 0..1;03:04: repeat05:   flag[i] := true;06:   while flag[j] do07:     if turn = j then08:     begin09:       flag[i] := false;10:       while turn = j do no-op;11:       flag[i] := true; 12:     end;13:14:   // critical section15:16:   turn := j;17:   flag[i] := false;18:19:   // remainder section20: until false;</td>

  </tr>

 </tbody>

</table>

<h1>Figure 6</h1>

<ol start="6">

 <li>[8 points] Reentrant Locks:</li>

</ol>

A reentrant mutual exclusion lock provides the same basic behavior and semantics as the regular lock, but with extended capabilities. A ReentrantLock is owned by the thread last successfully locking, but not yet unlocking it. A thread invoking lock will return, after successfully acquiring the lock, when the lock is not owned by another thread. The method will return immediately if the current thread already owns the lock.




State whether the following algorithms can be trivially modified to be reentrant capable, without any additional variables? Give reason.

<ol>

 <li>Peterson’s Lock</li>

 <li>Bakery Lock</li>

 <li>Filter Lock</li>

 <li>Lock in Figure 6 (irrespective of its correctness)</li>

</ol>

By trivial modification, we mean using an <em>if</em> conditional statement to check whether the current thread owns the lock and returning immediately.




<strong>Part II: Programming assignment [50 points] </strong>

Attached with this homework is a Java project that contains the implementation of <em>Peterson </em>and <em>Filter </em>locks, and simple benchmarks for testing the working and performance of these algorithms using a shared counter. Familiarize yourself with the code. Please configure IntelliJ to use JDK 8 to run the provided code and your development.

(http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

Do the following tasks:

<ol>

 <li>[15 points] Timestamp and Bakery lock:

  <ol start="2">

   <li>Provide an implementation of the Timestamp and TimestampSystem interfaces in Figure 2.10 of the textbook.</li>

   <li>Implement the <em>Bakery </em>lock algorithm using the implementation of the Timestamp interface.</li>

   <li>Compare the performance of <em>Bakery</em> lock with <em>Filter</em> and <em>Peterson </em>locks for different thread counts – 2 to as many threads your machine supports (e.g. my machine supports 8 threads), and preferably a high thread count value. For this purpose, you may modify the Test2.java which measures the runtime of each thread and reports the average. Show how the average thread runtime scales with the number of threads for both <em>Filter </em>and <em>Bakery </em></li>

  </ol></li>

</ol>




Fix the instantiation code for <em>Filter </em>lock so that it can be easily instantiated for any number of threads. Note that you should run Peterson’s algorithm won’t support more than two threads.

<ol>

 <li>Among the <em>Bakery </em>locks and <em>Filter </em>locks, which one performs better? Explain the reason.</li>

</ol>




<ol start="2">

 <li>[20 points] In the given benchmark, we are using only 2 threads. Consider a generalization of the two-thread Peterson lock by arranging a number of 2-thread Peterson locks in a binary tree, as follows. Each thread is assigned a leaf lock, which it shares with one other thread. Each lock treats one thread as thread 0 and the other as thread 1. In the tree-lock’s acquire method, the thread acquires every two-thread Peterson lock from that thread’s leaf to the root. The treelock’s release method for the tree-lock unlocks each of the 2-thread Peterson locks that thread has acquired, from the root back to its leaf. At any time, a thread can be delayed for a finite duration. (In other words, threads can take “naps”, or even “vacations”, but they do not “drop dead”.)

  <ol>

   <li>Run your new implementation against 16 competing threads modifying the Test class. Does each of the four properties mentioned above hold? Sketch a proof that it holds, or describe a, possibly infinite, execution where it is violated (you may also measure it by inserting trace statements in you code).</li>

   <li>Is there an upper bound on the number of times the tree-lock can be acquired and released between the time a thread starts acquiring the tree-lock and when it succeeds?</li>

   <li>The Test2 class measures the runtime of each thread and reports the average. Modify Test2 to run the new lock implementation. Run this benchmark class on your local machine as well as a high-core count server for different THREAD_COUNT (4, 8, 16, 32, and 64). Make sure you do not run any other application when running the benchmark on your local machine. Include the core count of your local machine in the report.</li>

  </ol></li>

</ol>




You may use any machine in the Rlogin cluster to satisfy the high-core count server requirement. The Rlogin cluster consists of 24 40-core server machines and 2 64-core server machines. Your report must indicate the core-count of the machine you used. The instructions to setup an account to access these machines have been communicated in a previous announcement. The Rlogin is a shared cluster, thus there may be multiple users using the same machine at any given time, interfering with your benchmark. Thus, to overcome this, you have to run your benchmark at 4-5 different times of the day (For example, 12AM, 6AM, 9AM, 12PM, 6PM, 9PM). You have report these results in a table similar to below for each THREAD_COUNT.

<table width="490">

 <tbody>

  <tr>

   <td width="88">Iterations</td>

   <td width="82">12AM</td>

   <td width="79">6AM</td>

   <td width="80">9AM</td>

   <td width="81">12PM</td>

   <td width="79">6PM</td>

  </tr>

  <tr>

   <td width="88">1</td>

   <td width="82"> </td>

   <td width="79"> </td>

   <td width="80"> </td>

   <td width="81"> </td>

   <td width="79"> </td>

  </tr>

  <tr>

   <td width="88">2</td>

   <td width="82"> </td>

   <td width="79"> </td>

   <td width="80"> </td>

   <td width="81"> </td>

   <td width="79"> </td>

  </tr>

  <tr>

   <td width="88">3</td>

   <td width="82"> </td>

   <td width="79"> </td>

   <td width="80"> </td>

   <td width="81"> </td>

   <td width="79"> </td>

  </tr>

 </tbody>

</table>

Note that every time you login into Rlogin, you will be provided a random machine in the cluster. You must choose a particular machine for all your tests. Indicate the machine name in your report. You can use “hostname” to find the machine name initially. Then, even if you are given a different machine you can connect to the intended machine with the following command:




ssh &lt;yourid&gt;@&lt;hostname&gt;




You must also plot the average runtime vs THREAD_COUNT as a bar graph. There must be two bars (one for local machine and another for server machine). Essentially, you should compute the average value of each table and construct the graph. A sample has been provided below:







<strong>Note that as you move to higher THREAD_COUNT values on your local machine, you might experience machine freezes. </strong>In such cases, you may ignore reporting that and other higher THREAD_COUNT values. (For example, if you experience intermittent freezes when running with THREAD_COUNT=16, it is advisable to ignore THREAD_COUNT=16,32,64). However, you should not have any issues with the Rlogin machines since they are capable of handling such high thread counts.




[Hint: The benchmark may use the provided binary tree implementation using Java generics. Balance the binary tree using an appropriate order of nodes insertions. Feel free to implement your own classes for this problem.]

<ol start="3">

 <li>[15 points] The L-exclusion problem is a variant of the starvation-free mutual exclusion problem, described as follows: as many as L threads may be in the critical section at the same time, and fewer than L threads might fail (by halting) in the critical section.</li>

</ol>




An implementation of an algorithm for this problem must satisfy the following conditions:

<ol>

 <li>L-Exclusion: At any time, at most L threads are in the critical section.</li>

 <li>L-Starvation-Freedom: As long as fewer than L threads are in the critical section, then some thread that wants to enter the critical section will eventually succeed (even if some threads in the critical section have halted).</li>

</ol>




Modify your implementation of the Bakery algorithm (from Question 1) and convert it into an L-exclusion algorithm. Call this class LBakery. Reason about the correctness of your design in about 50-100 words. Write a test program (not a unit test) and produce a trace to show that more than one (but less than L) threads are in the critical section at the same item.

Write your answers for Part I and Part II in a PDF file named <em>hw2_&lt;yourPID&gt;.pdf</em>. Zip up the PDF together with the source code for Part II and save it in a file called h<strong>w2_&lt;myPID&gt;.zip</strong>. Submit the archive as Homework 2 on the class’s Canvas page before the deadline.




<strong>Rlogin Registration instructions </strong>

<ul>

 <li>Create an account on – <u>https://admin.cs.vt.edu/</u></li>

 <li>Create the SLO password according to the password policy (7 characters, one uppercase letter, one lower case letter, one special character or number). This is the password that will be used to access Rlogin.</li>

 <li>Wait for  an  hour,  and  use  the  following  command  on  Terminal  (Windows  users,  see  below) to login:</li>

</ul>

ssh  <u><a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="bdc4d2c8cfe2cdd4d9fdcfd1d2dad4d393dece93cbc993d8d9c8">[email protected]</a></u>

<ul>

 <li>In case you can’t login into Rlogin, you will have to use Virginia Tech’s Remote Access VPN. <u>https://www.nis.vt.edu/ServicePortfolio/Network/RemoteAccess-VPN.html</u></li>

 <li>Rlogin accounts of non-CS majors are deleted at the end of every semester. So, if you are a nonCS major and had an account previously, you will have to create a new account.</li>

</ul>

<strong>For Windows users:  </strong>

<ul>

 <li>You can either use PuTTy or MobaXterm to login into Rlogin.</li>

 <li>Or you can install a Unix-like environment for Windows such as Cygwin or msys2. I suggest msys2 (Follow the guide here: https://www.msys2.org/). Follow the guide in the link. Install OpenSSH through the following command: pacman -S openssh</li>

 <li>You also have an option of using ‘Windows Subystem for Linux’ – <u>https://docs.microsoft.com/en-us/windows/wsl/install-win10</u></li>

</ul>