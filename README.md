[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Lei Ningxin

### Student Id:21142708

### Email:nleiaa@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > Your answer goes here.

    1. Tools: Phoronix Test Suite

    2. Configuration: 

       1. CPU Test: pts/compress-7zip compression 24.05

          Why: Compression tasks typically put a heavy load on the CPU and can help measure how well the EC2 instance performs under stress.

          Values: Test compression rating of 7-zip compression 24.05 (MIPS), which the higher the better

       2. Memory Test: pts/ramspeed copy floating point

          Why: Copy floating point ensures the results reflect the performance of more demanding numerical computations.

          Values: The speed of copy floating point (MB/s), which the higher the better.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` | 4326 | 11527.39 |
    | `t2.medium``t2.medium` | 9940 | 19754.02 |
    | `c5d.large``c5d.large` | 7428 | 13666.89 |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

    Performance does not scale linearly with the number of vCPUs or the amount of memory. The underlying architecture influence the performance.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | 4060           | 0.434    |
    | `m5.large` - `m5.large`   | 4930           | 0.168    |
    | `c5n.large` - `c5n.large` | 4940           | 0.140    |
    | `t3.medium` - `c5n.large` | 2150           | 0.684    |
    | `m5.large` - `c5n.large`  | 4950           | 0.320    |
    | `m5.large` - `t3.medium`  | 2040           | 0.689    |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | 31.6           | 64.038   |
    | N. Virginia - N. Virginia | 2500           | 0.243    |
    | Oregon - Oregon           | 4760           | 0.363    |

    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
