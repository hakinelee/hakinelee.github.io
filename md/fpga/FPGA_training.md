> 可编程器件与硬件描述语言（Verilog HDL）实训报告，基于Altera DE2-115 教育开发板
>
> ![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737563686096-dfaab638-bd08-4df9-94d6-e517bee6851f.jpeg)
>

## 实验一：4×4矩阵键盘实现简易计算器
### 一、实验任务
用Verilog HDL设计一个简易计算器，该计算器可以计算简单的十以内加、减、乘、除四种计算（不考虑小数的运算）。通过4×4矩阵键盘输入数字及运算符，并将输入的数字与计算结果显示在七段共阳极数码管上。

### 二、设计原理
基本设计原理如下：通过矩阵键盘进行输入，通过判断按下的按键是数字还是运算符，如果是数字把它分别传给num1、num2，若为运算符则保存此运算符，在进行输入第二个数，在第二次遇到运算符时则运算，把运算结果给num1，把num2清零，显示num1。这样就完成了简单的加减乘除运算。

4×4矩阵键盘十分常用，图1是此键盘电路原理图与10芯接口原理图，注意此项设计要求输入端有上拉电阻。假设其两个4位口A[3:0]和B[3:0]都有上拉电阻。在应用中，当接下某键后，为了辨别和读取键信息，一种比较常用的方法是，向A口扫描输入一组分别只含一个0的4位数据，如1110、1101、1011等。若有键按下，则B口一定会输出对应的数据，这时，只要结合A、B口的数据，就能判断出键的位置。如当键S0按下，对于输入的A=1110，那么输出的B=0111。于是{B,A}=0111_1110就成了S0的代码。

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737566197717-c1c249df-7e40-4ac5-aaa8-465336fb051f.png)

图1-1 键盘电路原理图

计算器状态转换图：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737566197883-ff114971-b98e-4881-af17-0f71908b81ea.png)

图1-2 计算器状态图

### 三、程序代码
1. **键盘输入**

使用Verilog的case语句检测哪个键被按下，并将其转化为相应的数字和运算符编码。假设键盘布局已知，且每个按键对应一个唯一的扫描码。

```verilog
module key_array(
  	input Clk, Rst_n,
  	input [3:0] key_r,
  	output reg [3:0] key_c, key_out, 
  	output reg key_in 		// 按键输入标志，当有按键按下时为高电平
);
    always@(posedge Clk or negedge Rst_n)
    		if(!Rst_n) 	
            key_c <= 4'b1110;			  // 初始状态，扫描第一列
    		else if (key_r == 4'b1111) begin						// 没有按键按下
      			if (key_c == 4'b0111)	
                key_c <= 4'b1110;		// 重新回到第一列
      			else					
                key_c <= {key_c[2:0], key_c[3]};		// 切换到下一列
    		end
    always@(posedge Clk or negedge Rst_n)
    		if(!Rst_n) begin						// 没有按键按下
            key_out <= 4'he;	key_in <= 1'b1; 	
        end		
    		else if (key_r == 4'b1111)	 
            key_in <= 1'b1;
    		else begin
      			case(key_c)
        				4'b1110 : begin
          					case(key_r)
            						4'b1110 : begin	key_out <= 4'h1;	 key_in <= key_r[0];	end
            						4'b1101 : begin	key_out <= 4'h4;	 key_in <= key_r[1];	end
            						4'b1011 : begin	key_out <= 4'h7;	 key_in <= key_r[2];	end
          					endcase
        				end
        				4'b1101 : begin
          					case(key_r)	
            						4'b1110 : begin	key_out <= 4'h2;	 key_in <= key_r[0];	end
            						4'b1101 : begin	key_out <= 4'h5;	 key_in <= key_r[1];	end
            						4'b1011 : begin	key_out <= 4'h8;	 key_in <= key_r[2];	end
            						4'b0111 : begin	key_out <= 4'h0;	 key_in <= key_r[3];	end
          					endcase
        				end
                4'b1011 : begin
          					case(key_r)
            						4'b1110 : begin	key_out <= 4'h3;	 key_in <= key_r[0];	end
            						4'b1101 : begin	key_out <= 4'h6;	key_in <= key_r[1];	end
            						4'b1011 : begin	key_out <= 4'h9;	key_in <= key_r[2];	end
          					endcase
        				end
        				4'b0111 : begin
          					case(key_r)
            						4'b1110 : begin	key_out <= 4'ha;	key_in <= key_r[0];	end
            						4'b1101 : begin	key_out <= 4'hb;	key_in <= key_r[1];	end
            						4'b1011 : begin	key_out <= 4'hc;	key_in <= key_r[2];	end
            						4'b0111 : begin	key_out <= 4'hd;	key_in <= key_r[3];	end
          					endcase
        				end
      			endcase
    		end
endmodule	
```

2. **逻辑处理**

设计一个状态机来处理输入和计算过程，状态包括：等待输入第一个数、接收运算符、等待输入第二个数、计算结果。根据接收到的运算符和数执行相应的计算。

