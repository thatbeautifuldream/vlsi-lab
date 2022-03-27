# 4 bit counter

- full_adder.v

```vhdl
module full_adder(A,B,C_in,Sum,C_out);
input A,B,C_in;
output Sum,C_out;
assign Sum = A ^ B ^ C_in;
assign C_out = (A & B) | (C_in & (A ^ B));
endmodule
```

- four_bit_adder.v

```vhdl
module four_bit_adder(A,B,C0,S,C4);
input[3:0]A;
input[3:0]B;
input C0;
output[3:0]S;
output C4;
wire C1,C2,C3;
full_adder fa0 (A[0],B[0],C0,S[0],C1);
full_adder fa1 (A[1],B[1],C1,S[1],C2);
full_adder fa2 (A[2],B[2],C2,S[2],C3);
full_adder fa3 (A[3],B[3],C3,S[3],C4);
endmodule
```

- four_bit_adder_test.v

```vhdl
module adder_test;
reg[3:0]A;
reg[3:0]B;
reg C0;
wire[3:0]S;
wire C4;
four_bit_adder fa (A,B,C0,S,C4);
initial
begin
A=4'b0011;B=4'b0011;C0=1'b0;
#10 A=4'b1011;B=4'b0111;C0=1'b1;
#10 A=4'b1111;B=4'b1111;C0=1'b1;
end
endmodule
```
