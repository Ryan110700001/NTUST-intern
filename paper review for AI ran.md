## IV. DEPLOYMENT AND RESOURCE REQUIREMENTS FOR AI MODELS IN MOBILE NETWORK NODES

### Selected Papers and Rationale  keyword:<img width="1682" height="185" alt="image" src="https://github.com/user-attachments/assets/9b4fe05e-77b4-45c6-aa01-e3bf776b6f56" />


#### For Computing Resources
1. **Resource Allocation for Network Slicing in Open RAN**
2. **Modelling of Computational Resources for 5G RAN**  
   - This article covers the cost of implementing O‑RAN and BBU on GPP, providing constraints for:  
     1. Real‑Time Latency Budget  
     2. Virtualization Delay vs. Isolation Trade‑off  
     3. Minimum CPU Frequency Requirement  
3. **Cost‑Effective Resource Allocation for Multitier Mobile Edge Computing in 5G Mobile Network**  
   - This article focuses on MEC and offers:  
     1. Survey of related MEC optimization work  
     2. Model of deployment cost  
     3. Several MEC optimization algorithms  
     4. Simulation performance results
for multi mobile edge computing, we can use the following to optimize our performance:


### Preparation Checklist

| Step                                             | Description                                                              | Prepared?   |
|--------------------------------------------------|--------------------------------------------------------------------------|-------------|
| Prepare fixed system parameters                  | Task complexity (D<sub>i</sub>), computational intensity (I<sub>i</sub>), throughput, UE count, CPU frequency | - [ ]       |
| Set total budget threshold                       | Operator capex limit; ensure `expenses(s) < B_thresh`                    | - [ ]       |
| Configure Bayesian TPE – warm‑up iterations      | Number of warm‑up iterations (not specified in paper; to decide)         | - [ ]       |
| Configure Bayesian TPE – optimization iterations | Number of optimization iterations (N<sub>iterations</sub> = 1000)        | - [ ]       |
## CMMRA Optimization Workflow

1. **Warm‑up Phase**  
   Repeat **N<sub>warmup</sub>** times:  
Evaluate  
\[  
  f(s,u) = \frac{N_{\text{failed}}(s,u)}{N_T}  
\]  
via Monte Carlo (trial_count = 1000) and insert `(s, f(s,u))` into `sample_set`. :contentReference[oaicite:0]{index=0}

2. **Main Iteration Phase**  
For **i = 1…N<sub>iterations</sub>**:  
- Build densities **l(s)** and **g(s)** from `sample_set` via Parzen estimation.  
- Sample a `candidate_set` from **l(s)**.  
- For each candidate **s<sub>i</sub>**, compute Expected Improvement:  
  \[  
    \mathrm{EI}(s_i) \propto \Bigl(\gamma + \tfrac{g(s_i)}{l(s_i)}\,(1-\gamma)\Bigr)^{-1}  
  \]  
- Pick **s*** with highest EI, evaluate **f(s*,u)** (Monte Carlo), and add `(s*, f(s*,u))` to `sample_set`. :contentReference[oaicite:1]{index=1}

3. **Select Optimal Configuration**  
- From `sample_set`, choose the configuration **s*** with the smallest **f(s,u)** as the (approximate) global optimum. :contentReference[oaicite:2]{index=2}



4. **Resource Management Across Edge Servers in Mobile Edge Computing**  
   - This article addresses resource management, providing:  
     1. Load balancing and migration in multi‑device/multi‑server scenarios  
     2. Location‑Aware VM Scheduling (ARCES)

   
5. **Resource-Efficient Generative AI Model Deployment in Mobile Edge Networks**
   - This article provides both deployment constraints and  Computing resource requirements for AI models at edge nodes, should be the best one according to the need.
  

note we have to calculate this parameters to  estimate our  AI model’s energy consumption using the paper’s framework:
<img width="907" height="501" alt="image" src="https://github.com/user-attachments/assets/e3f22953-e58f-4e2f-8037-6541bdec096b" />
than we put the parameter into this function to get the optimized result<img width="572" height="101" alt="image" src="https://github.com/user-attachments/assets/e96bd34e-0b22-4794-86db-8687240e8284" />
**the paper mentioned an algorithm for Genetic Algorithm–based Model‑Level Deployment Decision Selection which is to efficiently approximate the optimal solution of the NP‑hard edge‐deployment problem.<img width="660" height="665" alt="image" src="https://github.com/user-attachments/assets/85811e8e-3240-4317-aab3-ae82d3ba873c" />





