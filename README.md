# Pods configured with specific configuration
Pods with specific configurations, ready to deploy

# configmapunderscore.yaml

With this specific configmap we can change a specific configuration from ingress controler in AKS

The yaml should be changed to be used in the same namespace where the ingress is deployed<br>

kubectl get all -A<br>
kubectl get namespaces<br>
kubectl get pods --namespace app-routing-system<br>
kubectl --namespace app-routing-system exec -it nginx-7cd7f56848-dl42j -- grep underscores_in_headers nginx.conf<br>
kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/refs/heads/master/configmapunderscore.yaml<br>
kubectl delete --namespace app-routing-system pod nginx-7cd7f56848-799x5<br>
kubectl --namespace app-routing-system exec -it nginx-7cd7f56848-dl42j -- grep underscores_in_headers nginx.conf<br>

# ubuntuts.yaml
Ubuntu image good for troubleshooting with a sleep for one month


Deploy the image:
kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/master/ubuntuts.yaml

Enter the POD:
kubectl exec -it ubuntuts -- /bin/bash
<br>
![image](https://github.com/user-attachments/assets/5ffa31cd-6244-4a67-b3b2-e3c173a62464)
<br>

# deploymentwithpvc.yaml
Create a PV and PVC to use with a deployment

Install the drivers:
az aks update --enable-blob-driver -n k8s -g ts

Create PVC:
Create a file with the bellow information and run: 

kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/master/blob-nfs-pvc.yaml

Create file and check in another pod:
kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/master/deploymentwithpvc.yaml
kubectl get pods -A
kubectl exec deploymentwithpvc-7c5d8786fc-5fscl -- touch /mnt/blob/test.txt
kubectl exec deploymentwithpvc-7c5d8786fc-5fscl -- ls /mnt/blob


# ubuntuclean.yaml
Ubuntu image clean with no software added

Deploy the image:
kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/master/ubuntuclean.yaml

Enter the POD:
kubectl exec -it ubuntuts -- /bin/bash

# ubuntucleansysctl.yaml
Ubuntu deployment with a workaround to change the kernel parameter net.core.somaxconn to 1024

Deploy:
kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/master/ubuntucleansysctl.yaml

Check the parameter:

kubectl exec -it ubuntu-clean-sysctl-[d8f4977c4-m5z6w] -- /bin/cat /proc/sys/net/core/somaxconn

# pvcandpodwindows.yaml
After create a Windows node pool deploy this windows pod and it will get assigned the PVC

Deploy:
kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/master/pvcandpodwindows.yaml

kubectl exec -it iis-azurefile -- cmd <br>
kubectl exec -it iis-azurefile -- powershell <br>

# windowspod.yaml
After create a Windows node pool deploy this windows pod
Windows pod with IIS installed

Deploy:
kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/master/windowspod.yaml

kubectl exec -it iis-azurefile -- cmd <br>
kubectl exec -it iis-azurefile -- powershell <br>

# customstorageclass.yaml
Implementation of a storage class with custom file and dir permissions with pods

Deploy:
kubectl apply -f  https://raw.githubusercontent.com/zectorpt/pods/refs/heads/master/customstorageclass.yaml <br>
 <br>
kubectl exec -it test-pod -- bash <br>
cd /mnt/      <br>
ls -l <br>
 <br>
kubectl exec -it test-pod-docli -- bash <br>
cd /mnt/ <br>
ls -l <br>
![image](https://github.com/user-attachments/assets/b19ecba5-68df-41bc-890a-209c3e0bc0e6)

# call_pod_by_name_headless.yaml
Implementation of an headless service to allow to call a pod by name.

Deploy:
kubectl apply -f  https://raw.githubusercontent.com/zectorpt/pods/refs/heads/master/call_pod_by_name_headless.yaml <br>
<br>
Output
<br>
jose [ ~ ]$ kubectl apply -f  https://raw.githubusercontent.com/zectorpt/pods/refs/heads/master/call_pod_by_name_headless.yaml<br>
namespace/testing-headless created<br>
service/nginx-headless created<br>
statefulset.apps/nginx created<br>
jose [ ~ ]$ kubectl get pods --namespace testing-headless<br>
NAME      READY   STATUS    RESTARTS   AGE<br>
nginx-0   1/1     Running   0          41s<br>
nginx-1   1/1     Running   0          40s<br>
nginx-2   1/1     Running   0          38s<br>
jose [ ~ ]$ kubectl get services --namespace testing-headless<br>
NAME             TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE<br>
nginx-headless   ClusterIP   None         <none>        80/TCP    56s<br>
jose [ ~ ]$ kubectl get statefulset.apps --namespace testing-headless<br>
NAME    READY   AGE<br>
nginx   3/3     78s<br>
<br><br>
jose [ ~ ]$ kubectl exec -it nginx-0 --namespace testing-headless -- bash<br>
root@nginx-0:/# curl nginx-1.nginx-headless<br>
<!DOCTYPE html><br>
<html><br>
...........<br>
<br>
