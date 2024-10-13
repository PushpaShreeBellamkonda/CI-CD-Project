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





**Now we can observe that our service is changed to NodePort mode**




**Run the following command to get secret code in the editor**


```
kubectl edit secret example-argocd-server

```




**Now use the command to get the encrypted code of this secret**

```
echo "your_code" | base64 -d

```





**step:2 Now run the below command , so that we get default url to access our cluster**


```

minikube service example-argocd-server

```




**step:3 Now edit one of the url and provide the password that we got and give username as your choise**




**After logging in this is the interface we see**




**step:4 Now click on "new app" and click on "create" and give application name , project name , destination url , namespace , repository url and dockerfile path and click on create**












**This is the application we have created**





**step:5 Now click on "sync apps" and check the application  "test" and sync it**







**step:6 Now check the pods and deployment , we see that our pods are deployed and running**



```

kubectl get pods

```

```

kubectl get deploy

```


































 
