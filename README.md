
# Designing a Low Noise Amplifier (LNA) for the ISM Band (2.3 - 2.7GHz).

This project presents the design, simulation, and implementation of a **Low Noise Amplifier (LNA)** for RF applications. The LNA is optimized for **low noise figure (NF), high gain, and impedance matching** to ensure signal amplification with minimal distortion.



## Author

- Akkari Pranav Sai
- Email :- pranavsai.akkari.off@gmail.com
- LinkedIn :- https://www.linkedin.com/in/akkari-pranav-sai-256728218
- GitHub - https://github.com/pranavsai-3857


## 1.1 Introduction

This project describes the design of LNA for the Band (2.3 - 2.7GHz) using Keysight ADS software. However, the procedure specified here can be used to design for other frequency bands with slight modifications to specifications and parameters. The steps to deign the LNA are mentioned below.                

1. *Device Selection*      
2. *Obtain LNA Impedances* 
3. *Impedance Matching*
4. *Circuit Simulation*
5. *Results and Analysis*


## 1.2 LNA Introduction

A basic RF Radio system consists of a Receiver and a Transmitter chain, often sharing the same antenna with a Duplex switch isolating the both chains.  
  
The basic RF radio system contains a baseband processor, up-conversion Mixer, down-conversion Mixer, Voltage Controlled Oscillator (VCO), Local Oscillator (LO) or Frequency Generating Unit (FGU), pre-driver, driver, final Power Amplifier (PA), coupler, power controller, antenna switch, harmonic filter, antenna, pre-selector filter, Low Noise Amplifier (LNA) and post-selector filter. The image given below shows the same.
                
