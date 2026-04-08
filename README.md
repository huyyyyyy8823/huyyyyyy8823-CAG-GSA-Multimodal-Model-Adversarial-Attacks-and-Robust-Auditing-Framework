# CAG-GSA-Multimodal-Model-Adversarial-Attacks-and-Robust-Auditing-Framework

> **This repository presents the official implementation of the Graph-Structure Attack (GSA) framework, a multi-level adversarial approach designed to audit and expose vulnerabilities in fusion-based Vision-Language Pre-training (VLP) models like BLIP.
Unlike traditional attacks that operate on a single dimension, this framework implements a synergistic multi-channel optimization that simultaneously perturbs pixels, features, and internal reasoning topology.**

---

## 🌟 Core Concept: Multi-Level Coordinated AttackThe defining characteristic of this framework is its ability to perform a unified multi-channel attack. By coordinating perturbations across different abstraction layers of the model, it triggers a systemic performance collapse that structure-agnostic attacks cannot achieve.
### 1. Pixel-Level Perturbation (Visual Fidelity)
* **Universal Patch Generation**:Optimizes a localized, visually constrained patch that can be applied to arbitrary images.
* **Imperceptibility**: Uses a fidelity preservation stream to minimize pixel-level discrepancies and structural distortions (DSSIM), ensuring the attack remains stealthy to human observers.
### 2. Feature-Level Alignment (Semantic Misalignment)
* **Modality Decoupling**: Initiates attack signals to separate the paired image and text representations in the latent space.
* **Feature Drift**: Employs an InfoNCE-based loss to push adversarial visual embeddings away from their target text embeddings.
### 3. Topological-Level Rewiring (Structural Disruption)
* **Cross-modal Attention Graph (CAG)**: Formalizes the model's internal reasoning as a sparse bipartite graph to isolate significant interaction paths between textual tokens and visual patches.
* **Path Decoupling**: Explicitly targets and severs the "semantic bridge" between modalities by maximizing a topological discrepancy loss ($\mathcal{L}_{graph}$).

---

## 🛠 Methodology: 
The GSA FrameworkThe GSA framework operates as a closed-loop optimization cycle involving a Universal Patch Generator ($G_{\theta}$) and an Auxiliary Graph Encoder ($\Phi_{\psi}$).
### Synergistic Optimization
The framework overcomes the non-differentiable gap of discrete graph structures by introducing an auxiliary graph encoder. This allows the structural signals to be backpropagated alongside pixel and feature losses to the continuous patch generator.

The final joint objective function is defined as:

$$\mathcal{L}_{total} = \mathcal{L}_{visual} - \lambda_{g}\mathcal{L}_{graph} + \lambda_{l}\mathcal{L}_{lang}$$ 

### Unified Semantic Dispersion
To achieve stealthy "natural but wrong" hallucinations, GSA incorporates a dispersion mechanism that decouples linguistic fluency from visual grounding. It repels generated content from both ground-truth and batch-wise semantics, forcing the model to rely on its internal language priors.

---

## 📊 Experimental Performance
The multi-level coordination of GSA results in an abrupt degradation of model reasoning capabilities.

### Abrupt Retrieval Degradation
By acting as a topological catalyst, GSA severs the fine-grained connectivity required for cross-modal matching.
* **Recall@1 (MS COCO)**: Drops from 72.3% to a negligible 9.0%.
* **Median Rank (MedR)**: Shifts from 1.0 to 45.0, indicating catastrophic rank shift.

### Targeted Visual Reasoning Failure
GSA successfully dismantles the reasoning logic required for complex VQA tasks:
* **Yes/No Questions**: Achieves 88.5% Targeted ASR.
* **Counting Tasks**: Reaches 82.1% Targeted ASR.
* **Spatial Reasoning**: Reaches 85.3% Targeted ASR.

### Auditing "Plausible Hallucinations"
GSA induces hallucinations that remain syntactically fluent while being factually detached.
* **Semantic Accuracy (CLIP-S)**: Drops to 0.21 (vs. 0.99 clean).
* **Linguistic Fluency (PPL)**: Remains low at 19.2, comparable to clean baselines, proving the outputs are linguistically natural.

---

## 📜 Citation
If you utilize this multi-level coordinated attack framework in your research, please cite:

```bash 
@article{hu2026misguiding,
  title={Misguiding BLIP with Patches: Graph-Structure Attack on Cross-modal Attention Graph of BLIP},
  author={Hu, Yingying and Zhang, Peng and Mo, Minghao and Yang, Hong and Zhao, Peilin and Hoi, Steven C. H.},
  journal={IEEE Transactions on Pattern Analysis and Machine Intelligence (TPAMI)},
  year={2026}
}
```

---

## 📄 License
This work is licensed under a Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License.See [LICENSE](LICENSE) for more information.
