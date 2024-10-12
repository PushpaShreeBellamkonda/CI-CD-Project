## Steps for Continuous Integration


**Step:1 Create an ec2 instance of type " t2 large "**



![Screenshot (1092)](https://github.com/user-attachments/assets/7c73fc01-2110-4c2a-8b48-c0a5e69a8b6c)



**Step:2 Edit the inbound rules**



![Screenshot (1093)](https://github.com/user-attachments/assets/4ec392e5-bfc7-429e-9372-06e79445c730)




**Step:3 connect to the ec2 instance and Install java**



```

sudo apt update
sudo apt install openjdk-17-jre

```


**Verify if java is installed**

```

java --version

```


![Screenshot (1094)](https://github.com/user-attachments/assets/65435e2f-9d32-4c24-b4d3-6a137d3f4989)




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


![Screenshot (1095)](https://github.com/user-attachments/assets/04c74b5b-baef-4b6a-88b5-389f3414eb4c)




**Verify if jenkins is installed or not**



```
ps -ef | grep jenkins

```




![Screenshot (1096)](https://github.com/user-attachments/assets/0fe15f20-e0dc-4f9b-8ea3-74c4282c1d73)



**step:5 Browse the public IP of the ec2 instance with port 8080 to access jenkins**


![Screenshot (1098)](https://github.com/user-attachments/assets/2b46c0f9-f995-4802-8fec-daa963c84225)

**step:6 Copy the url and say "sudo cat url" to get the password for jenkins**


![Screenshot (1099)](https://github.com/user-attachments/assets/9555c0d0-0071-4086-95f5-5855d4fab629)


**step:7 Now login to the jenkins and install the plugin**


![Screenshot (1100)](https://github.com/user-attachments/assets/60edd6de-d125-49f3-afdd-90837c730bdc)


**step:8 Now select new item , give a name , and select pipeline and ok**

![Screenshot (1101)](https://github.com/user-attachments/assets/6532d322-00cf-4857-8e95-ca15c76d6e64)


**step:9 Now in the pipeline select "pipeline script from SCM" and give "github repo url" the "branch" and "Script path"**


![Screenshot (1103)](https://github.com/user-attachments/assets/661305fd-069c-4c9b-a434-9baeb23b643e)



![Screenshot (1104)](https://github.com/user-attachments/assets/30148134-0bdd-469c-b291-c506e53cd234)


**step:10 Install required plugins , " Docker Pipeline " and " Sonarqube Scanner "**


![Screenshot (1105)](https://github.com/user-attachments/assets/cc79b972-4f70-41d8-a427-644fe6204bfc)



![Screenshot (1106)](https://github.com/user-attachments/assets/9fd6322c-b5f8-471e-9907-84fffeb29e89)



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


![Screenshot (1107)](https://github.com/user-attachments/assets/ab5bac5a-52ec-4518-8e8e-84440342b197)


![Screenshot (1108)](https://github.com/user-attachments/assets/b7f7fd16-098e-4ae4-abdc-484fde17ccc4)


![Screenshot (1109)](https://github.com/user-attachments/assets/5eb251b0-b8b7-4c18-84e8-c0a3fa36bbc8)



**step:12 Now browse the public IP of instance with port 9000 to access sonarqube and login to it**

![Screenshot (1110)](https://github.com/user-attachments/assets/367bdb60-50b6-41b0-9f8e-bea083fe0b71)


**step:13 Now create a token and by using this token we can make jenkins to interact with sonarqube**

![Screenshot (1111)](https://github.com/user-attachments/assets/71dbdf08-3380-4747-a594-c5d7644d9ec1)


**step:14 Now in jenkins create sonarqube credentials in order to make both jenkins and sonarqube interact with eachother**

![Screenshot (1112)](https://github.com/user-attachments/assets/8db7e2ec-b670-499a-9992-2a014b53681e)


**step:15 Now install Docker inside ec2 instance**

```
sudo apt install docker.io

```

![Screenshot (1113)](https://github.com/user-attachments/assets/aa7b046c-3a4d-4c9c-a034-0e5a2db8061b)


**Now run these commands to give previleges and  restart docker**

![Screenshot (1114)](https://github.com/user-attachments/assets/0d21940e-f512-428a-a517-089958cd7a4e)


**Now restart jenkins**

![Screenshot (1115)](https://github.com/user-attachments/assets/802f0249-8e44-409c-9347-9c440262eb4f)


**Now browse "operatorhub argocd install" to install argocd operator**

![Screenshot (1117)](https://github.com/user-attachments/assets/a5e821c9-ab5a-4e8d-8bd4-01427e1c349d)

**Now run those commands one by one**

![Screenshot (1119)](https://github.com/user-attachments/assets/0117cec1-87b1-463a-9aa5-5bd0a13d71d2)


![Screenshot (1120)](https://github.com/user-attachments/assets/998259ec-0363-43d6-b994-c771a1faac0a)


![Screenshot (1121)](https://github.com/user-attachments/assets/df7c2e51-8cb1-4c48-ae4c-d9b4310586f6)


**Now add the dockerhub credentials in the jenkins so that the docker image will be stored inside the dockerhub of the respective**
**repository that we gave in the pipeline syntax**


![Screenshot (1122)](https://github.com/user-attachments/assets/5c224de2-f4ee-4bd9-b93b-042e82791df1)


**Now provide the github credentials in the jenkins , create a token in the github**

![Screenshot (1123)](https://github.com/user-attachments/assets/c210ebd0-143e-4dc7-8209-8455d3ea52ea)


**Now again restart the jenkins interface**


![Screenshot (1124)](https://github.com/user-attachments/assets/cf3df8c1-aef6-46fb-98be-4e75910918f5)


**step:16 Now build the pipeline**

![Screenshot (1125)](https://github.com/user-attachments/assets/690317fd-aebc-405a-8de5-30f2948ed94b)


**We can observe that our application is deployed in the sonarqube server**


![Screenshot (1126)](https://github.com/user-attachments/assets/23a48ca2-944b-46fb-ae68-c40891b131c8)


**And our docker image is also pushed inside our dockerhub repository**

![Screenshot (1127)](https://github.com/user-attachments/assets/9a4970fd-bd92-4daf-8b8f-86a098379615)


**Run this command to see the docker image in the ec2 instance**

```
docker images

```


![Screenshot (1128)](https://github.com/user-attachments/assets/ff458064-94ea-4c5c-b2a5-022bc244e1d0)

















































