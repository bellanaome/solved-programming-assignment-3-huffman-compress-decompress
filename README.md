Download Link: https://assignmentchef.com/product/solved-programming-assignment-3-huffman-compress-decompress
<br>
<h1>Assignment Overview</h1>

In this assignment you will:

&#x25aa; Implement Huffman’s algorithm using efficient supporting data structures to support encoding and decoding of files

&#x25aa; Justify why your algorithm runs correctly on test examples with ASCII &#x25aa; Extend the basic I/O functionality of C++ to include bitwise operations Provided files:

HCNode.h, HCTree.h, Makefile, refcompress, refuncompress, .gitignore, asnlib/ (with binary.bat, check1.txt, check2.txt), submit.sh

We also provide some test files in ieng6, see “<em>Testing Guide”</em> near the end of this document.

<u>!                                                                                                                                                           </u>

<strong>Goal: To implement Huffman’s Algorithm, using ASCII I/O to write and read the encoded files.</strong>

<h1>Instructions</h1>

<u>Step 1. Implement HCNode and HCTree</u>

The HCNode and HCTree implementations will help you create Huffman tree/code for the input files.

Implement the following:

<ul>

 <li>Implement the h methods in a new file HCTree.cpp (from scratch). You can modify both files in any way you want.</li>

 <li>Implement the h methods (overloaded operator) in a new file HCNode.cpp. You can modify both files in any way you want.</li>

 <li>Because you do NOT need to implement or use BitInputStream and BitOutputStream yet, you will either create “dummy” versions of these classes (with both header and implementation files) to get the code to compile, or remove all references to them from the provided files (by commenting them out) and edit the Makefile.</li>

 <li>When you finish this step, you should have added cpp, and HCNode.cpp with all the methods implemented, except for encode() and decode() using BitInputStream and BitOutputStream, respectively.</li>

</ul>

<strong>Note</strong>: When implementing Huffman’s algorithm, you should use multiple data structures (e.g., a priority queue, etc.). You should also use good object-oriented design. For example, since a Huffman code tree will be used by both your compress and uncompress programs, it makes sense to encapsulate its functionality inside a single class accessible by both programs. With a good design, the main methods in the compress and uncompress programs will be quite simple; they will create objects of other classes and call their methods to do the necessary work.

————————————————————————-

<u>Step 2. Implement </u><u>Compression</u>

Create compress.cpp (from scratch too!) to compress small files in plain ASCII. The compress.cpp should generate a program named compress that can be invoked from the command line as follows &gt; ./compress infile outfile ./compress will:

&#x25aa; Read the contents of the file named (infile).

&#x25aa; Construct a Huffman code for the contents of that file

&#x25aa; Use that code to construct a compressed file named (outfile).

The challenge of this assignment is to translate the following high-level algorithm into real code:

Implement The Following Control Flow in compress.cpp:

<ul>

 <li>Open the input file for reading. (infile can be assumed here to have only ASCII text and to be very small (&lt;1KB))</li>

 <li>Read bytes from the file. Count the number of occurrences of each byte value. Close the file.</li>

 <li>Use the byte counts to construct a Huffman coding tree. Each unique byte with a non-zero count will be a leaf node in the Huffman tree.</li>

 <li>Open the output file for writing.</li>

 <li>Write enough information (a “file header”) to the output file to enable the coding tree to be reconstructed when the file is read by your uncompress You should write the header as plain (ASCII) text for this step. See <em>“the file header demystified” </em>right below for more details.</li>

 <li>Open the input file for reading, again.</li>

 <li>Using the Huffman coding tree, translate each byte from the input file into its code, and append these codes as a sequence of bits to the output file, after the header (a new line). For here, this will be done with plain ASCII characters ‘1’ and ‘0’.</li>

</ul>

(<strong>Note</strong>: you have just written your entire outfile in ASCII characters. Thus, your “compressed” file will actually be larger than the original one!  The point here is purely to get the algorithm working.) 8)<sub>    </sub>Close the input and output files.

9)<sub>    </sub>Test your solution. For more details, see the “<em>Testing Guide</em>” section near the end of this document.

<strong>Note</strong>: Your Makefile must create the executables “compress” and “uncompress” with those exact names from the “make all” command. The Makefile given to you already does this, so just make sure you don’t change this part of the file.

<h2>The “file header” demystified</h2>

