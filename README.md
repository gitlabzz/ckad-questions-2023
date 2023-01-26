# ckad-questions-2023

just some questions from my practice
---

# Practice Question 26th Jan 2023

## Question:1

### Create a new deployment for running.nginx with the following parameters:

* Name the deployment nginx and configure with 4 replicas
* Configure the pod with a container image of nginx:latest
* Set an environment variable NGINX-PORT=8080 and also expose that port for the container

#### Answer:

*

---

## Question:2

### Create a secret and consume the secret in a pod using environment variables as follow:

* Create a secret named another-secret with a key/value pair - key1/value4
* Start nginx pod named nginx-secret using container image nginx,
* add an environment variable with name "COOL_VARIABLE" exposing the value of the secret key "key1"

#### Answer:

* kubectl create secret generic another-secret --from-literal=key1=value4
* kubectl run nginx --image=nginx --restart=Never --port=80 --dry-run=client -o yaml >> two.yaml
* kubectl exec -it nginx -- env | grep COOL_VARIABLE

---

## Question:3

Create a pod that requests a certain amount of CPU and memory,
so it gets scheduled to-a node that has those resources available:

* Create a pod named nginx-resources that requests a minimum of 200m CPU and 1Gi memory for its container
* The pod should use the nginx image

#### Answer:

* kubectl run nginx --image=nginx --restart=Never --port=80 --dry-run=client -o yaml >> three.yaml

---

## Question:4

Crate a deployment and expose it via a service of type ClusterIP:

Edit it to:

* Add the type=frontEnd key/value label to the pod template metadata to identify the pod for the service definition
* Have 4 replicas
* Exposes the service on TCP port 8080

#### Answer:

* kubectl create deployment nginx --image=nginx --port=80 --dry-run=client --replicas=3 -o yaml > four.yaml

---

## Question: 5

Create a ConfigMap and consume the ConfigMap in a pod using a volume mount.
Task Please complete the following:

* Create a ConfigMap named another-config containing the key/value pair: key4/value3
* start a pod named nginx-configmap containing a single container using the nginx image,
* and mount the key you just created into the pod under directory /also/a/path

#### Answer:

* kubectl create configmap another-config --from-literal=key4=value3

---

## Question: 6

Create a secret and consume the secret in a pod using environment variables as follows:

* Create a secret named another-secret with a key/value pair; key1/value4
* Start nginx pod named nginx-secret using container image nginx,
* and add an environment variable COOL_VARIABLE"" exposing the value of the secret key; key 1 inside the container

#### Answer:

* kubectl create secret generic another-secret --from-literal=key1=value4 --dry-run=client -o yaml >> six_a.yaml
* kubectl run nginx --image=nginx --restart=Never --port=80 --dry-run=client -o yaml > six_b.yaml
* kubectl exec -it nginx -- env | grep COOL_VARIABLE

---

## Question: 7

A project that you are working on has a requirement for persistent data to be available, perform the following tasks:

* Create a file on node for example "minion2" at /tmp/data/index.html with the content Acct=Finance
* Create a PersistentVolume named task-pv-volume using hostPath and allocate 1Gi to it, specifying that the volume is at
  /tmp/data on the cluster's node.
* The configuration should specify the access mode of ReadWriteOnce.
* Create a PersistentVolumeClaim named task-pv-claim that requests a volume of at least 100Mi and specifies an access
  mode of ReadWriteOnce
* Create a pod that uses the PersistentVolumeClaim as a volume with a label app: my-storage-app mounting the resulting
  volume to a mountPath /usr/share/nginx/html inside the pod

#### Answer:

* kubectl create deployment nginx --image=nginx --port=80 --replicas=4 --dry-run=client -o yaml > seven_d.yaml
* kubectl expose deployment nginx --target-port=80 --port=80

---

## Question: 8

Developers occasionally need to submit pods that run periodically.
Task:

> Follow the steps below to create a pod that will start at a predetermined time and]which runs to completion only once
> each time it is started:

* Create a YAML formatted Kubernetes manifest, that runs the following shell command, in a single busybox container:

> date

* The command should run every minute and must complete within 22 seconds or be terminated by Kubernetes.
* The Cronjob name and container name should both be "hello"
* Create the resource in the above manifest and verify that the job executes successfully at least once

#### Answer:

* kubectl create cronjob hello --image=busybox --schedule "*/1 * * * *" --dry-run=client -o yaml > eight.yaml

---

## Question: 9

create three pod:

1. web
2. storage
3. client

> use a network policy that will allow "client" pod to send and receive traffic only to and from the web and storage
> pods.

#### Answer:

* kubectl create deployment nginx --image=nginx --port=80 --dry-run=client -o yaml > nine_a.yaml
* kubectl expose deployment nginx --target-port=80 --port=80 --dry-run=client -o yaml > nine_b.yaml
* kubectl run nginx-client --image=busybox --labels=access-nginx=true --dry-run=client -o yaml > nine_d.yaml
* kubectl run nginx-do-not-allow-client --image=busybox --dry-run=client -o yaml > nine_e.yaml
* kubectl exec -it nginx-client -- wget http://nginx --timeout 2
* kubectl exec -it nginx-do-not-allow-client -- wget http://nginx --timeout 2

---

## Question: 9

> List all persistent volumes sorted by capacity

#### Answer:

* kubectl get persistentVolumes --sort-by=.spec.capacity.storage -o json > volume_list.json
* kubectl get persistentVolumes --sort-by=.spec.capacity.storage -o yaml > volume_list.yaml

---

## Question: 10

>Ensure a single instance of pod nginx is running on each node in the cluster

* where nginx also represents the image name which has to be used
* Do not override any taints currently in place.
* Use DaemonSet to complete this task and use ds-nginx as DaemonSet name