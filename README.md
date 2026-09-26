# Performance Analysis of Type-1 and Type-2 Hypervisors

## Project Overview

This project compares the performance of a **Type-1 hypervisor** and a **Type-2 hypervisor** by running the same CPU benchmark inside virtual machines.

The hypervisors considered are:

* **Proxmox VE** – Type-1 (Bare-Metal) hypervisor
* **VMware Workstation** – Type-2 (Hosted) hypervisor

The performance comparison is carried out using **Sysbench CPU benchmarking** with the same benchmark configuration.

## Objectives

* To understand the working and architecture of Type-1 and Type-2 hypervisors.
* To measure CPU performance inside virtual machines running on both hypervisor types.
* To compare benchmark metrics obtained under the same test conditions.
* To analyze the performance overhead introduced by virtualization.
* To understand the practical differences between bare-metal and hosted virtualization.

## Hypervisors Used

### Type-1 Hypervisor – Proxmox VE

Proxmox VE is a bare-metal virtualization platform that runs directly on the physical hardware.

In this project, Proxmox VE is used to host the virtual machine in which the Sysbench CPU benchmark is executed.

### Type-2 Hypervisor – VMware Workstation

VMware Workstation is a hosted hypervisor that runs as an application on top of a host operating system.

In this project, VMware Workstation is used to create and run the virtual machine in which the same Sysbench CPU benchmark is executed.

## Benchmark Used

The CPU performance is measured using **Sysbench**.

Benchmark command:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The benchmark calculates prime numbers up to a specified limit and reports CPU performance in **events per second**.

### Benchmark Parameters

| Parameter               | Value             |
| ----------------------- | ----------------- |
| Benchmark               | Sysbench CPU      |
| Prime number limit      | 20000             |
| Number of threads       | 1                 |
| Main performance metric | Events per second |

## Metrics Collected

The following values are collected from the Sysbench output:

* Events per second
* Total execution time
* Total number of events
* Minimum latency
* Average latency
* Maximum latency
* 95th percentile latency
* Thread fairness

## Experimental Procedure

The same benchmark procedure is followed for both hypervisors.

1. Set up the virtual machine.
2. Install Sysbench inside the virtual machine.
3. Verify the Sysbench version.
4. Run the CPU benchmark using the same prime-number limit.
5. Record the complete benchmark output.
6. Store the raw output in the `results` directory.
7. Capture screenshots of the benchmark execution.
8. Compare the measured performance values between the two hypervisors.

## Repository Structure

```text
Cloud Computing/
│
├── README.md
│
├── images/
│   ├── VMware/
│   └── Proxmox/
│
└── results/
    ├── VMware/
    │   └── sysbench_cpu.txt
    │
    └── Proxmox/
        └── sysbench_cpu.txt
```

### `images/`

Contains screenshots of the benchmark execution and relevant experimental setup.

### `results/`

Contains the raw Sysbench benchmark outputs for each hypervisor.

## Reproducibility

To reproduce the CPU benchmark, install Sysbench on the virtual machine and run:

```bash
sysbench --version
```

Then execute:

```bash
sysbench cpu --cpu-max-prime=20000 run 
```