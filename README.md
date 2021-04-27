# hpc-cluster
To run the deployment do:
kubectl apply -f volume(1).yaml
kubectl apply -f nfs-server(2).yaml

Then look up the IP of the nfs-server pod by doing:
kubectl describe pod nfs-server

Insert the IP into the user-pod(3).yaml where it is indicated by a comment at line 12.
Then run it:
kubectl apply -f user-pod(3).yaml

This should get the cluster running. To set up the SSH keys, exec into the nfs-client pod by doing:
kubectl exec -it nfs-client-xxxxx -- /bin/bash

Note that since the nfs-client pod is created by a replication controller, the pod's name will end with a random string.
You can lookup the pod names by doing:
kubectl get pods

Once you are inside of the nfs-client pod, as the root user go to the home directory and create a directory named jovyan.
Inside of the jovyan directory create a .ssh directory. Inside of the .ssh directory do:
ssh-keygen

