# Digital-VLSI-SoC-Design-and-Planning
End-to-end physical design of a RISC-V SoC using the OpenLane flow on the open-source SKY130 PDK. This project covers the full RTL-to-GDSII process, culminating in a timing-clean, manufacturable GDSII layout. A showcase for the VSD SoC Design workshop.


# End-to-End Physical Design of a RISC-V SoC on SKY130 using OpenLane

**A Project Showcase for the "Digital VLSI SoC Design and Planning" Workshop**

**Gundrathi Vinod Kumar**

---

### **1. Project Synopsis**

This repository documents the successful **RTL-to-GDSII physical design implementation** of a RISC-V SoC, serving as a capstone project for the intensive "Digital VLSI SoC Design" workshop guided by the [VLSI System Design (VSD) team]( https://www.vlsisystemdesign.com/). Leveraging the **OpenLane** automated framework and the open-source **SkyWater 130nm PDK**, this work translates a complex RISC-V core from abstract Verilog into a tangible, manufacturable, and timing-clean GDSII layout. It showcases a mastery of the modern digital ASIC workflow and the engineering discipline required to meet aggressive Performance, Power, and Area (PPA) targets.

---

### **2. The Final Result: A Sign-off Clean GDSII**

The project culminated in a fully verified GDSII layout, successfully meeting all design specifications and passing a rigorous suite of industry-standard sign-off checks.

![[Final GDSII Layout]([path/to/your/final_layout_view.png)](https://github.com/gundrathivinodkumar2409/Digital-VLSI-SoC-Design-and-Planning/blob/9d5d3172b5df144f1b91e699017173092edde2a5/3.png))
***Figure 1: The final GDSII layout of the SoC, showcasing the successful integration of 18,508 standard cells and a complete power and clock network.***

| **Final Sign-off Metric**   | **Result**                          | **Status** |
| --------------------------- | ----------------------------------- | ---------- |
| **Technology Node**         | SkyWater 130nm                      | -          |
| **Target Clock Frequency**  | 83.33 MHz                           | Met        |
| **Setup Violations (WNS)**  | 0.00 ns                             | ✅ **Pass**    |
| **Hold Violations (WHS)**   | 0.00 ns                             | ✅ **Pass**    |
| **Design Rule Check (DRC)** | 0 Errors                            | ✅ **Pass**    |
| **Layout vs. Schematic (LVS)**| No Mismatches                       | ✅ **Pass**    |
| **Antenna Violations**      | 0 Errors                            | ✅ **Pass**    |
| **Total Die Area**          | 1,547,700 µm² (1.55 mm²)            | -          |
| **Standard Cell Count**     | 18,508                              | -          |

---

### **3. The Implementation Journey: From RTL to Physical Reality**

The physical design was executed using the structured, automated stages within the OpenLane flow. Each stage addresses a specific set of engineering challenges.

#### **Stage 1: Synthesis and Floorplanning**
*   **Synthesis:** The process began by translating the Verilog RTL into a gate-level netlist using **Yosys**, mapping the design to the SKY130 standard cell library based on a **Synopsys Design Constraints (SDC)** file.
*   **Floorplanning:** The physical hierarchy was then established. A floorplan was created defining the die area, core utilization, and I/O pad placement. A robust multi-layer Power Delivery Network (PDN) was synthesized to ensure stable power across the chip.

![Floorplan View](path/to/your/floorplan_view.png)
***Figure 2: The initialized floorplan, defining the chip's physical boundaries and power grid.***

#### **Stage 2: Placement and Clock Tree Synthesis**
*   **Placement:** The standard cells were intelligently placed onto the core's site rows. This critical step optimizes for timing and congestion, directly impacting the final performance and routability of the design.
*   **Clock Tree Synthesis (CTS):** A balanced clock tree was constructed to deliver the clock signal to all sequential elements with minimal skew, a fundamental requirement for a synchronous digital system.

[![Placement View](path/to/your/placement_view.png)
](https://github.com/manjeet-vk/Digital-VLSI-SoC-Design-and-Planning/blob/main/Day-2/Images/22.png)***Figure 3: The design post-placement, with all 18,508 standard cells legally positioned.***

#### **Stage 3: Routing and Final Integration**
*   **Routing:** All logical connections in the netlist were transformed into physical metal interconnects using a multi-stage global and detailed router. This step meticulously avoids shorts and opens while adhering to all design rules.
*   **GDSII Generation:** The final step integrated all physical data—cell placements, routes, and filler cells—into a single GDSII file, the industry-standard format for tape-out to a foundry.

---

### **4. A Glossary of the SoC Implementation Flow: Key Concepts and Their Significance**

This section demystifies the key terminology and crucial stages of the RTL-to-GDSII flow. The goal is to explain not just *what* each step is, but *why* it is a critical engineering challenge in the journey to creating a functional and manufacturable chip.

#### **Register-Transfer Level (RTL)**
*   **What It Is:** A high-level hardware description language (HDL) like Verilog is used to describe a digital circuit's behavior in terms of data flow between registers. It's the primary "source code" for a chip.
*   **Why It Matters:** RTL is the blueprint that captures the intended functionality of the SoC. A well-written, synthesizable RTL is the non-negotiable starting point for the entire physical design process.

#### **Standard Cell Library**
*   **What It Is:** The fundamental building blocks of a digital design, provided by the foundry (e.g., SKY130). Each cell is a pre-designed, pre-characterized physical layout of a basic logic function (e.g., AND, OR, NOT, Flip-Flop).
*   **Why It Matters:** The synthesis tool translates the abstract RTL into a netlist of these physical, real-world cells. The performance, power, and area of the chip are entirely dependent on the quality and characteristics of this library.

#### **Synopsys Design Constraints (SDC)**
*   **What It Is:** A text file that defines the timing goals for the design. It specifies the clock frequency, I/O delays, and other critical performance targets.
*   **Why It Matters:** The SDC is the **contract between the designer and the EDA tools**. Without it, the tools are just guessing. A well-defined SDC guides synthesis, placement, and routing to create a design that actually meets its target performance.

#### **Floorplanning**
*   **What It Is:** The process of creating the chip's blueprint. It involves defining the total die area, allocating space for the core logic, placing I/O pads, and designing the Power Delivery Network (PDN).
*   **Why It Matters:** A good floorplan is the foundation for a successful design. A poor floorplan can lead to unsolvable timing issues, routing congestion, or power integrity problems later in the flow.

#### **Clock Tree Synthesis (CTS)**
*   **What It Is:** The process of building a dedicated network of buffers and inverters to distribute the clock signal to every flip-flop on the chip.
*   **Why It Matters:** This is the "heartbeat" of the chip. The goal of CTS is to deliver the clock edge to all sequential elements at the same time (i.e., with minimal **skew**). A poor clock tree is one of the most common causes of timing failures.

#### **GDSII (Graphic Data System II)**
*   **What It Is:** The final output file of the physical design process. It's a binary database format that contains the exact geometric representation of every layer of the chip, ready to be sent to the foundry for manufacturing.
*   **Why It Matters:** This is the ultimate "tape-out" file. It is the final, unambiguous blueprint that the foundry will use to fabricate the physical silicon chip.

#### **Sign-off Verification**
This is the final "exam" for the design, a series of rigorous checks to guarantee correctness and manufacturability.

*   **Static Timing Analysis (STA):** Verifies that the design meets **Setup Time** (data must be stable *before* the clock edge) and **Hold Time** (data must be stable *after* the clock edge) for all paths. STA is the primary method for guaranteeing a chip will operate at its target frequency.

*   **Design Rule Check (DRC):** Ensures the layout adheres to hundreds of geometric rules specified by the foundry (e.g., minimum wire spacing, minimum width). These rules prevent physical manufacturing defects.

*   **Layout Versus Schematic (LVS):** An electrical check that compares the final layout's extracted netlist against the original, post-synthesis netlist. LVS provides the ultimate confirmation that the physical design is an exact electrical match to the logical design.

---

### **5. Core Competencies Developed**

*   **End-to-End Digital Implementation:** Gained practical, hands-on experience in executing the complete RTL-to-GDSII flow for a complex digital SoC.
*   **Automated PnR Flow Management:** Mastered the use of the OpenLane automated design flow, learning to configure, run, and debug the entire physical design process.
*   **Timing Closure Methodologies:** Developed a strong understanding of creating timing constraints (SDC) and analyzing STA reports to achieve a timing-clean design.
*   **Physical Design and Verification:** Acquired critical skills in floorplanning, power grid design, CTS, and performing sign-off quality checks like DRC and LVS.
*   **Open-Source EDA Proficiency:** Became adept at utilizing a powerful suite of open-source tools (Yosys, OpenROAD, Magic, Netgen) on a real-world, open-source PDK.

---

### **6. Technology Stack**

| Category                  | Tool / Technology         | Role in Project                                               |
| ------------------------- | ------------------------- | ------------------------------------------------------------- |
| **Automation Framework**  | OpenLane                  | Orchestrated the entire RTL-to-GDSII physical design flow.    |
| **Process Design Kit**    | SkyWater 130nm (SKY130)   | Provided the standard cell libraries, tech files, and DRC rules. |
| **Logic Synthesis**       | Yosys                     | Converted the Verilog RTL into a gate-level netlist.            |
| **Physical Implementation**| OpenROAD                  | The core engine for placement, CTS, and routing within OpenLane. |
| **Verification & Sign-off** | OpenSTA, Magic, Netgen    | Used for STA, DRC, and LVS checks to ensure design quality.     |

---

### **7. Conclusion**

This project was a rigorous and rewarding deep dive into the practical realities of modern SoC implementation. By successfully guiding a complex RISC-V core from RTL to a sign-off clean GDSII using the OpenLane flow, I have solidified a robust, practical skill set in physical design. The key takeaway is a profound understanding of the engineering discipline required to meet performance targets within the constraints of a given process technology. This workshop has equipped me to effectively contribute to real-world ASIC design challenges.

### **8. Acknowledgements**

I am sincerely grateful to the [VLSI System Design (VSD) team]( https://www.vlsisystemdesign.com/) for their exceptional mentorship. The structure and hands-on nature of this workshop were instrumental in my successful journey through the complex world of digital physical design.
