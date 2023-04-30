Download Link: https://assignmentchef.com/product/solved-geological-computing-homework-2-flowcharts-and-scripting
<br>
<h1>Introduction</h1>

Geoscientists are awash in data. It is now possible to collect and use vast amounts of data in a typical geologic or geophysics project. Data collection is often highly automated. Locations are determined using a global positioning system (GPS) and sensors collect data at high rates. Huge datasets are also available from the internet. Many projects require the use of <em>on-line </em>data, such as bathymetric data, digital elevation models, or seismic hazard catalogs. This is all a bit of a double-edged sword. The quality of the science is generally improved by the increase in resolution that accompanies high volumes of data. On the other hand, it can be quite time-consuming and laborious to plow through these large data sets. What problems are associated with large data sets? A few are:

<ul>

 <li>Large data sets make the <em>point and click </em>style approach to data analysis intractable. It does no one any good to try to <em>highlight </em>30,000 measurements in a single file.</li>

 <li>Data sets come in an infinite variety of file formats. Different machines, different organizations, and different applications often save data sets in unique ways. It is crucial to be able to extract information from these various formats.</li>

 <li>Problems arise performing simple, repetitive calculations involving data extracted from large data sets. For instance, it may be appropriate to calculate a mean and standard deviation for some fraction of data stored in a file, or to add a correction to each data value in a file.</li>

 <li>Pre-processing is often necessary to transform data sets into a form that can be visualized using programs like GMT.</li>

</ul>

Today, these issues are ubiquitous in the discipline – a situation that simply did not exist in the recent past. Geoscientists are not alone. Most scientists are now faced with the need to handle large amounts of data in an efficient manner.

Fortunately, computer science has developed tools for manipulting large data sets that geoscientists can exploit. These include a number of high-level scripting languages designed to manipulate data files. A small subset of scripting languages include: awk, nawk, gawk, sed, Python, Perl (Practical Data Extraction Language); there are many others. These scripting tools have a great deal of power for manipulating and managing data beyond what we will be using. Perl and Python are particularly adept at manipulating databases on the worldwide web (WWW) and processing data, line-by-line, from files. For this class you are encouraged to explore the use of Python and/or Perl. Each of these scripting languages is extensively documented with howto’s and code examples via the WWW. Start your exploration by looking up Perl and Python in Wikipedia or just <em>google </em>Perl or Python.

<h1>Perl &amp; Python Examples</h1>

Most Perl or Python scripts written in this class will involve the manipulation of a data file.

<h2>Example 1</h2>

This first example <em>opens </em>a data file, <em>reads </em>from the data file one line at a time, <em>splits </em>each line into separate data elements, <em>manipulates </em>one of the data elements (does a little math), and <em>prints </em>out the transformed and original data. Try this and see if you understand the output. The output will be printed to the computer screen. Notice the similarities and the differences between the Python and the Perl scripts. Each language has its own unique syntax.

<h3>Perl script: example1.pl</h3>

open (IN, “&lt;$ARGV[0]”) || die (“Cannot open $ARGV[0]: $!”);

@MyData = &lt;IN&gt;;

foreach $line (@MyData) {

($data1, $data2) = split (” “, $line); $new_value = -3.28 * $data1; print (“$new_value $data2
”);

}

<h3>Python script: example1.py import sys</h3>

with open (sys.argv[1], “r”) as file: MyData = file.readlines() for line in MyData: line = line.strip() data1, data2 = line.split(” “) value = float(data1) new_value = -3.28 * value print (new_value, data2)

Let us review the code:

<strong>import </strong>Command line parameters or arguments, as they are often called, are identified by the <em>argv </em>variable. The Python script requires an additional code library (sys) to interpret command line arguments. The <em>import </em>directive loads this library into your python working space. Perl, on the other hand, identifies ARGV as a special variable to keep track of the command line arguments. In both cases this variable is actually a list, known as an array, with individual array elements accessed by a numerical index. In Perl, the first command line argument after the script name is indexed as 0, in Python this same argument is indexed as 1. It is possible to have multiple command line arguments; their names would be referenced with increasing index numbers following the appropriate syntax for each scripting language (sys.argv[2], $ARGV[3], etc).

<strong>open </strong>The first action, <em>open</em>, expects the name of the input file to be provided as an argument on the command line. Note that in Perl, the special variable <em>$ARGV[0] </em>refers to the name of this file; in Python this file is referenced by sys.argv[1]. The

|| die (“Cannot open $ARGV[0]: $!”);

