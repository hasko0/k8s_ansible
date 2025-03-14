# **Kubernetes Deployment Automation with Ansible**  

## **📌 Overview**  
This project automates the deployment of a **Kubernetes cluster** on **Ubuntu 22.04** using **Ansible**. It simplifies the setup of a **multi-node Kubernetes cluster** with **Calico networking** and ensures seamless worker node integration with the master node.  

## **🚀 Features**  
✅ **Automated Kubernetes Installation** – Deploys Kubernetes using `kubeadm` via Ansible.  
✅ **Worker Node Auto-Join** – Automatically adds worker nodes to the cluster.  
✅ **Calico Network Configuration** – Configures **Calico CNI** for pod networking.  
✅ **Infrastructure-as-Code** – Ensures consistency across deployments.  
✅ **Scalability** – Easily add or remove worker nodes.  

---

## **⚙️ Prerequisites**  
Before running the playbooks, ensure you have:  
- A control machine with **Ansible installed**  
- **Ubuntu 22.04 servers** (1 master, multiple worker nodes)  
- **SSH access** from the control machine to all nodes  

---

## **🔦 Architecture**  
- **Controller Node:** `192.168.100.215` 
- **Master Node:** `192.168.100.200`  
- **Worker Nodes:**  
  - `192.168.100.201` (node01)  
  - `192.168.100.202` (node02)  

**Ansible Playbooks:**  
| Playbook | Description |  
|----------|------------|  
| `prerequisites.yml` | Installs dependencies, sets up kernel modules |  
| `kube-deploy.yml` | Installs `kubeadm`, `kubelet`, `kubectl`, Deploys **Calico CNI** for networking|  
| `update_hosts.yml` | Add ips and hostname between the VMS |  

---

## **📌 Setup & Usage**  

### **1️⃣ Clone the Repository**  
```bash
git clone https://github.com/your-repo/k8s_ansible.git
cd k8s_ansible
```

### **2️⃣ Update the Inventory File**  
Edit `inventory.ini` with your server IPs:  
```ini
[master]
192.168.100.200

[workers]
192.168.100.201
192.168.100.202
```

### **3️⃣ Run the Playbooks**  

#### **Update Servers hostname **  
```bash
ansible-playbook -i inventory.ini  update_hosts.yml
```

#### **Install Prerequisites**  
```bash
ansible-playbook -i inventory.ini prerequisites.yml
```

#### **Deploy Kubernetes (Master & Workers)**  
```bash
ansible-playbook -i inventory.ini kube-deploy.yml
```


### **4️⃣ Verify Cluster Status**  
```bash
kubectl get nodes
```
Expected Output:  
```bash
NAME      STATUS   ROLES           AGE   VERSION
master01  Ready    control-plane   5m    v1.29.0
node01    Ready    <none>          4m    v1.29.0
node02    Ready    <none>          4m    v1.29.0
```

---

## **🛠️ Troubleshooting**  
🔹 If a worker node fails to join, check logs:  
```bash
journalctl -u kubelet -f
```
🔹 If `kubectl` is not working on the master, run:  
```bash
export KUBECONFIG=/etc/kubernetes/admin.conf
```

---

## **🛠️ Contributing**  
Contributions are welcome! If you find issues or have improvements, feel free to submit a pull request.  

---

## **🐟 License**  
This project is licensed under the **MIT License**.  

