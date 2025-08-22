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




    Xeon® series Processor with Intel Architecture are supported and the platform should be either Intel® Xeon® SkyLake or CascadeLake with at least 2.0 GHz core frequency.
<img width="776" height="324" alt="image" src="https://github.com/user-attachments/assets/c04a828b-d4ef-4a53-bf81-09cf0f429934" />
GPU Model	VRAM (GB)	Suitable Model Scale	Example Models
RTX 5090	32	100B+	Command R+ 104B (Q4), DeepSeek-R1-Distill-Qwen-32B (Q4), Mixtral 8x7B (Q4)
RTX 5080 / Super	24 / 16*	70B+	Llama 70B (Q4 quantized), Gemma 3 12B QAT (INT4), Mixtral 8x7B (Q4)
RTX 5070 Ti Super	18 / 16*	70B+	Llama 8B, Gemma 3 12B QAT (INT4), Phi-3 Medium
RTX 5070 Ti	16	13B–70B	Mixtral 8x7B (Q3), Llama 8B
RTX 5070	12	7B–30B	Same as 5070 Ti, but slower performance
RTX 5060 Ti	12 / 8*	7B–13B	DeepSeek-R1-Distill-Qwen-1.5B (Q4), Mistral 7B (Q4)
RTX 5060	8	3B–7B	TinyLlama, StableLM 3B
RTX 5050	8	3B–7B	Basic LLM use only