symbols indicate that the Perl script should stop and output a message to the terminal, if the expected data file could not be opened. After a successful <em>open</em>, Perl can now access the file by using its <em>file handle</em>, <em>IN</em>. The Perl code

@MyData = &lt;IN&gt;;

causes each line from the file to be read into the array, @MyData. Notice that in Perl an array variable begins with the symbol <strong>@</strong>; a regular variable begins with the symbol <strong>$</strong>. Python uses the statement <em>with </em>to handle the opening and closing of files; Python has a set of file <em>methods </em>that perform various file operations. The method <em>file.readline() </em>reads each line of data from a file and stores them in the array named <em>MyData</em>.

<strong>for loop </strong>In Perl, a loop structure begins with the keyword <em>foreach </em>and indicates that a series of identical steps will be performed on a series of variables, in this case the variables contained in the data array, <em>@MyData</em>. The series of actions performed by the <em>foreach </em>loop are contained within the symbols, <em>{}</em>. In Python the loop structure begins with the keywork <em>for</em>, the data array is called <em>MyData</em>, and the series of loop steps follow the symbol <strong>:</strong>. For each pass through the loop the variable, <em>$line </em>(<em>line </em>in Python), will hold one complete <em>line </em>of data from the data file and the code in the loop will operate on or transform this data.

<strong>split </strong>Each line of data must then be split into individual data elements that the script will act upon. Here, each line is split into 2 data elements, <em>$data1 </em>and <em>$data2 </em>(<em>data1 </em>and <em>data2 </em>in Python). In this case a <em>white space </em>or non-printing character separates each data element. This <em>white space </em>could be represented by spaces or tabs or a newline. In Python a newline is special and must be removed by the string method <em>line.strip()</em>. Try deleting this line from the python script and see what happens to the output when you run the code. Python is sensitive to indentation and new lines. Notice that each step in the for loop must be on one line and indented to the same tab-stop. Perl uses the semi-colon (;) to indicate the end of a code action. Your Perl script will fail to to run if you forget any semi-colons. <strong>math step </strong>Now some math, each data1 element will be multiplied by -3.28 and stored in a new variable, <em>$new value</em>.

<strong>print </strong>The last loop action is to print out a line of data, the transformed data, <em>$new </em><em>value </em>or <em>new </em><em>value </em>in Python), and the original data (<em>$data2 </em>or <em>data2 </em>in Python). Notice that in Perl the data to be printed is enclosed in quotes, ” ” and a new line symbol,




appears at the end of the line. This symbol places the cursor at a new line <em>(</em><em>very important, otherwise all the data will be printed on one line)</em>. In Python, each data value to be printed is just separated by a comma.

Two more steps remain, running the script and saving the printed output to a file. These steps happen together on the command line, typed as follows:

perl myscript.pl mydatafile.txt &gt; myoutputfile.txt

The keyword, <strong>perl</strong>, invokes the Perl interpreter. The name of the Perl script is typed next, in this case, <em>myscript.pl</em>, followed by the name of the data file, <em>mydatafile.txt</em>. The following symbol, <em>&gt;</em>, is called a redirection symbol. The action of this symbol causes output from the Perl script (<em>i.e. </em>the stuff after the <em>print </em>action, that is listed between the quotes) to be redirected and saved to a file. The name of the file, in this case, is <em>myoutputfile.txt</em>. To perform these steps using the Python script and the python interpretor type as follows: python3 example1.py mydatafile.txt &gt; myoutputfile.txt

Note: we are using the newer, <em>python3 </em>interpretor, hence <strong>python3 </strong>is the correct syntax for invoking this interpretor. Let’s look at a supposed line of input from our data file, <em>mydatafile.txt</em>:

5 4

20.1 40

54 78

3 0.7

99 305

The array assignment in PERL(or Python) looks like this. The first pass through the <em>foreach (or for) </em>loop gives

$data1 (or data1) = 5

$data2 (or data2) = 4

The second pass through the loop gives:

$data1 (or data1) = 20.1

$data2 (or data2) = 40

and so on for each line in the input date file. Suppose, instead, the values in the input data file are separated by commas, such as in a <em>.csv </em>file:

400234,3402202

400235,3402201

400236,340219

To read these values you would modify the <em>split </em>action of the script to separate variables by commas rather than white space:

($data1, $data2) = split (“,”, $line); or Python syntax:

data1, data2 = line.split(“,”)

The split operation works exactly the same as with spaces, except that the line is split at the commas. The loop acts on each line of the input data file until the end of the file and then the script stops.

<h2>Example 2</h2>

