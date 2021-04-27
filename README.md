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

Once you are inside of the nfs-client pod, as the root user go to the home directory and do:

mkdir jovyan

chown -R jovyan:jovyan jovyan

Then inside of the /home/jovyan/.ssh directory do:

ssh-keygen

This should generate id_rsa and id_rsa.pub which are the private and public SSH keys. 
Next you should copy id_rsa.pub to the authorized_keys file. You can do this by:

cat id_rsa.pub > authorized_keys

When you SSH between the mpi-worker-x pods and the nfs-client pod they should be added to the known_hosts file.

Go to https://github.com/hnw2y/HPC to see Dockerfile and get files for building the Singularity containers.

Go to https://github.com/jcwijaya/nfs-server to see the Dockerfile for the nfs-server pod.



