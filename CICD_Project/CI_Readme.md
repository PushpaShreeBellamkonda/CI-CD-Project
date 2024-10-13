## Steps for Continuous Integration


**Step:1 Create an ec2 instance of type " t2 large "**





**Step:2 Edit the inbound rules**








**Step:3 connect to the ec2 instance and Install java**



```

sudo apt update
sudo apt install openjdk-17-jre

```


**Verify if java is installed**

```

java --version

```







**Step:4 Install jenkins**


```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

```







**Verify if jenkins is installed or not**



```
ps -ef | grep jenkins

```








**step:5 Browse the public IP of the ec2 instance with port 8080 to access jenkins**



**step:6 Copy the url and say "sudo cat url" to get the password for jenkins**





**step:7 Now login to the jenkins and install the plugin**





**step:8 Now select new item , give a name , and select pipeline and ok**




**step:9 Now in the pipeline select "pipeline script from SCM" and give "github repo url" the "branch" and "Script path"**







**step:10 Install required plugins , " Docker Pipeline " and " Sonarqube Scanner "**









**step:11 Install sonarqube in the ec2 instance**


**Install unzip**

```
apt install unzip
```

**Add a user called sonarqube**

```

sudo adduser sonarqube

```

**Login to the user**

```

sudo su - sonarqube

```

**Now run this command one by one**

```
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip

```

```
unzip *

```

```
chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424

```

```
chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424

```

```

cd sonarqube-9.4.0.54424/bin/linux-x86-64/

```


```
./sonar.sh start

```





**step:12 Now browse the public IP of instance with port 9000 to access sonarqube and login to it**


**step:13 Now create a token and by using this token we can make jenkins to interact with sonarqube**




**step:14 Now in jenkins create sonarqube credentials in order to make both jenkins and sonarqube interact with eachother**




**step:15 Now install Docker inside ec2 instance**

```
sudo apt install docker.io

```



**Now run these commands to give previleges and  restart docker**




**Now restart jenkins**




**Now browse "operatorhub argocd install" to install argocd operator**



**Now run those commands one by one**


**Now add the dockerhub credentials in the jenkins so that the docker image will be stored inside the dockerhub of the respective**
**repository that we gave in the pipeline syntax**



**Now provide the github credentials in the jenkins , create a token in the github**




**Now again restart the jenkins interface**





**step:16 Now build the pipeline**



**We can observe that our application is deployed in the sonarqube server**





**And our docker image is also pushed inside our dockerhub repository**




**Run this command to see the docker image in the ec2 instance**

```
docker images

```




















































