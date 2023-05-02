Download Link: https://assignmentchef.com/product/solved-cits3402-assignment-1-2019-sparse-matrices
<br>
<h1>1      Details</h1>

This assignment is designed to provide students with experience implementing some fundamental mathematical codes. You are encouraged to read further than the provided notes on sparse matrices in order to complete the assignment. Please set aside enough time to complete the assignment as all functionality will require time to test, analyse and report upon.

Your ability to investigate code-performance is of more interest to us than your code’s performance. (We care more about what you do, not your machine).

<h1>2      Description</h1>

Matrix algebra underpins many compute intense applications in many fields (most fields of Engineering, Machine Learning, Scientific Modelling etc.); computers were originally used to crunch numbers so numbers we shall crunch.

Your goal, broadly speaking, is to:

<ul>

 <li>Create a piece of software implementing a variety of sparse matrix operations</li>

 <li>Ensure this software conforms to our input/output specification</li>

 <li>Performance test your software and comment on any speedup you observe (or lack thereof) in a brief report.</li>

</ul>

<h1>3        Sparse Matrix Introduction</h1>

<h2>3.1       What is a Matrix</h2>

A mathematical matrix is a rectangular array of numbers arranged in rows and columns. For simplicity we use the convention of (rows, columns) when giving dimensions. An example of a 3 × 2 matrix (read ’three by two’) is

(1)

In many practical cases involving matrix algebra, many elements will contain zero as their value. Storing all elements at all times wastes a potentially vast amount of memory in these cases. For a given machine this heavily restricts the size of problem able to be computed and so sparse matrices were developed to save space at the cost of more time. Loosely speaking, a matrix is considered ’sparse’ if it contains ≈ 10% non-zero elements.

The general idea is to save space by storing fewer zero elements (since they generally do not matter in any calculation). There are three broadly accepted sparse matrix representations used:

<h2>3.2        Coordinate Format (COO)</h2>

The most intuitive sparse matrix format specifies each non-zero element as a triple

<em>A<sub>i,j </sub></em>= (<em>i,j,</em>val)                                                                    (2)

For example, the matrix,

(3)

becomes

<em>X </em>= [(0<em>,</em>2<em>,</em>1)<em>,</em>(1<em>,</em>0<em>,</em>3)<em>,</em>(1<em>,</em>2<em>,</em>2)]                                                    (4)

This representation while simple can be cumbersome when wanting to look for all values in a particular row or column.

<h2>3.3         Compressed Sparse Row Format (CSR)</h2>

The compressed sparse row format stores a matrix with three arrays:

<ul>

 <li>NNZ: The non-zero values stored in row-major order (left to right, top to bottom)</li>

 <li>IA: The number of elements in each row. An extra element <em>IA</em>[0] = 0 is used by convention. This array can be used to index into the <em>NNZ </em>array for each <em>i</em>-th row</li>

 <li>JA: Stores the column index of each non-zero element.</li>

</ul>

For example, the matrix,

(5)

<table width="458">

 <tbody>

  <tr>

   <td width="441">becomes</td>

   <td width="17"> </td>

  </tr>

  <tr>

   <td width="441"><em>NNZ </em>= [1<em>,</em>3<em>,</em>2]</td>

   <td width="17">(6)</td>

  </tr>

  <tr>

   <td width="441"><em>IA </em>= [0<em>,</em>1<em>,</em>3<em>,</em>3]</td>

   <td width="17">(7)</td>

  </tr>

  <tr>

   <td width="441"><em>JA </em>= [2<em>,</em>0<em>,</em>2]</td>

   <td width="17">(8)</td>

  </tr>

 </tbody>

</table>

<h2>3.4         Compressed Sparse Column Format (CSC)</h2>

The compressed sparse column format is very similar to CSR format except the non-zero values are stored in a column-wise ordering, the <em>IA </em>array corresponds to the extent of each column and the <em>JA </em>array provides row indices. For example, the matrix,

(9)

<table width="458">

 <tbody>

  <tr>

   <td width="435">becomes</td>

   <td width="24"> </td>

  </tr>

  <tr>

   <td width="435"><em>NNZ </em>= [3<em>,</em>1<em>,</em>2]</td>

   <td width="24">(10)</td>

  </tr>

  <tr>

   <td width="435"><em>IA </em>= [0<em>,</em>1<em>,</em>1<em>,</em>3]</td>

   <td width="24">(11)</td>

  </tr>

  <tr>

   <td width="435"><em>JA </em>= [1<em>,</em>0<em>,</em>1]</td>

   <td width="24">(12)</td>

  </tr>

 </tbody>

</table>

<h1>4     Tasks</h1>

Your code will be a simple command-line application that will:

