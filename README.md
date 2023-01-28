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

> Ensure a single instance of pod nginx is running on each node in the cluster

* where nginx also represents the image name which has to be used
* Do not override any taints currently in place.
* Use DaemonSet to complete this task and use ds-nginx as DaemonSet name

---

## Question: 11

> Crate a pod that has main container and init container

* main container reads and prints the contents of file created by init container

#### Answer:

* kubectl run pod11 --image=busybox --restart=Never --dry-run=client -o yaml >> eleven.yaml

---

## Question: 12

Schedule a pod on a node with label zone:dmz

#### Answer:

* kubectl run pod12 --image=busybox --restart=Never --dry-run=client -o yaml >> twelve.yaml

---

## Question: 13

> Create a deployment with name nginx-app

* Using container nginx with version 1.23.3
* The deployment should contain 3 replicas
* Next, deploy the application with new version latest, by performing a rolling update
* Finally, rollback that update to the previous version 1.23.3

#### Answer:

* kubectl create deployment nginx-app --image=nginx:1.23.3 --replicas=3
* kubectl rollout status deployment nginx-app
* kubectl set image deployment nginx-app nginx=nginx:latest
* kubectl rollout status deployment nginx-app
* kubectl rollout undo deployment nginx-app

---

## Question: 14

> Create a service demo-service that routes to the existing pod named nginx

#### Answer:

* kubectl run nginx --image=nginx --port=80
* kubectl expose pod nginx --name=demo-service --target-port=80 --port=80

---

## Question: 15

> print pod names having label app=nginx

#### Answer:

* kubectl create deployment nginx --image=nginx --replicas=7
* kubectl get pods -l app=nginx -o NAME

---

## Question: 16

> Create a Kubernetes secret with Name "bobs-secret" containing data "password=bob"

* Create a pod named pod-secrets-via-file, using the nginx image, which mounts the secret named bobs-secret at
  /secrets
* Create a second pod named pod-secrets-via-env, using the nginx Image, which exports password as CONFIDENTIAL
  environment variable

#### Answer:

* kubectl create secret generic bobs-secret --from-literal=password=bob

---

## Question: 17

> Create two deployments both using same persistent volume to read and write data

* Deployment A uses worker node with label name=minion1
* Deployment B uses worker node with label name=minion2
* Create a writer pod using busybox image to write something in shared persistent volume that can be accessed by the
  deployments
* Persistent Volume is allocated by the storage class named nfs-client

#### Answer:

* kubectl create deployment deployA --image busybox --dry-run=client -o yaml >> seventeen.yaml

---

Question: 18

> Scale the deployment webserver to 6 pods.

#### Answer:

* kubectl scale deployment webserver --replicas=6

---

## Question: 19

> Create a deployment as follows:

* Deployment name nginx using nginx image
* Exposed via a service called nginx-svc
* Ensure that the service & pod are accessible via their respective DNS records
* use the utility nslookup to look up the DNS records of the service & pod

#### Answer:

* kubectl create deployment nginx --image=nginx --replicas=2
* kubectl expose deployment nginx --name nginx-svc --target-port=80 --port=80
* kubectl get pods -o wide | grep nginx
    * nginx-748c667d99-56t6q 1/1 Running 0 19m 192.168.179.215 minion2   <none>           <none>
    * nginx-748c667d99-rlzqz 1/1 Running 0 19m 192.168.34.30 minion1   <none>           <none>
* kubectl run -i --tty debugger --image=radial/busyboxplus:curl --restart=Never -- nslookup nginx-svc
* kubectl run -i --tty debugger --image=radial/busyboxplus:curl --restart=Never -- nslookup 192-168-179-215.web.pod

> for pod nslookup: pod-ip replace dots with hyphen and fully qualify with .namespace-name.pod

---

## Question: 20

> Create a snapshot of the etcd instance running at https://127.0.0.1:1111, saving the snapshot to the file path
> /tmp/snapshot.db. The following TLS certificates/key are supplied for connecting to the server with etcdctl:

* CA certificate: /tmp/ca.crt
* Client certificate: /tmp/client.crt
* Client key: /tmp/client.key

#### Answer:

* ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1.1111 --cacert=/tmp/ca.crt --cert=/tmp/client.crt
  --key=/tmp/client.key snapshot save /tmp/snapshot.db

---

## Question: 21

Set the node named "minion2" as unavailable and reschedule all the pods running on it.

#### Answer:

* kubecctl config use-context dev
* kubectl create deployment nginx --image=nginx --replicas=20
* kubectl drain minion2 --ignore-daemonsets --delete-emptydir-data --force

> to enable scheduling on node

* kubectl uncordon minion2

---

## Question: 21

> Your application’s namespace requires a specific service account to be used.

* Create service account "limited-service"
* Update the nginx deployment to run as "limited-service" using service account

#### Answer:

* kubectl create serviceaccount limited-service
* kubectl get serviceaccounts
* kubectl create deployment nginx --image=nginx
* kubectl get deployments
* kubectl set serviceaccount deployment nginx limited-service

---

## Question: 22

> A pod is running on the cluster, but it's not responding. The desired behavior is to have Kubernetes restart the pod
> when an endpoint returns an HTTP 500 on the /healthcheck endpoint. The service should never send traffic to the
> pod while it is failing. Please complete the following:

* The application has an endpoint, /ready, that will indicate if it can accept traffic by returning an HTTP 200. If
  the endpoint returns an HTTP 500, the application has not yet finished initialization.
* The application has another endpoint /healthcheck that will indicate if the application is still working as expected
  by
  returning an HTTP 200. If the endpoint returns an HTTP 500 the application is no longer responsive.

#### Answer:

* twentyTwo.yaml

---

## Question: 23

> Update the app deployment with a maxSurge of 10% and a maxUnavailable of 3%

* create a deployment with image nginx:latest
* Perform a rolling update of the nginx deployment, changing the nginx image version to 1.23.3
* Roll back the app deployment to the previous version that is nginx:latest

#### Answer:

* kubectl create deployment nginx --image=nginx:latest --port=80 --dry-run=client -o yaml >> twentyThree.yaml
* kubectl set image deployment nginx nginx=nginx:1.23.3
* kubectl rollout status deployment nginx
* kubectl rollout undo deployment nginx
* kubectl rollout status deployment nginx
* kubectl delete deployment nginx

---

