# K8s multinode setup

Setting up a Kubernetes environment with ***Vagrant*** using Ansible to configure the multiple nodes. The Vagrantfile mount multiple nodes predefined (*K-master-nodes* and *N-workers-nodes*) in a virtual machine (***VirtualBox***) with a "*bento/ubuntu-16.04*" OS. As container platform, ***Docker*** is the chosen.

**Tip**: The relation between the number of master nodes and worker nodes follow the [Raft Consensus Algorithm](https://raft.github.io/).

## Before you begin
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Packages needed
To execute the program in order to setup a functional Kubernetes environment must have installed the following packages:

- **MacOs**

	- [HomeBrew](https://brew.sh/): Package management system.
```$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"```

	- [VirtualBox](https://www.virtualbox.org/): As a virtualization tool used by Vagrant.
```$ brew cask install virtualbox```

	- [Vagrant](https://sourabhbajaj.com/mac-setup/Vagrant/README.html): Tool used for building and managing virtual machine environments in a single workflow.
```$ brew cask install vagrant```

### Hardware prerequisites

**Machines running one of**:
-   **Ubuntu 16.04+**
-   Debian 9
-   CentOS 7
-   RHEL 7
-   Fedora 25/26 (best-effort)
-   HypriotOS v1.0.1+
-   Container Linux (tested with 1800.6.0)

**Minimal required memory & CPU (cores)**
-   Master node minimal required memory is 2GB and the worker nodes need minimum is 1GB.
-   The master node needs at least 1.5 cores and the worker nodes need at least 0.7 cores.
-  Full network connectivity between all machines in the cluster (public or private network is fine)
-   Unique hostname, MAC address, and *product_uuid* for every node. See [here](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#verify-the-mac-address-and-product-uuid-are-unique-for-every-node)  for more details.
-   Certain ports are open on your machines. See [here](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#check-required-ports)  for more details.
-   Swap disabled. You  **MUST**  disable swap in order for the *kubelet* to work properly.

## How to run

Once the Vagrantfiles variables are set such as the ***OS_IMAGE_NAME*** for the  virtualization and the number of worker nodes (***N***), you just need to run the following command: 
```
$ vagrant up
```

This run a process which automatically download the OS image, setup the nodes and sync up with each other. For this networking synchronization between nodes is used [Calico](https://www.projectcalico.org/) project.

### Other useful commands

- `$ vagrat up --provision`: Setup the VM nodes forcing the provision.
- `$ vagrant ssh`: To SSH into any VM node.
- `$ vagrant halt`: Stop all the VM nodes.
- `$ vagrant destroy`: Destroy images completely.
