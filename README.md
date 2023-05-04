Download Link: https://assignmentchef.com/product/solved-csci262-csci862-system-security-assignment-1-solution
<br>
<strong>Part One: Short answer questions:                                                 4 Marks</strong>

<ol>

 <li>Determine the entropy associated with the following method of generating a password. <strong>1 Mark</strong></li>

</ol>

Choose, and place in this order, one lower case letter, following by one upper case letter, followed by two digits, followed by @, followed by two letters, each upper or lower case, and thSen followed by three symbols drawn from the set {$,9,5,v,w,J}. Finally, apply the hash function Tiger to give an output string in hex which will be used as a password.

Assume random choices are made with equal likelihood of each symbol from the space being chosen from. So for a random digit there are 10 possibilities, each chosen with probability 1/10.

<ol start="2">

 <li>Generate a BLP lattice–structured system where the objects and subjects are appropriately levelledto give access consistent with the access control matrix below. You need to describe the process by which you obtain your lattice. R and W correspond, respectively, to read and append. You are to use only the mandatory BLP rules, and a default allow in place of the discretionary rule. Be sure to add a level as necssary to ensure this is a lattice. <strong>2 Mark</strong></li>

</ol>

<table width="250">

 <tbody>

  <tr>

   <td width="29"></td>

   <td width="32"><em>O</em><sub>1</sub></td>

   <td width="42"><em>O</em><sub>2</sub></td>

   <td width="42"><em>O</em><sub>3</sub></td>

   <td width="32"><em>O</em><sub>4</sub></td>

   <td width="32"><em>O</em><sub>5</sub></td>

   <td width="42"><em>O</em><sub>6</sub></td>

  </tr>

  <tr>

   <td width="29"><em>S</em><sub>1</sub></td>

   <td width="32"><em>R</em></td>

   <td width="42"><em>R</em></td>

   <td width="42"><em>R</em></td>

   <td width="32"><em>R</em></td>

   <td width="32"><em>R</em></td>

   <td width="42"><em>RW</em></td>

  </tr>

  <tr>

   <td width="29"><em>S</em><sub>2</sub></td>

   <td width="32"><em>R</em></td>

   <td width="42"></td>

   <td width="42"></td>

   <td width="32"><em>W</em></td>

   <td width="32"><em>W</em></td>

   <td width="42"><em>W</em></td>

  </tr>

  <tr>

   <td width="29"><em>S</em><sub>3</sub></td>

   <td width="32"><em>R</em></td>

   <td width="42"><em>RW</em></td>

   <td width="42"><em>RW</em></td>

   <td width="32"></td>

   <td width="32"><em>W</em></td>

   <td width="42"><em>W</em></td>

  </tr>

  <tr>

   <td width="29"><em>S</em><sub>4</sub></td>

   <td width="32"><em>R</em></td>

   <td width="42"></td>

   <td width="42"></td>

   <td width="32"><em>R</em></td>

   <td width="32"></td>

   <td width="42"><em>W</em></td>

  </tr>

  <tr>

   <td width="29"><em>S</em><sub>5</sub></td>

   <td width="32"><em>R</em></td>

   <td width="42"></td>

   <td width="42"></td>

   <td width="32"></td>

   <td width="32"></td>

   <td width="42"></td>

  </tr>

  <tr>

   <td width="29"><em>S</em><sub>6</sub></td>

   <td width="32"><em>R</em></td>

   <td width="42"><em>R</em></td>

   <td width="42"><em>R</em></td>

   <td width="32"></td>

   <td width="32"><em>R</em></td>

   <td width="42"></td>

  </tr>

 </tbody>

</table>

<ol start="3">

 <li>For the following collection of statements, describe the sets of actions, objects, and subjects; anddraw an access control matrix to represent the scenario. <strong>1 Mark </strong>Alice can climb trees and eat apples.</li>

</ol>

Bob can climb fences, eat apples, and wave flags.

Trees can hurt apples.

Carol can jump waves and wave flags.

<strong>Part Two: Implementing a rainbow table                                      6 Marks</strong>

