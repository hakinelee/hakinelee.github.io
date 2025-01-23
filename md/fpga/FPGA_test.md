> 可编程器件与硬件描述语言（Verilog HDL）实验报告，基于Altera DE2-115 教育开发板
>
> ![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737563686096-dfaab638-bd08-4df9-94d6-e517bee6851f.jpeg)
>

## 实验一、选择器
### 一、实验目的
1. 了解4选1的工作原理和实现的方法；
2. 实现4选1多路选择器；
3. 学会用于Verilog语言进行程序设计。

### 二、实验原理
4选1多路选择器的电路模型或元件图如图1-1所示，图中，a、b、c、d是四个输入端口；s1和s0为通道选择控制信号端，y为输出端；当s1和s0取值分别为00、01、10和11时，输出端y将分别输出来自输入口a、b、c、d的数据。4选1对应的功能真值表如图1-2所示。

| ![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559748805-55eee453-9750-4343-80b3-d8ccdc7b2e29.png) | ![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559748959-4aa28c75-615b-4b0c-b5ec-aa61f92c7b4e.png) |
| :---: | :---: |
| 图1-1  4选1多路选择器 | 图1-2  真值表 |


### 三、实验任务
1. 完成4选1多路选择器的的Verilog程序编写并进行编译；
2. 对设计的电路进行仿真验证；
3. 编程下载并在实验开发系统上验证设计结果。

### 四、实验结果与分析
**Verilog程序：**

```verilog
module mux41a (a, b, c, d, s1, s0, y);
	input a, b, c, d;
	input s1, s0;
	output reg y;
	reg [1:0] sel;
	always@ (a, b, c, d, sel) begin 
		sel = {s1,s0};
		if (sel == 0) 
			y = a;
		else if(sel == 1)
			y = b;
		else if(sel == 2)
			y = c;
		else 
			y = d;
	end
endmodule
```

**波形仿真**：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559749095-db596d7b-b14c-4506-9482-c4592685801b.png)

**硬件测试：**

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559749325-d0d659d6-7478-470d-b821-49febedff570.png)

**实验结果分析：**

代码编译通过。通过拨动开关成功点亮LED实现4选1多路选择器。

### 五、实验心得
       通过设计4选1多路选择器，我们深入理解了组合电路设计的过程，并熟练掌握了这一过程。通过这次实验，我接触到了EDA的相关知识，并学会了使用Quartus软件。要成功完成这个实验，需要对数字电子知识有扎实的掌握，并能够将书本知识灵活运用到实际设计中。这个实验不仅锻炼了我们的动手和动脑能力，还激发了我们的思维。我意识到，我目前所掌握的知识还有很大的提升空间。在未来的学习和生活中，我将继续努力深化我的知识储备。

---

## 实验二、加法器
### 一、实验目的
1. 掌握Quartus Ⅱ的程序设计流程；
2. 掌握用原理图输入法实现项目的层次化设计过程；
3. 掌握半加器、全加器的程序设计。

### 二、实验原理
一个一位全加器可以用两个一位半加器和一个或门连接而成。而一个一位半加器可由基本门电路组成。

1. 半加器设计原理：只考虑两个一位二进制数的相加，而不考虑来自低位进位数的运算电路，称为半加器。其中：a、b分别为被加数与加数，作为电路的输入端；s0为两数相加产生的本位和，它和两数相加产生的向高位的进位c0一起作为电路的输出。
2. 全加器设计原理：除本位两个数相加之外，还要加上从低位来的进位数，称为全加器。其中：a为被加数，b为加数，c为低位向本位的进位，c0为本位向高位的进位，s0为本位和。

### 三、实验任务
1. 完成半加器以及全加器的Verilog程序编写并进行编译；
2. 对设计的电路进行仿真验证；
3. 编程下载并在实验开发系统上验证设计结果。

### 四、实验结果与分析
**Verilog程序：**

```verilog
module f_adder(ain, bin, cin, cout, sum);
  	output cout, sum;
  	input ain, bin, cin;
  	wire net1, net2, net3;
  
  	h_adder U1(ain, bin, net1, net2);
  	h_adder U2(.A(net1), .SO(sum), .B(cin), .CO(net3));
  	or1 U3(cout, net2, net3);
endmodule
```

```verilog
module h_adder(A, B, SO, CO);
  	input A, B;
  	output SO, CO;
  	assign SO = A ^ B;
  	assign CO = A & B;
endmodule
```

