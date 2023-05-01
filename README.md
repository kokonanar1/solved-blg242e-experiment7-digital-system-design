Download Link: https://assignmentchef.com/product/solved-blg242e-experiment7-digital-system-design
<br>
In this experiment, you will implement a single cycle CPU with Verilog HDL. Please read the introduction slide again carefully.

<strong>You can use any operator/code block in this experiment. You must simulate all parts and modules.</strong>

<h1>2      Part 1: Register Line and Decoder</h1>

In this part you will design:

<ul>

 <li>4:16 decoder module with enable input. If enable signal is logical low, all the outputs of decoder will be logical low.</li>

 <li>16-bit register line module. This module should take <strong>lineselect</strong>, <strong>clock</strong>, <strong>reset</strong>, and <strong>16-bit dataIn </strong>as input and give 16-bit <strong>stored data </strong>as output. At the falling edge of the reset signal data will be cleared. At the rising edge of the <strong>clock </strong>signal, the module should store the data which is given as input when the <strong>lineselect </strong>is high.</li>

</ul>

<h1>3      Part 2: Register File Design</h1>

In this part you should implement a 16 line 16-bit register file module (32 byte) using 4:16 decoder module and 16-bit register line module. This module should take 4-bit <strong>selA</strong>, 4-bit <strong>selB</strong>, 4-bit <strong>selWrite</strong>, 16-bit <strong>dataIn</strong>, <strong>reset</strong>, <strong>writeEnable</strong>, and <strong>clock </strong>as input and give 16-bit <strong>dataA </strong>and 16-bit <strong>dataB</strong>. The operations of the register file module are given below.

<ul>

 <li>At the falling edge of the <strong>reset</strong>, all lines of the register file will be cleared.</li>

 <li><strong>selWrite </strong>input selects the line to be updated. The selected line should store the <strong>dataIn </strong>input at the rising edge of the <strong>clock </strong>when the <strong>writeEnable </strong>is high.</li>

</ul>

Table 1: ALU Instructions

<table width="480">

 <tbody>

  <tr>

   <td width="88"><strong>OPCODE</strong></td>

   <td width="138"><strong>Operation Name</strong></td>

   <td width="146"><strong>Operation</strong></td>

   <td width="108"><strong>Update Flag</strong></td>

  </tr>

  <tr>

   <td width="88">1</td>

   <td width="138"> </td>

   <td width="146">|</td>

   <td width="108"> </td>

  </tr>

  <tr>

   <td width="88">5</td>

   <td width="138"> </td>

   <td width="146"><em>&gt;&gt;</em></td>

   <td width="108"> </td>

  </tr>

  <tr>

   <td width="88">6</td>

   <td width="138"> </td>

   <td width="146"><em>&lt;&lt;</em></td>

   <td width="108"> </td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Register outputs are exported via <strong>dataA </strong>and <strong>dataB</strong>. <strong>selA </strong>selects the line of the register file for <strong>dataA </strong> Similarly, <strong>selB </strong>selects the line of the registerfile for <strong>dataB </strong>output. These two operations do not require the clock signal.</li>

</ul>

<h1>4      Part 3: ALU Design</h1>

In this part you will design an Arithmetic Logic Units (ALU) that does some operations in the Table 1. In addition to these operations, the ALU will produce zero flag. Meaning that, if the result of the operation is zero, a special flip-flop (called <strong>zeroFlag</strong>) will be set to logical high. The inputs of the ALU will be called <strong>srcA</strong>, <strong>srcB</strong>. The output will be called <strong>dst</strong>. The ALU will decide its operations with the help of 3-bit <strong>Op </strong>input. Also, the module has <strong>clock </strong>and <strong>reset </strong>inputs and <strong>zeroFlag </strong>output. At the falling edge of the <strong>reset </strong>zeroFlag will be cleared. At the rising edge of the <strong>clock </strong>zeroFlag will be updated according to output of the ALU when the operation updates the flags. For example, AND operation does not update the flag.

<h1>5      Part 4: Instruction Decoder</h1>

In this part, you will create the control signals of your digital system according to <strong>instruction </strong>input. Table 2 shows the instruction set of the digital system. According to instruction set there are 4 type of instruction in this system. Table 3, 4, 5, and 6 shows the instructions bits separation for register, immediate, load, and branch respectively. Inputs and outputs ports information are given below.

<ul>

 <li><strong>instruction </strong>(15-bit Input): comes from the ROM and takes the current instruction as input.</li>

 <li><strong>opcode </strong>(4-bit Ouput): contains the operation information of the instruction.</li>

 <li><strong>selWrite </strong>(4-bit Ouput): contains the destination register address for writing operation.</li>