Both the compress and uncompress programs need to construct the Huffman Tree before they can successfully encode and decode information, respectively. The compress program has access to the original file, so it can build the tree by first deciphering the symbol counts. However, the uncompress program only has access to the compressed input file and not the original file, so it has to use some other information to build the tree. The information needed for the uncompress program to build the Huffman tree is stored in the header of the compressed file. So the header information should be sufficient in reconstructing the tree. Note that the “file header” is not a .h file but rather the top portion of the compressed file.

Here is the way to design your header at the step: A straightforward, non-optimized method that you MUST USE in order to receive points!

It is to save the frequency counts of the bytes in the original uncompressed file as a sequence of 256 integers at the beginning of the compressed file. You MUST write this frequencybased header as 256 lines where each line contains a single int written as plain text.  E.g.:

0

0

0

23

145

0

0

…

Where 0’s represent characters with no occurrences in the file (e.g. above the ASCII values 0, 1 and

2 do not occur in the file), and any non-zero number represents the number of times the ASCII value occurs in the file.

————————————————————————-

<u>Step 3. Implement </u><u>Uncompress</u>

Create uncompress.cpp (from scratch!!) that will use your above implementations to support decompress for small files. The uncompres.cpp should generate a program named uncompress that can be invoked from the command line as follows

&gt; ./uncompress infile outfile

./uncompress will:

&#x25aa; Read the contents of the file named by its first command line argument, which should be a file that has been created by the compress program

&#x25aa; Use the contents of that file to reconstruct the original, uncompressed version, which is written to a file named by the second command line argument. The uncompressed file must be exactly identical to the original file.

Implement The Following Control Flow in uncompress.cpp:

<ul>

 <li>Open the input file for reading.</li>

 <li>Read the file header at the beginning of the input file, and reconstruct the Huffman coding tree.</li>

 <li>Open the output file for writing.</li>

 <li>Using the Huffman coding tree, decode the bits from the input file into the appropriate sequence of bytes, writing them to the output file.</li>

 <li>Close the input and output files.</li>

 <li>Test your solution. For more details, see the “<em>Testing Guide</em>” section near the end of this document.</li>

</ul>

————————————————————————-

<u>Step 4. Writeup</u>

Verify your compression in <strong>Report.doc</strong> One easy way to verify your compression is to manually compress some simple strings in the following way:

Implementation Checklist:

<ul>

 <li>Run your compressor using the provided input files: <strong>txt</strong> and <strong>check2.txt</strong>.</li>

 <li>Record the encoded output in <strong>doc</strong> (will be converted to PDF at Step 6.) Don’t just copy and paste the output, which would contain many zeros. Specify your header by the line numbers and non-zeros, and ignore the zero frequency lines. For example, line 48 12 line 49 10</li>

</ul>

Encoded string: 111001001

…

<ul>

 <li>Use the same input to manually construct a Huffman coding tree. Draw the Huffman coding tree, describe how you build the tree and how you find the code word for each byte in your output.</li>

 <li>Manually encode the strings and compare with your compressor output. If your output is wrong, explain why your hand-coded text is different from your compressor output and how you fixed it.</li>

 <li>We expect it to be 1-3 pages at this point. You have reached about 40% of this PA.</li>

</ul>

————————————————————————-

<u>Step 5. Extend your functionality to use Bitwise I/O to actually compress the files</u> You will now implement a full Huffman Compression program along with bitwise I/O.

Implementation Checklist:

<ul>

 <li>Implement Bitwise I/O (See “<em>Bitwise I/O</em>” below for details about why we are doing this)</li>

 <li>Implement BitInputStream</li>

 <li>Implement BitOutputStream</li>

 <li>Implement encode() and decode() using BitOutputStream and BitInputStream in</li>

</ul>

HCTree

<ul>

 <li>Implement compress with new designed header</li>

 <li>Implement uncompress <strong>Note</strong>:</li>

</ul>

&#x25aa; You must handle input files that will <strong>be MUCH larger than 1KB</strong> (up to 1GB so a particular byte value may occur up to 1 billion times in the file) See “<em>Efficient header design</em>” below for more details.

&#x25aa; You must handle input files that are <strong>not restricted to text files</strong> (binary files, images, videos etc.)

&#x25aa; To receive any credit, your compressed files must be at least as small as the compressed files produced by the reference solution, within <strong>~25%</strong> of the compression obtained by the reference, that is, to have smaller than ~125% of compresson by the reference solution, and your programs must properly compress and uncompress the files exactly.

&#x25aa; Compressing and uncompressing the files should be done within <strong>a timeout of 180 seconds</strong> for files smaller than 30mb.

&#x25aa; For bigger files (100-300mb) your method should be able to compress and uncompress <strong>within twice the time it takes for reference solution</strong>.