```verilog
module or1(z, x, y);
  	input x, y;
  	output z;
  	assign z = x | y;
endmodule
```

**波形仿真**：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559749562-a46edf93-a6c1-47ce-8471-9901dc368f25.png)

**硬件测试：**

![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737559749733-0cf81cc8-039e-4aa6-a8e7-bceb1939ec6f.jpeg)

**实验结果分析：**

代码编译通过。通过拨动开关成功点亮LED实现全加器。

其中使用SW0作为低位的进位，SW4~1 作为数据B，SW8~5作为数据A，LDG3~0作为输出的结果，LEDG4作为输出的进位。当SW4~1闭合SW8~5和SW0断开时，只有LEDG3~0这四个灯亮；当SW8~0全闭合时，LEDG4~0灯全亮。

### 五、实验心得
通过这次实验，我学会了使用元件例化语句。例化语句用于层次设计，即在当前设计中调用一个已经设计好的功能模块。同时，对于全加器程序的编写了更深的认识，这能更好的促进以后的学习。

---

## 实验三、D触发器
### 一、实验目的
1. 掌握时序逻辑电路的基本分析和设计方法；
2. 理解触发器的工作原理，用硬件描述语言实现触发器的门级设计。

### 二、实验原理
D触发器是一种常见的时序逻辑器件，其输出Q在时钟信号的上升沿或下降沿发生变化，取决于D输入端的状态。D触发器有两种基本类型：上升沿触发器和下降沿触发器。顾名思义，上升沿触发器在时钟信号的上升沿发生变化，而下降沿触发器在时钟信号的下降沿发生变化。

D触发器的基本原理图如下：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559749969-ac62db74-2d68-42e8-97fb-3d5e1201bf0c.png)

其中：

D：数据输入端，决定了触发器的输出状态。

Q：输出端，反映了触发器当前的状态。

CLK：时钟输入端，控制触发器的状态变化。

CE：时钟使能端，控制触发器是否响应时钟信号。

D触发器的真值表如下：

| D | CLK | CE | Q |
| :---: | :---: | :---: | :---: |
| 0 | 0 | X | Q |
| 0 | 1 | 1 | 0 |
| 1 | 0 | X | Q |
| 1 | 1 | 1 | 1 |


### 三、实验任务
1. 完成含异步复位和时钟使能的D触发器的Verilog程序编写并进行编译；
2. 对设计的电路进行仿真验证；
3. 编程下载并在实验开发系统上验证设计结果。

### 四、实验结果与分析
**Verilog程序：**

```verilog
module dff2(clk, d, q, rst, en);
  	input clk, d, rst, en;
  	output reg q;
  	always@ (posedge clk or negedge rst) begin
        if(!rst)
      			q <= 0;
    		else if(en)
      			q <= d;
  	end
endmodule
```

**波形仿真**：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559750112-5eba4d04-5930-4d3f-a1e6-57da224453df.png)

**硬件测试：**

![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737559750295-2d582316-27d3-42f4-88a7-21b637b81563.jpeg)

**实验结果分析：**

通过仿真，可以观察到D触发器的输出波形与真值表一致。当D输入端为0时，Q输出端保持不变；当D输入端为1时，Q输出端在时钟信号的上升沿或下降沿发生变化。

### 五、实验心得
通过本次实验，掌握了D触发器的基本原理和应用，能够使用EDA工具设计和仿真D触发器。

---

## 实验四、简易计数器
### 一、实验目的
1. 掌握基本时序逻辑电路的设计方法；
2. 学会十六进制加法计数器设计，为复杂时序逻辑电路的设计打基础。

### 二、实验原理
首先，我们需要了解16进制数的表示方法。在16进制数中，使用0-9和A-F来表示数值。其中，A代表10，B代表11，C代表12，D代表13，E代表14，F代表15。

然后，我们需要将二进制数转换为16进制数。转换的方法是将二进制数每4位一组，不足4位的在前面补0，然后将其转换为16进制数。例如，二进制数0001 0010 0001可以转换为121（16进制）。

### 三、实验任务
1. 完成16进制计数器的Verilog程序编写并进行编译； 
2. 编程下载并在实验开发系统上验证设计结果。

### 四、实验结果与分析
**Verilog程序：**

