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
| Autonomy is the ability to <br> **perform given tasks** <br> based on the system's perception <br> <scb>without</scb> human intervention |  <img src="img/robot_profile_view.jpg" height="275"> |
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

So far, we've (briefly) talked about...

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


let's not forget the most important question of all...

<img src="img/drax_gamora.avif" width="400">

**why** is gamora?

### high-order functions

In order to answer the following, we need **additional functionality**. Let's go through what that might be.

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
- [hybrid](https://sibin.github.io/papers/2008_NCSU-Dissertation_CheckerMode_SibinMohan.pdf) &rarr; a combination of the two
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
|<center><img src="./img/embedded_arch/asic.webp" width="200"><br>An FPGA</center> | <center><img src="./img/embedded_arch/xilinx_spartan_fpga.webp" width="200"><br>Xilinx Spartan FPGA</center> | 
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
- controlling LCD/OLDEs displays 
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

While there is no "standard" CAN connector (each vehicle may use different ones), the **CAN Bus DB9** connector has becomem the de facto standard:

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
|USB | How USB works: [p:w
art 1](https://www.circuitbread.com/tutorials/how-usb-works-introduction-part-1), [part2](https://www.circuitbread.com/tutorials/how-usb-works-communication-protocol-part-2), [part 3](https://www.circuitbread.com/tutorials/how-usb-works-enumeration-and-configuration-part-3); [USB in a Nutshell (very detailed)](https://www.beyondlogic.org/usbnutshell/usb1.shtml).|
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