```verilog
module cal1 (
    input Clk, Rst_n,
    input [3:0] keypad_in,
  	output reg [3:0] key_c, cal,	// 加减乘除
    output reg [6:0] hex6, hex4, hex3, hex2, hex1, hex0
);
    parameter t1s = 500000/2, s0 = 2'b00, s1 = 2'b01, s2 = 2'b10, s3 = 2'b11;
  	reg [31:0] cnt;		reg [6:0] res, shang; 	// 计算结果
  	reg [3:0] key_out, num1, num2;		reg [1:0] oper, st;
  	reg clk1, boolflag;		// 标记结果正负
  	wire key_in, key_flag, key_state;		// key_flag按键按下标志位, key_state;按键状态
  	always @(posedge Clk or negedge Rst_n)
        if (!Rst_n)	
            cnt <= 0;
        else if (cnt == t1s - 1) begin	
            cnt <= 0;	clk1 = ~clk1;	
        end
        else	
            cnt <= cnt + 1;
  
    key_filter u1 (
      .Clk(clk1), .Rst_n(Rst_n), .key_in(key_in), 
      .key_flag(key_flag), .key_state(key_state)
    );
  
  	key_array u2 (
      .Clk(clk1),	.Rst_n(Rst_n), .key_r(keypad_in),	.key_c(key_c),
      .key_out(key_out), .key_in(key_in)
  	);

    always @(posedge clk1 or negedge Rst_n)
    		if (!Rst_n) begin
      			oper <= 2'b0; 		boolflag <= 1'b1;	  st <= s0; // 复位时回到s0状态
      			num1, num2, cal <= 4'b0000;		res, shang <= 7'b0000000;
    		end
    		else begin
      			case (st)
        				s0: begin		// 当前处于待输入第一个数字的状态
          					if (!key_in && key_out <= 4'h9) begin
            						num1 <= key_out;		num2 <= 4'b0000;
            						res, shang <= 7'b0000000;	 boolflag <= 1'b1;	  st <= s1;	
                    end
        				end
        				s1: begin		// 当前处于待输入操作符的状态
                    if (key_in && (key_out == 4'ha || key_out == 4'hb || key_out == 4'hc || key_out == 4'hd)) begin
            						case(key_out)
              							4'ha: begin	oper <= 2'b00; 	cal <= 4'b1000;	end
              							4'hb: begin	oper <= 2'b01;		cal <= 4'b0100;	end
              							4'hc: begin	oper <= 2'b10;		cal <= 4'b0010;	end
              							4'hd: begin	oper <= 2'b11;		cal <= 4'b0001;	end
              							default: begin	oper <= 2'b00;		cal <= 4'b1000;	end
            						endcase
            						st <= s2;
          					end
        				end
        				s2: begin		// 当前处于待输入第二个数字的状态
          					if (key_in && key_out <= 4'h9) begin	
                        num2 <= key_out;	st <= s3;	
                    end
          			end
                s3: begin		// 当前处于计算状态
          					case(oper)
            						2'b00: res <= num1 + num2;
            						2'b01: begin
              							if(num1 >= num2)		
                                res <= num1 - num2;
              							else begin	
                                boolflag <= 1'b0;	
                                res <= num2 - num1;	
                            end
            						end
            						2'b10: res <= mult4b(num1, num2);
            						2'b11: begin
              							shang <= div7(num1, num2);	
                            res <= num1 % num2;
            						end
            						default: begin		
                            res, shang <= 7'b0000000;	
                        end
            				endcase
            				st <= s0;
              	end
        				default: st <= s0;
          	endcase
        end

  	always @(*)
    		if (!Rst_n) begin	
            hex6, hex4, hex3, hex2, hex1, hex0 <= 7'b0111111;	 
        end
    		else begin
      			if(!boolflag)	
                hex2 <= 7'b0111111;	// 显示负号
      			else			
                hex2 <= 7'b1111111;	// 不显示负号
          
      			if(oper == 2'b11) begin
        				hex3 <= 7'b1000000;
        				case(shang)
          					7'd0: hex2 <= 7'b1000000;	7'd1: hex2 <= 7'b1111001;
          					7'd2: hex2 <= 7'b0100100;	7'd3: hex2 <= 7'b0110000;
          					7'd4: hex2 <= 7'b0011001;	7'd5: hex2 <= 7'b0010010;
          					7'd6: hex2 <= 7'b0000010;	7'd7: hex2 <= 7'b1111000;
          					7'd8: hex2 <= 7'b0000000;	7'd9: hex2 <= 7'b0010000;
          					default : hex2 <= 7'b1000000;
        				endcase
      			end
      			else		
                hex3 <= 7'b1111111;
        
            case(num1)
        				7'd0: hex6 <= 7'b1000000;	7'd1: hex6 <= 7'b1111001;
        				7'd2: hex6 <= 7'b0100100;	7'd3: hex6 <= 7'b0110000;
        				7'd4: hex6 <= 7'b0011001;	7'd5: hex6 <= 7'b0010010;
        				7'd6: hex6 <= 7'b0000010;	7'd7: hex6 <= 7'b1111000;
        				7'd8: hex6 <= 7'b0000000;	7'd9: hex6 <= 7'b0010000;
        				default : hex6 <= 7'b1000000;
      			endcase
      			case(num2)
        				7'd0: hex7 <= 7'b1000000;	7'd1: hex4 <= 7'b1111001;
        				7'd2: hex4 <= 7'b0100100;	7'd3: hex4 <= 7'b0110000;
        				7'd4: hex4 <= 7'b0011001;	7'd5: hex4 <= 7'b0010010;
        				7'd6: hex4 <= 7'b0000010;	7'd7: hex4 <= 7'b1111000;
        				7'd8: hex4 <= 7'b0000000;	7'd9: hex4 <= 7'b0010000;
        				default : hex4 <= 7'b1000000;
      			endcase
          	case(res/10)
        				7'd0: hex1 <= 7'b1000000;	7'd1: hex1 <= 7'b1111001;
        				7'd2: hex1 <= 7'b0100100;	7'd3: hex1 <= 7'b0110000;
        				7'd4: hex1 <= 7'b0011001;	7'd5: hex1 <= 7'b0010010;
        				7'd6: hex1 <= 7'b0000010;	7'd7: hex1 <= 7'b1111000;
        				7'd8: hex1 <= 7'b0000000;	7'd9: hex1 <= 7'b0010000;
        				default : hex1 <= 7'b1000000;
      			endcase
      			case(res%10)
        				7'd0: hex0 <= 7'b1000000;	7'd1: hex0 <= 7'b1111001;
        				7'd2: hex0 <= 7'b0100100;	7'd3: hex0 <= 7'b0110000;
        				7'd4: hex0 <= 7'b0011001;	7'd5: hex0 <= 7'b0010010;
        				7'd6: hex0 <= 7'b0000010;	7'd7: hex0 <= 7'b1111000;
        				7'd8: hex0 <= 7'b0000000;	7'd9: hex0 <= 7'b0010000;
        				default : hex0 <= 7'b1000000;
      			endcase
    		end
  
    function [6:0] mult4b;
        input [3:0] data_a, data_b;	integer i;
        begin
            mult4b = 7'b0;
            for (i = 0; i <= 3; i = i + 1) begin
                if (data_b[i])	
            				mult4b = mult4b + (data_a << i);
            end
        end
    endfunction
	
    function [6:0] div7;
    		input [3:0] data_c, data_d;	reg [3:0] at, bt, p;	
      	reg [6:0] q;	integer j;
        if (data_d == 4'b0000)		
            q = 7'b0000000;
        else if (data_c == data_d)	
            q = 7'b0000001;
        else if(data_c < data_d)		
            q = 7'b0000000;
        else begin
            at = data_c;	bt = data_d;	
            p = 4'b0000;	q = 7'b0000000;
            for (j = 3; j >= 0; j = j - 1) begin
                p = {p[2:0], at[3]};		at = {at[2:0], 1'b0};	
          			p = p - bt;
                if (p[3] == 1) begin		
            				q[j] = 0;	p = p + bt;
        				end
                else 	
                    q[j] = 1;
            end
        end
        div7 = q;
    endfunction

endmodule
```