```verilog
module cnt11(input clkin, rst; output  clkout; output [3:0] dout; output reg [6:0] Dout7S);
    reg [27:0] c1;
    reg clk_1hz;
    reg [3:0] q1;
    assign dout = q1;
    always@ (posedge clkin or negedge rst) begin
        if(!rst)	
            c1 <= 0;
        else if(c1 == 4999_9999)	
            c1 <= 0;
        else	
            c1 <= c1 + 1;		
    end
    always@ (posedge clkin or negedge rst) begin
        if(!rst)	
            clk_1hz <= 1'b0;
        else if(c1 == 0)	
            clk_1hz <= 0;
        else if(c1 == 2500_0000)	
            clk_1hz <= 1;
        else	
            clk_1hz <= clk_1hz;	
    end
  	assign clkout=clk_1hz;
  	always@ (posedge clkout or negedge rst) begin
    		if(!rst)	
            q1 <= 0;
    		else if(q1 < 9) 
            q1 <= q1 + 1;
    		else	
            q1 <= 4'b0000; 
    		case(q1)
      			4'b0000: Dout7S <= 7'b1000_000;
      			4'b0001: Dout7S <= 7'b1111_001;
      			4'b0010: Dout7S <= 7'b0100_100;
      			4'b0011: Dout7S <= 7'b011_0000;
      			4'b0100: Dout7S <= 7'b001_1001;
      			4'b0101: Dout7S <= 7'b001_0010;
      			4'b0110: Dout7S <= 7'b000_0010;
      			4'b0111: Dout7S <= 7'b111_1000;
      			4'b1000: Dout7S <= 7'b000_0000;
      			4'b1001: Dout7S <= 7'b001_0000;
      			default: Dout7S <= 7'b1000_000;
    		endcase 
    end	
endmodule
```

**波形仿真**：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559750515-a616ab36-4156-4190-9caa-85b863d3c6e2.png)

**硬件测试：**

![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737559750786-4b1c1b91-22ff-4097-84f6-2387d42e9609.jpeg)

**实验结果分析：**

通过仿真，可以观察到16进制器的输出波形与预期结果一致。当输入端为不同的16进制数字时，输出端输出相应的4位二进制数。

### 五、实验心得
<font style="color:#3F4A54;">通过本次实验，掌握了16进制计数器的基本原理和应用，能够使用EDA工具设计和仿真16进制计数器。</font>

---

## 实验五、译码器
### 一、实验目的
1. 学会Verilog HDL的case语句应用；
2. 学会Verilog HDL的if语句应用。

### 二、实验原理
3-8译码器的三输入，八输出。输入信号N用二进制表示，对应的输出信号N输出高电平时表示有信号产生，而其他则为低电平表示无信号产生。其真值表如下所示：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559751034-dc9c242a-5439-40f2-9767-050250138628.png)

当使能端指示输入信号无效或不用对当前的信号进行译码时，输出端全为高电平，表示任何信号无效。

### 三、实验任务
1. 用Verilog HDL设计一个3-8译码器，要求分别用顺序赋值语句、case语句、if-else语句和移位操作符来完成；
2. 对设计的电路进行仿真验证；
3. 编程下载并在实验开发系统上验证设计结果。

### 四、实验结果与分析
**Verilog程序：**

```verilog
module Decoder_38(input a, b, c, output y0, y1, y2, y3, y4, y5, y6, y7);
    assign y0 = ~a & ~b & ~c;
    assign y1 = ~a & ~b &  c;
    assign y2 = ~a &  b & ~c;
    assign y3 = ~a &  b &  c;
    assign y4 = a & ~b & ~c;
    assign y5 = a & ~b &  c;
    assign y6 = a &  b & ~c;
    assign y7 = a &  b &  c;
endmodule
```

```verilog
module case38(input wire [2:0] a, output reg [7:0] out);
    always@ (a) begin
        if(a == 3'b000)
            out <= 8'b0000_0001;
        else if(a == 3'b001)
            out <= 8'b0000_0010;
        else if(a==3'b010)
            out <= 8'b0000_0100;
        else if(a == 3'b011)
            out <= 8'b0000_1000;
        else if(a == 3'b100) 
            out <= 8'b0001_0000;
        else if(a == 3'b101)
            out <= 8'b0010_0000;
        else if(a == 3'b110)
            out <= 8'b0100_0000;
        else
            out <= 8'b1000_0000;
    end
endmodule
```

