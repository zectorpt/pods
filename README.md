# Pods configured with specific configuration
Pods with specific configurations, ready to deploy


# ubuntuts.yaml
Ubuntu image good for troubleshooting with a sleep for one month


Deploy the image:
kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/master/ubuntuts.yaml

Enter the POD:
kubectl exec -it ubuntuts -- /bin/bash

# deploymentwithpvc.yaml
Create a PV and PVC to use with a deployment

Install the drivers:
az aks update --enable-blob-driver -n k8s -g ts

Create PVC:
Create a file with the bellow information and run: kubectl apply -f blob-nfs-pv.yaml

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: azure-blob-storage
  annotations:
        volume.beta.kubernetes.io/storage-class: azureblob-nfs-premium
spec:
  accessModes:
  - ReadWriteMany
  storageClassName: my-blobstorage
  resources:
    requests:
      storage: 5Gi

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
