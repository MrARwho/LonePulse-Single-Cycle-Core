LonePulse-Single-Cycle-Core 
=======================
<img src='https://github.com/syedowaisalishah/Al-Battar-/blob/main/Single%20Cycle%20RISC-V%20Core.png' height=600 width=100%>

[![Join the chat at https://gitter.im/merledu/scala-chisel-learning-journey](https://badges.gitter.im/merledu/scala-chisel-learning-journey.svg)](https://gitter.im/merledu/scala-chisel-learning-journey?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


Start by setting up the working enviroment

### Dependencies

#### JDK 8 or newer

```bash
sudo apt-get install openjdk-11-jdk
sudo apt-get install openjdk-11-jre
```
#### SBT 

SBT is the most common built tool in the Scala community. You can download it [here](https://www.scala-sbt.org/download.html).  

#### VERILATOR
```bash
sudo apt-get install verilator
```

### For quick debugging
If you quickly want to see what verilog is being generated, go to this link  https://bit.ly/3u3zr0e and write Chisel here.

First of all get started by cloning this repository on your machine.

```ruby
git clone https://github.com/MrARwho/LonePulse-Single-Cycle-Core.git-.git
```

Create a .txt file and place the ***hexadecimal*** code of your instructions simulated on ***Venus*** (RISC-V Simulator)\
Each instruction's hexadecimal code must be on seperate line as following. This program consists of 9 instructions.

```ruby
00500113
00500193
014000EF
00120293
00502023
00002303
00628663
00310233
00008067
```
Then perform the following step
```
cd LonePulse-Single-Cycle-Core/src/main/scala/gcd/Single_Cycle/SingleCycle
```
Open **InstMem.scala** with this command. You can also manually go into the above path and open the file in your favorite text editor.
```ruby
open insMem.scala
```
Find the following line
``` python
loadMemoryFromFile(insMem, ""/home/owais/LonePulse-Single-Cycle-Core/src/main/scala/gcd/Single_Cycle/Imem.txt"")
```
Change the .txt file path to match your file that you created above storing your own program instructions. or you can also use this file\
After setting up the InstructionMem.scala file, go inside the RV32i folder.
```ruby
cd Single-Cycle-CPU/RV32i
```

And enter
```ruby
sbt
```
When the terminal changes to this type
```ruby
sbt:LonePulse-Single-Cycle-Core>
```
Enter this command
```ruby
sbt:LonePulse-Single-Cycle-Core> testOnly Single_Cycle.DataPathTester -- -DwriteVcd=1
```
### For quick debugging
If you quickly want to see what verilog is being generated, go to this link  https://bit.ly/3u3zr0e and write Chisel here.

### Test cases 

#### Program 1
```
addi x5 x0 0
addi x6 x0 5
add x8 x6 x5
LOOP:
addi x5 x5 1
sw x5 100(x0)
beq x5 x6 ANS
jal LOOP
ANS: lw x7 100(x0)

```
#### Program 2
```
addi x5 x0 3
LOOP:
addi x5 x5 1
addi x6 x0 7
sw x6 100(x5)
lw x7 100(x5)
bne x5 x7 LOOP

```
#### Program 3
```
addi x5 x0 0
addi x7 x0 1
addi x6 x0 10
addi x28 x0 0
LOOP: beq x28 x6 END
add x29 x5 x7
add x5 x0 x7
add x7 x0 x29
jal LOOP
END:
```
#### Fibonacci Series:
```
addi x1,x0,0
addi x2,x0,1
addi x10,x0,4
addi x6,x0,40
addi x3,x0,0
addi x4,x3,4
sw x1,0x100(x3)
sw x2,0x100(x4)
addi x14,x0,8
addi x5,x0,8
addi x13,x0,8
addi x15,x0,4
addi x9,x0,4
add x8,x1,x2
up:
beq x5,x6,end
add x12,x0,x8
sw x12,0x100(x5)
lw x11,0x100(x9)
add x8,x11,x8
addi x5,x5,4
addi x9,x9,4
jal x7,up
end:
beq x3,x6,break
lw x16,0x100(x3)
addi x3,x3,4
jal x7,end
break:
```

