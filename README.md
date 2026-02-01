# Multimodal RAG for Context-Aware UAV Navigation

This repository presents a **Multimodal Retrieval-Augmented Generation (RAG)** framework for **context-aware UAV navigation**, integrating visual perception, semantic scene understanding, and telemetry-aware reasoning to enable robust and interpretable decision-making in complex environments.

---

## Project Overview

Autonomous UAV navigation in urban and unstructured environments requires robust perception, long-horizon planning, and reliable decision-making under uncertainty. Vision-only approaches often fail in conditions such as poor lighting, motion blur, or visually ambiguous scenes.  

This project addresses these limitations by proposing a **multimodal fusion framework** that jointly reasons over:
- Visual semantics from RGB images
- Spatial scene layout from semantic segmentation
- UAV state context from telemetry signals

The fused representation is further leveraged using a **Retrieval-Augmented Generation (RAG)** pipeline to support context-aware reasoning and decision support.

---

## Key Contributions

- Multimodal fusion of **vision, scene layout, and telemetry** at the representation level  
- Learnable **gated fusion mechanism** for adaptive modality weighting  
- Improved robustness under low-visibility and ambiguous visual conditions  
- Interpretable analysis of modality contributions through gate trends and feature visualizations  
- Evaluation of fused representations against single-modality baselines  

---

## Methodology

### Visual Encoding
- **BLIP-2** for high-level semantic vision embeddings  
- **SegFormer** for semantic segmentation and spatial scene layout extraction  

### Telemetry Encoding
- Lightweight **MLP encoder** for normalized UAV telemetry parameters  
- Encodes altitude, pitch, roll, yaw, velocity, and battery into a dense latent representation  

### Gated Fusion
- Adaptive gating mechanism learns per-sample modality importance  
- Dynamically balances reliance on visual semantics versus telemetry and scene layout  
- Produces a unified fused embedding for downstream reasoning  

### Retrieval-Augmented Reasoning
- Fused embeddings indexed in a vector store  
- Retrieved context passed to an LLM for grounded and explainable reasoning  

---

## Dataset

- **CARLA-based Multi-View UAV Dataset**
- Modalities:
  - RGB front-view images (640×480)
  - Telemetry JSON files per frame
- Sample pairing aligned using frame identifiers  
- Semantic maps generated from RGB using SegFormer  

---

## Evaluation

- Latent space visualization using **t-SNE / UMAP**
- Cosine similarity heatmaps for modality alignment analysis
- Gate trend analysis to study adaptive modality trust over time
- Comparative analysis of vision-only, telemetry-only, and fused representations  

---

## System Architecture

The system consists of:
1. Visual encoders for semantic and spatial understanding  
2. Telemetry encoder for UAV state representation  
3. Gated fusion module for adaptive multimodal integration  
4. RAG pipeline for context-aware reasoning and decision support  

---

## Repository Structure

```text
.
├── data/                  # Dataset loaders and preprocessing scripts
├── vision/                # BLIP-2 and SegFormer encoders
├── telemetry/             # Telemetry MLP encoder
├── fusion/                # Gated fusion module
├── rag/                   # Vector store and retrieval logic
├── experiments/           # Evaluation and visualization scripts
├── configs/               # Configuration files
└── README.md