### 四、结果分析
| ![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737566198074-95598a66-ffce-41cf-a15e-d1e8258601f9.jpeg) | ![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737566198348-7991c573-f1c8-4054-9c46-02985bd59ed1.jpeg) |
| :---: | :---: |
| 图1-3 计算器-加法 | 图1-4 计算器-加法 |
| ![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737566198615-9410ed20-66ec-4ba8-85a6-7b0db5313c2d.jpeg) | ![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737566198864-f6955264-8266-4ed9-bfc6-0dffcab80e91.jpeg) |
| 图1-5 计算器-乘法 | 图1-6 计算器-除法 |


功能验证：通过仿真和实际硬件测试，验证计算器能够正确执行加、减、乘、除四种基本运算。

### 五、实验心得
通过这次简易计算器的Verilog HDL设计实验，我深刻体会到了理论与实践结合的重要性。通过亲手编写和调试代码，我不仅巩固了Verilog的语法知识，还学会了如何根据硬件需求进行逻辑设计。整个过程中，面对各种挑战和困难，我不断尝试、学习和改进，最终成功实现了计算器的基本功能。这次实验不仅提升了我的专业技能，还锻炼了我的问题解决能力和创新思维。

---

## 实验二：交通灯控制系统
### 一、实验任务
用Verilog HDL设计一个十字路口上使用的交通灯控制系统。具体要求如下：

1. 四个方向上各设一组信号灯，每个方向上分别有直行信号灯与左转信号灯；
2. 设置一组动态数码管，以倒计时的方式显示允许通行或禁止通行的时间，其中绿灯、黄灯和红灯的持续时间分别为10s、5s和15s；
3. 用红色 led 灯代表红灯，绿色led灯代表绿灯，黄灯则用四个红色的 led灯，红绿灯切换时有黄灯闪烁；
4. 允许特殊情况，当交通管制时，此时各个方向上均是红灯亮，倒计时停止，显示“-”，当交通管制结束后，信号灯恢复原来状态，继续正常运行。

### 二、设计原理
交通灯运行情况如下：

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737566199092-24d4deb8-8c11-45b0-a991-1726ef2db92e.png)

图2-1 交通信号灯状态图

为了设计一个十字路口的交通灯控制系统，需要将设计分为几个主要部分：状态机、计时器、交通灯控制以及数码管显示。以下是这个设计的Verilog HDL代码的基本框架和原理：

