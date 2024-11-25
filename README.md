# Verilog-50-Days-Challenge

8to1mux-verilog code[Structural Modeling]
module mux_8to1(
    input wire[7:0] in,
    input wire[2:0] sel,
    input out
    );
    wire [7:0]and_gate;
    assign and_gate[0]=in[0]&~sel[2]&~sel[1]&~sel[0];
    assign and_gate[1]=in[1]&~sel[2]&~sel[1]&sel[0];
    assign and_gate[2]=in[2]&~sel[2]&sel[1]&~sel[0];
    assign and_gate[3]=in[3]&~sel[2]&sel[1]&sel[0];
    assign and_gate[4]=in[4]&sel[2]&~sel[1]&~sel[0];
    assign and_gate[5]=in[5]&~sel[2]&sel[1]&~sel[0];
    assign and_gate[6]=in[6]&sel[2]&sel[1]&~sel[0];
    assign and_gate[7]=in[7]&sel[2]&sel[1]&~sel[0];
    assign out =|and_gate; 
endmodule
Testbench
module mux_8x1_tb;
    reg [7:0] in;       
    reg [2:0] sel;      
    wire out;           
    mux_8to1 UUT (
        .in(in), 
        .sel(sel), 
        .out(out)
    );
    initial begin
    $monitor("Time:%0t|in=%b|sel=%b|out=%b",$time,in,sel,out);
        in = 8'b00000000;
        sel = 3'b000;
        #10;
        in = 8'b01001010;
        sel = 3'b001;
        #10;     
        in = 8'b01000100;
        sel = 3'b010;
        #10;
        in = 8'b11010100;
        sel = 3'b110;
        #10;
        in = 8'b00001111;
        sel = 3'b111;
        #10;
        $finish; 
    end
endmodule
