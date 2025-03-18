
<!--link rel="stylesheet" href="./custom.sibin.css"-->

# introduction

## autonomy

what is "_autonomy_"? 

we see various examples of it...

<img src="img/philippine_uav.png" height="100" width = "200" style="display: inline-block; margin-right: 10px;">
<img src="img/white_tesla.png" height="100" width = "200"  style="display: inline-block;">


### what are the _aspects_ of autonomy?

|||
|------------|-----------------------------------------------------------------------------|
| **perception** | how do you "_see_" the world around you? |
| **sensing**    | various ways to perceive the world around you (_e.g_, camera, LiDar)        |
| **compute**    | what do you "_do_" with the information about the world?                    |
| **motion**     | do your computations result in any "_physical_" changes?                    |
| **actuation**  | what "_actions_", if any, do you take for said physical changes?            |
| **planning**   | can you do some "_higher order_" thinking <br> (_i.e.,_ not just your immediate next move) |
 

## let us define **autonomy**

|||
|-----|------|
| Autonomy is the ability to <br> **perform given tasks** <br> based on the systems perception <br> <scb>without</scb> human intervention |  <img src="img/robot_profile_view.jpg" height="275"> |
||


## autonomous systems

|||||
|------|------|------|------|
|**cyber** | <img src="img/cps_software.png" width="275"> | <img src="img/cps_networking.png" height="275"> | <img src="img/cps_ecus.png" height="275"> |
|**physical** |  <img src="img/cps_sensors.png" height="275"> | <img src="img/cps_actuators.png" height="275"> | <img src="img/cps_plants.png" height="275"> |
||

hence, they fall under the class of systems &rarr; **cyber-physical** systems


## sensors and actuators...

|||
|-----|-----|
|<img src="img/cps_sensors.png" width="150" style="border: 2px solid purple; display: inline-block; padding: 10px; background-color:rgb(236, 219, 250);">| <img src="img/cps_actuators.png" width="125" style="border: 2px solid purple; display: inline-block; padding: 10px; background-color:rgb(236, 219, 250);">|
||

...are **everywhere**!

the **embedded** components &rarr; interactions with the real world

## sensing and actuation in the real world

consider the following example of two cars...
![Two cars, one behind the over, top view](img/cars_sensing/cars_sensing_1.png)

the second car is approaching the first
![Two cars, one behind the over, top view, an arror to the left on top of the car on the right](img/cars_sensing/cars_sensing_2.png)

**sensors** &rarr; constantly gathering data/sensing

<div class="multicolumn">
<div>
<ol>
 <li> periodic sensing </li>
</ol>
</div>
<div>
<img src="img/cars_sensing/cars_sensing_3.png" width="400">
</div>
</div>

on detection (of other car) &rarr; quickly **compute** what to do

<div class="multicolumn">
<div>
<ol>
 <li> periodic sensing </li>
 <li> computation </li>
</ol>
</div>
<div>
<img src="img/cars_sensing/cars_sensing_4.png" width="400">
</div>
</div>

take **physical action** (actuation) &rarr; say by braking _in time_

<div class="multicolumn">
<div>
<ol>
 <li> periodic sensing </li>
 <li> computation </li>
 <li> actuation </li>
</ol>
</div>
<div>
<img src="img/cars_sensing/cars_sensing_5.png" width="400">
</div>
</div>

<div class="multicolumn">
<div>
<ol>
 <li> periodic sensing </li>
 <li> computation </li>
 <li> actuation </li>
</ol>
</div>
<div>
<img src="img/sense_planning_actuation.png" width="400">
</div>
</div>

"**control**"

Remember this &rarr; on detection (of other car) &rarr; <scb>quickly</scb> **compute** what to do

<img src="img/cars_sensing/cars_sensing_4.png" width="400">

"quickly" compute &rarr; complete computation/actuation &rarr; before a **deadline**

This is a **real-time system**.


### Come back to **sensing**

<!--div class="multicolumn">
<div>
<br>
<ul>
    <li>we see <i>one</i> sensor (maybe LiDAR)</li>
    <li>reality &rarr; <b>multiple</b> sensors</li>
    <li>cameras, radars, lidar, etc.</li>
<ul>
</div>
<div>
<img src="img/autonomous_cars_sensors.png">
</div>
</div-->

Multiple sensors in an autonomous vehicle &rarr; need to _combine_ them somehow

**sensor fusion**

Once we have information from the sensors (fused or otherwise)...

<img src="img/kalman_statistical_view.png" width="400">

We need **state estimation** (**kalman** filter, **ekf**).

## Overview/Architecture of Autonomous Systems

So far, we have (briefly) talked about...

Sensing:

<img src="img/stack_architecture/stack_overview.2.png" width="200">

Actuation:

<img src="img/stack_architecture/stack_overview.3.png" width="200">

But the system includes...an **operating system** (OS) in there

<img src="img/stack_architecture/stack_overview.4.png" width="300">

and it includes **real-time** mechanisms.

We have briefly discussed, **EKF**:

<img src="img/stack_architecture/stack_overview.5.png" width="300">

**note**: ekf is versatile; can be used for sensor fusion, slam, etc.

All of it integrates with...**control**:

<img src="img/stack_architecture/stack_overview.6.png" width="300">

There are some **real-time** functions in there...

<img src="img/stack_architecture/stack_overview.7.png" width="300">

like _braking_, _engine control_.

Question: if we design such a system...

<img src="img/stack_architecture/stack_overview.7.png" width="300">

is it "**autonomous**"?

We are missing some "higher order" functionss from the perspective of the autonomous system:

- _where_ am I?
- _where_ do I need to go?
- _how_ do I get there?
- _what_ obstacles may I face?
- _how_ do I avoid them?


let us not forget the most important question of all...

<img src="img/drax_gamora.avif" width="400">

**why** is gamora?

### high-order functions

In order to answer the following, we need **additional functionality**. Let us go through what that might be.

|||
|-----|------|
| <ul><li>where am I?</li> <li>where do I need to go?</li> <li>how do I get there?</li> <li>what obstacles may I face?</li> <li>how do I avoid them?</li></ul> | <img src="img/stack_architecture/stack_overview.7.png" width="300">|
||



### slam

Simultaneous localization and mapping &rarr; figure out **where** we are.

<img src="img/stack_architecture/stack_overview.8.png" width="300">



### waypoint detection

Understand how to move in the _right_ direction at the **micro** level, _i.e.,_ find **waypoints**.

<img src="img/stack_architecture/stack_overview.9.png" width="300">



### yolo

Is it "you only live once"? Actually this stands for: "you only **look** once". It is an object **detection** model that uses convolutional neural networks (cnns)

<img src="img/stack_architecture/stack_overview.10.png" width="300">



### object avoidance

The objective is to avoid objects in the **immediate path**.

<img src="img/stack_architecture/stack_overview.11.png" width="300">



### path planning

i.e., how to get to **destination** at the **macro** level &rarr; uses waypoints.

<img src="img/stack_architecture/stack_overview.12.png" width="300">



### compute platform

To run all of these functions, we need low power, embedded platforms.

<img src="img/stack_architecture/stack_overview.13.png" width="300">


### still some **non-functional** requirements remain

any guesses what they could be?

### safety!

Essentially safety of &rarr; operator, other people, the vehicle, environment This is **cross-cutting** issue &rarr; affected <scb>by</scb> **all** parts of system.

<img src="img/stack_architecture/stack_overview.14.png" width="300">



### security

Security is another cross-cutting issue &rarr; <scb>can affect</scb> **all** components.

<img src="img/stack_architecture/stack_overview.png" width="300">

### Course Structure

Hence this figure is a (loose) map of this course:

<img src="img/stack_architecture/stack_overview.png" width="300">
<!--link rel="stylesheet" href="./custom.sibin.css"-->


# Embedded Architectures

Just like "autonomy" describing and "embedded system" is hard. What (typically) distinguishes it from other types of computer systems (e.g., laptops, servers or GPUs even) is that such systems are typically created for _specific_ functionality and often remain fixed and operational for years, decades even.

Embedded systems often trade off between performance and other considerations such as power (or battery life), less memory, fewer peripherals, limited applications, smaller operating system (OS) and so on. There are numerous reasons for this -- chief among them is _predictability_ -- designers need to guarantee that the system works correctly, and remains safe, all the time. Hence, it must be easy to _certify_ [^1] the _entire_ system. This process ensures that the system operates **safely**.

## The **wcet** problem

