Download Link: https://assignmentchef.com/product/solved-cecs-341-introduction-to-xilinx-vivado-ip-integrator
<br>
<h1>Introduction</h1>

In this course, you will be using a block design to describe how the processor components connect to each other. For this purpose, you should be familiar with Vivado’s IP Integrator feature. The IP Integrator assists the users to understand how to achieve greater design productivity by rapidly creating and reusing subsystem level IP with Vivado and IP Integrator. As a result, tasks that you need to learn are:

<ul>

 <li>Creating a block design and adding IPs.</li>

 <li>Create a VHDL module and add it to the block design.</li>

 <li>Extract a subset of bus bits using the Slice IP.</li>

 <li>Concatenate signals using the Concat IP.</li>

 <li>Set signals to a specific constant using the Constant IP. ➢ Create HDL wrapper for your design.</li>

 <li>Instantiate your wrapper in test-bench and simulate it.</li>

</ul>

This lab simply begins with a 1-bit full adder (described in VHDL) and uses this block to construct a 2-bit adder using Vivado IP Integrator. The numbers to be added are A and B (each 2-bit unsigned integers) and the result (sum) is a three-bit unsigned integer.

<h1>Lab Objective</h1>

The objective of this lab is to create a 2-bit adder from a 1-bit full adder. This process should familiarize students with the IP Integrator tool to be used in next lab projects.

<h1>Design Entry and Simulation Steps</h1>

<ul>

 <li>In Vivado, create a new project (File → New Project … ). Select a location and name the project <em>lab1</em>. Click Next in the Add Sources and Add Constrains pages. These can be added later.</li>

 <li>Add a new VHDL source to your project. In the Sources window, Click the Add Sources button → Add or create design source → Create File. Name the file <em>FA → Finish</em>.</li>

</ul>

Replace the content of the file you created with the full adder code from Beachboard. The file name will be FA.vhd. Make sure to save the file.

<ul>

 <li>Now create a block design using the IP Integrator tool as shown below. Name the block design a<em>dder_2bit</em>.</li>

</ul>










<ul>

 <li>Add two instances of the full adder to the block design. In the Sources window, right-click on the source file FA.vhd and click “Add Module to Block Design”.</li>

</ul>







<ul>

 <li>Now add ports for input and output. These will serve as ports for the block design. Right-click on the block design background and click “Create Port…”. In this lab, we need two input ports.</li>

</ul>

A: a 2-bit data input

B: a 2-bit data input We need one output port:

Sum: a 3-bit data output.

Here is an example for setting up port A.







Follow this example to create all ports needed.

<ul>

 <li>Add 4 slice IP’s (in the Diagram window, click Add IP). The Slice IP can be used to extract a subset of bits from a bus. For example, we need to get bit0 and bit1 separately from port A which is a two-bit input.</li>

</ul>

To customize the IP, double-click on it. Now, set the following parameters:

Din Width==&gt; The size of the bus to be split. In this case the bus is 2 bits wide.

Din from ==&gt; Subset starts from this value.

Din Down To =&gt; Subset ends at this value.

The following figures show how to extract bit 0 from the 2-bit input.




Follow the previous example to extract individual bits from input A and B. Use one slice IP for each bit. The bits will be connected to the adder as follows.

A(0) →port A in FA_0

A(1) → port A in FA_1

B(0) →port B in FA_0

B(1) → port B in FA_1

<ul>

 <li>Use a Constant IP to provide the Cin for FA_0. The value of the constant should be zero. To customize the IP, double-click on it. Then set the <em>Const Width </em>and <em>Const Value</em>. In this case, they will be 1 and 0 respectively.</li>

 <li>Use a Concat IP to concatenate the S output from the two full-adder along with the Cout from FA_1. The Concat IP, combines signals into a wider signal. Customize the IP to increase its number of ports to 3. Also connect the cout output of FA_0 to Cin in FA_1. Your 2-bit adder should look as follows:</li>

</ul>







<ul>

 <li>Now we are ready to create a wrapper for the block design. Right-click on the block design in the Sources window (the yellow icon) and select “Generate HDL Wrapper” and also click on “Generate Output Products” accept the default options. Notice that an HDL wrapper is created and listed in the Sources window.</li>

 <li>Download the test-bench from BeachBoard (adder_tb.vhd). Create a test-bench source and replace its content with the code in the file you downloaded. Make sure that you understand how the wrapper is instantiated in the test-bench.</li>

 <li>Now run the behavioral simulation by clicking on “Run Simulation” in the Flow Navigator section and observe the waveform result.</li>

</ul>




<strong> </strong>


