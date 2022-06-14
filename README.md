# Pods configured with specific configuration
Pods with specific configurations, ready to deploy


# ubuntuts.yaml
Ubuntu image good for troubleshooting with a sleep for one month


Deploy the image:
kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/master/ubuntuts.yaml

Enter the POD:
kubectl exec -it ubuntuts -- /bin/bash

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
