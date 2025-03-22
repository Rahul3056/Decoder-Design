 Decoder Design 

## **1. Theory & Explanation**  
A **decoder** is a combinational logic circuit that converts **n-bit binary input** into **one of 2ⁿ unique outputs**. It is commonly used for:  
- **Address Decoding** (activating memory locations based on address lines).  
- **Instruction Decoding** (CPU interprets machine instructions).  
- **Multiplexers & Demultiplexers** (used as selection circuits).  

### **Types of Decoders**  
1. **2-to-4 Decoder** → 2-bit input → 4 unique outputs.  
2. **3-to-8 Decoder** → 3-bit input → 8 unique outputs.  
3. **4-to-16 Decoder** → 4-bit input → 16 unique outputs.  

---

## **2. Truth Table (2-to-4 Decoder)**  

| A1 | A0 | Y3 | Y2 | Y1 | Y0 |  
|----|----|----|----|----|----|  
| 0  | 0  | 0  | 0  | 0  | 1  |  
| 0  | 1  | 0  | 0  | 1  | 0  |  
| 1  | 0  | 0  | 1  | 0  | 0  |  
| 1  | 1  | 1  | 0  | 0  | 0  |  

---

## **3. Boolean Expressions**  

For a **2-to-4 decoder**, the output expressions are:  

\[
Y_0 = \overline{A_1} \cdot \overline{A_0}
\]

\[
Y_1 = \overline{A_1} \cdot A_0
\]

\[
Y_2 = A_1 \cdot \overline{A_0}
\]

\[
Y_3 = A_1 \cdot A_0
\]

---

## **4. K-map Reduction (Optional for Larger Decoders)**  
For a **3-to-8 decoder**, K-map can simplify logic expressions for each output.

---

## **5. Verilog Code (2-to-4 Decoder)**  

```verilog
module decoder_2to4(
    input [1:0] A,
    input EN,
    output reg [3:0] Y
);
    always @(*) begin
        if (EN)
            case (A)
                2'b00: Y = 4'b0001;
                2'b01: Y = 4'b0010;
                2'b10: Y = 4'b0100;
                2'b11: Y = 4'b1000;
                default: Y = 4'b0000;
            endcase
        else
            Y = 4'b0000;
    end
endmodule
```

---

## **6. Testbench for Verification**  

```verilog
module tb_decoder_2to4();
    reg [1:0] A;
    reg EN;
    wire [3:0] Y;

    decoder_2to4 uut (.A(A), .EN(EN), .Y(Y));

    initial begin
        $monitor("A=%b, EN=%b -> Y=%b", A, EN, Y);
        
        EN = 1; A = 2'b00; #10;
        A = 2'b01; #10;
        A = 2'b10; #10;
        A = 2'b11; #10;
        
        EN = 0; A = 2'b10; #10;

        $finish;
    end
endmodule
```

---

## **7. SystemVerilog Assertions (SVA) & Coverage**  

### **Assertions for Checking Output Uniqueness**  
```systemverilog
property unique_output;
    @(posedge clk) (EN) |-> (Y inside {4'b0001, 4'b0010, 4'b0100, 4'b1000});
endproperty
assert property (unique_output);
```

### **Functional Coverage Example**  
```systemverilog
covergroup cg_decoder;
    option.per_instance = 1;
    A_cp: coverpoint A { bins all_vals[] = {[0:3]}; }
    EN_cp: coverpoint EN;
    cross A_cp, EN_cp;
endgroup
```

---

## **8. Practical Application Example**  
A **decoder is essential** in digital electronics. Some real-world applications include:  
- **CPU Instruction Decoders:** Converting binary opcodes into specific control signals.  
- **Memory Selection:** Selecting one out of many memory blocks based on an address.  
- **Seven-Segment Displays:** Decoders convert binary inputs to segment control signals for display output.  

---