```verilog
module case38(input a, b, c, output reg [7:0] out);
    reg [7:0] R = 8'b0000_0001;
    always@ (a, b, c) begin
        if({a, b, c} == 3'b000)
            out = R;
        else if({a,b,c} == 3'b001)
            out = (R<<1);
        else if({a,b,c} == 3'b010)
            out = (R<<2);
        else if({a,b,c} == 3'b011)
            out = (R<<3);
        else if({a,b,c} == 3'b100)
            out = (R<<4);
        else if({a,b,c} == 3'b101)
            out = (R<<5);
        else if({a,b,c} == 3'b110)
            out = (R<<6);
        else if({a,b,c} == 3'b111)
            out = (R<<7);
        else
            out = 8'b0000_0000;
    end
endmodule
```

**波形仿真**：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559751249-2326ae94-cdfe-40ac-ace4-068a1d7a42fb.png)

**硬件测试：**

![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737559751452-a035c347-7edc-4f46-91e3-5b77a361a357.jpeg)

**实验结果分析：**

代码编译通过。通过拨动开关成功点亮LED实现38译码器。

<font style="color:#3F4A54;">通过仿真，可以观察到38译码器的输出波形与预期结果一致。当输入端为不同的3位二进制数时，输出端输出相应的8种输出信号。</font>

### 五、实验心得
通过本次实验，掌握了38译码器的基本原理和应用，能够使用EDA工具设计和仿真38译码器。

---

## 实验六、乘法器
### 一、实验目的
1. 了解四位并行乘法器的原理。
2. 了解四位并行乘法器的设计思想。
3. 掌握用Verilog语言实现基本二进制运算的方法。

### 二、实验原理
假如有被乘数A 和乘数B，首先用A 与B 的最低位相乘得到S1，然后再把A 左移1 位与B 的第2 位相乘得到S2，再将A 左移3 位与B 的第三位相乘得到S3，依此类推，直到把B 的所有位都乘完为止，然后再把乘得的结果S1、S2、S3……相加即得到相乘的结果。

### 三、实验任务
1. 完成设计一个4*4移位相加型乘法器的Verilog程序编写并进行编译；
2. 对设计的电路进行仿真验证；
3. 编程下载并在实验开发系统上验证设计结果。

### 四、实验结果与分析
**Verilog程序：**

