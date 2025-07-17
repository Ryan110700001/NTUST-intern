## IV. DEPLOYMENT AND RESOURCE REQUIREMENTS FOR AI MODELS IN MOBILE NETWORK NODES

### Selected Papers and Rationale  
![keyword](https://github.com/user-attachments/assets/9b4fe05e-77b4-45c6-aa01-e3bf776b6f56)

#### For Computing Resources
1. **Resource Allocation for Network Slicing in Open RAN**  
   This article is about Network slicing, seems that not so suited within the topic, if we aren't doing similar things can delete this.  
2. **Modelling of Computational Resources for 5G RAN**  
   - This article covers the cost of implementing O‑RAN and BBU on GPP, providing constraints for:  
     1. Real‑Time Latency Budget  
     2. Virtualization Delay vs. Isolation Trade‑off  
     3. Minimum CPU Frequency Requirement

### Deployment Constraints
- **HARQ timing budget:** It highlights that 5G RAN’s BBU processing must complete within 3 ms to satisfy the HARQ subframe deadline, and shows experimentally that container‑based virtualization adds negligible overhead at typical CPU frequencies—thereby meeting this strict latency constraint when choosing a deployment platform.  
- **Virtualization platform selection:** By comparing VMs, containers, and unikernels, the study demonstrates that containers offer the best trade‑off of isolation vs. deployment and runtime delay, establishing a practical deployment constraint for low‑latency RAN functions.

### Computing‑Resource Requirements
- **Per‑VNF profiling:** Using OAI’s dlsim/ulsim tools, it measures processing times for each PHY block (FFT/IFFT, modulation/demodulation, encoding/decoding) across CPU frequencies, MCS indices, and PRB counts, revealing that decoding is almost twice as expensive as encoding and that higher MCS indices drive exponential time increases.  
- **Polynomial complexity model:** It then fits these measurements with a Lasso‑regularized polynomial, providing a closed‑form estimator of processing time as a function of CPU frequency, PRB count, and MCS index.  
  ![polynomial model](https://github.com/user-attachments/assets/ea098a81-10b9-4841-ada9-565c02e10d21)  
- **Systematic framework:** This model serves as the “missing link” for elastic resource management—allowing a VIM or scheduler to map VNF workloads to node capacities in real time, based on predicted processing delays.

Together, these results give you (A) the latency and virtualization constraints under which VNFs must run, and (B) precise formulas to estimate the CPU resources needed for each function, thus solving the partial question on deployment constraints and compute‑resource requirements.

3. **Cost‑Effective Resource Allocation for Multitier Mobile Edge Computing in 5G Mobile Networks**  
   - This article focuses on MEC and offers:  
     1. Survey of related MEC optimization work  
     2. Model of deployment cost  
     3. Several MEC optimization algorithms  
     4. Simulation performance results  
   > For multi mobile edge computing, we can use the following to optimize our performance:

### Preparation Checklist

| Preparation                                     | Description                                                                                     | Prepared? |
|-------------------------------------------------|-------------------------------------------------------------------------------------------------|-----------|
| Prepare fixed system parameters                 | Task complexity (D<sub>i</sub>), computational intensity (I<sub>i</sub>), throughput, UE count, CPU frequency | - [ ]     |
| Set total budget threshold                      | Operator capex limit; ensure `expenses(s) < B_thresh`                                           | - [ ]     |
| Configure Bayesian TPE – warm‑up iterations     | Number of warm‑up iterations (not specified in paper; to decide)                                | - [ ]     |
| Configure Bayesian TPE – optimization iterations| Number of optimization iterations (N<sub>iterations</sub> = 1000)                               | - [ ]     |

4. **Resource Management Across Edge Servers in Mobile Edge Computing**  
   - This article addresses resource management, providing:  
     1. Load balancing and migration in multi‑device/multi‑server scenarios  
     2. Location‑Aware VM Scheduling (ARCES)

5. **Resource‑Efficient Generative AI Model Deployment in Mobile Edge Networks**  
   - This article provides both deployment constraints and computing‑resource requirements for AI models at edge nodes, should be the best one according to the need.

> Note: We have to calculate these parameters to estimate our AI model’s energy consumption using the paper’s framework:  
> ![energy parameters](https://github.com/user-attachments/assets/e3f22953-e58f-4e2f-8037-6541bdec096b)  
> Then we put the parameters into this function to get the optimized result:  
> ![optimization function](https://github.com/user-attachments/assets/e96bd34e-0b22-4794-86db-8687240e8284)  
> **The paper mentioned an algorithm for Genetic Algorithm–based Model‑Level Deployment Decision Selection** which efficiently approximates the optimal solution of the NP‑hard edge‑deployment problem:  
> ![GA Algorithm](https://github.com/user-attachments/assets/85811e8e-3240-4317-aab3-ae82d3ba873c)
