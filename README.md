# WSCAD - Registry

This repository includes the datasets and algorithms to perform the experiments made in the paper "Dynamic Provisioning of Container Registries in Edge Computing Infrastructures" submitted to the *XXIV Simpósio em Sistemas Computacionais de Alto Desempenho* (WSCAD). 

## Configuring the environment

# ☁️ Heterogeneous Edge Provisioning Benchmark

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)](https://python.org)
[![Edge Computing](https://img.shields.io/badge/Focus-Edge%20Computing-green?logo=serverless)](https://en.wikipedia.org/wiki/Edge_computing)
[![Paper](https://img.shields.io/badge/Academic-WSCAD%202024-red?logo=googlescholar)](LINK_DO_PDF_SE_TIVER)

## 📌 Project Overview

This project simulates and analyzes **container provisioning strategies** in Mobile Edge Computing (MEC) networks. The core objective was to stress-test a heterogeneous infrastructure mixing **High-Performance x86 Servers** with **Low-Power ARM Devices (Raspberry Pi 5)**.

We validated that integrating low-cost, energy-efficient ARM nodes into the edge mesh **does not compromise service latency**, offering a viable path for cost reduction in large-scale ISP deployments.

> **Research Context:** Originally published as *"Dynamic Register Distribution for Mobile Edge Computing"* at WSCAD Symposium.

---

## 📊 Key Results (Data Analysis)

The simulation compared a baseline infrastructure (100% Enterprise Servers) against a hybrid model (75% Enterprise / 25% Raspberry Pi 5).

| Metric | Outcome | Impact |
| :--- | :--- | :--- |
| **Latency** | **< 2% variation** | Replacing expensive nodes with RPi5 maintained QoS. |
| **Utilization** | **Balanced** | The load balancer successfully distributed tasks to ARM nodes. |
| **Efficiency** | **High** | Validated potential for significant energy savings (Green Computing). |

![Latency Comparison Graph](assets/figura2_latencia.png)
> *Figure 1: Latency comparison showing minimal degradation when introducing ARM nodes.*

---

## 🛠️ Technology & Methodology

This simulation was built using **Python** and the **EdgeSimPy** framework.

- **Dynamic Provisioning Strategies:** Implemented algorithms for Centralized, Peer-to-Peer, and Community-based container distribution.
- **Hardware Modeling:** Modeled CPU/RAM constraints of SGI/HPE servers vs. Raspberry Pi 5.
- **Metrics:** Latency (ms), CPU Usage (%), Network Congestion (Mbps).

## 🚀 How to Run

This project was configured with Poetry to manage its dependencies. Please ensure you have Python 3.10+ and Poetry installed. If not, you can install Poetry following the instructions [here](https://python-poetry.org/docs/#installation).

After installing these tools, you can install the dependencies of the project with the following command:


```sh
poetry install
```

## Building the datasets

To build the necessary datasets to replicate the paper's experiments, run the following commands at the repository root folder:

```sh
poetry run python -m datasets -s 1 -i datasets/inputs/base_minimal.json -o central_minimal -rp central && \
poetry run python -m datasets -s 1 -i datasets/inputs/base_recommended.json -o central_recommended -rp central && \
poetry run python -m datasets -s 1 -i datasets/inputs/base_minimal.json -o community_minimal -rp community -c 6 && \
poetry run python -m datasets -s 1 -i datasets/inputs/base_recommended.json -o community_recommended -rp community -c 6 && \
poetry run python -m datasets -s 1 -i datasets/inputs/base_minimal.json -o p2p_minimal -rp p2p && \
poetry run python -m datasets -s 1 -i datasets/inputs/base_recommended.json -o p2p_recommended -rp p2p
```

## Running the experiments

To run the experiments, navigate to the repository root folder and run the following command:

```sh
poetry run python run_experiments.py
```

Although the script runs a few cases in parallel, we recommend to run the script in background because it might take a while to complete all the executions.

## Getting the results

After the executions finished, the logs are available at the `logs` directory. To analyze the results, run the `analysis.ipynb` notebook. You can modify this notebook to explore different metrics and datasets for various scenarios.