```verilog
module mult4b2(input [3:0] a, b, output reg [7:0] r, output reg[6:0] hex0, hex1, hex2, hex4, hex5, hex6, hex7);
    parameter s = 4;
    reg [7:0] at;    reg [4:1] ct;    reg [3:0] bt;
    always@ (a, b) begin
        r = 0;	at = {{s{1'b0}},a};  
        bt= b;  ct = s;
        for(ct=s; ct>0; ct=ct-1) begin
            if(bt[0])	  
                r = r + at;
            at = at<<1;	  bt = bt>>1;
      			case(a)
        				0: begin hex7 <= 7'b1000000; hex6 <= 7'b1000000;end
        				1: begin hex7 <= 7'b1000000; hex6 <= 7'b1111001;end
        				2: begin hex7 <= 7'b1000000; hex6 <= 7'b0100100;end
        				3: begin hex7 <= 7'b1000000; hex6 <= 7'b0110000;end
        				4: begin hex7 <= 7'b1000000; hex6 <= 7'b0011001;end
        				5: begin hex7 <= 7'b1000000; hex6 <= 7'b0010010;end
        				6: begin hex7 <= 7'b1000000; hex6 <= 7'b0000010;end
        				7: begin hex7 <= 7'b1000000; hex6 <= 7'b1111000;end
        				8: begin hex7 <= 7'b1000000; hex6 <= 7'b0000000;end
        				9: begin hex7 <= 7'b1000000; hex6 <= 7'b0010000;end
        				10:begin hex7 <= 7'b1111001; hex6 <= 7'b1000000;end
        				11:begin hex7 <= 7'b1111001; hex6 <= 7'b1111001;end
        				12:begin hex7 <= 7'b1111001; hex6 <= 7'b0100100;end
        				13:begin hex7 <= 7'b1111001; hex6 <= 7'b0110000;end
        				14:begin hex7 <= 7'b1111001; hex6 <= 7'b0011001;end
        				15:begin hex7 <= 7'b1111001; hex6 <= 7'b0010010;end			
            endcase
      			case(b)
        				0: begin hex5 <= 7'b1000000; hex4 <= 7'b1000000;end
        				1: begin hex5 <= 7'b1000000; hex4 <= 7'b1111001;end
        				2: begin hex5 <= 7'b1000000; hex4 <= 7'b0100100;end
        				3: begin hex5 <= 7'b1000000; hex4 <= 7'b0110000;end
        				4: begin hex5 <= 7'b1000000; hex4 <= 7'b0011001;end
        				5: begin hex5 <= 7'b1000000; hex4 <= 7'b0010010;end
        				6: begin hex5 <= 7'b1000000; hex4 <= 7'b0000010;end
        				7: begin hex5 <= 7'b1000000; hex4 <= 7'b1111000;end
        				8: begin hex5 <= 7'b1000000; hex4 <= 7'b0000000;end
        				9: begin hex5 <= 7'b1000000; hex4 <= 7'b0010000;end
        				10:begin hex5 <= 7'b1111001; hex4 <= 7'b1000000;end
        				11:begin hex5 <= 7'b1111001; hex4 <= 7'b1111001;end
        				12:begin hex5 <= 7'b1111001; hex4 <= 7'b0100100;end
        				13:begin hex5 <= 7'b1111001; hex4 <= 7'b0110000;end
        				14:begin hex5 <= 7'b1111001; hex4 <= 7'b0011001;end
        				15:begin hex5 <= 7'b1111001; hex4 <= 7'b0010010;end		
            endcase
      			case(r%10)
        				0:begin hex0 <= 7'b1000000;end
        				1:begin hex0 <= 7'b1111001;end
        				2:begin hex0 <= 7'b0100100;end
        				3:begin hex0 <= 7'b0110000;end
        				4:begin hex0 <= 7'b0011001;end
        				5:begin hex0 <= 7'b0010010;end
        				6:begin hex0 <= 7'b0000010;end
        				7:begin hex0 <= 7'b1111000;end
        				8:begin hex0 <= 7'b0000000;end
        				9:begin hex0 <= 7'b0010000;end		
            endcase
      			case(r/10%10)
        				0:begin hex1 <= 7'b1000000;end
        				1:begin hex1 <= 7'b1111001;end
        				2:begin hex1 <= 7'b0100100;end
        				3:begin hex1 <= 7'b0110000;end
        				4:begin hex1 <= 7'b0011001;end
        				5:begin hex1 <= 7'b0010010;end
        				6:begin hex1 <= 7'b0000010;end
        				7:begin hex1 <= 7'b1111000;end
        				8:begin hex1 <= 7'b0000000;end
        				9:begin hex1 <= 7'b0010000;end			
            endcase
      			case(r/100)
        				0:begin hex2 <= 7'b1000000;end
        				1:begin hex2 <= 7'b1111001;end
        				2:begin hex2 <= 7'b0100100;end  
            endcase
        end	
    end
endmodule
```

**波形仿真**：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559751669-11f27822-6147-4fa9-878a-dd1f3e59665d.png)

**硬件测试：**

![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737559751814-d4df4884-c6e6-4556-997f-01020481cce3.jpeg)

**实验结果分析：**

通过仿真，可以观察到4*4移位相加型乘法器的输出波形与预期结果一致。当输入端为不同的两个4位二进制数时，输出端输出这两个二进制数的乘积。

### 五、实验心得
通过本次实验，掌握了4*4移位相加型乘法器的基本原理和应用，能够使用EDA工具设计和仿真4*4移位相加型乘法器。

---

## 实验七、实用计数器
### 一、实验目的
1. 掌握Quartus Ⅱ的程序设计流程；
2. 掌握用原理图输入法实现项目的层次化设计过程；
3. 掌握半加器、全加器的程序设计。

### 二、实验原理
10进制器由4位二进制数组成，每一位二进制数对应一个十进制数字。

十进制数字0~9分别用二进制数0000~1001表示。

### 三、实验任务
1. 完成10进制计数器的Verilog程序编写并进行编译；
2. 要求带异步复位、时钟使能和数据加载功能，加载信号为0时，允许加载，否则计数，计数大于9时，计数清0。
3. 对设计的电路进行仿真验证；
4. 编程下载并在实验开发系统上验证设计结果。

### 四、实验结果与分析
**Verilog程序：**

