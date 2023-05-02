Download Link: https://assignmentchef.com/product/solved-cpe431-homework-5
<br>
<strong>1.0          &lt;4.7&gt; </strong>This exercise is intended to help you understand the cost/complexity/performance tradeoffs of forwarding in a pipelined processor. Problems in this exercise refer to pipelined datapaths from Figure 4.45. Thse problems assume that, of all the instructions executed in a processor, the following fraction ofthese instructions have a particular type of RAW data dependence. The type of RAW data dependence is identifies by the stage that produces the result (EX or MEM) and the instruction that consumes the result (1<sup>st</sup> instruction that follows the one that produces the result, 2<sup>nd</sup> instruction that follows, or both). We assume that the register write is done in the first half of the clock cycle and that register reads are done in the second half of the cycle so “EX to 3<sup>rd</sup>” and “MEM to 3<sup>rd</sup>” dependences are not counted because they cannot result in data hazards. Also, assume that the CPI  of the processor is 1 if there are no data hazards.

<strong> </strong>

<table width="575">

 <tbody>

  <tr>

   <td width="93">EX to 1<sup>st</sup> Only</td>

   <td width="96">Memto 1<sup>st</sup> Only</td>

   <td width="93">EX to 2<sup>nd</sup> Only</td>

   <td width="96">MEMto 2<sup>nd</sup> Only</td>

   <td width="94">EX to 1<sup>st</sup> and MEM to 2<sup>nd</sup></td>

   <td width="103">Other RAW dependences</td>

  </tr>

  <tr>

   <td width="93">5%</td>

   <td width="96">20%</td>

   <td width="93">5%</td>

   <td width="96">10%</td>

   <td width="94">10%</td>

   <td width="103">10%</td>

  </tr>

 </tbody>

</table>

<strong> </strong>




EX to 1<sup>st</sup> only example MEM to 2<sup>nd</sup> only example   add   $t0, $t1, $t2   lw    $t0, 20($t1)   add   $t3, $t0, $t4   add   $t3, $t5, $t4  MEM to 1<sup>st</sup> only example   add   $t6, $t0, $s0   lw    $t0, 20($t1)  EX to 1<sup>st</sup> and MEM to 2<sup>nd</sup> example

add   $t3, $t0, $t4   lw    $t4, 24($t0)  EX to 2<sup>nd</sup> only example   add   $t9, $s0, $s4   add   $t0, $t1, $t2   add   $s1, $t4, $t9   add   $t3, $t5, $t4  Other RAW Dependence example

add   $t6, $t0, $s0                        add   $t0, $t1, $t2                       add   $s0, $t3, $s0     addi  $s1, $s1, 4

add   $t3, $t0, $t4

<strong>1.0.1      </strong>If we use no forwarding, what fraction of cycles are we stalling due to data hazards?




<strong>1.0.2      </strong>If we use full forwarding (forward all results that can be forwarded), what fraction of cycles are we stalling due to data hazards?

<strong> </strong>

<strong>2.0          &lt;4.8&gt; </strong>This exercise is intended to help you understand the relationship between delay slots, control hazards, and branch exectution in a pipelined processor. In this exercise, we assume that the following MIPS code is executed on a pipelined processor with a 5-stage pipeline, full forwarding, and a predict-taken branch predictor:

lw    r2, 0(r1)      label1:  beq   r2, r0, label2     # not taken once, then taken                 lw    r3, 0(r2)               beq   r3, r0, label1     #taken           add   r1, r3, r1     label2:  sw    r1, 0(r2)

Page 1 of 2




CPE 431/531                                                                     Homework #5                                                                           Fall 2020

<strong>2.0.1      </strong>Draw the pipeline execution diagram for this code, assuming there are no delay slots and that branches execute in the EX stage.

<strong> </strong>

<strong>2.0.2      </strong>For the given code, what is the speedup achieved by moving branch execution into the ID stage? Explain your answer. In your speedup calculations, assume that the additional comparison in the ID stage does not affect clock cycle time.

<strong> </strong>

<strong>2.0.3      </strong>Using the first branch instruction in the given code as an example, describe the forwarding support that must be added to support branch execution in the ID stage. Compare the complexityof this new forwarding unit to the complexity of the existing forwarding unit in Figure 4.62.

<strong> </strong>

<strong>3.0 </strong>         <strong>&lt;4.8&gt;</strong> The importance of having a good branch predictor depends on how often conditional branches are executed. Together with branch predictor accuracy, this will determine how much time is spent stalling due to mispredicted branches. In this exercise, assume that the breakdown of dynamic instructions into various instruction categories is as follows:




<table width="413">

 <tbody>

  <tr>

   <td width="86">R-type</td>

   <td width="86">BEQ</td>

   <td width="77">JMP</td>

   <td width="77">LW</td>

   <td width="86">SW</td>

  </tr>

  <tr>

   <td width="86">40%</td>

   <td width="86">25%</td>

   <td width="77">5%</td>

   <td width="77">25%</td>

   <td width="86">5%</td>

  </tr>

 </tbody>

</table>

Also, assume the following branch predictor accuracies:

<table width="336">

 <tbody>

  <tr>

   <td width="115">Always-Taken</td>

   <td width="134">Always-Not-Taken</td>

   <td width="86">2-Bit</td>

  </tr>

  <tr>

   <td width="115">45%</td>

   <td width="134">55%</td>

   <td width="86">85%</td>

  </tr>

 </tbody>

</table>




<strong>3.0.1</strong>      Stall cycles due to mispredicted branches increase the CPI. What is the extra CPI due to mispredicted branches with the always-taken predictor? Assume that branch outcomes are determined in the EX stage, that there are no data hazards, and that no delay slots are used.

<strong> </strong>

<strong>3.0.1      </strong>With the 2-bit predictor, what speedup would be achieved if we could convert half of the branch instructions in a way that replaces a branch instruction with an ALU instruction? Assume that correctly and incorrectly predicted instructions have the same chance of being replaced.

<strong> </strong>

<strong>4.0</strong>          &lt;4.10&gt; In this exercise, we consider the execution of a loop in a statically scheduled superscalar processor that has full forwarding. To simplify the exercise, assume that any combination of instruction types can execute in the same cycle, e.g., in a 3-issue superscalar, the three instructions can be three ALU operations, three branches, three load/store instruction, or any combination of these instructions. Note that this only removes a resource constraint, but data and control dependences must be still be handled correctly. Problems in this exercise refer to the following loop:<strong>  </strong>

<strong>Loop:  lw   $t0, 0($s1)        lw   $t4, 0($s2)        mul  $t0, $t0, $t4        add  $t0, $t3, $t0        addi $s1, $s1, -8        addi $s2, $s2, -8        bne  $s1, $zero, Loop </strong>

Unroll this loop so that four iterations of it are done at once and schedule it for a 2-issue static superscalar processor. Assume that the loop always executes a number of iterations that is a multiple of 4. You can use any unused registers when changing the code to eliminate dependences.<strong>  </strong>

Page 2 of 2