&#x25aa; You will gain 2 points for a correct implementation of compress that creates a smaller compressed file than the reference implementation (at least 1 byte smaller), running on two particular files, including a test file called warandpeace.txt on ieng6 (and one other we won’t tell you about in advance). This means that you should use a more efficient method for writing the header and Bitwise I/O to write and read the codes.

&#x25aa; You will gain 1 point if you are able to compress huge files (like 1GB). If you used a different algorithm/method for compressing huge files mention that in your writeup (Report.doc).

<h2>Bitwise I/O</h2>

If you encode your files using ASCII representations of 0 and 1, you don’t get any compression at all because you are using 1 byte to store the ‘0’ or ‘1’.  Once you’ve got your Huffman tree working, you’ll modify your code so that you can write data to a file one bit “at a time”. All disk I/O operations (and all memory read and write operations, for that matter) deal with a byte as the smallest unit of storage. But in this assignment, it would be convenient to have an API to the filesystem that permits writing and reading one bit at a time. Define classes BitInputStream and BitOutputStream (with separate interface header and implementation files) to provide that interface.

To implement bitwise file I/O, you’ll want to make use of the existing C++ IOstream library classes ifstream and ofstream that ‘know how to’ read and write files. However, these classes do not support bit-level reading or writing. So, use inheritance or composition to add the desired bitwise functionality. Refer to the lecture notes for more information.

<h2>Efficient header design</h2>

The reference solution header is not very efficient.  It uses 4-byte int to store the frequencies of each character, using 4*256 bytes for the entire header no matter what the statistics of the input file are.

In order to earn full credit for your final submission, you must BEAT our reference solution by coming up with a more efficient way to represent this header.

There are several possible solutions, but a good approach is to represent the structure of the tree itself in the header.  With some cleverness, it is possible to optimize the header size to about 10*M bits, where M is the number of distinct byte values that actually appear in the input file. However, we strongly encourage you to implement the naive (1024-byte) approach first, and do not attempt to reduce the size of the header until you’ve gotten your compress and uncompress to work correctly for the provided inputs.

————————————————————————-

<u>Step 6. Writeup again</u>

In your <strong>Report.doc</strong>, please add to the end that how you designed a more efficient header. Specifically, what are your algorithm and data structure to make a smaller header than the naive 1024-byte approach.

When you are done, take a deep breath, and <strong>convert your Report.doc to PDF</strong>.

<u>!                                                                                                                                                           </u>

<h1>Testing Guide</h1>

Getting the first 3 steps working is a great middle-step along the way to a full working program. Remember large programs are hard to debug. So test each function that you write before writing more code. We will only be doing “black box” testing of your program, so you will not receive partial credit for each function that you write. However, to get correct end-to-end behavior you must unit test your program extensively. For some useful testing tools, refer to <u><a href="https://docs.google.com/document/d/1VpO9jrzFSbb8t1G76GQIKIxZeCqiwutMGGpR1_R3y7Q/edit">this</a></u> doc. Don’t try out your compressor on large files (say &gt; 10 MB) until you have it working on the smaller test files (&lt; 1 MB).

Even with compression, larger files can take a long time to write to disk, unless your I/O is implemented efficiently. The rule of thumb here is that most of your testing should be done on files that take 15 seconds or less to compress, but never more than about 1 minute. If all of you are writing large files to disk at the same time, you’ll experience even larger writing times. Try this only when the system is quiet and you’ve worked your way through a series of increasing large files so you are confident that the write time will complete in about a minute.

<u>Edge Cases Checklist:</u>

<ul>

 <li>Empty File</li>

 <li>Files that contain only one character repeated many times 3) Think of more edge cases yourself!</li>

</ul>

<strong>The reference solution</strong> (refcompress / refuncompress):

You can use the “reference” implementations to verify your results (file size).
 <strong>Note</strong>:

&#x25aa; Your compress is not expected to work with refuncompress, and your uncompress is not expected to work with refcompress. The provided reference executable files are a matched pair.

&#x25aa; The reference binaries were compiled to run on ieng6. If you attempt to run it on a different architecture they will most likely not work.

<strong>Data files for test (Input test files): </strong>

The data files are available in the public folder on your ieng6 server (NOT in the starter code provided to you). The path for these input files is:

/home/linux/ieng6/cs100f/public/pa3_input_files

If you want to have them in your home directory for your convenience, we would advise against copying them, as ieng6 accounts have relatively limited storage space. Instead, create a symbolic link to the directory:

ln -s /home/linux/ieng6/cs100f/public/pa3_input_files

<u>!                                                                                                                                                         </u>