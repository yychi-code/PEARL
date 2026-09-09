# PEARL

This repository contains a cleaned implementation for training and ranking evaluation on inductive knowledge graph completion datasets. It includes the core graph model, subgraph extraction pipeline, optional LLM-based multi-hop path ranking, and a single evaluation entry point.

## Project layout
- train.py: training entry point
- test_ranking.py: ranking evaluation and latency benchmarks
- subgraph_extraction/: subgraph generation and dataset loading
- model/: DGL model components
- managers/: training and evaluation loops
- utils/: data and graph utilities
- data/: dataset location
- experiments/: checkpoints and logs

## Installation

Create a Python environment and run:

    pip install -r requirements.txt

Install a DGL build compatible with your PyTorch and CUDA versions when GPU acceleration is required.

## Data

First, download the dataset from [Google Drive](https://drive.google.com/drive/folders/1MFZntSPYmpAOxYVOAWuZot7KMug4-V5v?usp=drive_link) and extract it to the `data/` directory of this project.

Place each dataset under `data/<dataset_name>/` with `train.txt`, `valid.txt`, and `test.txt`. Each line must contain a whitespace-separated triple:

    head_entity relation tail_entity

## Training

    python train.py --dataset fb237_v2 --experiment_name pearl_fb_v2 --hop 2

Training outputs are written to experiments/<experiment_name>/. The ranking script expects best_graph_classifier.pth in that directory.

## Qwen3-4B model

Download it into Qwen3-4B under the current project directory,: [Qwen/Qwen3-4B](https://huggingface.co/Qwen/Qwen3-4B).

## Ranking evaluation

    python test_ranking.py --dataset fb237_v2_ind --experiment_name pearl_fb_v2 --mode sample

Enable local LLM path ranking with:

    python test_ranking.py --dataset fb237_v2_ind --experiment_name pearl_fb_v2 --use_llm_path_filter --llm_path_local_model /path/to/model