1. 状态机

状态机将控制交通灯的切换顺序和特殊情况（如交通管制）。状态可以包括：

S0：交通管制时，所有方向的灯全是红灯；

S1：东西直行灯：绿，东西左转灯：红，南北直行灯：红，南北左转灯：红；

S2：东西直行灯：黄，东西左转灯：红，南北直行灯：红，南北左转灯：红；

S3：东西直行灯：红，东西左转灯：绿，南北直行灯：红，南北左转灯：红；

S4：东西直行灯：红，东西左转灯：黄，南北直行灯：红，南北左转灯：红；

S5：东西直行灯：红，东西左转灯：红，南北直行灯：绿，南北左转灯：红；

S6：东西直行灯：红，东西左转灯：红，南北直行灯：黄，南北左转灯：红；

S7：东西直行灯：红，东西左转灯：红，南北直行灯：红，南北左转灯：绿；

S8：东西直行灯：红，东西左转灯：红，南北直行灯：红，南北左转灯：黄；

2. 计时器

计时器用于控制每个状态的持续时间。需要使用四个变量用于记录东西直行倒计时、东西左转倒计时、南北直行倒计时、南北左转倒计时。 

3. 交通灯控制

根据状态机的当前状态，控制交通灯的亮灭。

4. 数码管显示

数码管用于显示剩余时间。在交通管制模式下，显示“-”。

### 三、程序代码
1. **灯光闪烁控制**

```verilog
module led(
  	input clk, rst,
  	input [4:0] c_st,
  	output reg [3:0] ledg, 
  	output reg [15:0] ledr
);
    parameter s0 = 5'b00000, s1 = 5'b00001, s2 = 5'b00010, s3 = 5'b00011, s4 = 5'b00100, s5 = 5'b00101, s6 = 5'b00110, s7 = 5'b00111, s8 = 5'b01000;
    reg flag = 1'b1;
  	always @(posedge clk or negedge rst)
    		if(!rst)	
            ledg <= 4'b0000;
    		else begin
      			case(c_st)
                s0: ledg <= 4'b0000;	 s1: ledg <= 4'b1000;
        				s2: ledg <= 4'b0000;	 s3: ledg <= 4'b0100;
        				s4: ledg <= 4'b0000;	 s5: ledg <= 4'b0010;
        				s6: ledg <= 4'b0000;	 s7: ledg <= 4'b0001;
        				s8: ledg <= 4'b0000;	 default: ledg <= ledg;
        		endcase
        end

    always @(posedge clk or negedge rst)  	/* 针对黄灯闪烁 */
    		if(!rst)	 
            ledr <= 16'b0;
    		else begin
      			case(c_st)
        				s0: ledr <= 16'b1111_1111_1111_1111; 
                s1: ledr <= 16'b0000_0001_0001_0001;
        				s2: begin
          					if(flag)  	
                        ledr <= 16'b1111_0001_0001_0001;
          					else		
                        ledr <= 16'b0000_0001_0001_0001;
          					flag <= ~flag;
        				end				
        				s3: ledr <= 16'b0001_0000_0001_0001;
        				s4: begin
          					if(flag) 	
                        ledr <= 16'b0001_1111_0001_0001;
          					else
                        ledr <= 16'b0001_0000_0001_0001;
          					flag <= ~flag;
        				end				
                s5: ledr <= 16'b0001_0001_0000_0001;
        				s6: begin
          					if(flag) 	
                        ledr <= 16'b0001_0001_1111_0001;
          					else
                        ledr <= 16'b0001_0001_0000_0001;
          					flag <= ~flag;
        				end
        				s7: ledr <= 16'b0001_0001_0001_0000;
        				s8: begin
          					if(flag) 	
                        ledr <= 16'b0001_0001_0001_1111;
          					else
                        ledr <= 16'b0001_0001_0001_0000;
          					flag <= ~flag;
        				end
        				default: ledr <= ledr;
        		endcase
        end
endmodule
```

**2. 状态机切换**

