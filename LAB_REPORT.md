# LAB REPORT

## Performance Analysis of Type-1 and Type-2 Hypervisors

---

## 1. Introduction

Virtualization allows multiple virtual machines to run on a single physical computer. A hypervisor is the software layer responsible for creating and managing these virtual machines and allocating hardware resources such as CPU, memory, storage, and networking.

Hypervisors are broadly classified into two types:

* **Type-1 hypervisor (Bare-Metal):** Runs directly on the physical hardware.
* **Type-2 hypervisor (Hosted):** Runs on top of a host operating system.

This project performs a performance comparison between a Type-1 hypervisor, **Proxmox VE**, and a Type-2 hypervisor, **VMware Workstation**.

The comparison is performed by running the same CPU benchmark inside virtual machines using **Sysbench**.

---

## 2. Problem Statement

Virtualization introduces some level of overhead because applications running inside a virtual machine do not directly operate on the physical hardware.

The amount of overhead can depend on the hypervisor architecture and the way hardware resources are managed.

Therefore, this project aims to experimentally compare the CPU performance of virtual machines running on a Type-1 and Type-2 hypervisor using the same benchmark conditions.

---

## 3. Objectives

The main objectives of this project are:

1. To understand the concept of virtualization and hypervisors.
2. To study the differences between Type-1 and Type-2 hypervisors.
3. To configure virtual machines on Proxmox VE and VMware Workstation.
4. To execute the same CPU benchmark on both platforms.
5. To collect benchmark performance metrics.
6. To compare the measured CPU performance.
7. To analyze the effect of hypervisor architecture on virtual machine performance.

---

## 4. Hypervisors Used

### 4.1 Proxmox VE

Proxmox VE is used as the **Type-1 hypervisor** in this project.

A Type-1 hypervisor operates directly on the physical hardware rather than depending on a conventional host operating system as an intermediate software layer.

The virtual machine used for the experiment runs on top of the Proxmox virtualization platform.

### 4.2 VMware Workstation

VMware Workstation is used as the **Type-2 hypervisor**.

A Type-2 hypervisor runs as an application within a host operating system. Virtual machines are created and managed through the hosted virtualization software.

For this experiment, the same CPU benchmark is executed inside a virtual machine running through VMware Workstation.

---

## 5. Benchmark Tool

### Sysbench

Sysbench is a benchmarking tool that can be used to evaluate CPU, memory, file I/O, and other system performance characteristics.

For this project, the **CPU benchmark** is used.

The benchmark command is:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The benchmark calculates prime numbers up to the specified limit and measures how many benchmark events can be completed per second.

### Benchmark Configuration

| Parameter               | Value             |
| ----------------------- | ----------------- |
| Benchmark               | Sysbench CPU      |
| Prime number limit      | 20,000            |
| Number of threads       | 1                 |
| Main performance metric | Events per second |

---

## 6. Performance Metrics

The following metrics are collected from the Sysbench output.

### 6.1 Events per Second

Events per second represents the number of benchmark operations completed by the CPU in one second.

A higher value indicates that more benchmark events were completed during the test.

### 6.2 Total Execution Time

This represents the total time taken to complete the benchmark.

### 6.3 Total Number of Events

This represents the total number of benchmark events completed during the test.

### 6.4 Latency

Latency represents the time required to complete individual benchmark operations.

The following latency values are recorded:

* Minimum latency
* Average latency
* Maximum latency
* 95th percentile latency

---

## 7. Experimental Procedure

The following procedure is used for the experiment.

### Step 1: Prepare the Virtual Machine

A virtual machine is created for the experiment on each hypervisor.

### Step 2: Install the Benchmark Tool

Sysbench is installed inside the virtual machine.

The installed version is checked using:

```bash
sysbench --version
```

### Step 3: Run the CPU Benchmark

The following command is executed:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The same benchmark configuration is used for both hypervisors.

### Step 4: Record the Results

The complete Sysbench output is saved as a text file.

The raw benchmark results are stored in:

```text
results/VMware/sysbench_cpu.txt
results/Proxmox/sysbench_cpu.txt
```

### Step 5: Capture Screenshots

Screenshots of the benchmark execution are stored separately for each hypervisor.

```text
images/VMware/
images/Proxmox/
```

### Step 6: Compare the Results

The benchmark metrics obtained from both environments are compared to study their CPU performance.

---

## 8. VMware Workstation Results

The following results were obtained from the VMware Workstation virtual machine.

### VMware Benchmark Configuration

| Parameter          | Result |
| ------------------ | -----: |
| Sysbench version   | 1.0.20 |
| Test               |    CPU |
| Number of threads  |      1 |
| Prime number limit | 20,000 |

### VMware Benchmark Results

| Metric                  | VMware Workstation |
| ----------------------- | -----------------: |
| Events per second       |             684.51 |
| Total time              |          10.0005 s |
| Total number of events  |              6,846 |
| Minimum latency         |            1.31 ms |
| Average latency         |            1.46 ms |
| Maximum latency         |            6.16 ms |
| 95th percentile latency |            1.58 ms |
| Sum latency             |         9991.50 ms |

### VMware Thread Fairness

