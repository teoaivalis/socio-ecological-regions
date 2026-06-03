# Regional Grounding of AI Weather Predictions for Historical Analog Retrieval

This repository contains the official implementation, architecture schemas, and evaluation pipelines for anchoring global, data-driven weather foundation models into high-resolution local environmental contexts using a dual-space grounding framework.

---

## Overview

Data-driven weather forecasting models offer improved efficiency but function as black boxes ungrounded in localized environmental contexts. Because counterfactual retraining on global weather architectures is computationally prohibitive, evaluating localized data influence and physical consistency remains a significant challenge. To resolve this resolution and semantic gap, we implement a dual-space grounding framework that aligns continuous atmospheric latent spaces with discrete environmental domain knowledge. We evaluate a multi-axis Environmental Knowledge Graph that anchors dense taxonomic biodiversity, urban morphology, and physical land-cover layers directly into regional disaster hubs. Continuous planetary states are compressed using multi-level encoder configurations trained on ERA5 data, while discrete topological properties are mapped using structured graph representation learning layers. Through a systematic ablation study across multiple graph projections, we quantify the specific impacts of individual environmental variables on regional fidelity. The evaluation demonstrates that the framework successfully filters out geographically proximal but ecologically divergent matches, replacing them with out-of-region historical analogs that elevate average taxonomic similarity. Finally, a systematic analysis of cross-border retrieval patterns reveals that the pipeline maps continuous physical geography into consistent socio-environmental biomes. This work establishes a verifiable physical grounding layer to validate data-driven weather forecasts against localized environmental footprints.

---

## Architecture Framework

The dual-space architecture bridges the gap between planetary neural configurations and regional environmental footprints by running an asymmetric boost fusion over a Continuous Latent Engine and a Structural Domain Engine.

![Framework Architecture Overview](framework.png)

### Key Architecture Components:
1. **Continuous Latent Engine:** Maps multi-level meteorological data cubes from foundational configurations (e.g., Pangu-Weather, ERA5) into a compressed 512-dimensional manifold, isolating vertical thermodynamics and active moisture fluxes.
2. **Structural Domain Engine:** Isolates active subgraphs from a native Neo4j graph database to parameterize regional hubs across taxonomic biodiversity (iNaturalist), urban morphology (LCZ & GHSL), and physical land cover (ESA WorldCover).
3. **Asymmetric Boost Fusion:** Executes a dynamic re-ranking mechanism derived from ordinal graph ranks rather than raw topological weights, ensuring the engine remains resilient to metadata sparsity.

---

## Dataset Access

The multi-axis regional footprints, topological connectivity matrices, and socio-environmental metadata used to populate $\mathcal{G}_E$ are hosted natively on Hugging Face:

👉 **[Socio-Ecological Regions Dataset on Hugging Face Hub](https://huggingface.co/datasets/teoaivalis/socio-ecological-regions)**

---

## Repository Structure

```text
├── data/                  # Placeholder for data caching configurations
├── figures/               # Architecture diagrams and learning curves
│   └── framework_overview.png
├── models/                # 2D and 3D Atmospheric Autoencoders
├── graph/                 # Node2Vec projection scripts and Neo4j queries
├── notebooks/             # Evaluation and rank-shifting analysis examples
├── README.md
└── requirements.txt
