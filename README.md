# Performance Analysis of Low-Power Power-on-Reset Circuit using SKY130 PDK Technology

This repository presents an analysis and design of a low-power Power-on-Reset (POR) circuit using eSim, Ngspice and SKY130 PDK technology. 

## Contents
- [Overview](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Overview)
- [Circuit Design](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Circuit-Design)
  - [Components](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Components)
- [Block Diagram of the POR Circuit](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Block-Diagram-of-the-POR-Circuit)
- [Circuit Diagram of the POR Circuit](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Circuit-Diagram-of-the-POR-Circuit)
- [Power-On-Reset Circuit Parameters](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Power-On-Reset-Circuit-Parameters)
- [Implementation](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Implementation)
- [Pre-Layout Performance Characteristics](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Pre-Layout-Performance-Characteristics)
- [Open Source Tools Used](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Open-Source-Tools-Used)
  - [eSim](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#eSim)
  - [Ngspice](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Ngspice)
  - [Skywater SKY130 PDK](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Skywater-SKY130-PDK)
- [Installation of Tools](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Installation-of-Tools)
  - [Installation on Windows](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Installation-on-Windows)
  - [Installation on Ubuntu](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Installation-on-Ubuntu)
  - [Note](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Note)
- [Simulation of SKY130 Schematic in eSim on Windows](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Simulation-of-SKY130-Schematic-in-eSim-on-Windows)
- [Future Work](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Future-Work)
- [Resources](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Resources)
- [Contributors](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Contributors)
- [Acknowledgements](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Acknowledgements)
- [Contact Information](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Contact-Information)

## Overview
Power-On Reset (POR) circuits are commonly used in various electronic systems to ensure that components start up in a defined, predictable state. When an IoT device is first powered on, it needs a well-defined reset signal to ensure that all internal components start from a known state. POR circuits generate this reset signal, which is crucial for initializing the system reliably and avoiding potential issues like data corruption or unstable operation.

Traditional designs often consume significant power due to bandgap reference architectures. Here, we propose an alternative using a current reference and comparator architecture that reduces power overhead while enhancing performance and resilience against brown-out events.

## Circuit Design
Conventional Power-On Reset (POR) circuits tend to use more power due to their reliance on bandgap reference architectures, which draw current continuously to keep a stable reference voltage.

To address these challenges, we propose an alternative POR design that leverages a current reference and comparator-based architecture. This design reduces the overall power consumption of the POR circuit by eliminating the need for a bandgap reference, instead using a more efficient reference current. 

The comparator continuously monitors the supply voltage (VDD) and initiates a reset when VDD surpasses the predefined trip voltage (VPOR). This setup cuts down on power use and responds quickly and accurately during power-up.

This approach not only saves power but also improves resilience against voltage fluctuations, such as brown-out events, which could otherwise lead to unreliable operation.

### Components

1. Reference Current Generation: Sub-threshold currents through specific NMOS transistors generate a stable reference current.
2. Comparator: The reference current is compared to a tracking current from VDD to determine the reset conditions.
3. Inverter for Reset Signal: Inverters generate a reset signal, ensuring correct reset operation during power fluctuations.

## Block Diagram of the POR Circuit

![Block Diagram of the POR Circuit](https://github.com/user-attachments/assets/86eea463-e1f6-4365-99d7-504f0db5ec07)

## Circuit Diagram of the POR Circuit

![Schematic](https://github.com/user-attachments/assets/d1806c98-a36b-473a-b545-c94c71728e9b)

## Power-On-Reset Circuit Parameters

## Implementation
This POR circuit uses a 10-transistor configuration, integrating components like current mirrors and inverters for effective low-power operation.

- Current Mirrors: Formed by PMOS and NMOS pairs to replicate reference currents.
- Power Supply Voltage Tracking: Monitored through an NMOS transistor directly connected to VDD.
- Reset Signal (RSTN): An inverter outputs the RSTN signal, activated during power-up and brown-out events, ensuring a reliable POR function.

The design was simulated using the open-source SKY130 PDK, eSim and Ngspice.

## Pre-Layout Performance Characteristics

### VDD vs. Time [0ms - 30 ms] @ VDD = 1 V
![V(VDD)](https://github.com/user-attachments/assets/21433269-46d9-4c88-83d4-d742ddfa4650)

### V1 vs. Time [0ms - 30 ms] @ VDD = 1 V

![V(V1)](https://github.com/user-attachments/assets/5d051642-18f6-4eb7-806c-316a72ab3892)

### V2 vs. Time [0ms - 30 ms] @ VDD = 1 V

![V(V2)](https://github.com/user-attachments/assets/6d4c8da1-99b0-4a08-b073-52c487f525f5)

### RSTN vs. Time [0ms - 30 ms] @ VDD = 1 V

![V(RSTN)](https://github.com/user-attachments/assets/ba77da62-b9b0-4737-9a78-8a1cd30544ef)

### I(REF) vs. Time [0ms - 30 ms] @ VDD = 1 V

![I(IREF)](https://github.com/user-attachments/assets/3ce5938e-5ee4-4aa8-93d4-dc996359924e)

### I(NM1) vs. Time [0ms - 30 ms] @ VDD = 1 V

![I(NM1)](https://github.com/user-attachments/assets/b6c6598b-d170-45ef-9317-d849cb489e73)

### VDD vs. Time [0ms - 30 ms] @ VDD = 0.5 V

![V(VDD)](https://github.com/user-attachments/assets/0e55fec4-6d27-48a1-9b03-bede281b283f)

### V1 vs. Time [0ms - 30 ms] @ VDD = 0.5 V

![V(V1)](https://github.com/user-attachments/assets/c02c1629-8ad7-43e7-8470-76ce4a389cd6)

### V2 vs. Time [0ms - 30 ms] @ VDD = 0.5 V

![V(V2)](https://github.com/user-attachments/assets/0d8abe06-9128-44f8-b6d1-33d9244648f1)

### RSTN vs. Time [0ms - 30 ms] @ VDD = 0.5 V

![V(RSTN)](https://github.com/user-attachments/assets/21868042-80f4-4087-95db-18036fb907ff)

### I(REF) vs. Time [0ms - 30 ms] @ VDD = 0.5 V

![I(IREF)](https://github.com/user-attachments/assets/22299da5-f4cf-4a2e-9c5a-a20fd0e1d31d)

### I(NM1) vs. Time [0ms - 30 ms] @ VDD = 0.5 V

![I(NM1)](https://github.com/user-attachments/assets/b2b97ef6-a992-4ea5-9e93-8f1d84e2e4b4)

## Open Source Tools Used
### eSim

  - eSim (previously known as Oscad / FreeEDA) is a free/libre and open source EDA tool for circuit design, simulation, analysis and PCB design. It is an integrated tool built using free/libre and open source software such as KiCad, Ngspice and GHDL. eSim is released under GPL.
  - https://esim.fossee.in/home
  
### Ngspice

  - ngspice is the open source spice simulator for electric and electronic circuits.
  - http://ngspice.sourceforge.net/

### SkyWater SKY130 PDK

  - The SkyWater SKY130 PDK is a collaboration between Google and SkyWater Technology Foundry to provide a fully open source Process Design Kit and related resources, which can be used to create manufacturable designs at SkyWater’s facility.
  - https://github.com/google/skywater-pdk

## Installation of Tools
### Installation on Windows
1. Download the latest eSim release for Windows OS from the link: https://esim.fossee.in/downloads
2. Locate the installer file in the folder where your downloaded files are kept.
3. Double click on the file.
4. If a pop-up window appears asking ”Do you want to allow the following program from an unknown publisher to make changes to this computer?”, click YES.
5. Then in the ”License Agreement” window, select the I Agree option.
6. Click Next when the program asks for you to "Choose Install Location". Choose the auto-selected the destination folder path.
7. In the next window that appears, select Install.
8. A progress bar will appear; once it reaches 100%, "Installation Complete" message will be shown at the top of the eSim setup window. Click onClose. eSim shortcut icon will be on your Desktop.

### Installation on Ubuntu
1. Download eSim installer from http://esim.fossee.in/downloads to a local directory and unpack it.
2. You can also unpack the installer through the terminal. Open the terminal and navigate to the directory where the installer is located. Use the following command to unpack:
```bash
unzip eSim-2.4.zip
```
2. To install eSim and other dependencies run the following command:
```bash
$ cd eSim-2.4
$ chmod +x install-eSim.sh
$ ./install-eSim.sh --install
```
3. To run eSim from the terminal, type:
```bash
$ esim
```
or you can double click on eSim icon created on Desktop after installation.

### Note:

- eSim is available for Windows 8, 10, and 11 (64-bit).
- If you face issues with eSim-2.4, try using the more stable version eSim-2.3.
- eSim is also available for Ubuntu 18.04 and 20.04 LTS (including flavors).
- When eSim is installed on Windows, Ngspice and the SkyWater SKY130 PDK are also installed automatically.
- There is no need to install Ngspice or the Sky130 PDK separately on Windows as they are bundled with eSim.

## Simulation of SKY130 Schematic in eSim on Windows

1. Access the eSim SKY130 library by clicking on the Place Component button in the Right Toolbar and searching for the desired component in the Choose Component Dialog Box.
2. Alternatively, use predefined IPs made in SKY130 available in the eSim SKY130 Subckts library by searching for them in the same dialog box.
3. Ensure eSim is in SKY130 mode by selecting the SKY130mode option from the eSim SKY130 library.
4. When in SKY130 mode, use components with designators such as ‘sc’, ‘u’, ‘x’, ‘v’, ‘i’, and ‘a’ to avoid including unnecessary technology nodes.
5. Annotate your schematic and generate the netlist.
6. Click on the Convert KiCad to Ngspice button in the Left Toolbar to convert the schematic to a Ngspice-compatible format.
7. In the Analysis Tab, set all the simulation parameters and source details.
8. In the Device Modeling Tab, select options for the SKY130 PDK. Add the Default Path of the PDK installed with eSim by clicking on Add Default Path, or click Add and browse to a different SKY130 PDK path.
9. Add SPICE model parameters for each component in the provided text box in the Device Modeling Tab.
10. If using a SKY130 Subcircuit IP, go to the Subcircuits Tab, click Add, browse to the SKY130 folder, select the subcircuit, and click Open to add it.
11. Click Convert to complete the KiCad to Ngspice conversion. A dialog box will confirm the successful conversion.
12. If needed, manually edit the netlist by clicking on the Project Name.cir.out file in the left project panel.
13. Click the Simulate button in the Left Toolbar to run the simulation.
14. Following these steps will interface the SKY130 PDK with eSim, allowing simulations of designs using SKY130 technology.

## Future Work
- Design a variant of the circuit with more transistors (e.g., 14 or more) to support higher supply voltages while maintaining low power consumption.
- Explore the performance of the proposed circuit in smaller technology nodes to evaluate its scalability and effectiveness at lower power levels.
- Investigate improvements in brown-out detection accuracy and power consumption.
- Study the circuit's behavior under varying temperature conditions to ensure reliable operation in diverse environmental settings.

## Resources
- https://esim.fossee.in/
- https://esim.fossee.in/downloads
- https://static.fossee.in/esim/manuals/eSim_Manual_2.4.pdf
- https://static.fossee.in/esim/manuals/eSim_Manual_2.3.pdf
- https://ngspice.sourceforge.io/
- https://ngspice.sourceforge.io/docs/ngspice-42-manual.pdf
- https://github.com/google/skywater-pdk

## Contributors
- Sree Vishnu Varthini S, Pre-Final Year Student, Sri Eshwar College of Engineering.

## Acknowledgements
- Mr. Kunal Ghosh, Director, VSD Corp. Pvt. Ltd.
- Mr. Sumanto Kar, Assistant Project Manager, FOSSEE
- Dr. Maheswari Raja, Dean Innovations, Rajalakshmi Institute of Technology
- Mr. Saravanan M, Assistant Professor and Head of System On Chip - Center of Excellence, Sri Eshwar College of Engineering

## Contact Information
- Sree Vishnu Varthini S, Pre-Final Year Student, Sri Eshwar College of Engineering, sreevishnuvarthini@gmail.com
- Mr. Sumanto Kar, Assistant Project Manager, FOSSEE, sumantokar@iitb.ac.in
- Mr. Kunal Ghosh, Director, VSD Corp. Pvt. Ltd., kunalpghosh@gmail.com
- Dr. Maheswari Raja, Dean Innovations, Rajalakshmi Institute of Technology, maherajasadhana@gmail.com
- Mr. Saravanan M, Assistant Professor and Head of System On Chip - Center of Excellence, Sri Eshwar College of Engineering, saravanan.m@sece.ac.in
