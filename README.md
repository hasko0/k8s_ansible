# k8s_ansible
This project automates the deployment and configuration of a Kubernetes cluster on Ubuntu 22.04 using Ansible. It simplifies the setup of a multi-node cluster with Calico networking and ensures seamless worker node integration with the master node

Features
✅ Automated Kubernetes Installation – Deploys Kubernetes using kubeadm with Ansible.
✅ Worker Node Auto-Join – Automatically adds worker nodes to the cluster.
✅ Calico Network Configuration – Set up Calico CNI for pod networking.
✅ Infrastructure-as-Code – Ensures consistency across deployments.

Requirements
Ansible installed on the control node
Ubuntu 22.04 servers 1 master 3 server work node
SSH access to worker nodes


How to use:
Clone the repository
Update the inventory file (inventory.ini) with your server IPs
Run the playbooks:

ansible-playbook -i inventory.ini prerequisites.yml
ansible-playbook -i inventory.ini kube-deploy.yml

Verify cluster status:

kubectl get nodes



