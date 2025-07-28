### B).Demonstration architectures
### 6G Architecture for Enabling Predictable, Reliable and Deterministic Networks: The PREDICT6G Case-----

### 🏗️ Overall Architecture
The architecture is composed of **two main pillars**:
#### 1. AICP - AI-driven Inter-domain Control Plane
- Based on **service-based architecture**
- Organizes network management through **Management Services (MS)** grouped into **Management Domains (MD)**
- Supports E2E deterministic service orchestration, SLA assurance, and failure mitigation
- Integrates multi-domain networks (3GPP, DetNet, IEEE TSN, etc.)
#### 2. MDP - Multi-Domain Data Plane
- A “smart user-plane” with programmable data and control mechanisms
- Supports TSN, DetNet, and integrates with multiple standards
- Enables reliable and predictable data forwarding across domains


#### Architecture Figure
<img width="937" height="438" alt="image" src="https://github.com/user-attachments/assets/ce5a0de5-9b98-4a42-9607-5f94022f6b7e" />

- **Fig. 1**: Overall system architecture (AICP + MDP)
- <img width="435" height="194" alt="image" src="https://github.com/user-attachments/assets/f390c8fd-d072-4e70-9791-ced843faf000" />

- **Fig. 2**: Structure of Management Domains (MDs)
- <img width="851" height="376" alt="image" src="https://github.com/user-attachments/assets/7d131c81-866d-4949-8088-1e50c58ef5f1" />

- **Fig. 3**: Multi-domain management and integration

---

### 🤖 AI/ML Integration

#### AI-Enabled Functional Components:
- **AI/ML Resource Orchestrator**: Manages computational and networking resources
- **Learning Orchestrator**: Manages model training within domains
- **Dataset & Model Registries**: Metadata management for models and datasets
- **Digital Twin (DT)**: Supports real-time simulation and predictive analysis

These components enable:
- Proactive SLA monitoring
- Cross-domain adaptation
- Self-healing and intelligent fault recovery

### 🌐 Multi-Domain Operation
The architecture supports seamless integration across:
- **3GPP domains**: using NEF for configuration and automation
- **DetNet domains**: via path computation, topology exposure
- **IEEE TSN domains**: for time synchronization and deterministic flows

Each domain provides **technology-agnostic APIs** to ensure interoperability while maintaining domain-specific implementations internally.

---

## 🔧 Challenges Addressed

- **Extension to non-deterministic domains**: Optional modules can be deployed to enhance legacy domains with deterministic capabilities.
- **5G–6G transition**: PREDICT-6G provides a pathway to upgrade 5G systems by layering deterministic and AI-enhanced capabilities.

---

## ✅ Relevance to "Demonstration Architectures"

| Criterion | Assessment | Description |
|----------|------------|-------------|
| System-level reference design | ✅✅✅✅ | Clear AICP + MDP architecture with component-level detail |
| Modular functional decomposition | ✅✅✅✅ | Describes MS, MD, and orchestration layers |
| Multi-domain and cross-layer orchestration | ✅✅✅✅ | Strong emphasis on interoperability across 3GPP, DetNet, TSN |
| AI/ML integration | ✅✅✅ | Covers model training, orchestration, and registry layers |
| Prototype/deployment details | ✅✅ | High-level discussion; actual testbed development TBD |

---



