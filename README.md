### Decoder (2-to-4 and 3-to-8) - Theory, Design & Implementation  

### Concept Overview  
A **Decoder** is a combinational circuit that converts `n` input lines into `2^n` output lines. Decoders are widely used in memory addressing, demultiplexers, and instruction decoding in CPUs.

### Detailed Explanation  

#### ✅ 2-to-4 Decoder  
- **Definition:** A 2-to-4 decoder has 2 input lines (`A1`, `A0`) and 4 output lines (`Y0` to `Y3`). It activates exactly one output for each input combination.  
- **Boolean Expressions:**  
  - `Y0 = A1' A0'`  
  - `Y1 = A1' A0`  
  - `Y2 = A1 A0'`  
  - `Y3 = A1 A0`  

- **Truth Table:**  

| A1 | A0 | Y3 | Y2 | Y1 | Y0 |
|:--:|:--:|:--:|:--:|:--:|:--:|
|  0 |  0 |  0 |  0 |  0 |  1 |
|  0 |  1 |  0 |  0 |  1 |  0 |
|  1 |  0 |  0 |  1 |  0 |  0 |
|  1 |  1 |  1 |  0 |  0 |  0 |

**Example Application:** Used in **memory selection** to enable one memory block at a time.


#### ✅ 3-to-8 Decoder  
- **Definition:** A 3-to-8 decoder has 3 input lines (`A2`, `A1`, `A0`) and 8 output lines (`Y0` to `Y7`).  
- **Boolean Expressions:**  
  - `Y0 = A2' A1' A0'`  
  - `Y1 = A2' A1' A0`  
  - `Y2 = A2' A1 A0'`  
  - `Y3 = A2' A1 A0`  
  - `Y4 = A2 A1' A0'`  
  - `Y5 = A2 A1' A0`  
  - `Y6 = A2 A1 A0'`  
  - `Y7 = A2 A1 A0`  

- **Truth Table:**  

| A2 | A1 | A0 | Y7 | Y6 | Y5 | Y4 | Y3 | Y2 | Y1 | Y0 |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  1 |
|  0 |  0 |  1 |  0 |  0 |  0 |  0 |  0 |  0 |  1 |  0 |
|  0 |  1 |  0 |  0 |  0 |  0 |  0 |  0 |  1 |  0 |  0 |
|  0 |  1 |  1 |  0 |  0 |  0 |  0 |  1 |  0 |  0 |  0 |
|  1 |  0 |  0 |  0 |  0 |  0 |  1 |  0 |  0 |  0 |  0 |
|  1 |  0 |  1 |  0 |  0 |  1 |  0 |  0 |  0 |  0 |  0 |
|  1 |  1 |  0 |  0 |  1 |  0 |  0 |  0 |  0 |  0 |  0 |
|  1 |  1 |  1 |  1 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |

**Example Application:** Used in **instruction decoding** inside microprocessors.

### Code Explanation  
- **`assign` Statements:** Implements the logic equations for the decoder outputs.  
- **`$monitor` Task:** Displays real-time changes in decoder inputs and outputs.  
- **Test Cases:** Verifies both 2-to-4 and 3-to-8 decoders for all possible input combinations.  

---

### Execution Steps  
1. Copy the Verilog code into your simulator (e.g., **ModelSim, Xilinx Vivado**).  
2. Compile and run the code.  
3. Verify that the outputs match the expected **truth table values**.  

---

### Real-World Example for Practice  
- **Design a 4-to-16 Decoder** using two 3-to-8 decoders and an enable signal.  