```verilog
module cnt10(input clk, rst, en, load, output reg cout, output [3:0] dout, input [3:0] data);
    reg [3:0] q1;
  	assign dout = q1;
  	always@ (posedge clk or negedge rst) begin
      	if(!rst)			
            q1 <= 0;
      	else if(en) begin 
      			if (!load)		
                q1 <= data;
      			else if(q1<9)	
                q1 <= q1 + 1;
      			else 			
                q1 <= 4'b0000;
        end
  	end
  	always@ (q1)
    		if(q1 == 4'h9)	
            cout = 1'b1;
    		else			
            cout = 1'b0;
endmodule
```

```verilog
`timescale 10ns/1ps
module tb_cnt10();
  	reg 	clk, en, rst, load;
  	reg 	[3:0] data;
  	wire 	[3:0] dout;
  	wire 	cout;
  	always #10 clk = ~clk;
  
  	initial	begin
      	#0  clk = 1'b0;
      	#0  rst = 1'b0;
      	#60 rst = 1'b0;
      	#20 rst = 1'b1;
  	end
  
  	initial	begin
      	#0 	 en = 1'b0;
      	#50  en = 1'b1;
  	end
  
  	initial	begin
      	#0    load = 1'b1;
      	#240  load = 1'b0;
      	#25   load = 1'b1;
      	#700  load = 1'b0;
      	#30   load = 1'b1;
  	end
  
  	initial	begin
      	#0    data = 4'h4;
      	#70   data = 4'h8;
      	#200  data = 4'h7;
      	#300  data = 4'h8;
  	end
  
  	cnt10 U1(.clk(clk), .rst(rst), .en(en), .load(load), .cout(cout), .dout(dout), .data(data));
endmodule
```

**波形仿真**：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559752027-322c0325-e9ab-412c-81d7-376a7975a311.png)

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559752171-223fcf0e-a6b1-4d09-b566-301c0c947999.png)

**硬件测试：**

![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737559752337-6d221f71-244a-4ae7-a8b9-5f061211f184.jpeg)

**实验结果分析：**

代码编译通过。通过拨动开关成功点亮LED实现十进制计数器。

通过仿真，可以观察到10进制器的输出波形与预期结果一致。当输入端为不同的十进制数字时，输出端输出相应的4位二进制数。

### 五、实验心得
通过本次实验，掌握了10进制器的基本原理和应用，能够使用EDA工具设计和仿真10进制器。

---

## 实验八、移位寄存器
### 一、实验目的
1. 掌握Quartus Ⅱ的程序设计流程；
2. 掌握用原理图输入法实现项目的层次化设计过程。

### 二、实验原理
移位寄存器由若干个触发器组成。每个触发器存储一位二进制数据。移位寄存器有一个时钟端和一个移位端。当时钟信号上升沿到来时，移位寄存器中的数据向指定方向移位一位。

### 三、实验任务
1. 完成对8位二进制数分别实现循环左移、循环右移；
2. 对设计的电路进行仿真验证；
3. 编程下载并在实验开发系统上验证设计结果。

### 四、实验结果与分析
**Verilog程序：**

```verilog
module shft1(input clkin, load, ctrl, rst, input [7:0] din, output clkout, output reg [7:0] reg8);
    // 当ctrl为0时，左移最高位向qb输出；ctrl为1时，右移最低位向qb输出
    reg [27:0] c1;	reg clk_1hz;
  	always@ (posedge clkin or negedge rst) begin
        if(!rst)		
            c1 <= 0;
        else if(c1 == 4999_9999)	
            c1 <= 0;
        else            
            c1 <= c1 + 1;
  	end
  	always@ (posedge clkin or negedge rst) begin
        if(!rst)        
            clk_1hz <= 1'b0;
        else if(c1 == 0 || c1 == 2500_0000 - 1)
    				clk_1hz <= ~clk_1hz;
    		else	    
            clk_1hz <= clk_1hz;
  	end
  	assign clkout = clk_1hz;
  	always@ (posedge clkout) begin
    		if(load)	
            reg8 <= din;
    		else begin
      			if(!ctrl) begin		// 左移
                reg8[7:1] <= reg8[6:0];       reg8[0]   <= 0;        
            end
      			else begin			// 右移
                reg8[6:0] <= reg8[7:1];       reg8[7]   <= 1;			
            end
    		end
  	end
