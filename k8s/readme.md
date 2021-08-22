# Ansible-based Kubernetes cluster example
This is an example of a kubernetes cluster build on virtual machines using Vagrant and provisioned by Ansible.
It's used for modeling a multi-server production topology, such as :
- separating a web and database server of a k8s cluster
- testing k8s API and components
- disaster-case testing: machines dying, network partitions, slow networks, inconsistent world views, etc.

## Quick start guide
### Install dependencies
- VirtualBox
- Vagrant
- Ansible (Mac/Linux only])

## How to run the playbook
### 1- Locally
To install k8s on the localhost machine, just run the following command. It will ask for the user password.
```
ansible-playbook main.yml -i inventory/localhost --ask-become-pass
```

### 2- VM cluster
1. In the terminal, navigate to the project dir, then to spark directory `cd ansible-vagrant-stacks && cd k8s`
2. Install Ansible requirements `ansible-galaxy install -r requirements.yml -f`
3. Run `vagrant up` and watch the magic 🪄

## Notes
- To shut down the cluster enter `vagrant halt` in the Terminal in the same folder that has the **Vagrantfile**. 
- To destroy it completely type in `vagrant destroy -f`.

## About the Author
This project was created by [Hamza KAROUI](https://sharek.dev) as part of my [Home cloud](https://sharek.dev/home_cloud/overview/) project.