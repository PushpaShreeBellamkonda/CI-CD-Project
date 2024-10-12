## Steps for Continuous Deployment

**step:1 create a new Argo CD cluster with the default configuration**

```
apiVersion: argoproj.io/v1alpha1
kind: ArgoCD
metadata:
  name: example-argocd
  labels:
    example: basic
spec: {}

```

**Create a yaml file called "argocd-basic.yaml" which is used to create argocd cluster**

```
vim argocd-basic.yml

```

**Configure this yaml file i.e we are giving previliges to the file**

```
kubectl apply -f argocd-basic.yml

```

**To see all the pods**

```
kubectl get pods

```

**To see all the services**


```
kubectl get svc

```

**We can observe that our "argocd-basic" service  is in "ClusterIP" mode , it means only people who has access with cluster can access this service so to make it accessable to our friends or collegues  we will make it into "NodePort" mode**


**For that**

```

kubectl edit svc example-argocd-server

```


**Now in the editor , change the type from ClusterIP to "NodePort"


![Screenshot (1158)](https://github.com/user-attachments/assets/cb5925d7-ea0b-4d07-b75f-0fc86f2b283e)


**Now we can observe that our service is changed to NodePort mode**


![Screenshot (1159)](https://github.com/user-attachments/assets/4ede793a-8e94-48d7-aa7e-69b6454705e9)

**Run the following command to get secret code in the editor**


```
kubectl edit secret example-argocd-server

```

![Screenshot (1162)](https://github.com/user-attachments/assets/f22109bb-f97a-4d5b-af7d-7e583b43b830)


**Now use the command to get the encrypted code of this secret**

```
echo "your_code" | base64 -d

```

![Screenshot (1163)](https://github.com/user-attachments/assets/c7ac3fd4-1b55-4816-9880-bc082313b1d4)



**step:2 Now run the below command , so that we get default url to access our cluster**


```

minikube service example-argocd-server

```

![Screenshot (1168)](https://github.com/user-attachments/assets/8234ab16-2ede-4b14-b26b-6b7c8b02918e)


**step:3 Now edit one of the url and provide the password that we got and give username as your choise**

![Screenshot (1165)](https://github.com/user-attachments/assets/8f0b1055-eff2-411d-95ab-da36c94c503d)


**After logging in this is the interface we see**

![Screenshot (1169)](https://github.com/user-attachments/assets/aed8bec5-b9d3-4321-a80a-728f7a444b80)


**step:4 Now click on "new app" and click on "create" and give application name , project name , destination url , namespace , repository url and dockerfile path and click on create**


![Screenshot (1170)](https://github.com/user-attachments/assets/58c86a70-2648-48e7-8de7-17324e8db914)



![Screenshot (1173)](https://github.com/user-attachments/assets/b8dad62e-9528-41b9-974d-9dcd7f338f98)



![Screenshot (1175)](https://github.com/user-attachments/assets/c6c5830f-220a-499d-a997-05e9e1de0273)



**This is the application we have created**


![Screenshot (1176)](https://github.com/user-attachments/assets/b07e4e61-eadd-46ad-a00b-1b2b317502f5)


**step:5 Now click on "sync apps" and check the application  "test" and sync it**


![Screenshot (1179)](https://github.com/user-attachments/assets/b605a930-73fe-43a4-8ee8-b509a89baed3)



![Screenshot (1180)](https://github.com/user-attachments/assets/fb60316c-dab8-4b30-8539-a5b24fd2efcf)


**step:6 Now check the pods and deployment , we see that our pods are deployed and running**



```

kubectl get pods

```

```

kubectl get deploy

```


![Screenshot (1182)](https://github.com/user-attachments/assets/6e477163-0812-4115-8c46-bb7fd07780fa)
































 
