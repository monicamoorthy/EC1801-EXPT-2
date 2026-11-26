# EXPT 2 - Verification of Logic Gates
## SIMULATION AND VERIFICATION OF AND, OR, AND NOT GATES<br><br>
# Aim
To design, implement, and verify the functionality of basic AND, OR, and NOT logic gates using Verilog HDL, and verify the functionality using Synopsys VCS and DVE.<br><br>

# Software Required
•	Synopsys VCS<br>
•	Synopsys DVE<br>
•	Linux Terminal<br>
•	Verilog HDL<br><br>

# Boolean Function
The basic logic gates realize the following Boolean functions:<br><br>

•	AND: Y_AND = A . B<br>
•	OR: Y_OR = A + B<br>
•	NOT: Y_NOT = A'<br><br>

# Theory / Synopsis<br>
Logic gates are the basic building blocks of digital systems. NAND and NOR are universal gates. XOR produces 1 when its inputs differ, while XNOR produces 1 when its inputs are equal.<br><br>

# Files to be Created
File name	Purpose<br>
logic_gates.v	Logic-gate RTL<br>
logic_gates_tb.v	All input combinations and VCD generation<br><br>

 # Verilog  Program<br>
    // gedit basic_gates.v

    module basic_gates (
    input  wire a,
    input  wire b,
    output wire y_and,
    output wire y_or,
    output wire y_not
    );

    assign y_and = a & b;   // AND gate
    assign y_or  = a | b;   // OR gate
    assign y_not = ~a;      // NOT gate (inverter)

# **Test Bench Program**<br>
    reg a, b;
      wire y_and, y_or, y_not;

    // Instantiate the design under test (DUT)
    basic_gates uut (
        .a(a),
        .b(b),
        .y_and(y_and),
        .y_or(y_or),
        .y_not(y_not)
    );

    initial begin
        // ---- VCD dump setup ----
        $dumpfile("basic_gates.vcd");   // name of the VCD file to be generated
        $dumpvars(0, tb2);               // dump all signals in this testbench hierarchy

        // ---- Apply all 4 input combinations ----
        $monitor("Time=%0t a=%b b=%b | AND=%b OR=%b NOT(a)=%b", $time, a, b, y_and, y_or, y_not);

        a = 0; b = 0; #10;
        a = 0; b = 1; #10;
        a = 1; b = 0; #10;
        a = 1; b = 1; #10;

        #10 $finish;
   <br><br>

# Truth Table <br>
<img width="940" height="318" alt="image" src="https://github.com/user-attachments/assets/8a343bdb-ffb4-4aac-8b88-cf59eca374a8" />
<br><br>

# Simulation Procedure<br><br>
STEP 1 – Open Terminal<br>
Open a terminal in the experiment folder.<br>
bash<br><br>

STEP 2 – Load Synopsys Environment<br>
source /synopsys/start.sh<br><br>

STEP 3 – Compile Using VCS<br>
vcs logic_gates.v logic_gates_tb.v -full64<br>
If compilation is successful, VCS generates the simulation executable:<br>
simv<br><br>

STEP 4 – Run Simulation<br>
./simv<br>
The terminal displays the input combinations and corresponding output F.<br>
A VCD waveform file is also generated:<br>
exp1_boolean_min.vcd<br><br>

STEP 5 – Open DVE<br>
dve -full64<br>
Other option<br>
dve -full64 &<br>
A DVE environment will open.<br>
DVE Waveform Verification<br>
In DVE:<br>
Open the testbench hierarchy.<br>
Locate the signals: <br>
a<br>
b<br>
y_and<br>
y_or<br>
y_not<br>
Add the signals to the waveform window.<br>
Run/inspect the waveform.<br>
Verify that y_and = 1 only when a=1 AND b=1 — the single combination where both inputs are high.<br>
Verify that y_or = 1 whenever a=1 OR b=1 (any input high forces the output high).<br>
Verify that y_not is always the exact complement of a, regardless of b.<br>
The waveform should agree with the truth table.<br><br>

# Expected Result<br>
The basic logic gates — AND, OR, and NOT — were realized using Verilog HDL:<br>
Y_AND = A.B<br>
Y_OR = A+B<br>
Y_NOT = A'<br>
The design was compiled and simulated using Synopsys VCS, and the functionality was verified using DVE waveform analysis, matching the expected truth table.
Output<br><br>
# OUTPUT<br>

<img width="1832" height="1017" alt="Screenshot 2026-11-25 133633" src="https://github.com/user-attachments/assets/d6dd9db7-84a1-46d9-b92a-934370f3e0c1" />
<br><br>
 
# Viva-Voce Questions

•	What is a logic gate?

•	What are the basic logic gates in digital electronics?

•	What is the Boolean expression for an AND gate? An OR gate? A NOT gate?

•	Why is the NOT gate also called an inverter?

•	What is a universal gate, and how can NAND/NOR realize AND, OR, and NOT?

•	What is the purpose of a Verilog testbench?

•	Why is a VCD file generated?

•	What is the purpose of ./simv?

•	What is the purpose of DVE?

•	What is the difference between simulation and synthesis?

•	What is the difference between $dumpfile and $dumpvars?