<ul>

 <li>Read in up to two dense matrix files</li>

 <li>Convert this matrix (these matrices) to a suitable sparse format.</li>

 <li>Perform a single matrix algebra routine specified by command-line</li>

 <li>Time the whole process and log the results to a file</li>

 <li>Cleanup all memory usage and terminate</li>

</ul>

We elaborate on the tasks required of you (and your code) below:

<h2>4.1      Reading in Files</h2>

Depending on the algebra operation requested one or two matrices will be required. These should be provided by command-line as .in files (see Section B).

<h2>4.2       Sparse Matrix Representation</h2>

You have a choice of using any of the three sparse matrix representations presented in Section 3. There will be pros and cons to each representation depending on what operation is requested; you will need to comment on this in your report.

<h2>4.3       Matrix Algebra Routines</h2>

We request five different operations to be implemented. They range in difficulty (and are presented in roughly increasing difficulty). Marks are distribution accordingly.

<strong>4.3.1         Scalar Multiplication</strong>

<strong>Type: Single matrix</strong>

<strong>Command-line argument: </strong>–sm %f For a matrix <em>A </em>and scalar (float) <em>α </em>compute:

<em>Y </em>= <em>α </em>· <em>A                                                                    </em>(13)

i.e. multiply each element of <em>A </em>by <em>α</em>.

The command line argument expects the scalar to be supplied immediately after (either an int or float). You only need to consider a floating point scalar when using floating-point matrices.

<strong>4.3.2       Trace</strong>

<strong>Type: Single matrix</strong>

<strong>Command-line argument: </strong>–tr

The trace(<em>t</em>) of a matrix <em>A </em>is given as:

<em>t </em>= <sup>X </sup>(<em>A<sub>i,i</sub></em>)                                                                   (14)

<em>i</em>=1<em>,n</em>

i.e. the sum of each diagonal element. Note: the Trace is only well defined for square matrices.

<strong>4.3.3         Matrix Addition</strong>

<strong>Type: Double matrix</strong>

<strong>Command-line argument: </strong>–ad