![Basic Radio RF Circuit](https://drive.google.com/uc?export=view&id=17PBgfntREjGrt9dVbVY1wouENjv4R34u)

The LNA is located in the Receiver chain. The signal received by the antenna would be directed to the receiver chain by the Duplex switch. The Pre-Selector Filter filters out the out of band frequencies, sending the filtered signal to LNA, which is responsible for amplifying the weak signals with addition of minimal noise.  Post-Selector Filter would further filter the received signal.  Then the signal is sent to Down Conversion Mixer, then to the Baseband Processor.  

The challenge while designing LNA  is to minimize noise introduced by LNA while obtaining appropriate gain and efficiency.


## 1.2.1 Implementation of LNA.


Although LNA could be implemented as Discrete or Integrated Circuit, each has its own advantages and dis-advantages. Two figures are attached below to show the advantages vs disadvantages for both Discrete and Integrated Circuit.


![Discrete LNA Adv vs Dis-Adv](https://drive.google.com/uc?export=view&id=1nuCjFHijKZY5wrKI4gFD-V9iV91tQXnL)


![IC LNA Adv vs Dis-Adv](https://drive.google.com/uc?export=view&id=1L8948t1AGQxj1V585apfNO7yB7ostcDE)


Though both could be used, we will proceed with the discrete implementation..
 

## 1.2.2 Cumulative Noise Figure (by Friis's Equation)

Noise Figure is an essential parameter that determines the receiver's sensitivity. Friis's Equation is used to calculate the total noise figure of a cascaded connection. We can also calculate Third Order Intercept Point (IP3) and Second Order Intercept Point(IP2), however we will limit our analysis to Noise Figure only. The formula for this is given in the image attached below.

 ![Friis's Equation](https://drive.google.com/uc?export=view&id=1QC5doOUdHKLxs4xnz5YFEGF7veOYhFz7)

 In the above equation, first term (F1) is the most significant contributor to the cumulative noise figure since it's not divided by the gain. Hence, it's essential to minimise this term.

 ## 1.2.3 Types of  Noise
 As we are dealing with LNA, it would be beneficial to discuss briefly about noise. It's the main obstacle in the receiver chain. 
 #### 1. Thermal Noise
 Thermal Noise (or Johnson–Nyquist noise) is unavoidable. It's generated due to random thermal motion of charge carriers inside a conductor, regardless of any applied voltage. It's approximately white till high frequencies (~1THz).The amplitude of the signal follows approximately Gaussian probability density function and the communication system affected by thermal noise is often modeled as an additive white Gaussian noise (AWGN) channel.
 #### 2. Shot Noise
 Shot noise arises when current flows through a semiconductor device or vacuum tube due to the random arrival of individual electrons at a junction. The RMS value of the shot noise current can be calculated using Shottky Formula. It can be observed in a mesoscopic resistor.
 #### 3. Flicker Noise
 Flicker Noise (or 1/f noise) is an electronic noise that occurs in low-frequency signals. It's predominant at lower frequencies(less than 1KHz). It can be caused due to trapping and de-trapping of charge carriers, impurities and imperfections in materials and Surface effects in MOSFETs.
 #### 4. Burst Noise   
  Burst Noise (or Popcorn Noise) is a sudden step-like transitions between two or more discrete voltage or current levels, as high as several hundred microvolts, at random and unpredictable times where each shift in offset voltage or current lasts for several milliseconds to seconds. It's caused due to defects and impurities in ICs, Manufacturing Imperfections, ageing of components and temperature changes.
#### 5. Partition Noise 

Partition Noise occurs when current divides into two or more paths. It occurs due to random fluctuations when dividing.


#### 6. Transit-time Noise 
Transit time noise  occurs in high-frequency semiconductor devices when the time taken by charge carriers to travel through the device becomes significant compared to the signal frequency. It increases with frequency and quickly dominates other noise sources. 

## 1.2.4 LNA parameters

###### 1. Pin_RF - Input power into the LNA.
###### 2. S(2,1) – Small Signal Gain of LNA.
###### 3. Noise Figure – Measures how much noise the LNA introduces into the system.
###### 4. S(1,1) - Input Return Loss.
###### 5. S(2,2) - Output Return Loss. Both S(1,1) & S(2,2) determines how good the impedance matching is done.
###### 6. S(1,2) – Reverse Isolation.
 
 ## 1.2.5 Stability 
 Issue of stability comes into picture when LNA oscillates similarly to an oscillator. Stability is checked in the design stage simulating Stability factors. Common Stability fixes are Collector and Base bypass capacitor, RC-feedback, Input resistive loading, Output resistive loading, and Emitter feedback resistor.

 ## 1.3 Device Selection
 Selection of right device is the most important step. This process has to be done based on the specifications of the LNA.
 ## 1.3.1 Design specifications
 To select the right device, we have to first state our desired design specifications. The frequency range of LNA is 2.3 - 2.7 GHz.The  remaining specifications are given below.

 ![Design Specifications](https://drive.google.com/uc?export=view&id=1ramcoyHzkkyBujvFl_npWTCcO1vv5tZ5)
 ## 1.3.2 Device Technology

 Selecting right material is also important. This depends on our working range, i.e Input Power and Frequency Range. Based on the data retrieved from the *Analog Devices* website, we can come to a conclusion. The graph is attached below.

 ![Device Technology](https://drive.google.com/uc?export=view&id=1hCvPL1BV4ZfaDhOr4daJ6LkU_hZD1PC9)

 Upon analysing the above graph and our specifications, we arrive at conclusion that SiGe devices suits our requirement. The right candidate is **BFU730F** manufactured by **NXP**. It's a SiGe Transistor.
 ## 1.3.3 Device Parameters
 The parameters of BFU730F can be extracted from the data sheet from manufacturer's website. Below is the data sheet of BFU730F.
 ![Data Sheet](https://www.nxp.com/docs/en/data-sheet/BFU730F.pdf)
 ![Quick Reference Data](https://drive.google.com/uc?export=view&id=1yQA1nPQj_4ypv3OS3-9gyTjbkPdj-xzo)

 ## 1.4 LNA Impedances
 We have to obtain the input and output impedances of the LNA. To calculate it, we can use the template of LNA impedance extraction in ADS. After studying various combinations, we finally arrived at one set that suits the best considering the design specifications. The result is  attached below. The matching is done for Noise Figure as it results in least Noise Figure and maximum gain.
 ![Input and Output Impedances](https://drive.google.com/uc?export=view&id=1h9oL9_55NkpNniXq42rjrpqNvgeOTASi)

 ## 1.5 Impedance Matching
  
Impedance Matching can be done using the Smith Chart utility.  The first
 step is to set the frequency to the center frequency of our band of interest and the characteristic
 impedance is set to 50 ohms. The next step is to insert the Q circle value. For our frequency band of interest, the
 calculated Q circle value is 8. Then LNA output impedance is matched to 50 ohms.
 ## 1.6 Circuit Simulation

 We arrive at our final step, simulating the circuit. Below attached one is the final schematic of the LNA circuit.

  ![Schematic of LNA](https://drive.google.com/uc?export=view&id=1AaXn02fP04Vcm9p2_ec3iFwGDYY5I0W3)

  Now we have to run few simulations to analyze our circuit, to check whether it's matching our Design Specifications.


  ## 1.7 Results 
  First, let us check the S-Parameter performance of our circuit. Our LNA met all the expectations, with Gain reaching above 20dB, Input Return Loss of 7.9dB and Output Return loss of 17.5 dB. 
   ![S-Parameter performance](https://drive.google.com/uc?export=view&id=1psEzOaJS4oUjITJJtalnpClrvu6S8nFi)
   Below attached is the curve depicting the stablity.
    
![Stability](https://drive.google.com/uc?export=view&id=1tW7w-Z3Nv1hgUGyhRkMogHRldu0ODUE4)

Next is the analysis of Noise Figure.
![Noise Figure](https://drive.google.com/uc?export=view&id=1c_CORadwLPzrFcv0OKYDTU-URfJXRKwc)

Finally we arrive at the measurement results of our circuit. Below is the circuit that states the values of all the parameters after analysing.

![Measurement Results](https://drive.google.com/uc?export=view&id=1ypjHUiTOMTOLZ16tX01JoUe8Me9-5g0O)

As far as circuit is concerned, we have met all the design goals set for the s-parameter, noise figure, and stability simulations.

We have finally designed the circuit of LNA using ADS software for the band 2.3 - 2.7 GHz.

## 1.8 Layout Design

Although we are not proceeding with Layout Designing, it's important to note few points while doing it. While designing it, one must be aware of *Parasitic Capacitance* and *Parasitic Inductance* that arises while using PCB.   

Parasitic Capacitance is caused due to the electric field created between two (or more) metal traces of the PCB.   

Parasitic Inductance is caused by the magnetic field present between two traces of the PCB.  

Layout Simulation and EM Circuit CO Simulation can be done on Keysight's ADS software.
