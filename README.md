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

Each node is automatically labeled based on its public IP:1. Prepare your inventory

```bash
country=de
country=us
country=fi[manager]
<manager-ip>

## 📜 License

This project is licensed under the MIT License.

1. Prepare your inventory (inventory.ini)
[manager]
<manager-ip>

[workers]
<worker-ip-1>
<worker-ip-2>
...

2. Install Docker on all nodes
ansible-playbook playbooks/01_docker_prep.yml

3. Deploy the Swarm Cluster
ansible-playbook playbooks/02_swarm_cluster.yml

4. Verify Cluster
ssh root@<manager-ip>
docker node ls

🔍 Example Cluster Output
Multiple nodes across different countries
Automatic labeling
Ready for distributed workloads

Notes
GeoIP detection is based on public IP → may not be 100% accurate
Cloud provider firewalls must allow Swarm ports:
TCP 2377
TCP/UDP 7946
UDP 4789

🔥 Use Cases
Distributed applications
Load-balanced services
Tor relay infrastructure
Monitoring stacks
Multi-region deployments

🛠️ Future Improvements
Portainer integration
Prometheus & Grafana monitoring
Provider-based labeling
Multi-manager HA setup
CI/CD (GitHub Actions)

👨‍💻 Author

Stephan Miebach – IT System Administrator focused on automation, distributed systems, and infrastructure engineering.

🧠 Architektur Autodeploy
Git Push → GitHub Actions → SSH → Ansible Master → Playbook → Cluster
