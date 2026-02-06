# FDS-Accelerator
# FDS Matrix Accelerator

This repository contains the full design and implementation of **Flexible Data Structure (FDS)** for matrix computations, developed during my summer internship at NIT Trichy, 2025.

The goal of the project was to address performance inefficiencies in traditional matrix operations on hardware by aligning **data layout** with **computation patterns**. This was achieved by creating specialized cores that handle row-wise, column-wise, tile-based, and sparse matrix segments—much like a systolic array, but tailored to embedded AI workloads.


## Problem Motivation

Traditional matrix multiplications use fixed storage formats like row-major or column-major order. While these are fine in general-purpose processors, they can cause inefficiencies when mapped to hardware:

- Increased memory latency
- Wasted compute cycles on zeroes (in sparse data)
- Poor cache behavior
- More power consumption

To address these, we propose a **modular, layout-aware hardware architecture**, where the way data is stored and accessed depends on how it will be used.


## Project Overview

This project explores:

- A new data structure format called **Flexible Data Structure (FDS)**
- Modular **Verilog cores** for handling different matrix access patterns:
  - row_core (row-wise)
  - col_core (column-wise)
  - tile_core (local extrema in tiles)
  - sparse_core (non-zero-only data)
- A test setup on the **Zybo Z7-10 FPGA**
- A case study using **gem5** to compare performance between FDS and traditional methods


## Architecture Overview

Each matrix is split logically into formats best suited for computation:
- **Row-wise** for predictable traversal
- **Column-wise** for dot product matching
- **Tiled** for local block computation (e.g., min/max)
- **Sparse** for skipping zeros

Each format is assigned to a **dedicated Verilog core**, containing:
- A local register file
- A small instruction set 
- Minimal logic for efficiency

These cores can be extended to work together in a **systolic-array-inspired grid**, allowing scalable, parallel processing of matrix operations.


## Features

- RTL design and testbenches in Verilog for 4 custom cores
- Fully working implementation of row_core on Zybo Z7-10 FPGA
- Functional simulation of all cores in ModelSim
- FDS vs Conventional matrix multiplication comparison in gem5
- Support for 4x4, 8x8, and 16x16 matrix sizes
- LED-based output verification on FPGA using buttons and switches


## Tools Used

- **Vivado**: RTL development and FPGA implementation
- **ModelSim**: Simulation and debugging of Verilog cores
- **gem5**: Performance simulation and analysis of memory access patterns
- **RISC-V Toolchain**: Compiling custom matrix multiplication binaries
- **Zybo Z7-10 FPGA**: Hardware validation
- **C/C++**: Writing test workloads for gem5




