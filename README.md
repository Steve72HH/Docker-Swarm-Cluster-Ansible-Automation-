# 🚀 Distributed Docker Swarm Cluster (Ansible + GitOps)

This project provides a fully automated setup for a **distributed Docker Swarm cluster** across multiple providers using **Ansible** and **GitHub Actions (GitOps)**.

It is designed for real-world infrastructure with a focus on:

* Scalability
* Automation
* Geo-distributed workloads
* Reproducibility

---

## 🧠 Key Features

* 🔧 Automated Docker installation on all nodes
* 🌐 Multi-provider cluster (Hetzner, OVH, etc.)
* ⚙️ Fully automated Swarm initialization and node joining
* 🔁 Idempotent Ansible playbooks (safe re-runs)
* 🌍 Geo-aware node labeling (country-based)
* 🔐 Firewall preparation (UFW)
* 🧩 Clean separation of manager and worker roles
* 🚀 GitHub Actions based auto-deployment (GitOps)

---

## 🏗️ Architecture

* **1 Manager Node**
* **Multiple Worker Nodes**
* Distributed across multiple countries/providers

```text
Git Push → GitHub Actions → SSH → Ansible Master → Swarm Cluster
```

---

## 🌍 Geo-Aware Scheduling

Each node is automatically labeled based on its public IP:

```bash
country=de
country=us
country=fi
...
```

Example usage:

```yaml
deploy:
  placement:
    constraints:
      - node.labels.country == de
```

---

## ⚙️ Technologies Used

* Docker Swarm
* Ansible
* GitHub Actions
* UFW Firewall
* GeoIP API (ip-api.com)

---

## 📁 Project Structure

```
docker-swarm-cluster/
├── inventory/
│   └── inventory.ini
├── group_vars/
│   └── all.yml
├── playbooks/
│   ├── 01_docker_prep.yml
│   ├── 02_swarm_cluster.yml
│   └── 03_portainer.yml (optional)
├── scripts/
│   └── cleanup.sh
├── .github/workflows/
│   └── deploy.yml
├── ansible.cfg
├── README.md
└── LICENSE
```

---

## ⚙️ Setup

### 1. Configure Inventory

```ini
[manager]
<manager-ip>

[workers]
<worker-ip-1>
<worker-ip-2>
...
```

---

### 2. Install Docker on all nodes

```bash
ansible-playbook playbooks/01_docker_prep.yml
```

---

### 3. Deploy Swarm Cluster

```bash
ansible-playbook playbooks/02_swarm_cluster.yml
```

---

### 4. Verify Cluster

```bash
ssh root@<manager-ip>
docker node ls
```

---

## 🔍 Example Cluster

* Multi-node cluster
* Geo-labeled nodes
* Ready for distributed workloads

---

## 🔐 Required Ports

Ensure these ports are open (OS + provider firewall):

| Port | Protocol | Purpose            |
| ---- | -------- | ------------------ |
| 2377 | TCP      | Swarm management   |
| 7946 | TCP/UDP  | Node communication |
| 4789 | UDP      | Overlay network    |

---

## 🚀 GitOps Auto Deployment

This project includes a **GitHub Actions pipeline**.

### Workflow:

```text
git push → GitHub Actions → SSH → Ansible → Cluster update
```

---

### Required GitHub Secrets

| Name            | Description                    |
| --------------- | ------------------------------ |
| SSH_PRIVATE_KEY | Private key for Ansible master |
| SSH_HOST        | IP of Ansible master           |

---

### Deployment Trigger

* Runs automatically on push to `main`

---

## 🧪 Optional: Dry Run

```bash
ansible-playbook playbooks/02_swarm_cluster.yml --check
```

---

## 🧹 Cleanup Script

```bash
bash scripts/cleanup.sh
```

Removes all nodes from swarm and resets manager.

---

## ⚠️ Notes

* GeoIP detection is based on IP → not 100% accurate
* Cloud firewalls (Hetzner, OVH) must allow required ports
* Playbooks are idempotent → safe to re-run

---

## 🔥 Use Cases

* Distributed applications
* Load-balanced services
* Tor relay infrastructure
* Monitoring clusters
* Multi-region deployments

---

## 🛠️ Roadmap

* [ ] Portainer integration
* [ ] Prometheus + Grafana monitoring
* [ ] Provider-based labeling
* [ ] Multi-manager HA setup
* [ ] Zero-downtime deployments
* [ ] Advanced CI/CD pipelines

---

## 📜 License

This project is licensed under the MIT License.

---

## 👨‍💻 Author

Stephan Miebach – IT System Administrator

Focus: Automation, Distributed Systems, Security, Tor, Linux, AI

---


