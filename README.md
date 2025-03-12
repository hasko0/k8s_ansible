Kubernetes Deployment Automation with Ansible
📌 Overview
This project automates the deployment of a Kubernetes cluster on Ubuntu 22.04 using Ansible. It simplifies the setup of a multi-node Kubernetes cluster with Calico networking and ensures seamless worker node integration with the master node.

🚀 Features
✅ Automated Kubernetes Installation – Deploys Kubernetes using kubeadm via Ansible.
✅ Worker Node Auto-Join – Automatically adds worker nodes to the cluster.
✅ Calico Network Configuration – Configures Calico CNI for pod networking.
✅ Infrastructure-as-Code – Ensures consistency across deployments.
✅ Scalability – Easily add or remove worker nodes.

⚙️ Prerequisites
Before running the playbooks, ensure you have:

A control machine with Ansible installed
Ubuntu 22.04 servers (1 master, multiple worker nodes)
SSH access from the control machine to all nodes
🖥️ Architecture
Master Node: 192.168.100.200
Worker Nodes:
192.168.100.201 (node01)
192.168.100.202 (node02)
Ansible Playbooks:

Playbook	Description
prerequisites.yml	Installs dependencies, sets up kernel modules
kube-deploy.yml	Installs kubeadm, kubelet, kubectl
calico.yml	Deploys Calico CNI for networking
📌 Setup & Usage
1️⃣ Clone the Repository
bash
Copy
Edit
git clone https://github.com/your-repo/kubernetes-ansible.git
cd kubernetes-ansible
2️⃣ Update the Inventory File
Edit inventory.ini with your server IPs:

[master]
192.168.100.200

[workers]
192.168.100.201
192.168.100.202
3️⃣ Run the Playbooks
Install Prerequisites

ansible-playbook -i inventory.ini prerequisites.yml
Deploy Kubernetes (Master & Workers)

ansible-playbook -i inventory.ini kube-deploy.yml
Configure Calico Networking

ansible-playbook -i inventory.ini calico.yml
4️⃣ Verify Cluster Status

kubectl get nodes
Expected Output:

NAME      STATUS   ROLES           AGE   VERSION
master01  Ready    control-plane   5m    v1.28.0
node01    Ready    <none>          4m    v1.28.0
node02    Ready    <none>          4m    v1.28.0
🔧 Troubleshooting
🔹 If a worker node fails to join, check logs:


journalctl -u kubelet -f
🔹 If kubectl is not working on the master, run:


export KUBECONFIG=/etc/kubernetes/admin.conf
🛠️ Contributing
Contributions are welcome! If you find issues or have improvements, feel free to submit a pull request.

📜 License
This project is licensed under the MIT License.




