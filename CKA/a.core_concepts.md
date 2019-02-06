![](https://gaforgithub.azurewebsites.net/api?repo=CKAD-exercises/core_concepts&empty)
## Core Concepts (13%)

This covers the API primitives and how to create and configure basic Pods
- YAML
- POD
- ReplicaSet
- Deployment
- Namespaces


> First of all, make sure to configure kubectl autocomplete, it will easy your life

```yaml
# BASH

source <(kubectl completion bash) # setup autocomplete in bash into the current shell, bash-completion package should be installed first.
echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanently to your bash shell.

# ZSH

source <(kubectl completion zsh)  # setup autocomplete in zsh into the current shell
echo "if [ $commands[kubectl] ]; then source <(kubectl completion zsh); fi" >> ~/.zshrc # add autocomplete permanently to your zsh shell
```

##### 1. Create a pod with the NGINX image in a namespace called webtier

<details><summary>show</summary>
<p>

```bash
# Create the namespace if not exist
kubectl get ns
kubectl create ns webtier

# Create the pod
kubectl run nginx --image=nginx --restart=Never -n webtier
```

</p>
</details>

==================================================================================================

##### 2. Dry run. Print the corresponding API objects without creating them.

<details><summary>show</summary>
<p>

```bash
kubectl run nginx --image=nginx --dry-run
```

</p>
</details>

==================================================================================================

##### 3. Create the same pod in a namespace called dev using YAML definition file

<details><summary>show</summary>
<p>

```bash
# Create the namespace if not exist
kubectl get ns
kubectl create ns dev
```

```
# An easy way to generate YAML is to use imperactive command with dry-run option
kubectl run nginx --image=nginx --restart=Never -n dev --dry-run -o yaml > nginx-pod.yaml
```
```basj
cat nginx-pod.yaml
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    imagePullPolicy: IfNotPresent
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```
```
# Edit the file by adding namespace dev
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
namespace: dev
spec:
  containers:
  - image: nginx
    imagePullPolicy: IfNotPresent
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```
```bash
# Another way to add namespace dev to the command
kubeclt create -f nginx-pod.yaml -n dev
```

</p>
</details>


==================================================================================================

##### 4. Get pods on all namespaces

<details><summary>show</summary>
<p>

```bash
kubectl get po --all-namespaces
```

</p>
</details>

==================================================================================================

##### 5. Start a single instance of hazelcast and let the container expose port 5701 .

<details><summary>show</summary>
<p>

```bash
kubectl run hazelcast --image=hazelcast --port=5701
```
</p>
</details>

==================================================================================================

##### 6. Create a busybox pod using kubectl command that runs the command "env". Run it and see the output

<details><summary>show</summary>
<p>

```bash
kubectl run busybox --image=busybox --command --restart=Never -it -- env # -it will help in seeing the output
```

```bash
# Another way is to run it without -it
kubectl run busybox --image=busybox --command --restart=Never -- env
# and then, check its logs
kubectl logs busybox
```

</p>
</details>

==================================================================================================

##### 7. Start a single instance of hazelcast and set environment variables "DNS_DOMAIN=cluster" and "POD_NAMESPACE=default" in the container.

<details><summary>show</summary>
<p>

```bash
kubectl run hazelcast --image=hazelcast --env="DNS_DOMAIN=cluster" --env="POD_NAMESPACE=default"
```
```
# Verify it via
kubectl logs hazelcast
```
</p>
</details>

==================================================================================================

##### 8. Using kubectl command, create a pod using busybox image, set env value var1=val1. Verify the existance of the env inside the pod

<details><summary>show</summary>
<p>

```bash
# This is an easy way
kubectl run busybox --image=busybox --restart=Never --env=var1=val1 -it -- env
```

```bash
# Another way is to run it without -it
kubectl run busybox --image=busybox --restart=Never --env=var1=val1
# and then
kubectl exec -it busybox -- env
# or
kubectl describe po busybox | grep val1
```
</p>

</details>

==================================================================================================

##### 9. Using kubectl command, create a pod using nginx image, set env value var2=val2, print it and make sure the pod is automatically deleted after it's completed.

<details><summary>show</summary>
<p>

```bash
kubectl run nginx --image=nginx --restart=Never --env=var2=val2 -it  --rm -- env

```
</p>

</details>

![](https://gaforgithub.azurewebsites.net/api?repo=CKAD-exercises/core_concepts&empty)
## Core Concepts (13%)

This covers the API primitives and how to create and configure basic Pods
- YAML
- POD
- ReplicaSet
- Deployment
- Namespaces


> First of all, make sure to configure kubectl autocomplete, it will easy your life

```yaml
# BASH

source <(kubectl completion bash) # setup autocomplete in bash into the current shell, bash-completion package should be installed first.
echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanently to your bash shell.

# ZSH

source <(kubectl completion zsh)  # setup autocomplete in zsh into the current shell
echo "if [ $commands[kubectl] ]; then source <(kubectl completion zsh); fi" >> ~/.zshrc # add autocomplete permanently to your zsh shell
```

##### 1. Create a pod with the NGINX image in a namespace called webtier

<details><summary>show</summary>
<p>

```bash
# Create the namespace if not exist
kubectl get ns
kubectl create ns webtier

# Create the pod
kubectl run nginx --image=nginx --restart=Never -n webtier
```

</p>
</details>

==================================================================================================

#### 2. Dry run. Print the corresponding API objects without creating them.

<details><summary>show</summary>
<p>

```bash
kubectl run nginx --image=nginx --dry-run
```

</p>
</details>

==================================================================================================

##### 2. Create the same pod in a namespace called dev using YAML definition file

<details><summary>show</summary>
<p>

```bash
# Create the namespace if not exist
kubectl get ns
kubectl create ns dev
```

```
# An easy way to generate YAML is to use imperactive command with dry-run option
kubectl run nginx --image=nginx --restart=Never -n dev --dry-run -o yaml > nginx-pod.yaml
```
```basj
cat nginx-pod.yaml
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    imagePullPolicy: IfNotPresent
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```
```
# Edit the file by adding namespace dev
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
namespace: dev
spec:
  containers:
  - image: nginx
    imagePullPolicy: IfNotPresent
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```
```bash
# Another way to add namespace dev to the command
kubeclt create -f nginx-pod.yaml -n dev
```

</p>
</details>


==================================================================================================

##### 3. Get pods on all namespaces

<details><summary>show</summary>
<p>

```bash
kubectl get po --all-namespaces
```

</p>
</details>

==================================================================================================

#### 4. Start a single instance of hazelcast and let the container expose port 5701 .

<details><summary>show</summary>
<p>
```bash
kubectl run hazelcast --image=hazelcast --port=5701
```
</p>
</details>

==================================================================================================

#### 5. Create a busybox pod using kubectl command that runs the command "env". Run it and see the output

<details><summary>show</summary>
<p>

```bash
kubectl run busybox --image=busybox --command --restart=Never -it -- env # -it will help in seeing the output

# Another way is to run it without -it
kubectl run busybox --image=busybox --command --restart=Never -- env
# and then, check its logs
kubectl logs busybox
```

</p>
</details>

==================================================================================================

#### 6. Start a single instance of hazelcast and set environment variables "DNS_DOMAIN=cluster" and "POD_NAMESPACE=default" in the container.

<details><summary>show</summary>
<p>
```bash
kubectl run hazelcast --image=hazelcast --env="DNS_DOMAIN=cluster" --env="POD_NAMESPACE=default"
```
```
# Verify it via
kubectl logs hazelcast
```
</p>
</details>

==================================================================================================

#### 7. Using kubectl command, create a pod using busybox image, set env value var1=val1. Verify the existance of the env inside the pod

<details><summary>show</summary>
<p>

```bash
# This is an easy way
kubectl run busybox --image=busybox --restart=Never --env=var1=val1 -it -- env


# Another way is to run it without -it
kubectl run busybox --image=busybox --restart=Never --env=var1=val1
# and then
kubectl exec -it busybox -- env
# or
kubectl describe po busybox | grep val1
```
</p>

</details>

==================================================================================================

#### 8. Using kubectl command, create a pod using nginx image, set env value var2=val2, print it and make sure the pod is automatically deleted after it's completed.

<details><summary>show</summary>
<p>

```bash
kubectl run nginx --image=nginx --restart=Never --env=var2=val2 -it  --rm -- env

```
</p>

</details>

#### 9. perform the pervious task using YAML file definition

==================================================================================================

#### Start a single instance of nginx, but overload the spec of the deployment with a partial set of values parsed from JSON.

<details><summary>show</summary>
<p>

```bash
kubectl run nginx --image=nginx --overrides='{ "apiVersion": "v1", "spec": { ... } }'

```
</p>

</details>

==================================================================================================
#### 10. Create a busybox pod that echoes 'hello world' and then exits

<details><summary>show</summary>
<p>

```bash
kubectl run busybox --image=busybox -it --restart=Never -- echo 'hello world'
# Another way
kubectl run busybox --image=busybox -it --restart=Never -- /bin/sh -c 'echo hello world'
```

</p>
</details>

==================================================================================================

##### 11. Using kubectl command to get YAML definition file for creating a namespace call production

<details><summary>show</summary>
<p>

```bash
kubectl create ns production --dry-run -o yaml

```
</p>

</details>

==================================================================================================

##### 12. Using kubectl command, create a pod using kubectl command that uses perl to calculate pi to 2000 digits, then stops and print the output

<details><summary>show</summary>
<p>

```bash
kubectl run pi --image=perl --restart=OnFailure --dry-run -- perl -Mbignum=bpi -wle 'print bpi(2000)' 

```
```bash
kubectl logs pi
```
</p>

</details>


==================================================================================================

##### 12. Start the cron job to compute π to 2000 places and print it out every 5 minutes.

<details><summary>show</summary>
<p>

```bash
kubectl run pi --schedule="0/5 * * * ?" --image=perl --restart=OnFailure -- perl -Mbignum=bpi -wle 'print bpi(2000)' 

```
```bash
kubectl logs pi
```
</p>

</details>


==================================================================================================

##### 13. Get the YAML for a new ResourceQuota called 'myrq' without creating it

<details><summary>show</summary>
<p>

```bash
kubectl create resourcequota myrq -o yaml --dry-run
```

</p>
</details>
  
==================================================================================================

##### 14. Change pod's image to nginx:1.7.1. Observe that the pod will be killed and recreated as soon as the image gets pulled

<details><summary>show</summary>
<p>

```bash
# kubectl set image POD/POD_NAME CONTAINER_NAME=IMAGE_NAME:TAG
kubectl set image pod/nginx nginx=nginx:1.7.1
kubectl describe po nginx # you will see an event 'Container will be killed and recreated'
kubectl get po nginx -w # watch it
```

</p>
</details>

==================================================================================================

##### 15. Get the pod's ip, use a temp busybox image to wget its '/'

<details><summary>show</summary>
<p>

```bash
kubectl get po -o wide # get the IP, will be something like '10.1.1.131'
# create a temp busybox pod
kubectl run busybox --image=busybox --rm -it --restart=Never -- sh
# run wget on specified IP:Port
wget -O- 10.1.1.131:80
exit
```

</p>
</details>

==================================================================================================

##### 16. Get this pod's YAML without cluster specific information

<details><summary>show</summary>
<p>

```bash
kubectl get po nginx -o yaml --export
```

</p>
</details>

==================================================================================================

##### 17. Get information about the pod, including details about potential issues (e.g. pod hasn't started)

<details><summary>show</summary>
<p>

```bash
kubectl describe po nginx
```

</p>
</details>

==================================================================================================

##### 18. Get pod logs

<details><summary>show</summary>
<p>

```bash
kubectl logs nginx
```

</p>
</details>

==================================================================================================

##### If pod crashed and restarted, get logs about the previous instance

<details><summary>show</summary>
<p>

```bash
kubectl logs nginx -p
```

</p>
</details>

==================================================================================================

##### 19. Connect to the nginx pod

<details><summary>show</summary>
<p>

```bash
kubectl exec -it nginx -- /bin/sh
```

</p>
</details>

==================================================================================================


# Start a single instance of hazelcast and set labels "app=hazelcast" and "env=prod" in the container.

<details><summary>show</summary>
<p>

```bash
kubectl run hazelcast --image=hazelcast --labels="app=hazelcast,env=prod"
```

</p>
</details>

==================================================================================================

# Start a replicated instance of nginx.

<details><summary>show</summary>
<p>

```bash
kubectl run nginx --image=nginx --replicas=5
```

</p>
</details>

##### 10. perform the pervious task using YAML file definition

==================================================================================================

##### 11. Start a single instance of nginx, but overload the spec of the deployment with a partial set of values parsed from JSON.

<details><summary>show</summary>
<p>

```bash
kubectl run nginx --image=nginx --overrides='{ "apiVersion": "v1", "spec": { ... } }'

```
</p>

</details>

==================================================================================================
##### 12. Create a busybox pod that echoes 'hello world' and then exits

<details><summary>show</summary>
<p>

```bash
kubectl run busybox --image=busybox -it --restart=Never -- echo 'hello world'
```

```bash
# Another way
kubectl run busybox --image=busybox -it --restart=Never -- /bin/sh -c 'echo hello world'
```

</p>
</details>

==================================================================================================

##### 13. Using kubectl command to get YAML definition file for creating a namespace call production

<details><summary>show</summary>
<p>

```bash
kubectl create ns production --dry-run -o yaml

```
</p>

</details>

==================================================================================================

##### 15. Using kubectl command, create a pod using kubectl command that uses perl to calculate pi to 2000 digits, then stops and print the output

<details><summary>show</summary>
<p>

```bash
kubectl run pi --image=perl --restart=OnFailure --dry-run -- perl -Mbignum=bpi -wle 'print bpi(2000)' 

```
```bash
kubectl logs pi
```
</p>

</details>


==================================================================================================

##### 16. Start the cron job to compute π to 2000 places and print it out every 5 minutes.

<details><summary>show</summary>
<p>

```bash
kubectl run pi --schedule="0/5 * * * ?" --image=perl --restart=OnFailure -- perl -Mbignum=bpi -wle 'print bpi(2000)' 

```
```bash
kubectl logs pi
```
</p>

</details>


==================================================================================================

##### 17. Get the YAML for a new ResourceQuota called 'myrq' without creating it

<details><summary>show</summary>
<p>

```bash
kubectl create resourcequota myrq -o yaml --dry-run
```

</p>
</details>
  
==================================================================================================

##### 18. Change pod's image to nginx:1.7.1. Observe that the pod will be killed and recreated as soon as the image gets pulled

<details><summary>show</summary>
<p>

```bash
# kubectl set image POD/POD_NAME CONTAINER_NAME=IMAGE_NAME:TAG
kubectl set image pod/nginx nginx=nginx:1.7.1
kubectl describe po nginx # you will see an event 'Container will be killed and recreated'
kubectl get po nginx -w # watch it
```

</p>
</details>

==================================================================================================

##### 19. Get the pod's ip, use a temp busybox image to wget its '/'

<details><summary>show</summary>
<p>

```bash
kubectl get po -o wide # get the IP, will be something like '10.1.1.131'
# create a temp busybox pod
kubectl run busybox --image=busybox --rm -it --restart=Never -- sh
# run wget on specified IP:Port
wget -O- 10.1.1.131:80
exit
```

</p>
</details>

==================================================================================================

##### 20. Get this pod's YAML without cluster specific information

<details><summary>show</summary>
<p>

```bash
kubectl get po nginx -o yaml --export
```

</p>
</details>

==================================================================================================

##### 21. Get information about the pod, including details about potential issues (e.g. pod hasn't started)

<details><summary>show</summary>
<p>

```bash
kubectl describe po nginx
```

</p>
</details>

==================================================================================================

##### 22. Get pod logs

<details><summary>show</summary>
<p>

```bash
kubectl logs nginx
```

</p>
</details>

==================================================================================================

##### 23. If pod crashed and restarted, get logs about the previous instance

<details><summary>show</summary>
<p>

```bash
kubectl logs nginx -p
```

</p>
</details>

==================================================================================================

##### 24. Connect to the nginx pod

<details><summary>show</summary>
<p>

```bash
kubectl exec -it nginx -- /bin/sh
```

</p>
</details>

==================================================================================================


##### 25. Start a single instance of hazelcast and set labels "app=hazelcast" and "env=prod" in the container.

<details><summary>show</summary>
<p>

```bash
kubectl run hazelcast --image=hazelcast --labels="app=hazelcast,env=prod"
```

</p>
</details>

==================================================================================================

##### 26. Start a replicated instance of nginx.

<details><summary>show</summary>
<p>

```bash
kubectl run nginx --image=nginx --replicas=5
```

</p>
</details>