</ul>

Table 2: Digital System Instruction Set

<table width="661">

 <tbody>

  <tr>

   <td width="88"><strong>OPCODE</strong></td>

   <td width="138"><strong>Operation Name</strong></td>

   <td width="244"><strong>Operation</strong></td>

   <td width="83"><strong>Type</strong></td>

   <td width="108"><strong>Update Flag</strong></td>

  </tr>

  <tr>

   <td width="88">1</td>

   <td width="138"> </td>

   <td width="244">|</td>

   <td width="83"> </td>

   <td width="108"> </td>

  </tr>

  <tr>

   <td width="88">5</td>

   <td width="138"> </td>

   <td width="244"><em>&gt;&gt;</em></td>

   <td width="83"> </td>

   <td width="108"> </td>

  </tr>

  <tr>

   <td width="88">6</td>

   <td width="138"> </td>

   <td width="244"><em>&lt;&lt;</em></td>

   <td width="83"> </td>

   <td width="108"> </td>

  </tr>

  <tr>

   <td width="88">9</td>

   <td width="138">ORI</td>

   <td width="244">dst = srcA | Immediate</td>

   <td width="83">Immediate</td>

   <td width="108">No</td>

  </tr>

  <tr>

   <td width="88">10</td>

   <td width="138">ADD Immediate</td>

   <td width="244">dst = srcA + Immediate</td>

   <td width="83">Immediate</td>

   <td width="108">Yes</td>

  </tr>

  <tr>

   <td width="88">11</td>

   <td width="138">Compare</td>

   <td width="244">Compare srcA, srcB</td>

   <td width="83">Register</td>

   <td width="108">Yes</td>

  </tr>

  <tr>

   <td width="88">12</td>

   <td width="138">NOOP</td>

   <td width="244">–</td>

   <td width="83">–</td>

   <td width="108">No</td>

  </tr>

  <tr>

   <td width="88">13</td>

   <td width="138">B</td>

   <td width="244">PC = Immediate</td>

   <td width="83">Branch</td>

   <td width="108">No</td>

  </tr>

  <tr>

   <td width="88">14</td>

   <td width="138">BNE</td>

   <td width="244">PC = PC + Immediate if not equal</td>

   <td width="83">Branch</td>

   <td width="108">No</td>

  </tr>

  <tr>

   <td width="88">15</td>

   <td width="138">BEQ</td>

   <td width="244">PC = PC + Immediate if equal</td>

   <td width="83">Branch</td>

   <td width="108">No</td>

  </tr>

 </tbody>

</table>

<ul>

 <li><strong>selA </strong>(4-bit Ouput): contains the first operand address information of the instruction in the registerFile.</li>

 <li><strong>selB </strong>(4-bit Ouput): contains the second operand address information of the instruction in the registerFile.</li>

 <li><strong>fourBitImmediate </strong>(16-bit Ouput): contains the 4-bit immediate value information for immediate instructions. Zero extension will be used to extend 4-bit to</li>

</ul>

16-bit.

<ul>

 <li><strong>eightBitImmediate </strong>(16-bit Ouput): contains the 8-bit immediate value information for load and branch instructions. Zero extension will be used to extend 4-bit to 16-bit.</li>

 <li><strong>writeEnable </strong>(1-bit Ouput): If the instruction needs to write the results to register file, it must be 1. Otherwise, it will be 0.</li>

 <li><strong>isLoad </strong>(1-bit Ouput): The flag will 1 if the instruction is the load instruction.</li>

 <li><strong>isImmediate </strong>(1-bit Ouput): The flag will 1 if the instruction is the immediate instruction.</li>

 <li><strong>isBranch </strong>(1-bit Ouput): The flag will 1 if the instruction is the branch instruction (Opcode 13).</li>

</ul>

Table 3: Register Type Instructions

<table width="202">

 <tbody>

  <tr>

   <td width="64">Opcode</td>

   <td width="46">dst</td>

   <td width="46">srcA</td>

   <td width="46">srcB</td>

  </tr>

  <tr>

   <td width="64">4-bit</td>

   <td width="46">4-bit</td>

   <td width="46">4-bit</td>

   <td width="46">4-bit</td>

  </tr>

 </tbody>

</table>

Table 4: Immediate Type Instructions

<table width="240">

 <tbody>

  <tr>

   <td width="64">Opcode</td>

   <td width="46">dst</td>

   <td width="46">srcA</td>

   <td width="83">Immediate</td>

  </tr>

  <tr>

   <td width="64">4-bit</td>

   <td width="46">4-bit</td>

   <td width="46">4-bit</td>

   <td width="83">4-bit</td>

  </tr>

 </tbody>

