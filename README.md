# Performance Analysis of Low-Power Power-on-Reset Circuit using SKY130 PDK Technology

This repository presents an analysis and design of a low-power Power-on-Reset (POR) circuit using eSim, Ngspice and SKY130 PDK technology. 

**View the Report** - [Report](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/blob/master/Documentation/Low_Power_POR.pdf)

## Contents
- [Overview](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Overview)
- [Circuit Design](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Circuit-Design)
  - [Components](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Components)
  - [Implementation](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Implementation)
- [Block Diagram of the POR Circuit](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Block-Diagram-of-the-POR-Circuit)
- [Circuit Diagram of the POR Circuit](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Circuit-Diagram-of-the-POR-Circuit)
- [Specifications](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Specifications)
- [Power-On-Reset Circuit Parameters](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#Power-On-Reset-Circuit-Parameters)
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
- [References](https://github.com/Sree-Vishnu-Varthini/POR_SKY130/#References)
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

1. **Reference Current Generation:** Sub-threshold currents through specific NMOS transistors generate a stable reference current.
2. **Comparator:** The reference current is compared to a tracking current from VDD to determine the reset conditions.
3. **Inverter for Reset Signal:** Inverters generate a reset signal, ensuring correct reset operation during power fluctuations.

### Implementation
The proposed POR circuit uses a 10-transistor configuration, integrating components such as current mirrors and inverters to achieve effective low-power operation.

- **Current Mirrors:** Formed by PMOS and NMOS pairs to replicate reference currents.
- **Power Supply Voltage Tracking:** Monitored through an NMOS transistor directly connected to VDD.
- **Reset Signal (RSTN):** An inverter outputs the RSTN signal, activated during power-up and brown-out events, ensuring a reliable POR function.

This design was simulated using the open-source SKY130 PDK, eSim, and Ngspice for validation and analysis.

## Block Diagram of the POR Circuit

![POR](https://github.com/user-attachments/assets/6dcf29e8-cfd1-4052-92a9-fe41dd9619b3)


## Circuit Diagram of the POR Circuit

![Schematic](https://github.com/user-attachments/assets/9d6a220d-8df4-4255-a520-08497f27505f)

## Specifications

| Parameter                   | Value               |
|-----------------------------|---------------------|
| Technology                  | 130nm (SKY130 PDK  |
| Type                        | Current-Based      |
| Voltage                     | 0.5V               |
| VPOR(V)                     | 0.45               |
| TC (µV/ °C)                 |-25 to 227          |
| Static Power                | 32nW               |

## Power-On-Reset Circuit Parameters

| Parameter                    | Description                                      | Min  | Typical | Max | Unit   | Condition               |
|------------------------------|--------------------------------------------------|------|---------|-----|--------|-------------------------|
| **VDD**                      | Power-on-reset trip-voltage                      |   -  | 0.5     | -   | V      |   |
| **VPOR**                     | Power-on-reset trip-voltage                      | 0.45 | -       | -   | V      | 500 mV supply voltage   |
| **VBOD**                     | Brown-out detection trip-voltage                 | 0.439| -       | -   | V      | Room temperature        |
| **Temperature Coefficient of VPOR** | Sensitivity of trip-voltage to temperature changes | -    | 227     | -   | µV/°C | −40°C to 125°C, VDD = 0.5 V |
| **Temperature Coefficient of VBOD** | Sensitivity of trip-voltage to temperature changes | -    | 204     | -   | µV/°C | −40°C to 125°C, VDD = 0.5 V |
| **Quiescent Current**        | Current drawn at low supply voltage              | -    | 64      | -   | nA     | 0.5 V supply voltage    |
| **Static Power**             | Power consumption of the circuit                 | -    | 32      | -   | nW     | 0.5 V supply voltage    |



## Pre-Layout Performance Characteristics

### VDD vs. Time [0 ms - 30 ms] @ VDD = 0.5 V

![V(VDD)](https://github.com/user-attachments/assets/ea2f3464-f7b9-46b6-af21-070bc79e293c)



### V1 vs. Time [0 ms - 30 ms] @ VDD = 0.5 V


![V(V1)](https://github.com/user-attachments/assets/ecb89a6a-2f22-40fa-a94b-6f738c99078a)


### V2 vs. Time [0 ms - 30 ms] @ VDD = 0.5 V

![V(V2)](https://github.com/user-attachments/assets/8aba40d2-4d93-468d-9bb6-46d64980cbbc)



### RSTN vs. Time [0 ms - 30 ms] @ VDD = 0.5 V


![V(RSTN)](https://github.com/user-attachments/assets/93c3bf3c-90e2-4cce-9f3c-c09ab7d89d96)

### I(REF) vs. Time [0 ms - 30 ms] @ VDD = 0.5 V

![I(IREF)](https://github.com/user-attachments/assets/7b2a931b-b25a-4a60-96e9-a9803811f28f)


### I(NM1) vs. Time [0 ms - 30 ms] @ VDD = 0.5 V

![I(NM1)](https://github.com/user-attachments/assets/9e890c35-5457-4e97-9c41-a2463998192a)

### VDD vs. Time [0 ms - 30 ms] @ VDD = 1 V

![V(VDD)](https://github.com/user-attachments/assets/b7da2836-0fae-4dc4-a39c-e9d217a4253c)


### V1 vs. Time [0 ms - 30 ms] @ VDD = 1 V

![V(V1)](https://github.com/user-attachments/assets/aef76963-dd42-4d74-9033-5cb68b196aab)

### V2 vs. Time [0 ms - 30 ms] @ VDD = 1 V

![V(V2)](https://github.com/user-attachments/assets/3efd8d5a-2f68-4647-921c-6a43f6fd6898)


### RSTN vs. Time [0 ms - 30 ms] @ VDD = 1 V
![V(RSTN)](https://github.com/user-attachments/assets/185f648f-a538-4fa1-add5-172f129150bf)

### I(REF) vs. Time [0 ms - 30 ms] @ VDD = 1 V

![I(IREF)](https://github.com/user-attachments/assets/c5b5e7d9-f33b-48a9-998c-61ed7acb1c22)


### I(NM1) vs. Time [0 ms - 30 ms] @ VDD = 1 V

![I(NM1)](https://github.com/user-attachments/assets/6758e5d8-58f3-44da-b1d0-486b3a7338e7)

## Open Source Tools Used
### eSim

  - **eSim** (previously known as Oscad / FreeEDA) is a free/libre and open source EDA tool for circuit design, simulation, analysis and PCB design. It is an integrated tool built using free/libre and open source software such as KiCad, Ngspice and GHDL. eSim is released under GPL.
  - https://esim.fossee.in/home
  
### Ngspice

  - **Ngspice** is the open source spice simulator for electric and electronic circuits.
  - http://ngspice.sourceforge.net/

### SkyWater SKY130 PDK

  - The **SkyWater SKY130 PDK** is a collaboration between Google and SkyWater Technology Foundry to provide a fully open source Process Design Kit and related resources, which can be used to create manufacturable designs at SkyWater’s facility.
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

## References
[1] Xinxin Ren, xiaoyu hu, Shushan Qiao. "An Ultra-Low-Power Reconfigurable Power-On Reset for Multi-Supply Voltages Applications", Authorea, Jan. 2023.  

[2] H. You, J. Yuan, Z. Yu and S. Qiao, "An Accurate Low-Power Power on-Reset Circuit in 55-nm CMOS Technology," in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 69, no. 8, pp. 3361 3365, Aug. 2022.  

[3] H. -B. Le, X. -D. Do, S. -G. Lee and S. -T. Ryu, "A Long Reset-Time Power-On Reset Circuit With Brown-Out Detection Capability", in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 58, no. 11, pp. 778-782, Nov. 2011.

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
