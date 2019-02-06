## Core Concepts - 19%

- Understand the Kubernetes API primitives.
- Understand the Kubernetes cluster architecture.
- Understand Services and other network primitives.

> Try to use imperative kubectl command as much as possible. Easier and faster

==================================================================================================




==================================================================================================




#### Create a new pod with the name 'redis' and with the image 'redis:1.3' using YAML pod-definition

kubectl run redis --image=redis:1.3 --restart=Never --dry-run -o yaml > redis.yaml
kubectl create -f redis.yaml


Now fix the image on the pod to 'redis'.
Update the pod-definition file and use 'kubectl apply' command or use 'kubectl edit pod redis' command. 

    If you are given a pod definition file, edit that file and use it to create a new pod.

    If you are not given a pod definition file, you may extract the definition to a file using the below command:

    kubectl get pod <pod-name> -o yaml > pod-definition.yaml

    Then edit the file to make the necessary changes, delete and re-create the pod.

    Use the kubectl edit pod <pod-name> command to edit pod properties.
    
    

Create a ReplicaSet using the 'replicaset-definition-1.yaml' file located at /root/
apiVersion: v1
kind: ReplicaSet
metadata:
 name: replicaset-1
spec:
 replicas: 2
 selector:
  matchlabels:
   tier: frontend:
  template:
   metadata:
    labels:
     tier: frontend
   spec:
    containers:
     - name: nginx
       image: nginx

Create a ReplicaSet using the 'replicaset-definition-2.yaml' file located at /root/
apiVersion: apps/v1
kind: ReplicaSet
metadata:
 name: replicaset-2
spec:
 replicas: 2
 selector:
  matchlabels:
   tier: frontend:
  template:
   metadata:
    labels:
     tier: nginx
   spec:
    containers:
     - name: nginx
       image: nginx
       


Fix the original replica set 'new-replica-set' to use the correct 'busybox' image
Either delete and re-create the ReplicaSet or Update the existing ReplicSet and then delete all PODs, so new ones with the correct image will be created. 

kubectl edit rs new-replica-set
kubectl delete pod --all


Scale the ReplicaSet to 5 PODs
Use 'kubectl scale' command or edit the replicaset using 'kubectl edit replicaset' 

kubectl scale replicaset new-replica-set --replicas=5 




Scale the ReplicaSet to 2 PODs
Use 'kubectl scale' command or edit the replicaset using 'kubectl edit replicaset' 

kubectl scale replicaset new-replica-set --replicas=2



Create a new Deployment with the below attributes using your own deployment definition file
Name: httpd-frontend; Replicas: 3; Image: httpd:2.4-alpine 

Create the service again, but this time pass theLoadBalancertype. Check to see the status and note the external portsmentioned. The output will show theExternal-IPaspending. Unless a provider responds with a load balancer it willcontinue to show as pending.
kubectl expose deployment nginx --type=LoadBalancer

Scale the deployment to zero replicas. Then test the web page again. It should fail.

Scale the deployment up to two replicas. The web page should work again.

Delete the deployment to recover system resources. Note that deleting adeploymentdoes not delete the endpoints orservices.

Here is some sample yaml for a job which uses perl to calculate pi to 2000 digits and then stops.
```bash
apiVersion: batch/v1
kind: Job
metadata:
  name: pi
spec:
  template:
    spec:
      containers:
      - name: pi
        image: perl
        command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
      restartPolicy: Never
  backoffLimit: 4
```

 Rub a job with imperative command which uses perl to calculate pi to 2000 digits and then stops.
 


Write yaml for a new job.  Use the image "busybox" and have it sleep for 10 seconds and then complete.  Run your job to be sure it works.
```bash
apiVersion: batch/v1
kind: Job
metadata:
  name: busybox
spec:
  template:
    spec:
      containers:
      - name: busybox
        image: busybox
        command: ["sleep", "10"]
      restartPolicy: Never
  backoffLimit: 4
```

