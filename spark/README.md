# Ansible-based Spark Standalone cluster
This is an example of a spark standalone cluster built with Vagrant on virtual machines and managed with Ansible.
The example is explained in more details in the How_To section on my personal website [sharek.dev](https://sharek.dev)

## Quick start guide
### 1- Install dependencies
- VirtualBox
- Vagrant
- Ansible (Mac/Linux only])


### 2- Build the cluster
1. Download this git repo `git clone git@github.com:helkaroui/ansible-vagrant-stacks.git`
2. In the terminal, navigate to the project dir, then to spark directory `cd ansible-vagrant-stacks && cd spark`
3. Run `vagrant up` and watch the magic 🪄

### 3- Run Spark Standalone cluster
1. ssh into the master node `vagrant ssh spark-1`
2. Run spark cluster `start-all.sh`
3. In the browser, open [192.168.1.71:8080](192.168.1.71:8080)
4. Optionnaly, you can start spark-history server by running `start-history-server.sh`. The server will be available at address [http://192.168.1.71:18080](http://192.168.1.71:18080)

### 4- Run a simple example
To test the cluster, you can run one of the examples shipped with spark. To run the PI example run :
`spark-submit --master spark://192.168.1.71:7077  --class org.apache.spark.examples.SparkPi  /opt/spark/examples/jars/spark-examples_2.12-3.1.2.jar`


## Notes
- To shut down the cluster enter `vagrant halt` in the Terminal in the same folder that has the **Vagrantfile**. 
- To destroy it completely type in `vagrant destroy -f`.

## About the Author
This project was created by [Hamza KAROUI](https://sharek.dev) as part of my [Home cloud](https://sharek.dev/home_cloud/overview/) project.