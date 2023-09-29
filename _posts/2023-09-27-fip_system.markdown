---
layout: post
title:  "How to build a Fiber Photometry System"
date:   2023-09-27 12:00:01 -0800
categories: FIP neuroscience optics
excerpt_separator: <!--more-->
---

At its core, fiber photometry (FIP) is a method used to record and measure changes in fluorescence signals within specific neuronal populations in the living brain. These fluorescence signals can be elicited by genetically encoded calcium indicators (GECIs) or other fluorophores, which glow brighter when a neuron fires. By channeling light through optical fibers directly to a target brain region, and then collecting and analyzing the emitted light in response, scientists can track neuronal activity in real-time.

FIP is minimally invasive and highly popular. However, off-the-shelf FIP systems can be costly and inflexible which is why open-source systems such as [the one presented in this paper](https://www.nature.com/articles/nmeth.3770) were developed. These systems have the advantage that they can record from multiple brain regions simultaneously and that they can be flexibly modified. In addition, building your own system has the important advantage that you'll become intimately familiar with the mechanics of FIP.

In this walk-through we'll go over how build a camera-based FIP system. I'll also share code for the acquisition and analysis of FIP recordings.

<!--more-->

### Source material
The design of this system is largely based on a system that was first presented by Christina Kim in [this](https://www.nature.com/articles/nmeth.3770) paper. The accompanying code to this walkthrough can be found on this [GitHub repository](https://github.com/handejong/Fipster). It consists of:
- [A wiki](https://github.com/handejong/Fipster/wiki) with detailed building instructions
- [MATLAB acquisition code](https://github.com/handejong/Fipster/blob/master/FIP_acquisition.m)
- [GUI-based MATLAB analysis code](https://github.com/handejong/Fipster/tree/master/Fipster_Matlab%20(legacy))
- [Python FIP analysis code](https://github.com/handejong/Fipster/tree/master/Fipster_python)

Note: If you don't feel like building your own system, a pre-build version of this system is available from [NeuroPhotometrics](https://neurophotometrics.com/).

### Parts
See the ["parts_list"](https://github.com/handejong/Fipster/blob/master/FIP%20part%20list.xlsx) Excel sheet on the accompanying GitHub.

### Overview
You are essentially building a rudimentary epifluorescence microscope. A computer (Arduino, or National Instruments pulse generator) generates alternating pulses that trigger LEDs. That same pulse generator generates the pulses that trigger a camera to take pictures of a fiber bundle. Individual fibers are then cropped from these pictures and the pixel intensity is recorded.

![schematic of a FIP setup](https://github.com/handejong/Fipster/blob/master/Images/FIP_setup.jpg?raw=true)

### Building instructions
Putting the parts together is a relatively straightforward process. For a step-by-step guide click [here](https://github.com/handejong/Fipster/wiki).

### Data analysis
The prefered analysis method is using [Fipster Python](https://github.com/handejong/Fipster/tree/master/Fipster_python), but there is also a GUI-based MATLAB package available [here](https://github.com/handejong/Fipster/tree/master/Fipster_Matlab%20(legacy)).


### Example recording
Using our FIP system, we captured the following example of real-time neuronal activity. For this experiment, we utilized GCaMP6m, a calcium indicator, selectively expressed in the glutamatergic neurons of the Lateral Hypothalamus (LH) that project to the VTA. We placed mice in a rectangular arena to roam freely. In the top-right corner of this arena we placed an aversive stimulus: a tissue drenched in formaldehyde, which has a very pungent smell. Note how there is a large positive transient in LH->VTA activity (in green, on the right) every time the mouse encountered the noxious formaldehyde smell.
<video width="100%" controls>
  <source src="https://ars.els-cdn.com/content/image/1-s2.0-S0896627318309966-mmc5.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>