---
layout: post
title:  "How to build a Fiber Photometry System"
date:   2023-09-30 12:00:01 -0800
categories: FIP neuroscience optics
excerpt_separator: <!--more-->
---

At its core, fiber photometry (FIP) is a method used to record and measure changes in fluorescence signals within specific neuronal populations in the living brain. These fluorescence signals can be elicited by genetically encoded calcium indicators (GECIs) or other fluorophores, which glow brighter when a neuron fires. By channeling light through optical fibers directly to a target brain region, and then collecting and analyzing the emitted light in response, scientists can track neuronal activity in real-time.

FIP is minimally invasive and highly popular. However, off-the-shelf FIP systems can be costly and inflexible which is why open-source systems such as [this one](https://www.nature.com/articles/nmeth.3770) were developed. These systems have the advantage that they can record from multiple brain regions simultaneously and that they can be flexibly modified. In addition, building your own system has the important advantage that you'll become intimately familiar with the mechanics of FIP.

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

