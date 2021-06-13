# install spark : 
## setup users :
?? is it needed ?

## Install java JRE
sudo apt install default-jre -y

echo 'JAVA_HOME=/usr/lib/jvm/default-java' | sudo tee -a /etc/environment > /dev/null
source /etc/environment
echo $JAVA_HOME
java -version

## install spark
/// PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/opt/spark/bin:/opt/spark/sbin"


wget https://miroir.univ-lorraine.fr/apache/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2.tgz
sudo tar -xvf spark-3.1.2-bin-hadoop3.2.tgz -C /opt/
rm spark-3.1.2-bin-hadoop3.2.tgz
sudo ln -s /opt/spark-3.1.2-bin-hadoop3.2 /opt/spark


sudo chown -R vagrant:vagrant /opt/spark /opt/spark-3.1.2-bin-hadoop3.2


echo 'SPARK_HOME=/opt/spark' | sudo tee -a /etc/environment > /dev/null
echo 'PATH="$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin"' | sudo tee -a /etc/environment > /dev/null
echo 'PYSPARK_PYTHON=/usr/bin/python3' | sudo tee -a /etc/environment > /dev/null

source /etc/environment

mkdir /opt/spark/eventLogs


## Configure slaves
echo "10.11.13.11\n10.11.13.12" > /opt/spark/conf/workers

## Configure spark
### Spark env
cp /opt/spark/conf/spark-env.sh.template /opt/spark/conf/spark-env.sh 

```
SPARK_MASTER_HOST="10.11.13.10"
SPARK_MASTER_WEBUI_PORT=8080
SPARK_LOCAL_IP=
```


### Spark defaults
cp /opt/spark/conf/spark-defaults.conf.template /opt/spark/conf/spark-defaults.conf

```
spark.eventLog.enabled=true
spark.eventLog.dir=/opt/spark/eventLogs
spark.serializer=org.apache.spark.serializer.KryoSerializer
spark.driver.memory=1g
spark.driver.extraJavaOptions=-XX:+UseG1GC
spark.executor.extraJavaOptions=-XX:+UseG1GC
```




## Set passwordless ssh access :
### Master side
ssh-keygen -t rsa -f ${HOME}/.ssh/id_rsa -q -N '' -C vagrant@master
chmod 0600 ${HOME}/.ssh/id_rsa


cat ${HOME}/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys


ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC73fu1P1RH2U4Sgsp2HVyF3Pb8QqfS7Wg8r6cT0f+BpL1elg52eBoblOPvxYnjp1tO1MGhqZCDRyvr1PqCY59hfCswP5L2EALSyR65fImm/XBi96IFP8D3T66zRW0EOD2bLuKbGRIBZ5afnUbBAS9w6WjtB2mmvvCzPG/e0pEf3TnO9X3hFph/nbRIMOY4rCmJcacCnY338TGJJagd2TdyY50Vgk3FDyKlGoaAA/GtHHG9Zr9JaHDPlTjcZCTPHHyrsBY+R9xQPhqKf25tOD9z/JEQw10mASSdktT8vE0j40oGXIq00QrnNnLP+ODrkUWqUJjryFkTC1Ey0xCerHqp vagrant@master

### Worker side
ssh-keygen -t rsa -f ${HOME}/.ssh/id_rsa -q -N '' -C vagrant@worker
chmod 0600 ${HOME}/.ssh/id_rsa


# Test : run pi example
start worker cmd: start-worker.sh spark://10.11.13.10:7077

spark-submit --master spark://localhost:7077  --class org.apache.spark.examples.SparkPi  /opt/spark/examples/jars/spark-examples_2.12-3.1.2.jar






# Spark HS
Run : start-history-server.sh


# Healthcheck spark 
ps -ef | grep spark
or
curl http://<master-ip>:8080

# Healthcheck spark hs
curl http://<master-ip>:18080