```verilog
module jtd_logic(
    input clk, rst, ctrl,
    output reg [4:0] c_st,
    output reg [5:0] ts_dx_1, ts_dx_2, ts_nb_1, ts_nb_2
);
    parameter s0 = 5'b00000, s1 = 5'b00001, s2 = 5'b00010, s3 = 5'b00011, s4 = 5'b00100, 
              s5 = 5'b00101, s6 = 5'b00110, s7 = 5'b00111, s8 = 5'b01000;
    reg [4:0] n_st;		reg [31:0] cnt;
    always @(posedge clk or negedge rst)
        if (!rst) 
            c_st <= s1;
        else
            c_st <= n_st;
     always @(*)
        case (c_st)
            s0: n_st <= (!ctrl) ? s0 : s1;
            s1: n_st <= (!ctrl) ? s0 : ((ts_dx_1 == 1) ? s2 : s1);
            s2: n_st <= (!ctrl) ? s0 : ((ts_dx_1 == 1 && ts_dx_2 == 1) ? s3 : s2);
            s3: n_st <= (!ctrl) ? s0 : ((ts_dx_2 == 1) ? s4 : s3);
            s4: n_st <= (!ctrl) ? s0 : ((ts_dx_2 == 1 && ts_nb_1 == 1) ? s5 : s4);
            s5: n_st <= (!ctrl) ? s0 : ((ts_nb_1 == 1) ? s6 : s5);
            s6: n_st <= (!ctrl) ? s0 : ((ts_nb_1 == 1 && ts_nb_2 == 1) ? s7 : s6);
            s7: n_st <= (!ctrl) ? s0 : ((ts_nb_2 == 1) ? s8 : s7);
            s8: n_st <= (!ctrl) ? s0 : ((ts_dx_1 == 1 && ts_nb_2 == 1) ? s1 : s8);
            default: n_st <= s1;
        endcase
     always @(posedge clk or negedge rst)
        if (!rst) begin
            ts_dx_1 <= 6'd10;  ts_dx_2 <= 6'd15;
            ts_nb_1 <= 6'd30;  ts_nb_2 <= 6'd45;
        end
        else begin
      			if (c_st == s0) begin
                ts_dx_1 <= 6'd10;  ts_dx_2 <= 6'd15;
                ts_nb_1 <= 6'd30;  ts_nb_2 <= 6'd45;
            end
            else begin
        				if (c_st == s1 || c_st == s2 || c_st == s3 || c_st == s4 || c_st == s5 || c_st == s6 || c_st == s7 || c_st == s8) begin
          					ts_dx_1 <= (ts_dx_1 == 1) ? ((c_st == s2) ? 6'd45 : (c_st == s1 ? 6'd5 : (c_st == s8 ? 6'd10 : ts_dx_1 - 1))) : ts_dx_1 - 1;
          					ts_dx_2 <= (ts_dx_2 == 1) ? ((c_st == s4) ? 6'd45 : (c_st == s3 ? 6'd5 : (c_st == s2 ? 6'd10 : ts_dx_2 - 1))) : ts_dx_2 - 1;
          					ts_nb_1 <= (ts_nb_1 == 1) ? ((c_st == s6) ? 6'd45 : (c_st == s5 ? 6'd5 : (c_st == s4 ? 6'd10 : ts_nb_1 - 1))) : ts_nb_1 - 1;
          					ts_nb_2 <= (ts_nb_2 == 1) ? ((c_st == s8) ? 6'd45 : (c_st == s7 ? 6'd5 : (c_st == s6 ? 6'd10 : ts_nb_2 - 1))) : ts_nb_2 - 1;
        				end
            end
        end
endmodule
```

**3. 数码管显示**

