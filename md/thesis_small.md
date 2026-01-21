## Control Design of HVDC Link with Virtual Synchronous Generator and Implementation on Real-Time Simulator



<div style="display:flex; flex-direction:column; gap:0.6rem;">
    <div class="project-tags" style="display:flex; align-items:center; gap:1rem;">
        <span class="timeline-meta" style="display:inline-flex; align-items:center; gap:0.5rem;">
            <svg viewBox="0 0 24 24" width="14" height="14" aria-hidden="true" style="opacity:1;">
                <rect x="3" y="4" width="18" height="18" rx="2"
                      fill="none" stroke="currentColor" stroke-width="1.5"/>
                <path d="M16 2v4M8 2v4M3 10h18"
                      fill="none" stroke="currentColor" stroke-width="1.5"/>
            </svg>
            October 7, 2025
        </span>
        <div style="zoom:0.8; display:flex; align-items:center; gap:0.5rem; transform: translateY(1px);">
            <span class="tag tag-safety">Matlab/simulink</span>
            <span class="tag tag-conference">typhoon hil</span>
            <span class="tag tag-arxiv">python</span>
            <span class="tag tag-workshop">PHIL</span>
        </div>
    </div>
    <div style="height:1.5px; width:100%; background: currentColor; opacity:0.15; margin-bottom: 0.5rem"></div>
   
</div>

The main inspiration for this project was a visit by <strong>Hitachi Energy</strong> to my University, where I studied.
The main goals of the project were:
- Current and voltage control of a three-phase inverter
- Implementation of virtual inertia technology (VSM)
- Investigation of **HVDC** interconnection using two virtual inertia technologies: **VSM** and **Synchronverter**
- Experimental validation through a one-of-a-kind **PHIL** setup
Part of this project was accepted and presented at the IEEE PES ISGT 2025 conference (read the full paper <a href="https://ieeexplore.ieee.org/document/11314231" target="_blank" class="cactus-link">here</a>).

<!-- <div class="md-h4">Hello</div> -->
<!-- <a class="cactus-link" href="https://link-url-here.org">IEEE PES ISGT 2025 conference</a> -->

<!-- ### Getting the idea -->
<div class="md-h4">Getting the Idea</div>
The primary objective of this project is to unify two virtual inertia technologies for the converter stations of an HVDC transmission system.<br> <br> 
<!-- <blockquote>HVDC transmission system</blockquote> -->
<img  style="width: 85%; height: auto; display: block; margin: 0 auto;" class = "filter-bnwsvg" alt="HVDC schematic" src="../assets/Both.svg"><br> 
Each station is connected to its respective grid via AC filters, while the DC sides are coupled through an HVDC link. This link creates a direct path for active power to flow between the grids, whenever frequency needs support.

<!-- ### Control Structure -->
<div class="md-h4">Control Structure</div>
In this setup, Grid 1 is interfaced via a Synchronverter (SV) and Grid 2 via a Virtual Synchronous Machine (VSM). On the AC side, both stations use **droop control** to keep the capacitor voltage steady near rated values.
 
<blockquote>Synchronverter</blockquote>
<img  style="width: 70%; height: auto; display: block; margin: 0 auto;" class = "filter-bnwsvg" alt="SV schematic" src="../assets/SV.svg">
 
The DC side management is splits: 
the **SV** handles the **Active Power** flowing through the HVDC link, 
while the **VSM** maintains the **DC bus voltage**.


<blockquote>Virtual Synchronous Machine</blockquote>
<img  style="width: 70%; height: auto; display: block; margin: 0 auto;" class = "filter-bnwsvg" alt="VSM schematic" src="../assets/VSM.svg">

Both controllers are driven by droop expressions that react dynamically to changes in each grid’s frequency.
<!-- <blockquote>VSM</blockquote> -->


<div class="md-h4">PHIL Experimental Setup</div>
The setup consists of two real-time digital simulators (**Typhoon HIL**). Each one is connected with a **programmable bi-directional power supply**, implementing the converter stations (SV & VSM). 

<div class="theme-image" alt="PHIL setup"></div>

The **HVDC line module** is used to connect the stations, in order to capture the dynamic responce of a real HVDC transmission line (160km, 100kV, 1000A).<br>
Real grid data are fed to the simulations in real-time, via a **smart grid meter**. 
Note that the **left power supply** operates as a **current source**, while the **right** one operates as a **voltage source**. Additionally, the left inverter (**SV**) operates as a **Voltage Source Converter**, whereas the right inverter (**VSM**) operates as a **Current Source Converter**. 
<!-- <div class="container" style = "display: block;">
    <img src="../assets/Phil_layer1.svg" style="position:relative; visibility:hidden; display: flex;">
    <img  src="../assets/Phil_layer2.svg">
    <img  class = "filter-imagesvg" src="../assets/Phil_layer1.svg">
</div> -->




<div class="md-h4">Results</div>
The reference value of active power is set to zero per unit, ensuring that when both grid frequencies are at 50 Hz, no power flow occurs. 
This operating point can be seen at around 60 seconds, where the system remains balanced and neither grid requires support. 

<div class="theme-results"></div>
The reference value of the DC-link voltage is set to one per unit. 
Whenever a grid requires support, the droop mechanisms, for active power and DC link voltage on the VSM side, are automatically activated to stabilize the system. 

<br> <br> 
<div class="md-h4">Read the full diploma thesis here:</div> 
Alternatively, you can download it from the official <a href="https://nemertes.library.upatras.gr/items/81c60c6a-3bd4-4f67-8ef5-f61a1edc67b2" target="_blank" class="cactus-link">University of Patras repository</a>.

