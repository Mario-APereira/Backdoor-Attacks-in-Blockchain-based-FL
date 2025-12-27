# Backdoor Attacks on Blockchain-based Federated Learning

This repository contains the implementation, experimental frameworks, and results for the Master's Thesis: **"Backdoor Attacks on Blockchain-based Federated Learning"**.

Federated Learning (FL) enables collaborative training without sharing private data, but it remains vulnerable to adversarial threats like backdoor attacks. This research investigates the effectiveness of these attacks within a **decoupled pooled-mining blockchain architecture** under non-IID settings.

## Research Objectives
* Evaluate the vulnerability of blockchain-based FL against backdoor attacks under various consensus mechanisms.
* Analyze the impact of **non-IID data distributions** and the degree of **decentralization** on model security.
* Investigate the advantages of combining **inter-pool (consensus)** and **intra-pool (robust aggregation)** defenses.

## Experimental Setup

### Architecture
The experiments utilize a **decoupled pooled-mining architecture** where:
* **Clients** are grouped into fixed pools, each coordinated by a **Miner**.
* **Intra-pool**: Miners aggregate updates from their local pool clients.
* **Inter-pool**: A blockchain consensus mechanism elects a winning pool to update the global model.

### Datasets and Models
We evaluate performance across three datasets and three CNN architectures:
* **Datasets**: MNIST, CIFAR-10, and GTSRB.
* **Models**: ResNet-18, EfficientNet-B0, and MobileNet V2.

### Consensus Mechanisms (Inter-pool Defenses)
We evaluate four primary mechanisms:
1. **Proof of Work (PoW)**: Traditional blockchain selection, the first miner to match the previous block's hash wins.
2. **Proof of Federated Learning (PoFL)**: Selection based on model validation accuracy in each round.
3. **Proof of Reputation (PoR)**: Selection based on historical performance and contributions.
4. **Proof of Similarity (PoS)**: Selection based on directional closeness (cosine similarity) to the average update.

### Pool aggregation function (Intra-pool Defenses)
We evaluate two federated learning aggregation mechanisms for miners to aggregate their clients' weights:
1. **FedAvg**: Standard weighted averaging of client updates, without robustness against malicious clients.
2. **Krum**: Byzantine-robust aggregation that selects updates closest to the majority, reducing the impact of poisoned models.

## Attack Scenarios
The repository implements two types of triggers and two attack strategies:
* **Triggers**: 
    * **Red Square**: A visible, static patch in the bottom right corner.
    * **WaNet**: A stealthy, noise-based warping trigger.
* **Strategies**:
    * **Dirty-label**: Attacker poisons samples from various classes and flips labels to a target class.
    * **Clean-label**: Poisoned samples retain their original (target) labels for higher stealth.

### Prerequisites
- Python 3.8+
- PyTorch
- CUDA-enabled GPU (recommended for training)

### Installation
```bash
git clone https://github.com/Mario-APereira/Backdoor-Attacks-in-Blockchain-based-FL.git
cd blockchain-fl-backdoors
pip install -r requirements.txt
