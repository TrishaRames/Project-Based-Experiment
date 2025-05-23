NAME:R.TRISHA
REGISTER NUMBER :212224100061
### Project-Based-Experiment

**AIM:**

To design and simulate the traffic light controller.

**SOFTWATE USED:**

Quartus II

**THEORY:**
	
     	Consider a controller for traffic at the intersection of three main roads.  

  ![image](https://github.com/naavaneetha/Project-Based-Experiment/assets/154305477/e3af03dd-a4de-4b21-af0a-a5a332a3e4b6)


 The traffic signal for all the three main roads have equal priority and they remain red by default.

 In state 00,the traffic signals remains red for first five counts and yellow of road1 turns on for the next four counts.

 In state 01, the green of road1 turns on for first five counts and yellow of road1 and road2 turns on for next four4 counts of this state.
 
 In state 10, the traffic signal of road1 comes back to the red and that of road2 goes to green for tee first five counts.For the next four counts the traffic signal of road2 and road3 remains yellow.


 In state 11, the traffic signal of road2 comes back to the red and that of road3 goes to green for the first five counts.For the next four counts the traffic signal of road3 turns to yellow

 At the end of four states,the traffic signal of all the three roads come back to red.

**Task Assigned**

From the HDL code given formulate the correct code  to divert the traffic to path 1 direction and disable the control in other directions (Assume user is at MR3 spot)

**Procedure**

1.	Type the program in Quartus software.
2.	Compile and run the program.
3.	Generate the RTL schematic and save the logic diagram.
4.	Create nodes for inputs and outputs to generate the timing diagram.
5.	For different input combinations generate the timing diagram
   
**Program:**
```

module sp1(
    input clk,
    output reg red1,
    output reg yellow1,
    output reg green1,
    output reg red2,
    output reg yellow2,
    output reg green2,
    output reg red3,
    output reg yellow3,
    output reg green3
);

// State machine definition
parameter S_IDLE = 2'b00;
parameter S_ROAD1 = 2'b01;
parameter S_ROAD2 = 2'b10;
parameter S_ROAD3 = 2'b11;

reg [1:0] state;
reg [3:0] count;

always @(posedge clk) begin
    // State transition
    case(state)
        S_IDLE: begin
            count <= count + 1;
            if (count == 5) begin
                state <= S_ROAD1;
                count <= 0;
            end
        end
        S_ROAD1: begin
            count <= count + 1;
            if (count == 5) begin
                state <= S_ROAD2;
                count <= 0;
            end
        end
        S_ROAD2: begin
            count <= count + 1;
            if (count == 5) begin
                state <= S_ROAD3;
                count <= 0;
            end
        end
        S_ROAD3: begin
            count <= count + 1;
            if (count == 5) begin
                state <= S_IDLE;
                count <= 0;
            end
        end
    endcase
end

// Traffic light control logic
always @(*) begin
    case(state)
        S_IDLE: begin
            red1 = 1;
            yellow1 = (count >= 1 && count <= 4) ? 1 : 0;
            green1 = 0;
            red2 = 1;
            yellow2 = 0;
            green2 = 0;
            red3 = 1;
            yellow3 = 0;
            green3 = 0;
        end
        S_ROAD1: begin
            red1 = 0;
            yellow1 = (count >= 6 && count <= 9) ? 1 : 0;
            green1 = (count >= 1 && count <= 5) ? 1 : 0;
            red2 = 1;
            yellow2 = (count >= 6 && count <= 9) ? 1 : 0;
            green2 = 0;
            red3 = 1;
            yellow3 = 0;
            green3 = 0;
        end
        S_ROAD2: begin
            red1 = 1;
            yellow1 = 0;
            green1 = 0;
            red2 = 0;
            yellow2 = (count >= 1 && count <= 4) ? 1 : 0;
            green2 = (count >= 6 && count <= 9) ? 1 : 0;
            red3 = 1;
            yellow3 = (count >= 6 && count <= 9) ? 1 : 0;
            green3 = 0;
        end
        S_ROAD3: begin
            red1 = 1;
            yellow1 = 0;
            green1 = 0;
            red2 = 1;
            yellow2 = 0;
            green2 = 0;
            red3 = 0;
            yellow3 = (count >= 1 && count <= 4) ? 1 : 0;
            green3 = (count >= 6 && count <= 9) ? 1 : 0;
        end
    endcase
end

endmodule

```
**RTL Schematic**

![Screenshot 2025-04-25 143642](https://github.com/user-attachments/assets/e6bc12a2-46b3-45fd-9214-ce1b411875db)

**Output Timing Waveform**

![Screenshot 2025-04-25 143819](https://github.com/user-attachments/assets/fd94fced-838f-4b76-9d9c-c831fcd432c7)

**Result:**

 simulate the traffic light controller.




