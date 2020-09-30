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
