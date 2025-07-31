# HashDrill

# Energy-Efficient CPU Mining Framework

### Description

- A lightweight, cross-platform CPU mining framework written in C with a focus on energy efficiency, hardware awareness, and sustainability
- EcoMiner targets general-purpose processors (especially ARM SoCs) and applies techniques like SIMD, cache optimization, and dynamic scaling to mine or validate with low power consumption

---

## NOTICE

- Please read through this `README.md` to better understand the project's source code and setup instructions
- Also, make sure to review the contents of the `License/` directory
- Your attention to these details is appreciated — enjoy exploring the project!

---

## Problem Statement

- Traditional proof-of-work mining solutions waste significant power on GPU or ASIC computation
- EcoMiner addresses this by offering a CPU-centric, energy-aware alternative that runs efficiently on ARM or x86 CPUs, using C-level optimizations for performance and minimal thermal/power impact

---

## Project Goals

### Energy-Aware Mining Loop

- Design and implement an efficient, RandomX-style memory-hard mining algorithm optimized for CPU execution

### Low-Level Optimization

- Use C for complete control, targeting thread pinning, SIMD vectorization, and hardware-aware computation

---

## Tools, Materials & Resources

### Tools

- C compiler with SIMD support (e.g., GCC/Clang with AVX2 or NEON), Python (for optional backend server)

### Materials

- ARM development board (e.g., Raspberry Pi 4), Thermal and power sensors (Linux APIs)

### Resources

- Linux DVFS interface documentation, FastAPI docs for backend integration

---

## Design Decision

### Language Selection

- Chose C for direct control over threading, memory, and CPU-specific optimizations

### Architecture Compatibility

- Targeted x86_64 and ARMv7/v8 using portable compiler flags and preprocessor detection

### Power Scaling Hooks

- Integrated Linux DVFS APIs and thermal monitoring to dynamically adapt miner workload

---

## Features

### SIMD Optimization

- Accelerated hash loops using AVX2, SSE, or NEON intrinsics

### Adaptive Workload Management

- Auto-throttling and scaling based on battery level, temperature, or system load

### Cross-Platform Execution

- Designed to work on desktops, laptops, and embedded ARM devices with minimal setup

---

## Block Diagram

```plaintext
                         ┌───────────────────────────────┐
                         │      EcoMiner CLI Tool        │
                         │-------------------------------│
                         │ - Optimized Hash Core (C)     │
                         │ - SIMD/Thread Pinned Loops    │
                         │ - Power + Temp Monitor        │
                         └──────┬───────────────┬────────┘
                                │               │
                   ┌───────────▼───────┐   ┌────▼───────────┐
                   │   CPU (ARM/x86)   │   │   Sensors/API  │
                   │ - L1/L2 Caches    │   │ - Thermal Zones│
                   │ - SIMD Extensions │   │ - DVFS Scaling │
                   └──────────┬────────┘   └────────────────┘
                              │
                  Optional Network Sync & Stats API
                              │
                 ┌────────────▼────────────┐
                 │   FastAPI Server (opt)  │
                 │ - Leaderboard Reports   │
                 │ - Device Metrics View   │
                 └─────────────────────────┘
				 
```

---

## Functional Overview

- Launch via command-line and automatically detect CPU features
- Start randomized mining workload across threads pinned to physical cores
- Monitor system temperature and scale frequency or pause under load
- Report metrics to a green backend or display local stats

---

## Challenges & Solutions

### Power-Hungry Loops

- Replaced traditional hash functions with memory-bound, cache-aware RandomX logic

### Cache Contention on Multicore CPUs

- Introduced thread affinity with aligned data structures to avoid thrashing

---

## Lessons Learned

### SIMD Programming in C

- Learned how to write vectorized code paths for AVX2 and NEON to gain measurable performance improvements

### Power & Thermal Adaptation

- Integrated dynamic throttling based on system metrics and Linux interfaces for energy savings

---

## Project Structure

```plaintext
root/
├── License/
│   ├── LICENSE.md
│   │
│   └── NOTICE.md
│
├── .gitattributes
│
├── .gitignore
│
└── README.md

```

---

## Future Enhancements

- Integrate Proof-of-Space variant for hybrid mining
- Build a real-time dashboard using WebSockets and FastAPI
- Add automatic deployment with Docker Compose for miner + backend
- Support new CPU extensions (e.g. ARMv9 SVE)
- Enable solar-powered mining mode with energy-harvesting awareness
