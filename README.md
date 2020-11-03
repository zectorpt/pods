# Pods configured with specific configuration
Pods with specific configurations, ready to deploy


# ubuntuts.yaml
Ubuntu image good for troubleshooting with a sleep for one month

# ubuntuclean.yaml
Ubuntu image clean with no software added

Deploy the image:
kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/master/ubuntuts.yaml

Enter the POD:
kubectl exec -it ubuntuts -- /bin/bashubuntuts.yaml

# ubuntucleansysctl.yaml
Ubuntu deployment with a workaround to change the kernel parameter net.core.somaxconn to 1024

Deploy:
kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/master/ubuntucleansysctl.yaml

Check the parameter:

kubectl exec -it ubuntu-clean-sysctl-[d8f4977c4-m5z6w] cat /proc/sys/net/core/somaxconn