You are to write a program, in C/C++, Java or Python, that should run using the following instruction:

$ ./Rainbow Passwords.txt

where the file Passwords.txt contains a list of possible passwords. The password file contains a password per line, as in the provided words file and consists of strings of printable characters. Any password used must be taken from this file, so the only stored hash information needs to relate to those entries in the file.

The program is used to find pre–images for given hash values. Rainbow tables can be used to solve pre–image problems for hash functions. At the simplest level they can simply be a list of hash values and the corresponding pre-images, often from some dictionary. This can be expensive in terms of storage space however, and a more efficient way of identifying pre-images involves the use of the hash function and reduction functions.

<strong>First step (3 marks)</strong>: Your program will do some initial computations to generate the rainbow table. The process is as follows:

<ol>

 <li>Read in the list of possible passwords. Report on the number of words read in. (<strong>5 mark</strong>)</li>

 <li>For each previously unused word <em>W</em>, first mark it as used and then carry out the following process (<strong>5 marks</strong>):

  <ul>

   <li>Apply the hash function <em>H </em>to the word <em>W </em>to produce a hash value <em>H</em>(<em>W</em>), which we refer to as the current hash.</li>

   <li>Apply the reduction function <em>R </em>to the current hash, which will give a different possible password which should be marked as used and then hashed. The resulting hash value is recorded as the current hash.</li>

   <li>Repeat the previous step four times. You can deal with collisions if you like but are not requiredto.</li>

   <li>Store the original word <em>W </em>and the final current hash as an entry in your rainbow table.</li>

  </ul></li>

 <li>To assist with the later identification of the pre–images you should sort the rainbow table based onthe hash values (<strong>5 mark</strong>).</li>

 <li>Output the list of words and corresponding ”final current hashes” to a text file txt. Report to standard out the number of lines in your rainbow table (<strong>0.5 mark</strong>).</li>

</ol>

<strong>Second Step (3 marks)</strong>: You are now ready to carry out the second part of the exercise, finding pre– images. Request a hash value from the user. There should be appropriate error checking as to the length of the input string etc. The process of identifying the pre–image for the provided hash value is sketched as follows:

<ol>

 <li>Check if the hash value is in the rainbow table (<strong>1 mark</strong>).</li>

 <li>If the hash value isn’t in the rainbow table you reduce and hash until you get a hash value that isin the rainbow table, or until you have done the reduce and hash enough times that it’s clear from the way the rainbow table is generated that something is wrong. Display an appropriate message if this happens (<strong>1 mark</strong>).</li>

 <li>Once you have identified the relevant hash value in the table you take the corresponding passwordand hash it. If that is your hash value you have your pre–image. If it isn’t, then reduce and hash again, until the reduced word hashes to the hash value being searched for (<strong>5 mark</strong>).</li>

 <li>Output the releative reduced word, that is your pre–image (<strong>5 mark</strong>).</li>

</ol>

A reduction function is designed to take a valid hash value and return a valid password, in this case a valid word from Passwords.txt. The reduction function to be used should be based on the number of words in the Passwords.txt file, and since that isn’t a fixed length file your method needs to be dynamic. You should find a way to convert a hash value to an integer that identifies one of the passwords. You can define yourself a reduction function <em>R </em>or find some examples online. You should describe how your reduction function works in readme.txt.

You should use MD5 as the hash function. You don’t need to implement the MD5 hash function by yourself. You can find such a file online. Provide a reference if you use any open source implementation.

<ol>

 <li>Submission is via Moodle.</li>

 <li>Include the compilation instructions with your submission in a file txt. That file should also contain a description of how you do the reduction. If no such file exists in your submission then you will get <strong>zero </strong>for this Part two.</li>

 <li>Late submissions will be marked with a 25% deduction for each day, including days over the weekend.</li>

 <li>Submissions more than three days late will not be marked, unless an extension has been granted.</li>

 <li>If you need an extension apply through SOLS, if possible <strong>before </strong>the assignment deadline.</li>

 <li>Plagiarism is treated seriously. Students involved will receive zero.</li>

</ol>