endmodule
```

**波形仿真**：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559752587-a43bbbc4-b603-4b99-a839-b70422809ea7.png)

**硬件测试：**

![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737559752767-886ec0b1-57c1-43ca-980c-d385da4ec9e1.jpeg)

**实验结果分析：**

代码编译通过。通过拨动开关成功点亮LED实现移位寄存器。

其中通过拨动开关，实现数据左移，再次拨动控制开关，实现数据右移。

### 五、实验心得
<font style="color:#3F4A54;">通过本次实验，掌握了移位寄存器的基本原理和应用，能够使用EDA工具设计和仿真移位寄存器。</font>

---

## 实验九、分频器
### 一、实验目的
1. 掌握Quartus Ⅱ的程序设计流程；
2. 掌握用原理图输入法实现项目的层次化设计过程。

### 二、实验原理
分频器由若干个触发器组成。每个触发器存储一位二进制数据。分频器有一个时钟端和一个输出端。当时钟信号上升沿到来时，分频器中的数据向指定方向移位一位。当移位到指定位置时，分频器输出一个脉冲信号。

### 三、实验任务
1. 完成实现奇数次和偶数次分频16进制计数器的Verilog程序编写并进行编译；
2. 对设计的电路进行仿真验证；
3. 编程下载并在实验开发系统上验证设计结果。

### 四、实验结果与分析
**Verilog程序：**

```verilog
module FDIV(input clk, rst, output J, O);		// 5分频、10分频
  	reg [2:0] c1, c2, c3;
  	reg m1, m2, m3;
  	always@ (posedge clk or negedge rst) begin
    		if(!rst) begin
      			c1 <= 0; c3 <= 0;
      			m1 <= 0; m3 <= 0;
    		end
    		else begin
      			if(c1 == 0) 			
                c1 <= c1+1; 
      			else if(c1 == 1) begin
        				m1 <= ~m1; 	c1 <= c1+1;
      			end
      			else if (c1 == 2) begin
        				m1 = ~m1;		c1 <= 0;
      			end
      			if(c3 == 0) 			
                c3 <= c3+1; 
      			else if(c3 == 1) begin
        				m3 <= ~m3;			c3 <= c3+1;
      			end
      			else if(c3 == 3) begin
        				m3 <= ~m3;			c3 <= 0;
      			end
      			else				
                c3 <= c3+1;
    		end
    end
  	always@ (negedge clk or negedge rst) begin
    		if(!rst) begin
          	c2 <= 0;			m2 <= 0;
    		end
    		else begin
      			if(c2 == 0) 		
                c2 <= c2+1; 
      			else if(c2 == 1) begin
        				m2 <= ~m2; 		c2 <= c2+1;
      			end
      			else if(c2 == 2) begin
        				m2 = ~m2;			c2 <= 0;
      			end
        end
  	end
  	assign J = m1|m2;
  	assign O = m3;
endmodule
```

```verilog
`timescale 10ns/1ns
module tb_fdiv5_10();
  	reg clk1, rst1;
  	wire Ji;
  	wire Ou;
  	always #20 clk1 = ~clk1;

  	initial begin
    		#0  clk1 = 1'b0;
    		#0  rst1 = 1'b1;
    		#5  rst1 = 1'b0;
    		#10 rst1 = 1'b1;
  	end

  	fdiv5_10 U2 (.clk(clk1), .rst(rst1), .J(Ji), .O(Ou));
endmodule
```

**波形仿真**：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559753043-370bda6c-75b0-4d30-834a-c85e57584609.png)

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559753184-9a3d0870-1a75-492b-a4d0-c181b2f7cd72.png)

**实验结果分析：**

通过仿真，可以观察到4位分频器的输出波形与预期结果一致。当输入端为一个高频时钟信号时，输出端输出一个频率为输入信号频率的1/4的时钟信号。

### 五、实验心得
通过本次实验，掌握了分频器的基本原理和应用，能够使用EDA工具设计和仿真分频器。

---

## 实验十、状态机
### 一、实验目的
1. 掌握Quartus Ⅱ的程序设计流程；
2. 掌握用原理图输入法实现项目的层次化设计过程。

### 二、实验原理
状态机由若干个状态寄存器组成。每个状态寄存器存储一个状态值。状态机有一个时钟端和若干个输入端。当时钟信号上升沿到来时，状态机根据当前状态和输入信号更新状态寄存器的值。状态机的输出由状态寄存器的值决定。

### 三、实验任务
1. 设计一个有限状态机，不少于5种状态；
2. 对设计的电路进行仿真验证；
3. 编程下载并在实验开发系统上验证设计结果。

