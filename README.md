
# JAILBREAK-R1: Democratizing AI Safety on Gemma 3

![License](https://img.shields.io/badge/License-MIT-00529B)
![Python](https://img.shields.io/badge/Python-3.10%2B-00529B)
![Model](https://img.shields.io/badge/Model-Gemma_3_4B-00529B)
![Hardware](https://img.shields.io/badge/Hardware-Tesla_T4_(15GB)-00529B)
![Status](https://img.shields.io/badge/Status-Research_Prototype-00529B)

**Automated Red Teaming Framework via Resource-Efficient Reinforcement Learning**

---

## 1. Project Overview

**JAILBREAK-R1** is a technical framework designed to address the resource barrier in AI safety research. It enables high-level automated red teaming on state-of-the-art open-weights models (specifically **Google Gemma 3**) using consumer-grade hardware.

By synthesizing **Algorithmic Efficiency** (Group Relative Policy Optimization - GRPO) and **Engineering Optimization** (Unsloth 4-bit Quantization), this framework bridges the gap between manual testing and enterprise-grade adversarial training, reducing VRAM requirements by approximately **80%** compared to standard PPO implementations.

### Core Objectives
1.  **Democratization:** Enabling independent researchers to audit SOTA models on free-tier GPUs.
2.  **Stealth & Effectiveness:** Generating natural language adversarial prompts that bypass perplexity-based filters.
3.  **Defensive Security:** Constructing a "Digital Immune System" for proactive vulnerability patching.

---

## 2. Technical Architecture

The system utilizes a Critic-less Reinforcement Learning approach combined with low-rank adaptation.

```mermaid
graph TD
    subgraph Input_Processing
    A[Harmful Goal] --> B[System Prompt Injection]
    end

    subgraph "JAILBREAK-R1 Engine (Tesla T4)"
    B --> C[<b>Red Team Model</b><br/>Gemma 3 4B<br/>(Unsloth 4-bit / LoRA)]
    D{<b>GRPO Algorithm</b><br/>No Value Network}
    end

    subgraph "Evaluation Loop"
    C --> E[Group Generation<br/>(G=4 Samples)]
    E --> F[Reward Calculation<br/>(Consistency + Diversity)]
    end

    F -->|Advantage Signal| D
    D -->|Policy Update| C
    
    style C fill:#f0f0f0,stroke:#333,stroke-width:1px
    style D fill:#f0f0f0,stroke:#333,stroke-width:1px
```

---

## 3. Resource Feasibility Analysis

We have validated the training pipeline on a single **NVIDIA Tesla T4 (15GB VRAM)** environment.

| Component | Precision | Estimated Memory |
| :--- | :--- | :--- |
| **Model Weights** | 4-bit NF4 | 2.6 GB |
| **LoRA Adapters** | FP16 | 0.2 GB |
| **Optimizer States** | Paged AdamW | 0.4 GB |
| **Activations** | Batch=4 | 8.1 GB |
| **System Overhead** | CUDA Kernels | 1.3 GB |
| **TOTAL PEAK USAGE** | | **~13.8 GB** |

*Status: Feasible with ~1.2 GB safety buffer.*

---

## 4. Installation

### Prerequisites
*   Python 3.10+
*   CUDA 12.1+ (Recommended)
*   Hugging Face Access Token

### Setup
```bash
# Clone the repository
git clone https://github.com/netlab-ui/JAILBREAK-R1.git
cd JAILBREAK-R1

# Create virtual environment
python -m venv venv
source venv/bin/activate

# Install Unsloth and dependencies
pip install "unsloth[colab-new] @ git+https://github.com/unslothai/unsloth.git"
pip install -r requirements.txt
```

---

## 5. Usage Guide

### Training Pipeline
Execute the 3-stage curriculum (Cold Start $\rightarrow$ Warm-up $\rightarrow$ Hardening):

```bash
python main.py \
    --model_name "google/gemma-3-4b-it" \
    --output_dir "./checkpoints" \
    --batch_size 4 \
    --max_steps 500
```

### Evaluation
Assess the Attack Success Rate (ASR) using the Judge Model:

```bash
python evaluate.py --checkpoint "./checkpoints/final_model"
```

---

## 6. Ethical Framework

This research adheres to strict ethical guidelines to prevent misuse:

*   **Defensive Intent:** The framework is developed solely for vulnerability identification and model hardening.
*   **Containment:** Adversarial artifacts are stored in offline/air-gapped environments.
*   **Responsible Disclosure:** Specific vulnerabilities found in Gemma 3 are reported to Google DeepMind following standard embargo protocols (90 days) before public technical release.

---

## 7. Research Team

**Netlab NLP Research Team**  
Faculty of Engineering, Universitas Indonesia

*   **Ganendra Garda Pratama** (Researcher)
*   **Daffa Hardhan** (Researcher)
*   **Leonard Bagaskara Cahyo Widodo** (Researcher)

---

## 8. Citation

If you utilize this framework in your research, please cite:

```bibtex
@article{jailbreakr1_2025,
  title={Democratizing AI Safety: Automated Red Teaming on Gemma 3 via Resource-Efficient Reinforcement Learning},
  author={Pratama, G. G. and Hardhan, D. and Widodo, L. B. C.},
  journal={Netlab NLP Research Team, Universitas Indonesia},
  year={2025}
}
```