```verilog
module smg(
  	input clk, rst, ctrl,
  	input [5:0] ts_dx_1, ts_dx_2, ts_nb_1, ts_nb_2,
  	output reg [6:0] hex7, hex6, hex5, hex4, hex3, hex2, hex1, hex0
);
    always @(posedge clk or negedge rst)
      	if (!rst) begin			// 所有数码管显示 0
      			hex0 <= 7'b1000000;  	hex1 <= 7'b1000000;
      			hex2 <= 7'b1000000;  	hex3 <= 7'b1000000;
      			hex4 <= 7'b1000000;  	hex5 <= 7'b1000000;
      			hex6 <= 7'b1000000;  	hex7 <= 7'b1000000;
        end
        else if (!ctrl) begin	   // 所有数码管显示 - 
      			hex0 <= 7'b0111111;  	hex1 <= 7'b0111111;
      			hex2 <= 7'b0111111;  	hex3 <= 7'b0111111;
      			hex4 <= 7'b0111111;  	hex5 <= 7'b0111111;
      			hex6 <= 7'b0111111;  	hex7 <= 7'b0111111;
      	end
        else begin
      			case(ts_dx_1 / 10)		/* 东西直行 */
        				0: hex7 <= 7'b1000000;		1: hex7 <= 7'b1111001;
        				2: hex7 <= 7'b0100100;		3: hex7 <= 7'b0110000;
        				4: hex7 <= 7'b0011001;		5: hex7 <= 7'b0010010;
        				6: hex7 <= 7'b0000010;  	7: hex7 <= 7'b1111000;
        				8: hex7 <= 7'b0000000;		9: hex7 <= 7'b0010000;
        				default: hex7 <= 7'b1000000;
      			endcase
            case(ts_dx_1 % 10)
        				0: hex6 <= 7'b1000000;		1: hex6 <= 7'b1111001;
        				2: hex6 <= 7'b0100100;		3: hex6 <= 7'b0110000;
        				4: hex6 <= 7'b0011001;		5: hex6 <= 7'b0010010;
        				6: hex6 <= 7'b0000010;		7: hex6 <= 7'b1111000;
        				8: hex6 <= 7'b0000000;		9: hex6 <= 7'b0010000;
        				default: hex6 <= 7'b1000000;
      			endcase
            case(ts_dx_2 / 10)		/* 东西左转 */
        				0: hex5 <= 7'b1000000; 	1: hex5 <= 7'b1111001;
        				2: hex5 <= 7'b0100100; 	3: hex5 <= 7'b0110000;
        				4: hex5 <= 7'b0011001; 	5: hex5 <= 7'b0010010;
        				6: hex5 <= 7'b0000010; 	7: hex5 <= 7'b1111000;
        				8: hex5 <= 7'b0000000; 	9: hex5 <= 7'b0010000;
        				default: hex5 <= 7'b1000000;
        		endcase	
            case(ts_dx_2 % 10)
        				0: hex4 <= 7'b1000000;	1: hex4 <= 7'b1111001;
        				2: hex4 <= 7'b0100100; 	3: hex4 <= 7'b0110000;
        				4: hex4 <= 7'b0011001; 	5: hex4 <= 7'b0010010;
        				6: hex4 <= 7'b0000010; 	7: hex4 <= 7'b1111000;
        				8: hex4 <= 7'b0000000; 	9: hex4 <= 7'b0010000;
        				default: hex4 <= 7'b1000000;
        		endcase
            case(ts_nb_1 / 10)		/* 南北直行 */
        				0: hex3 <= 7'b1000000; 	1: hex3 <= 7'b1111001;
        				2: hex3 <= 7'b0100100; 	3: hex3 <= 7'b0110000;
        				4: hex3 <= 7'b0011001; 	5: hex3 <= 7'b0010010;
        				6: hex3 <= 7'b0000010; 	7: hex3 <= 7'b1111000;
        				8: hex3 <= 7'b0000000; 	9: hex3 <= 7'b0010000;
        				default: hex3 <= 7'b1000000;
        		endcase	
            case(ts_nb_1 % 10)
        				0: hex2 <= 7'b1000000; 	1: hex2 <= 7'b1111001;
        				2: hex2 <= 7'b0100100; 	3: hex2 <= 7'b0110000;
        				4: hex2 <= 7'b0011001; 	5: hex2 <= 7'b0010010;
        				6: hex2 <= 7'b0000010; 	7: hex2 <= 7'b1111000;
        				8: hex2 <= 7'b0000000; 	9: hex2 <= 7'b0010000;
        				default: hex2 <= 7'b1000000;
        		endcase
      			case(ts_nb_2 / 10)		/* 南北左转 */
        				0: hex1 <= 7'b1000000; 	1: hex1 <= 7'b1111001;
        				2: hex1 <= 7'b0100100; 	3: hex1 <= 7'b0110000;
        				4: hex1 <= 7'b0011001;	5: hex1 <= 7'b0010010;
        				6: hex1 <= 7'b0000010; 	7: hex1 <= 7'b1111000;
        				8: hex1 <= 7'b0000000; 	9: hex1 <= 7'b0010000;
        				default: hex1 <= 7'b1000000;
      			endcase	
            case(ts_nb_2 % 10)
        				0: hex0 <= 7'b1000000; 	1: hex0 <= 7'b1111001;
        				2: hex0 <= 7'b0100100; 	3: hex0 <= 7'b0110000;
        				4: hex0 <= 7'b0011001; 	5: hex0 <= 7'b0010010;
        				6: hex0 <= 7'b0000010; 	7: hex0 <= 7'b1111000;
        				8: hex0 <= 7'b0000000; 	9: hex0 <= 7'b0010000;
        				default: hex0 <= 7'b1000000;
      			endcase
        end
endmodule
```