For two matrices <em>A </em>and <em>B </em>(of identical dimensions (<em>n,m</em>) their pair-wise sum is:

<em>Y<sub>i,j </sub></em>= <em>A<sub>i,j </sub></em>+ <em>B<sub>i,j</sub></em>∀<em>i,j</em>|<em>i </em>≤ <em>n,j </em>≤ <em>m                                                  </em>(15)

i.e. add each element of both matrices together.

<strong>4.3.4       Transpose</strong>

<strong>Type: Single matrix</strong>

<strong>Command-line argument: </strong>–ts

The transpose of matrix <em>A </em>(denoted <em>A</em><sup>0</sup>) is given by:

<em>A</em><sup>0</sup><em><sub>j,i </sub></em>= <em>A<sub>i,j</sub></em>∀<em>i </em>≤ <em>n,j </em>≤ <em>m                                                         </em>(16)

i.e. The rows of <em>A </em>become the columns of <em>A</em><sup>0 </sup>and vice-versa for the columns.

<strong>4.3.5          Matrix Multiplication</strong>

<strong>Type: Double matrix</strong>

<strong>Command-line argument: </strong>–mm

Note: Sparse matrix multiplication is a notorious bottle-neck in many codes; achieving speedup will be difficult and that is okay. Focus on implementing a simple, correct solution and working from there.

<h2>4.4       Timing and Logging</h2>

Your code is required to time the following events (in seconds)

<ul>

 <li>The time to load in and convert any matrix files.</li>

 <li>Time to execute the requested operation</li>

</ul>

This information must be logged to a .out file with the a header containing the following information:

<ul>

 <li>Operation requested</li>

 <li>File1</li>

 <li>File2 (if needed)</li>

 <li>Number of threads used</li>

</ul>

Followed by the result of your computation (single value or dense-matrix depending on the operation).

<h2>4.5     Report</h2>

Your report should be fairly brief but covers the following:

<ul>

 <li>The operation system used in your submission.</li>

 <li>The sparse matrix representation(s) used</li>

 <li>For each matrix operation implemented:

  <ul>

   <li>Description of the parallelism implemented</li>

   <li>Some informal reasoning about expected run-time and scalability</li>

   <li>Testing results</li>

   <li>Comment on the performance observed</li>

  </ul></li>

</ul>

We expect the report to be around six pages (including figures).

<h2>4.6     Restrictions</h2>

We place a number of restrictions on the type of matrix your solution will encounter and the design of your solution. They are briefly summarised below as a reminder

<ul>

 <li>Input File format – See App. B for a detailed description of the matrix file-type we use.</li>

 <li>Log-File format – See App. D for an example. Some further clarifications:

  <ul>

   <li>Operation requested – Provide the command line argument fed to the program as the label</li>

   <li>Input Filenames – Provide the command line argument fed to the program as the label</li>

   <li>Number of threads – Given as an integer</li>

   <li>Output filename – Provide the date and time of execution plus your student number(s) .out as the filename</li>

   <li>Computation result – Finally, output the result of the requested operation on the provided matrix (matrices). <em>Floating point results will be tested up to </em>1<em>e </em>− 6 <em>difference</em></li>

   <li>We provide example output files for all types of operations for reference</li>

  </ul></li>

 <li>Matrix Datatype

  <ul>

   <li>Integers</li>

   <li>Floats</li>

   <li>You will never be required to perform operations involving matrices of different data-types</li>

  </ul></li>

 <li>Command-Line Arguments – See App. C for a detailed description. We guarantee that we will test your solution with arguments presented in the order described and will only provide valid command line arguments.</li>

 <li>Input matrices – We provide a number of guarantees in our test matrices

  <ul>

   <li>All command line arguments provided will be valid</li>

   <li>All input files will be well-formed, valid and of a single data-type</li>

   <li>The dimensions of tested matrices will range in powers of two in the range [2<em>,</em>16<em>,</em>384]</li>

   <li>Input matrices are not guaranteed to be square</li>

   <li>Input matrices are not guaranteed to be the correct dimensions for the requested operation (e.g. we may ask for the Trace of a nonsquare matrix or addition of two matrices differing in dimension(s))</li>

  </ul></li>

</ul>




<h1>Marking Rubric</h1>

<table width="604">

 <tbody>

  <tr>

   <td width="121"> </td>

   <td width="121">Critera</td>

   <td width="121">HighlySatisfactory</td>

   <td width="121">Satisfactory</td>

   <td width="121">Unsatisfactory</td>

  </tr>

  <tr>

   <td width="121">File Reading (5)</td>

   <td width="121">Successfully reads in matrix files in the format specified. Implements arguments as specified.</td>

   <td width="121">Reads in matrix files correctly.</td>

   <td width="121">Attempts to read matrix files and attempts to implement command line arguments.</td>

   <td width="121">Fails to read matrix files and does not implement correct command line arguments.</td>

  </tr>

  <tr>

   <td width="121">Sparse matrix representation(10)</td>

   <td width="121">Implements suitable sparse matrix formats and coverts from dense to sparse formats correctly.</td>

   <td width="121">Uses appropriate sparse matrix formats and converts from dense to sparse formats correctly.</td>

   <td width="121">Attempts to convert from dense to sparse formats but is not always correct.</td>

   <td width="121">Does not convert from dense to sparse matrix formats correctly.</td>

  </tr>

  <tr>

   <td width="121">Scalarmultiplication (5)</td>

   <td width="121">Able to multiply both integer and floating point sparse matrices by a floating point scalar appropriate threading.</td>

   <td width="121">Is able to multiply both integer and floating point maitrices by a floating point scalar correctly.</td>

   <td width="121">Is able to multiply one type of sparse matrix by one type of scalar correctly.</td>

   <td width="121">Is unable to multipy a sparse matrix by a scalar.</td>

  </tr>

  <tr>

   <td width="121">Trace (5)</td>

   <td width="121">Computes the trace of both integer and floating point sparse matrices using appropriate threading.</td>

   <td width="121">Can compute the trace of integer and floating point matrices correctly.</td>

   <td width="121">Computes the trace of one type of sparse matrix correctly.</td>

   <td width="121">Is unable to compute the trace of a sparse matrix.</td>

  </tr>

  <tr>

   <td width="121">Matrix addition(10)</td>

   <td width="121">Correctly adds two sparse matrices together. Exits if not possible using appropriate thredaing.</td>

   <td width="121">Adds two integer or two floating point matrices together correctly. Exits gracefully if addition is not possible.</td>

   <td width="121">Correctly adds sparse matrices together. Does not exit gracefully if not possible.</td>

   <td width="121">Is unable to add two sparse matrices together correctly.</td>

  </tr>

  <tr>

   <td width="121">Transpose (10)</td>

   <td width="121">Computes the transpose of integer and floating point sparse matrices using appropriate threading.</td>

   <td width="121">Computes the transpose of integer and floating point matrices correctly.</td>

   <td width="121">Computes the transpose of one type of sparse matrix correctly.</td>

   <td width="121">In unable to compute the transpose of a sparse matrix correcly.</td>

  </tr>

 </tbody>

</table>




<table width="604">

 <tbody>

  <tr>

   <td width="121">Matrixmultiplication (15)</td>

   <td width="121">Correctly multiplies two matrices together using appropriate threading. Exits gracefully if not possible</td>

   <td width="121">Correctly multiplies two integer or two floating point matrices. Exits gracefully if multiplication is not possible.</td>

   <td width="121">Attempts to multiply two sparse matrices together. Does not exit gracefully if not possible.</td>

   <td width="121">Is unable to multiply two sparse matrices together.</td>

  </tr>

  <tr>

   <td width="121">Log file format(10)</td>

   <td width="121">Output files conform to the assignment specification</td>

   <td width="121">Output files contain the correct header and content in all cases.</td>

   <td width="121">Produces output files containing most information. Some minor formatting issues present.</td>

   <td width="121">Does not write correct content to output files.</td>

  </tr>

  <tr>

   <td width="121">Report (30)</td>

   <td width="121">Addresses all required points and is presented clearly. Testing is thorough and clear.</td>

   <td width="121">Report addresses all points effectively and is presented clearly. Performance testing is thorough and meaningful.</td>

   <td width="121">Report does not address all points required or some minor readiblity issues.</td>

   <td width="121">Report addresses few points or is very difficult to read.</td>

  </tr>

 </tbody>

</table>




<h2>                   A       Some words of advice</h2>

Writing, testing and reporting on a piece of threaded software will feel slightly different to your previous projects. Here are some humbly offered tips to get started:

<ul>

 <li>Start early – Said with every project but is especially true here. You will need time to test your final solution</li>

 <li>Practice good code management – Write your code in multiple files, comment as you go, use a good text editor and a debugger etc. Make life easy for yourself</li>

 <li>On sparse matrices – Start by thinking carefully about how you will manage your data separate to the matrix functions</li>

 <li>On matrix functions – Focus on correctness to begin with. A ’sub-optimal’ solution that exists will be more useful to you than a fantastic solution that you have not finished. Get something simple working, then make it fast.</li>

 <li>On command-line-arguments and log files – Read the specification carefully and clear up any possible confusions early.</li>

 <li>On the report – We are most concerned with your testing method and results. Again, start early while writing your code.</li>

</ul>

<em>Finally, feel free to ask the lab demonstrators and lecturer for advice if you get stuck.</em>

<h2>                  B        Dense Matrix File Format</h2>

There exist many sophisticated methods to store matrices in industry. For the sake of simplicity however we will use a plain-text representation of the data. Our format is quite simple

<ul>

 <li>Datatype: ”int” or ”float”</li>

 <li>Number of rows: An integer <em>n &gt; </em>0</li>

 <li>Number of columns: An integer <em>m &gt; </em>0</li>

 <li><em>n </em>× <em>m </em>space-separated integers/floats representing each value For example in</li>

</ul>

int 4

4

<ul>

 <li>0 0 0 0 1 0 0 0 0 1 0 0 0 0 1</li>

</ul>




This file represents the identity matrix

<sup></sup>1     0     0     0<sup></sup>

<sub></sub>0     1     0     0<sub></sub>

0   0     1   0                                                            (17)

0     0     0     1

For an example of a float matrix float1.in

float 4

4

1.0 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0.0 1.0 0.5 0.0 0.0 0.0 0.0 0.75

This file represents the following matrix

(18)

<h2>C          Command Line Arguments Glossary</h2>

To give direction in how to design your solution we require that your solution implements specific command line arguments (CLAs). You are allowed to implement more than these but these are a required minimum.

<ul>

 <li>Several operators, determines what matrix operation will be performed</li>

</ul>

(have been discussed previously)

<ul>

 <li>–sm – Scalar multiplication</li>

 <li>–tr – Trace</li>

 <li>–ad – Addition</li>

 <li>–ts – Transpose</li>

 <li>–mm – Matrix multiplication</li>

</ul>

<ul>

 <li>-f %s (%s) depending on the operation requested, one or more matrix files will need to be passed

  <ul>

   <li>Example: ./mysolution.exe –sm 2.0 -f matrix1.in</li>

   <li>Example: ./mysolution.exe –mm -f matrix1.in matrix2.in</li>

  </ul></li>

 <li>-t %d If present specifies the number of execution threads to use.</li>

 <li>-l If present, results will be logged to file</li>

</ul>

Again, you are allowed to add extra command line arguments but for full marks, our specified options <em>must </em>be implemented.

<h2>D        Log-file Format</h2>

In addition to the specified command line arguments we also have specific requirements for the .out files your solution must produce. Timing values are not accurate and are merely there for example. The following file would be the result of calling

./mysolution.exe –tr -f int1.in -t 4

at 11 : 59pm on the 22nd of August. Filename: 21726929_22082019_2359_tr.out

tr int1.in 4

4

0.001

0.0001

The following file would be the result of calling

./mysolution.exe –mm -f float1.in float2.in -t 4

at 12 : 00am on the 23rd of August. Filename: 21726929_23082019_0000_mm.out

mm float1.in float2.in 4 float 4

4

0.75 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0.75 0.375 0.0 0.0 0.0 0.0 0.5625

0.002

0.003

We have included a number of other example output files for your interest.