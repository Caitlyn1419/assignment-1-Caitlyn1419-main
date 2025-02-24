[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Yuchen FAN
### Student Id: 21093476
### Email: yfanbi@connect.ust.hk
### Upload Date: 24/02/2024

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > I used the Phoronix Test Suite (PTS) as the measurement tool, which is a comprehensive open-source benchmarking platform. The specific configurations are as follows:

    - CPU Performance Test: Used pts/compress-7zip test with Ultra compression level, and thread count matching the instance's vCPU count. This configuration was chosen because it effectively tests overall CPU performance, including both single-thread and multi-thread capabilities. The measurement results are expressed in MIPS (Million Instructions Per Second), where higher values indicate better compression performance.

    - Memory Performance Test: Used pts/stream test with an array size of 10,000,000 elements, running 3 times and taking the average. This configuration was chosen because the STREAM benchmark is an industry standard for measuring memory bandwidth, and the array size is large enough to ensure the test data doesn't fit entirely in CPU cache. The results are measured in MB/s, representing memory read/write bandwidth.

These tools and parameter choices ensure the reliability and reproducibility of the test results while comprehensively reflecting the performance characteristics of different EC2 instance types.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance                 | Memory performance |
    | ----------- | ------------------------------- | ------------------ |
    | `t2.micro`  |  4081 MIPS (compression rating) |     11437.57 MB/s  |
    | `t2.medium` |  9981 MIPS (compression rating) |     19704.24 MB/s  |
    | `c5d.large` |  7917 MIPS (compression rating) |     14533.55 MB/s  |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |      4100      |  0.228   |
    | `m5.large` - `m5.large`   |      4960      |  0.174   |
    | `c5n.large` - `c5n.large` |      4960      |  0.130   |
    | `t3.medium` - `c5n.large` |      2660      |  0.601   |
    | `m5.large` - `c5n.large`  |      2550      |  0.606   |
    | `m5.large` - `t3.medium`  |      3980      |  0.345   |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |      3370      |   61.042 |
    | N. Virginia - N. Virginia |      4890      |   0.205  |
    | Oregon - Oregon           |      9040      |   0.096  |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