Geophysicists are always rearranging columns in their data files. For example, suppose you have a file of gravity values. The first column is the latitude, the second column longitude, the third column the gravity reading, the fourth column is the free air correction, and the last column is the simple Bouguer anomaly. Consider these 2 lines of data from a text file:

24.093 -87.003 23.22 20.78 20.99

24.165 -86.954 23.41 20.98 21.03

Suppose you want to contour the simple Bouguer anomaly in GMT (Generic Mapping Tools). Note that GMT would prefer to have the longitude, or <em>x</em>, in the first column and the latitude, or <em>y </em>in the second column.

<h3>Perl script: example2.pl</h3>

A Perl script that is slightly modified from Example 1 makes short work of this:

open (IN, “&lt;$ARGV[0]”) || die (“Cannot open $ARGV[0]: $!”);

@MyData = &lt;IN&gt;;

foreach $line (@MyData) {

($latitude, $longitude, $grav, $free_air, $bouguer) = split ” “, $line; print “$longitude $latitude $bouguer
”;

}

<h3>Python script: example2.py</h3>

Similarly, the Python script that would perform this task is as follows:

import sys

with open (sys.argv[1], “r”) as file: MyData = file.readlines() for line in MyData: line = line.strip() latitude, longitude, obs_grav, free_air_grav, bouguer_grav = line.split(” “) print (longitude, latitude, bouguer_grav)

The output file contains three columns of data <em>(longitude latitude bouguer)</em>. One line of the output file would look this:

-87.003 24.093 20.99

<h2>Example 3</h2>

Suppose you need to count the number of gravity readings in a file.

<h3>Perl script: example3.pl</h3>

open (IN, “&lt;$ARGV[0]”) || die (“Cannot open $ARGV[0]: $!”);

@MyData = &lt;IN&gt;; $total = 0; foreach $line (@MyData) { $total++; }

print “Total number of readings = $total
”;

<h3>Python script: example3.py import sys</h3>

total = 0 with open (sys.argv[1], “r”) as file: MyData = file.readlines() for line in MyData:

total += 1

print (“total lines in file = “,total)

In Perl, ++, the increment operator, increases the value of the variable <em>$total</em>, by one, each pass through the loop, thus, counting each line in the file. The total number of lines counted is maintained by the variable <em>$total</em>. In Python, the variable <em>total </em>is incremented by += 1.

<h1>Writing, Editing, and Running Scripts</h1>

The process of wrinting, editing and running a script is summarized by the flowchart in Figure 1. First the script is created with a text editor. A Perl script is saved with a <em>.pl </em>file extension; a Python script is saved with a <em>.py </em>file extension. The file extension is a visual clue, even before the file is opened, indicating that the file is a particular type of script.

Scripts can be executed, or run, from the command line using the syntax shown previously. At this point, there are two possible outcomes: 1) the script executs without any errors, or 2) the script fails to execute and gives one or more error messages. If there were errors, lots of text usually gets printed out to the terminal and words like <em>error </em>or <em>warning </em>will appear. The best plan of attack, is to scroll back to the first error listed and note the line number the interpreter gives for the error location in the file. Sometimes warnings can be ignored, but errors need to be fixed. Fixing errors involves opening the script with a text editor and fixing the lines that are causing the errors. It is usually best to fix the first error listed and then try to run your script again. Often, multiple errors are all related to the first error listed, so just fix the first error and try running the script again. This sequence can take some time. It is often difficult to discover errors when first beginning to write programs. Persistence and practice is the key. All errors can be fixed.

Once the script executes cleanly, without any errors, the next step is to examine the output. Ask yourself, <em>Is this the output I expected?</em>. Remember, the script is under your direction and will only execute what you program. If the output is correct and what you intended, then you are finished. If the script gives unacceptable output, then the script needs to be edited and executed until the desired output is printed out. Good Luck!

<h2>Flowchart Toolbox</h2>

Design and create your flowcharts using the following suggested design objects. Using consistent design objects will make the flowchart easier to understand, easier to discuss, and easier to code. Each action, decision structure, loop structure, array, and variable can be specifically coded in Perl or Python. An example flowchart is shown on the last page in Figure (2).

<strong>Code Action </strong>Use boxes to indicate a code action. Specify the action with a verb, such as <strong>Initialize</strong>, <strong>Read</strong>, <strong>Increment</strong>, <strong>Assign</strong>, <strong>Calculate</strong>, <strong>Input</strong>, <strong>Output</strong>. If the code action includes a mathematical operation, then show the math. Specify the types of data <em>inputs </em>and data <em>outputs</em>.