One piece of information that is required to ensure predictability and guarentee safety is **[worst-case execution time](https://www.cs.fsu.edu/~whalley/papers/tecs07.pdf)** (WCET). The WCET/BCET is the **longest**/shortest execution time possible for a program, **on a specific hardware platform** -- and it has to consider _all possible inputs_. WCET is necessary to ensure the "schedulability", resource requirements and performance limits of embedded and real-time programs. There are lots of approaches to computing the WCET, _e.g.,_

- [dynamic/empirical](https://www.cs.fsu.edu/~whalley/papers/tecs07.pdf) analysis &rarr; run the program lots of times (thousands, millions?) on the platform and measure it
- [static](https://www.cs.fsu.edu/~whalley/papers/tecs07.pdf) analysis &rarr; analyze the program at _compile time_ to compute the _worst-case paths_ through the program
- [hybrid](https://sibin.github.io/papers/2008\_NCSU-Dissertation_CheckerMode_SibinMohan.pdf) &rarr; a combination of the two
- [probabilistic](https://people.ac.upc.edu/fcazorla/articles/jabella_ecrts2014_2.pdf) &rarr; a combination of dynamic analysis+statistical methods
- [ML-based methods](https://dl.acm.org/doi/10.1145/3570361.3615740) &rarr; applying machine-learning to the problem

At a high-level, the execution time distributions of applications look like:

<img src="./img/embedded_arch/wcet_wilhelm.png" width="400" style="display: inline-block;" title="https://www.inf.ed.ac.uk/teaching/courses/es/PDFs/lecture_11.pdf" />

WCET analysis is a very active area of research and hundreds of papers have been written about it, since it directly affects the safety of many critical systems (aircraft, power systems, nuclear reactors, space vehicles and...autonomous systems). 

There are structural challenges (both in software and hardware) that prevent the computation of _proper_ wcet for anything but trivial examples. For instance, consider,

```c
void main()
{
    int max = 10 ;
    int sum = 0;
    for( int i = 0 ; i < max ; ++i)
        sum += i ;
}
```

How do you compute the WCET for this code? Say running on some known processor, P?

Well, there's some information we need, 

- how long each instruction takes to execute on P
- how many loop iterations?
- what is the startup/cleanup times for the program on P?

Let's assume (from the manual for P), we get the following information,

```c
1   void main()         // startup cost = 100 cycles
2   {
3       int max = 15 ;  // 10 cycles
4       int sum = 0;    // 10 cycles 
5       for( int i = 0 ; i < max ; ++i) // 5 cycles, once
6            sum += i ; // 20 cycles each iteration
7   }                   // cleanup cost = 120 cycles
```

So, based on this, we can calculate the total time to execute this program:

$$
wcet = startup\_cost + line\_3 + line\_4 + loop\_startup\_cost + ( line\_6 * max) \quad [1] 
$$

$$
wcet = 100 + 10 + 10 + 5 + (20 * 15) 
$$

$$
wcet = 425\ cycles
$$

Now consider this slight change to the above code:
```c
void main( int argc, char* argv[] )
{
    int max = atoi( argv[1] ) ;     // convert the command line arg to max
    int sum = 0; 
    for( int i = 0 ; i < max ; ++i) // how many iterations?
        sum += i ;
}
```

The problem is that equation [1] above fails since we no longer know the value of `max`. Hence the _program can run for any arbitrary amount of time, depending on the given input!_ Note that **none** of the aforemention wcet methods will help in this case since the input can be completely arbitrary. Hence, the structure of the software code can affect wcet calculations.

Another problem is that of **hardware** (and interactions between hardware and software). Now consider if we modify the original code as,
```c

#define VERY_LARGE_ARRAY+SIZE 1>>18

void main()
{
    int first_array[VERY_LARGE_ARRAY_SIZE] ;
    int second_array[VERY_LARGE_ARRAY_SIZE] ;

    int sum_first = 0;
    int sum_second = 0;
    for( int i = 0 ; i < VERY_LARGE_ARRAY_SIZE * 2 ; ++i)
    {
        if( i%2 )
            first_sum += first_array[i/2] ;
        else
            second_sum += second_array[(int)((i/2)+1)] ;
    }
}
```

Now, while we can compute, using equation [1] the wcet from the code perspective (since we know the loop runs for `VERY_LARGE_ARRAY_SIZE * 2` iterations), there will be significant non-obvious hardware issues, in the **cache**. Each iteration is accessing a _different_ large array. Hence, it will load the cache with lines from that array and in the _very next iteration_ the other array will be loaded, also missing in the cache. For instance, 

| iteration | operation | cache state | reason |
|----------------|----------------------------|-------------------|---------------------------------------------|
| 1 | `first_array` loaded | miss | evicts whatever was previously in cache |
| 2 | `second_array` loaded | miss | **evicts `first_array`** due to lack of space |
| 3 | `first_array` loaded again | miss | **evicts `second_array`** due to lack of space |
|...|
||

Hence, this program will _constantly_ sufffer cache misses and since caches misses (and reloads) are expensive (in terms of time), the loop's execution time will balloon out of control! Hence, even though we fixed the code issue (upper bound on number of iterations, hardware artifacts can change the wcet calculations). So now, we need to _model cache behavior_ for each program and data variable! This is [notoriously complicated](https://user.it.uu.se/~wangyi/pdf-files/2015/lgyrw-acm15.pdf) even for the simplest of programs. 

Other hardware designs further complicate matters, e.g., 

- processor pipelining
- prefetching
- branch prediction
- multithreading
- multicore systems
- memory buses
- networks-on-chip
- and too many others to recount here...

Any contemporary processor design that improves  performance, *turns out to be bad for wcet analysis*. So, the fewer (or simpler versions of) these features, the better it is for the (eventual) safety and certification of the system. 

This is one of the main reasons why embedded (and especially real-time) systems **prefer simpler processors** (simple pipelines, fewer complex features, simpler memory/cache architectures, if any) since they're easier to analyze. In fact, many critical systems (e.g., aircraft, cars, etc.) **use older processors** (often designed in the 1980s and 1990s) -- even the ones beind design today! 



## Embedded Processors

Just as embedded systems are varied, embedded processors come in a myriad of shapes and sizes as well. From the very small and simple (e.g., DSPs) to the very large and complex (modern multicore chips, some with GPUs!). Here is a (non-exhaustive) list of the types of embedded processors/architectures in use today:

1. [Microcontrollers](#microcontrollers)
2. [Digital Signal Processors](#digital-signal-processors-dsps) (DSPs)
3. [Microprocessors](#microprocessors) of various designs and architectures (e.g., ARM, x86)
4. [System-on-a-Chip](#system-on-a-chip-soc) (SoC)
5. [Embedded accelerators](#embedded-accelarators-eg-gpu-enabled-systems)
6. [ASICs and FPGAs](#asics-and-fpgas)


### Microcontrollers

According to [Wikipedia](https://en.wikipedia.org/wiki/Microcontroller),

>   "A microcontroller (MC, UC, or μC) or microcontroller unit (MCU) is a small computer on a single integrated circuit."

These may be among the most common type of "processors" used in embedded systems. According to many studies, **[more than 55%](https://www.embedded.com/the-two-percent-solution/)** of the world's processors are microntrollers! Microcontrollers are typically used in small, yet critical, systems such as car engine control, implantable medical devices, thermal monitoring, [fault detection and classification](https://sibin.github.io/papers/2021_BuildSys_PIRMedic_AshishKashinath.pdf) among millions of other applications. 

Microcontrollers hardware features typically include,

| component | details |
|-----------|---------|
| one (sometimes more) CPU cores | typically simple `4` or `8` bit chips |
| small pipelined architectues | sometimes `2` or `4` stage pipelines |
| some limited memory | typically a few hundred kilobytes, perhaps in the form of EEPROMs or FLASH |
| some programmable I/O | to interact with the real world |
| low operating frequencies | e.g., `4 KHz`; simpler/older processors, yet more predictable |
| low power consumption | in the **milliwatts** or **microwatts** ranges; might even be **nanowatts** when the system is _sleeping_ |
| interrupts (some programmable) | often _real-time_ (ficed/low latency) |
| several general-purpose I/O (GPIO) pins | for I/O |
| timers | e.g., a programmable interval timer (PIT) |
||

<br>

There are some **additional features** found on some microcontrollers, viz.,

| component | details |
|-----------|---------|
| analog to digital (ADC) signal convertors | to convert incoming (real-world, sensor) data to a digital form that the uC can operate on |
| digital-to-analog (DAC) convertor | to do the opposite, convert from digital to analog signals to send outputs in that form |
| universal asynchronous transmitter/receiver (UART) | to receive/send data over a _serial_ line |
| pulse width modulation (PWM) | so that the CPU can control **motors** (significant for us in autonomous/automotive systems), power systems, resistive loads, etc. |
| JTAG interace | debugging interface |
||

<br>

Some examples of popular microcontroller families:

|||||
|----|----|----|----|
|<img src="./img/embedded_arch/ATmega169-MLF.jpg" height="100"><br>Atmel ATmega | <img src="./img/embedded_arch/Microchip_PIC24HJ32GP202.jpg" height="100"> <br> Microchip Technology | <img src="./img/embedded_arch/Motorola_68HC11.jpg" height="100"> <br> Motorola (Freescale) | <img src="./img/embedded_arch/NXP_LPC2387FBD100-5543.jpg" height="100"> <br> NXP |
||

Microcontroller programs and data,

- are small --> must fit in memory (since very little expandable memory exists)
- often directly programmed in **assembly**!
    - sometimes the assembly code might need _hand tuning_ --> for both, performance as well as fitting into the limited memory
- **C** is another popular language
- **no operating systems** (or very rare)!
- sometimes have their own special-purpose programming languages or instructions

### Digital Signal Processors (DSPs)

DSPs are specialized microcontrollers optimized for _digital signal processing_. They find wide use in audio processing, radar and sonar, speech recognition systems, image processing, satellites, telecommunications, mobile phones, televisions, etc. Their main goals are to isoloate, measure, compress and filter _analog_ signals in the real world. They often have **stringent real-time constraints**. 

The Texas Instruments DSP chip, [TMS320 Series](https://www.ti.com/lit/ug/spruh79c/spruh79c.pdf?ts=1736945981001) is one of the most famous example of this type of system:

<img src="./img/embedded_arch/TI_DSP.jpg" height="100" title="Texas Instruments DSP Chip">

Typical digital signal processing (of any kind) requires repetitive mathematical operations over a large number of samples, in real-time, viz., 
- analog to digital conversion
- maniupulation (the core algorithm)
- digital to analog conversion

Often, the _entire_ process must be completed with low latency, even within a fixed deadline. They also have **low power** requirements since DSPs are often used in battery-constrained devices such as mobile phones. Hence, the proliferation of specialized DSP chips (instead of pure [software implementations](https://liquidsdr.org), which also exist; MATLAB has an entire [DSP System Toolbox](https://www.mathworks.com/help/dsp/index.html)).

**Typical DSP architecture**/flow (credit: [Wikipedia](https://en.wikipedia.org/wiki/Digital_signal_processor)):

<img src="./img/embedded_arch/dsp_architecture.png" height="100" title="https://en.wikipedia.org/wiki/Digital_signal_processor">

These types of chips typically have custom instructions for optimizing certain (mathematical) operations (apart from the typical `add`, `subtract`, `multiply` and `divide`), e.g., 
- `saturate`; caps the minimum or maximum value that can be held in a fixed-point representation
- `ed` ; euclidian distance
- `accumulate` instructions ; for [_multiply-and-accumulate_](https://skills.microchip.com/dsp-features-of-the-microchip-dspic-dsc/693207) operations, i.e., $a \leftarrow a + (b * c )$

> See the [Microchip instruction set](https://ww1.microchip.com/downloads/en/DeviceDoc/sect2.pdf) details for more information for a typical DSP ISA.

DSPs require _optimization of streaming data_ and hence,
- require **optimized memories and caches** &rarr; fetch multiple data elements at the same time
- code may need to be aware of, and **explicitly** manipulate caches
- may have rudimentary OS but **no virtual memory**


### Microprocessors

Microprocessors are, then, **general-purpose** chips (as opposed to microcontrollers and DSPs) that are also used extensively in embedded systems. They are used in systems that need more heavy duty computing/memory and/or more flexibility in terms of programming and management of the system. They use a number of commodity processor architectures (e.g,, ARM, Intel x86). 

Main features of microprocessors:

| component | details |
|-----------|---------|
| cores | single or multicore; powerful |
| pipelines | more complex pipelines; better performance, harder to analyze (e.g., wcet) |
| clock speeds | higher clock speeds; `100s` of khz, or even GHz |
| ISA | common ISA; well understood, not custom |
| memory | significant memory; megabytes, even gigabytes |
| cache hierarchies | multiple levels, optimized |
| power consumption | much higher, but can be reduced (e.g., via [voltage and frequency scaling](https://developer.arm.com/documentation/ddi0375/a/functional-overview/intelligent-energy-management--iem-/dynamic-voltage-scaling--dvs-)) |
| size, cost | often higher |
| interrupts, timers | more varied, easily programmable |
| I/O | more interfaces, including commodity ones like USB |
| security | often includes additional hardware security features, e.g., [ARM TrustZone](https://sefcom.asu.edu/publications/trustzone-explained-cic2016.pdf).
||

The [ARM M-85](https://armkeil.blob.core.windows.net/developer/Files/pdf/product-brief/arm-cortex-m85-product-brief.pdf) Embedded Microprocessor architecture:

<img src="./img/embedded_arch/arm_cortex_m85.png" width="300" title="Arm M-85">

When compared to microcontrollers (or even SoCs), most microprpcessors **do not** include components such as DSPs, ADCs, DACs, etc. It is possible to _augment_ the microprocessor to include this functionality &rarr; usually by _connecting one or more microcontrollers to it_!

On the software side, microprocessors typically have the **most flexibility**:

- general purpose operating systems (e.g., Linux, Android, Windows, UNIX, etc.)
- most programming languages and infrastructures (even [Docker](https://www.docker.com/blog/getting-started-with-docker-for-arm-on-linux/)!)
- large number of tooling, analysis, debugging capabilities
- complex code can run, but **increases analysis difficulty**

Due to their power (and cost) these types of systems are only used when really necessary or in higher-end systems such as mobile phones and autonomous cars. 


### System-on-a-Chip (SoC)

An SoC **integrates** most components in and around a processor into a **single** circuit, viz.,

- processor/chip &rarr; could be a microcontroller or even a microprocessor
- memory and memory interfaces
- I/O devices
- buses (memory and I/O)
- storage (e.g., flash) and sometimes even secondary storage
- radio modems
- (sometimes) accelerators such as GPUs

All of these are placed on a **single substrate**. 

SoCs are often designed in `C++`, `MATLAB`, `SystemC`, etc. Once the hardware architectures are defined, additional hardware elements are written in hardware description languages, e.g., register transfer levels (`RTL`) [^2]. 

Additional components could include,

- DAC
- ADC
- radio and signal processing
- wireless modems
- [_programmable logic_](https://www.amd.com/en/products/adaptive-socs-and-fpgas/soc/zynq-7000.html). 
- networks on chip (NoC) [^3]

In some sense, an SoC is an _integration of a processor with peripherals_. New hardware elements

Some examples of modern SoCs:

<div class="multicolumn">
<div>
<img src="./img/embedded_arch/broadcom_pi_chip.png" width="200" title="Broadcom SoC chip used in the Raspberry Pi">

Broadcom Soc from Raspberry Pi
</div>
<div>
<img src="./img/embedded_arch/Apple_M1.jpg" width="200" title="Apple M1 SoC">

Apple M1 SoC
</div>
</div>

The integration of all hardware components has some interesting side-effects:

| effect | benefit | problems |
|----------|---------|----------|
| tight integration | better performance, fewer latencies | cannot replace individual components |
| custom code/firmware | better use of hardware | not reusable in other systems |
| custom software libraries | easier programming of SoC | reduces code reusability in other systems |
| low power consumption | better battery life, less heat | (potentially) slower |


Depending on the processor/microcontroller that sits at the center of the SoC, the software stack/capabilities can vary. Many commons SoCs exhibit the following software properties:

- usually use contemporary operating systems, though optimized for embedded/SoC systems &rarr; e.g., [Raspbian](http://www.raspbian.org) aka Rasberry Pi OS. Hence, they can handle multiprocessing, virtual memory, different scheduling policies, etc. 
- can be programmed using most common programming languages &rarr; `C`, `C++`, `python`, `java`, even [`lisp`](https://medium.com/@kenichisasagawa/rediscovering-the-joy-of-hardware-hacking-with-raspberry-pi-and-lisp-574c833ab20e)!

The Raspberry Pi is a common example of a system that uses a [Broadcom BCM series of SoCs](https://www.raspberrypi.com/documentation/computers/processors.html). We use the [BCM2711](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2711) SoC in our course for the Raspberry Pi 4-B.


### Embedded Accelarators (e.g. GPU-enabled systems)

There are hardware platforms that include **accelerators** in embedded systems, e.g., [GPUs](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/), [AI-enabled silicon](https://www.nature.com/articles/s41928-022-00778-y), [extra programmable FPGA fabric](https://www.amd.com/en/products/adaptive-socs-and-fpgas/soc/zynq-7000.html), [security features](https://developer.arm.com/documentation/100230/0002/functional-description/external-coprocessors/configuring-which-coprocessors-are-included-in-secure-and-non-secure-states), etc. The main idea is that certain computation can be _offloaded_ to these accelerators while the main CPU continues to process other code/requests. The accelerators are specialized for certain computations (e.g., parallel matrix multiplications on GPUs, AES encryption). Some chips include FPGA fabric where the designer/user can _implement their own custom logic/accelerators_. 

In a loose sense, the [Navio2](https://navio2.hipi.io) can be considered as a hardware coprocessor for the Raspbery Pi.

The [NVidia Jetson Orin](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-orin/) is a good example of an AI/GPU focussed embedded processor:

<img src="./img/embedded_arch/jetson-agx-orin-4c25-d-2x.png" width="300" title="NVIDIA Jetson AGX Orin 64 GB">

<br>

This system's [specifications](https://www.techpowerup.com/gpu-specs/jetson-agx-orin-64-gb.c4085):

- 1300 MHz clock speeds
- 64 GB Memory
- 256 bit memory bus
- 204 GB/s bandwidth
- supports a variety of graphics features (DirectX, OpenGL, OpenCL, CUDA, Vulkan and Shader Models )
- maximum of 60W power
- **275 trillion** operations/s (TOPS)!

These systems are finding a lot of use in autonomous systems since they pack so much processing power into such a small form factor


### ASICs and FPGAs

Application-specific integrated circuits (ASICs) and field programmable gate arrays (FPGAs). These platforms combine the advantages of both, hardware (_speed_) and software (_flexibility/programmability_). They are similar, yet different. Both are semiconductor devices that include **programmable logic gates** but an ASIC is _static_ -- i.e., once the board has been "programmed" it cannot be changed while an FPGA, as the name implies, allows for "reprogramming". 

ASICs are **custom-designed** for specific applications and provide high efficiency and performance. FPGAs are **reprogramamble** devices that provide significant flexibility. Many designers also used it for prototyping hardware components (before they are eventually included either in the processors or custom ASICs). The [choice between ASICs and FPGAs](https://www.wevolver.com/article/asic-vs-fpga) depends entirely on the application requirements and other factors such as cost.


|||
|----|----|
|<img src="./img/embedded_arch/asic.webp" width="200">| <img src="./img/embedded_arch/xilinx_spartan_fpga.webp" width="200">| 
| An ASIC | Xilinx Spartan FPGA|
||

#### ASICs

These are specialized semiconductor devices -- to implement a _custom_ function, e.g., cryptocurrency mining, nuclear reactor control, televisions. ASICs are tailored to their specific applications. Once created, it cannot be reprogrammed or modified. ASICs are created using a process known as [photolithography](https://www.sciencedirect.com/topics/physics-and-astronomy/photolithography), a method to prepare nanoparticles, that allows components to be "etched" on to a silicon wafer. 

The [ASIC design process](https://www.wevolver.com/article/the-ultimate-guide-to-asic-design-from-concept-to-production), while expensive and time consuming, becomes valuable for _high-volume_ products as the per-unit cost decrease when production nunbers increase. 

| advantages | disadvantages |
|------------|---------------|
| high performance | lack of flexibility |
| low power consumption | high initial costs |
| small form factor | long development time |
| ip protection | obsolescence risk |
| good for mass production | risks with manufacturing yields |
| can integrate multiple functions | design complexity |
||


#### FPGAs

These are also semiconductor devices but they can be **preprogrammed** to implement various circuits and functions. Designers can change the functionality **after** the curcuits have been embossed onto the hardware. Hence, they're good for systems that might require changes at design time and rapid prototyping. An FPGA is a collection of programmable logic and interconnects. They include lookup tables (LUTs) and other parts that can be used to develop multiple, fairly wide-ranging, functions. The programmable blocks can be connected to each other via the interconnects. Some FPGAs even come with additional flash memory. 

[FPGAs are programmed](https://www.wevolver.com/article/fpga) using hardware description languages such as Verilog/VHDL.

| advantages | disadvantages |
|------------|---------------|
| flexibility | lower performance |
| shorter development time | higher power consumption |
| upgradability | high design complexity |
| lower (initial) costs | higher per-unit costs |
| better processing capabilities | design complexity |
| lower obsolescence risks | larger form factor |


## Communication and I/O

Embedded systems need to **communicate** and/or **interface** with various elements:

- the physical world via sensors and actuators
- computers for programming (of the embedded system) or for data transfer
- with other embedded systems/nodes
- handheld devices
- with the internet (either public or to access back end servers)
- satellites?

Hence a large number of communication standards and I/O interfaces have been developed over the years. Let's look at a few of them:

1. [serial (UART)](#uart--rs-232) &rarr; e.g., RS 232
2. [synchronous](#synchronous--i2c-and-spi) &rarr; I2C, SPI
3. [general-purpose I/O](#general-purpose-io-gpio) &rarr; GPIO
4. [debugging interface](#jtag-debugging-interface) &rarr; JTAG
5. [embedded internal communication](#controller-area-network-can) &rarr; CAN
6. [other broadly used protocols](#other-broadly-used-protocols) &rarr; USB, Ethernet/WiFi, Radio, Bluetooth


### UART | RS-232

Serial communication standards are used extensively across many domains, mainly due to their **simplicity** and **low hardware overheads**. The most common among these are the _asynchronous serial communication systems_.

From [Wikipedia](https://en.wikipedia.org/wiki/Asynchronous_serial_communication): 

> Asynchronous serial communication is a form of serial communication in which the communicating endpoints' interfaces are not continuously synchronized by a common clock signal. Instead of a common synchronization signal, the data stream contains synchronization information in form of start and stop signals, before and after each unit of transmission, respectively. The start signal prepares the receiver for arrival of data and the stop signal resets its state to enable triggering of a new sequence.

The following figure shows a communication sample that demonstrates these principles:

<img src="img/embedded_arch/comms/Puerto_serie_Rs232.png" width="300">

We see that each byte has a `start` bit, `stop` bit and eight `data` bits. The last bit is often used as a `parity` bit. All of these "standards" (i.e., the start/stop/parity bits) must be _agreed upon ahead of time_.

A **universal asynchronous receiver-transmitter** (**UART**) then is a peripheral device for such asynchronous commnication; the data format and transmission speeds are configurable. It sends data bits _one-by-one_ (from least significant to most). The precise timing is handlded by the communication channel. 

The electric _signalling levels_ are handled by an external driver circuit. Common signal levels:

- [RS 232](https://www.analog.com/en/resources/technical-articles/fundamentals-of-rs232-serial-communications.html) 
- [RS-485](https://www.renkeer.com/what-is-rs485/)
- raw [TTL](https://www.seeedstudio.com/blog/2019/12/11/rs232-vs-ttl-beginner-guide-to-serial-communication)

Here we will focus on the **RS-232** standard since it is most widely used UART signaling level standard today. The full name of the standard is: "EIA/TIA-232-E Interface Between Data Terminal Equipment and Data Circuit-Termination Equipment Employing Serial Binary Data Interchange" ("EIA/TIA" stands for the Electronic Industry Association and the Telecommunications Industry Association). It was introduced in 1962 and has since been updated _four_ times to meet evolving needs. 

The RS-232 is a _complete_ standard in that it specifies,

- (common) voltage and signal levels
- (common) pin and wiring configurations
- (minimal) control information between host/peripherals 

The RS-232 specifies the electrical, functional and mechanical characteristics to meet all of the above criteria. 

For instance, the _electrical_ characteristics are defined in the following figure:

<img src="img/embedded_arch/comms/rs232-electrical.gif" width="400">

Details:

- **high** level [**logical `0`**] (aka "marking") &rarr; `+5V` to `+15V` (realistically `+3V` to `+15V`)
- **low** level [**logical `1`**] (aka "spacing") &rarr; `-5V` to `-15V` (realistically `-3V` to `-15V`)

Other properties also defined, _e.g._, "[slew rate](https://en.wikipedia.org/wiki/Slew_rate)", impedance, capacitive loads, etc. 

The standard also defines the mechanical interfaces, i.e., the _pin connector_:

<img src="img/embedded_arch/comms/rs232_pins.gif" width="400">

While the official standard calls for a 25-pin connector, it is rarely used. Instead, the **9-pin** connector (shown on the right in the above figure) is in common use.

You can read more details about the standard here: [RS 232](https://www.analog.com/en/resources/technical-articles/fundamentals-of-rs232-serial-communications.html)


### Synchronous | I<sup>2</sup>C and SPI

Synchronous Serial Interfaces (SSIs) are a widely used in industrial applications between a master device (e.g. controller) and a slave device (e.g. sensor). It is based on the [RS-422](https://www.analog.com/media/en/technical-documentation/tech-articles/guide-to-selecting-and-using-rs232-rs422-and-rs485-serial-data-standards--maxim-integrated.pdf) standards and has a high protocol efficiency as well multiple hardware implementations.

SSI properties:

- [differential signalling](https://en.wikipedia.org/wiki/Differential_signalling)
- simplex (i.e., unidirectional communication only)
- non-multiplexed
- point-to-point and 
- uses time-outs to frame the data. 


#### I<sup>2</sup>C

The [Inter-Integrated Circuit](https://www.ti.com/lit/an/sbaa565/sbaa565.pdf) (I<sup>2</sup>C, IIC, I2C) is a synchronous, multi-controller/multi-target (historically termed as multi-master/multi-slave), single-ended, serial communication bus. I2C systems are used for _attaching low-power integrated circuits to processors and microcontrollers_ -- usually for short distance or _intra-board communication_.

I2C components are found in a wide variety of products, _e.g.,_

- EEPROMs
- VGA/DVI/HDMI connectors
- NVRAM chips
- real-time clocks
- reading hardware monitors and sensors
- controlling actuators 
- DAC/ADC
- controlling LCD/OLEDs displays 
- changing computer display settings (contrast, brightness, etc.)
- controlling speaker volume
- and many many more

The main advantage of I2C is that a microcontroller can control a _network_ of chips with just **two** general-purpose I/O pins (serial data line and a serial clock line) and software. A controller device can communicate with any target device through a unique I2C address sent through the serial data line. Hence the two signals are:

|line|voltage| description|
|------|-------|-------|
| serial data line (SDL) | `+5V` | transmit data to or from target devices |
| serial clock line (SCL) | `+3V` | synchronously clock data in or out of the target device |
||

Both are bidirectional and pulled up with resistors.

Here is a typical implementation of I2C:

<img src="img/embedded_arch/comms/i2c_implementation.png" width="400">

An I2C chip example (used for controlling certain TV signals):

<img src="img/embedded_arch/comms/i2c_tv_control.jpg" width="100">

I2C is half-duplex communication where only a single controller or a target device is sending data on the bus at a time. In comparison, the serial peripheral interface (SPI) is a full-duplex protocol where data can be sent to and received back at the same time. An I2C controller device starts and stops communication, which removes the potential problem of bus contention. Communication with a target device is sent through a unique address on the bus. This allows for both multiple controllers and multiple target devices on the I2C bus.

I2C communication details (initiated from the controller device):

| condition | description |
|-----------------|-------|
| I2C `START`| the controller device first pulls the SDA low and then pulls the SCL low |
| I2C `STOP` | the SCL releases high and then SDA releases high |
||

<img src="img/embedded_arch/comms/i2c_start_stop.png" width="300">

<br>

I2C communication is split into: **frames**. Communciation starts when one controller sends an `address frame` after a `START`. This is followed by one or more `data frames`, each consisting of **one byte**. Each frame also has an `acknowledgement` bit. An example of two I2C communication frames:

<img src="img/embedded_arch/comms/i2c_frames.png">

<br>

You can read more at: [I2C](https://www.ti.com/lit/an/sbaa565/sbaa565.pdf).


#### SPI

The [Serial Peripheral Interface](https://www.analog.com/en/resources/analog-dialogue/articles/introduction-to-spi-interface.html) (SPI) has become the de facto standard for _synchronous_ serial communication. It is used in embedded systems, especially between microcontrollers and peripheral ICs such as sensors, ADCs, DACs, shift registers, SRAM, _etc._

The main aspect of SPI is that one main device **orchestrates communication** with one ore more sub/peripheral devices by **driving the clock and chip select signals**.

SPI interface properties:

- _synchronous_
- _full duplex_
- _main-subnode_ (formerly called "master-slave")
- data from the main or the subnode is synchronized on the rising or falling clock edge
- main and subnode can transmit data at the same time
- interface can be 3 or 4-wire (4 wire version is more popular)

|microchip SPI|basic SPI Interface|
|------|-------|
|<img src="img/embedded_arch/comms/spi_microchip.avif" width="100"> |<img src="img/embedded_arch/comms/spi_basic.png" width="500">|
||

The SPI interface contains the following wires:

| signal | description | function |
|--------|-------------|----------|
| `SCLK`   | serial clock | clock signal from main |
| `CS`     | chip/serial select | To select which host to communicate with |
| `MOSI`   | main out, subnode In | serial data out (SDO) for host to target communication |
| `MISO`   | main in, subnode Out | serial data in (SDI) for target to host communication |
||

The main node generates the clock signal. Data transmissions between main ahd sub nodes is synchronized by that clock signal generated by main. SPI devices support _much higher clock frequencies_ than I2C. The `CS` signal is used to select the subnode. Note that this is an **active low signal**, _i.e.,_ a low (`0`) is a selection and a high (`1`) is a disconnect. SPI is a full-duplex interface; both main and subnode can send data at the same time via the MOSI and MISO lines respectively. During SPI communication, the data is simultaneously transmitted (shifted out serially onto the MOSI/SDO bus) and received (the data on the bus (MISO/SDI) is sampled or read in).

**Example**: the [following example](https://www.analog.com/en/resources/analog-dialogue/articles/introduction-to-spi-interface.html) demonstrates the significant savings and simplification in systems design (reduce the number of GPIO pins required). 

Consider the ADG1412 switch being managed by a microcontroller as follows:

<img src="img/embedded_arch/comms/spi_adg_example1.svg" width="300">

Now, as the number of switches increases, the requirement on GPIO pins also increases significantly. A `4x4` configuration requires `16` GPI pins, thus reducing the number of pins available for the microcontroller for other tasks, as follows:

<img src="img/embedded_arch/comms/spi_adg_example2.svg" width="300">

One approach to reduce the number of pins would be to use a serial-to-parallel convertor:

<img src="img/embedded_arch/comms/spi_adg_example3.svg" width="300">

This reduces the pressure on the number of GPIO pins but still introduces additional circuitry. 

Using an SPI-enabled microcontroller reduces the number of GPIOs required and and eliminates the overheads of the needing additional chips (serial-to-paralle convertor):

<img src="img/embedded_arch/comms/spi_adg_example4.svg" width="300">

In fact, using a different SPI configuration ("**daisy-chain**"), we can optimize the GPIO count even further!

<img src="img/embedded_arch/comms/spi_adg_example5.svg" width="300" height="250">

You can read more about [SPI here](https://www.analog.com/en/resources/analog-dialogue/articles/introduction-to-spi-interface.html).


### General-Purpose I/O (GPIO)

A GPIO is a **signal pin** on an integrated circuit or board that can be used to perform _digital I/O operations_. By design, it **has no predefined purpose** &rarr; can be used by hardware/software developers to perform functions _they choose_, _e.g.,_

- GPIO pins can be enabled or disabled.
- GPIO pins can be configured to be input or output.
- input values are readable, often with a 1 representing a high voltage, and a 0 representing a low voltage.
- input GPIO pins can be used as "interrupt" lines, which allow a peripheral board connected via multiple pins to signal to the primary embedded board that it requires attention.
- output pin values are both readable and writable.

GPIOs can be implemented in a variety of ways,

- as a _primary_ function of the microcontrollers, _e.g._, [Intel 8255](https://www.geeksforgeeks.org/programmable-peripheral-interface-8255/)
- as an _accessory_ to the chip

While microcontrollers may use GPIOs are their primary external interface, many a time the pins may be capable of other functions as well. In such instances, it may be necessary to configure the pins using other functions. 

Some examples of chips with GPIO pins:

|Intel 8255|PIC microchip|ASUS Tinker|
|------|-------|---------|
|<img src="img/embedded_arch/comms/gpio_Ic-photo-Intel--D8255.JPG" width="250"> |<img src="img/embedded_arch/comms/gpio_microchip_PIC18F8720.jpg" width="150"> | <img src="img/embedded_arch/comms/gpio_Asus_Tinker_Board.jpg" width ="200"> |
|24 GPIO pins |29 GPIO pins| 28 GPIO pins|
||


GPIOs are used in a diverse variety of applications, limited only by the electrical and timing specifications of the GPIO interface and the ability of software to interact with GPIOs in a sufficiently timely manner.

Some "properties"/applications of GPIOs:

- GPIOs use standard logic levels and cannot supply significant current to output loads
- high-current output buffers or relays can be used to control high-power devices
- input buffers, relays, or opto-isolators translate incompatible signals to GPIO logic levels
- GPIOs can control or monitor other circuitry on a board, such as enabling/disabling circuits, reading switch states, and driving LEDs
- multiple GPIOs can implement bit banging communication interfaces like I²C or SPI
- GPIOs can control analog processes via PWM, adjusting motor speed, light intensity, or temperature
- PWM signals from GPIOs can be converted to analog control voltages using RC filters

GPIO interfaces vary widely. Most commonly, they're simple _groups of pins_ that can switch between input/output. On the other hand, each pin can be set up differently &rarr; set up/accept/source different voltages/drive strengths/pull ups and downs. 

Programming the GPIO:

- usually pin states are exposed via different interfaces, _e.g.,_ **memory-mapped I/O** peripherals or dedicated I/O port instructions 
- input values can be used as interrupts (IRQs)

For more information on programming/using GPIOs, read these: [GPIO setup and use](https://docs.oracle.com/javame/8.0/me-dev-guide/gpio.htm), [Python scripting the GPIO in Raspberry Pis](https://www.instructables.com/Raspberry-Pi-Python-scripting-the-GPIO/), [general purpose I/O](https://docs.nordicsemi.com/bundle/ps_nrf52810/page/gpio.html), [GPIO setup in Raspberry Pi](https://projects.raspberrypi.org/en/projects/physical-computing/1).


### JTAG Debugging Interface

The JTAG standard (named after the "Joint Test Action Group"), technically the [IEEE Std 1149.1-1990 IEEE Standard Test Access Port and Boundary-Scan Architecture](https://web.archive.org/web/20170830070123/http://www.intel.com/content/dam/www/public/us/en/documents/white-papers/jtag-101-ieee-1149x-paper.pdf), is an industry standard for **testing and verification of printed circuit boards**, _after manufacture_.

"JTAG", depending on the context, could stand for one or more of the following:

- implementation of IEEE 1149.x for Board Test, or Boundary Scan testing
- appliance used to program on board flash or eeprom devices on a circuit board
- hardware device used to debug microprocessor software
- hardware device used to test a board using Boundary Scan

The basic building block of a JTAG OCD is the **Test Access Point** or **TAP controller**. This allows access to all the custom features within a specific processor, and must support a minimum set of commands. On-chip debugging is a _combination of hardware and software_. 

| type     | description |
|----------|-----------|
| hardaware | **on chip debug** (OCD)|
| software  | **in-circuit-emulator** (ICE)/JTAG emulator |
||

The off-chip parts are actually PC peripherals that need corresponding drivers running on a separate computer. On most systems, JTAG-based debugging is available from the very first instruction after CPU reset, letting it assist with development of early boot software which runs before anything is set up. The JTAG emulator allows developers to access the embedded system at the **machine code level** if needed! Many silicon architectures (Intel, ARM, PowerPC, etc.) have built entire infrastructures and extensions around JTAG.

A high-level overview of the JTAG architecture/use:

<img src="img/embedded_arch/comms/jtag_high_level.png" width="400">

<br>

JTAG now allows for,

- processors can not be _halted_, _single-stepped_ or _run freely_
- can set code _breakpoints_ for both, code in RAM as well as ROM/flash
- _data breakpoints_  are available 
- _bulk data download_ to RAM
- _access to registers and buses_, even without halting the processors!
- _complex logic routines_, _e.g.,_ ignore the first seven accesses to a register from one particular subroutine

JTAG allows for _device programmer hardware_ allows for transfering data into internal, _non-volatile_ memory of the system! Hence, we can use JTAGs to **program** devices such as FPGAs. In fact, many memory chips also have JTAG interfaces. Some modern chips also allow access to the the (internal and external) data buses via JTAG.

**JTAG interface**: depending on the actual interface, JTAG has 2/4/5 pins. The 4/5 pin versions are designed so that _multiple chips_ on a board can have their JTAG lines **daisy-chained** together if specific conditions are met.

 Schematic Diagram of a JTAG enabled device:

 <img src="img/embedded_arch/comms/jtag_schematic_diagram.gif" width="300">

 The various pins signals in the JTAG TAP are:

| signal | description |
|--------|-------------|
| `TCK` | synchronizes the internal state machine operations |
| `TMS` | sampled at the rising edge of `TCK` to determine the next state |
| `TDI` | data shifted into the device’s test or programming logic; sampled at the rising edge of `TCK` when the internal state machine is in the correct state |
| `TDO` | represents the data shifted out of the device’s test or programming logic and is valid on the falling edge of `TCK` when the internal state machine is in the correct state |
| `TRST` | optional pin which, when available, can reset the tap controller’s state machine |
||

The TAP controller implements the following state machine:

<img src="img/embedded_arch/comms/jtag_tap_state_machine.gif" width="300">

<br>

To use the JTAG interface, 

- host is connected to the target's JTAG signals (`TMS`, `TCK`, `TDI`, `TDO`, etc.) through some kind of JTAG adapter
- adapter connects to the host using some interface such as USB, PCI, Ethernet, etc.
- host communicates with the TAPs by manipulating `TMS` and `TDI` in conjunction with `TCK` 
- host reads results through `TDO` (which is the only standard host-side input)
- `TMS`/`TDI`/`TCK` output transitions create the basic JTAG communication primitive on which higher layer protocols build

<br>

For more information about JTAG, read: [Intel JTAG Overview](https://web.archive.org/web/20170830070123/http://www.intel.com/content/dam/www/public/us/en/documents/white-papers/jtag-101-ieee-1149x-paper.pdf), [Raspberry Pi JTAG programming](https://forums.raspberrypi.com/viewtopic.php?t=286115), [Technical Guide to JTAG](https://www.xjtag.com/about-jtag/jtag-a-technical-overview/) and the [JTAG Wikipedia Entry](https://en.wikipedia.org/wiki/JTAG) is quite detailed.


### Controller Area Network (CAN)

CAN is a vehicle bus standard to enable efficient communication between electronic control units (ECUs). CAN is,

- broadcast-based
- message-oriented
- uses arbitration &rarr; for data integrity/prioritization

CAN **does not** need a a host controller. ECUs connected via the CAN bus can easily share information with each other. all ECUs are connected on a two-wire bus consisting of a twisted pair: CAN high and CAN low. The wires are often color coded: 

|||
|-----|------|
|CAN high| yellow| 
|CAN low | green|
||

|||
|------|--------|
| <img src="img/embedded_arch/comms/can-twisted-can-bus-wiring-harness-high-low-green-yellow.svg" width="200"> | <img src="img/embedded_arch/comms/CAN-bus_basic.svg" width="300"> |
|CAN wiring | multi-ecu CAN setup|
||

<br>

An ECU in a vehicle consists of:

<table>
    <tr>
        <th>components</th>
        <th>internal architecture</th>
    </tr>
    <tr>
        <td>
            <ul>
                <li><b>microcontroller</b> to interpret/send out CAN messages</li>
                <li><b>CAN controller</b> ensures all communication adheres to CAN protocols</li>
                <li><b>CAN transceiver</b> connects CAN controller to the physical wires</li>
            </ul>
        </td>
        <td>
            <img src="img/embedded_arch/comms/can_ecu_internals.svg" width="250">
        </td>
    </tr>
    <tr> <td></td> <td></td></tr>
</table>

_Any_ ECU can broadcast on the CAN bus and the messages are accepted by _all_ ECUs connected to it. Each ECU can either choose to ignore the message or act on it.

> what are the implications for **security**?

While there is no "standard" CAN connector (each vehicle may use different ones), the **CAN Bus DB9** connector has become the de facto standard:

<img src="img/embedded_arch/comms/can-bus-db9-connector-pinout-d-sub.svg" width="350">

The above figure shows the various pins and their signals.

<br>

**CAN Communication Protocols**: CAN is split into:

<table>
    <tr>
        <th>layer</th>
        <th>relation to OSI stack</th>
    </tr>
    <tr>
        <td>
            <ul>
                <li><b>data link</b>: CAN frame formats, <br>error handling, data transmission, <br>data integrity</li>
                <li><b>physical</b>: cable types, <br>electrical signal levels, <br>node requirements, <br>cable impedance, etc.</li>
            </ul>
        </td>
        <td>
            <img src="img/embedded_arch/comms/can-bus-osi-model-7-layer-iso-11898-physical-data.svg" width="350">
        </td>
    </tr>
    <tr> <td></td> <td></td></tr>
</table>

<br>

All communication over the CAN bus is done via the **CAN frames**. The _standard_ CAN frame (with an `11-bit` identifier) is shown below:

<img src="img/embedded_arch/comms/CAN-bus-frame-standard-message-SOF-ID-RTR-Control-Data-CRC-ACK-EOF.svg" width="400">

<br>

While the lower-level CAN protocols described so far work on the two lowest layers of the OSI networking stack, it is still limiting. For instance, the CAN standard doesn't discuss how to,

- decode RAW data
- handle larger data (more than 8 bytes)


Hence, some **higher-order** protocols have been developed, _viz.,_

|protocol|description|
|--------|-----------|
|[OBD2](https://www.csselectronics.com/pages/obd2-explained-simple-intro) | on-board diagnostics in cars/trucks for diagnostics, maintenance, emissions tests |
|[UDS](https://www.csselectronics.com/pages/uds-protocol-tutorial-unified-diagnostic-services) | Unified Diagnostic Services (UDS) used in automotive ECUs for diagnostics, firmware updates, routine testing|
|[CCP/XCP](https://www.csselectronics.com/pages/ccp-xcp-on-can-bus-calibration-protocol) | used in embedded control/industrial automation for _off-the-shelf interoperability_ between CAN devices|
|[SAE J1939](https://www.csselectronics.com/pages/j1939-explained-simple-intro-tutorial) | for heavy-duty vehicles |
|[NMEA 2000](https://www.csselectronics.com/pages/nmea-2000-n2k-intro-tutorial )| used in maritime industry for connecting e.g. engines, instruments, sensors on boats|
|[ISOBUS](https://www.csselectronics.com/pages/isobus-introduction-tutorial-iso-11783)| used in agriculture and forestry machinery to enable plug and play integration between vehicles/implements, _across brands_|
||

There also exist other higher-order protocols (numbering in the thousands) the most prominent of which are: ARINC, UAVCAN, DeviceNet, SafetyBUS p, MilCAN, HVAC CAN. 

<br>

More details about CAN and its variants: [CAN Bus Explained](https://www.csselectronics.com/pages/can-bus-simple-intro-tutorial).


### Other Broadly Used Protocols 

Autonomous (and other embedded systems) use a variety of other communication protocols in order to interface with the external world and/or other systems (either other nodes in the system or external components such as back end clouds).

Note that since many of these are well known and publicly documented, we won't elaborate much here.

Here are some of the well known communication protocols, also used in embedded systems:

|protocol|links|
|--------|------|
|USB | How USB works: [part 1](https://www.circuitbread.com/tutorials/how-usb-works-introduction-part-1), [part2](https://www.circuitbread.com/tutorials/how-usb-works-communication-protocol-part-2), [part 3](https://www.circuitbread.com/tutorials/how-usb-works-enumeration-and-configuration-part-3); [USB in a Nutshell (very detailed)](https://www.beyondlogic.org/usbnutshell/usb1.shtml).|
|Ethernet | [Reliable Embedded Ethernet](https://www.embedded.com/implement-reliable-embedded-ethernet-connectivity/), [Embedded Ethernet and Internet (book, online)](https://www.google.com/books/edition/_/3ZPPBgAAQBAJ?hl=en&gbpv=1&pg=PA1)|
|WiFi | [WiFi Sensing on the Edge (paper)](https://ebulutvcu.github.io/COMST22_WiFi_Sensing_Survey.pdf) |
|Bluetooth| [Bluetooth Basics](https://learn.sparkfun.com/tutorials/bluetooth-basics/all), [Bluetooth Low Energy](https://novelbits.io/bluetooth-low-energy-ble-complete-guide/) |
|Radio| [Embedded Development with GNU Radio](https://wiki.gnuradio.org/index.php/Embedded_Development_with_GNU_Radio)|
||


## Raspberry Pi and Navio2

Let us look at the two architectures we use extensively in this course: 

- [Raspberry Pi](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/) model 4(b)
- [Navio2](https://navio2.hipi.io) &rarr; autopilot hat for the Raspberry Pi


The high-level architecture of the Pi shows many of the components we have discussed so far:

<img src="img/embedded_arch/pi-4-architectural_features.png" width="400">

In particular, the Pi has,

|component | description/details|
|----------|--------------------|
|processor | Broadcomm **BCM2711**, Quad core Cortex-A72 (ARM v8) 64-bit SoC at 1.8GHz|
|memory | 1GB, 2GB, 4GB or 8GB LPDDR4-3200 SDRAM|
|network | Wifi (2.4/5.0 GHz), Gigabit ethernet, Bluetooth/BLE|
|I/O |   40 pin GPIO, USB 3.0/2.0/C|
|storage | Micro-SD Card |
|misc | micro-hdmi, stereo audio/video, displayport, camera port, power|
|os | [Raspberry Pi OS](https://www.raspberrypi.com/software/) (formerly called Raspbian)|
||

<br>

Read more about the Raspberry Pi: [Raspberry PI -- A Look Under the Hood](https://www.electronics-lab.com/project/raspberry-pi-4-look-hood-make/)

<br>

The **Navio2** is a "hat" that adds the following to a Raspberry Pi:

- autopilot functionality
- multiple sensors

The high-level architecture,

<img src="img/embedded_arch/navio2_features.jpg" width="400">

As the figure shows, the Navio2 adds the following components:

|component|description/details|
|---------|-------------------|
|GNSS receiver | for GPS signals|
|high-precision barometer| for measuring pressure (and altitude)|
|(dual) IMU | two 9 DOF with gyroscope, accelerometer, magnetometer, each|
|RC I/O co-processor | PWM, ADC, SBUS, PPM |
|extension ports | ADC, I2C, UART |
|power supply | triple redundant |
||

<br>

More details about the Navio2 and how to program it: [Navio2 Documentation](https://docs.emlid.com/navio2/).

<br>
<br>


## References

[^1]: TBD
[^2]: https://dl.acm.org/doi/10.5555/244522.244548
[^3]: https://www.cecs.uci.edu/~papers/compendium94-03/papers/2002/date02/pdffiles/05a_1.pdf
<!--link rel="stylesheet" href="./custom.sibin.css"-->


# Sensors and Sensing

An embedded/autonomous system _perceives_ the physical world via sensors -- either to gather information about its environment or to model its _own_ state. Hence it is a critical component in the _sensing &rarr; planning &rarr; actuation_ loop and a critical component in the design of embedded and autonomous systems.

|||
|------|-------|
|<img src="img/sense_planning_actuation.png" width="400">|<img src="img/stack_architecture/stack_overview.2.png" width="300">|
||

Modern autonomous systems used a _wide array_ of sensors. This is necessary due to:

- there is a need to measure **different** quantities, _e.g.,_ GPS, velocity, objects, _etc._
- sensor measurements often have **errors** &rarr; hence, we need multiple sensors, often using **different physical properties** to measure the _same thing_; _e.g.,_ LiDar and cameras can both be used to detect objects in front of, and around, an autonomous vehicle.

At its core, 

> a sensor captures a physical/chemical/environmental quantity and **converts it to a digital quantity**.

(hence the need for an Analog-to-Digital Convertor (ADC) as we shall see later)

By definition, sensors generate **signals**. A signal, `s`, is defined as a mapping from the _time_ domain to a _value_ domain:

$$
s: D_t \mapsto D_v
$$

where,

| symbol | description  |
|--------|------------------------------------------|
| $D_t$  | continuous or discrete **time** domain   |
| $D_v$  | continuous or discrete **value** domain  |
||

**Note:** remember that computers require **discrete** sequences of physical values. Hence, we need to **convert** the above into the discrete domain. The way to achieve this: **sampling**:

<img src="img/sensors/discretization_sampled.signal.svg" title="Sampling image from Wikipedia" width="300">

The figure shows a continuous signal being sampled (in <font color="red"><b>red</b></font> arrows). We will discuss sampling and related issues later in this topic.


## Types of Sensors

Sensors come in various shapes and sizes. Usually designers of autonomous systems will develop a "**sensor plan** that will consider,

- required functionality
- sensor range(s)
- cost

Hence, each autonomous system will likely have its own set of sensors (or sensor plan). _Typical_ sensors found on modern autonomous systems can be classified based on the underlying physics used:

|physical property|sensor|
|-----------------|-------|
|[_internal_ measurements](#inertial-measurement-units-imu)| IMU |
|_external_ measurements| GPS |
|["bouncing" electromagnetic waves](#bouncing-of-electromagnetic-waves--lidar-and-mmwave)| LiDAR, RADAR, mmWave Radar|
|optical| cameras, infrared sensors|
|[accoustic](#ultrasonic)| ultrasonic sensors|
||

Some of the above can be combined to generate other sensing patterns, _e.g.,_ **stereo vision** using multiple cameras or camera+LiDAR.

We will go over **some** of these sensors and their underlying physical principles. 

### Inertial Measurement Units (IMU)

These sensors define the **movement of a vehicle**, along the three axes, in addition to other behaviors like acceleration and directionality. An IMU typically includes the following sensors:

|||||
|---------|--------|---------|-----------|
|<img src="img/sensors/imu_exploded_view.jpg" width="600">|<img src="img/sensors/imu_accelerometer.png" width="400">|<img src="img/sensors/imu_gyro.png" width="400">|<img src="img/sensors/imu_magnetometer.png" width="400">|
||

As we see from the first picture above, an IMU also has a CPU (typically a microcontroller) to manage/collect/process the data from the sensors.

The functions of the three sensors are:

1. **gyroscope**: is an inertial sensor that measure an object's angular rate with respect to an inertial reference frame. It measures the following movements:

||||
|--------|----------|---------|
|<img src="img/sensors/imu_yaw.gif">|<img src="img/sensors/imu_pitch.gif">|<img src="img/sensors/imu_roll.gif">|
| "yaw" | "pitch" | "roll" |
||

IMUs come in all shapes and sizes. These days they're very small but the original IMU's ver really large, as evidenced by the one used in the [Apollo space missions](http://klabs.org/history/history_docs/mit_docs/1690.pdf):

<img src="img/sensors/imu_apollo.jpg" width="300">

<br>


2. **accelerometer**: is the primary sensor responsible for measuring inertial acceleration, or the change in velocity over time.

3. **magnetometer**: measures the strength and direction of magnetic field – to find the magnetic north


### Bouncing of Electromagnetic Waves | LiDAR and mmWave

A very common principle for measuring surroundings is to bounce electromagnetic waves off nearby objects and measuring the round trip times. Shorter times indicate closer objects while longer times indicate objects that are farther away. [RADAR](https://www.noaa.gov/jetstream/doppler/how-radar-works) is a classic example of this type of sensor and its (basic) operation is shown in the following image (courtesy NOAA):

<img src="img/sensors/radar_doppler_ani.gif" width="400">

While many autonomous vehicles use RADAR, we will focus on other technologies that are more prevalent and provide much higher precision, _viz.,_

1. [LiDAR](#light-detection-and-ranging-lidar)
2. millimeter Wave RADAR (mmWave)


#### Light Detection and Ranging (LiDAR)

[LiDAR](https://web.stanford.edu/class/ee259/lectures/ee259_05_lidar.pdf) is a sensor that uses (_eye safe_) **laser beams** for mapping surroundings and creating **3D representation** of the environment. So lasers are used for,

- imaging
- detection 
- ranging

We can use LiDAR to distance, angle as well as the _radial velocity_ of some objects -- all relative to the autonomous system (rather the sensor). So, in practice, this is how it operates:

<img src="img/sensors/lidar_principle_operation.png" width="400">

We define a **roundtrip time**, $	au$, as the time between when a pulse is sent out from the transmitter (`TX`) to when light reflected from the object is detected at the receiver (`RX`). 

So, the **target range** (_i.e.,_ the distance to te object), $R$, is measured as:

$$
R = rac{c	au}{2}
$$

where, `c` is the speed of light. 

More details (from [Mahalati](https://web.stanford.edu/class/ee259/lectures/ee259_05_lidar.pdf)):
> Lasers used in lidars have frequencies in the $100s$ of Terahetrz. Compared to RF waves, lasers have significantly smaller wavelengths and can hence be easily collected into narrow beams using lenses. This makes DOA estimation almost trivial in lidar and gives it significantly better reso- lution than MIMO imaging radar.

The _end product_ of LiDAR is essentially a **point cloud**, defined as:

> a collection of points generated by a sensor. Such collections can be very dense and contain billions of points, which enables the creation of highly detailed 3D representations of an area.

<img src="img/sensors/lidar_point_cloud_torus.gif" title="3D point cloud of a Torus. Courtesy Wikipedia">

In reality, point cloud representations around autonomous vehicles end up looking like:

<video controls width="500"> <source src="https://sibin.github.io/teaching/csci6907_88-gwu-secure_autonomous/fall_2022/other_docs/What-is-Lidar-video.mp4"></video>

[Point clouds](https://www.yellowscan.com/knowledge/lidar-point-cloud-basics/) provide valuable information, _viz.,_

- 3D coordinates, $(x, y, z)$
- **strength** of returned signal &rarr; provides valuable information about the **density** of the object (or even material composition)!
- additional attributes: return number, scan angle, scan direction, point density, RGB color values, and time stamps &rarr; each can be used for refining the scan.

There are **two types** of _scene illumination_ techniques for LiDAR:

| type | illumination method  | detector |
|--------|---------------------|-----------|
| flash lidar | _entire_ scene using wide laser  | receives all echoes on a photodetector array |
| scanning lidar | very narrow laser beams, scan illumination spot with laser beam scanner | single photodetector to sequentially estimate $	au$ for each spot |
||

<br>

| | flash lidar | scan lidar |
|----|----|------|
| **architecture** | <img src="img/sensors/lidar_flash.png" width="400"> | <img src="img/sensors/lidar_scan.png" width="400"> |
| **resolution** determined by | photodetector array pizel size (like camera) | laser beam size and spot fixing |
| **frame rates** | higher (up to `100 fps`) | lower (< `30 fps`) |
| **range** | shorter (quick beam divergence, like photography) | longer (`100m+`) |
| **use**   | less common | **most common** |
||

<br>

Now, consider the following scene (captured by a camera):

<img src="img/sensors/lidar_camera_image.png" width="400">

<br>
<br>

Compare this to the LiDAR images captured by the two methods:

|flash lidar | scan lidar (16 scan lines)| scan lidar (32 scan lines)|
|----|----|-----|
| <img src="img/sensors/lidar_flash_image.png" width="400"> | <img src="img/sensors/lidar_scan_16.png" width="400"> | <img src="img/sensors/lidar_scan_32.png" width="400">|

<br>

> A "LiDAR scan line" refers to a **single horizontal line** of laser pulses emitted by a LiDAR sensor, essentially capturing a cross-section of the environment at a specific angle as the sensor rotates, creating a 3D point cloud by combining multiple scan lines across the field of view; it's the basic building block of a LiDAR scan, similar to how a single horizontal line is a building block of an image. 

**Potential Problems**:

Atmospheric/environmental conditions can **negatively** affect the quality of the data captured by the LiDAR. For instance, **fog** can scatter the laser photons resulting in **false positives**. 

<img src="img/sensors/lidar_fog.png" width="400">

As we see from the above image, the scattering due to the fog results in the system "identifying" multiple objects even though there is only _one_ person in the scene.

Here are additional examples from the [Velodyne VLP-32C](https://www.mapix.com/lidar-scanner-sensors/velodyne/velodyne-vlp-32c/) sensor:

1. **light** fog (camera vs LiDAR)

<img src="img/sensors/lidar_veoldyne_lightfog.png" width="600">

The LiDAR does a good job isolating the main subject with very few false positives.

2. **heavy** fog (camera vs LiDAR)

<img src="img/sensors/lidar_velodyne_heavyfog.png" width="600">

The LiDAR _struggles_ to isolate the main subject with very _high_ false positives.

In spite of these issues, LiDAR is one of the most popular sensors used in autonomous vehicles. They're getting smaller and more precise by the day; also decreasing costs means that we will see a proliferation of these types of sensors in many autonomous systems. 

For an in-depth study on LiDARs, check this out: [Stanford EE 259 LiDAR Lecture](https://web.stanford.edu/class/ee259/lectures/ee259_05_lidar.pdf).


#### Millimeter Wave Radar [mmWave]

Short wavelengths like the *millimeter wave** (**mmWave**) in the electromagnetic spectrum allows for:

- smaller antennae
- integration of entire RADAR circuitry in a single chip!
- spectrum of 10 millimeters (`30 GHz`) to 1 millimeter (`300 GHz`)

|||
|-----|------|
| <img src="img/sensors/mmwave.jpg" width="300"> | <img src="img/sensors/mmwave_ucsdavif.avif" width="300">
||

As we see from the above images, the sensors can be **very small**, yet **very precise** &rarr; some can detect movements up to _4 millionths of a meter_!

**Advantages** of mmWave:

| Advantage | Description |
|-----------|-------------|
| small antenna caliber | narrow beam gives high tracking, accuracy; high-level resolution, high-resistance interference performance of narrow beam; high antenna gain; smaller object detection |
| large bandwidth | high information rate, details structural features of the target; reduces multipath, and enhances anti-interference ability; overcomes mutual interference; high-distance resolution |
| high doppler frequency | good detection and recognition ability of slow objectives and vibration targets; can work in snow conditions |
| good anti-blanking performance | works on the most used stealth material |
| robustness to atmospheric conditions | such as dust, smoke, and fog compared to other sensors |
| operation under different lights | radar can operate under bright lights, dazzling lights, or no lights |
| insusceptible to ground clutter | allowing for close-range observations; the low reflectivity can be measured using mmwave radar |
| fine spatial resolution | for the same range, mmwave radar offers finer spatial resolution than microwave radar >
||

<br>

mmWave is also used for **in-cabin monitoring of drivers**!

<br>

**Limitations**:

- line of sight operations
- affected by water content, gases in environments
- affected by contaminated environment and physical obstacles

<br>

**Resources**:

For a more detailed description of mmWave RADAR, read: [Understanding mmWave RADAR, its Principle & Applications](https://www.design-reuse.com/articles/55851/mmwave-radar-principle-applications.html)

For programming a LiDAR, see: [how to program a LiDAR with an Arduino](h.ttps://www.engineersgarage.com/how-to-use-a-lidar-sensor-with-arduino/).




### Ultrasonic 

Much like lidars, we can use reflected sounds waves to detect objects. They work by emitting high-frequency sound waves, typically above human hearing, and then listening for the echoes that bounce back from nearby objects. The sensor calculates the distance based on the time it takes for the echo to return, using the speed of sound. Popular modules like the HC-SR04 (Used in Lab#2) are easy to integrate with microcontrollers such as Arduino and Raspberry Pi. These sensors are widely used in robotics for obstacle avoidance, automated navigation, and liquid level sensing.

However, unlike optical (electromagnetic waves) detectors, ultrasonic sensors, while useful for basic distance measurements, cannot replicate the functionalities of LiDAR systems due to several key limitations. Unlike LiDAR, which employs laser beams to generate high-resolution, three-dimensional point clouds, ultrasonic sensors emit sound waves that provide only limited, single-point distance data with lower precision. LiDAR offers greater accuracy and longer range, enabling detailed mapping and object recognition essential for applications like autonomous vehicles and advanced robotics. Additionally, LiDAR systems can cover a wider field of view and operate effectively in diverse environments by rapidly scanning multiple directions, whereas ultrasonic sensors typically have a narrow detection cone and struggle with complex or cluttered scenes. Furthermore, LiDAR’s ability to capture data at high speeds allows for real-time processing and dynamic obstacle detection, which ultrasonics cannot match. This is because comparitively, it sounds waves take a lot of time to return since they're much slower in speed compared to light waves (360m/s vs 299,792,458m/s). These differences in data richness, accuracy, and versatility make ultrasonic sensors unsuitable substitutes for the sophisticated capabilities offered by LiDAR technology.

We'll be using ultrasonic distance finders in futures MPs to stop our rovers from colliding into objects. Since our rovers don't moove to fast and complexity is relatively low, only a ultrasonic sensor would suffice.

## Errors in Sensing

Since sensors deal with and measure the _physical_ world, **errors** will creep in over time. 

Some typical errors in the use of physical sensors:

| error type | description |
|----------------|-------------|
| **sensor drift** | over time the sensor measurements will "drift", i.e., a gradual change in its output &rarr; away from average values (e.g., due to wear and tear) |
| **constant bias** | bias of an accelerometer is the offset of its output signal from the actual acceleration value. A constant bias error causes an error in position which grows with time |
| **calibration errors** | ‘calibration errors’ refers to errors in the scale factors, alignments and linearities of the gyros. Such errors tend to produce errors when the device is turning. These errors can result in additional drift |
| **scale factor** | scale factor is the relation of the accelerometer input to the actual sensor output for the measurement. Scale factor, expressed in ppm, is therefore the linear growth of input variation to actual measurement |
| **vibration rectification errors** | vibration rectification error (VRE) is the response of an accelerometer to current rectification in the sensor, causing a shift in the offset of the accelerometer. This can be a significant cumulative error, which propagates with time and can lead to over compensation in stabilization |
| **noise** | random variations in the sensor output that do not correspond to the actual measured value |
||

<br>

Each error type must be dealt with in different ways though one of the commomn ways to prevent sensor errors from causing harm to autonomous systems &rarr; **sensor fusion**, _i.e.,_ use information from **multiple sensors** before making any decisions. We will dicuss sensor fusion later in this course.


## Analog to Digital Convertors (ADCs)

As [mentioned earlier](#sensors-and-sensing), a sensor maps a physical quantity from the time domain to the value domain,

$$
s: D_t \mapsto D_v
$$

where,

| symbol | description                              |
|--------|------------------------------------------|
| $D_t$  | continuous or discrete **time** domain   |
| $D_v$  | continuous or discrete **value** domain  |
||

Remember that computers require **discrete** sequences of physical values since **microcontrollers cannot read values unless it is digital data**. Microcontrollers can only see “levels” of voltage, which depends on the resolution of the ADC and the system voltage.

Hence, we need to **convert** the above into the discrete domain, _i.e.,_ we require $D_v$ to be composed of discrete values. 

According to [Wikipedia](https://en.wikipedia.org/wiki/Discrete_time_and_continuous_time#),

> A discrete signal or discrete-time signal is a time series consisting of a sequence of quantities. Unlike a continuous-time signal, a discrete-time signal is not a function of a continuous argument; however, it may have been obtained by sampling from a continuous-time signal. When a discrete-time signal is obtained by sampling a sequence at uniformly spaced times, it has an associated **sampling rate**.

<br>

A visual respresentation of the sampling rate and how it correlates to the sampling of an analog signal:

|analog signal|sampling rate|sampling|
|-------------|-------------|--------|
|<img src="img/sensors/adc_analog_signal.png">|<img src="img/sensors/adc_sampling_rate.png">|<img src="img/sensors/adc_sampling.png">|
||


Hence, a device that converts analog signals to digital data values is called &rarr; an **analog-to-digital convertor** (**ADC**). This is one of the most common circuits/microcontrollers in embedded (and hence, autonomous) systems. _Any_ sensor that measures a physical property must pass its values through an ADC so that the sensor values can be used by the system (the embedded processor/microcontroller, really).

This is best described using an example:

<img src="img/sensors/adc_example.jpg" width="400">

The <font color="blue"><b>analog</b></font> signal is **discretized** into the <font color="red"><b>digital</b></font> signal after passing through an ADC.

ADCs follow a sequence:

- **sample** the signal
- **quantify** it to determine the resolution of the signal
- set **binary values**
- **send it to the system** to read the digital signal

Hence, two important aspects of an ADC are:

- [sampling rate](#adc-sampling-rate)
- [resolution](#adc-resolution)

### ADC Sampling Rate 

The sampling rate (aka Sampling Frequency) is measured in **samples per second** (SPS or S/s). It dictates _how many samples_ (data points) are taken in one second. If an ADC records more samples, then it can handle higher frequencies. 

The sample rate, $f_s$ is defined as,

$$
f_s = rac{1}{T}
$$

where,

|symbol|definition|
|------|----------|
|$f_s$ | sampling rate/frequency|
|$T$ | period of the sample |
||

Hence, in the previous example, 

|symbol|value|
|------|----------|
|$f_s$ | `20 Hz` |
|$T$ | `50 ms` |
||

While this looks slow (`20 Hz`), the digital signal tracks the original analog signal quite faithfully &rarr; the original signal itself is quite slow (`1 Hz`).

Now, if the sampling signal is _considerably slower_ than the analog signal, then it loses fidelity and we see **aliasing**, where the reconstructed signal (the digital one in the case) **differs from the original**. Consider the following example of such a case:

<img src="img/sensors/adc_aliasing_example.jpg" width="400">

As we see from the above figure, the digital output is **nothing** like the original. Hence, this (digital) output will not be of much use to the system. 

<br>

[**Nyquist-Shannon Sampling Theorem**](https://fab.cba.mit.edu/classes/S62.12/docs/Shannon_noise.pdf):

> to accurately reconstruct a signal from its samples, the sampling rate must be **at least twice the highest frequency component** present in the signal

If the sampling frequency is less than the Nyquist rate, then aliasing starts to creep in.

Hence, 

$$
f_{Nyquist} = 2* f_{max}
$$

where,

|symbol|definition|
|------|----------|
|$f_{Nyquist}$ | Nyquist sampling rate/frequency|
|$f_{max}$ | the maximum frequency that appears in the signal |
||

For instance, if your analog signal has a maximum frequency of `50 Hz` then your sampling frequency must be _at least_, `100 Hz`. If this principle is followed, then it is possible to **accurately reconstruct** the original signal and its values.

Note that sometimes _noise_ can introduce additonal (high) frequencies into the system but we don't want to sample those (for obvious purposes). Hence, it is a good idea to add [anti-aliasing fitlers](https://www.analog.com/en/resources/technical-articles/guide-to-antialiasing-filter-basics.html) to the analog signal _before_ it is passed to the ADC.

### ADC Resolution

An ADC's resolution is directly related to the **precision** of the ADC, determined by its **bit length**. The following examples shows the fidelity of the reconstruction, based on various bit lengths:

<img src="img/sensors/adc_resolution_example.jpg" width="400">

Increasing bit lengths the digital signal more closely represents the analog one.

There exists a correlation between the bit length and the **voltage** of the signal. Hence, the **true resolution** of the ADC is calculated using the bit length **and** the voltage as follows:

$$
Step Size = rac{V_{ref}}{N}
$$

where,

|symbol|definition|
|------|----------|
|$Step Size$| resolution of each level in terms of voltage|
|$V_{ref}$ |voltage reference/range of voltages|
|$N = 2^n$ | total "size" of the ADC|
|$n$ | bit size|
||

This is easier to understand with a concrete example:

> consider a sine wave with a voltage, `5 V` that must be digitized. <br>
> <br>
> If our ADC precision is `12 bits`, then we get <br>
> $N = 2^{12} = 4096$ <br>
> <br>
> Hence, $Step Size = 5V /\ 4096$ which is `0.00122V` (or `1.22mV`)<br>
> <br>
> Hence, the system can tell when a voltage level changes by `1.22 mV`!

(Repeat the exercise for say, bit length, $n = 4$)

<br>

**Visual Example:**

The above maybe intuitively understood as follows:

Consider the following signal:

<img src="img/sensors/adc_bits/adc_bits.1.png" width="300">

Now, if we want to sample this signal, we can obtain measurements at:

<img src="img/sensors/adc_bits/adc_bits.2.png" width="300">

<br>

The figure shows `9` measurements. 

Suppose, the ADC registers have a width of: `2 bits`. Hence it can store at most: `4 values`.

Since is is **not** possible to store `9` values &rarr; `2` bits, we must select **only `4` values** omn the digital side. 

We then get the following representation:

<img src="img/sensors/adc_bits/adc_bits.3.png" width="300">

<br>

which, to be honest, is not really a good representation of the original signal!

Now, consider the case where the ADC registers have a bit width: **`4 bits`** &rarr; `16 values`! Hence, we can easily store **all `9 values`** easily. 

So, we can get a digital representation as follows:

<img src="img/sensors/adc_bits/adc_bits.4.png" width="300">

<br>

We see that this is a better representation, *but still not exact*. We can increase the bit length but at this point we are limited by the sampling as well. Since we only have `9` samples, adding more bits won't help. 

Hence, to get a better fidelity representation of the original signal, we see that **sampling frequency** and **resolution** need to be increased, since they determine the quality of output we get from an ADC.


**Resources**

- for more details about ADC, read: [Analog-to-Digital Convertor Basics](https://www.arrow.com/en/research-and-events/articles/engineering-resource-basics-of-analog-to-digital-converters)
- an **in-depth** explanation of how ADCs work: [Iowa State CpreE 288 Course Slides](http://class.ece.iastate.edu/cpre288/lectures/lect12_13.pdf)
- more details with videos: [Analog to Digital Conversion, EE319K Univ. of Texas](https://users.ece.utexas.edu/~valvano/Volume1/E-Book/C14_ADCdataAcquisition.htm)
- Programming an ADC: [1](https://blog.embeddedexpert.io/?p=68), [2](https://labs.dese.iisc.ac.in/embeddedlab/tm4c123-adc-programming/)
<!--link rel="stylesheet" href="./custom.sibin.css"-->


# Real-Time Operating Systems

Real-Time Operating Systems (RTOS) are specialized operating systems designed to manage hardware resources, execute applications and process data in a **predictable** manner. The main aim of this focus on "predictability" is to ensure that critical tasks complete in a **timely** fashion. Unlike general-purpose operating systems (GPOS) like Windows or Linux, which prioritize multitasking and user experience, RTOS focuses on meeting strict timing constraints, ensuring that tasks are completed within defined **deadlines**. This makes RTOS essential for systems where timing accuracy and reliability are critical, such as in embedded systems, autonomous driving, industrial automation, automotive systems, medical devices and aerospace applications, among others.

Hence, real-time systems (RTS), and RTOSes in general, have _two_ criteria for "correctness":

| criteria | description |
|------------------------|-----------------------------------------------------------------------------|
| **functional** correctness | the system should work as expected, _i.e._, carry out its intended function without errors |
| **temporal** correctness   | the functionally correct operations must be completed within a predefined timing constraint (**deadline**) |

<br>

To place ourselves in the context of this course, this is where we are:

<img src="img/stack_architecture/stack_overview.4.png" width="300">

<br>

We haven't looked at the actuation part but we will come back to it later. 

### Key characteristics for RTOS

| characteristic | description |
|----------------|-------------|
| **determinism** | primary feature of an RTOS is its ability to perform tasks within guaranteed time frames; this predictability ensures that high-priority tasks are executed without delay, even under varying system loads |
| **task scheduling** | RTOS uses advanced scheduling algorithms (e.g., priority-based, round-robin or earliest-deadline-first) to manage task execution; RT tasks are often assigned priorities and the scheduler ensures that higher-priority tasks preempt lower-priority ones when necessary |
| **low latency** | RTOS minimizes interrupt response times and context-switching overhead, enabling rapid task execution and efficient handling of time-sensitive operations (_e.g._, Linux spends **many milliseconds** handling interrupts such as disk access!) |
| **resource management** | RTOS provides mechanisms for efficient allocation and management of system resources, such as memory, CPU and peripherals, to ensure optimal performance |
| **scalability** | RTOS is often lightweight and modular, making it suitable for resource-constrained environments like microcontrollers and embedded systems |
| **reliability and fault tolerance** | many RTOS implementations include features to enhance system stability, such as error detection, recovery mechanisms and redundancy |
||

## Kernels in RTOS

As with most operating systems, the kernel provides the essential services in an RTOS. In hard real-time systems, the kernel must guarantee predictable and deterministic behavior to ensure that all tasks meet their deadlines. In this chapter we focus on kernel aspects that are _specific to RTS_.

The RTOS kernel deals with,

1. [task management](#tasks-jobs-threads)
2. [communication and synchronization](#inter-task-communication-and-synchronization)
3. [memory management](#memory-management)
4. [timer and interrupt handling](#timer-and-interrupt-management)
5. [performance metrics](#kernel-performance-metrics)


### Tasks, Jobs, Threads

The design of RTOSes (and RTS in general) deal with **tasks**, **jobs** and, for implementation-specific details, **threads**. 

A real-time **task**, $\tau_i$ is defined using the following parameters: $(\phi_i, p_i, c_i, d_i)$ where,

| Symbol | Description |
| ------ | ----------- |
| $\phi_i$ | Phase (offset for the first job of a task) |
| $p_i$    | Period |
| $c_i$    | Worst-case execution time |
| $d_i$    | Deadline |
||

Hence, a real-time tast _set_ (of size '_n_') is collection of such tasks, _i.e.,_ $\tau = {\tau_1, \tau_2, ... \tau_n}$. Given a real-time task set, the _first_ step is to check if the task set is **schedulable**, _i.e.,_ check whether all **jobs** of a task will meet their deadlines (a **job** is an **instance** of a task). For this purpose, multiple **schedulability tests** have been developed, each depending on the scheduling algorithm being used.

> - remember that task is a set of parameters.
> - We "release" multiple "_jobs_" of each task, each with its own deadline
> - if all jobs of all tasks meet their deadlines, then the system remains _safe_.

A **thread**, then, is an **implementation** of task/job -- depending on the actual OS, it could be either, or both. 

At a high level, here is a comparison between tasks, jobs and threads (**note:** these details may vary depending on the _specific_ RTOS):

| **aspect** | **task** | **job**| **thread** |
|-------------|---------|--------|-------------|
| **definition** | a task is a **unit of work** that represents a program or function executing in the RTOS | a job is a **specific instance** or execution of a task, often tied to a particular event or trigger | a thread is the **smallest unit of execution** within a task, sharing the task's resources |
| **granularity** | coarse-grained; represents a complete function or program | fine-grained; represents a single execution of a task | fine-grained; represents a single flow of execution within a task |
| **resource ownership** | owns its resources (e.g., stack, memory, state) | does not own resources; relies on the task's resources | shares resources (e.g., memory, address space) with other threads in the same task |
| **scheduling** | scheduled by the RTOS kernel based on priority or scheduling algorithm | not directly scheduled; executed as part of a task's execution | scheduled by the RTOS kernel, often within the context of a task |
| **concurrency** | tasks run concurrently, managed by the RTOS scheduler | jobs are sequential within a task but may overlap across tasks | threads run concurrently, even within the same task |
| **state management** | maintains its own state (e.g., ready, running, blocked) | state is transient and tied to the task's execution | maintains its own state but shares the task's overall context |
| **isolation** | high isolation; tasks do not share memory or resources by default **++** | no isolation; jobs are part of a task's execution | low isolation; threads share memory and resources within a task |
| **overhead** | higher overhead due to separate stacks and contexts | minimal overhead, as it relies on the task's resources | moderate overhead, as threads share resources but require context switching |
| **use case** | used to model independent functions or processes (e.g., control loops) | used to represent a single execution of a task (e.g., processing a sensor reading) | used to parallelize work within a task (e.g., handling multiple i/o operations) |
| **example** | a task for controlling a motor | a job for processing a specific motor command | a thread for reading sensor data while another thread logs the data |
||

(**++** sometimes tasks **do** contend for resources, so we need to mitigate access to them, via locks, semaphores, etc. and then have to deal with thorny issues such as **priority inversions**)

A task is often described using a **task control block** (TCB):

<img src="img/rtos/tcb_sequence_png/tcb_12.png">


Tasks typically cycle through a set of states, for instance (taken from the [FreeRTOS](https://www.freertos.org/Documentation/02-Kernel/02-Kernel-features/01-Tasks-and-co-routines/02-Task-states) real-time OS):

<img src="img/rtos/free_rtos/freertos_taskstate.gif" width="300">

<br>

While the `READY`, `RUNNING` and `BLOCKED` states are similar to those in general-purpose operating systems (GPOS), _periodic_ RTOSes must introduce an additional state: **`IDLE`** or **`SUSPENDED`**:

- periodic task enters this state when it (rather one 'job') completes its execution &rarr; has to wait for the beginning of the next period
-  to be awakened by the timer (_i.e.,_ to launch the next instance/job), the task must notify the end of its cycle by executing a specific system call, `end cycle` &rarr; puts the job in the IDLE state and assigns the processor to another ready job
- at the right time, each periodic task in IDLE state &rarr; awakened by kernel and inserted in the ready queue

This operation is carried out by a routine **activated by a timer** &rarr; verifies, at each tick, whether some task(job) has to be awakened. 

TCBs are usually managed in kernel **queues** (the implementation details may vary depending on the particular RTOS).

**Context Switch Overheads**:

One of the main issues with multitasking and preepmtion is that of **context switch overheads**, _i.e.,_ the time and resources required to switch from one task to another. For instance, consider this example of two tasks running on an ARM Cortex-M4:

```c
void Task1(void) {
    while(1) {
        // Task 1 operations
        LED_Toggle();
        delay_ms(100);
    }
}
```

and

```C
void Task2(void) {
    while(1) {
        // Task 2 operations
        ReadSensor();
        delay_ms(200);
    }
}
```

When switching between Task1 and Task2, an RTOS might need to:

- save `16` general-purpose registers
- save the program counter and stack pointer
- update the memory protection unit settings
- load the new task's context (program into memory, registers, cache, _etc._)

So, on the ARM Cortex-M4, 

| effect | cost|
|--------|-------------|
| basic context switch | `200-400` CPU cycles |
| cache and pipeline effects, total overhead | `1000+` cycles |
| frequent switching (e.g., every `1 ms`) | could consume `1-2%` of CPU time! |
||


These costs can add up, especially if the system has,

- many RT tasks and frequent **preemption**
- high-frequency/short period jobs that execute frequently
- if tasks contend with each other for shared resources

Hence and RTOS must not only be cognizant of such overheads but also **actively manage/mitigate** them. Some strategies could include:

1. **better task/schedule design**: _e.g.,_ group related operations to reduce context switches

```C
void Task_Sensors(void) {
    while(1) {
        // Handle multiple sensors in one task
        ReadTemperature();
        ReadPressure();
        ReadHumidity();
        delay_ms(500);
    }
}
```

2. **priority-based scheduling**: _e.g.,_ high priority task gets more CPU

```C
void CriticalTask(void) {
    // Set high priority
    setPriority(HIGH_PRIORITY);
    while(1) {
        ProcessCriticalData();
        delay_ms(50);
    }
}
```

3. **optimizing memory layouts**: _e.g._, align task stacks to cache line boundaries

```C
#define STACK_SIZE 1024
static __attribute__((aligned(32))) 
uint8_t task1_stack[STACK_SIZE];
```

**Note:** these are not comprehensive and other strategies could be followed, for instance **avoiding multitasking altogether**! All functions could be implemented in a **single** process that runs a giant, infinite loop known as a [**cyclic executive**](https://my.eng.utah.edu/~cs5785/slides-f10/22-1up.pdf). Newer RTOSes shun ths cyclic executive in favor of the multitasking model since the latter provides more flexibility, control and adaptability but many critical systems (especially older, long-running ones) still use the cyclic executive. For instance, nuclear reactors, chemical plants, _etc._

In any case, a **precise** understanding of these overheads is crucial for:

- setting appropriate task priorities
- determining minimum task periods
- calculating worst-case execution times
- meeting real-time deadlines
- optimizing system performance

There is significant (ongoing) work, both in industry as well as academia, on how to get a handle on context switch overheads while still allowing for flexibility and modularity in the development of RTS.

### (Inter-Task) Communication and Synchronization

RTOSes use various mechanisms like semaphores, mutexes, message queues and event flags for communication and synchronization between tasks. Here are some examples:

1. **Semaphores**:

- binary semaphores: work like a mutex, with values 0 or 1
- counting semaphores: can have multiple values, useful for managing resource pools

```c
// Example of binary semaphore usage
semaphore_t sem;
sem_init(&sem, 1);  // Initialize with 1

void TaskA(void) {
    while(1) {
        sem_wait(&sem);
        // Critical section
        accessSharedResource();
        sem_post(&sem);
    }
}
```

2. **Mutexes** (mutual exclusion):

- mutexes provide exclusive access to shared resources
- they include **priority inheritance** to prevent **priority inversion**

```c
mutex_t mutex;
mutex_init(&mutex);

void TaskB(void) {
    mutex_lock(&mutex);
    // Protected shared resource access
    updateSharedData();
    mutex_unlock(&mutex);
}
```

3. **Message Queues**:

- they allow **ordered data transfer** between tasks
- provide for buffering capabilities

```c
queue_t msgQueue;
queue_create(&msgQueue, MSG_SIZE, MAX_MSGS);

void SenderTask(void) {
    message_t msg = prepareMessage();
    queue_send(&msgQueue, &msg, TIMEOUT);
}

void ReceiverTask(void) {
    message_t msg;
    queue_receive(&msgQueue, &msg, TIMEOUT);
    processMessage(&msg);
}
```

4. **Event Flags**:

- enable **multiple tasks** to wait for one or more events
- support `AND`/`OR` conditions for event combinations

```c
event_flags_t events;
#define EVENT_SENSOR_DATA 0x01
#define EVENT_USER_INPUT  0x02

void TaskC(void) {
    // Wait for both events
    event_wait(&events, EVENT_SENSOR_DATA | EVENT_USER_INPUT, 
               EVENT_ALL, TIMEOUT);
    processEvents();
}
```

5. **Condition Variables**:

- tasks can wait for **specific conditions**
- used with mutexes for complex synchronization

```c
mutex_t mutex;
cond_t condition;

void ConsumerTask(void) {
    mutex_lock(&mutex);
    while(bufferEmpty()) {
        cond_wait(&condition, &mutex);
    }
    processData();
    mutex_unlock(&mutex);
}
```

<br>

Each mechanism has specific use cases:

| mechanism  | use case |
|--------|------------|
| **semaphores** | resource management and simple synchronization |
| **mutexes** | exclusive access to shared resources |
| **message queues** | data exchange and task communication |
| **event flags** | multiple event synchronization |
| **condition variables** | complex state-dependent synchronization |
||

Common considerations:

1. Priority Inversion Prevention: a high-priority (HP) task is **indirectly preempted** by a lower-priority (LP) task; HP &rarr; needs resource (R); R held by &rarr; LP, LP preempted by medium-priority (MP) task. So **HP waits for MP** &rarr; inversion of priorities! We will discuss solutions (priority inheritance/priority ceiling) later.
2. Deadlock Avoidance: tasks are *permanently blocked** waiting on resources from each other; $\tau_1$ holds resource $R_A$ and waits for $R_B$; $\tau_2$ holds resource $R_B$ and waits for $R_A$.
3. Timeout Handling: _every_ synchronization mechanism should have a **timeout** to avoid indefinite blocking of critical tasks. 
4. Error Handling: detecting errors and handling them in a **robust** manner is critical to maintain system reliability; RTOSes use _retry mechanisms_, _logging_ and, most importantly, have **clear recovery procedures** for failure scenarios.

These considerations are crucial for ensuring system reliability, maintaining real-time performance, preventing system deadlocks, managing system resources effectively and handling error conditions gracefully.


### Memory Management

Real-time systems require **predictable memory allocation and deallocation** to avoid delays or fragmentation. Hence, they often use **limited memory management techniques** often eschewing even the use of dynamic memory allocation in favor of **static memory allocation**. For instance, many RTS don't even use `malloc()` or `new` (_i.e.,_ no heap allocated memory) and very often avoid garbage collection. The main goal is for tight control of the memory management &rarr; this makes _timing behavior more predictable_. Hence, the following become easier:

- wcet analysis
- schedulability and other analyses
- runtime monitoring and management
- recovery/restart

Some **goals** for memory management in RTOSes:

1. predictable execution times for memory operations
2. fast allocation/deallocation
3. minimal fragmentation, if any
4. protection mechanisms between tasks

In fact, to achieve these goals, many RTSes **don't even use caches** since they can be a major source of non-determinism in terms of timing behavior, _e.g.,_

> if we cannot **exactly calculate** when some data/code will hit/miss in cache, then we cannot estimate its true timing behavior, leading to a lot of uncertainty &rarr; **bad**!

Some RTSes use [**scratchpads**](http://www.irisa.fr/alf/downloads/puaut/papers/date07.pdf) since they provide cache-like performance but have higher predictability since the data onboarding/offloading is **explicitly managed** (either by the program or the [RTOS](https://cs-people.bu.edu/rmancuso/files/papers/SPM-OS_RTSJ19.pdf)).

**Some common memory-management techniques for RTOSes**:

1. **static memory allocation**: all memory used is allocated/deallocated at **compile time**.
2. **memory pools**: fixed-size blocks are pre-allocated for specific purposes &rarr; fragmentation and provides deterministic allocation times.
3. **careful stack management**: careful sizing/placing/management of the stack
4. **limited heap memory**: using "safe" versions of `malloc()` for instance
5. **memory protection**: using hardware such as memory protection units (MPUs)
6. **memory partitioning**: explicitly partition memory/caches so that tasks cannot read/write in each others' memory regions
7. **runtime mechanisms**: such as memory usage monitoring, leak detection and managing the fragmentation

> Of course, each of these mechanisms have their own problems and a deliberation on those is left as an exercise for the reader. 

### Timer and Interrupt Management

Timer and interrupt management are crucial components of an RTOS, ensuring that tasks are **executed at precise intervals** and that the system responds promptly to (internal and) external events. The role between timers and interrupts is closely related, since they offer the very **basic** timing mechanism in RTOSes (from [Hard Real-Time Computing Systems: Predictable Scheduling Algorithms and Applications](https://link.springer.com/book/10.1007/978-1-4614-0676-1)): 

> to generate a **time reference**, a timer circuit is programmed to interrupt the processor at a **fixed rate** and the internal system time is represented by an integer variable, which is reset at system initialization and is incremented at each **timer interrupt**. The interval of time with which the timer is programmed to interrupt defines the unit of time in the system; that is, the minimum interval of time handled by the kernel (time resolution). The unit of time in the system is also called a system **`tick`**.

<br>

Timers, in general, play important roles in such systems, _viz.,_

| role |description |
|------|------------|
| **task scheduling** | enable periodic execution of tasks |
| **timeout management** | prevent indefinite blocking of resources |
| **event timing** | measure intervals between events |
| **system timing** | maintain system clock and timestamps |
| **watchdog functions** | monitor system health and detect lockups |
||

<br>

Typically these systems have the following _three_ types of timers:

|type | properties |
|-----|------------|
| **hardware** |- direct access to hardware timing resources<br>- highest precision and accuracy<br>- limited in number (hardware dependent)<br>- used for critical timing functions|
| **software** |- implemented in software, using hardware timer as base<br>- more flexibility, less precise<br>- limited only by memory<br>- more suitable for non-critical timing functions|
| **system `tick`** |- **core** timer for RTOS <br> - drives task scheduling <br> - fixed frequency|
||

<br>

<img src="img/mermaid_figs/6.realtime.system_tick.png" width="400">

There are various **design considerations** for timers in an RTOS, _viz.,_

1. **resolution** &rarr; the smaller the resolution, the higher the system/hardware/software/runtime overheads
2. **accuracy** &rarr; need to understand and manage _drift_ and _jitter_; timers may need to be calibrated often++
3. **power consumption** &rarr; more accurate/high-precision a timer, higher the power consumption; also the `tick` can result in significant power consumption if not implemented/managed well

(++ drift indicates a _gradual, long-term change_ in the timer's frequency over time, whereas jitter refers to _short-term, random fluctuations_ in the timing of individual clock pulses)

**Interrupt Latencies** &rarr; time from when an interrupt occurs to when the corresponding interrupt service routine (ISR) starts executing. As interrupts are integral to the operation of an RTOS, from the implementation of the system `tick` to notifcations of internal (watchdog timers) and external events (new sensor data), it is important to **minimize interrupt latencies**.  

Optimization Techniques (to minimize latencies):

- minimize interrupt frequency &rarr; oftean an RTOS will disable interrupts in critical sections
- efficient timer and interrupt queue management &rarr; "nesting" interrupts, 
- power-aware timing strategies &rarr; "_tickless_" operating systems have been tried
- optimize ISRs &rarr; keep them short, use other methods ([deferred procedure calls](https://www.osr.com/nt-insider/2009-issue1/deferred-procedure-call-details/) or "[bottom halves](http://www.cs.otago.ac.nz/cosc440/labs/lab08.pdf)").


### Kernel Performance Metrics

> Essentially, the kernel must be designed to **minimize jitter** and ensure that all operations have bounded and predictable execution times.

Hence, we can try to evaluate whether an RTOS kernel meets these goals using the following metrics (**note**: not exhaustive):

| metric | description |
|------------|-------------|
| **interrupt latency** | the time taken to respond to an interrupt |
| **context switch time** | time to switch between tasks |
| **dispatch latency** | time difference between task being ready and when it starts executing |
| **throughput** | number of tasks?operations kernel can handle per unit time |
||



## Examples of RTOS

| **name** | **description** | **features** |
|----------|-----------------|--------------|
| [FreeRTOS](https://www.freertos.org) | a widely used, **open-source** RTOS for embedded systems | small footprint, portable, supports a wide range of microcontrollers |
| [VxWorks](https://www.windriver.com/products/vxworks) | **commercial** RTOS used in aerospace, defense, applications | high reliability, real-time performance, and support for multi-core processors |
| [QNX](https://blackberry.qnx.com/en) | a **commercial** RTOS known for its reliability and use in automotive and medical systems | microkernel architecture, high security, support for posix apis |
| [Zephyr](https://www.zephyrproject.org) | **open-source** RTOS designed for IoT and Edge devices | modular, scalable, supports a wide range of hardware architectures |
||

<br>

Why is Linux not on the list? While it has many (increasing) [list of real-time features](https://www.zdnet.com/article/real-time-linux-leads-kernel-v6-12s-list-of-new-features/), it is still far from a **hard real-time system**, mainly due to its complexity. It is difficult to analyze WCETs on Linux or completely control its timers &rarr; the list is endless. It still sees use in many real-time and embedded systems and we will (brielfy) explore its real-time capabilities soon.


### FreeRTOS

As mentioned earlier, FreeRTOS is one of the most popular open-source RTOS options, widely used in embedded systems due to its simplicity, portability and extensive community support. It supports,

- creation of multiple tasks, each with its own priority
- preemptive and cooperative scheduling
- mechanisms like queues, semaphores, and mutexes for communication and synchronization between tasks
- several memory management schemes, including heap_1, heap_2, heap_3, heap_4, and heap_5, to suit different application requirements
-  **highly portable** and supports a wide range of microcontrollers and development boards, including ARM Cortex-M, ESP32 and STM32
-  a large and active community, with [extensive documentation, tutorials and examples available online

Here is an example that uses FreeRTOS to blink the LEDs on a microcontroller:

```C
#include <FreeRTOS.h>
#include <task.h>
#include <gpio.h>

// Task to blink an LED
void vBlinkTask(void *pvParameters) {
    while (1) {
        GPIO_TogglePin(LED_PIN);  // Toggle LED
        vTaskDelay(pdMS_TO_TICKS(500));  // Delay for 500ms
    }
}

int main(void) {
    // Initialize hardware
    GPIO_Init(LED_PIN, GPIO_MODE_OUTPUT);

    // Create the blink task
    xTaskCreate(vBlinkTask, "Blink", configMINIMAL_STACK_SIZE, NULL, 1, NULL);

    // Start the scheduler
    vTaskStartScheduler();

    // The program should never reach here
    for (;;);
}
```

**Resources**:

1. [FreeRTOS Documentation](https://www.freertos.org/Documentation/RTOS_book.html)
2. [FreeRTOS Tutorials](https://www.freertos.org/Why-FreeRTOS/Features-and-demos/RAM_constrained_design_tutorial/Real-time-application-design)
3. [**Raspberry Pi and FreeRTOS**](https://forums.freertos.org/t/using-freertos-with-the-raspberry-pi-pico-blog-series/16497) \[[GitHub Repo](https://github.com/aws-iot-builder-tools/freertos-pi-pico)\]



### Linux+Real-Time

As mentioned earlier, Linux, as a general-purpose operating system, is not inherently a real-time operating system (RTOS). However, it does provide several features and mechanisms that can be used to achieve real-time performance, especially when combined with real-time patches or specialized configurations.

Some of the real-time features of Linux include:

- **[Preempt-RT Patch](https://wiki.linuxfoundation.org/realtime/start)**: a set of patches that convert the Linux kernel into a fully preemptible kernel, reducing latency and improving real-time performance; the Preempt-RT patch achieves this by:

    - making almost **all kernel code preemptible**: allows higher-priority tasks to preempt lower-priority tasks, even when the lower-priority tasks are executing kernel code
    - **converting interrupt handlers to kernel threads**: reduces time spent with interrupts disabled, for better predictability and lower latency
    - **implementing priority inheritance**: helps prevent priority inversion by temporarily elevating priority of lower-priority tasks holding a resource needed by higher-priority tasks
    - **reducing non-preemptible sections**: minimizes time during which preemption is disabled, further reducing latency
    - **enhancing timer granularity**: allows for more precise timing and scheduling of tasks, crucial for real-time applications

    the Preempt-RT patch is widely used in industries such as telecommunications, industrial automation and audio processing. It is actively maintained and supported by the Linux Foundation's [Real-Time Linux](https://wiki.linuxfoundation.org/realtime/rtl/start) (RTL) collaborative project

- **[Real-Time scheduling policies](https://man7.org/linux/man-pages/man7/sched.7.html)**: support for real-time scheduling policies such as `SCHED_FIFO` and `SCHED_RR`, which provide deterministic scheduling behavior
- **[High-resolution timers](https://www.kernel.org/doc/html/latest/timers/hrtimers.html)**: support for high-resolution timers that allow for precise timing and scheduling of tasks
- basic **[priority inheritance](https://www.kernel.org/doc/Documentation/locking/priority-inheritance.txt)**: mechanism to prevent priority inversion by temporarily elevating the priority of lower-priority tasks holding a resource needed by higher-priority tasks
- **[CPU isolation](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.html#isolcpus)**: ability to isolate CPUs from the general scheduler, dedicating them to specific real-time tasks; also pinning processes to certain cores
- **[Threaded interrupts](https://www.kernel.org/doc/Documentation/core-api/genericirq.rst)**: support for handling interrupts in kernel threads, reducing interrupt latency and improving predictability
- **[Memory management](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_for_real_time/8/html/understanding_rhel_for_real_time/assembly_memory-management-on-rhel-for-real-time-_understanding-rhel-for-real-time-core-concepts#con_demand-paging_assembly_memory-management-on-rhel-for-real-time-)** techniques: such as [**memory locking**](https://linux.die.net/man/2/mlock) to prevent pages from being swapped, the use of "[**huge**](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/performance_tuning_guide/s-memory-transhuge)" pages and memory [**pre-allocation**](https://docs.kernel.org/core-api/memory-allocation.html)
- **[Control groups (cgroups)](https://www.kernel.org/doc/Documentation/cgroup-v1/cgroups.txt)**: mechanism to allocate CPU, memory and I/O resources to specific groups of tasks, ensuring resource availability for real-time tasks

These features, when properly configured, can help achieve real-time performance on Linux, making it suitable for certain real-time and embedded applications.


### Raspberry Pi OS+Real-Time

The [Raspberry Pi OS](https://www.raspberrypi.com/software/) can also be made "real-time" in the same manner as decribed above, since it is a Linux variant.

Though, there are some attempts at getting the Pi to behave in a real-time fashion, _e.g.,_: [**1**](https://www.socallinuxexpo.org/sites/default/files/presentations/Steven_Doran_SCALE_13x.pdf), [**2**](https://all3dp.com/2/rtos-raspberry-pi-real-time-os/#google_vignette), [**3**](https://floating.io/2023/04/raspberry-pi-in-real-time/).

<br>

## Robot Operating System (ROS)

ROS is an **open source middleware** framework built for robotics applications. The main goal &rarr; develop **standards** for robotic software. ROS provides many **reusable modules** for developing robotic applications. 

Embedded/autonomous programs that do simple tasks (or operate with a single sensor/motor) are relatively easy to program. As more sensing, actuation, functionality is added (consider a larege industrial robot or even an autonomous car), programs quickly become quite complex -- coordination of the data and system states becomes challenging. 

<img src="img/rtos/ros/ros.complexity.webp" width="400">

<br>

ROS helps to develop and **scale** such applications and also **manages communications** between various parts of the software. As mentioned earlier, ROS is [**middleware**](https://www.redhat.com/en/topics/middleware/what-is-middleware):

> Middleware is a software layer that connects the operating system to applications, data, and users. It provides common services and capabilities, like single-sign on (SSO), easy communication/coordination (like ROS) or application programming interface (API) management. Developers can rely on middleware to provide consistent, simplified integrations between application components. This frees up developers to build core features of applications, rather than spend time connecting those features to different endpoints and environments, including legacy systems.

At a high level, ROS,

- creates a _separation_ of code blocks &rarr; into reusable blocks
- provides _tools_ &rarr; easy communication between sub-programs
- is _language agnostic_ &rarr; allows different components to be written in, say Python and C and yet communicate using the **ROS communication protocol**

A simple example: [control of a robotic arm+camera](https://dilipkumar.medium.com/ros-v1-robot-operating-system-88039990e913):

<img src="img/rtos/ros/ros.robot_camera_example.webp" width="400">

<br>

To write a ROS application to control this robotic arm, we first create a few **subprograms**: 

- one for the camera &rarr; `node`
- another for &rarr; `motion planning`
- one for &rarr; `hardware drivers`
- finally one for &rarr; `joystick`

Now we use ROS &rarr; **communication** between these nodes. 

ROS even provides **plug and play libraries** for designing your system, _e.g.,_ [inverse kinematics libraries](https://moveit.ai/moveit/ros2/2020/02/18/moveit-2-beta-feature-list.html), [trajectory planning for robotic arms](https://roboticseabass.com/2024/06/30/how-do-robot-manipulators-move/), _etc._

### ROS Components

Some important **components** of ROS:

<img src="img/mermaid_figs/6.realtime.ros_architecture_legends.png" width="400">
<br>
<img src="img/mermaid_figs/6.realtime.ros_architecture.png" width="400">

1. [node](http://wiki.ros.org/Nodes)

- a process that performs **computation** (a program/subprogram)
- combined together into a graph
- communicate via "topics"
- operate at a fine-grained scale
- a full system will have _multiple_ nodes, _e.g.,_
    - one node controls a laser range-finder
    - one Node controls the robot's wheel motors
    - one node performs localization
    - one node performs path planning
    - one node provides a graphical view of the system

The use of nodes has several benefits such as **fault tolerance**, **reduced complexity** and **modularity**. 

2. [topics](http://wiki.ros.org/Topics)

- they're **named buses** over which nodes exchange "messages"
- **anonymous publish/subscribe semantics** &rarr; decouples production of information from its consumption
- nodes are not aware of who they are communicating with
- nodes that are interested in data **subscribe** to the _relevant topic_
- nodes that _generate_ data **publish** to the relevant topic
- can be **multiple** publishers and subscribers to a topic
- topic is **strongly typed** by publisher &rarr; nodes can only receive messages with a matching type

Topics are meant for _unidirectional_, _streaming_ communication. ROS includes other mechanisms such as [services](http://wiki.ros.org/Services) and [parameter servers]http://wiki.ros.org/Parameter%20Server) for different types of communciations.

3. [messages](http://wiki.ros.org/Messages)

- nodes communicate with each other by publishing messages to topics
- simple text files
- simple data structure &rarr; **typed fields**
- support standard primitives (`int`, `float`, `boolean`)
- can include arbitrarily nested `structs` and `arrays`
- nodes can exchange &rarr; `request` an `response` messages

A simple ROS message:

```ros
std_msgs/Header header
  uint32 seq
  time stamp
  string frame_id
geometry_msgs/Point point
  float64 x
  float64 y
  float64 z
```

Example: [our first ROS message](https://classes.cs.uchicago.edu/archive/2022/spring/20600-1/ros_intro.html).

4. [ROS Master](http://wiki.ros.org/Master)

- provides naming and registration services to the rest of the nodes in the ROS system
- also runs the [parameter server](http://wiki.ros.org/Parameter%20Server) &rarr; a shared, multi-variate dictionary that is accessible via network APIs, used by nodes to **store/retrieve parameters**
- tracks publishers and subscribers to topics as well as services
- enable individual ROS nodes to locate one anothe
- once located, they communicate in a **peer-to-peer** fashion

Example:

1. consider two nodes &rarr; `camera` node and `image_viewer` node
2. `camera` notifies `master` &rarr; wants to publish images on the topic, `images`

<img src="img/rtos/ros/ROS_master_example_english_1.png">

3. no one is subscribing to the topic, yet &rarr; **no images sent**
4. `image viewer` &rarr; subscribe to `images` topic

<img src="img/rtos/ros/ROS_master_example_english_2.png">

5. topic, `images` has both &rarr; publisher and subscriber
6. `master` notifies both &rarr; of each others' existence

<img src="img/rtos/ros/ROS_master_example_english_3.png">

7. both start **communicating with each other**, directly

<br>

A more intricate example of the same:

<img src="img/mermaid_figs/6.realtime.ros_publish_subscribe.png" width="400">

5. [ROS transform](http://wiki.ros.org/tf2)

- robotic system typically has many 3D coordinate frames that change over time
    - _e.g.,_ world frame, base frame, gripper frame, head frame, _etc._
- lets the user keep track of multiple coordinate frames over time
- maintains the relationship between coordinate frames &rarr; manages **spatial relationships** 
- in a tree structure buffered in time
- lets the user transform points, vectors, _etc._ &rarr; at any desired point in time 
- **distributed** &rarr; coordinate frames of robot available to **all** ROS components on any computer in the system
- sensor fusion, motion planning, and navigation
- organizes all coordinate frames and their relationships into a **transform tree**

An example of a ROS transform and tree:

<img src="img/mermaid_figs/6.realtime.ros_transform.png" width="400">


### ROS and Real-time?

ROS (the first version) is **not** real-time. Hence, systems that requires **hard real-time guarantees** shoud not use it. But ROS can be itegrated into systems that require _some_ latency guarantees. If needed, ROS can be run on top of the `RT_PREEMPT` real-time patch on Linux. In addition, **specific nodes** can be designed to handle real-time functions or programmed to behave as real-time control systems. 

If better real-time guarantees are required on ROS, then [**ROS 2**](https://roscon.ros.org/2015/presentations/RealtimeROS2.pdf) if your best bet. 

**Resources**: more information on real-time and ROS2 can be found at [RT ROS2 Xilinx](https://xilinx.github.io/KRS/sphinx/build/html/docs/features/realtime_ros2.html) and [RT ROS Github](https://github.com/ros-realtime).


### Ros+Navio2

We use ROS (the original version, not ROS2) in our class. **Note:** while ROS has no real-time capabilities, one some embedded systems, if it _fast enough_ that we can use it to control safety-critical systems such as drones and other small autonomous systems. 

In fact, the basic Raspbian image comes installed with ROS. We can use it communicate between the Navio2 and the controller running on the Pi to exchange critical information, _e.g._, sensor data. 

<img src="img/rtos/ros/ros.ardupilot_navio.png" width="400">

**Resources**: please read the [step-by-step instructions](https://docs.emlid.com/navio2/ros/) on how to connect/use the Navio2 and the Pi using ROS.

<!--t
 rel="stylesheet" href="./custom.sibin.css"-->


# Scheduling for Real-Time Systems

Consider an engine control system that cycles through the various phases of operation for an [automotive engine](http://automobile-us.blogspot.com):

<img src="img/scheduling/engine_animation.gif">

<br>

This system **periodically** cycles through multiple tasks, _viz._,

1. air intake
2. pressure
3. fuel injection+combustion
4. exhaust

If we correlate this to task "activations", then we may see the [following](https://retis.sssup.it/~a.biondi/papers/ERIKA_AVR_RTAS16.pdf):

|||
|-----|-----|
|<img src="img/scheduling/engine_animation.gif" width="180">|<img src="img/scheduling/angular_task.png" width="300">|
||

This is a (somewhat) simple execution model known as the [cyclic executive](#cyclic-executives) that we shall return to later. Hence, there is a **direct** correlation between the physical aspects of a real-time and autonomous system and issues such as scheduling. 


## Real-Time Models

Most real-time systems can be classified into:

|property|hard|soft|
|----|----|--------|
|"_usefulness_" of results| <img src="img/scheduling/hard_soft/pngs/hard_rts.png" width="200">| <img src="img/scheduling/hard_soft/pngs/soft_rts.png" width="200">|
|optimality criterion| **all** deadlines must be satisfied | **most** deadlines must be met |
| examples| sensor readings, vehicular control | video decoding, displaying messages|
||


There are many ways to **model** a real-time system:

1. [**workload** model](#workload-model) &rarr; describes applications supported by system, using
    - functional parameters
    - temporal parameters
    - precedence constraints and dependencies
2. [**resource** model](#resource-model) &rarr; describes system resources available to applications
    - modeling resources, e.g., processors, network cards, etc.
    - resource parameters
3. [**algorithms**](#scheduling-and-algorithms) &rarr; defines how application uses resources at all times
    - scheduling policies
    - other resource management algorithms 


### Workload Model

We have already discussed [tasks vs. jobs vs. thread](#tasks-jobs-threads) earlier so we understand how to model computation. We also discussed how actual execution is modeled (via threads). 

Let us focus on **jobs** and some of their properties:

<img src="img/scheduling/jobs/job.final.svg" width="400">

**note** &rarr; deadlines and periods don't have to match, but they **usually** do, _i.e., $D = P$

| property/parameters | description  |
|----------|--------------|
| **temporal** | timing constraints and behavior |
| **functional** | intrinsic properties of the job |
| **resource** | resource requirements|
| **interconnection** | how it depends on other jobs and how other jobs depend on it |
||

As discussed earlier, we need to get a good understanding of the [wcet](l#the-wcet-problem) of jobs.


### Utilization

One of the important ways to understand the **workload requirements** for a **task** is to compute,

> how much **utilization** is taken up by **all** jobs of the task?

One might ask: if there are (potentially) an _infinite_ number of jobs for each task, since they're periodic++ and long running, then how can one campute the utilization?

> Recall that a **periodic** function is of the type &rarr; $f(t) = f(t+T)$
>
> where $T$ is the "period"

**Note:** utilization is **not** the time taken by a task (or its jobs). It is, 

> the **fraction** of the processor's total available utilization that is soaked up by the jobs of a task

Hence, the utilization for a **single** task is,

$$ U_i = \frac{c_i}{T_i} $$

where,

| symbol | description |
|--------|-------------|
| $c_i$  | wcet of the task |
| $T_i$  | period of the task |

Now, we can compute the utilization for the **entire task set**,

$$ U = \sum_{i=1}^{n} U_i = \sum_{i=1}^{n} \frac{c_i}{T_i} $$

**Simple Exercise**: what is the total utilization for the following task set?

| Task | c | T |
|------|---|---|
| τ1   | 1 | 4 |
| τ2   | 2 | 5 |
| τ3   | 5 | 17 |
||

> what does it mean if $U > 1$? 


#### Precedence Constraints

Jobs can be either **precedence constrained** or **independent** &rarr; we can use directed acyclic graphs (DAGs) to specify/capture these constraints. 

For instance, 
$ J_a \prec J_b$ implies,

- $J_a$ is a **predecessor** of $J_b$
- $J_b$ is a **successor** of $J_a$

$ J_a \to J_b$ implies

- $J_a$ is an **immediate** predecessor of $J_b$

Consider the following example:

|dag| relationships|
|-----|-----|
|<img src="img/scheduling/jobs/job_precedence.png" width="150"> |  $J_1 \prec J_2$ <br> $ J_1 \to J_2$ <br> $J_1 \prec J_4$ <br> $J_1 \not\to J_4$|
||


Here is a more realistic example &rarr; the precedence constraints in an **autonomous driving system**:

<img src="img/scheduling/jobs/autonomous_precedence_constraints_rtss2021.png" width="400">


### Resource Model

A "resource" is some structure used by task &rarr; advance execution.

Type of resources:

- **active** &rarr; e.g., processors (they execute jobs)
    - every job &rarr; one or more processors
    - same type if functionally identical and used interchangeably
- **passive** &rarr; _e.g.,_ files, network sockets, _etc._
- **private** vs **shared**

We have already discussed [resource sharing and synchronization](#inter-task-communication-and-synchronization) earlier &rarr; mutexes, locks, _etc._ Esentially there is a need for **mutual exclusion** that is guaranteed via one of these methods or by the use of [critical sections](https://cs.gmu.edu/~rcarver/ModernMultithreading/LectureNotes/Chapter2Notes.pdf).


### Scheduling and Algorithms

Before we proceed, we need to understand &rarr; **preemption**:

> preemption is the process of **suspending a running task** in **favor of a higher priority task**.

<img src="img/scheduling/preemption.png" width="400">

Most OS (real-time & non real-time) allow preemption since they allow,

- greater flexibility in constructing schedules
- exception handling
- interrupt servicing

Preemptions, among others, help define a variety of **scheduling events**; essentially, these are the time when the **scheduler is invoked**:

- in a _fully_ preemptive system &rarr; task arrival, task completion, resource reauest, resource release, interrupts and exceptions, _etc._ 
- in a _non-preemptive_ system &rarr; task completion
- in _limited_ preemptive systems &rarr; predefined preemptions points, _e.g.,_ POSIX thread cancel (`pthread_testcancel()`)


#### Task Schedule

We have been talking about "scheduling" all this while so it is time to formally define what a **schedule** is.

Given &rarr; a set of jobs, $J = \{ J_1, J_2,...,J_n \}$

> A schedule &rarr; an **assignment** of Jobs to the CPU, so that each task can execute till completion.


## Schedulers

Finally, we get to the main topic at hand &rarr; schedulers and scheduling! Historically there have been many scheduling policies developed for a variety of systems, _e.g.,_ [FIFO](https://www.geeksforgeeks.org/program-for-fcfs-cpu-scheduling-set-1/), [round robin](https://www.geeksforgeeks.org/program-for-round-robin-scheduling-for-the-same-arrival-time/), [time sharing](https://dl.acm.org/doi/abs/10.1145/1460833.1460871), _etc._

Here is a good comparison of the various types of (historical) CPU/OS schedulers: [CPU Scheduling in Operating Systems](https://www.geeksforgeeks.org/cpu-scheduling-in-operating-systems/).

In the realm of real-time systems, to _formally_ define a scheduling problem, we need to specify:

1. a set of **tasks**, $\tau$
2. a set of **processors**, $P$
3. a set of **resources**, $R$

Hence, the **general scheduling problem** is,

> assign processors and resources to tasks, such that the following constraints are met:
> 
> - timing constraints
> - precedence constraints
> - resource constraints

There is a [large body of literature](https://link.springer.com/book/10.1007/978-1-4614-0676-1) in the domain of real-time scheduling algorithms. In this chapter, we will focus on a few of them, _viz._,

- completely static &rarr; _e,g.,_ [cyclic executives](#cyclic-executives)
- [priority-based](#priority-based-schedulers) &rarr; static (_e.g.,_ RM) and dynamic (_e.g.,_ EDF)
- dynamic best effort

One of the main problems with the scheduling problem, as defined above (and in general), is that many variants of the problem are **intractable**, _i.e.,_ NP-Hard or even NP-Complete.

> Recall that an NP-Hard problem is one where no _known_ polynomial time algorithm exists. So, all known algorithms are superlinear or, usually, of _exponential_ time complexity!

[Will leave it to the reader to recall or look up the definition of NP-Complete.]

Since the scheduling problems may not be tractable (or "solvable" in a realistic time frame), we need to find _heuristics_ but they can be "sub-optimal". Luckily, we have a couple of **provably optimal** real-time schedulers (in the single core domain). 

**Additional, important definitions**:

|concept| definition |
|-------|------------|
| **feasibility** | schedule is feasible if all tasks can be completed by satisfying a set of specified constraints|
| **schedulable** | set of tasks is schedulable if there exists **at least one algorithm** that can produce a feasible schedule |
| **schedulability analysis** | analysis to confirm that deadlines for a set of threads can be guaranteed using a **given scheduling policy** |
||



### Cyclic Executives

In the automotive enginer example from earlier, we see that for each **cycle**, the same set of tasks **repeat** (_i.e._., "periodic behavior"). Note though that the tasks _need not_ execute in parallel -- rather, they must execute sequentially for this application. Usually such applications use a scheduling mechanism known as a "**cyclic executive**". 

Consider this simple example with three tasks:

|task|c|
|----|--|
| $T_1$ | 1|
| $T_2$ | 2|
| $T_3$ | 3|
||

How would we **schedule** this? Assuming a single processors (hence a single timeline).

<img src="img/scheduling/cyclic/pngs/cyclic1.png" width="400">

Well, the _simplest_ mechanism is to just use a **sequential** schedule,

<img src="img/scheduling/cyclic/pngs/cyclic4.png" width="400">

If, as in the case of the engine control example we saw earlier, the tasks repeat _ad infinitum_, then we see the pattern also repeating...

<img src="img/scheduling/cyclic/pngs/cyclic5.png" width="400">

Cyclic executives were common in many critical RTS, since they're **simple** and **deterministic**. An implementation could look like,

```
while(1)    // an infinite loop
{
    // Some Initialization

    Task_T1() ;

    // Some processing, maybe

    Task_T2() ;

    // Some other processing, maybe

    Task_T3() ;

    // Cleanup
}
```

**Question**: what problems, if any, can happen due to cyclic executives?

The very simplicity of such systems can also be their biggest weakness. 

1. **lack of flexibility**: as the example and code above demonstrate, once a pattern of executions is set, it cannot be changed, **unless the system is stopped, redesigned/recompiled and restarted**! This may not be possible for critical applications. Even for the engine control application in cars, this doesn't just mean stopping and restarting the car, but **re-flashing** the firmware for the engine, which is quite an involved task. 

2. **scalability**: along similar lines, it is difficult to scale the system to deal with additional issues or add functionality. 

3. **priority**: there is no way to assign priority or preemption since all tasks essentially execute a the _same priority_. Hence, if we want to deal with higher-priority events (_e.g._, read a sensor) or even _atypical_ (aperiodic/sporadic) events, such as sudden braking in an autonomous car, then a cyclic executive is not the right way to go about it.

4. **resource management**: certain tasks can corral resources and hold on to them while others may _starve_ -- leading to the system becoming unstable. For instance, even in the simple example, we see that $T_3$ can dominate the execution time on the CPU:

<img src="img/scheduling/cyclic/cyclic6.svg" width="400">

Since the system is _one giant executable_, it is difficult to stop a "runaway task" -- the entire system must be stopped and restarted, which can lead to serious problems.



### Frames

One way to mitigate _some_ of the problems with cyclic executives, is to split the resource allocation into "frames" &rarr; **fixed** chunks of time when a task can claim exclusive access to a resource, _e.g.._ the processor:

- once a frame starts, the task gets to execute _uninterrupted_
- at the end of the frame, the task _must give up_ the resource &rarr; regardless of whether it was done or not

So, if we revisit our simple example and break the processor schedule into frame sizes of `2` units, each,

<img src="img/scheduling/cyclic/cyclic6_5.frame.svg" width="400">

> why `2`? Well, it is arbitrary for now. But, as we shall see later, we can calculate a "good" frame size

Now, our schedule looks like,

<img src="img/scheduling/cyclic/cyclic8.frame.svg" width="400">

As we see from this picture, task $T_1$ doesn't end up using its entire frame and hence, can waste resources (one of the pifalls of this method).

Continuing further,

<img src="img/scheduling/cyclic/cyclic9.frame.svg" width="400">

Task $T_3$ is _forced_ to relinquish the processo at `t=6` even though it has some execution left &rarr; on account of the frame ending. Now $T_1$ resumes in its own frame. $T_3$ has to wait until `t=10` to resume (and complete) its execution:

<img src="img/scheduling/cyclic/cyclic12.frame.svg" width="400">

**Other Static/Table-Driven Scheduling**:

Cyclic executives are an example of schedulers where the tasks are fixed, _ahead of time_, and all that a scheduler has to do is to _dispatch_ them one at a time in the **exact same order**. Often the tasks are stored in a lookup table (hence the name "table-driven"). Other examples of such systems (with some prioritization and other features built in) have been built, _e.g.,_ [weighted round robin](https://par.nsf.gov/servlets/purl/10383232) &rarr; also finds use in cloud computing and networking load balancing, _etc._


### Priority-Based Schedulers

One method that overcomes the disadvantages of a completely static method is to **assign priorities for jobs as they arrive**. Hence, when a job is _released_ it gets assigned a **priority** and the scheduler then dispatches/schedules the job accordingly. Hence, it if is the highest priority job so far, it gets scheduled _right away_, by preempting any currenlty running tasks. If, on the other hand, it is not the highest priority task then it is inserted into the ready queue at the right position (priority level).

To deal with this, we need an **online scheduler**, _i.e.,_ one that is always available to make scheduling decisions -- when tasks arrive, complete, miss their deadlines, _etc._

Before we go any further, let's **update the task model** a little, to make matters simple for us. 

- as before, we have a task set comprised of $n$ **periodic** tasks, $\tau = {\tau_1, \tau_2...\tau_n}$
- deadline **is equal to** period, _i.e.,_ $T=D$; task periods are $T_1, T_2, ... T_n$
- all tasks are **independant** &rarr; no precedence or resource constraints exist
- tasks **cannot suspend** themselves (or others)
- tasks are **preemptible** by the OS &rarr; each time the highest priority task is executed (under preemptive scheduling)
- execution time of each task is **bounded** &rarr; wcet ($c_1, c_2, ... c_n$)
- tasks are released (_i.e.,_ placed into the ready queue) **as soon as they arrive**
- all kernel overheads (_e.g.,_ context switches) &rarr; assumed to be **zero**

While these may seem to be overly simplifying, they still fit the model of many systems and help us develop _fundamental results_. And we can always add them back one-by-one and still retain the correctness of the theoretical results we develop, while making the system more realistic. 

Now, in the real of **online, priority-driven** schedulers, we have **two** options:

| priority assignment | algorithms |
|---------------------|------------|
| **static** | [Rate-Monotonic](#rate-monotonic-scheduler-rm) (RM), Deadline-Monotonic (DM) |
| **dynamic** | [Earliest-Deadline First](#earliest-deadline-first-scheduler-edf), Least-Slack Time (LST) |
||

<br>

Let's look at one of each (the most popular ones), _viz._ the [Rate-Monotonic](#rate-monotonic-scheduler-rm) (RM) and [Earliest-Deadline First](#earliest-deadline-first-scheduler-edf) schedulers. Note that both were first described and analyzed in a **seminal Computer Science Paper**, that has since become one of the most cited and influential papers in the field: [Scheduling Algorithms for Multiprogramming in a Hard- Real-Time Environment](https://dl.acm.org/doi/10.1145/321738.321743) by Liu and Layland.

Interestingly, both of these algorithms are **provably optimal**, _i.e.,_ no other static or dynamic algorithm can do better than RM and EDF respectively! Not bad for the first paper in the area -- talk about setting a high bar, or rather _bound_!

#### Rate-Monotonic Scheduler (RM)

The Rate-Montonic priority assignment algorithm assigns **priority based on the period of the task** &rarr; shorter the period, the higher the priority!

Consider the following example:

|task|c|T|
|----|--|----|
| $\tau_1$ | 2| 4 |
| $\tau_2$ | 2| 5 |
| $\tau_3$ | 1| 10 |
||

So, based on the RM algorithm, the priority will be:

$$\tau_1 > \tau_2 > \tau_3$$

since, $T_1 < T_2 < T_3$.

The question now is whether the above task set is **schedulable**? Let us use our previous utilization-based check, _i.e._,

$$U = \sum_{i=1}^{n} \frac{c_i}{T_i}$$

So, plugging in the numbers, we get,

$$ U = \frac{1}{2} + \frac{1}{4} + \frac{2}{6} = 0.5 + 0.4 + 0.1 = 1.0 $$

Our test was: $U \le 1$. So, this task set is...schedulable? Let us see -- by plotting it on the timeline:

<img src="img/scheduling/rm_unschedulable/pngs/rm.final.png" width="400" >

As we see, task $\tau_3$ misses its deadline! In fact, with the other two tasks, $\tau_1$ and $\tau_2$ constantly executing, $\tau_3$ will **never** get to execute and **all** of its jobs will miss their deadlines!

> "Wait!", you say. OK, _one_ job has missed its deadline, maybe two (from the picture). So how can I make the bold claim that _all_ will miss their deadlines?
> <br>
> If you pay close attention to the figure, I have only checked for `10` time steps. Why that number? Well it so happens that `20` is the **LCM** (lowest common multiple) of **all** the task periods, `4`, `5`, `10`.
> <br>
> Why do we care about the LCM? Turns out, in real-time scheduling, the LCM of the task periods have a special significance. Turns out that if we construct the schedule for **one LCM** nunber of time units, then the schedule **repeats exactly** after that! Hence, the exact same schedule repeats every LCM number of units.
> <br>
> The LCM of the constituent (periodic) tasks in the system is referred to as &rarr; **hyperperiod**. So, we only need to check our schedule for **one hyperiod**. If the task set is schedulable in that timeframe then it will be and, if not, it will not be.
> <br>
> So, for this example, I can state, with confidence, that **all** jobs of $\tau_3$ will miss their deadlines since within **half** of the hyperperiod, one job has missed its deadline!

So, coming back to our analysis, we started with our utilization test $U < 1$ which this task set, _passed_, yet it **failed to schedule*! So, it seems we need something _better_. 

Turns out the [Liu and Layland paper](https://dl.acm.org/doi/10.1145/321738.321743) has figured this out. So they created another test, one based on: **utilization upper bound**. Since RM is a static priority assignment mechanism, there is a **theoretical limit** on the utilization for a task set, that **depends on the number of tasks**, `n`, in the system.

So, we derive (I leave out the details here. Check the Liu and Layland paper for more details) another check for utilization,

$$ U = \sum_{i=1}^n \frac{c_i}{T_i} \le n.(2^{\frac{1}{n}} -1) $$

If the **total** utilization of the system is below this bound, then the task set is schedulable by RM. **Note** that this is a _necessary but **not** sufficient_ test (more on that later).

As we see from above, the value of the right hand side will change with the number of tasks in the system. Hence, with more tasks, the upper bound for $U$ will reduce. 

> let's open up the simulator-plotter for checking this for various values of `n` and see for $n=1, 2, ...$

So, we see that 

$$n = 3\\
U_{ub} \approx 0.78
$$

The utilization for our task set was: $\approx$ `1.0` which is significantly higher! No wonder our task set wasn't schedulable!


Here is a plot that shows the values for different numbers of tasks:

<img src="img/scheduling/rm_util_bounds.png" width="400">

As we see, the value keeps reducing. Does it keep going _all_ the way down to zero? What if I schedule `100` tasks? A `1000`?

Turns out, we can check! With the exact same equation.

> let's open up the simulator-plotter for checking this for various values of `n` and see for $n=100, 1000, etc.$

<img src="img/scheduling/rm_util_bound_100.png" width="400">

As we see from the figure (and the active plotting), the values seem to _plateau_ out and converge...to **`0.69`**! So, for any real-time system scheduled using the RM assignment mechanism, if the utilization bound is under `0.69` then it is schedulable. 

**Optimality**: as mentioned earlier, RM is **optimal**, _i.e.,_

- if a task set is schedulable by RM &rarr; then there is no other _static_ algorithm that can do better (in terms of utilization)
- if a task set is _not_ schedulable by RM &rarr; there is **no other _static_ algorithm** can schedule it

##### Exact (Response Time) Analysis

Now, let's go back to one of our earlier examples (from the [cyclic executive](#cyclic-executives) chapter):

|task|c|T|
|----|--|----|
| $\tau_1$ | 1| 4 |
| $\tau_2$ | 2| 6 |
| $\tau_3$ | 3| 12 |
||

We added some period information to the tasks.

We know that using the naive utilization test, $U \approx. 0.833$. But, recall that the utilization bound test, for $n=3$ tasks requires, $U < 0.78$. So, this task set must be _unschedulable_, right? Let's draw it out on the timeline and see:

<img src="img/scheduling/rm_schedulable_example/rm.final.svg" width="400">

Wait, this is **schedulable**? But it fails our test!

This is why I referred to it as a _necessary but **not** sufficient_ test. Hence, for the Liu and Layland utilization bound test,

|result of test|schedulable?|
|--------------|------------|
| pass, _i.e.,_ $U_{ub} < 0.69$ | yes |
| fail, $U_{ub} > 0.69$ | **unsure**|
||

We we need a _better_ test &rarr; **Response Time Analysis** (RTA):

- if **all jobs** of a task are able to **complete before their respective deadlines** &rarr; task set is schedulable
- caveat &rarr; we account for the **interference** (hence, delays) encountered by the jobs by _all_ higher priority jobs

Let's look at it in more detail:

1. **worst-case** response time of task, $\tau_i$ is

$$R_i = c_i + I_i$$

where $I_i$ is the **interference** faced by that job from **all** higher prioriy jobs until then.

2. For _each_ higher priority job, $\tau_j$, the number of _jobs_ released during the time interval $R_i$ is:

$$\left\lceil \frac{R_i}{T_j} \right\rceil$$

Since _each period_ of task $\tau_j$ results in a new job being released. Since RM gives higher priority to shorter periods, those released jobs will execute ahead of the current teak, $\tau_i$.

3. Since $\lceil {R_i}/{T_j} \rceil$ number of $\tau_j$'s jobs execute before $\tau_i$, the interference caused by all of them:

$$I_j = \left\lceil \frac{R_i}{T_j} \right\rceil .\ c_j$$


4. the **total** interference then, is the sum of the individual interference by each of the higher priority jobs, _i.e.,_

$$I = \sum_{j\in hp(i)}\left\lceil \frac{R_i}{T_j} \right\rceil .\ c_j $$

5. Finally, the **response time** for task, $\tau_i$ must combine its own (worst-case) execution time with the total interference from **all** higher priority tasks, 

$$R_i = c_i + I_i$$

$$ R_i = c_i + \sum_{j\in hp(i)}\left\lceil \frac{R_i}{T_j} \right\rceil .\ c_j $$

For each task, we carry out the above analysis &rarr; stop when consecutive iterations provide the **same** values. 

6. At each stage, check if the response time for a task is less than or equal to its deadline

$$ \forall \tau_i: R_i < T_i $$

If the above test passes for all tasks, then the task set is **schedulable** even if the earlier tests fail. Hence, this is both, _necessary **and** sufficient_.

**Example** [contd.]: Now, applying this to our errant example:

1. assign priorities: $\tau_1 > \tau_2 > \tau_3$

2. response time calculations

For each task, we calculate the response time using the above formula via iterative analysis.

|task | iteration | calculations| $R_i < T_i$ |
|-----|-----------|-------------|-------------|
| $\tau_1$ | 1 | $R_1 = c_1 = 1$ | yes [ $1<4$ ]
| $\tau_2$ | 1 | $R_2^0 = c_2 = 2$ <br> $R_2^1 = c_2 + \lceil\frac{R_2^0}{T_1}\rceil c_1$ <bR> $R_2^1 = 2 + \lceil\frac{2}{4}\rceil \cdot 1 = 3$ ||
|          | 2 | $R_2^2 = 2 + \lceil\frac{3}{4}\rceil \cdot 1 = 3$ [stop] | yes [ $3 < 6$ ]
| $\tau_3$ | 1 | $R_3^0 = c_3 = 3$ <br> $R_3^1 = c_3 + \lceil\frac{R_3^0}{T_1}\rceil c_1 + \lceil\frac{R_3^0}{T_2}\rceil c_2$ <br> $R_3^1 = 3 + \lceil\frac{3}{4}\rceil \cdot 1 + \lceil\frac{3}{6}\rceil \cdot 2 = 6$ ||
|          | 2 | $R_3^2 = 3 + \lceil\frac{6}{4}\rceil \cdot 1 + \lceil\frac{6}{6}\rceil \cdot 2 = 8$ | |
|          | 3 | $R_3^3 = 3 + \lceil\frac{8}{4}\rceil \cdot 1 + \lceil\frac{8}{6}\rceil \cdot 2 = 8$ [stop] | yes [ $8<12$ ]
||

Since the response time of **all** tasks meet their deadlines under RM scheduling, therefore the task set is **schedulable**.

The response time analysis algorithm:

<img src="img/scheduling/response_time_algo.png" width="500">

<br>

There exist many of static assignment algorithms, for instance the [Deadline Monotonic Scheduler](http://www.cs.csi.cuny.edu/~yumei/csc744/Examples/realtimetasks.pdf) where priorities assigned to processes are **inversely proportional to the length of the deadline**.

**Resources**:

1. to read more about the schedulability analysis details or other types of schedulers, see: [Priority-Driven Scheduling](https://www.eecs.umich.edu/courses/eecs571/lectures/lecture5-schedule2.pdf).
2. [A Review of Priority Assignment in Real-Time Systems](https://iris.unimore.it/bitstream/11380/1118762/4/POST_PRINT_JSA2016Priority.pdf) by Davis et al.





#### Earliest-Deadline First Scheduler (EDF)

The problem with static priority assignments, is that they are typically _non-optimal_. Wait, but we said earlier that RM _is_ optimal? Well, among static priority assignment algorithms RM is optimal but, as we saw from the analyses and the graphs, upper bounds for tasksets often taper off at $U = 0.69$. While we can create task sets with higher utilization (as the response-time analyis shows us), it takes a lot of manual effort to create such task sets. This means, that in the _common_ case, we are **wasting nearly `31 %` utilization**!

A dynamic assignment of priorities can help mitigate these problems and ensure that we make better use of the system resources. Many dynamic scheduling algorithms have been proposed, _e.g._, [FIFO](https://d-nb.info/1240614632/34) and [Least Slack Time](https://www.javatpoint.com/least-slack-time-lst-scheduling-algorithm-in-real-time-systems) among others.

In this section we will focus on **the** priority assignment mechanism for real-time systems which, actually, is one of the mainline schedulers in Linux, named [`SCHED_DEADLINE`](https://docs.kernel.org/scheduler/sched-deadline.html).

In a nutshell, as the name implies, EDF assigns priority based on the **absolute deadline** of the job. From [Wikipedia](https://en.wikipedia.org/wiki/Earliest_deadline_first_scheduling):
> Whenever a scheduling event occurs (task finishes, new task released, etc.) the queue will be searched for the process closest to its deadline. This process is the next to be scheduled for execution.

While the exact priority of a job depends on its deadline, the latter are calculated statically. Hence, even though jobs of a task may have different priorities, **each** job has only one priority level. As jobs complete, the priorities of the remaining (or new, incoming) jobs change.

**EDF Schedulability Test**: is the **same** as the first test we discussed, _i.e.,_

$$ U = \sum_{i=1}^{n} \frac{c_i}{T_i} \le 1 $$

As long as we're following the task model described earlier, this is a **very simple** check to test for the validity of the task set for EDF. 

Let's revisit our example from RM that was _not_ schedulable, _viz.,

|task|c|T|
|----|--|----|
| $\tau_1$ | 2| 4 |
| $\tau_2$ | 2| 5 |
| $\tau_3$ | 1| 10|

Before we proceed, we need to decide on some policies:

- two jobs have the **same** deadlines &rarr; pick the one that was released _first_
- same deadline **and** released at the same time++ &rarr; pick one with the smaller index?

These are some simple rules that help in simplifying the decision-making process. We can change them, as long as it helps us make forward progress and we remain _consistent_.

++ in this scenario, ideally we should redesign the system to combine these two tasks -- if they always run together, then why pay the extra costs of preemption/context-switch, _etc._?

For the above task set, we see that,

$$U = \frac{2}{4} + \frac{2}{5} + \frac{1}{10} = 0.5 + 0.4 + 0.1 = 1 \le 1$$

Hence, this task set is **schedulable** using EDF (just barely though since its utilization is `1`!). At least theoretically! Remember that this task set _failed_ for RM.

The schedule diagram for this task set looks like,

<img src="img/scheduling/edf/pngs/edf.final.png" width="400">

So far, it looks schedulable. It is left as an exercise to the reader to check until the hyperperiod (`20`).

**Optimality**: EDF is an **optimal scheduling algorithm** &rarr; if the task set is schedulable by some algorithm, it is also schedulable under EDF.

EDF can definitely _squeeze_ out the maximum from a system -- as we just saw, it can even schedule task sets with the theoretical utilization vound (`1`)!


#### RM vs. EDF

So, let's compare the two superstars of the real-time scheduling world, RM and EDF. The &check; symbol indicates which one is better. 

|parameter | RM | EDF |
|----------|----|-----|
| optimality | &check; (static) | &check; |
| context switch overheads | &check; | &cross; |
| preemptions | &cross; | &check; |
| analysis overheads | &cross; | &check; |
| utilization | &cross; | &check; |
| implementation ease | &check; | &cross; |
| predictability | &check; | &cross; |
|**total**| <scb>4</scb> | <scb>4</scb> |
||

<br>

**Other Issues**: note that we have mostly considered a simple task model. But these may vary in real world systems, _e.g.,_

- $ D <T $, $D > T$ &rarr; essentially situations where deadlines and periods don't align; there are other analyses methods that can be applied
- **multicore** &rarr; so far we have only discussed single core systems; scheduling across multiple cores is an NP-complete problem but many heuristics have been developed; see [A Survey of Hard Real-Time Scheduling for Multiprocessor Systems](https://dl.acm.org/doi/pdf/10.1145/1978802.1978814) for a summary of many results
- **priority inheritance protocols** &rarr; for dealing with resource contentions; again a large body of work exists in this domain; see [Lecture Note \#6](https://www.eecs.umich.edu/courses/eecs571/lectures/lecture6-schedule3.pdf) for a good summary.
- **power consumption** and scheduling &rarr; scheduling methods can help alleviate power consumption issues; see [Real-Time Dynamic Voltage Scaling for Low-Power Embedded Operating Systems](https://www.eecs.umich.edu/courses/eecs571/lectures/lecture12-rtdvs.pdf) for one of the early results.
- **[memory](https://link.springer.com/article/10.1007/s11241-012-9158-9)**, **[networks](https://sibin.github.io/papers/2017_RTSS_SDNQoS_Rakesh.pdf)**, **[networks-on-chip](https://www.computer.org/csdl/journal/td/2017/05/07728147/13rRUwj7coW)**, **[5G](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9773317)**, _etc.,_ &rarr; real-time scheduling has been applied to wide variety of domains.



<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

<!--rel="stylesheet" href="./custom.sibin.css"-->


# Control Theory

Consider a simple problem &rarr; how do you balance a ball?

<img src="img/controls/soccer_ball_balance.gif">

<br>

I guess that's more complicated than what we wanted! So, let's make it really simple and try in a _one dimensional plane_, as follows:

<img src="img/controls/ball/ball.unstable.gif" width="300">

We want to balance the ball in the _middle_ of the table. And the ball moves either left or right, based on how we _tilt_ the table. 

As we see from this picture, a naive attempt at balancing the ball can quickly make it "_unstable_". But, our objective, is to make sure that,

- the ball remains **stable** and
- it is in the **middle** of the table

The options that are available to us are:

1. tilt the table down on the left (anti-clockwise)
2. title the table down on the right (clockwise)

We also have the ability to control the _speed_ at which the table tilts to either side. We can actually combine these, as we shall see.

Hence, the parameters for the problem are:

|type | options |
|-----|---------|
| inputs | speed (clockwise, anticlockwise) |
| output | ball velocity, acceleration |
||

Some how, we need to _control_ the outputs by modifying the inputs to the system. Enter **control theory**. 


## Control Theory | Introduction

Control theory is a _multidisciplinary_ field at the intersection of applied mathematics and engineering. Engineering fields that heavily utilize control theory include mechanical, aerospace, electrical and chemical engineering. Control theory has been applied to the biological sciences, finance, you name it.

Anything that you,

- **want to control** and
- can **develop a model**

you can develop a "_controller_" for managing it, using the tools of control theory.

In our everyday life, we interact with technologies that utilize control theory. They appear in applications like adaptive cruise control, thermostats, ovens and even lawn sprinkler systems. The field of control theory is huge and there's a wide range of subdisciplines.

The basic idea behind control theory is to _understand a process or a system_ by developing a model for it that represents,

> the **relationships between inputs and outputs for the system**

We then use this model to **adjust the inputs** &rarr; to get **desired outputs**. The relationship between the inputs and outputs is usually obtained through empirical analysis, _viz.,_,

1. make changes to the input
2. wait for the system to respond
2. observe changes in the output. 

Even if the model is based on an equation from physics, the parameters within the model are still identified experimentally or through computer simulations.

We repeat the experiments/simulations as needed to "understand" the system as well as we can, in ordero to develop the model. Once the model has been developed, we develop a **control model** that can used to tune the input &rarr; output relationship.

In effect, we are _inverting_ the original model (input &rarr; output) to develop, 

> control model: input &larr; output

To better understand this, consider the example of a light bulb and switch:

<img src="img/controls/lightbulb.png" width="300">

Even if we didn't know the relationship between the switch and bulb, we can conduct a few experiments to figure out the following:

|switch state <br> (input) | bulb state <br> (output)|
|---------------------|--------------------|
| off | off |
| on  | on |
||

Now we have our "model" of input (switch state) &rarr; output (ligthbulb state). This model works as as no _external_ disturbances occur (power failure or bulb burn out).

But, this is _not_ our control model. For that, we need to **invert** the model we've built so far. 

So, we start with the **desired output state**, _e.g.,_ the "lightbulb must be on". Then, we reason backwards to: "_what should the input be to achieve this desired state?_". Should the switch be `on` or `off`?

From our original model (and experiments), we have created the I/O relationship table above. Hence, it stands to reason that we can "invert" it as:

|desired output <br> lightbulb state| corresponding input <br> switch state|
|---------------------|--------------------|
| on | on |
| off  | off |
||

<br>

Now, let's **formalize** things a little. 

Consider the following mathematical model that describes the behavior of a system:

<img src="img/controls/equations/svgs/equations.002.svg" width="300">

The model says that if we change the input `u` the output `y` will change to be **twice** the value of the input `u`.

Now, in control theory, we are concerned about how to **get to a specific output**. Hence, if we want to reach a specific value of `y`, say &rarr; **$y^*$**, we need to _manipulate the model_ to now create a "control model", _i.e.,_

$$u = \frac{y^*}{2}$$

This model says for any value of the output $y^*$ that we want, we can identify the input `u` &rarr; essentially dividing $y^*$ by `2`. Notice that this equation is now **in terms of `u`** &rarr; we have our **control law**! Restating the obvious, this is an "inverse" of the original model of the system.

We have just developed our **first controller**! The desired value, $y^*$ is referred to as the **setpoint**. We get to the setpoint by picking the right value for `u`. 

Developing a control law, in a sense, is inverting your model to rewrite the output in terms of the input so that you can get the output you want. More complex systems lead to more complicated control laws. Practitioners have developed methods of developing control laws for systems whose models cannot be cleanly inverted, _e.g.,_ such as nonlinear systems or systems with dead times.

For context, this is where we are in this course _map_:

<img src="img/stack_architecture/stack_overview.6.png" width="300">

### Open-Loop vs Closed-Loop Control

For the control law we just developed, if our model is accurate and there are no disturbances then, 

$$ y = y^*$$

However, note that there is nothing ensuring that the value of $y = y^*$. We just assume (rather, _expect_) that it would be the case. This is known as an **open loop controller**. You desire a certain output and hope that the controller actually gets there.

So, the open loop controller is depicted as:

<img src="img/controls/controls_openloop/controls.openloop.svg">

What we really want, is to somehow _ensure_ that the controllers gets to its setpoint. How do we do that?

The problem is that while the input drives the output, there is no way to _guarantee_ that the controller will get to the set point. 

What we really need, is a **closed-loop controller** &rarr; one that uses **feedback** to,

- **adjust `u`**
- ensure that we get to $y^*$ (or, at least as close to it as possible).

The feedback typically comes from the output of the controller model that we created. So,

<img src="img/controls/controls_closedloop/controls.closedloop.final.svg">

Note that the feedback can be positive or negative. 


[The above description is distillation of the [excellent description found here](https://www.reddit.com/r/ControlTheory/comments/lqjgb3/comment/gogu5pu/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button).]


## Feedback Control

[The following material is thanks to [Prof. Sathish Gopalakrishan](https://ece.ubc.ca/sathish-gopalakrishnan/), Univ. of British Columbia].

Consider the following problem (that we increasingly encounter in the real world):

> how do you ensure that a car remains in the _center_ of its lane?

So, we have a car moving on the road, thus:

<img src="img/controls/feedback_lane/car_road.1.png" width="200">

<br>

the blue arrow shows the direction of motion of the car. Hence, for the car to remain in the _center_ of the lane, we need to apply a **correction** to its direction of motion,

<img src="img/controls/feedback_lane/car_road.2.png" width="200">

<br>

There are some questions that come up:

- **how** do we apply the corrections?
- **how much** and
- **when** do we **stop**?

Enter **feedback control**:

> - _compare_ system state to the desired state
> - apply a _change_ to the system inputs &rarr; counteract the deviations
> - repeat until desired outcome &rarr; setpoint

**Example**: let's see how feedback control can be applied to a temperature control of a room. 

Given a "desired" room temperature (as input to a thermostat), what do we need to consider while attempting to achieve this temperature?

<img src="img/controls/feedback_temp/temperature.1.png" width="200">

The thermostat needs to control/provide inputs to a furnace/AC,

<img src="img/controls/feedback_temp/temperature.2.png" width="300">

which then affects the temperature in the room:

<img src="img/controls/feedback_temp/temperature.3.png" width="400">

Easy! Done...right?

Except, the real world is far from ideal. We have to deal with disturbances...

<img src="img/controls/feedback_temp/vader_disturbance_force.jpg" width="300">

<br>

Well not that kind of disturbance, but pesky issues like heat loss, bad insulation and physical problems in general:

<img src="img/controls/feedback_temp/temperature.4.png" width="500">

As we see from the picture, we may not get to the expected behavior due to external factors. So, as before, just the input will not suffice to reach the setpoint. 

So, we provide "feedback" to the controller:

<img src="img/controls/feedback_temp/temperature.5.png" width="500">

Essentially the temperature reading of the room, _after_ the thermostat and furnace/AC have completed their operations based on the original inputs (desired temperature).

Let's introduce some _generic_ technical terms for each of these components:

<img src="img/controls/feedback_temp/temperature.6.png" width="500">

The "controller" is based on the "control model" that we developed earlier. It sends commands ("_actuation signals_") to an actuator and then affects the _process under control_. Finally, the _process variable_ (the "output" from the earlier discussions) is what we want to drive towards the set point.

**Note**: in the case that feedback is not possible, there is work on &rarr; [open-loop control](https://www.electronics-tutorials.ws/systems/open-loop-system.html) and [feedforward control](https://web.stanford.edu/class/archive/ee/ee392m/ee392m.1034/Lecture5_Feedfrwrd.pdf).

Another example &rarr; cruise control.

<img src="img/controls/feedback_temp/cruise_control.png" width="500">

Note how the feedback reaches the controller in this case. 

So, at a high-level, a **closed-loop feedback control system** looks like,

<img src="img/controls/closed_loop_feedback.1.png" width="400">

Some of these inputs/edges have _specific_ names:

<img src="img/controls/closed_loop_feedback.2.png" width="400">

**Note:** the main goal &rarr; **error is minimized** (ideally `0`).

A more formal definition of the same quantities,

<img src="img/controls/closed_loop_feedback.3.png" width="400">

|quantity | definition |
|---------|------------|
| $r(t)$  | **reference**/set point|
| $e(t)$  | **error** |
| $u(t)$  | **control signal**/"input" |
| $y(t)$  | (expected/final) **output** |
| $\overline{y(t)}$ | "feedback"/**estimate** |
||

Now let's apply this feedback control model to the earlier problem of lane following.


## Feedback Control Applied to Lane Following

Recall that we want to keep the car in the center of its lane:

<img src="img/controls/feedback_lane/car_road.2.png" width="100">

But here's a question &rarr; _how do you find the **center** of the lane?_

Consider a road with lane markings on either side,

<img src="img/controls/feedback_lane/lane.1.png" width="300">

Now, let's assume that some system (say, a camera), can track the yellow lines to an extent. We need to find the center of the lane, as marked in the figure:

<img src="img/controls/feedback_lane/lane.2.png" width="400">

Based on the _two_ points marked up ahead (that we can detect to be on the same plane), we can calculate,

$$x_{center} = \frac{x_{left\_end}+x_{right\_end}}{2}$$

Now, a car need not be in the actual center of the lane,

<img src="img/controls/feedback_lane/lane.3.png" width="400">

Now, assuming that the camera is mounted at the center of the car,

<img src="img/controls/feedback_lane/lane.4.png" width="300">

The car's position can be calculated as:

$$x_{car} = \frac{width}{2}$$

From this we can calculate the **cross-track error** (CTE), 

$$CTE = x_{car} - x_{center}$$

What happens when,

- $CTE > 0$
- $CTE < 0$?

Now, back to our original problem &rarr; keeping the car in the center of the lane. We do this by &rarr; **keep CTE as small as possible** and applying **corrections**,

<img src="img/controls/feedback_lane/car_road.2.png" width="100">

The \$64,000 question is: **how**?

Answer: **feedback control**!

Recall the various components of the feedback control:

<img src="img/controls/closed_loop_feedback.2.png" width="200">
<img src="img/controls/closed_loop_feedback.3.png" width="200">

<br>

Now, let's map the lane following components on to this:

<img src="img/controls/feedback_lane/feedback.1.png" width="400">

As we see from the figure, the **lane following controller** sends the control/actuation signal to the steering unit. Sensors (perhaps a camera equipped with vision algorithms in this case) provide **feedback** to the controller ($\overline y_t$). Mapping this back to the lane variables and CTE,

<img src="img/controls/feedback_lane/feedback.2.png" width="400">

This figure shows the important part &rarr; the **CTE is the feedback** for the lane following controller! The **input** then is the negative error, _i.e.,_ the goal is to reduce the CTE. Also note that the _output_ of the controller is the **steering input**.

So, let's focus in on how the controller operates, _i.e.,_ this part:

<img src="img/controls/feedback_lane/feedback.3.png" width="400">

<br>

Problem statement:

> given the CTE, how do we compute the **control** signal so that the car _stays in the middle of the lane_?

The final "corrections", when applied, may look something like this:

<img src="img/controls/feedback_lane/car_road.3.png" width="100">

## PID Control

Let's start with one goal &rarr; **lateral position control**:

||||
|-----|-----|-----|
|process variable| $\textbf{y(t)}$ | $y$ position at time, $t$|
|goal | $y = 0$| keep the car at position `0`|
|control signal| $u(t)$ | steering |
||

Let's say we have the car's _start_ and _end_ position,

<img src="img/controls/feedback_lane/lateral_axis.2.png" width="400">

And we know the relationship between $u(t)$ and $y(t)$:

<img src="img/controls/feedback_lane/lateral_axis.3.png" width="200">

Basically we want $u(t)$ to be negative &rarr; so that $y$ tends towards its eventual goal, $y = 0$.

So, what should our **control input**, 
$$e(t) = ?$$

<br>

As we see below, we want the input to be a _decreasing value of the feedback_, 

$$e(t) = -y(t)$$

<br>

<img src="img/controls/feedback_lane/lateral_axis.4.png" width="400">

This is called **proportional (P) control**.

### Proportional (P) Control

The correction is **proportional** to the **size of the error**, _i.e.,_

<img src="img/controls/feedback_lane/p_control.2.png" width="400">

So, going back to our example of lateral control, let us try to apply the proportional control methodology to it:

<img src="img/controls/feedback_lane/p_lateral_axis.1.png" width="400">

We have the following choices:

- $K_p > 0$
- $K_p < 0$

We pick the $K_p > 0$ since we want the following relationship to hold (following from $e(t) = -y(t)$):

$$ K_p e(t) = - K_p y(t)$$

<img src="img/controls/feedback_lane/p_lateral_axis.2.png" width="400">

<br>

We see that this proportional controller helps us move the car towards our goal, $y=0$.

Now, let's consider a few situations:

1. what happens if $K_p$ &rarr; **too small** (small _"gain"_)?

<img src="img/controls/feedback_lane/p_lateral_axis.3.png" width="400">

<br>

The response is **too slow**/gradual. We may _never_ get to the goal in this case. 

2. what happens if $K_p$ &rarr; **too large** (large _"gain"_)?

<img src="img/controls/feedback_lane/p_lateral_axis.4.png" width="400">

<br>

The response is **too sudden**. The system may **overshoot** the goal!

So, the next question that comes up &rarr; _can the car be stabilized at $y=0$?_ This is **unlikely** using just the proportional control method since,

|gain|effect|
|----|------|
|small| **stead-state error**|
|large| **oscillations**|
||

The question then becomes &rarr; _how can we **reduce oscillation**_, _i.e._, can we get to the following situation (smoother, _actual_ approach to the goal)?

<img src="img/controls/feedback_lane/d_lateral_axis.1.png" width="400">


### Derivative (D) Control 

Derivative control **improves the dynamic response** of the system by,

- studying the **rate of change** of the error and
- **decreasing oscillation**

<br>

<img src="img/controls/feedback_lane/d_control.2.png" width="400">

So, what does this mean, in practice? What we're measuring and trying to control, is the **rate of change**, _i.e.,_ the change from,

$$y(t-1) \rightarrow y(t)$$

<br>

<img src="img/controls/feedback_lane/d_lateral_axis.2.png" width="400">

Typically, proportional and derivative control are often **used together**, as a way to counteract each others' influences. So, we get:

<img src="img/controls/equations/svgs/equations.004.svg" width="400">

As with the proportional controller, we have two options for the derivative as well. Should,

- $\frac{dy(t)}{dt} < 0$
- $\frac{dy(t)}{dt} > 0$

Note that the derivative controller's job is to steer **away** from the reference line, to act as a counter to the proportional controller pushing in the opposite direction. Hence, we pick $\frac{dy(t)}{dt} < 0$.

The derivative controller acts like a **brake** and counteracts the correctional force. It reduces overshoot by **slowing the correctional factor** &rarr; as the reference goal approaches.

<img src="img/controls/feedback_lane/pd_lateral_axis.1.png" width="400">

We see numerous uses of the combination, known as the **P-D** controllers in every day life, from the smallest to the largest, even rocket ships!

<video controls width="500"> <source src="img/controls/feedback_lane/SpaceX_landing.mp4"></video>

#### Tuning P-D Controllers

Consider the following values for the two coefficients, $K_p$ and $K_d$:

<img src="img/controls/feedback_lane/pd_graph.1.png" width="150">
<img src="img/controls/feedback_lane/pd_graph.2.png" width="150">
<img src="img/controls/feedback_lane/pd_graph.3.png" width="150">

As we see, tuning $K_d$ has a significant impact! The oscillations pretty much go away and we _quickly_ get to the reference line with very little oscillation. Of course, the car overshoots a little but the combination of P-D brings it back soon enough.

An interesting question arises &rarr; _what if we increase the value of $K_d$ -- eventually making it **very large**?_

<img src="img/controls/feedback_lane/pd_graph.4.png" width="150">
<img src="img/controls/feedback_lane/pd_graph.5.png" width="150">
<img src="img/controls/feedback_lane/pd_graph.6.png" width="150">

While we see from the first graph ($K_p = 0.2$, $K_d = 4.0$) that the oscillations have gone away, increasing $K_d$ further makes the situation worse -- it drives the car _away_ from the reference goal!

How do we deal with this?

Well, by **tuning** the paramters, of course! For instance, in the last case, if we make a change *K_p = 3.0*, 

<img src="img/controls/feedback_lane/pd_graph.6.png" width="150">
&rarr;
<img src="img/controls/feedback_lane/pd_graph.7.png" width="150">

We see a quick, "smooth" path to the reference! 

In fact, a lot of the design of control systems involves the tuning of such parameters, depending on the system, to get things "just right". 


### Integral (I) Control

Are we done? Not quite. Let's take a closer look at the results:

<img src="img/controls/feedback_lane/i.graph.2.png" width="400">

As we see from this image, even though we reached the reference, the behavior is **not smooth**! There could be many reasons for this, such as _steering drift_, caused by the mechanical design of the system:

<img src="img/controls/feedback_lane/i_control.1.png" width="200">
<img src="img/controls/feedback_lane/i_control.2.png" width="150">

<br>

There are a variety of **unmodeled disturbances** and **systemic errors** (_"bias"_):

- actuators and processes &rarr; not ideal
- friction, steering, drift, changing workloads, misalignments, _etc._

Hence, the signal **may never reach** the set points! It will end up "settling" near the reference, which is not always ideal.

To deal with this, we need **integral** (I) control.

First, let's define **steady state error** (SSE):

> difference between the reference and the steady-state process variable

Hence, when time goes to _infinity_,

$$SSE = \lim_{x\to\infty} [r(t) - y(t)]$$

The correction must be **proportional** to both &rarr; **error** and **duration** of the error. Essentially it **sums the error over time**.

<img src="img/controls/feedback_lane/i_control.4.png" width="400">

<br>

**Note:** unless the error is _zero_, this term will **grow**! In fact, the error keeps adding up, so the **correction must also increase** &rarr; this drives the steady state error to **zero**.

<img src="img/controls/feedback_lane/i.graph.4.png" width="400">

In many instances, integral control is used **in conjunction with** the P and D controllers,

<img src="img/controls/equations/svgs/equations.006.svg" width="500">

<br>

This is known as: **PID Control**,

<img src="img/controls/feedback_lane/pid_control.2.png" width="400">

Let's look at some examples of tuning the various paramters of a PID controller, as applied to our problem:

<img src="img/controls/feedback_lane/pid_graph.1.png" width="200">
<img src="img/controls/feedback_lane/pid_graph.2.png" width="200">

<br>

Let's increase $K_p$ now and see the effect:

<img src="img/controls/feedback_lane/pid_graph.3.png" width="200">

We see that the system has stabilized well around the reference point and, if we zoom in, we will see fewer disturbances. 

Now, let's keep increasing $K_p$,

<img src="img/controls/feedback_lane/pid_graph.4.png" width="200">
<img src="img/controls/feedback_lane/pid_graph.5.png" width="200">

Wait, the signal _oscillates_? The main reason is that the I term is not zero when crossing the reference, $y(t) = 0$ and it takes a little while to wash out the cumulative error.

In summary:

- **P** is required
- depending on the system, one or both of **I**/**D** is combined with **P**
    - **PI**, **PD** or **PID**

**Tuning** P, I, D gains. There is no "optimal" way to tune the PID gains

1. start with &rarr; $K_p = 0$, $K_d = 0$, $K_i = 0$
2. **slowly** increase $K_p$ until &rarr; system oscillates around set point
3. slowly increase $K_d$ until &rarr; system settles around set point
4. if steady-state error exists &rarr; slowly increase $K_i$ until corrected without causing additional oscillations


### Some additional feedback control applications:

1. Segway balance control

<video controls width="500"> <source src="img/controls/feedback_lane/segway.mp4"></video>

2. Drone control

<video controls width="500"> <source src="img/controls/feedback_lane/drone_PID.mp4"></video>

3. Motor speed control

<video controls width="500"> <source src="img/controls/feedback_lane/motor_speed_control.mp4"></video>


**References**:

1. Control theory introductions: [1](https://www.basicknowledge101.com/pdf/control/Control%20theory.pdf), [2](https://engineeringmedia.com/controlblog/what-is-control-engineering), [3](https://www.basicknowledge101.com/pdf/control/Control%20system.pdf)
2. [Map of Control Theory](https://engineeringmedia.com/maps)
3. [What is PID Control](https://www.mathworks.com/discovery/pid-control.html) by Mathworks
4. [Control Theory Lectures](https://www.youtube.com/watch?v=oBc_BHxw78s&list=PLUMWjy5jgHK1NC52DXXrriwihVrYZKqjk) by Brian Douglas. 
5. [Introduction to Control Theory and Application to Computing Systems](https://www.eecs.umich.edu/courses/eecs571/reading/control-to-computer-zaher.pdf) by Abdelzaher et al.
6. [Automotive Control Systems](https://www.sciencedirect.com/topics/engineering/automotive-control-system)
7. [PID Controller Design](https://ctms.engin.umich.edu/CTMS/index.php?example=Introduction&section=ControlPID)
8. [Introduction to PID controllers](https://www.digikey.com/en/maker/projects/introduction-to-pid-controllers/763a6dca352b4f2ba00adde46445ddeb)
10. [Construction and theoretical study of a ball balancing platform](https://www.diva-portal.org/smash/get/diva2:1373784/FULLTEXT01.pdf.) by Frank and TJERNSTRÖM.
11. [Understanding PID Control: 2-DOF Ball Balancer Experiments](https://acrome.net/post/understanding-pid-control-using-2-dof-ball-balancer-experiments)
12. [Control Engineering for Industry](https://web.stanford.edu/class/archive/ee/ee392m/ee392m.1034/) from Stanford University.
13. [A Line Following Robot Using PID Controller](http://robinhsieh.com/line-following-robot/)
14. [Ball and Beam: System Modeling](https://ctms.engin.umich.edu/CTMS/index.php?example=BallBeam&section=SystemModeling)
15. [Open Loop Control System](https://www.geeksforgeeks.org/open-loop-control-system/)<!--rel="stylesheet" href="./custom.sibin.css"-->


# Actuation

A controller will typically generate a _control signal_ which, in many physical systems, is used to "**actuate**" a physical component -- _i.e.,_ make it move.

An actuator, then, is a part of a device or machine that helps it to achieve physical movements by converting energy, such as electrical, air or hydraulic, into mechanical force. Simply put, it is the component in any machine that enables movement. They're like muscles on a human body -- converting energy to **physical** action. Actuators are present in almost every machine around us, from simple electronic access control systems, the vibrator on your mobile phone and household appliances to vehicles, industrial devices, and robots. Common examples of actuators include electric motors, stepper motors, jackscrews, electric muscular stimulators in robots, etc.

<iframe width="560" height="315" src="https://www.youtube.com/embed/izeXcf5qu6s?si=yohPUDy1Uf10mges" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

[Defined simply](https://www.progressiveautomations.com/pages/actuators), an actuator is a device that converts energy, which may be electric, hydraulic, pneumatic, etc., to mechanical in such a way that it can be **controlled**. The quantity and the nature of input depend on:

- the kind of energy to be converted and
- function of the actuator. 

<img src="img/actuation/electric_actuator_diagram.png" width=300>

<br>

[Electric](https://www.norgren.com/en-us/support/blog/what-is-an-electric-actuator) and piezoelectric actuators, for instance, work on the input of electric current or voltage, for hydraulic actuators, its incompressible liquid, and for pneumatic actuators, the input is air. The **output is always mechanical energy**.

They are responsible for ensuring a device such as a robotic arm is able to move when electric input is provided. A car uses actuators in the engine control system to regulate air flaps for torque and optimization of power, idle speed and fuel management for ideal combustion.

An actuator requires,

- a control device (which provides control signal) and 
- a source of energy.

The displacement achieved is commonly linear or rotational, as exemplified by

- linear motors and
- rotary motors.

Another broad classification of actuators separates them into two types: 

1. continuous-drive actuators and
2. incremental-drive actuators (_e.g.,_ **stepper motors**).

<img src="img/actuation/Electric_motor.gif">

**Brushed DC motors** move **continuously** when DC voltage is applied to their terminals. 

**Stepper motors** are a variant of motors, named **brushless motors**, that rotate in a series of small and discrete angular steps. Stepper motors can be set to any given step position **without needing a position sensor for feedback**. step position can be rapidly increased or decreased to create continuous rotation, or the motor can be ordered to actively hold its position at one given step. Motors vary in size, speed, step resolution and torque.

The stepper motor is known for its property of converting a **train of input pulses (typically square waves) into a precisely defined increment** in the shaft’s rotational position. Each pulse rotates the shaft through a fixed angle.

<img src="img/actuation/200px-StepperMotor.gif">

[From [Wikipedia](https://en.wikipedia.org/wiki/Stepper_motor): Animation of a simplified stepper motor turned on, attracting the nearest teeth of the gear-shaped iron rotor
- with the teeth aligned to electromagnet 1, they will be slightly offset from right electromagnet (2)
- Frame 2: The top electromagnet (1) is turned off, and the right electromagnet (2) is energized, pulling the teeth into alignment with it. This results in a rotation of 3.6° in this example.
- Frame 3: The bottom electromagnet (3) is energized; another 3.6° rotation occurs.
- Frame 4: The left electromagnet (4) is energized, rotating again by 3.6°. 

When the top electromagnet (1) is again enabled, the rotor will have rotated by one tooth position; since there are 25 teeth, it will take 100 steps to make a full rotation in this example.]


**[Motor Control](https://control.com/technical-articles/understanding-the-basicsof-pulse-width-modulation-pwm/)**: motor speed and direction are dictated by the voltage applied -- change or reverse the polarity of the voltage and the motor will respond in a similar fashion. Voltage can be changed by raising the series resistance within the electrical circuit, which in turn lowers the current through the motor. This change in voltage can be accomplished by series resistors, potentiometers or rheostats. While these devices may be effective for small changes in voltage, the power and torque of the motor are decreased as the current drops. In addition, significant resistance from these devices can _produce a lot of heat_ which could damage other devices within the electrical system.

A more efficient way to vary voltage is to use a **[PWM controller](#pulse-width-modulation)**.


## Pulse Width Modulation

Digital Signals are represented as `0` and `1`. Analog signals, on the other hand, have a greater range of values, often continuous in nature (as we saw in the bit about [ADC](#analog-to-digital-convertors-adcs)s). To control a physical/"analog" device using a microcontroller, we need to do the opposite &rarr; **convert from digital to analog** signal.

<img src="img/actuation/analog-vs-digital-signal.png" width="300">

Some microcontrollers have an onboard [digital-to-analog converter](https://www.whathifi.com/advice/dacs-what-is-a-dac-and-do-you-need-one) (DAC) to output a true analog signal in order to control analog devices and we can even use an external DAC. But a DAC is relatively expensive to produce in terms of cost and it also takes up a lot of silicon area. To overcome these issues and to easily achieve the functionality of a DAC in a much more cost-efficient way, we use **pulse-width modulation** (PWM).

PWM is a method to control analog devices using digital signals. We output an "**analog-like signal**" from the microcontroller that can then control motors, lights and various actuators. 

**Note**: the PWM is **not** a true analog signal, just a digital one modified to **behave** like one. It is essentially a **rectangular wave** with varying "duty cycle" and periods.

In the following [example](https://en.wikipedia.org/wiki/Pulse-width_modulation), an idealized inductor is driven by a set of voltage pulses (in <font color="blue">blue</font>) that result in a sine-wave-like current (in <font color="red">red</font>).

<img src="img/actuation/PWM,_3-level.svg.png" width="300">

PWM is useful for controlling the **average** power or amplitude delivered by an electrical signal. The average value of voltage (and current) fed to the load is controlled by switching the supply between 0 and 100% at a rate faster than it takes the load to change significantly. The longer the switch is on, the higher the total power supplied to the load.

**Example**: Consider the following analogy. Imagine you have a ceiling fan that has just an off-on switch, _i.e.,_ it is either stationary or goes to $100\%$.

<img src="img/actuation/ceiling_fan_cartoon.gif">

What if I say: _I want the fan to operate at $50\%$?_ The only "control" you have is the on-off switch. Can you do it?

Solution:

- turn `on` switch
- wait till fan reaches $50\%$ (or close to it)
- turn it `off`
- when it starts to slow down &rarr; turn it `on` again
- repeat **fast enough** and you get close to the $50\%$
- the faster you do this &rarr; closer to the desired value (aka **setpoint**)

Ideally I don't recommend doing this...

<img src="img/actuation/ceiling_fan_cartoon-meme.gif" width="300">

<br>

So a PWM "wave" looks like:

<img src="img/actuation/PWM-signal-pulse-time-period.png" width="300">


|||
|------|------|
|`on`-`off` switching| **pulse**|
|duration for which the pulse is held at a **high** state| **pulse width**|
| $T$ | **period** |
||

A PWM wave has two important properties that needs to be tuned:

1. [duty cycle](#duty-cycle)
2. [period](#pwm-period) &rarr; one complete cycle of the signal/pulse.

### Duty Cycle

Recall that logic **high** &rarr; `on` (or `off` depending on the system, but pick one for consistency). To represent an `on` time, we use the concept of the **duty cycle**, defined as:

>  duty cycle describes the proportion of 'on' time to the regular interval or 'period' of time.

Duty cycles are represented as percentages (of time that the signal is `on`, relative to its period).

<img src="img/actuation/PWM-different-duty-cycles-average-voltage.jpg.webp" width="240">
<img src="img/actuation/Duty_Cycle_Examples.png" width="200">

The duty cycle can be calculated as:

$$D = \frac{T_{on}}{T} * 100$$

where,

|||
|----|----|
| **D** | duty cycle (percentage)|
| $T_{on}$ | duration when signal is `on`|
| $T$ | total period|
||

Consider the periodic pulse wave, $f(t)$, with a low value, $y_\text{min}$, high value, $y_\text{max}$, and constant duty cycle, $D$, as shown below:

<img src="img/actuation/Duty_cycle_general.svg.png" width="300">

<br>

The **average** value of a wave is,

$$\bar{y} = \frac{1}{T}\int^T_0f(t)\,dt$$

Since $f(t)$ is a pulse wave, its value is,

|||
|-----|-----|
| $y_{max}$ | $0<t<D.T$|
| $y_{min}$ | $D.T<t<T$|

Now, we can expand the above expression as,

$$
\begin{align*}
  \bar{y} &= \frac{1}{T} \left(\int_0^{DT} y_\text{max}\,dt + \int_{DT}^T y_\text{min}\,dt\right)\\
          &= \frac{1}{T} \left(D \cdot T \cdot y_\text{max} + T\left(1 - D\right) y_\text{min}\right)\\
          &= D\cdot y_\text{max} + \left(1 - D\right) y_\text{min}
\end{align*}
$$

So we can now compute how long the signal should be at $y_{max}$ and how much at $y_{min}$.

### PWM Period

The period (or frequency, recall that $f=\frac{1}{T}$) is another important parameter that defines a PWM signal. It essentially determines _the number of times a signal repeats per second_. The choice of $T$ depends heavily on the application. For instance, when [controlling an LED](https://www.circuitbread.com/ee-faq/what-is-a-pwm-signal),

> the frequency of a PWM signal should be sufficiently high if we wish to see a proper dimming effect while controlling LEDs. A duty cycle of 20% at 1 Hz will be noticeable to the human eye that the LED is turning ON and OFF. However, if we increase the frequency to 100Hz, we’ll get to see the proper dimming of the LED.

### PWM Sampling Theorem

Is directly related to the [Nyquist-Shannon Sampling Theorem](https://autonomy-course.github.io/textbook/autonomy-textbook.html#adc-sampling-rate) discussed earlier. A simple summary,

> number of pulses in the waveform is equal to the number of Nyquist samples.

Recall that the Nyquist rate is, _a value equal to **twice** the highest frequency_. 


### Example | Servo Motor Control

Servos (also RC servos) are small, cheap, mass-produced servomotors or other actuators used for radio control and small-scale robotics. 

<img src="img/actuation/Micro_servo.png" width="300">

They're controlled by sending the servo a PWM (pulse-width modulation) signal, a series of repeating pulses of variable width where either the width of the pulse (most common modern hobby servos) or the duty cycle of a pulse train (less common today) determines the position to be achieved by the servo. 

<img src="img/actuation/Servomotor_Timing_Diagram.svg.png" width="300">

### PWM Generation in Microcontrollers

We can use the built-in PWM components in many microcontrollers or timer ICs. Using Arduino, generating a PWM is as simple as writing out _a few lines of code_!

```
analogWrite(pin, value)
```

Note that **not all pins** of an Arduino can generate a PWM signal. In the case of Arduino Uno, there are only 6 I/O pins (3,5,6,9,10,11) that support PWM generation and they are marked with a tilde (~) in front of their pin number on the board.

<img src="img/actuation/arduino_uno_pwm.png" width="300">

<br>

Examples of various duty cycles:

```
analogWrite(PWM_PIN, 64);   // 25% Duty Cycle or 25% of max speed
analogWrite(PWM_PIN, 127);  // 50% Duty Cycle or 50% of max speed
analogWrite(PWM_PIN, 191);  // 75% Duty Cycle or 75% of max speed
analogWrite(PWM_PIN, 255);  // 100% Duty Cycle or full speed
```

<br>

The Raspberry Pi also has a variety of GPIO pins that can be used for generating PWM signals:

<img src="img/actuation/pi_pwm.png" width="300">

<br>

Consider this [code](https://circuitdigest.com/microcontroller-projects/raspberry-pi-pwm-tutorial) for controlling the brightness of an LED:

```python
import RPi.GPIO as IO       #calling header file which helps us use GPIO’s of PI
import time                 #calling time to provide delays in program
IO.setwarnings(False)       #do not show any warnings
IO.setmode (IO.BCM)         #we are programming the GPIO by BCM pin numbers. (PIN35 as ‘GPIO19’)
IO.setup(19,IO.OUT)         # initialize GPIO19 as an output.
p = IO.PWM(19,100)          #GPIO19 as PWM output, with 100Hz frequency
p.start(0)                  #generate PWM signal with 0% duty cycle
while 1:                    #execute loop forever
    for x in range (50):    #execute loop for 50 times, x being incremented from 0 to 49.
        p.ChangeDutyCycle(x) #change duty cycle for varying the brightness of LED.
        time.sleep(0.1)      #sleep for 100m second
    for x in range (50):     #execute loop for 50 times, x being incremented from 0 to 49.
        p.ChangeDutyCycle(50-x)  #change duty cycle for changing the brightness of LED.
        time.sleep(0.1)          #sleep for 100m second
```


**References**:

Additional reading/examples/etc. if you want to learn more about PWMs, programming, _etc._:

1. [What is a PWM Signal?](https://www.circuitbread.com/ee-faq/what-is-a-pwm-signal)
2. [Servo Motors programing](https://www.circuitbread.com/tutorials/servo-motor-indirect-addressing-and-electronic-lock---part-10-microcontroller-basics-pic10f200)
3. [What is a DAC and why do you need on anyways?](https://www.whathifi.com/advice/dacs-what-is-a-dac-and-do-you-need-one)
4. [An Engineer's Primer on Actuators](https://pdhonline.com/courses/m543/m543content.pdf)
5. [What is a Linear Actuator?](https://www.youtube.com/watch?v=izeXcf5qu6s) [YouTube Video]
6. [Understanding the Basics of PWM](https://control.com/technical-articles/understanding-the-basicsof-pulse-width-modulation-pwm/)
7. [Raspberry Pi: PWM Outputs with Python (Fading LED)](https://randomnerdtutorials.com/raspberry-pi-pwm-python/)
8. [Raspberry Pi PWM tutorial](https://circuitdigest.com/microcontroller-projects/raspberry-pi-pwm-tutorial)
9. [Actuation and Avionics](https://www.collinsaerospace.com/what-we-do/industries/business-aviation/power-controls-actuation/actuation)<!--rel="stylesheet" href="./custom.sibin.css"-->

# State Estimation

Consider a robot in a simple grid starting at $(0,0)$ with the intention of moving to $(2,2)$:

<img src="img/ekf/robot_grid.1.png" width="300">
<img src="img/ekf/robot_grid.2.png" width="300">

Now the robot can take multiple paths to get to its destination. The robot has multiple choices as shown in the following figure:

<img src="img/ekf/robot_grid.3.png" width="300">

Let's assume that it follows one of these paths and ends up at the following position:

<img src="img/ekf/robot_grid.4.png" width="200">
<img src="img/ekf/robot_grid.5.png" width="200">
<img src="img/ekf/robot_grid.6.png" width="200">

Clearly this is not the intended goal so a few things need to happen:

1. first of all, the robot has to understand and estimate where it is _right now_ &rarr; _i.e.,_ **estimate its current state**
2. the robot has to then make a decision, based on its current state, where to head next 

How to do this?

Answer: **[state estimation](#state-estimation)**!

But before we go there, we have to answer the following question &rarr; _how did we end up here in spite of onboard sensors?_

The sensor gave us a value, $x_k$ &rarr; we can't seem to trust it as is &rarr; because sensors are imperfect, mainly due to:

- physical limitations, measurement noise, poor calibrations, etc.
- errors can’t be zero
    - $error = observation\ –\ true\_value$

In some sense, we need to "filter" out noisy data and only allow correct data to guide us. Hence, our robot can pick the right direction to end up at its _correct_ destination. 

<img src="img/ekf/robot_grid.7.png" width="200">
<img src="img/ekf/robot_grid.8.png" width="200">
<img src="img/ekf/robot_grid.9.png" width="200">


## State Estimation

State estimation is a fundamental problem in control theory, robotics and signal processing. It involves **determining the state of a dynamic system from noisy or incomplete measurements**. The Kalman filter, developed by Rudolf E. Kálmán in the early 1960s, is one of the most widely used and powerful algorithms for state estimation.

In the context of dynamic systems, "**state**" is defined as,

> a set of variables that completely describe the system at a given time. 

For example:

| **system** | **state variables** |
|------------|----------------------|
| **moving vehicle** | position, velocity, acceleration |
| **pendulum** | angle, angular velocity |
| **financial system** | asset prices, market indicators |
||

State **evolves over time** according to the system dynamics, which can be described by a **state transition model**.


### How to Estimate State?

Let's look at some data:

<img src="img/ekf/noisy_data.1.png" width="300">

<br>

How we take these values ($x_k$) and generate a state _estimate_, $\overline{x_k}$?

What if we have a few more values?

<img src="img/ekf/noisy_data.2.png" width="300">
<img src="img/ekf/noisy_data.3.png" width="300">

<br>

Do we see a trend? What if we had many more values?

<img src="img/ekf/noisy_data.4.png" width="300">

<br>

What's the best way to capture the behavior? We can see that it is "noisy" in that it doesn't follow an "exact" trend. 

Remember that $\overline{x_k}$ is the estimate we want:

<img src="img/ekf/sensor_state.3.png" width="400">


One way to compute $\overline{x_k}$ would be as an **average** of a **running window of samples**. Why "window" and not all the samples? Well we may only care about the most recent `n` values -- anything older and it may not be directly applicable to our current situation.

We can compute the average as follows:

$$
\overline{x_{k}}=\frac{x_{k-n-1}+\cdots+x_{k-1}+x_{k}}{n}
$$

where the only parameter is the window size, $n$.

Consider the following data:

| $k$ | $x_k$ | $\overline{x_{k}}$ |
| --- | --- | --- |
| 0 | 0.08187 | 0.08187 |
| 1 | 0.97601 | 0.52894 |
| 2 | 1.18350 | 0.74713 |

Using the running window average method (for window size $n=3$), we get:

<img src="img/ekf/average_window.1.png" width="300">

<br>

As we add more values, we see that the window moves as well, aggregating groups of values:

| $k$ | $x_k$ | $\overline{x_{k}}$ |
| --- | --- | --- |
| 0 | 0.08187 | 0.08187 |
| 1 | 0.97601 | 0.52894 |
| 2 | 1.18350 | 0.74713 |
| 3 | 0.99502 | 1.05151 |


<img src="img/ekf/average_window.2.png" width="300">

<br>

| $k$ | $x_k$ | $\overline{x_{k}}$ |
| --- | --- | --- |
| 0 | 0.08187 | 0.08187 |
| 1 | 0.97601 | 0.52894 |
| 2 | 1.18350 | 0.74713 |
| 3 | 0.99502 | 1.05151 |
| 4 | -0.31375 | 0.62159 |
| 5 | -0.25739 | 0.14129 |
| 6 | 1.52112 | 0.31666 |

<img src="img/ekf/average_window.3.png" width="300">

<br>

We can see that the estimate is trying to match the changes in the original sensor readings. 


finally, we get:

| $k$ | $x_k$ | $\overline{x_{k}}$ |
| --- | --- | --- |
| 0 | 0.08187 | 0.08187 |
| 1 | 0.97601 | 0.52894 |
| 2 | 1.18350 | 0.74713 |
| 3 | 0.99502 | 1.05151 |
| 4 | -0.31375 | 0.62159 |
| 5 | -0.25739 | 0.14129 |
| 6 | 1.52112 | 0.31666 |
| 7 | 1.75454 | 1.00609 |
| 8 | 1.82412 | 1.69993 |
| 9 | 1.89229 | 1.82365 |
| 10 | 1.10513 | 1.60718 |
| 11 | 1.22321 | 1.40688 |
| 12 | 2.20793 | 1.51209 |
| 13 | 3.02390 | 2.15168 |
| 14 | 2.45511 | 2.56231 |
| 15 | 2.07442 | 2.51781 |
| 16 | 1.49280 | 2.00744 |
| 17 | 1.19093 | 1.58605 |
| 18 | 2.32653 | 1.67009 |
| 19 | 3.84177 | 2.45308 |

<img src="img/ekf/average_window.4.png" width="300">

<br>


This is a good start, but let's consider a few changes.

First: what happens if window size *increases**? 

We consider $n=4$ or $n=9$ even.

<img src="img/ekf/average_window.5.png" width="300">

<br>

But first, let's discuss some properties that correlate with _larger_ window size:

|property | effect (larger $n$) |
|---------|--------|
| smoothening | more/less?|
| sensitivity (to changes) | more/less? |
||

These properties can significantly affect the **response** for the system &rarr; whether it is jerky or sudden vs. a better, albeit slower, response. Also, the sensitivity tells us that the system doesn't respond easily to big changes in output, thus increasing inertia!


Let's look at a few examples:

<img src="img/ekf/average_window.6.png" width="150">
<img src="img/ekf/average_window.7.png" width="150">
<img src="img/ekf/average_window.8.png" width="150">
<img src="img/ekf/average_window.9.png" width="150">

<br>

What about **delays**? Does the window size affect how delayed the estimate is?

<img src="img/ekf/average_window.10.png" width="150">
<img src="img/ekf/average_window.11.png" width="150">
<img src="img/ekf/average_window.12.png" width="150">

<br>

As we see, this is the case! With increased window sizes &rarr; delays increase.

**Questions**: Why does this happen?

|property | effect (larger $n$) |
|---------|--------|
| smoothening | **more**|
| sensitivity (to changes) | **less**|
| delays | **more**|
||


### Exponential Moving Average (EMA)

To give more weights to _recent_ data, prevent delays and get a better control over the smoothing, we use EMA that usese **exponentially decreasing weights over time**,

$$
\begin{aligned}
& \overline{x_{0}}=x_{0} \\
& \overline{x_{k}}=\alpha x_{k}+(1-\alpha) \overline{x_{k-1}}, k>0
\end{aligned}
$$

where, $\alpha$ ($0 < \alpha < 1$) &rarr; **smoothing factor**.

Example ($\alpha = 0.75$):

| $k$ | $x_{k}$ | $\overline{x_{k}}$ |
| :---: | :---: | :---: |
| 0 | 2.0 | 2.0000 |
| 1 | 3.0 | 2.7000 |
| 2 | 2.0 | 2.2100 |
| 3 | 4.0 | 3.4630 |
| 4 | 3.0 | 3.1389 |
||

One of the main advantages of EMA is that we **only need to store one value**, $\overline{x_{k}}$. 

But why "exponential"? If we expand the term for $\overline{x_{k}}$ we see,

$$
\begin{array}{rlrl}
\overline{x_{k}} & =\alpha x_{k}+(1-\alpha) \overline{x_{k-1}}\\
& =\alpha x_{k}+\alpha(1-\alpha) x_{k-1}+(1-\alpha)^{2} \overline{x_{k-2}} \\
& =\alpha x_{k}+\alpha(1-\alpha) x_{k-1}+\alpha(1-\alpha)^{2} x_{k-2}+(1-\alpha)^{3} \overline{x_{k-3}} & \vdots \\
& =\cdots & \\
& =\alpha\left[x_{k}+(1-\alpha) x_{k-1}+(1-\alpha)^{2} x_{k-2}+(1-\alpha)^{3} x_{k-3}+\cdots+(1-\alpha)^{k-1} x_{1}\right]+(1-\alpha)^{k} x_{0}
\end{array}
$$

As we see, the effect of the smoothing factor, $\alpha$, is applied exponentially with each sensor reading. For various values of $\alpha$,

$$
\begin{array}{c}
\alpha=0.3000 \\
\alpha(1-\alpha)=0.2100 \\
\alpha(1-\alpha)^{2}=0.1470 \\
 \alpha(1-\alpha)^{3}=0.1029 \\
\vdots \\
\end{array}
$$

EMA takes into acount **all past data** and encodes it into a **single** value, $\overline{x_{k}}$. 

Consider the following example where $\alpha=0.5$:


| ${ }_{k}$ | $\chi_{k}$ | $\overline{\chi_{k}}$ |
| ---: | :--- | :--- |
| 0 | 0.08187 | 0.08187 |
| 1 | 0.97601 | 0.52894 |
| 2 | 1.18350 | 0.85622 |
| 3 | 0.99502 | 0.92562 |
| 4 | -0.31375 | 0.30594 |
| 5 | -0.25739 | 0.02427 |
| 6 | 1.52112 | 0.77269 |
| 7 | 1.75454 | 1.26362 |
| 8 | 1.82412 | 1.54387 |
| 9 | 1.89229 | 1.71808 |
| 10 | 1.10513 | 1.41161 |
| 11 | 1.22321 | 1.31741 |
| 12 | 2.20793 | 1.76267 |
| 13 | 3.02390 | 2.39328 |
| 14 | 2.45511 | 2.42420 |
| 15 | 2.07442 | 2.24931 |
| 16 | 1.49280 | 1.87105 |
| 17 | 1.19093 | 1.53099 |
| 18 | 2.32653 | 1.92876 |
| 19 | 3.84177 | 2.88526 |
||

The graph looks like:

<img src="img/ekf/ema.1.png" width="300">

<br>

Let's consider some of the values:

| ${ }_{k}$ | $\chi_{k}$ | $\overline{\chi_{k}}$ |
| ---: | :--- | :--- |
| 0 | 0.08187 | 0.08187 |
| 1 | 0.97601 | 0.52894 |
| 2 | 1.18350 | 0.85622 |
| 3 | 0.99502 | **0.92562** |
| 4 | **-0.31375** | **0.30594** |
| 5 | -0.25739 | 0.02427 |
| 6 | 1.52112 | 0.77269 |
|...|...|...|

$\overline{x_{4}}=0.5 x_{4}+0.5 \overline{x_{3}}$

We see that for this value of $\alpha$, the estimate is "halfway" between the two sensor readings,

<img src="img/ekf/ema.3.png" width="300">

<br>

Now, if we change $\alpha=0.7$, we get $\overline{x_{4}}=0.7 x_{4}+0.3 \overline{x_{3}}$ and the graph now looks like,

<img src="img/ekf/ema.4.png" width="300">

<br>

As we see, there's a **heavier bias** towards the **more recent value**.

Now, of these graphs, which one is $\alpha=0.05$ and which one is $\alpha=0.95$?

<img src="img/ekf/ema.5.png" width="300">
<img src="img/ekf/ema.6.png" width="300">

<br>

We can see the significance of changing $\alpha$,

<img src="img/ekf/ema.7.png" width="300">
<img src="img/ekf/ema.8.png" width="300">

<br>

As we see from the following figures, increasing $\alpha$ (left to right) results in:

- **less delay**
- **less smoothening out**

<img src="img/ekf/ema.9.png" width="200">
<img src="img/ekf/ema.10.png" width="200">
<img src="img/ekf/ema.11.png" width="200">

<br>


### State Space Representation

A more "formal" description of **state**:

> a **quantitative** characterization of a system that is **not directly observable**

Examples: temperature, position, velocity, weight, etc.

There are _many_ ways to represent state, even for the same quantity. For instance, consider how to estimate the position of a car in a 2D plane, with the intent of **tracking** it:

<img src="img/ekf/state.1.png" width="200">

<br>

So, how do we represent the "state" of this car?

1. $\boldsymbol{x}_{\boldsymbol{k}}=(x, y)$

A simple position on the coordinate system. Is this sufficient? 

While this captures a **static** state of the system, it doesn't necessarily allow for tracking the car. 

2.  $\boldsymbol{x}_{\boldsymbol{k}}=(x, \dot{x}, y, \dot{y})$

So, let's also track the **velocity**. Clearly that will tell us how fast the car is moving and so we can "track" it correctly?

Well, not quite. This is **instantaneous velocity** that doesn't tell us if the car is accelerating or deccelerating!

3. $\boldsymbol{x}_{\boldsymbol{k}}=(x, \dot{x}, \ddot{x}, y, \dot{y}, \ddot{y})$

Ok, so now we have position, velocity **and** acceleration! Surely, we're done?

But do we know which **direction** the car is heading in?

4. $\boldsymbol{x}_{\boldsymbol{k}}=(x, \dot{x}, \ddot{x}, y, \dot{y}, \ddot{y}, \theta)$

Now, we have a better sense of the "state" of the car, in order to track it.

**State estimation** &rarr; estimating state from sensor measurements.

While the moving averages and EMA are good ways to deal with noisy measurements, estimating state is much harder. There is often **uncertainty** in the measurements and state estimation. 

### Probabilistic State Estimation

These methods allow us to deal with the uncertanties in sensor measurements as well as in state estimation by use of probility. The main idea &rarr; represent state in a **probability distribution**
    
- Measurements are noisy
- Models ‘uncertainty’

We start with the following _"belief"_ &rarr; knowledge about the state or 'estimate of the true state’

A Probabilistic state estimation, then &rarr; computes **new belief based on measurement data**

<img src="img/ekf/prob_state.1.jpeg" width="300">

There are various methods for **probabilistic state estimations**, most notably,

1. [Bayes filter](#bayes-filter)
2. [Kalman filter](#kalman-filter)
3. [Extended Kalman Filter]()


####  Review of Probability Theory

Let's take a quick detour to review some concepts in probability theory.

**Random variable**, $X$

- A variable whose possible values are numerical outcomes of a random phenomenon
    - A function X: $\Omega \rightarrow \mathbb{R}$, where $\Omega$ is the set of possible outcomes
    - Example: rolling a dice, $\Omega=\{1,2,3,4,5,6\}$
- It models state, measurement, controls, environments, etc.


- **Discrete random variable** &rarr; X can take on a countable number of values
- **Continuous** random variable &rarr; X can take on an infinite number of values


**Probability distribution**, $p(x)$

- Links each outcome with probability

Probability distribution: $p(\cdot)$
Probability: $\operatorname{Pr}(\cdot)$

Two way do represent probability distributions:

|probability mass function (PMF) | probability density function (PDF)|
|--------------------------------|-----------------------------------|
| <img src="img/ekf/pmf.png" width="200">| <img src="img/ekf/pdf.png" width="200">|

- **Joint distribution**
    - $p(x, y)=p(X=x$ and $Y=y)$
- If X and Y are **independent**
    - $p(x, y)=p(x) p(y)$

<br>

**Conditional distribution**

- $p(x \mid y)$ : probability of $x$ given $y$
- If $p(y)>0$,
    - $p(x \mid y)=\frac{p(x, y)}{p(y)}$
    - $p(x, y)=p(x \mid y) p(y)$
- If X and Y are independent, $p(x \mid y)=$ ?, $p(y \mid x)=$ ?
    - i.e., X (resp. Y ) tells nothing about Y (resp. X )


Consider the example of rolling two dice ( $\mathrm{X}, \mathrm{Y}$ )

| $(1,1)$ | $(1,2)$ | $(1,3)$ | $(1,4)$ | $(1,5)$ | $(1,6)$ |
| :---: | :---: | :---: | :---: | :---: | :---: |
| $(2,1)$ | $(2,2)$ | $(2,3)$ | $(2,4)$ | $(2,5)$ | $(2,6)$ |
| $(3,1)$ | $(3,2)$ | $(3,3)$ | $(3,4)$ | $(3,5)$ | $(3,6)$ |
| $(4,1)$ | $(4,2)$ | $(4,3)$ | $(4,4)$ | $(4,5)$ | $(4,6)$ |
| $(5,1)$ | $(5,2)$ | $(5,3)$ | $(5,4)$ | $(5,5)$ | $(5,6)$ |
| $(6,1)$ | $(6,2)$ | $(6,3)$ | $(6,4)$ | $(6,5)$ | $(6,6)$ |

<br>

What is $Pr(𝑋=2 | 𝑋 + 𝑌 \le 5)$?

| |  |  |  |  |  |  |  |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|  | 1 | 2 | 3 | 4 | 5 | 6 |  |
| 1 | 2 | 3 | 4 | 5 | 6 | 7 |  |
| 2 | 3 | 4 | 5 | 6 | 7 | 8 |  |
| 3 | 4 | 5 | 6 | 7 | 8 | 9 |  |
| 4 | 5 | 6 | 7 | 8 | 9 | 10 |  |
| 5 | 6 | 7 | 8 | 9 | 10 | 11 |  |
| 6 | 7 | 8 | 9 | 10 | 11 | 12 |  |

**Theorem of total probability**

$$
\begin{array}{ll}
\underline{\text { Discrete }} & p(x)=\sum_{y} p(x, y)=\sum_{y} p(x \mid y) p(y) \\
\underline{\text { Continuous }} & p(x)=\int p(x, y) d y=\int p(x \mid y) p(y) d y
\end{array}
$$

Consider the following problem:

<img src="img/ekf/cond_prob.1.jpg" width="400">

<br>

Let's look at the row where "eye color" is `brown`:

<img src="img/ekf/cond_prob.2.jpg" width="400">

<br>

Filling in the right values:

<img src="img/ekf/cond_prob.3.jpg" width="400">

<br>


**Conditional independence**

- $x$ and $y$ are independent if $z$ is known

$$
\begin{aligned}
& p(x, y \mid z)=p(x \mid z) p(y \mid z) \\
& p(x \mid z)=p(x \mid y, z) \\
& p(y \mid z)=p(y \mid x, z)
\end{aligned}
$$

- Conditional (resp. absolute) independence does not imply absolute (resp. conditional) independence

<br>

**Bayes Rule**:

| | |
|----------|------------|
|discrete | $p(x \mid y)=\frac{p(y \mid x) p(x)}{p(y)}=\frac{p(y \mid x) p(x)}{\sum_{x \prime} p\left(y \mid x^{\prime}\right) p\left(x^{\prime}\right)}$ | 
|continuous | $\quad p(x \mid y)=\frac{p(y \mid x) p(x)}{p(y)}=\frac{p(y \mid x) p(x)}{\int p\left(y \mid x^{\prime}\right) p\left(x^{\prime}\right) d x^{\prime}}$|
||


**Prior and posterior probabilities**

$$
\text p(x \mid y)=\frac{p(y \mid x) p(x)}{p(y)}
$$

where,

- $p(x \mid y)$ &rarr; posterior
- $p(x)$ &rarr; prior

Hence,

- Inferring $x$ from $y$
    - $x$ : state, $y$ : data (measurement)
- Bayes rule helps compute a posterior using the inverse, $p(y \mid x)$, and prior, $p(x)$
    - The probability of an event ( $x=$ state) given information ( $y=$ measurement)
    - Easier to obtain $p(y \mid x)$
        - E.g., sensor accuracy: $p$ (thermometer reading $=72$ | temperature $=71$ )?
    - Example
        - $x$ : has disease, $y$ : test is positive
        - x: position, y: sensor reading

<br>

**Conditioning Bayes rule on an arbitrary random variable**

$$
p(x \mid y, z)=\frac{p(y \mid x, z) p(x \mid z)}{p(y \mid z)}
$$

<br>

**Expectation of a random variable**, $\mathrm{E}[X]$ (or $\mu$, mean)

$$
\begin{array}{ll}
\underline{\text { Discrete }} & \mathrm{E}[X]=\sum_{x} x p(x) \\
\underline{\text { Continuous }} & \mathrm{E}[X]=\int x p(x) d x
\end{array}
$$

|  | $X=0$ | $X=1$ | $X=2$ | $X=3$ |
| :---: | :---: | :---: | :---: | :---: |
| $p(x)$ | 0.10 | 0.20 | 0.60 | 0.10 |
||

<br>

$\mathrm{E}[X]=\sum_{x} x p(x)=0 \cdot 0.10+1 \cdot 0.20+2 \cdot 0.60+3 \cdot 0.10=1.70$

<bR>

**Variance**, $\operatorname{Var}(X)$ or $\sigma^{2}$

- How far values are spread out from the mean
- It can represent uncertainty or noise

$$
\begin{aligned}
\operatorname{Var}[X]=\mathrm{E}\left[(X-\mu)^{2}\right] & =\sum_{x}(x-\mu)^{2} p(x) & & \text { Discrete } \\
& =\int(x-\mu)^{2} p(x) d x & & \text { Continuous }
\end{aligned}
$$

where,

- $\sigma^{2}$ : variance
- $\sigma$ : standard deviation

<br>

**Covariance**, $\operatorname{Cov}(X, Y)$ or $\sigma_{X Y}^{2}$

- Joint variability of $X$ and $Y$

$$
\begin{array}{ll}
\operatorname{Cov}(X, Y)=\mathrm{E}[(X-\mathrm{E}[X])(Y-\mathrm{E}[Y])]=\mathrm{E}[\mathrm{XY}]-\mathrm{E}[\mathrm{X}] \mathrm{E}[Y] & \\
\operatorname{Cov}(X, Y)=\operatorname{Cov}(Y, X) & 
\end{array}
$$

If $X$ and $Y$ are **independent**, $\operatorname{Cov}(X, Y)=0$

## Bayes Filter

Recall that sensors capture **incomplete** or **noisy** information. Consider the example of two LiDAR sensors that are trying to estimate the distance to a pedestrian. One of the LiDAR sensors, measure the distance to be at $10 m$ (with a probability of $50 \%$) while the other estimates the person to be at $10.8 m$ (also with a probability of $50\%$). 

<img src="img/ekf/bayes.lidar.4.png" width="400">

In reality, as we see in the picture, the person is **between $10.3 m$ and $10.5 m$**. So, how do we deal with such situations? And what happens if the probabilities differ greatly? **Which** sensor would you trust and **how much**?

### Bayes filter | **Prediction**

Let's revisit our previous example of a car:

<img src="img/ekf/state.1.png" width="200">

<br>

Let say the car is in $state_k$ at a certain point in time and we want to make a prediction for its future state, $state_{k+1}$,

<img src="img/ekf/bayes_car.2.png" width="200">

<br>

To simplify matters, assume:

- assume car moving along *one* axis, _e.g.,_ x-axis
- follow **discrete** position: $0,1,2, .., 9$
- this is a "circular" track: a $+1$ move from $9 \rightarrow 0$

So, we essentially have,

<img src="img/ekf/bayes_car.3.png" width="400">

<br>

Now, the car starts moving. Let's assume the existence of **another sensor** that tells us about the car's movement, _i.e.,_

| sensor output | meaning |
|---------------|---------|
| `0` | **stay** |
| `+1`, `+2`, ... | move forward by that amount |
||

We also assume this sensor is **always correct** (for now). 

Based on the location of the car, we can plot our (current) "belief" as:

<img src="img/ekf/bayes_car.4.png" width="300">

Now, let the car move forward, say by `1` step. 

<img src="img/ekf/bayes_car.5.png" width="400">

How does this update the belief?

<img src="img/ekf/bayes_car.6.png" width="400">

This is a simple case where the car has _obviously_ moved forward by `1` step and we can verify it. so the belief is updated accordingly.

Now, let's assume that the motion sensor is more realistic and has **noise** with the following probabilities:

| probability | meaning |
|-------------|-------------|
| $80 \%$         | correct reading |
| $10 \%$         | overestimate |
| $10 \%$         | underestimate |
||

<img src="img/ekf/bayes_car.7.png" width="400">

If  the sensor says the **number** of moves is `+3`,

- Car is $80 \%$ likely to have moved &rarr; `+3`
- Car is $10 \%$ likely to have moved &rarr; `+2`
- Car is $10 \%$ likely to have moved &rarr; `+4`

Let's look at our belief as a result of this update:

<img src="img/ekf/bayes_car.8.png" width="400">

The **updated belief** looks like:

<img src="img/ekf/bayes_car.9.png" width="400">

The question is: &rarr; **how**?

$$
\begin{aligned}
& \operatorname{Pr}\left(x_{1}=5\right)= \\
& \operatorname{Pr}\left(x_{0}=1\right) \operatorname{Pr}(\text { under })+ \\
& \operatorname{Pr}\left(x_{0}=2\right) \operatorname{Pr}(\text { correct }) \\
& =0.5 \times 0.1+0.5 \times 0.8=0.45
\end{aligned}
$$

This comes from the **[law of total probability](#review-of-probability-theory)**:

$$p\left(x_{k}\right)=\sum_{i} p\left(x_{k} \mid x_{k-1}=i\right) p\left(x_{k-1}=i\right)$$

So, after `3` moves, the **predicted** probability estimate is:

<img src="img/ekf/bayes_car.10.png" width="400">

<br>

Let's keep going on...

<img src="img/ekf/bayes_car.13.png" width="400">

<br>

Now, what happens after &rarr; **`20` predictions** ?

<img src="img/ekf/bayes_car.15.png" width="400">

<br>

Wait, what is happening? Why did the probabilities collapse into a lower spread?

Well, **sensors are imperfect**! Hence, **information is lost**. As a result, we may end up with the sitauation where the actual state **differs** from the predicted state.

<img src="img/ekf/bayes_car.16.png" width="400">

<br>

### Bayes filter | **Measurement Update**

We use a **measurement** to "fix" the problem of divergence between the actual state and predicted state. So, in essence, we get some **feedback** from the real world &rarr; using **sensors** (same or different type). [Sounds familiar](#control-theory)? 

<img src="img/ekf/bayes_car.17.png" width="400">

<br>

**Prior**: probability prior to incorporating measurement &rarr; **equally likely** to be in any position, _i.e.,_ $\frac{1}{10}$ for every position. Let's put aside prediction, for now.

<img src="img/ekf/bayes_measure.1.png" width="400">

<br>

Let the **first** sensor reading &rarr; $z_0 = 2$. But the sensor is **noisy**. Let's also assume it has a probability of $90 \%$.

> Note: in the "predict" stage, we were using "noisy" sensors as well, but those were measuring **different** quantities. In that case, the sensor could be from the car engine or the wheels (or odometers) that say how much we "**intended**" to move, _e.g., "we generated enough torque in the engine to move forward by `3` slots.
> <br>
> In contrast, the sensors in this section **measure** &rarr; "how much was **actually** moved?". This could be via other types of sensors, _e.g.,_ GPS.
> <br>
> **Both** of these sensors can, and will, of course have noise and probabilities associated with them. The question then, is &rarr; "how to **reconcile** the two?"

So now, what is the **new belief**? From this setup, intuitively, it seems &rarr; $x_{0}=2 \text { is } 9 \text { times likely than } x_{0} \neq 2$.

Time to use **[Bayes Rule](#review-of-probability-theory)**:


<img src="img/ekf/equations/pngs/equations-0.png" width="500">

<br>

where,  $p\left(z_{k}\right)=\sum_{x_{i}} p\left(z_{k} \mid x_{i}\right) p\left(x_{i}\right)$ (as we've seen before, from the law of total probability). 

So now, we get the **likelihood**, $p\left(z_{k} \mid x_{k}\right)$,

<img src="img/ekf/bayes_measure.2.png" width="300">

<br>

**Question**: what if the probability was $80 \%$?

Carrying on, the numerator on the right hand side, _i.e.,_ $p\left(z_{k} \mid x_{k}\right) \times p\left(x_{k}\right)$:

<img src="img/ekf/bayes_measure.3.png" width="500">

<br>

The result of which is:

<img src="img/ekf/bayes_measure.4.png" width="300">

<br>

which puts our car at the **right spot**:

<img src="img/ekf/bayes_car.3.png" width="400">

<br>

We're still not done. We have to compute the denominator, $p\left(z_{k}\right)=\sum_{x_{i}} p\left(z_{k} \mid x_{i}\right) p\left(x_{i}\right)$, which essentially **normalizes** the belief:

<img src="img/ekf/bayes_measure.5.png" width="300">

<br>

So our final value, the new belief, aka **posterior**, $p\left(x_{k} \mid z_{k}\right)$ &rarr; probability **after incorporating measurement**.

Let's look at the **formal calculations** for each:

If we want to calculate, 

$$
p\left(x_{0}=2 \mid z_{0}=2\right)=\square
$$

Recall, 

$$
\begin{aligned}
& p\left(z_{k}=a \mid x_{k}=a\right)=90 \% \\
& p\left(z_{k}=a \mid x_{k}=b\right)=10 \%
\end{aligned}
$$

_i.e.,_ sensor is correct with probability of $90\%$ &rarr; the belief that the measurement $z_k = a$ matches reality $x_k = a$ is $90 \%$ otherwise it is $10 \%$. For instance,

|measurement ($z_k$) | reality ($x_k$) | belief (prob %) |
|------------|------------|--------|
| $z_k = 2$ | $x_k = 2$ | $90 \%$|
| $z_k = 2$ | $x_k = 5$ | $10 \%$|
||

<br>

$$
p\left(x_{0}=2 \mid z_{0}=2\right)=\frac{p\left(z_{0}=2 \mid x_{0}=2\right) \times p\left(x_{0}=2\right)}{p\left(z_{0}=2\right)}=\frac{\textbf{0.9} \times 0.1}{p\left(z_{0}=2\right)}=\frac{0.09}{p\left(z_{0}=2\right)}
$$

<br>

In the same vein,

$$
p\left(x_{0}=1 \mid z_{0}=2\right)=\frac{p\left(z_{0}=2 \mid x_{0}=1\right) \times p\left(x_{0}=1\right)}{p\left(z_{0}=2\right)}=\frac{\textbf{0.1} \times 0.1}{p\left(z_{0}=2\right)}=\frac{0.01}{p\left(z_{0}=2\right)}
$$

<br>

Use this formula, we can find $p\left(x_{0}=x \mid z_{0}=2\right)$ &rarr; for all `x`.

But we still need to compute &rarr; $p\left(z_{0}=2\right)$.

Recalling the law of total probability, so we can compute:

$$
p\left(z_{0}=2\right)=\sum_{x} p\left(z_{0}=2 \mid x_{0}=x\right) p\left(x_{0}=x\right)
$$


From the above table,

$$
\begin{aligned}
& p\left(z_{k}=a \mid x_{k}=a\right)=90 \% \\
& p\left(z_{k}=a \mid x_{k}=b\right)=10 \%
\end{aligned}
$$

Plugging in the values,

$$
\begin{aligned}
p\left(z_{0}=2\right) & =\sum_{x} p\left(z_{0}=2 \mid x_{0}=x\right) p\left(x_{0}=x\right) \\
& =0.09+9 \times 0.01=\textbf{0.18}
\end{aligned}
$$

Hence, the final, **normalized** probability distribution looks like:

<img src="img/ekf/bayes_measure.6.png" width="300">

<br>

Now, the sensor gives again $z_{1}=2$ &rarr; same likelihood ($90\%$ correct), _i.e.,_

$$
p\left(x_{1} \mid z_{1}=2\right)
$$

Then, what's our new belief (using the previous belief as the **prior**), $\operatorname{Pr}\left(x_{1}=2 \mid z_{1}\right)=90.00 \%$?

For the next iteration, we get:

$$
\operatorname{Pr}\left(x_{2}=2 \mid z_{2}\right)=\textbf{98.78} \%
$$

<img src="img/ekf/bayes_measure.8.png" width="300">

<br>

We can keep calculating this for various values of `k`:

<img src="img/ekf/bayes_measure.9.png" width="500">

<br>

What is happening here? Why is only one bar increasing? Nothing ele changes?

**Answer**: the car is stationary at location `2`!

<img src="img/ekf/bayes_car.3.png" width="400">

<br>


If we **drop the sensor accuracy** to say, $60 \%$, we see:

<img src="img/ekf/bayes_measure.10.png" width="500">

<br>

The confidence in the measurement increases, albeit at a much slower rate.

Now, if we drop it further, to say, $50 \%$,

<img src="img/ekf/bayes_measure.12.png" width="500">

<br>

Why is nothing changing? Because the sensor is **not providing any additional information**! The $50 \%$ rate keeps it at the same belief level as everything else. 


### Bayes filter | **Combining** Prediction and Measurement

- prediction **loses** information
- measurement **improves** knowledge (i.e., decreases uncertainty)

Let's **combine** prediction and measurement!

We start with the same initial position and sensor accuracies:

- initial position = `2`
- motion model:

| sensor output | meaning | accuracy |
|---------------|---------|----------|
| `0` | **stay** | $10 \%$ |
| `+1` | move forward by `1`| $80 \%$ |
| `+2` | move forward by `2` | $10 \%$ |
||

This **motion model** can be represented as:

$$
p\left(x_{k} \mid x_{k-1}=i\right)
$$

<br>

_i.e.,_ what is the probability of $x_k$, given $x_{k-1} = i$, represented visually as,

<img src="img/ekf/bayes_combined.1.png" width="400">

<br>

And given the **posterior** at time $k-1$, _i.e.,_

$$
p\left(x_{k-1}=i \mid z_{k-1}\right)
$$

The **combined** model, _i.e.,_ the **new prior**, is:

$$
p\left(x_{k}\right)=\sum_{i} p\left(x_{k} \mid x_{k-1}=i\right) p\left(x_{k-1}=i \mid z_{k-1}\right)
$$

Let's start with the **initial belief**, _viz.,_

<img src="img/ekf/bayes_combined.2.png" width="200">

<br>

At time, $t=0$, the predictions and updates:

<img src="img/ekf/bayes_combined.6.png" width="500">

<br>

Note that the end result is the **new posterior** &rarr; that we will use in the future cycles as, 

$$p\left(x_{k}\right)=\sum_{i} p\left(x_{k} \mid x_{k-1}=i\right) p\left(x_{k-1}=i \mid z_{k-1}\right)
$$. 

Hence we see:

<img src="img/ekf/bayes_combined.8.png" width="500">

<br>

The confidence in the prediction and belief in the system both increase, as we see in the next cycle:

<img src="img/ekf/bayes_combined.9.png" width="500">

<br>

**Note:** when the measurement matches the prediction, the uncertainty decreases. 

Now what happens if &rarr; the car **did not move**? We see:

<img src="img/ekf/bayes_combined.10.png" width="500">

<br>

The true position remains same (`5`), but the prediction is still based on the original motion model:

| sensor output | meaning | accuracy |
|---------------|---------|----------|
| `0` | **stay** | $10 \%$ |
| `+1` | move forward by `1`| $80 \%$ |
| `+2` | move forward by `2` | $10 \%$ |
||

The **uncertainty increases**! But still the estimate $\approx$ true state.

We keep going...

<img src="img/ekf/bayes_combined.11.png" width="500">

<br>

Let's see what happens if we don't follow the motion model, _i.e.,_ the car **moved by `2`** (instead of `1`):

<img src="img/ekf/bayes_combined.12.png" width="500">

<br>

The **true position** &rarr; `8` but the prediction is still based on the original motion model hence, the confidence drops.

Getting back to the original motion model, one last time,

<img src="img/ekf/bayes_combined.13.png" width="500">

<br>

We get back to the high confidence levels, **really quickly**!

To **summarize**, the steps in the Bayes Filter are:

<img src="img/ekf/bayes/bayes_filter.final.png" width="300">

<br>

1. **predict**: 
    - calculate the prior, $p\left(x_{k}\right)$, from the previous posterior, $p\left(x_{k-1} \mid z_{k-1}\right)$ 
    - by incorporating the motion (process) model, 
    
$$
p\left(x_{k}\right)=\sum_{i} p\left(x_{k} \mid x_{k-1}=i\right) p\left(x_{k-1}=i \mid z_{k-1}\right)
$$

2. **update**: 
    - given a measurement, $z_{k}$, compute the likelihood
    - from the likelihood and prior, apply Bayes Rule to update the belief:

$$
p\left(x_{k} \mid z_{k}\right)=\frac{p\left(z_{k} \mid x_{k}\right) \times p\left(x_{k}\right)}{p\left(z_{k}\right)}
$$

where, $p\left(z_{k}\right)=\sum_{x} p\left(z_{k} \mid x\right) p(x)$.


**Limitations**:

While the Bayesian filter works for many instances, the main problem is that it is **discrete** in nature. Consider the example for robots that need a $1 cm$ resolution in a $100m$ space &rarr; $10,000$ positions needed to model the environment!

**Scaling** is much harder, especially in the multidimensional systems. For instance, how do we model the original state of the car that we discussed earlier:

$$
\boldsymbol{x}_{\boldsymbol{k}}=(x, \dot{x}, \ddot{x}, y, \dot{y}, \ddot{y}, \theta)
$$

We need to **update** the Bayes model itself to handle such situations. 

Enter the **[Kalman Filter](#kalman-filter)**.

## Kalman Filter

To deal with some of the issues with the basic Bayes filter, we introduce the **Kalman Filter** that express state and uncertainty using **Gaussians** (aka the "[normal](https://en.wikipedia.org/wiki/Normal_distribution)" distribution).

<img src="img/ekf/kalman/discrete_bayes.png" width="200">
<img src="img/ekf/kalman/kalman_gaussian.png" width="200">

<br>

### Gaussian Distribution

Now a quick detour on Gaussians. A normal distribution or Gaussian distribution is a type of **continuous probability distribution** for a **real-valued random variable** and is represented as:

<img src="img/ekf/equations/pngs/equations-1.png" width="500">

<!--
$$
\mathcal{N}\left(\mu, \sigma^{2}\right)=\frac{1}{\sqrt{2 \pi \sigma^{2}}} e^{-\frac{(x-\mu)^{2}}{2 \sigma^{2}}} 
$$
-->

<br>

A very common Gaussian can be visualized as:

<img src="img/ekf/kalman/normal_distribution_wiki.svg" width="400">

<br>


Note that **variance** ($\sigma^2$) captures the **uncertainty** in the system and is the **square** of the standard deviation ($\sigma$).

<img src="img/ekf/kalman/variance_uncertainty_examples.png" width="400">

<br>

More specific examples:

<img src="img/ekf/kalman/uncertainty.1.png" width="200">
<img src="img/ekf/kalman/uncertainty.2.png" width="200">
<img src="img/ekf/kalman/uncertainty.3.png" width="200">

<br>

Some properties of Gaussians:

1. **area** under the curve = `1` (since it is the sum of all the probabilities)

$$
area = \int_{-\infty}^{+\infty} \mathcal{N}\left(\mu, \sigma^{2}\right)
$$

Note that the curve approaches **infinity** ($\infty$) on **either side** &rarr; the probability of certain events is **never `0`**, no matter how small.

Hence, 

$$
area = \int_{-\infty}^{+\infty} \frac{1}{\sqrt{2 \pi \sigma^{2}}} e^{-\frac{(x-\mu)^{2}}{2 \sigma^{2}}} = \textbf{1}
$$

2. probability that a value, $x$ &rarr; is in a **range**, $(a,b)$:

$$
\operatorname{Pr}(a \leq x \leq b)=\int_{a}^{b} \frac{1}{\sqrt{2 \pi \sigma^{2}}} e^{-\frac{(x-\mu)^{2}}{2 \sigma^{2}}} d x
$$

3. since it is often useful to find the probability **within one standard deviation** (on either side), 

$$
\operatorname{Pr}(\mu-\sigma \leq x \leq \mu+\sigma)=\int_{\mu-\sigma}^{\mu+\sigma} \frac{1}{\sqrt{2 \pi \sigma^{2}}} e^{-\frac{(x-\mu)^{2}}{2 \sigma^{2}}} d x \approx \textbf{68 \%}
$$

4. **sum** and **product** of two Gaussian distributions is fairly easy to calculate

Given, two Gaussians,

$X_{1} \sim \mathcal{N}\left(\mu_{1}, \sigma_{1}^{2}\right)$

$X_{2} \sim \mathcal{N}\left(\mu_{2}, \sigma_{2}^{2}\right)
$

|result| sum | product|
|------|-----|--------|
| **new** Gaussian, $Z \sim \mathcal{N}\left(\mu, \sigma^{2}\right)$ | $Z=X_{1}+X_{2}$ | $Z=X_{1} X_{2}$ |
| new **mean**, $\mu$ | $\mu_{1}+\mu_{2}$ | $\mu=\frac{\sigma_{2}^{2} \mu_{1}+\sigma_{1}^{2} \mu_{2}}{\sigma_{1}^{2}+\sigma_{2}^{2}}$ |
| new **variance**, $\sigma^{2}$ | $\sigma_{1}^{2}+\sigma_{2}^{2}$ | $\sigma^{2}=\frac{\sigma_{1}^{2} \sigma_{2}^{2}}{\sigma_{1}^{2}+\sigma_{2}^{2}}$ |
||

5. **closure** under **linear transformations**

From [Probabilistic Robotics](https://soulhackerslabs.com/sensor-fusion-with-the-extended-kalman-filter-in-ros-2-d33dbab1829d):

The advantage of using Gaussians (or Normals) lies in their mathematical properties, which simplify the Kalman Filter equations. A key property is their closure under linear transformations: when a Gaussian belief undergoes a linear transformation, the **result remains a Gaussian random variable**! This property ensures that the equations of the Kalman Filter remain,

- elegant and 
- manageable


### **State** in Kalman Filters

So, we can define state in this model as:

<img src="img/ekf/kalman/kalman.state.png" width="400">

<br>

The **prior** &harr; **measurement** &harr; **update** process looks like:

<img src="img/ekf/kalman/kalman.car.state.png" width="300">

<br>

As we see from this figure, the prediction and measurements are not just single points but a **distribution**.

The various transitions look like:

<img src="img/ekf/kalman/kalman.final.png" width="300">

<br>

Essentially the same as the Bayes Filter &rarr; the difference being that each of the edges is now a probabilistic Gaussian value.

### Kalman Filter | **Prediction**

First of all, we note that the **process model**, _i.e.,_ the model of how the system evolves over time (essentially the physics) is also a Gaussian! For instance, in the equations of motion, &rarr; _velocity_ follows a Gaussian distribution. 

Suppose we want to track the motion of this car:

<img src="img/ekf/kalman/kalman.predict.1.png" width="300">

<br>

From Newton's laws of motion we can **predict** the next state using the following **process model**:

$$
\overline{x_{k+1}}=x_{k} +v_{k} \Delta t
$$

where,

|variable | description
|---------|-----------|
| $x_{k}$ | current state |
| $x_{k+1}$ | **predicted** next state |
| **$v_{k}$** | velocity|
| $\Delta t$ | time difference |
||

Since velocity follows a Gaussian distribution, let's assume,

$$
v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 1^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)
$$

Now, if the current state, $x_k$ is a Gaussian, as we've established before,

<img src="img/ekf/kalman/kalman.predict.3.png" width="300">

<br>

Now clearly, $x_{k+1}$ has to be a Gaussian as well &rarr; since at least one of the terms on the right is a Gaussian, _viz.,_ the current state **and** velocity.

So, the question is &rarr; what is the value for,

<img src="img/ekf/kalman/kalman.predict.4.png" width="300">

<br>

$$
\overline{x_{k+1}} \sim \mathcal{N}\left(? \mathrm{~m}, ? \mathrm{~m}^{2}\right) 
$$

Recall, that the sum of two Gaussians is,

$$
\begin{aligned}
\mu & =\mu_{1}+\mu_{2} \\
\sigma^{2} & =\sigma_{1}^{2}+\sigma_{2}^{2}
\end{aligned}
$$

Assume that $\Delta t = 1s$. Plugging in thes values,

$$
\overline{x_{k+1}} \sim \mathcal{N}\left(6.5 \mathrm{~m}, 2 \mathrm{~m}^{2}\right)
$$

In this example, the second parameter in the velocity term is the **process noise** in the physics model:

<img src="img/ekf/kalman/kalman.predict.6.png" width="300">

<br>

*Important Notes**: Kalman Filter is **unimodel**, _i.e.,_ there is a **single peak** each time.

<img src="img/ekf/kalman/kalman_unimodal.png" width="300">

<br>

An obstacle is **not** both, $10m$ away with $90\%$ and $8m$ away with $70\%$ probability. It is:

- **$9.7m$ away with $98\%$** or 
- **nothing**

Let's look at some examples for prediction. Consider the following velocity models:

|||
|----|----|
| **A** | $$v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 0^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$$
| **B** | $$v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 1^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$$
| **C** | $$v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 2^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$$
||

And we have the following *predicted** states:

|prediction| velocity model|
|-----|----|
| <img src="img/ekf/kalman/kalman.predict.7.png" width="300"> | <br> **A**, **B** or **C** ? |
| <img src="img/ekf/kalman/kalman.predict.8.png" width="300"> | **A**, **B** or **C** ? |
| <img src="img/ekf/kalman/kalman.predict.9.png" width="300"> | **A**, **B** or **C** ? |
||

<br>

So, which one of the above is &rarr, **A**, **B** and **C**? Let us plug in the values:

|prediction| velocity model|
|-----|----|
| <img src="img/ekf/kalman/kalman.predict.7.png" width="300"> | $v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 1^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ [**B**] |
| <img src="img/ekf/kalman/kalman.predict.8.png" width="300"> | $v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 0^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ [**A**]|
| <img src="img/ekf/kalman/kalman.predict.9.png" width="300"> | $v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 2^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ [**C**]|
||

So, what does the predicted state look like?

|prediction| velocity model| predicted state |
|-----|----|------|
| <img src="img/ekf/kalman/kalman.predict.7.png" width="300"> | $v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 1^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ [**B**] | $\overline{x_{k+1}} \sim \mathcal{N}\left(6.5 \mathrm{~m}, ? \mathrm{~m}^{2}\right)$|
| <img src="img/ekf/kalman/kalman.predict.8.png" width="300"> | $v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 0^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ [**A**]| $\overline{x_{k+1}} \sim \mathcal{N}\left(6.5 \mathrm{~m}, ? \mathrm{~m}^{2}\right)$|
| <img src="img/ekf/kalman/kalman.predict.9.png" width="300"> | $v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 2^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ [**C**]| $\overline{x_{k+1}} \sim \mathcal{N}\left(6.5 \mathrm{~m}, ? \mathrm{~m}^{2}\right)$|
||

<br>

Coming back to the sum of two Gaussians, $\sigma^{2} =\sigma_{1}^{2}+\sigma_{2}^{2}$, and the current state, $\overline{x_{k}} \sim \mathcal{N}\left(3.5 \mathrm{~m}, 1 \mathrm{~m}^{2}\right)$,

|prediction| velocity model| predicted state |
|-----|----|------|
| <img src="img/ekf/kalman/kalman.predict.7.png" width="300"> | $v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 1^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ [**B**] | $\overline{x_{k+1}} \sim \mathcal{N}\left(6.5 \mathrm{~m}, 2 \mathrm{~m}^{2}\right)$|
| <img src="img/ekf/kalman/kalman.predict.8.png" width="300"> | $v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 0^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ [**A**]| $\overline{x_{k+1}} \sim \mathcal{N}\left(6.5 \mathrm{~m}, 1 \mathrm{~m}^{2}\right)$|
| <img src="img/ekf/kalman/kalman.predict.9.png" width="300"> | $v_{k} \sim \mathcal{N}\left(3 \mathrm{~m} / \mathrm{s}, 2^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ [**C**]| $\overline{x_{k+1}} \sim \mathcal{N}\left(6.5 \mathrm{~m}, 5 \mathrm{~m}^{2}\right)$|
||

As we see from these examples, depending on the **noise** in the intial Gaussian, the **uncertainty increases** for the predicted state, even when the velocity model had `0` noise! 

The problem is that we don't know &rarr; how **close** is our prediction to reality. Hence, we need an **update** step &rarr; measurements!


### Kalman Filter | **Update**

In the measurement (or sensor) model, the **measurement uncertainty** (aka "likelihood") is also represented as a Gaussian.

<img src="img/ekf/equations/pngs/equations-2.png" width="500">

<br>

For instance, current temperature is $72^{\circ} \mathrm{F} \pm 1^{\circ} \mathrm{F}$.

Now, recall that,

$$
posterior = prior \times likelihood
$$

$$
posterior = \overline x_k \times z_k
$$

What does this **actually mean**?

Let's consider a few examples.

1. Example 1

| prediction ($\overline x_{k}$) | measurement ($z_k$) | posterior ($\overline x_{k} \times z_k$) |
|----------|----------|----------|
|$\overline{x_{k}} \sim \mathcal{N}\left(5,1^{2}\right)$ | $z_{k} \sim \mathcal{N}\left(5,1^{2}\right)$ | **?** |
||

Let's plot these two Gaussians,

<img src="img/ekf/kalman/kalman.update.1.png" width="300">

<br>

As we see from the figure, the two align perfectly &rarr; since they're the **same** distribution. What would $\overline{\mathrm{x}}_{\mathrm{k}} \times \mathrm{z}_{\mathrm{k}}$ look like?

Recall the **product** of two Gaussians,

$$
\begin{aligned}
\mu & =\frac{\sigma_{2}^{2} \mu_{1}+\sigma_{1}^{2} \mu_{2}}{\sigma_{1}^{2}+\sigma_{2}^{2}} \\
\sigma^{2} & =\frac{\sigma_{1}^{2} \sigma_{2}^{2}}{\sigma_{1}^{2}+\sigma_{2}^{2}}
\end{aligned}
$$

Hence, the posterior would be,

| prediction ($\overline x_{k}$) | measurement ($z_k$) | posterior ($\overline x_{k} \times z_k$) |
|----------|----------|----------|
|$\overline{x_{k}} \sim \mathcal{N}\left(5,1^{2}\right)$ | $z_{k} \sim \mathcal{N}\left(5,1^{2}\right)$ | $\overline{\mathrm{x}}_{\mathrm{k}} \times \mathrm{z}_{\mathrm{k}} \sim \mathcal{N}(5,0.5)$ |
||

Graphically this looks like,

<img src="img/ekf/kalman/kalman.update.4.png" width="300">

<br>

Hence, we see the following:

- an **increase** in the probability around `5` (**taller** Gaussian)
- a **decrease** in the uncertainty (**narrower** Gaussian)

<br>

2. Example 2: this time the initial Guassians differ slightly,

| prediction ($\overline x_{k}$) | measurement ($z_k$) | posterior ($\overline x_{k} \times z_k$) |
|----------|----------|----------|
|$\overline{x_{k}} \sim \mathcal{N}\left(5,1^{2}\right)$ | $z_{k} \sim \mathcal{N}\left(5.4,1^{2}\right)$ | $\overline{\mathrm{x}}_{\mathrm{k}} \times \mathrm{z}_{\mathrm{k}} \sim \mathcal{N}(5.2,0.5)$ |
||

We see that the result is in the **midddle** of the two original Gaussians.

<img src="img/ekf/kalman/kalman.update.5.png" width="300">

<br>


3. Example 3: let's see what happens if the Gaussian's differ significantly, _i.e.,_

| prediction ($\overline x_{k}$) | measurement ($z_k$) | posterior ($\overline x_{k} \times z_k$) |
|----------|----------|----------|
|$\overline{x_{k}} \sim \mathcal{N}\left(4,1^{2}\right)$ | $z_{k} \sim \mathcal{N}\left(6,0.5^{2}\right)$ | $\overline{\mathrm{x}}_{\mathrm{k}} \times \mathrm{z}_{\mathrm{k}} \sim \mathcal{N}(?,?)$ |
||

<img src="img/ekf/kalman/kalman.update.6.png" width="300">

<br>

After the update, the resultant distribution looks like,

| prediction ($\overline x_{k}$) | measurement ($z_k$) | posterior ($\overline x_{k} \times z_k$) |
|----------|----------|----------|
|$\overline{x_{k}} \sim \mathcal{N}\left(4,1^{2}\right)$ | $z_{k} \sim \mathcal{N}\left(6,0.5^{2}\right)$ | $\overline{\mathrm{x}}_{\mathrm{k}} \times \mathrm{z}_{\mathrm{k}} \sim \mathcal{N}(5.6,0.2)$ |
||

<img src="img/ekf/kalman/kalman.update.7.png" width="300">

<br>

What this tells us is &rarr; we give **more weight to more ‘certain’ information**, _i.e.,_ the measurement in this case that has a higher+narrower Gaussian. Which is as it should be.

Hence, the **posterior** is,

- between prediction ($\overline x_{k}$) and measurement ($z_k$)
- closer to **more certain side* (based on the variances)
- so, a ‘**weighted average**’

<img src="img/ekf/kalman/kalman.update.8.png" width="300">

<br>

Let us look at a few more **detailed examples**.

1. Example I

| process model | measurement noise/sensor error |
|---------------|--------------------|
| $\overline{x_{k+1}}=x_{k}+v_{k} \Delta t$ | $\sigma^2 = 0.5^2$ |
| $ v_{k} \sim \mathcal{N}\left(2 \mathrm{~m} / \mathrm{s}, 1^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ ||
| $ \Delta t=1 \mathrm{~s}$ ||
||

<br>

The initial state looks like,

<img src="img/ekf/kalman/kalman.posterior_example.1.png" width="500">

<br>

If we plot this system, the actual position vs measurements (first graph) and afer applying the Kalman Filter.

<img src="img/ekf/kalman/kalman.posterior_example.2.png" width="300">
<img src="img/ekf/kalman/kalman.posterior_example.3.png" width="300">

<br>

We see the following properties:

1. posterior &rarr; **always between** prior and measurement
2. posterior is **closer to** measurement &rarr; sensor noise is small

| $v_{k} \sim \mathcal{N}\left(2 \mathrm{~m} / \mathrm{s}, 1^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ <br> prior (prediction)  | $\sigma^{2}=0.5^{2}$ <br> measurement | posterior (with measurement) |
| :---: | :---: |:---: |
| $\mathcal{N}(2,101)$ | 1.555  | $\mathcal{N}(1.556,0.249) $ |
| $\mathcal{N}(3.556,1.249)$ | 2.267 | $\mathcal{N}(2.482,0.208) $ |
| $\mathcal{N}(4.482,1.208)$ | 1.233 | $\mathcal{N}(1.790,0.207) $ |
| $\mathcal{N}(3.790,1.207)$ | 3.534 | $\mathcal{N}(3.578,0.207) $ |
| $\mathcal{N}(5.578,1.207)$ | 4.644 | $\mathcal{N}(4.804,0.207)$ |
||

Note that the uncertainty ($\sigma^2$) values for the prior ($v_k$) are all **larger** than that for the measurement (`0.5`). Hence the prior is **almost useless** for the posterior. Whereas, the posterior is **very close** to the measurement! This shows us what a difference a good measurement makes.

2. Example II: let's update the model so that the measurement error is $\sigma^2 = 1.5^2$

How do you think this will change the posterior?

Updated model:

| process model | measurement noise/sensor error |
|---------------|--------------------|
| $\overline{x_{k+1}}=x_{k}+v_{k} \Delta t$ | **$\sigma^2 = 1.5^2$**  (**more inacccurary**!)|
| $ v_{k} \sim \mathcal{N}\left(2 \mathrm{~m} / \mathrm{s}, 1^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ | |
| $ \Delta t=1 \mathrm{~s}$ ||
||

<br>

We see **more noise** in the measurements:

<img src="img/ekf/kalman/kalman.posterior_example.4.png" width="300">

<br>

Let's look at the results of applying the Kalman Filter (side-by-side with the previous example):

<img src="img/ekf/kalman/kalman.posterior_example.5.png" width="300">
<img src="img/ekf/kalman/kalman.posterior_example.6.png" width="300">

<br>

Let's look at the detailed data:

| $v_{k} \sim \mathcal{N}\left(2 \mathrm{~m} / \mathrm{s}, 1^{2} \mathrm{~m}^{2} / \mathrm{s}^{2}\right)$ <br> prior (prediction)  | $\sigma^{2}=1.5^{2}$ <br> measurement | posterior (with measurement) |
| :---: | :---: |:---: |
| $\mathcal{N}(2,101)$ | 1.499  | $\mathcal{N}(1.510,2.201) $ |
| $\mathcal{N}(3.510,3.201)$ | 3.907 | $\mathcal{N}(3.743,1.321) $ |
| $\mathcal{N}(5.743, 2.3218)$ | 0.391 | $\mathcal{N}(3.025,1.143) $ |
| $\mathcal{N}(5.025,2.143)$ | 2.289 | $\mathcal{N}(3.690,1.097) $ |
| $\mathcal{N}(5.690,2.097)$ | 3.735 | $\mathcal{N}(4.747,1.086)$ |
||

We see that the $\sigma^2$ for the prior is **similar to or better** than the measurement uncertainty ($\sigma^2 = 1.5^2$)!


### Kalman Filter | **Kalman Gain**

The **update** step for the Kalman Filter now (recall that the posterior is obtained by "mixing") looks like,

<img src="img/ekf/kalman/kalman.gain.1.png" width="300">
<img src="img/ekf/kalman/kalman.gain.2.png" width="300">

<br>

So, consider these simplifications,

$$
\begin{aligned}
\mu & =\frac{\sigma_{z}^{2} \bar{\mu}+\bar{\sigma}^{2} \mu_{z}}{\bar{\sigma}^{2}+\sigma_{z}^{2}} \\
& =K_{1} \mu_{z}+K_{2} \bar{\mu} \\
& =K \mu_{z}+(1-K) \bar{\mu}
\end{aligned}
$$

where $K_2 = 1-K$ is a simplification that works as follows &rarr; the final result tells us whether the posterior is **closer to the prior or the measurement**, _i.e.,_ where does it like on this line?

<img src="img/ekf/kalman/kalman.gain.3.png" width="300">

<br>

Hence, the **Kalman Gain**, 

$$
K = \frac{\bar{\sigma}^{2}}{\bar{\sigma}^{2} + \sigma_{z}^{2}}
$$

The Kalman gains tells us,

- **how much** measurement is **trusted**
- **mixing ratio** between measurement and prior

**Example**: measurement is **three times** more accurate than prior. What is the Kalman Gain?

$$
\begin{gathered}
\bar{\sigma}^{2}=3 \sigma_{z}^{2} \\
K=\frac{3 \sigma_{z}^{2}}{3 \sigma_{Z}^{2}+\sigma_{Z}^{2}}=\frac{3}{4}
\end{gathered}
$$

Hence, the posterior is:

<img src="img/ekf/kalman/kalman.gain.4.png" width="300">

<br>

Now we can write the posterior as:

|||
|----|----|
| **residual** | $y = \mu_z - \bar{\mu}$|
| posterior **mean** | $\mu = \bar{\mu} + Ky$|
| posterior **noise** | $\sigma^2 = (1-K) \bar{\sigma^2}$|
||

(since $\sigma^{2} =\frac{\sigma_{1}^{2} \sigma_{2}^{2}}{\sigma_{1}^{2}+\sigma_{2}^{2}}$).

*Note:** **higher K** &rarr; **more certainty**!

### Kalman Filter | **Summary**

<img src="img/ekf/kalman/kalman.summary.png" width="500">

<br>

1. **Step 0**: **initialize** $x_{0} \sim \mathcal{N}\left(\mu_{0}, \sigma_{0}^{2}\right)$, the initial belief
    - to reasonably random values or initial measurement

2. **Step 1**: **predict**
    -  calculate the prior, $\overline{x_{k}} \sim \mathcal{N}\left(\overline{\mu_{k}},{\overline{\sigma_{k}}}^{2}\right)$, from the previous posterior, $x_{k-1} \sim \mathcal{N}\left(\mu_{k-1}, \sigma_{k-1}^{2}\right)$
    - by incorporating the process model, $f_{x} \sim \mathcal{N}\left(\mu_{f}, \sigma_{f}^{2}\right)$
$$
\begin{gathered}
\overline{\mu_{k}}=\mu_{k-1}+\mu_{f} \\
{\overline{\sigma_{k}}}^{2}=\sigma_{k-1}^{2}+\sigma_{f}^{2}
\end{gathered}
$$

3. **Step 2**: **update**
    - given a measurement, $z_{k}$, compute the residual and the Kalman gain
    - set the posterior, $x_{k}$, between the prior, $\bar{x}_{k}$, and the measurement, $z_{k}$, based on the residual and the Kalman gain

$$
\begin{aligned}
y_{k} & =\mu_{z, k}-\overline{\mu_{k}} \\
K_{k} & =\frac{{\overline{\sigma_{k}}}^{2}}{{\overline{\sigma_{k}}}^{2}+\sigma_{z, k}^{2}} \\
\mu_{k} & =\overline{\mu_{k}}+ K_{k}.y_{k} \\
\sigma_{k}^{2} & =\left(1-K_{k}\right) \bar{\sigma}_{k}^{2}
\end{aligned}
$$


## Multivariate Kalman Filter

In reality state is _not_ single dimensional &rarr; it is **multi-dimensional**. In fact, it is a multi-dimensional **vector**, for instance,

- Example: [position, velocity] ${ }^{\top}$
- Represented by a **multivariate gaussian**:

<img src="img/ekf/multi_kalman/n_dimensional.png" width="300">

Let's look at [position, velocity] ${ }^{\top}$,

<img src="img/ekf/multi_kalman/variance_velocity_position.png" width="300">

How do we represent this? They're two _different_ Gaussians, with different properties. We use an **ellipse** (from [Engineering Media](https://engineeringmedia.com/controlblog/the-kalman-filter)),

<img src="img/ekf/multi_kalman/variances_ellipse.png" width="300">

We represent these unequal variances as an ellipse, where the major and minor axes are set to the variance for that dimension. The above image is graphically showing that we have _more uncertainty in position than we do in velocity_.

This is great for combining the means but what about the **variance**? We need to understand how the two variables, velocity and position, _relate_ to each other, since the state of one variable depends on the other. For instance, the faster that an object is traveling, the **further the position will be from the actual measurements**. Hence, capturing the velocity will allow us to better estimate the position. On the other hand, a better estimation of the position tells us whether our velocity measurements were accurate. 

So what we need to really capture is &rarr; **covariance** between the two variables.  

<img src="img/ekf/multi_kalman/covariance_velocity_position.png" width="300">

Covariance is captured using the **covariance matrix** &rarr; a square matrix with the number of rows and columns equal to the number of state variables. So, our position and velocity system would have a $2 \times 2$ covariance matrix, $P$ where,

|terms| meaning|
|-----|--------|
|diagonal| variances with **itself**|
|off-diagonal| **covariances** of each state w.r.t. **other** states|
||

The **state vector** for our system (also a matrix):

$$
\hat{x} = 
\begin{bmatrix}
position\\
velocity
\end{bmatrix}
$$

So, our position and velocity co-variance can be represented as:

$$
\Sigma = 
\begin{bmatrix}
\text{how pos varies with pos} & \text{how vel varies with pos}\\
\text{how pos varies with vel} & \text{how vel varies with vel}
\end{bmatrix}
$$

Using the actual terms for variance,

$$
\Sigma = 
\begin{bmatrix}
\sigma^2_{11} & \sigma^2_{12} \\
\sigma^2_{21} & \sigma^2_{22} 
\end{bmatrix}
$$

So now, we can represent our multivariate Gaussian as:

$$
\mathcal{N}(\boldsymbol{\mu}, \boldsymbol{\Sigma})=\frac{1}{(2 \pi)^{n / 2}|\boldsymbol{\Sigma}|^{1 / 2}} e^{-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})^{T} \boldsymbol{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu})}
$$

where,

|variable| definition | meaning |
|--------|---------|------------|
|$\mathbf{x}$ | $\left(x_{1}, x_{2}, \ldots, x_{n}\right)$ |state variable |
|$\boldsymbol{\mu}$ | $\left(\mu_{1}, \mu_{2}, \ldots, \mu_{n}\right)$ | mean vector |
| $\Sigma$ | $\Sigma_{\mathrm{i}, \mathrm{j}}=\operatorname{Cov}\left(\mathrm{x}_{\mathrm{i}}, \mathrm{x}_{\mathrm{j}}\right)$ | covariance matrix|
||

Let's look at some examples of multivariate Gaussians and corresponding values:

|example|comments|
|-------|:-------|
|<img src="img/ekf/multi_kalman/multi_g.1.png" width="300">| $x_1$ and $x_2$ are **not** correlated|
|<img src="img/ekf/multi_kalman/multi_g.2.png" width="300">| $x_1$ and $x_2$ are **not** correlated|
|<img src="img/ekf/multi_kalman/multi_g.3.png" width="300">| $x_1$ and $x_2$ are **not** correlated|
|<img src="img/ekf/multi_kalman/multi_g.4.png" width="300">| $x_1$ and $x_2$ **are** correlated &rarr; $x_{1}\left(x_{2}\right)$ gives us information about what $x_{2}\left(x_{1}\right)$ could be|

### Process Model and Noise

Now, we need to figure out how to model the system with these updates to the system model, covariance, multivariate gaussians and what not. Let's look at the position and velocity as examples. 

Recall the state is,

$$
\hat{x} = 
\begin{bmatrix}
position\\
velocity
\end{bmatrix}
=
\begin{bmatrix}
x_{k}\\
\dot{x}_{k}
\end{bmatrix}
$$

> Why is velocity represented as: $\dot{x}_{k}$?

Now, in the original model, our physical equation was:

- $\overline{x_{k+1}}=x_{k}+\dot{x}_{k} \Delta t$
- $\dot{x}$ remains **constant** (_i.e.,_ $\overline{\dot{x}_{k+1}}=\dot{x}_{k}$ )

But, in this multivariate Gaussian version of things, velocity and position are correlated. So,

$$
\overline{\mathbf{x}_{k+1}}=\left[\begin{array}{cc}
\square & \square \\
\square & \square \\
\end{array}\right] \mathbf{x}_{k}
$$

Because the transition from $\mathbf{x_k}$ &rarr; $\overline{\mathbf{x}_{k+1}}$ requires a **vector**!

**Note:** **bold** variables indicate vectors, non bold variables indicate scalars.

Plugging in the remanining parts from the motion equation ($\overline{x_{k+1}}=x_{k}+\dot{x}_{k} \Delta t$) we get,


$$
\overline{\mathbf{x}_{k+1}}=\left[\begin{array}{cc}
1 & \Delta t \\
0 & 1
\end{array}\right] \mathbf{x}_{k}
$$

The matrix, 

$$
\mathbf{F}=\left[\begin{array}{cc}
1 & \Delta t \\
0 & 1
\end{array}\right]
$$

is known as the **state transition matrix**.

So we write the equation as:

$$
\overline{\mathbf{x}_{k+1}} = \mathbf{F} \mathbf{x}_{k}
$$

Let's revisit out multivariate Gaussian definition,

$$
\mathcal{N}(\boldsymbol{\mu}, \Sigma)=\frac{1}{(2 \pi)^{n / 2}|\Sigma|^{1 / 2}} e^{-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})^{T} \Sigma^{-1}(\mathbf{x}-\boldsymbol{\mu})}
$$

We particularly care about $\textcolor{orange}{\Sigma}$,

$$
\mathcal{N}(\boldsymbol{\mu}, \textcolor{orange}{\Sigma})=\frac{1}{(2 \pi)^{n / 2}|\textcolor{orange}{\Sigma}|^{1 / 2}} e^{-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})^{T} \textcolor{orange}{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu})}
$$

$\textcolor{orange}{\Sigma}$ &rarr; **error covariance** (or state covariance):

- represents the state uncertainty
- typically denoted by &rarr; $\mathbf{P}$

So,

$$
\mathbf{P} = 
\begin{bmatrix}
\sigma^2_{11} & \sigma^2_{12} \\
\sigma^2_{21} & \sigma^2_{22} 
\end{bmatrix}
$$

We also need to worry about &rarr; **noise/uncertainty** during state transitions because, well, we live in the real world. Hence, there is a matrix $\mathbf{Q}$ used to represent this,

- uncertainty in state transition (_e.g.,_ friction, winds, etc.)
- white noise (_i.e.,_ zero mean)

So, looking at the state transition, $k \rightarrow k+1$, can we write?

$$
\overline{\mathbf{P}_{k+1}}=\mathbf{P}_{k}+\mathbf{Q} 
$$

This is incorrect! The right way to do this is as follows:

$$
\overline{\mathbf{P}_{k+1}}=\mathbf{F P}_{k} \mathbf{F}^{\mathrm{T}}+\mathbf{Q}
$$

Where, $\mathbf{F}^{\mathrm{T}}$ is the **[transpose](https://en.wikipedia.org/wiki/Transpose)** of matrix $\mathbf{F}$. 


<details>
<summary>Proof and Further Details</summary>

In the given equations, the symbol $E[.]$ represents the expectation operator, also known as the expected value.

- for _scalar_ random variables, the expectation is the **arithmetic average value** you’d expect to observe if you repeated the experiment infinitely many times
- for random _vectors_, the expectation denotes the **vector of expectations of each component**:

Given a random vector:

$$
\mathbf{x} = \begin{bmatrix}
x_1 \\
x_2 \\
\vdots \\
x_n
\end{bmatrix},
$$

the expectation is defined component-wise as:

$$
\mathrm{E}[\mathbf{x}] = \begin{bmatrix}
\mathrm{E}[x_1] \\
\mathrm{E}[x_2] \\
\vdots \\
\mathrm{E}[x_n]
\end{bmatrix}.
$$

Additionally, the expression,

$$
\mathrm{E}\left[(\mathbf{x}-\boldsymbol{\mu})(\mathbf{x}-\boldsymbol{\mu})^{T}\right]
$$

represents the covariance matrix of the random vector $x$, typically denoted by:
$$
\operatorname{Var}(\mathbf{x}) \quad \text{or} \quad \boldsymbol{\Sigma}
$$

Now, we have:

$$
\begin{aligned}
\operatorname{Var}(\mathbf{A x}) & =\mathrm{E}\left[(\mathbf{A}(\mathbf{x}-\boldsymbol{\mu}))(\mathrm{A}(\mathbf{x}-\boldsymbol{\mu}))^{\mathrm{T}}\right] \\
& =\mathrm{E}\left[\left(\mathbf{A}(\mathbf{x}-\boldsymbol{\mu})(\mathbf{x}-\boldsymbol{\mu})^{T}\right) \mathbf{A}^{\mathrm{T}}\right] \\
& \left.=\operatorname{AE}\left[(\mathbf{x}-\boldsymbol{\mu})(\mathbf{x}-\boldsymbol{\mu})^{T}\right)\right] \mathbf{A}^{\mathrm{T}} \\
& =\operatorname{AVar}(\mathbf{x}) \mathbf{A}^{\mathrm{T}}
\end{aligned}
$$

Going back to our state transition model, recall,

$$
\overline{\mathbf{x}_{k+1}}=\mathbf{F} \mathbf{x}_{k}
$$

We have seen, from above, 

$$
\operatorname{Var}(\mathbf{A x})=\mathbf{A V a r}(\mathbf{x}) \mathbf{A}^{\mathrm{T}}
$$

Replacing with the right vectors/paramters,

$$
\operatorname{Var}\left(\mathbf{F x}_{k}\right)=\mathbf{F} \operatorname{Var}\left(\mathbf{x}_{k}\right) \mathbf{F}^{\mathrm{T}}=\mathbf{F P}_{k} \mathbf{F}^{\mathbf{T}}
$$

since, $\mathbf{P}_{k}$ is the (state/error) **covariance** matrix.

</details>

Now, at the system start, we have:

$$
\begin{aligned}
\mathbf{F} & =\left[\begin{array}{cc}
1 & \Delta t \\
0 & 1
\end{array}\right] \quad
\text{and} \quad
\mathbf{P}_{\mathbf{k}} & =\left[\begin{array}{cc}
\sigma_{x_{k}}^{2} & 0 \\
0 & \sigma_{x_{k}}^{2}
\end{array}\right]
\end{aligned}
$$

_i.e.,_ **no correlation** between position and velocity. 

But, after _one_ step (_i.e.,_ **prediction**), 

$$
\begin{aligned}
\overline{\mathbf{P}_{k+1}} & =\mathbf{F P}_{k} \mathbf{F}^{\mathrm{T}} \\
& =\left[\begin{array}{cc}
1 & \Delta t \\
0 & 1
\end{array}\right]\left[\begin{array}{cc}
\sigma_{x_{k}}^{2} & 0 \\
0 & \sigma_{x_{k}}^{2}
\end{array}\right]\left[\begin{array}{cc}
1 & 0 \\
\Delta t & 1
\end{array}\right] \\
& =\left[\begin{array}{cc}
\sigma_{x_{k}}^{2}+\sigma_{x_{k}}^{2} \Delta t^{2} & \textcolor{orange}{\sigma_{x_{k}}^{2} \Delta t} \\
\textcolor{orange}{\sigma_{x_{k}}^{2} \Delta t} & \sigma_{x_{k}}^{2}
\end{array}\right]
\end{aligned}
$$

Position and velocity &rarr; **correlated**!

Let's look at an example:

$$
\begin{array}{llll}
\mathbf{x}_{0}=\left[\begin{array}{l}
x_{0} \\
\dot{x}_{0}
\end{array}\right]=\left[\begin{array}{c}
0 \\
10
\end{array}\right] & \mathbf{F}=\left[\begin{array}{cc}
1 & \Delta t \\
0 & 1
\end{array}\right] & \Delta t=1 \mathrm{~s} & \mathbf{P}_{\mathbf{0}}=\left[\begin{array}{ll}
1 & 0 \\
0 & 3
\end{array}\right] \\
\begin{array}{l}
\text { Initial position }=0 \mathrm{~m}
\end{array} & \overline{x_{k+1}}=x_{k}+\dot{x}_{k} \Delta t & & \text { Initial state covariance } \\
\text { Initial velocity }=10 \mathrm{~m} / \mathrm{s} & \overline{\dot{x}_{k+1}}=\dot{x}_{k} &
\end{array}
$$

<details>
<summary>Example Details</summary>

Recall that we write our model as,

$$
\begin{aligned}
& \overline{\mathbf{x}_{k+1}}=\mathbf{F} \mathbf{x}_{k} \\
& \overline{\mathbf{P}_{k+1}}=\mathbf{F} \mathbf{P}_{k} \mathbf{F}^{\mathrm{T}}+\boldsymbol{Q}
\end{aligned}
$$

Let's forget about $\mathbf{Q}$ for now,

So, our starting state can be represented as (we see that velocty and position are **not correlated**):

<img src="img/ekf/multi_kalman/process_model.1.png" width ="300">

Now, after one iteration/prediction,

$$
\begin{aligned}
\overline{\mathbf{x}_{1}}=\mathbf{F} \mathbf{x}_{0} & =\left[\begin{array}{cc}
1 & \Delta t \\
0 & 1
\end{array}\right]\left[\begin{array}{c}
0 \\
10
\end{array}\right]=\left[\begin{array}{l}
10 \\
10
\end{array}\right] \\
\overline{\mathbf{P}_{1}}=\mathbf{F P}_{0} \mathbf{F}^{\mathrm{T}} & =\left[\begin{array}{cc}
1 & \Delta t \\
0 & 1
\end{array}\right]\left[\begin{array}{cc}
1 & 0 \\
0 & 3
\end{array}\right]\left[\begin{array}{cc}
1 & 0 \\
\Delta t & 1
\end{array}\right] \\
& =\left[\begin{array}{ll}
1 & 3 \\
0 & 3
\end{array}\right]\left[\begin{array}{cc}
1 & 0 \\
\Delta t & 1
\end{array}\right]=\left[\begin{array}{ll}
4 & 3 \\
3 & 3
\end{array}\right]
\end{aligned}
$$

If we plot this, we see that **velocity and position are now correlated**:

<img src="img/ekf/multi_kalman/process_model.2.png" width ="300">

A couple more iterations,

$$
\begin{aligned}
& \overline{\mathbf{x}_{2}}=\left[\begin{array}{l}
20 \\
10
\end{array}\right] \\
& \overline{\mathbf{P}_{2}}=\left[\begin{array}{cc}
13 & 6 \\
6 & 3
\end{array}\right]
\end{aligned}
$$

<img src="img/ekf/multi_kalman/process_model.3.png" width ="300">

$$
\begin{aligned}
& \overline{\mathbf{x}_{3}}=\left[\begin{array}{l}
30 \\
10
\end{array}\right] \\
& \overline{\mathbf{P}_{3}}=\left[\begin{array}{cc}
28 & 9 \\
9 & 3
\end{array}\right]
\end{aligned}
$$

</details>

<br>

<img src="img/ekf/multi_kalman/process_model.4.png" width ="300">

<br>

Hence, after multiple iterations,

- we started with $\mathbf{x}_{0}=\left[\begin{array}{c}0 \mathrm{~m} \\ 10 \mathrm{~m} / \mathrm{s}\end{array}\right]$
- position moves by $10 m$ in each step due to the velocity estimate $=10 \mathrm{~m} / \mathrm{s}$
- velocity estimate **does not change** because we **predict** it based on ${\overline{\dot{x}_{k+1}}}=\dot{x}_{k}$
- position **uncertainty increases**
- position and velocity become more **correlated** because $\overline{x_{k+1}}=x_{k}+\dot{x}_{k} \Delta t$


### Control Input

The state of the system is not only dependant on the sensor and model. Recall that **control input** is meant to drive the system to a particular state. So, we must include it (if it is present) as,

<!-->
$$
\overline{\mathbf{x}_{k+1}}=\mathbf{F} \mathbf{x}_{k}+\mathbf{\textcolor{orange}{B u}}
$$
<-->

<img src="img/ekf/equations/pngs/equations-3.png" width="500">

where,

|term| definition | details|
|:---|:-----------|:-------|
|$\mathbf{u}$ | control input | example: input to motor `ESC`|
|$\mathbf{B}$ |control input model |models the contribution of control input to the state transition|
||

Note: $\mathbf{B}=\mathbf{0}$ if there is no control input.


### Summary of Prediction Model

To summarize,

$$
\begin{aligned}
& \overline{\mathbf{x}_{k+1}}=\mathbf{F} \mathbf{x}_{k}+\mathbf{B} \mathbf{u} \\
& \overline{\mathbf{P}_{k+1}}=\mathbf{F P}_{k} \mathbf{F}^{\mathrm{T}}+\mathbf{Q}
\end{aligned}
$$

- from $\mathbf{x}_{k}$, we predict the next state $\overline{\mathbf{x}_{k+1}}$ (i.e., prior)
- $\mathbf{F}$ and $\mathbf{Q}$ are typically **constant**
- $\mathbf{B u}$ can be set to `0` &rarr; if there is no explicit control input to the system
- $\mathbf{B u}$ can be used to provide additional information &rarr; better prediction


### Measurement Update

As with the simpler Kalman filter, we need to "fix" our prediction using a measurement from the sensor(s) which is essentially a **Gaussian multiplication** step between &rarr; the prior and the measurement, 

$$
\text{prior:} \quad
\mathbf{\mu_1} = \begin{bmatrix}
3.0\\
5.0
\end{bmatrix}
\quad
\mathbf{\Sigma_1} = \begin{bmatrix}
4 & 3\\
3 & 3
\end{bmatrix}
$$

$$
\text{measurement:} \quad
\mathbf{\mu_2} = \begin{bmatrix}
3.3\\
4.8
\end{bmatrix}
\quad
\mathbf{\Sigma_2} = \begin{bmatrix}
3 & -1\\
-1 & 1
\end{bmatrix}
$$

Visually, we can represent these as:

<img src="img/ekf/multi_kalman/measure.1.png" width="300">

<br>

The multivariate Gaussian multiplication equations are:

$$
\boldsymbol{\mu}=\boldsymbol{\Sigma}_{\mathbf{2}}\left(\boldsymbol{\Sigma}_{\mathbf{1}}+\boldsymbol{\Sigma}_{2}\right)^{-\mathbf{1}} \boldsymbol{\mu}_{\mathbf{1}}+\boldsymbol{\Sigma}_{\mathbf{1}}\left(\boldsymbol{\Sigma}_{\mathbf{1}}+\boldsymbol{\Sigma}_{\mathbf{2}}\right)^{\mathbf{- 1}} \boldsymbol{\mu}_{\mathbf{2}} 
$$

$$
\boldsymbol{\Sigma}=\boldsymbol{\Sigma}_{\mathbf{1}}\left(\boldsymbol{\Sigma}_{\mathbf{1}}+\boldsymbol{\Sigma}_{\mathbf{2}}\right)^{-\mathbf{1}} \boldsymbol{\Sigma}_{\mathbf{2}}
$$

Recall the univariate Gaussian equivalents:

$$
\mu=\frac{\sigma_{2}^{2} \mu_{1}+\sigma_{1}^{2} \mu_{2}}{\sigma_{1}^{2}+\sigma_{2}^{2}} \quad \sigma^{2}=\frac{\sigma_{1}^{2} \sigma_{2}^{2}}{\sigma_{1}^{2}+\sigma_{2}^{2}}
$$

The net result is:

<img src="img/ekf/multi_kalman/measure.2.png" width="300">

<br>

A problem with Gaussian multiplication is that the dimensionalities of the state and the measurement **need not match**! For instance,

- state &rarr; $[position, velocity]$
- measurement &rarr; $[position]$

Hence, we need a **measurement function** &rarr; converts a state into a measurement space, _e.g.,_

- different dimensions and/or
- different units (voltage &rarr; distance, celsius &rarr; fahrenheit)

So, incorporating the measurement function, $\mathbf{H}$, we get

<img src="img/ekf/equations/pngs/equations-4.png" width="500">

<br>

**Note:** the "**residual**" is the difference between measurement and prediction.

If we have,

$$
\text{State:} \quad \mathbf{x}=\left[\begin{array}{l}x \\ \dot{x} \\ y \\ \dot{y}\end{array}\right]
\quad
\text{and \quad Measurement:} \quad \mathbf{z}=\left[\begin{array}{l}x \\ y\end{array}\right]
$$

Then the **measurement function**, is

$$
 \mathbf{H}=\left[\begin{array}{llll}1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0\end{array}\right]
$$

Recall that measurement &rarr; also follows a Gaussian and has some noise. Hence it is represented as a **multivariate** Gaussian,

$$
\mathcal{N}\left(\mathbf{z}_{\mathbf{k}}, \textcolor{orange}{\mathbf{R}}\right)
$$

where, the **measurement noise** is given by,

$$
\mathbf{R}=\left[\begin{array}{ccc} 
\square & \ldots & \square \\
\vdots & \ddots & \vdots \\
\square & \cdots & \square
\end{array}\right]
$$

$\mathbf{R}$ &rarr; models the **accuracy** of the sensor,

- $m \times m$ covariance matrix ($m$ &rarr; \# of sensors)
- also models correlations between sensors
- typically **constant**


### State and Uncertainty Update

If this is the state of our system,

<img src="img/ekf/multi_kalman/k_gain.1.png" width="300">

<br>

then let's define **system uncertainty** ($\mathbf{S_k}$) as,

- the sum of (predicted) state noise and sensor noise
- equivalent to $\bar{\sigma}^{2}+\sigma_{Z}^{2}$ in the univariate case

$$
\mathbf{S}_{\mathbf{k}}=\mathbf{H} \overline{\mathbf{P}_{\mathbf{k}}} \mathbf{H}^{\mathrm{T}}+\mathbf{R}
$$

Bringing all of the prior terms together, we can now define &rarr; the **Kalman Gain** ($\mathbf{K_k}$) which is answering the question:

> "how much we can trust the predicted state vs the measurement?"

$$
\mathbf{K}_{\mathbf{k}}=\overline{\mathbf{P}_{\mathbf{k}}} \mathbf{H}^{\mathrm{T}} \mathbf{S}_{\mathbf{k}}^{-1}
$$

So, to update the state and uncertainty,

<img src="img/ekf/multi_kalman/update.png" width="300">

<br>

1. **state update**:

$$
\mathbf{x}_{\mathbf{k}}=\overline{\mathbf{x}}_{k}+\mathbf{K}_{\mathbf{k}} \mathbf{y}_{\mathbf{k}}
$$

2. **state uncertainty update**:

$$
P_{k}=\left(I-K_{k} H\right) \overline{P_{k}}
$$

**Note**: if $\mathbf{K_k}$ is large &rarr; then we're **closer to the measurement**.


Consider the following example:

$$
\overline{\mathbf{x}_{1}}=\left[\begin{array}{l}
10 \\
10
\end{array}\right] \quad \overline{\mathbf{P}_{1}}=\left[\begin{array}{ll}
4 & 3 \\
3 & 3
\end{array}\right]
$$

represented as:

<img src="img/ekf/multi_kalman/update_example.1.png" width="300">


Now consider the following sensor measurement and noise model:

$$
\begin{aligned}
& \mathbf{z}_{\mathbf{1}}=[12], \quad \textcolor{orange}{\mathbf{R}=[1]} \quad \mathbf{H}=[1 0]\\
& \mathbf{y}_{\mathbf{1}}=\mathbf{z}_{\mathbf{1}}-\mathbf{H} \overline{\mathbf{x}_{\mathbf{1}}}=\left[\begin{array}{ll}
12
\end{array}\right]-\left[\begin{array}{ll}
1 & 0
\end{array}\right]\left[\begin{array}{l}
10 \\
10
\end{array}\right]=[2] \\
& \mathbf{S}_{\mathbf{1}}=\mathbf{H} \overline{\mathbf{P}_{\mathbf{1}}} \mathbf{H}^{\mathrm{T}}+\mathbf{R}=\left[\begin{array}{ll}
1 & 0
\end{array}\right]\left[\begin{array}{ll}
4 & 3 \\
3 & 3
\end{array}\right]\left[\begin{array}{l}
1 \\
0
\end{array}\right]+[1]=[5] \\
& \mathbf{K}_{\mathbf{1}}=\overline{\mathbf{P}_{\mathbf{1}}} \mathbf{H}^{\mathrm{T}} \mathbf{S}_{\mathbf{1}}^{-1}=\left[\begin{array}{ll}
4 & 3 \\
3 & 3
\end{array}\right]\left[\begin{array}{l}
1 \\
0
\end{array}\right][1 / 5]=\left[\begin{array}{l}
4 / 5 \\
3 / 5
\end{array}\right] \\
& \mathbf{x}_{\mathbf{1}}=\overline{\mathbf{x}_{1}}+\mathbf{K}_{\mathbf{1}} \mathbf{y}_{\mathbf{1}}=\left[\begin{array}{l}
10 \\
10
\end{array}\right]+\left[\begin{array}{l}
4 / 5 \\
3 / 5
\end{array}\right] 2=\textcolor{orange}{\left[\begin{array}{l}
11.6 \\
11.2
\end{array}\right]} \\
& \mathbf{P}_{\mathbf{1}}=\left(\mathbf{I}-\mathbf{K}_{\mathbf{1}} \mathbf{H}\right) \overline{\mathbf{P}_{1}}=\left[\begin{array}{ll}
4 & 3 \\
3 & 3
\end{array}\right]-\left[\begin{array}{l}
4 / 5 \\
3 / 5
\end{array}\right]\left[\begin{array}{ll}
1 & 0
\end{array}\right]\left[\begin{array}{ll}
4 & 3 \\
3 & 3
\end{array}\right] \\
& =\left[\begin{array}{ll}
0.8 & 0.6 \\
0.6 & 1.2
\end{array}\right]
\end{aligned}
$$

The result looks like,

<img src="img/ekf/multi_kalman/update_example.2.png" width="300">

<br>

Let's see what happens if we change $\mathbf{R}$.


$$
\begin{aligned}
& \mathbf{z}_{\mathbf{1}}=[12], \quad \textcolor{orange}{\mathbf{R}=[4]} \begin{array}{c}
\text {\textcolor{orange}{Degraded sensor accuracy}}
\end{array} \quad \mathbf{H}=\left[\begin{array}{ll}
1 & 0
\end{array}\right] \\
& \mathbf{y}_{\mathbf{1}}=\mathbf{z}_{\mathbf{1}}-\mathbf{H} \overline{\mathbf{x}_{\mathbf{1}}}=[12]-\left[\begin{array}{ll}
1 & 0
\end{array}\right]\left[\begin{array}{l}
10 \\
10
\end{array}\right]=[2] \\
& \mathbf{S}_{\mathbf{1}}=\mathbf{H} \overline{\mathbf{P}_{\mathbf{1}}} \mathbf{H}^{\mathrm{T}}+\mathbf{R}=\left[\begin{array}{ll}
1 & 0
\end{array}\right]\left[\begin{array}{ll}
4 & 3 \\
3 & 3
\end{array}\right]\left[\begin{array}{l}
1 \\
0
\end{array}\right]+[4]=[8] \\
& \mathbf{K}_{\mathbf{1}}=\overline{\mathbf{P}_{\mathbf{1}}} \mathbf{H}^{\mathrm{T}} \mathbf{S}_{\mathbf{1}}^{-1}=\left[\begin{array}{ll}
4 & 3 \\
3 & 3
\end{array}\right]\left[\begin{array}{l}
1 \\
0
\end{array}\right][1 / 8]=\left[\begin{array}{l}
4 / 8 \\
3 / 8
\end{array}\right] \\
& \mathbf{x}_{1}=\overline{\mathbf{x}_{1}}+\mathbf{K}_{1} \mathbf{y}_{1}=\left[\begin{array}{l}
10 \\
10
\end{array}\right]+\left[\begin{array}{l}
4 / 8 \\
3 / 8
\end{array}\right] 2=\textcolor{orange}{\left[\begin{array}{c}
11 \\
10.75
\end{array}\right]} \\
& \mathbf{P}_{\mathbf{1}}=\left(\mathbf{I}-\mathbf{K}_{\mathbf{1}} \mathbf{H}\right) \overline{\mathbf{P}_{1}}=\left[\begin{array}{ll}
4 & 3 \\
3 & 3
\end{array}\right]-\left[\begin{array}{l}
4 / 8 \\
3 / 8
\end{array}\right]\left[\begin{array}{ll}
1 & 0
\end{array}\right]\left[\begin{array}{ll}
4 & 3 \\
3 & 3
\end{array}\right] \\
& =\textcolor{orange}{\left[\begin{array}{cc}
2 & 1.5 \\
1.5 & 1.5
\end{array}\right]}
\end{aligned}
$$

And the result looks like,

<img src="img/ekf/multi_kalman/update_example.3.png" width="300">

<br>

When compared with the previous result, we see that the sensor's accuracy isn't very good so the update, while narrowing things down, is **still imprecise**. 

As we increase the values of $\mathbf{R}$, we see that the sensor measurements matter less &rarr; at $\mathbf{R} = \left[200\right]$, the sensor values don't matter at all! 

$$
\begin{aligned}
& \mathbf{z}_{\mathbf{1}}=[12], \quad \textcolor{orange}{\mathbf{R}=[16]} \quad \mathbf{H}=\left[\begin{array}{ll}
1 & 0
\end{array}\right] \\
& \mathbf{x}_{\mathbf{1}}=\left[\begin{array}{l}
10.4 \\
10.3
\end{array}\right] \\
& \mathbf{P}_{\mathbf{1}}=\left[\begin{array}{ll}
3.2 & 2.4 \\
2.4 & 2.4
\end{array}\right]
\end{aligned}
$$

<img src="img/ekf/multi_kalman/update_example.4.png" width="300">

<br>

$$
\begin{aligned}
& \mathbf{z}_{\mathbf{1}}=[12], \quad \textcolor{orange}{\mathbf{R}=[200]} \quad \mathbf{H}=\left[\begin{array}{ll}
1 & 0
\end{array}\right] \\
& \mathbf{x}_{\mathbf{1}}=\left[\begin{array}{l}
10.039 \\
10.029
\end{array}\right] \\
& \mathbf{P}_{\mathbf{1}}=\left[\begin{array}{ll}
3.922 & 2.941 \\
2.941 & 2.941
\end{array}\right]
\end{aligned}
$$

<img src="img/ekf/multi_kalman/update_example.5.png" width="300">

<br>


### Estimating Hidden Variables

In Kalman filter-based state estimations, **hidden variables** (also called **latent variables** or states) refer to those variables or quantities that cannot be measured directly but influence observable quantities. The Kalman filter estimates these hidden variables by processing available measurements through a mathematical model of system dynamics and measurement processes.

Examples: velocity, attitude, orientation, angular velocity, bias of sensors or internal temperature of a component.

Let's see how **velocity** can be estimated.

Initially, the velocity _estimate_ is, say, $10 \mathrm{~m} / \mathrm{s}$, _i.e.,_

$$
\overline{\mathbf{x}_{1}}=\left[\begin{array}{c}
10 \mathrm{~m} \\
10 \mathrm{~m} / \mathrm{s}
\end{array}\right]
$$

<img src="img/ekf/multi_kalman/hidden.1.png" width="300">

<br>

As we get more measurements (of position) and we work through the Kalman Filter predictions and state updates, we can get more precise estimates for &rarr; velocity!

<img src="img/ekf/multi_kalman/hidden.2.png" width="500">

<br>

The various values are:

| Time | Measurement \( z_k \) | Posterior \( x_k \) | Posterior \( \dot{x}_k \) |
|------|-----------------------|---------------------|---------------------------|
| 1 | 12 | 11.60 | 11.20 |
| 2 | 17 | 18.38 | 8.71  |
| 3 | 22 | 23.67 | 7.28  |
| 4 | 27 | 28.63 | 6.52  |
| 5 | 32 | 33.52 | 6.07  |
| 6 | 37 | 38.40 | 5.80  |
| 7 | 42 | 43.29 | 5.62  |
| 8 | 47 | 48.19 | 5.49  |
| 9 | 52 | 53.10 | 5.40  |
| 10 | 57 | 58.03 | 5.33  |
||

<img src="img/ekf/multi_kalman/hidden.3.png" width="500">

<br>

so then, how is this velocity "inferred"? Let's look at the state equations:


$$
\begin{array}{ll}
\mathbf{S}=\mathbf{H} \overline{\mathbf{P}} \mathbf{H}^{\mathrm{T}}+\mathbf{R} & \mathbf{S}=\mathbf{H} \overline{\mathbf{P}} \mathbf{H}^{\mathrm{T}}+\mathbf{R}=\left[\begin{array}{ll}
1 & 0
\end{array}\right]\left[\begin{array}{cc}
\sigma_{\bar{x}}^{2} & \sigma_{\bar{x} \bar{x}} \\
\sigma_{\bar{x} \bar{x}} & \sigma_{\bar{x}}^{2}
\end{array}\right]\left[\begin{array}{l}
1 \\
0
\end{array}\right]+\left[\sigma_{z}^{2}\right]=\left[\sigma_{\bar{x}}^{2}+\sigma_{z}^{2}\right] \\
\mathbf{K}=\overline{\mathbf{P}} \mathbf{H}^{\mathrm{T}} \mathbf{S}^{-\mathbf{1}} & \mathbf{K}=\overline{\mathbf{P}} \mathbf{H}^{\mathrm{T}} \mathbf{S}^{-\mathbf{1}}=\left[\begin{array}{cc}
\sigma_{\bar{x}}^{2} & \sigma_{\bar{x} \bar{x}} \\
\sigma_{\bar{x} \bar{x}} & \sigma_{\bar{x}}^{2}
\end{array}\right]\left[\begin{array}{l}
1 \\
0
\end{array}\right]\left[\begin{array}{c}
1 \\
\frac{\sigma_{\bar{x}}^{2}+\sigma_{z}^{2}}{2}
\end{array}\right]=\left[\begin{array}{c}
\sigma_{\bar{x}}^{2} /\left(\sigma_{\bar{x}}^{2}+\sigma_{z}^{2}\right) \\
\sigma_{\bar{x} \bar{x}}^{2} /\left(\sigma_{\bar{x}}^{2}+\sigma_{z}^{2}\right)
\end{array}\right] \\
\mathbf{H}=\left[\begin{array}{cc}
1 & 0
\end{array}\right] \quad \mathbf{R}=\left[\sigma_{z}^{2}\right] & \mathbf{x}=\overline{\mathbf{x}}+\mathbf{K y}=\left[\begin{array}{l}
\bar{x} \\
\overline{\dot{x}}
\end{array}\right]+\left[\begin{array}{c}
\sigma_{\bar{x}}^{2} /\left(\sigma_{\bar{x}}^{2}+\sigma_{Z}^{2}\right) \\
\sigma_{\overline{\bar{x}} \bar{x}}^{2} /\left(\sigma_{\bar{x}}^{2}+\sigma_{z}^{2}\right)
\end{array}\right] y
\end{array}
$$

Recall that,

$$
\mathbf{\overline{P}} = \left[\begin{array}{c}
\sigma_{\bar{x}}^{2} /\left(\sigma_{\bar{x}}^{2}+\sigma_{z}^{2}\right) \\
\sigma_{\bar{x} \bar{x}}^{2} /\left(\sigma_{\bar{x}}^{2}+\sigma_{z}^{2}\right)
\end{array}\right] 
$$


Hence, we can obtain the equation for the velocity,

$$
\dot{x}=\bar{x}+\frac{\sigma_{\bar{x} \bar{x}}^{2}}{\sigma_{x}^{2}+\sigma_{z}^{2}} y 
$$

From this equation,

|$\mathbf{y}$|meaning|result|
|------------|:------|:-----|
| $y = 0$ | **perfect** prediction | velocity &rarr; **no change** |
| $y \ne 0$ | **wrong** prediction | velocity &rarr; **updated** |
||

The delta of the update, in the second case, depends on:

- residual and
- $\sigma_{\bar{x} \bar{x}}^2$


### Multivariate Kalman Filter Summary

To summarize, 

<img src="img/ekf/multi_kalman/multivariate_summary.png" width="500">

where,

1. **prediction**

$$
\begin{aligned}
& \overline{\mathbf{x}_k}=\mathbf{F} \mathbf{x}_{k-1}+\mathbf{B} \mathbf{u} \\
& \overline{\mathbf{P}_k}=\mathbf{F P}_{k-1} \mathbf{F}^{\mathrm{T}}+\mathbf{Q}
\end{aligned}
$$

2. **update**

$$
\begin{aligned}
& \mathbf{x}_{\mathbf{k}}=\overline{\mathbf{x}_k}+\mathbf{K}_{\mathbf{k}} \mathbf{y}_{\mathbf{k}} \\
& \mathbf{P}_{\mathbf{k}}=\left(\mathbf{I}-\mathbf{K}_{\mathbf{k}} \mathbf{H}\right) \overline{\mathbf{P}_{\mathbf{k}}}
\end{aligned}
$$

where $\mathbf{K_k}$ and $\mathbf{y_k}$ are calculated as, 

$$
\begin{aligned}
& \mathbf{y}_{\mathbf{k}}=\mathbf{z}_{\mathbf{k}}-\mathbf{H} \overline{\mathbf{x}_{\mathbf{k}}} \\
& \mathbf{S}_{\mathbf{k}}=\mathbf{H} \overline{\mathbf{P}_{\mathbf{k}}} \mathbf{H}^{\mathrm{T}}+\mathbf{R} \\
& \mathbf{K}_{\mathbf{k}}=\overline{\mathbf{P}_{\mathbf{k}}} \mathbf{H}^{\mathrm{T}} \mathbf{S}_{\mathbf{k}}^{-1}
\end{aligned}
$$

An example of a 2D state estimation using multivariate Kalman filters:

<img src="img/ekf/multi_kalman/2d_estimation.png" width="500">


**Note**: the problem with Kalman Filters is that it only works for **linear** systems, _i.e.,_

- next state is a linear function of the previous state
- example of non-linear systems: falling object with air resistance

But the real world is actually **non-linear**! To deal with non-linear systems, we use &rarr; the **extended Kalman filter** (EKF). We will explore this using an important application &rarr; **sensor fusion**.


**References:**

- Kalman, R. E. (1960). [A New Approach to Linear Filtering and Prediction Problems](https://www.cs.unc.edu/~welch/kalman/kalmanPaper.html). Journal of Basic Engineering, 82(1), 35-45.
- Bar-Shalom, Y., Li, X. R., & Kirubarajan, T. (2001). [Estimation with Applications to Tracking and Navigation](https://onlinelibrary.wiley.com/doi/book/10.1002/0471221279). Wiley-Interscience.
- Simon, D. (2006). [Optimal State Estimation: Kalman, H∞, and Nonlinear Approaches](https://onlinelibrary.wiley.com/doi/book/10.1002/0470045345). Wiley-Interscience.
- Thrun, S., Burgard, W., & Fox, D. (2005). [Probabilistic Robotics](https://mitpress.mit.edu/books/probabilistic-robotics). MIT Press.
- Welch, G., & Bishop, G. (2006). [An Introduction to the Kalman Filter](https://www.cs.unc.edu/~welch/media/pdf/kalman_intro.pdf). University of North Carolina at Chapel Hill.
- Julier, S. J., & Uhlmann, J. K. (1997). [A New Extension of the Kalman Filter to Nonlinear Systems](https://www.cs.unc.edu/~welch/kalman/media/pdf/Julier1997_SPIE_KF.pdf). Proc. SPIE 3068, Signal Processing, Sensor Fusion, and Target Recognition VI.
- [Kalman Filter Tutorial](https://www.kalmanfilter.net) - A comprehensive online resource with examples and applications.
- [Kalman and Bayesian Filters in Python](https://github.com/rlabbe/Kalman-and-Bayesian-Filters-in-Python) - A free interactive book and Python library by Roger Labbe.
- [FilterPy](https://filterpy.readthedocs.io) - A Python library for Kalman filtering and optimal estimation.
- Särkkä, S. (2013). [Bayesian Filtering and Smoothing](https://www.cambridge.org/core/books/bayesian-filtering-and-smoothing/C372FB31C5D9A100F8476C1A41A5B700). Cambridge University Press.
- [How a Kalman filter works, in pictures](https://www.bzarg.com/p/how-a-kalman-filter-works-in-pictures/)
- [#2: The Kalman Filter](https://engineeringmedia.com/controlblog/the-kalman-filter) by Brian Douglas
- [The multivariate gaussian distribution](https://web.mat.upc.edu/josep.fabrega/pipe/gaussianes_ndim-e-handout-4pp.pdf) by Josep FÀBREGA<!--rel="stylesheet" href="./custom.sibin.css"-->

# Sensor Fusion 

As we've discussed so far, sensors and state estimation, by its very probabilistic and noisy nature, introduces **errors**. The [example from Bayes' Filter](#bayes-filter) where two (seemingly identical) sensors measure the same object differently, highlights this:

<img src="img/ekf/bayes.lidar.4.png" width="400">

<br>

So, the question is &rarr; _"which sensor do we believe?"_

Maybe, instead of framing it as picking one sensor vs. the other, perhaps we can use **both**? This is the objective of **sensor fusion**.

> Sensor fusion is the process of combining sensory data from multiple sources to obtain more accurate information than would be possible using individual sensors alone.

Recall that individual sensors have inherent limitations:

- **limited accuracy**: each sensor has measurement errors
- **limited range/coverage**: sensors may only work reliably in certain conditions
- **limited sampling rates**: some sensors cannot provide updates fast enough
- **sensor-specific weaknesses**: GPS fails indoors, cameras struggle in darkness, etc.

Sensor fusion addresses these limitations by combining complementary data from multiple sensors, each with different strengths and weaknesses. The goal is to produce a combined result that is more accurate, complete, and robust than any single sensor could provide.


### Kalman Filter for Sensor Fusion

We can, of course, use the Kalman Filter to carry out the sensor fusion. For instance,

- consider State, $\mathbf{x}=\left[\begin{array}{l}x \\ \dot{x}\end{array}\right]$
- **two sensors**, GPS (in metres), odometry (in feet): $\mathbf{z}=\left[\begin{array}{c}z_{G P S} \\ z_{\text {odom }}\end{array}\right]$

So, by using the parameters for the Kalman Filter,

$$
\begin{aligned}
\mathbf{H} & =\left[\begin{array}{cc}
1 & 0 \\
1 / 0.3048 & 0
\end{array}\right] \\
\mathbf{R} & =\left[\begin{array}{cc}
\sigma_{\text {GPS }}^{2} & 0 \\
0 & \sigma_{\text {Odom }}^{2}
\end{array}\right]
\end{aligned}
$$

$$
\begin{aligned}
\mathbf{y}= & \mathbf{z}-\mathbf{H} \overline{\mathbf{x}} \\
\mathbf{y}= & {\left[\begin{array}{c}
z_{G P S} \\
z_{\text {Odom }}
\end{array}\right]-\left[\begin{array}{cc}
1 & 0 \\
1 / 0.3048 & 0
\end{array}\right]\left[\begin{array}{l}
\bar{x} \\
\bar{x}
\end{array}\right] } \\
\mathbf{x}= & \overline{\mathbf{x}}+{\mathbf{K} \mathbf{y}} \\
\end{aligned}
$$

Note that $\mathbf{K}$ and $\mathbf{y}$ are $2 \times 2$ matrices &rarr; it **mixes the GPS and odometry**!

As mentioned earlier, the Kalman Filter doesn't work well with *non-linear** systems. But what _exactly_ is the problem with nonlinear systems?

Recall that Kalman Filter (and any Bayes' Filter) requires the use of Gaussians that has some nice properties but that breaks down in the face of non-linearities:

|mixing of|result |
|:--------|:------|
| two Gaussians | Gaussian |
| Gaussian and linear function | Gaussian |
| Gaussian and non-linear function | **non-Gaussian**|
| linear and non-linear function | **non-Gaussian** |
| two non-linear function | **non-Gaussian** |
||

So, all the nice Kalman filter steps (prediction, measurement, update) **falls apart** when the results are no longer Gaussians. Let's see [two instances of passing a Gaussian through other functions](https://soulhackerslabs.com/sensor-fusion-with-the-extended-kalman-filter-in-ros-2-d33dbab1829d), $y = g(x)$

- a linear one, $g = 0.5*x + 1$
- a non-linear one, $g = \cos(3 * (\frac{x}{2} + 0.7)) * \sin(1.3 * x) — 1.6 * x$

<img src="img/fusion/ekf/gaussian_linear.gif" width="300">
<img src="img/fusion/ekf/gaussian_non_linear.gif" width="300">

<br>

As we see from the second animation, the **output is no longer a Gaussian**.

**Note:** This output distribution also violates the **unimodality assumption** of the Kalman Filter, which requires a single peak. Hence, all of our elegant Kalman filter equations are rendered useless!

Of course, we can try to compute an equivalent of a Gaussian using,

- [Monte Carlo simulations](https://en.wikipedia.org/wiki/Monte_Carlo_method) that uses **repeated random sampling** to obtain numerical results

<img src="img/fusion/ekf/monte_carlo_wiki.gif" width="300" title="Monte Carlo Animation By Titouan Christophe - Own work, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=30599003">

The problem is that this is **not a closed form**, _i.e.,_ it **cannot** be represented as s combination of,

-  constants
- variables
- a finite set of basic functions connected by arithmetic operations (+, −, ×, /, and integer powers)
- function composition

Hence, we still do not have a mathematical function for the Gaussian that can be plugged into the Kalman Equations.

Enter the **[Extended Kalman Filter (EKF)](#extended-kalman-filter-ekf)** that uses **linearization** &rarr; to **approximate** a non-linear function, $g(.)$, by a **linear function that is tangent to $g(.)$** at the **point of interest**. 

EKF achieves this by use of the [Taylor Series Expansion](#taylor-series).

### Taylor Series 

Before diving into the Extended Kalman Filter, it's important to understand Taylor series expansions, which are the mathematical foundation for linearization in EKF.

A Taylor series expansion approximates a function around a specific point using polynomial terms. The Taylor Expansion of a function is an infinite sum of terms (polynomials) expressed in terms of the function’s derivatives at a single point, $a$, expanded as:

$$
f(x) = f(a) + f'(a)(x-a) + \frac{f''(a)}{2!}(x-a)^2 + \frac{f'''(a)}{3!}(x-a)^3 + \ldots
$$

where:

| term | description |
|:-----|:------------|
| $f(a)$ | the function value at point $a$ |
| $f'(a)$, $f''(a)$, etc. | the derivatives of $f$ evaluated at point $a$ |
| $(x-a)$ | represents the deviation from the expansion point |
||

<br>

<img src="img/fusion/ekf/taylor_series_degrees.webp" width="300">

<br>

Note that the higher-order Taylor Expansions provide a **closer approximation** of the original function. But the amount of computation required quickly makes it **intractable**! There is still a use for it though, as we shall see shortly.

For multivariate functions $f(\mathbf{x})$ where $\mathbf{x}$ is a vector, the first-order Taylor expansion around a point $\mathbf{a}$ is:

$f(\mathbf{x}) \approx f(\mathbf{a}) + \nabla f(\mathbf{a})^T(\mathbf{x}-\mathbf{a})$

Where $\nabla f(\mathbf{a})$ is the gradient of $f$ evaluated at $\mathbf{a}$, containing all partial derivatives.

**Example**: Consider a simple nonlinear function $f(x) = x^2$ expanded around $a = 1$:
1. $f(1) = 1$
2. $f'(x) = 2x$, so $f'(1) = 2$
3. First-order Taylor approximation: $f(x) \approx 1 + 2(x-1)$
4. This gives us a linear approximation: $f(x) \approx 2x - 1$

This linear approximation is accurate near $x = 1$ but becomes less accurate as we move away from this point.

**Example 1**: Consider a simple nonlinear function $f(x) = x^2$ expanded around $a = 1$:

1. $f(1) = 1$
2. $f'(x) = 2x$, so $f'(1) = 2$
3. First-order Taylor approximation: $f(x) \approx 1 + 2(x-1)$
4. This gives us a linear approximation: $f(x) \approx 2x - 1$

This linear approximation is accurate near $x = 1$ but becomes less accurate as we move away from this point.

<img src="img/fusion/ekf/taylor-series-fixed.svg" width="300">

<br>

**Example 2**: consider the non-linear function we discussed earlier, 

$$
g = \cos(3 * (\frac{x}{2} + 0.7)) * \sin(1.3 * x) — 1.6 * x
$$

The first-order Taylor expansion of g at a point a is shown below in red. It clearly **does not provide a good approximation** &rarr; if we observe it over a large range of values for $x$.

<img src="img/fusion/ekf/taylor.1.webp" width="300">

<br>

Remember that

- we are only concerned with the approximation at the values of &rarr; the posterior
- we will be **recomputing** such approximations for the new posteriors **after a very short period of time**
- our approximation &rarr; is **quite good** in the **close vicinity of the point of interest**

<img src="img/fusion/ekf/taylor.2.webp" width="300">

<br>

For EKF, we use **first-order Taylor expansions** to &rarr; linearize our nonlinear system and measurement functions.


## Extended Kalman Filter (EKF)

The Extended Kalman Filter addresses the limitations of the linear Kalman Filter by linearizing nonlinear functions **around the current estimate**. For nonlinear systems of the form:

**State Equation**:
$x_k = f(x_{k-1}, u_k) + w_k$

**Measurement Equation**:
$z_k = h(x_k) + v_k$

The EKF linearizes these equations using first-order Taylor series expansions:

$f(x_{k-1}, u_k) \approx f(\hat{x}_{k-1|k-1}, u_k) + F_k(x_{k-1} - \hat{x}_{k-1|k-1})$
$h(x_k) \approx h(\hat{x}_{k|k-1}) + H_k(x_k - \hat{x}_{k|k-1})$

Where:
- $F_k = \left.\frac{\partial f}{\partial x}\right|_{\hat{x}_{k-1|k-1},u_k}$ is the Jacobian of $f$ with respect to $x$
- $H_k = \left.\frac{\partial h}{\partial x}\right|_{\hat{x}_{k|k-1}}$ is the Jacobian of $h$ with respect to $x$

These Jacobian matrices contain all the partial derivatives of the nonlinear functions with respect to each state variable, evaluated at the current estimate. They represent the sensitivity of the functions to small changes in the state.

This linearization allows us to

-  apply the Kalman filter equations to nonlinear systems
- but introduces **approximation errors** when the system is highly nonlinear or when the state estimate is far from the true state.

Let's revisit our earlie example function, $g(.)$ and see what happens when we use the linearized functions (as compared to the Monte-Carlo output):

<img src="img/fusion/ekf/gaussian_linearization.2.webp" width="500">

<br>

We see that the EKF Gaussian is **not exactly the same** as the one fitted from the Monte Carlo simulation, but it is **close enough**. This discrepancy (albeit small) is the price we pay for,

- obtaining a closed form estimate and 
- the low computational costs.

**Note**: these graphs show the results of EKF approximations applied to **scalar** functions but our **state is a vector** so we need to:

- we compute the partial derivative of g with respect to the state
- use [Jacobian matrices](https://en.wikipedia.org/wiki/Jacobian_matrix_and_determinant).


### EKF Algorithm

The EKF algorithm follows these steps:

**1. Prediction Step**:
$$\hat{x}_{k|k-1} = f(\hat{x}_{k-1|k-1}, u_k)$$
$$P_{k|k-1} = F_kP_{k-1|k-1}F_k^T + Q_k$$

**2. Update Step**:
$$K_k = P_{k|k-1}H_k^T(H_kP_{k|k-1}H_k^T + R_k)^{-1}$$
$$\hat{x}_{k|k} = \hat{x}_{k|k-1} + K_k(z_k - h(\hat{x}_{k|k-1}))$$
$$P_{k|k} = (I - K_kH_k)P_{k|k-1}$$

The key difference compared to the linear Kalman filter is that we use the **nonlinear functions**,
- $f$ &rarr; state
- $h$ directly &rarr; measurement prediction

but use their **linearized versions** (Jacobians) for &rarr; covariance calculation.


### EKF and Sensor Fusion

There are **two main approaches** to multi-sensor fusion with EKF:

1. **Centralized Fusion**:
    
- all sensor measurements are processed in a single EKF
- the measurement vector combines all sensor readings:

$$z_k = \begin{bmatrix} z_k^1 \\ z_k^2 \\ \vdots \\ z_k^n \end{bmatrix}$$

- the measurement function and noise covariance are:

$$h(x_k) = \begin{bmatrix} h^1(x_k) \\ h^2(x_k) \\ \vdots \\ h^n(x_k) \end{bmatrix}, \quad R_k = \begin{bmatrix} R_k^1 & 0 & \cdots & 0 \\ 0 & R_k^2 & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & R_k^n \end{bmatrix}$$

3. **Decentralized Fusion**:

- each sensor &rarr; has its own local filter
- the results are combined at a **fusion center**

This approach is **more modular** and **fault-tolerant**.

- the state estimates from individual filters can be combined using covariance intersection:

$$P_{fused}^{-1} = \sum_{i=1}^n P_i^{-1}$$
$$P_{fused}^{-1}\hat{x}_{fused} = \sum_{i=1}^n P_i^{-1}\hat{x}_i$$


**Sensor Covariance and Weighting**

The measurement noise covariance matrix $R_k$ determines how much weight each sensor's measurements receive during fusion. Sensors with **lower measurement uncertainty** (smaller values in $R_k$) &rarr; have **more influence on final state estimate**.

Adaptive methods can dynamically adjust these covariances based on:

- current operating conditions
- sensor health monitoring
- consistency checks between sensors
- historical performance

For example, GPS accuracy might degrade in urban canyons, so its covariance should increase in those environments.

### Example: IMU and GPS Fusion using EKF

Let's consider a common problem: fusing IMU (accelerometer and gyroscope) and GPS data for position tracking.

**State Vector**:
$$
x = [\text{position}_x, \text{position}_y, \text{velocity}_x, \text{velocity}_y, \text{heading}]^T
$$

**Note:** The "$T$" as a superscript after the closing bracket indicates that this is a column vector (transposed from a row vector). This is standard mathematical notation for representing a column vector in a single line of text.

**State Transition**:
Using a constant velocity model with heading changes from gyroscope:

$$f(x_{k-1}, u_k) = \begin{bmatrix}
\text{position}_x + \text{velocity}_x \Delta t \\
\text{position}_y + \text{velocity}_y \Delta t \\
\text{velocity}_x + a_x \Delta t \\
\text{velocity}_y + a_y \Delta t \\
\text{heading} + \omega_z \Delta t
\end{bmatrix}$$

Where $a_x, a_y$ are accelerometer readings and $\omega_z$ is the gyroscope reading (yaw rate).

**Measurement Models**:
- GPS: $h_{GPS}(x_k) = [\text{position}_x, \text{position}_y]^T$
- IMU (for update): $h_{IMU}(x_k) = [\text{velocity}_x, \text{velocity}_y, \text{heading}]^T$

**Jacobian Matrices**:
The state transition Jacobian $F_k$ is:

$$F_k = \begin{bmatrix}
1 & 0 & \Delta t & 0 & 0 \\
0 & 1 & 0 & \Delta t & 0 \\
0 & 0 & 1 & 0 & 0 \\
0 & 0 & 0 & 1 & 0 \\
0 & 0 & 0 & 0 & 1
\end{bmatrix}$$

The measurement Jacobians for GPS and IMU are:

$$H_{GPS} = \begin{bmatrix}
1 & 0 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 & 0
\end{bmatrix}$$

$$H_{IMU} = \begin{bmatrix}
0 & 0 & 1 & 0 & 0 \\
0 & 0 & 0 & 1 & 0 \\
0 & 0 & 0 & 0 & 1
\end{bmatrix}$$


**Pseudocode for Implementation**

```python
# Initialize state and covariance
x_hat = np.zeros(5)  # [pos_x, pos_y, vel_x, vel_y, heading]
P = np.eye(5) * 1000  # Initial uncertainty

# Process noise covariance
Q = np.diag([0.1, 0.1, 1.0, 1.0, 0.01])

# Measurement noise covariance
R_gps = np.diag([5.0, 5.0])  # GPS position accuracy (in meters)
R_imu = np.diag([0.5, 0.5, 0.1])  # IMU velocity and heading accuracy

while True:
    # Get IMU data (acceleration and angular velocity)
    accel_x, accel_y, gyro_z = read_imu()
    
    # Prediction step
    dt = time_since_last_update()
    
    # State transition
    x_hat[0] += x_hat[2] * dt  # pos_x += vel_x * dt
    x_hat[1] += x_hat[3] * dt  # pos_y += vel_y * dt
    x_hat[2] += accel_x * dt   # vel_x += accel_x * dt
    x_hat[3] += accel_y * dt   # vel_y += accel_y * dt
    x_hat[4] += gyro_z * dt    # heading += gyro_z * dt
    
    # State transition Jacobian
    F = np.eye(5)
    F[0, 2] = dt
    F[1, 3] = dt
    
    # Update covariance
    P = F @ P @ F.T + Q
    
    # Check if GPS reading is available
    if gps_available():
        # Get GPS position
        gps_x, gps_y = read_gps()
        
        # GPS measurement Jacobian
        H_gps = np.zeros((2, 5))
        H_gps[0, 0] = 1.0
        H_gps[1, 1] = 1.0
        
        # Innovation
        y = np.array([gps_x, gps_y]) - x_hat[0:2]
        
        # Innovation covariance
        S = H_gps @ P @ H_gps.T + R_gps
        
        # Kalman gain
        K = P @ H_gps.T @ np.linalg.inv(S)
        
        # Update state
        x_hat += K @ y
        
        # Update covariance
        P = (np.eye(5) - K @ H_gps) @ P
```

**Analysis**

1. **high-frequency updates** &rarr; IMU provides updates at $100-1000$ Hz, allowing for **smooth tracking**
2. **drift correction** &rarr; GPS (updating at $1-10$ Hz) corrects the **accumulated drift** from IMU integration
3. **robustness to GPS outages** &rarr; system can continue to provide **reasonable position estimates during short GPS outages**!

The following graph shows a typical position tracking result comparing:

| **data source** | **description** |
|:----------------|:----------------|
| **<span style="color:blue">blue dots</span>** | raw gps data |
| **<span style="color:red">red line</span>** | dead reckoning using only imu data |
| **<span style="color:green">green line</span>** | ekf fusion of gps and imu |
||

<img src="img/fusion/ekf/positional-tracking.svg" width="300">

<br>

### Miscellaneous and Advanced Topics

**Best Practices** when implementing EKF for sensor fusion,

| **best practices** | description |
|:-------------------|:------------|
| **careful state selection** | include only necessary states to avoid computational burden |
| **proper initialization** | set initial covariance to reflect actual uncertainty |
| **tuning noise parameters** | adjust $Q$ and $R$ based on empirical data |
| **consistency monitoring** | check filter consistency using normalized innovation squared (NIS) |
| **fault detection** | implement mechanisms to detect sensor failures |
| **numerical stability** | use square-root or UD factorization for improved numerical properties |
||

<br>

**Handling Non-Gaussian Noise**

EKF assumes that both process and measurement noise are Gaussian. For systems with non-Gaussian noise, consider:
| **method** | description |
|:-----------|:------------|
| **particle filters** | represent the probability distribution using samples |
| **robust kalman filters** | use heavy-tailed distributions to model outliers |
| **pre-filtering** | apply outlier rejection before using EKF |
||


The Extended Kalman Filter is a powerful tool for sensor fusion in nonlinear systems. It provides a principled approach for combining measurements from multiple sensors with different characteristics, rates and accuracies.

Despite its limitations with highly nonlinear systems, EKF remains the workhorse of many practical sensor fusion applications due to its relatively simple implementation and computational efficiency.

For more complex scenarios, consider alternatives like the [Unscented Kalman Filter](#unscented-kalman-filter-comparison), [Particle Filters[(https://en.wikipedia.org/wiki/Monte_Carlo_localization)] or more recent developments in factor graph-based fusion.




### Unscented Kalman Filter Comparison

The EKF uses first-order linearization, which can introduce significant errors for highly nonlinear systems. The **[Unscented Kalman Filter (UKF)](https://soulhackerslabs.com/the-unreasonable-power-of-the-unscented-kalman-filter-with-ros-2-d4c97d4b4bb9)** is an alternative that:

1. selects a set of sigma points around the current state estimate
2. propagates these points through the nonlinear functions
3. computes a weighted mean and covariance from the transformed points

This **avoids the need for explicit Jacobian calculations** and can **handle nonlinearities better**. The computational complexity is similar to EKF for most practical applications.

**Example**: Target Tracking with Radar

To illustrate the difference between EKF and UKF performance, consider a radar-based target tracking scenario:

**System Configuration:**

- single radar measuring range, azimuth, and range-rate to a target
- target following a coordinated turn trajectory (highly nonlinear dynamics)
- measurement frequency: 1 Hz
- state vector: $[x, y, velocity_x, velocity_y, turn\_rate]$

**Nonlinearity Challenges:**

1. coordinate conversion (polar to Cartesian)
2. rotational motion during turns
3. range-dependent measurement noise

**Testing Methodology:**

- 100 Monte Carlo simulations of 120-second trajectories
- Process noise: Medium (acceleration uncertainty σ = 0.5 m/s²)
- Measurement noise: Range (σ = 25m), Azimuth (σ = 0.5°), Range-rate (σ = 3m/s)


Comparison of EKF vs UKF error performance:

<img src="img/fusion/ekf/ukf-radar-diagram.svg" width="300">

<br>

| Parameter | EKF Error | UKF Error | Improvement |
|-----------|-----------|-----------|-------------|
| Position  | 1.45 m    | 0.95 m    | 34.5%       |
| Velocity  | 0.32 m/s  | 0.25 m/s  | 21.9%       |
| Heading   | 2.1 deg   | 1.7 deg   | 19.0%       |
||

**Analysis:**

- UKF **outperforms** the EKF in all state variables
- most significant improvement is in **position estimation** (34.5%)
- improvement becomes more pronounced during **high-rate turns**
- **computational load increased** by approximately $15\%$ for the UKF

**When to Use UKF Instead of EKF:**

- dealing with highly nonlinear system or measurement models
- high accuracy is needed during rapid maneuvers
- Jacobian matrices are difficult to derive or implement
- the additional computational cost is acceptable

The UKF's ability to better capture nonlinear transformations makes it particularly valuable for aerospace, underwater navigation and other domains with complex motion models.



**References**:

- Thrun, S., Burgard, W., & Fox, D. (2005). [Probabilistic Robotics](http://www.probabilistic-robotics.org). MIT Press. [Slides](http://probabilistic-robotics.informatik.uni-freiburg.de/ppt/)
- Bar-Shalom, Y., Li, X.R., & Kirubarajan, T. (2001). Estimation with Applications to Tracking and Navigation. Wiley-Interscience.
- Grewal, M.S., & Andrews, A.P. (2014). Kalman Filtering: Theory and Practice Using MATLAB (4th ed.). Wiley.
- Simon, D. (2006). Optimal State Estimation: Kalman, H∞, and Nonlinear Approaches. Wiley-Interscience.
- Crassidis, J.L., & Junkins, J.L. (2011). Optimal Estimation of Dynamic Systems (2nd ed.). CRC Press.
- [Sensor Fusion with the Extended Kalman Filter in ROS 2](https://soulhackerslabs.com/sensor-fusion-with-the-extended-kalman-filter-in-ros-2-d33dbab1829d)
- [The Unreasonable Power of The Unscented Kalman Filter with ROS 2](https://soulhackerslabs.com/the-unreasonable-power-of-the-unscented-kalman-filter-with-ros-2-d4c97d4b4bb9)
- [The math behind Extended Kalman Filtering](https://medium.com/@sasha_przybylski/the-math-behind-extended-kalman-filtering-0df981a87453) by Sasha Przybylski. Check out the cool video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/dFPCFmd5uJE?si=Iy8K0EeV6TP3amor" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>




