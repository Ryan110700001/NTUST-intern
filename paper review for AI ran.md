## IV. DEPLOYMENT AND RESOURCE REQUIREMENTS FOR AI MODELS IN MOBILE NETWORK NODES

### Selected Papers and Rationale  keyword:<img width="1682" height="185" alt="image" src="https://github.com/user-attachments/assets/9b4fe05e-77b4-45c6-aa01-e3bf776b6f56" />
### Prompt for Chatgpt:
1.""you are a professional journal reader, pls first determine whether this paper conform to my need, my need is IV. DEPLOYMENT AND RESOURCE REQUIREMENTS FOR
AI MODELS IN MOBILE NETWORK NODES
This section analyzes the deployment constraints and computational resources for AI models in mobile network nodes.
We evaluate the deployment conditions and resource allocation
strategies for AI models based on the varying requirements
of different network nodes, including latency tolerance, bandwidth constraints, types of data collection, and inference cycles
to enhance the feasibility assessment.
A. Deployment constraints for AI models in mobile network
nodes
B. Computing resource requirements for AI models in mobile
network nodes
AI deployment in RAN, MEC, and core nodes differs in
latency constraints, data types, and model sizes
Real-time inference at the edge demands lightweight models
with localized training and decision-making [22].
Centralized training and distributed inference architectures
face trade-offs in accuracy, efficiency, and cost 
Different scenarios require tailored resource allocation policies for computing, memory, and bandwidth
A systematic framework is needed to model AI workload
requirements and match them to node capabilities.
2. ""list the requirement I need to do this experiment""
### For Computing Resources
 #### 1.Resource Allocation for Network Slicing in Open RAN
   This article is about Network slicing, seems that not so suited within the topic, if we aren't doing similar things can delete this.
#### 2.Modelling of Computational Resources for 5G RAN  
   - This article covers the cost of implementing O‑RAN and BBU on GPP, providing constraints for:  
     1. Real‑Time Latency Budget  
     2. Virtualization Delay vs. Isolation Trade‑off  
     3. Minimum CPU Frequency Requirement
   **Deployment constraints**
HARQ timing budget: It highlights that 5G RAN’s BBU processing must complete within 3 ms to satisfy the HARQ subframe deadline, and shows experimentally that container‑based virtualization adds negligible overhead at typical CPU frequencies—thereby meeting this strict latency constraint when choosing a deployment platform 
Virtualization platform selection: By comparing VMs, containers, and unikernels, the study demonstrates that containers offer the best trade‑off of isolation vs. deployment and runtime delay, establishing a practical deployment constraint for low‑latency RAN functions
   **Computing‑resource requirements**
Per‑VNF profiling: Using OAI’s dlsim/ulsim tools, it measures processing times for each PHY block (FFT/IFFT, modulation/demodulation, encoding/decoding) across CPU frequencies, MCS indices, and PRB counts, revealing that decoding is almost twice as expensive as encoding and that higher MCS indices drive exponential time increases.
Polynomial complexity model: It then fits these measurements with a Lasso‑regularized polynomial, providing a closed‑form estimator of processing time as a function of CPU frequency, PRB count, and MCS index.<img width="279" height="88" alt="image" src="https://github.com/user-attachments/assets/ea098a81-10b9-4841-ada9-565c02e10d21" />
Systematic framework: This model serves as the “missing link” for elastic resource management—allowing a VIM or scheduler to map VNF workloads to node capacities in real time, based on predicted processing delays.Together, these results give you  the latency and virtualization constraints under which VNFs must run, and precise formulas to estimate the CPU resources needed for each function, thus solving the partial question on deployment constraints and compute‑resource requirements.
### 3.Cost‑Effective Resource Allocation for Multitier Mobile Edge Computing in 5G Mobile Network**  
   - This article focuses on MEC and offers:  
     1. Survey of related MEC optimization work  
     2. Model of deployment cost  
     3. Several MEC optimization algorithms  
     4. Simulation performance results
for multi mobile edge computing, we can use the following to optimize our performance:


**Preparation Checklist**
| preparation                                              | Symbol                          | Description                                                             | Prepared?   |
|---------------------------------------------------|---------------------------------|-------------------------------------------------------------------------|-------------|
| Prepare fixed system parameters                   | **u**                           | Task complexity (D<sub>i</sub>), computational intensity (I<sub>i</sub>), throughput, UE count, CPU frequency | - [ ]       |
| Set total budget threshold                        | **B<sub>thresh</sub>**         | Operator capex limit; ensure `expenses(s) < B_thresh`                   | - [ ]       |
| Configure Bayesian TPE – warm‑up iterations       | **N<sub>warmup</sub>**         | Number of warm‑up iterations (not specified in paper; to decide)       | - [ ]       |
| Configure Bayesian TPE – optimization iterations  | **N<sub>iterations</sub> = 1000** | Number of optimization iterations                                       | - [ ]       |

**CMMRA Optimization Workflow**
1. **Warm‑up Phase**  
   Repeat **N<sub>warmup</sub>** times:  
Evaluate  
<img width="224" height="68" alt="image" src="https://github.com/user-attachments/assets/c84bea83-90b2-4cca-ad1f-b74834453108" />
 
via Monte Carlo (trial_count = 1000) and insert `(s, f(s,u))` into `sample_set`. :contentReference[oaicite:0]{index=0}

2. **Main Iteration Phase**  
For **i = 1…N<sub>iterations</sub>**:  
- Build densities **l(s)** and **g(s)** from `sample_set` via Parzen estimation.  
- Sample a `candidate_set` from **l(s)**.  
- For each candidate **s<sub>i</sub>**, compute Expected Improvement:  
 <img width="319" height="63" alt="image" src="https://github.com/user-attachments/assets/38f0d040-2049-444f-868b-c0979f398516" />

- Pick **s*** with highest EI, evaluate **f(s*,u)** (Monte Carlo), and add `(s*, f(s*,u))` to `sample_set`. :contentReference[oaicite:1]{index=1}

3. **Select Optimal Configuration**  
- From `sample_set`, choose the configuration **s*** with the smallest **f(s,u)** as the (approximate) global optimum. :contentReference[oaicite:2]{index=2}



 ### 4.Resource Management Across Edge Servers in Mobile Edge Computing
   - This article addresses resource management, providing:  
     1. Load balancing and migration in multi‑device/multi‑server scenarios  
     2. Location‑Aware VM Scheduling (ARCES)
   
### 5.Resource-Efficient Generative AI Model Deployment in Mobile Edge Networks
   - This article provides both deployment constraints and  Computing resource requirements for AI models at edge nodes, should be the best one according to the need.  

note we have to calculate this parameters to  estimate our  AI model’s energy consumption using the paper’s framework:
<img width="907" height="501" alt="image" src="https://github.com/user-attachments/assets/e3f22953-e58f-4e2f-8037-6541bdec096b" />
than we put the parameter into this function to get the optimized result<img width="572" height="101" alt="image" src="https://github.com/user-attachments/assets/e96bd34e-0b22-4794-86db-8687240e8284" />
**the paper mentioned an algorithm for Genetic Algorithm–based Model‑Level Deployment Decision Selection which is to efficiently approximate the optimal solution of the NP‑hard edge‐deployment problem.<img width="660" height="665" alt="image" src="https://github.com/user-attachments/assets/85811e8e-3240-4317-aab3-ae82d3ba873c" />