<strong>Decision Structure </strong>A decision structure poses a mathematical question. Use diamonds to indicate decision structures. Use operators such as, <em>less than </em>(<em>&lt;</em>), <em>greater than </em>(<em>&gt;</em>), <em>equivalence </em>(==), <em>not equal </em>(! =), <em>AND</em>, <em>OR</em>, etc., to indicate the question. A decision structure defines two paths, a <em>true </em>path and a <em>false </em>path. Use <strong>TRUE </strong>and <strong>FALSE </strong>to identify the appropriate path. Each path should eventually lead back to the main line of the code.

<strong>Loop Structure </strong>Use long arrows to represent loop structures. A loop structure performs the same sequence of actions for different variables. Loops should include a decision structure that indicates when the loop should continue or stop.

<strong>Variables </strong>Within the code environment, data are accessible via variables. It is often helpful to define known variables and to initialize them. These variables can then be used to make the flowchart more accurate and readable.

<strong>Array </strong>An array is a special variable that indicates a sequential arrangement of values. A numerical series of: <em>0, 1, 2 . . . . . N </em>can be used to indicate an array. An array value is accessed via an <em>index</em>. Be sure to indicate the data being stored and the total number of elements in the array. The exact total may not be known, this value can be a variable, such as <em>N </em>in this example.

<h1>Problem 1</h1>

We return to the volume problem. Using a Perl or Python script, we want to find the volume of a prism, given its three dimensions (width, depth, height). Given that the three dimensions of the prism are 3002m × 2456m × 1901m, calculate the volume of the prism in cubic meters and in cubic kilometers. Use the following steps:

<ul>

 <li><strong>Develop </strong>a flowchart for this problem, using the <em>flowchart toolbox </em> Your flowchart needs to show: what are the inputs, what are the outputs, what are the procedures. Be as specific as possible and use the <em>tools </em>described in the <em>toolbox</em>!</li>

 <li><strong>Discuss </strong>the syntax needed to create a script based on your flowchart design (as a group). The steps in your flowchart should suggest the layout of your script.</li>

 <li><strong>Create </strong>a script using a text editor (<em>g. </em>gedit, on linux systems) and execute (<em>i.e. </em>run) it.</li>

 <li><strong>Turn in </strong>the problem you are trying to solve, your flowchart for solving this problem, the script developed from your flowchart, the command line you used to run your script, and the output from your script. Your code should output a complete sentence or mathematical phrase. The output should clearly show the solution to the problem. <em>Units are important! </em>Don’t forget to list them.</li>

</ul>

<h1>Problem 2</h1>

Suppose this volume estimate is for the amount of tephra (volcanic ash) erupted from a volcano. Given that the density of the tephra is 1000kgm<sup>−3</sup>. What is the volume of magma (density = 2650kgm<sup>−3</sup>) that erupted to form this tephra? What is the total mass of magma erupted? Use the same steps as before:

<ul>

 <li><strong>Develop </strong>a flowchart for this problem, using the <em>flowchart toolbox </em> Your flowchart needs to show the inputs and the outputs, what are the procedures. Be as specific as possible and use the <em>tools </em>described in the <em>toolbox</em>!</li>

 <li><strong>Discuss </strong>the syntax needed to create a script based on your flowchart design (as a group). The steps in your flowchart should suggest the layout of your script.</li>

 <li><strong>Create </strong>a script using a text editor (<em>g. </em>gedit, on linux systems) and execute (<em>i.e. </em>run) it.</li>

 <li><strong>Turn in </strong>the problem you are trying to solve, your flowchart for solving this problem, the script developed from your flowchart, the command line you used to run your perl script, and the output from your script. Your code should output a complete sentence or mathematical phrase. The output should clearly show the solution to the problem. <em>Units are important! </em>Don’t forget to list them.</li>

</ul>

Figure 1: Flow chart for creating and running a Perl or Python script.

<h1>Problem 3</h1>

Next we return to the integration problem. Suppose there are ten prisms of equal width and depth, but these prisms vary in height. For each prism the width = depth = 90m. The set, or array, of heights is 234.3, 233.5, 220.5, 200.5, 210.7, 222.3, 245.6, 254.5 270.6, 289.9 meters. What is the cumulative volume of the the prisms? If the heights correspond to elevation above sea level, and the rock is granite (density = 2670kgm<sup>−3</sup>), what is the mass of rock above sea-level, represented by the prisms? Follow the same steps listed for Problem 1 and Problem 2.

Figure 2: Example flowchart