| Metric                      |         Result |
| --------------------------- | -------------: |
| Events (avg/stddev)         | 6846.0000/0.00 |
| Execution time (avg/stddev) |    9.9915/0.00 |

The complete raw VMware benchmark output is available in:

```text
results/VMware/sysbench_cpu.txt
```

The corresponding screenshots are stored in:

```text
images/VMware/
```

---

## 9. Proxmox VE Results

The Proxmox VE benchmark was executed using the same Sysbench CPU benchmark configuration used for the VMware Workstation experiment.

### Proxmox Benchmark Configuration

| Parameter            | Result        |
|----------------------|--------------:|
| Sysbench version     | Not recorded  |
| Test                 | CPU           |
| Number of threads    | 1             |
| Prime number limit   | 20,000        |

### Proxmox Benchmark Results

| Metric                   | Proxmox VE        |
|--------------------------|------------------:|
| Events per second        | 1716.69           |
| Total time               | 10.0004 s         |
| Total number of events   | 17,169            |
| Minimum latency          | 0.57 ms           |
| Average latency          | 0.58 ms           |
| Maximum latency          | 2.78 ms           |
| 95th percentile latency  | 0.65 ms           |
| Sum latency              | 9996.45 ms        |

### Proxmox Thread Fairness

| Metric                      | Result          |
|----------------------------|-----------------:|
| Events (avg/stddev)        | 17169.0000/0.00  |
| Execution time (avg/stddev)| 9.9965/0.00      |

The complete raw Proxmox benchmark output will be stored in:

```text
results/Proxmox/sysbench_cpu.txt
```

The corresponding screenshots will be stored in:

```text
images/Proxmox/
```

---

## 10. Results Comparison

The benchmark results obtained from VMware Workstation and Proxmox VE are compared below.

| Metric                    | VMware Workstation | Proxmox VE       |
|---------------------------|-------------------:|-----------------:|
| Events per second         | 684.51             | 1716.69          |
| Total time                | 10.0005 s          | 10.0004 s        |
| Total events              | 6,846              | 17,169           |
| Minimum latency           | 1.31 ms            | 0.57 ms          |
| Average latency           | 1.46 ms            | 0.58 ms          |
| Maximum latency           | 6.16 ms            | 2.78 ms          |
| 95th percentile latency   | 1.58 ms            | 0.65 ms          |
| Sum latency               | 9991.50 ms         | 9996.45 ms       |

For the tested configuration, Proxmox VE recorded 1716.69 events per second, while VMware Workstation recorded 684.51 events per second.

The difference in measured throughput is:

```text
1716.69 - 684.51 = 1032.18 events/sec

---

## 11. Performance Analysis

The Sysbench CPU benchmark was executed using the same prime-number limit and single-thread configuration on both hypervisors.

The VMware Workstation virtual machine achieved **684.51 events per second**, while the Proxmox VE virtual machine achieved **1716.69 events per second**.

Therefore, the measured Proxmox VE throughput was approximately **2.51 times** the VMware Workstation throughput in this experiment.

The latency measurements also differed between the two environments. The average latency was **0.58 ms** for Proxmox VE compared with **1.46 ms** for VMware Workstation. The maximum latency was **2.78 ms** on Proxmox VE and **6.16 ms** on VMware Workstation.

The 95th percentile latency was **0.65 ms** for Proxmox VE and **1.58 ms** for VMware Workstation.

The results show that, under the tested configuration, the Proxmox VE virtual machine completed more Sysbench CPU events per second and reported lower latency values than the VMware Workstation virtual machine.

However, these results are specific to the hardware, VM configuration, host system load, and benchmark conditions used during the experiment. They should not be generalized to every Proxmox VE or VMware Workstation installation.

---

## 12. Advantages and Limitations

### Advantages

* The same CPU benchmark is used for both hypervisors.
* The benchmark uses a fixed prime-number limit.
* Raw benchmark outputs are preserved.
* Performance is measured using multiple metrics.
* Screenshots provide evidence of the experiment.

### Limitations

* CPU benchmark results can be affected by the underlying physical hardware.
* Host system load can influence Type-2 hypervisor performance.
* VM resource allocation can affect the results.
* A CPU benchmark alone does not represent every aspect of virtualization performance.
* Results from a single benchmark configuration cannot represent all possible workloads.

---

## 13. Repository Structure

```text
Cloud Computing/
│
├── README.md
├── LAB_REPORT.md
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

---

## 14. Conclusion

This project compared the CPU performance of a Type-1 hypervisor and a Type-2 hypervisor using Proxmox VE and VMware Workstation respectively.

The same Sysbench CPU benchmark was executed with a prime-number limit of 20,000 and one benchmark thread.

In the tested configuration, the Proxmox VE virtual machine achieved **1716.69 events per second**, while the VMware Workstation virtual machine achieved **684.51 events per second**.

The Proxmox VE test also recorded lower average latency, with **0.58 ms** compared with **1.46 ms** for VMware Workstation.

The experimental results therefore show a measurable difference in CPU benchmark performance between the two virtualization environments under the conditions used in this project.

The results are specific to the tested hardware, virtual machine configuration, and system conditions. Further experiments using different workloads, resource allocations, and repeated benchmark runs could provide a broader performance comparison.