# 🖥️ Vagrant Automation - CentOS Stream 9

---

## 📖 Overview

This project automates Virtual Machine (VM) provisioning using Vagrant with CentOS Stream 9. It simplifies the process of setting up a virtualized development environment with predefined configurations.

---

## 📑 Table of Contents

- [Prerequisites](#prerequisites) 🔑  
- [Architecture](#architecture) 🏗️  
- [Setup & Installation](#setup--installation) 🛠️  
- [Vagrant Setup](#vagrant-setup) 🐾  
- [Cleaning Up Resources](#cleaning-up-resources) 🧹  
- [Conclusion](#conclusion) ✅  

---

## 🔑 Prerequisites

Before you start, ensure you have the following installed:

- [Vagrant](https://www.vagrantup.com/downloads)  
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)  
- Basic understanding of Linux and virtualization  

---

## 🏗️ Architecture

This project uses Vagrant to automate VM provisioning with the following configurations:

- **OS**: CentOS Stream 9  
- **Networking**: Private network with IP `192.168.56.14`  
- **Resources**: 1600MB RAM, 2 CPU cores  
- **SSH Configuration**: Custom SSH key setup  
- **Provisioning (optional)**: Install and configure Apache web server  

---

## 🛠️ Setup & Installation

### 1⃣ Initialize Vagrant:
```bash
vagrant init eurolinux-vagrant/centos-stream-9
```

### 2⃣ Start the Virtual Machine:
```bash
vagrant up
```

### 3⃣ Check VM Status:
```bash
vagrant status
```

### 4⃣ SSH into the VM:
```bash
vagrant ssh
```

### 5⃣ Check Network Configuration:
```bash
ip addr show
``` 

### 6⃣ Exit the VM:
```bash
exit
``` 


## 🐾 Vagrant Setup 🖥️

Below is the `Vagrantfile` configuration used:

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Use the CentOS Stream 9 box
  config.vm.box = "eurolinux-vagrant/centos-stream-9"

  # Private network for host-only access (you can modify the IP)
  config.vm.network "private_network", ip: "192.168.56.14"

  # Synced folder from host to guest
  # config.vm.synced_folder "D:\\scripts\\shellscripts", "/opt/scripts", type: "virtualbox"

  # VirtualBox provider-specific configurations
  config.vm.provider "virtualbox" do |vb|
    # Allocate memory and CPUs
    vb.memory = "1600"
    vb.cpus = 2
    vb.gui = false  # Run the VM in headless mode (without GUI)
  end

  # Disable the default insecure SSH key and use newly generated keys
  config.ssh.insert_key = false

  # Ensure SSH keys are properly configured
  config.ssh.private_key_path = "~/.vagrant.d/insecure_private_key"
  
  # Provision the VM with necessary updates and package installations
  #config.vm.provision "shell", inline: <<-SHELL
    # Update and install necessary packages
    # You can comment below commands to just have a simple Centos standard VM
    sudo dnf -y update
    sudo dnf -y install httpd
    sudo systemctl enable httpd
    sudo systemctl start httpd
  #SHELL
end

```
### 🧹 Cleaning Up Resources

To remove the VM and free up system resources, run the following commands in order:

### 1⃣ Destroy the Virtual Machine:
   ```bash
   vagrant destroy
   ```
### 2⃣ Remove Unused Vagrant Instances:
   ```bash
   vagrant global-status --prune
   ```
---

## ✅ Conclusion

This project demonstrates how to automate VM provisioning using Vagrant and VirtualBox, making it easier to manage development and testing environments efficiently.

---

## 👨‍🏫 Instructor

This project was guided by Imran Teli, who provided valuable mentorship throughout the process.
