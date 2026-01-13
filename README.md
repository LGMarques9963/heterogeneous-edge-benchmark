# ☁️ Heterogeneous Edge Provisioning Benchmark

This repository contains the **experimental framework and datasets** from a **research-based engineering study** that evaluates **container registry placement in heterogeneous edge computing networks**.

The project focuses on how **low-power ARM nodes (Raspberry Pi 5)** can be integrated into **containerized edge platforms** without significantly impacting **application latency**, enabling **lower-cost and more energy-efficient edge infrastructures**.

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)](https://python.org)
[![Edge Computing](https://img.shields.io/badge/Focus-Edge%20Computing-green?logo=serverless)](https://en.wikipedia.org/wiki/Edge_computing)

## 📌 Project Overview

This project simulates and analyzes **container provisioning strategies** in Mobile Edge Computing (MEC) networks. The core objective was to stress-test a heterogeneous infrastructure mixing **High-Performance x86 Servers** with **Low-Power ARM Devices (Raspberry Pi 5)**.

We validated that integrating low-cost, energy-efficient ARM nodes into the edge mesh **does not compromise service latency**, offering a viable path for cost reduction in large-scale ISP deployments.

## What problem does this solve?

In large edge platforms, **container provisioning time** is a major bottleneck:
- Edge nodes need to pull images before applications can start
- Centralized registries create bandwidth and latency bottlenecks
- High-capacity nodes are expensive and energy-intensive

This project investigates whether **smaller, cheaper and more energy-efficient devices** can act as edge registry nodes **without breaking latency requirements**.

---

## What we did

We reproduced and extended a prior large-scale edge simulation using **EdgeSimPy**, introducing **Raspberry Pi 5 nodes** into the mesh.

The simulation included:
- 24 geographically distributed edge servers  
- 36 mobile users  
- Multiple container provisioning strategies:
  - Centralized Registry
  - Peer-to-Peer
  - Community-based
  - Dynamic strategy

We replaced 25% of the original servers with **low-power Raspberry Pi 5 nodes** (4 cores, 8GB RAM) and measured:
- User-perceived latency
- CPU, memory and disk utilization per node
- Impact across provisioning strategies
---

## 📊 Key Results (Data Analysis)

The simulation compared a baseline infrastructure (100% Enterprise Servers) against a hybrid model (75% Enterprise / 25% Raspberry Pi 5).

| Metric | Outcome | Impact |
| :--- | :--- | :--- |
| **Latency** | **< 2% variation** | Replacing expensive nodes with RPi5 maintained QoS. |
| **Utilization** | **Balanced** | The load balancer successfully distributed tasks to ARM nodes. |
| **Efficiency** | **High** | Validated potential for significant energy savings (Green Computing). |

- **No statistically significant increase in application latency**
- Raspberry Pi nodes were **actively used** by the system
- Even under Peer-to-Peer strategies, low-power nodes participated in container distribution
- This suggests that **heterogeneous, low-energy edge meshes are viable**

> **Conclusion:** This supports the idea that **edge platforms can reduce cost and energy consumption** without sacrificing performance.

---

## Why this matters

This has direct implications for:
- **Edge computing platforms**
- **CDNs and microservice delivery**
- **IoT and mobile networks**
- **Cloud cost optimization**
- **Sustainable computing**

It demonstrates that **capacity-aware, dynamic registry placement** enables:
> *“More nodes, less power, same latency.”*


## How this connects to real systems

The same principles apply to:
- Kubernetes image registries
- CDN caching layers
- Edge clusters
- Service meshes
- Geo-distributed microservices

This project models how **placement and replication strategies** affect real-world SLA and infrastructure cost.


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
