# pods
Pods with specific configurations


# ubuntuts.yaml
Ubuntu image good for troubleshooting with a sleep for one month

# ubuntuclean.yaml
Ubuntu image clean with no software added

kubectl apply -f https://raw.githubusercontent.com/zectorpt/pods/master/ubuntuts.yaml

kubectl exec -it ubuntuts -- /bin/bashubuntuts.yaml
