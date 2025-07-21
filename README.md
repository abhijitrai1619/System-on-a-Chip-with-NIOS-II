# FPGA Capstone Project – SoC Design with NIOS II

### Author: Abhijit Rai

**Institution:** Army Institute of Technology, Pune  
**Course:** CU Boulder FPGA Specialization (Coursera)  
**Project Name:** Embed  
**Board:** Terasic DE10-Lite (Intel MAX10 FPGA)  
**Date:** Dec 2024  

---

## Executive Summary

As my third hands-on FPGA project, I developed the hardware for a System on Chip (SoC) on the DE10-Lite board using the NIOS II soft processor. I used Qsys (Platform Designer) to integrate interfaces and compiled the design into a top-level HDL file. This project represents my entry into embedded SoC design, emphasizing system-level thinking, custom IP integration, and interrupt-based control logic.

---

## Project Overview

This project showcases the deployment of a NIOS II/f-based soft processor system on Intel's MAX10 FPGA. The complete embedded system was architected using Platform Designer (Qsys), synthesized in Quartus Prime, and tested using Eclipse SBT for real-time control and UART feedback.

The system was designed for reliable communication and peripheral integration, allowing full interaction with SPI-based sensors, modular ADC, and GPIO modules in a synchronized multi-clock environment.

---

## Learning Outcomes

- Design and integration of processor-based embedded systems using NIOS II/f  
- Creation of memory-mapped peripherals and interconnects via Avalon bus  
- Clock domain management using PLLs  
- Peripheral interface design (UART, SPI, ADC, GPIO)  
- Embedded software development using Eclipse and SBT  
- Timing analysis, resource optimization, and system debug  

---

## System Architecture

### Key IP Components

- **NIOS II/f Processor**  
- **On-Chip RAM / Flash Memory**  
- **External SDRAM Controller**  
- **Interval Timer (1ms tick)**  
- **SPI Interface for ADXL345 Accelerometer**  
- **Modular ADC**  
- **JTAG UART Console**  
- **System ID & Clock Crossing Bridges**  
- **GPIO for Switches and LEDs**

### Clock Configuration

| Clock Domain    | Frequency | Use Case                    |
|-----------------|-----------|-----------------------------|
| altpll_0.c0     | 80 MHz    | Core logic, RAM, SDRAM, SPI |
| altpll_0.c2     | 40 MHz    | UART, Timer, GPIO           |
| altpll_1.c0     | 10 MHz    | Modular ADC                 |

---

## Development Stack

| Tool/Component           | Description                         |
|--------------------------|-------------------------------------|
| Quartus Prime            | FPGA Design and Compilation (v16.1) |
| Platform Designer (Qsys) | IP integration and address mapping  |
| NIOS II SBT for Eclipse  | Firmware development in C           |
| ModelSim (optional)      | Functional simulation               |
| USB Blaster              | Programming interface (JTAG)        |

---

## Implementation Flow

1. **Project Setup:** Quartus project `Embed` initialized for MAX10 and DE10-Lite.  
2. **IP Configuration:** NIOS II, UART, SPI, ADC, GPIO, System ID, Timers integrated via Platform Designer.  
3. **Address & IRQ Mapping:** Managed via Avalon interconnect and Qsys auto-assignment.  
4. **Top-Level HDL Integration:** Qsys export instantiated in top-level Verilog.  
5. **Software Development:** Bare-metal C firmware developed in Eclipse.  
6. **Programming:** System `.sof` loaded to FPGA, `.elf` deployed via JTAG.  
7. **Testing & Debug:** UART used for I/O, real-time observation of LED and sensor response.  

---

## Embedded Application Features

- Real-time counter with variable step size  
- UART command interface (`u` = up, `d` = down, `3` = reset)  
- LED display control via GPIO  
- Optional bitwise inversion  
- Dynamic memory management via BSP  

---

## Directory Layout

| Path                | Description                           |
|---------------------|---------------------------------------|
| `Embed/`            | Quartus project root                  |
| `Embed_System/`     | Eclipse C source project              |
| `Embed_System_bsp/` | Board Support Package files           |
| `.sof`, `.elf`      | Configuration and executable binaries |
| `LabNotebook.pdf`   | Logs, metrics, test results           |

---

## Key Metrics

- **Fmax:** Extracted from post-fit Timing Analyzer  
- **Logic Elements Used:** Verified from Quartus Compilation Report  
- **Power Estimate:** Based on Quartus Power Analyzer (default switching)  
- **Peripheral Latency:** Estimated during UART/SPI interaction testing  

---

## Motivation

This project represents a pivot point in my embedded systems journey—from modular RTL design to a scalable SoC platform. My goal was to create a reliable and modular embedded system capable of adapting to increasingly complex I/O needs, while keeping latency low and documentation sharp.

The integration of memory, peripherals, and real-time logic through the NIOS II soft processor mirrors professional design workflows in the embedded world.

---

## Deployment Steps

1. Connect DE10-Lite to your PC via USB Blaster.  
2. Open Quartus and program the FPGA with `Embed.sof`.  
3. Launch Eclipse, import `Embed_System` and `Embed_System_bsp`.  
4. Build both BSP and application.  
5. Run `Embed_System.elf` using NIOS II Hardware configuration.  
6. Open UART terminal and test inputs (e.g., `u`, `d`, `3`).  

---

## References

- [Intel MAX 10 FPGA Handbook](https://www.intel.com/content/www/us/en/programmable/products/fpga/max-series/max-10/support.html)  
- [Platform Designer (Qsys) Guide](https://www.intel.com/content/dam/www/programmable/us/en/pdfs/literature/tt/tt_qsys_intro.pdf)  
- [Terasic DE10-Lite Board Manual](https://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&CategoryNo=165&No=1046)  

---

## Licensing & Attribution

This project was developed by **Abhijit Rai** under the academic framework of the **University of Colorado Boulder FPGA Specialization**. All components and source files were created independently. Any future adaptation should retain attribution.

> This isn’t just another lab submission—it’s a professionally structured dive into SoC design using FPGA technology. Because real engineers build from the ground up, and we document every line of it.
---
## Contact

**Abhijit Rai**  
Email: [abhijit.airosys@gmail.com](mailto:abhijit.airosys@gmail.com)  
---
