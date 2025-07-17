## IV. DEPLOYMENT AND RESOURCE REQUIREMENTS FOR AI MODELS IN MOBILE NETWORK NODES

### Resource Allocation for Network Slicing in Open RAN  
This article is about Network slicing, seems that not so suited within the topic, if we aren't doing similar things can delete this.

### Modelling of Computational Resources for 5G RAN  
- This article covers the cost of implementing O‑RAN and BBU on GPP, providing constraints for:  
  1. Real‑Time Latency Budget  
  2. Virtualization Delay vs. Isolation Trade‑off  
  3. Minimum CPU Frequency Requirement  

### Cost‑Effective Resource Allocation for Multitier Mobile Edge Computing in 5G Mobile Networks  
- This article focuses on MEC and offers:  
  1. Survey of related MEC optimization work  
  2. Model of deployment cost  
  3. Several MEC optimization algorithms  
  4. Simulation performance results  

### Resource Management Across Edge Servers in Mobile Edge Computing  
- This article addresses resource management, providing:  
  1. Load balancing and migration in multi‑device/multi‑server scenarios  
  2. Location‑Aware VM Scheduling (ARCES)  

### Resource‑Efficient Generative AI Model Deployment in Mobile Edge Networks  
- This article provides both deployment constraints and computing‑resource requirements for AI models at edge nodes, should be the best one according to the need.

---

#### Preparation Checklist

| Preparation                                     | Description                                                                                     | Prepared? |
|-------------------------------------------------|-------------------------------------------------------------------------------------------------|-----------|
| Prepare fixed system parameters                 | Task complexity (D<sub>i</sub>), computational intensity (I<sub>i</sub>), throughput, UE count, CPU frequency | - [ ]     |
| Set total budget threshold                      | Operator capex limit; ensure `expenses(s) < B_thresh`                                           | - [ ]     |
| Configure Bayesian TPE – warm‑up iterations     | Number of warm‑up iterations (not specified in paper; to decide)                                | - [ ]     |
| Configure Bayesian TPE – optimization iterations| Number of optimization iterations (N<sub>iterations</sub> = 1000)                               | - [ ]     |

---

#### CMMRA Optimization Workflow

1. **Warm‑up Phase**  
   Repeat **N<sub>warmup</sub>** times:  