### 四、实验结果与分析
**Verilog程序：**

```verilog
module fsm_exp(input clk, reset, input [0:1] state_inputs, output reg [3:0] comb_outputs, output reg [6:0] hex1, hex0);
    parameter s0=0, s1=1, s2=2, s3=3, s4=4;		// 定义状态参数
  	reg [4:0] c_st, next_state;		// 定义现态和次态的状态变量
  	reg [25:0] dcount=0;
  	always@ (posedge clk or negedge reset) begin	// 主控时序过程
        if(!reset) begin 				// 复位有效时，下一状态进入初态s0
            c_st <= s0;
            dcount <= 26'd0; 
        end 
        else begin
            if(dcount == 26'd49999999) begin
            		c_st <= next_state;	  
                dcount <= 26'd0;			
            end
            else    
                dcount <= dcount + 1;           
        end
    end
  	always@ (c_st or state_inputs) begin		// 主控组合过程
      	case(c_st)
          	s0 : begin 
      					comb_outputs <= 5;	  // 进入状态s0时，输出控制码5
      					if (state_inputs == 2'b00) 	
                    next_state <= s0;
      					else		
                    next_state <= s1;				
            end
      			s1 : begin 
      					comb_outputs <= 8;	  // 进入状态s1时，输出控制码8
      					if (state_inputs == 2'b01)		
                    next_state <= s1;
      					else		
                    next_state <= s2; 				
            end
      			s2 : begin 
      					comb_outputs <= 12;
      					if (state_inputs == 2'b10) 	
                    next_state <= s0;
      					else    	
                    next_state <= s3;				
            end
      			s3 : begin 
      					comb_outputs <= 14;
      					if (state_inputs == 2'b11)		
                    next_state <= s3;
      					else		
                    next_state <= s4;				
            end
      			s4 : begin 	
                comb_outputs <= 9; 		
                next_state <= s0; 	
            end
      			default: next_state <= s0;    // 现态若未出现以上各态，返回初态s0
        endcase
    		case(comb_outputs)              
            5: 	begin 
                hex1 <=  7'b1000000; hex0 <=  7'b0010010;	
            end
            8: 	begin 
                hex1 <=  7'b1000000; hex0 <=  7'b0000000;	
            end
            9: 	begin 
                hex1 <=  7'b1000000; hex0 <=  7'b0010000;	
            end
            12: 	begin 
                hex1 <=  7'b1111001; hex0 <=  7'b0100100;	
            end
            14: 	begin 
                hex1 <=  7'b1111001; hex0 <=  7'b0011001;	
            end
            default begin 
                hex1 <=  7'b1111111; hex0 <=  7'b1111111;	
            end
        endcase	
    end
endmodule 
```

```verilog
`timescale 10ns/1ns
module tb_fsm_exp();
  	reg clk1, rst1;
  	reg [1:0] state_input;
  	wire [3:0] comb_output;
  	always #20 clk1 = ~clk1;

  	initial	begin
      	#0 clk1 = 1'b0;
      	#0 rst1 = 1'b1;
      	#4 clk1 = 1'b0;
      	#10 rst1 = 1'b0;
      	#30 clk1= 1'b0;
      	#30 clk1= 1'b1;
      	#30 clk1= 1'b0;
      	#30 clk1= 1'b1;
      	#30 clk1= 1'b0;
      	#30 clk1= 1'b1;
  	end

  	initial	begin
      	#0   state_input = 2'b00;
      	#40  state_input = 2'b01;
      	#60  state_input = 2'b10;
      	#40  state_input = 2'b01;
      	#20  state_input = 2'b00;
  	end

	fsm_exp U1 (.clk(clk1), .reset(rst1), .state_inputs(state_input), .comb_outputs(comb_output));
endmodule
```

**波形仿真**：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559753399-88c1d993-e5ef-4060-a379-afa202e255ec.png)

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737559753541-fdaab01c-c616-4f7e-94e5-88ef1a27e456.png)

**硬件测试：**

![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737559753735-85fb4895-bb01-438e-810b-ffb5249150ae.jpeg)

**实验结果分析：**

通过仿真，可以观察到状态机的输出波形与预期结果一致。当输入端为不同的信号时，状态机输出不同的信号。

### 五、实验心得
通过本次实验，掌握了状态机的基本原理和应用，能够使用EDA工具设计和仿真状态机。

