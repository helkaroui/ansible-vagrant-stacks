# Ansible-based Kubernetes cluster example
This is an example of a kubernetes cluster build on virtual machines using Vagrant and provisioned by Ansible.
It's used for modeling a multi-server production topology, such as :
- separating a web and database server of a k8s cluster
- testing k8s API and components
- disaster-case testing: machines dying, network partitions, slow networks, inconsistent world views, etc.

## Quick start guide
### 1- Install dependencies
- VirtualBox
- Vagrant
- Ansible (Mac/Linux only])

### 2- Build the cluster
1. Download this git repo `git clone git@github.com:helkaroui/ansible-vagrant-stacks.git`
2. In the terminal, navigate to the project dir, then to spark directory `cd ansible-vagrant-stacks && cd k8s`
3. Install Ansible requirements `ansible-galaxy install -r requirements.yml -f`
4. Run `vagrant up` and watch the magic 🪄


## Notes
- To shut down the cluster enter `vagrant halt` in the Terminal in the same folder that has the **Vagrantfile**. 
- To destroy it completely type in `vagrant destroy -f`.

## About the Author
This project was created by [Hamza KAROUI](https://sharek.dev) as part of my [Home cloud](https://sharek.dev/home_cloud/overview/) project.