### 四、结果分析
| ![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737566199262-32a325f5-3b3c-4f05-ac66-1d64fd9bc7e4.jpeg) | ![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737566199756-58ae5a24-5a9f-4f46-9044-d639fdcbb732.jpeg) |
| :---: | :---: |
| 图2-2 东西直行黄灯亮 | 图2-3 东西左转黄灯亮 |
| ![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737566200031-63159476-8310-4eaf-bcae-69b0d9e26514.jpeg) | ![](https://cdn.nlark.com/yuque/0/2025/jpeg/29514937/1737566200259-6be4d281-ae95-4bdd-aa44-13ed0a17cceb.jpeg) |
| 图2-4 南北直行黄灯亮 | 图2-5 南北左转黄灯亮 |


信号灯逻辑：

+ 每个方向直行和左转信号灯的切换顺序为：绿灯（10s）→ 黄灯闪烁（5s）→ 红灯（15s），然后切换到下一个方向。

倒计时显示：

+ 使用动态数码管来显示剩余时间。当倒计时结束时，切换到下一个状态或方向。

LED灯表示：

+ 红灯使用红色LED灯。绿灯使用绿色LED灯。
+ 黄灯使用四个红色LED灯，并让它们交替闪烁以表示黄灯状态。

交通管制：

+ 在交通管制状态下，所有方向均显示红灯，数码管显示“-”。
+ 交通管制结束后，系统恢复到正常运行状态。

### 五、实验心得
通过这次实验，我深入了解了如何使用Verilog HDL来设计一个复杂的控制系统。在设计过程中，我遇到了不少挑战，但通过不断地学习和尝试，我最终成功地完成了这个设计。

状态机的设计是本次实验的关键。我花费了相当长的时间来思考和规划各个状态之间的转换逻辑。通过这个过程，我更加熟悉了状态机的概念和设计方法。

在设计倒计时显示功能时，我遇到了计时器精度和同步的问题。通过查阅资料和实践，我最终选择了合适的计时器实现方式，并确保了数码管显示的准确性。

控制LED灯的闪烁和亮灭需要精确的时序控制。我通过编写精确的Verilog代码，利用不同的分频逻辑，实现了LED灯的闪烁效果，并确保了它们在正确的时刻亮起或熄灭。

---

## 实验三：简易DDS信号发生器
### 一、实验任务
使用FPGA开发板设计并实现一个简易DDS（Direct Digital Frequency Synthesize，直接数字频率合成）信号发生器，能够产生频率、幅度可调的正弦波、方波、三角波、锯齿波等波形，该信号发生器可以使用4个拨码开关控制输出波形切换。

### 二、设计原理
DDS信号产生的理论基础是“奈奎斯特采样定理”。在定理中可知当抽样频率大于等于模拟信号最高频率两倍时，就可以从离散序列无失真的信号中恢复出原始模拟信号。DDS信号发生原理是对模拟信号进行抽样。当一个抽样过程已经发生且抽样值已经量化完成，从量化数值重建原始模拟信号。

一个基本的DDS的基本结构，主要由相位累加器、相位调制器、波形数据表ROM、D/A转换器等四大结构组成，其中较多设计还会在数模转换器之后增加一个低通滤波器。其中相位累加器和波形量化数据存储器称为数控振荡器，是DDS结构中的数字部分。DDS基本结构原理如下图所示。

![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737566200494-30924c85-a397-492c-a61d-16a8053fb951.png)

图3-1 DDS基本结构原理图

### 三、程序设计
要实现DDS信号发生器需要4部分，D/A转换器交由外部挂载的高速AD/DA板卡处理，其他3部分，相位累加器、相位调制器、波形数据表ROM由FPGA负责。需要建立一个单独的模块对DDS部分进行处理；还需要使用按键实现4种波形的切换，还要加上按键消抖；同时也要声明一个按键控制模块对4个输入按键进行控制，最后再加一个顶层模块。

1. **ROM内波形数据写入**

该DDS信号发生器想要实现正弦波、方波、三角波和锯齿波4种波形的输出，需要事先在波形数据表ROM中存入4种波形信号各自的完整周期波形数据。使用MATLAB绘制4种信号波形，对波形进行等间隔采样，以采样次数作为ROM存储地址，将采集的波形幅值数据做为存储数据写入存储地址对应的存储空间。

2. **DDS模块**

```verilog
module dds (
  	input wire sys_clk,  	   			// 系统时钟,50MHz
  	input wire sys_rst_n,      		// 复位信号,低电平有效
  	input wire [3:0] wave_select, // 输出波形选择
  	output wire [7:0] data_out 		// 波形输出
);
    parameter sin_wave = 4'b0001 , 		// 正弦波
      			  squ_wave = 4'b0010 , 		// 方波
      			  tri_wave = 4'b0100 , 		// 三角波
      			  saw_wave = 4'b1000 ; 		// 锯齿波
  	parameter FREQ_CTRL = 32'd42949 , // 相位累加器单次累加值
      			 PHASE_CTRL = 12'd1024 ; 	// 相位偏移量
  	reg [31:0] fre_add ;  	 // 相位累加器
  	reg [11:0] rom_addr_reg; // 相位调制后的相位码
  	reg [13:0] rom_addr ; 	 // ROM读地址
    always@(posedge sys_clk or negedge sys_rst_n)		// fre_add: 相位累加器
    		if(sys_rst_n == 1'b0)	 
            fre_add <= 32'd0;
    		else
      			fre_add <= fre_add + FREQ_CTRL;
    always@(posedge sys_clk or negedge sys_rst_n)		// rom_addr: ROM读地址
    		if(sys_rst_n == 1'b0) begin	
            rom_addr <= 14'd0;	 rom_addr_reg <= 11'd0; 	
        end
    		else
      			case(wave_select)
        				sin_wave: begin 	// 正弦波
          					rom_addr_reg <= fre_add[31:20] + PHASE_CTRL;
          					rom_addr <= rom_addr_reg;
        				end
        				squ_wave: begin		// 方波
          					rom_addr_reg <= fre_add[31:20] + PHASE_CTRL;
          					rom_addr <= rom_addr_reg + 14'd4096;
        				end 
        				tri_wave: begin		// 三角波
          					rom_addr_reg <= fre_add[31:20] + PHASE_CTRL;
          					rom_addr <= rom_addr_reg + 14'd8192;
        				end 
        				saw_wave: begin		// 锯齿波
          					rom_addr_reg <= fre_add[31:20] + PHASE_CTRL;
          					rom_addr <= rom_addr_reg + 14'd12288;
        				end 
        				default: begin 		// 正弦波
          					rom_addr_reg <= fre_add[31:20] + PHASE_CTRL;
          					rom_addr <= rom_addr_reg;
        				end
      			endcase
  
  	rom_wave rom_wave_inst (
    		.address(rom_addr), // ROM读地址
    		.clock(sys_clk), 	  // 读时钟
    		.q(data_out) 				// 读出波形数据
  	);
endmodule
```

3. 按键控制模块

```verilog
module key_control (
  	input wire sys_clk , 					// 系统时钟,50MHz
  	input wire sys_rst_n , 				// 复位信号,低电平有效
  	input wire [3:0] key , 				// 输入4位按键
  	output reg [3:0] wave_select 	// 输出波形选择
);
  	parameter sin_wave = 4'b0001,    // 正弦波
      			  squ_wave = 4'b0010,    // 方波
      			  tri_wave = 4'b0100,    // 三角波
      			  saw_wave = 4'b1000;    // 锯齿波
  	parameter CNT_MAX = 20'd999_999; // 计数器计数最大值
  	wire key0, key1, key2, key3;  	 // 按键 0 - 3
  	always@(posedge sys_clk or negedge sys_rst_n)		// wave: 按键状态对应波形
    		if(sys_rst_n == 1'b0)
      			wave_select <= 4'b0000;
    		else if(key0 == 1'b1)
      			wave_select <= sin_wave;
    		else if(key1 == 1'b1)
      			wave_select <= squ_wave;
    		else if(key2 == 1'b1)
      			wave_select <= tri_wave;
    		else if(key3 == 1'b1)
      			wave_select <= saw_wave;
    		else
      			wave_select <= wave_select;
  
  	key_filter #(.CNT_MAX(CNT_MAX)) key_filter_inst3 (
    		.sys_clk(sys_clk), 			// 系统时钟50Mhz
    		.sys_rst_n(sys_rst_n),  // 全局复位
    		.key_in(key[3]), 				// 按键输入信号
    		.key_flag(key3) 				// 按键消抖后标志信号
  	);
  
  	key_filter #(.CNT_MAX(CNT_MAX)) key_filter_inst2 (
    		.sys_clk(sys_clk),
    		.sys_rst_n(sys_rst_n),
    		.key_in(key[2]),
    		.key_flag(key2)
  	);
  
  	key_filter #(.CNT_MAX(CNT_MAX)) key_filter_inst1 (
    		.sys_clk(sys_clk),
    		.sys_rst_n(sys_rst_n),
    		.key_in(key[1]),
    		.key_flag(key1)
  	);
  
  	key_filter #(.CNT_MAX(CNT_MAX)) key_filter_inst0 (
    		.sys_clk(sys_clk),
    		.sys_rst_n(sys_rst_n),
    		.key_in(key[0]),
    		.key_flag(key0)
  	);
endmodule
```

4. 顶层模块

```verilog
module top_dds (
  	input wire sys_clk, 				// 系统时钟,50MHz
  	input wire sys_rst_n, 			// 复位信号,低电平有效
  	input wire [3:0] key, 			// 输入4位按键
  	output wire dac_clk, 				// 输入DAC模块时钟
  	output wire [7:0] dac_data 	// 输入DAC模块波形数据
);
  	wire [3:0] wave_select ; 		// 波形选择
  	assign dac_clk = ~sys_clk;	// dac_clka:DAC模块时钟

  	dds dds_inst (
    		.sys_clk (sys_clk), 				// 系统时钟,50MHz
    		.sys_rst_n (sys_rst_n),	 		// 复位信号,低电平有效
    		.wave_select (wave_select), // 输出波形选择
    		.data_out (dac_data) 				// 波形输出
  	);

  	key_control key_control_inst (
    		.sys_clk (sys_clk), 				// 系统时钟,50MHz
    		.sys_rst_n (sys_rst_n), 		// 复位信号,低电平有效
    		.key (key), 								// 输入4位按键
    		.wave_select (wave_select)  // 输出波形选择
  	);
endmodule
```

### 四、结果分析
使用ModelSim软件对顶层模块进行仿真，由图可知，输入与输出信号能正常传入传出顶层模块，顶层模块通过仿真验证。

| ![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737566200723-5c535ecb-e1fd-498e-9a65-15e43f5096fb.png) |
| :---: |
| 图3-2 顶层模块仿真波形 |


系统能输出的波形有方波、三角波、锯齿波与正弦波，使用按键可进行输出波形切换。

将程序编译并下载至DE2-115开发板中，使用SignalTap（内嵌逻辑分析仪）观察到的波形与MATLAB生成波形对比，可以发现信号正常输出，模块通过仿真验证。

| ![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737566200903-cdcd6682-b3dd-4f50-a1d1-bf4e0d0e01ad.png) |
| :---: |
| 图3-3 测量图（一） 正弦波 |
| ![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737566201036-51645a68-bdd1-4277-969a-5293baf41619.png) |
| 图3-4 测量图（二） 方波 |
| ![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737566201179-12733e47-762d-43ef-a002-3d1f43836483.png) |
| 图3-5 测量图（三） 三角波 |
| ![](https://cdn.nlark.com/yuque/0/2025/png/29514937/1737566201330-e77d54ee-10c5-43ef-849d-a4141240d2f2.png) |
| 图3-6 测量图（四） 锯齿波 |


### 五、实验心得
设计DDS信号发生器是一个具有挑战性的项目，但也为我提供了很多学习的机会。我深入了解了DDS的工作原理、Verilog HDL的编程技巧以及硬件设计和测试的方法。编写Verilog代码时，我注意到了模块化设计的重要性。通过将DDS的不同部分（如相位累加器、查找表和DAC模型）封装成独立的模块，我可以更容易地测试和调试每个部分。通过这个项目，我不仅提高了我的技术能力，还学会了如何解决实际问题并不断优化我的解决方案。我相信这些经验将对我未来的学习和工作产生积极的影响。