</table>

<ul>

 <li><strong>isBranchNotEqual </strong>(1-bit Ouput): The flag will be 1 if the instruction is the branchNotEqual instruction.</li>

 <li><strong>isBranchEqual </strong>(1-bit Ouput): The flag will be 1 if the instruction is the branchEqual instruction.</li>

</ul>

<h1>6      Part 5: Program Counter</h1>

In this part, program counter module will develop the program counter module for the digital design. The output of the program counter module (<strong>PC</strong>) stores the current program address of the system. The inputs of the module are <strong>reset</strong>, <strong>clock</strong>, <strong>isBranch</strong>, <strong>isBranchNotEqual</strong>, <strong>isBranchEqual</strong>, and <strong>immediateAddress (8-bit)</strong>. The instruction fetched from the program memory using this information. <strong>PC </strong>will be cleared at the falling edge of the reset signal. If the operation is branch (Opcode 13), <strong>PC </strong>value will be the <strong>immediateAddress </strong>(8-bit input) at the rising edge of the clock. PC value will be the <strong>immediateAddress </strong>(8-bit input) at the rising edge of the clock. PC value will be current <strong>PC </strong>value + <strong>immediateAddress </strong>at the rising edge of the clock if the operation is branch not equal and flag shows the result is not equal, or the operation is branch equal and flag shows the result is equal.You can access the result information using zeroFlag. Otherwise, PC value will be next address of the memory at the rising edge of the clock.

<h1>7      Part 6: Mini Computer</h1>

In this part, you will implement the mini computer using the modules you implemented in the previous parts. The module only needs <strong>clock </strong>and <strong>reset </strong>signals. Clock and reset signal will be connected to other modules which needs the this signals. You must give

Table 5: Load Type Instructions

<table width="194">

 <tbody>

  <tr>

   <td width="64">Opcode</td>

   <td width="46">dst</td>

   <td width="83">Immediate</td>

  </tr>

  <tr>

   <td width="64">4-bit</td>

   <td width="46">4-bit</td>

   <td width="83">8-bit</td>

  </tr>

 </tbody>

</table>

Table 6: Branch Type Instructions

<table width="211">

 <tbody>

  <tr>

   <td width="64">Opcode</td>

   <td width="63">Unused</td>

   <td width="83">Immediate</td>

  </tr>

  <tr>

   <td width="64">4-bit</td>

   <td width="63">4-bit</td>

   <td width="83">8-bit</td>

  </tr>

 </tbody>

</table>

<strong>instruction</strong>, <strong>dataA</strong>, <strong>dataB</strong>, <strong>dst</strong>, <strong>PC</strong>, <strong>input value of ALU srcB </strong>for debugging and test of the system. You will also needs the ROM module, but we have already developed it for you. You can directly add this module to your design files. You must also include the memory data to your project, the guideline have been added to homework files for this operation. The input connection information of the modules are given below.

<ul>

 <li>Program Memory

  <ul>

   <li>PC <em>&lt;</em>– PC output of the Program Counter</li>

  </ul></li>

 <li>Instruction Decoder

  <ul>

   <li>instruction <em>&lt;</em>– instruction output of the Program Memory</li>

  </ul></li>

 <li>Register File

  <ul>

   <li>selA <em>&lt;</em>– selA output of the Instruction Decoder</li>

   <li>selB <em>&lt;</em>– selB output of the Instruction Decoder</li>

   <li>selWrite <em>&lt;</em>– selWrite output of the Instruction Decoder</li>

   <li>dataIn <em>&lt;</em>– dst output of the ALU</li>

   <li>writeEnable <em>&lt;</em>– writeEnable output of the Instruction Decoder</li>

  </ul></li>

 <li>ALU

  <ul>

   <li>srcA <em>&lt;</em>– dataA output of the Register File</li>

   <li>srcB <em>&lt;</em>– It can be dataB, 4-bit immediate or 8-bit immediate according to instruction type. You must select it for each type of instruction.</li>

   <li>Op <em>&lt;</em>– Opcode output of the Instruction Decoder</li>

  </ul></li>

 <li>Program Counter

  <ul>

   <li>zeroFlag <em>&lt;</em>– zeroFlag output of the ALU</li>

   <li>isBranch <em>&lt;</em>– isBranch output of the Instruction Decoder</li>

   <li>isBranchNotEqual <em>&lt;</em>– isBranchNotEqual output of the Instruction Decoder</li>

   <li>isBranchEqual <em>&lt;</em>– isBranchEqual output of the Instruction Decoder</li>

   <li>immediateAddress <em>&lt;</em>– One of the immediate value output of the Instruction Decoder.</li>

  </ul></li>

</ul>