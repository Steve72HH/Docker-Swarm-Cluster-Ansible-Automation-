# Docker-Swarm-Cluster-Ansible-Automation
# 🚀 Distributed Docker Swarm Cluster (Ansible Automation)

This project provides a fully automated setup for a distributed Docker Swarm cluster across multiple providers using Ansible.

It is designed for real-world infrastructure with a focus on scalability, automation, and geo-distributed workloads.

---

## 🧠 Key Features

- 🔧 Automated Docker installation on all nodes
- 🌐 Multi-provider cluster (Hetzner, OVH, etc.)
- ⚙️ Fully automated Swarm initialization and node joining
- 🧠 Idempotent Ansible playbooks (safe re-runs)
- 🌍 Geo-aware node labeling (country-based placement)
- 🔐 Firewall preparation (Swarm ports)
- 🧩 Clean separation of manager and worker roles

---

## 🏗️ Architecture

- **1 Manager Node**
- **Multiple Worker Nodes**
- Distributed across different locations and providers
- Designed for high availability and workload distribution

---

## 🌍 Geo-Aware Scheduling

Each node is automatically labeled based on its public IP:

```bash
country=de
country=us
country=fi
...

## 📜 License

This project is licensed under the MIT License.
