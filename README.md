# ckad-questions-2023

just some questions from my practice
---

# Practice Question 26th Jan 2023

## Question:1

### Create a new deployment for running.nginx with the following parameters:

* Name the deployment nginx and configure with 4 replicas
* set the rolling update strategy with 25%
* Configure the pod with a container image of nginx:latest
* Set an environment variable NGINX-PORT=8080 and also expose that port for the container
* set cpu and memory limit for container to cpu=150m and memory=150Mi
* when creating deployment ensure that you record the change cause
* check deployment status
* change deployment's container's image to nginx:1.23.1 with change cause recording
* check deployment history
* rollback to previous version

#### Answer:

* kubectl create deployment nginx --image=nginx --replicas=4 --dry-run=client --port=8080 -o yaml > one.yaml
* check one.yaml
* kubectl apply -f one.yaml --record
* kubectl set image deployment nginx-deployment nginx-container=nginx:1.23.1 --record
* kubectl rollout status deployment nginx-deployment
* kubectl rollout history deployment nginx-deployment
* kubectl rollout undo deployment nginx-deployment --to-revision=1
* kubectl rollout status deployment nginx-deployment

---

## Question:2

### Create a secret and consume the secret in a pod using environment variables as follows:

* Create a secret named another-secret with a key/value pair - key1/value4
* Start nginx pod named nginx-secret using container image nginx on worker node named minion2
* add an environment variable with name "COOL_VARIABLE" exposing the value of the secret key "key1"
* add an annotation that records secretName:another-secret
* start the pod and check the value of COOL_VARIABLE

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
* Have 2 replicas
* Exposes the service on TCP port 8080
* increase deployment replicas to 5
* test the service using its DNS name using a temporary pod
* decrease deployment replicas to 2
* change deployment image for nginx container to nginx:latest
* update the change cause for revision 2 to "only updated nginx image, set to nginx:latest"
* add a custom annotation with key: my-custom-annotation and value="just a custom annotation for testing!!!"

#### Answer:

* kubectl create deployment nginx --image=nginx --port=80 --dry-run=client --replicas=2 -o yaml > four.yaml
* kubectl expose deployment nginx-deployment --name=nginx-service --target-port=8080 --port=8080
  --selector=type=frontEnd --dry-run=client -o yaml > four_b.yaml
* kubectl scale deployment nginx-deployment --replicas=10
* kubectl rollout status deployment nginx-deployment
* kubectl run tmp --image=radial/busyboxplus:curl --restart=Never --rm -i --tty -- curl nginx-service:8080
* kubectl scale deployment nginx-deployment --replicas=2
* kubectl rollout status deployment nginx-deployment
* kubectl rollout history deployment nginx-deployment
* kubectl set image deployment nginx-deployment nginx=nginx:latest --record
* kubectl patch deployments nginx-deployment --patch '{"metadata": {"annotations": {"kubernetes.io/change-cause": "only
  updated nginx image, set to nginx:latest"}}}'
* kubectl rollout history deployment nginx-deployment
* kubectl patch deployments nginx-deployment --patch '{"metadata": { "annotations": { "my-custom-annotation": "just a
  custom annotation for testing!!!" } } }'

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

> Follow the steps below to create a pod that will start at a predetermined time and runs to completion only once
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
* print service account token in base64 decoded form

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

## Question: 24

> define pod that run periodically:

* runs date command in a single busybox container.
* The command should run every minute and must complete within 22 seconds

#### Answer:

* kubectl create cronjob datewriter --image=busybox --schedule "*/1 * * * *" --dry-run=client -o yaml >>
  twentyFound.yaml

---

## Question: 24

> Create a resource quota and apply to a namespace

* kubectl create quota test-quota --hard=pods=5,cpu=500m,memory=1Gi --namespace=web
* kubectl delete quota test-quota

---

### High level questions:

Ability to use Kubernetes API objects to manage and configure a cluster
Configuring and using secrets and ConfigMaps
Creating and managing custom resources and controllers
Creating and managing pods, services, and replication controllers
Debugging and troubleshooting Kubernetes clusters
Describe how to set up and use a ConfigMap in Kubernetes.
Describe how to set up and use a ConfigMap.
Describe how to set up and use a Persistent Volume Claim.
Describe how to set up and use a Secret.
Describe the difference between a Deployment and a ReplicationController in Kubernetes.
Describe the different types of Volumes in Kubernetes and when to use each.
Describe the process for creating and using a Kubernetes Custom Resource Definition (CRD).
Describe the process for debugging a Kubernetes application.
Describe the process for rolling out an update to a Deployment in Kubernetes.
Describe the process for rolling out an update to a Kubernetes deployment.
Describe the process for scaling a Deployment in Kubernetes.
Describe the process for scaling a Kubernetes deployment.
Describe the process of draining a node.
Describe the process of rolling out an update to a deployment.
Discuss the use of ConfigMaps and Secrets in a Kubernetes cluster.
Discuss the use of namespaces in Kubernetes and the process for switching between them.
Experience with configuring and running stateful applications on Kubernetes
Explain how to configure liveness and readiness probes in a Kubernetes pod.
Explain how to scale a deployment and what the impact is on the pods.
Explain how to set up and use a StatefulSet.
Explain how to troubleshoot a pod that is not starting or crashing.
Explain how you would roll out an update to a Deployment in a safe and controlled manner.
Explain the concept of a Kubernetes service and its role in networking.
Explain the difference between a Deployment and a ReplicaSet.
Explain the difference between a pod and a deployment.
Explain the purpose of a service and its different types.
Explain the role of the Kubernetes API server and how it communicates with other components in the cluster.
Explain the use of labels and selectors in Kubernetes.
Familiarity with Kubernetes advanced features such as horizontal pod autoscaling, custom resource definitions, and
operator frameworks
Familiarity with Kubernetes extensions and other ecosystem projects like Istio and Prometheus.
How can you create a ConfigMap using a YAML file?
How can you create a Kubernetes cluster on a public cloud provider such as GKE or EKS?
How do you configure a Kubernetes ConfigMap and use it in a Pod?
How do you configure a Kubernetes ConfigMap?
How do you configure a Kubernetes Pod to run multiple containers?
How do you configure a Kubernetes Pod to use a specific amount of CPU and memory resources?
How do you configure a Kubernetes Secret and use it in a Pod?
How do you configure a Kubernetes secret?
How do you configure a Kubernetes Service to access a Deployment using a specific IP and port?
How do you configure a Kubernetes Service to access a Deployment?
How do you configure a Kubernetes service to use a specific IP address?
How do you configure and use a Kubernetes Ingress resource?
How do you configure and use Kubernetes Security Contexts and Pod Security Policies?
How do you configure environment variables for a container running in a Kubernetes Pod?
How do you configure liveness and readiness probes for a container in a pod?
How do you configure network policies in a Kubernetes cluster?
How do you configure resource limits and requests for a container in a pod?
How do you configure resource limits for a pod in Kubernetes?
How do you create a ConfigMap in a Kubernetes cluster?
How do you create a ConfigMap in a specific namespace?
How do you create a Kubernetes Deployment?
How do you create a pod in Kubernetes?
How do you create and manage Persistent Volumes and Persistent Volume Claims in Kubernetes?
How do you create and use a Secret in Kubernetes?
How do you deploy an application using a Helm chart?
How do you ensure that a specific version of a container image is deployed to a pod?
How do you handle rolling updates in a Kubernetes deployment?
How do you implement Kubernetes network policies?
How do you perform a rolling update on a deployment in Kubernetes?
How do you roll back a Deployment in Kubernetes?
How do you roll back a deployment to a previous version?
How do you roll out a new version of a deployment?
How do you scale a Deployment in a Kubernetes cluster?
How do you scale a deployment in Kubernetes?
How do you scale a Deployment in Kubernetes?
How do you scale a deployment?
How do you set up a multi-container Pod in Kubernetes?
How do you set up a rolling update strategy for a Deployment in Kubernetes?
How do you set up and use a ConfigMap in a Kubernetes cluster?
How do you set up and use a horizontal pod autoscaler?
How do you set up and use a Kubernetes Ingress resource?
How do you set up and use a liveness probe for a pod?
How do you set up and use a readiness probe for a pod?
How do you set up and use a Secret in a Kubernetes cluster?
How do you set up automatic sidecar injection in a Kubernetes cluster?
How do you set up persistent storage for a Kubernetes Pod?
How do you troubleshoot a deployment that is not working as expected?
How do you troubleshoot a failing pod in Kubernetes?
How do you troubleshoot a Kubernetes cluster?
How do you troubleshoot a Pod that is in a CrashLoopBackOff state in Kubernetes?
How do you troubleshoot a pod that is in a CrashLoopBackOff state?
How do you troubleshoot a Pod that is not starting in Kubernetes?
How do you update the data in an existing ConfigMap?
How do you use Kubernetes for storage provisioning?
How to configure and use Kubernetes services?
How to configure liveness and readiness probes for a Pod?
How to configure security settings and network policies
How to create and manage config maps and secrets
How to create and manage ConfigMaps and Secrets?
How to create and manage Deployments
How to create and manage deployments and rollouts
How to create and manage Kubernetes objects using kubectl commands
How to create and manage Kubernetes objects using manifests
How to create and manage Kubernetes pods and deployments?
How to create and manage Pods
How to create and manage pods and replica sets
How to create and manage Replication Controllers and Replica Sets
How to create and manage Services
How to create and manage services and network access
How to create and manage Services, Endpoints, and Network Policies?
How to create and manage StatefulSets and PersistentVolumes?
How to debug and troubleshoot pods and replica sets
How to define and use environment variables in a Pod?
How to deploy stateful applications in Kubernetes?
How to manage and troubleshoot a Kubernetes cluster
How to manage storage and persistent volumes
How to roll back a Deployment?
How to scale and roll out updates to a deployment?
How to scale and update a Deployment?
How to scale and update application deployments
How to secure a Kubernetes cluster using network policies and secrets?
How to set resource limits and requests for a Pod?
How to troubleshoot and debug a Kubernetes cluster?
How to troubleshoot and debug common issues in a Kubernetes cluster.
How to troubleshoot and debug Kubernetes clusters
How to use and configure kubeadm and kubectl command-line tool to create a cluster.
How to use and configure kubectl command-line tool
How to use and create custom resources
How to use and manage ConfigMaps and Secrets
How to use and manage Ingress resources
How to use and manage Jobs and CronJobs
How to use and manage Namespaces and Resource Quotas.
How to use and manage Persistent Volumes and Claims
How to use kubectl command-line tool
How to use Kubernetes APIs and client libraries to automate cluster management tasks.
How to use Kubernetes autoscaling?
How to use Kubernetes config maps and secrets?
How to use Kubernetes ConfigMaps and Secrets to configure applications
How to use Kubernetes labels, selectors and annotations.
How to use Kubernetes Namespaces and Resource Quotas for multi-tenancy
How to use Kubernetes network primitives such as Services and Ingress
How to use Kubernetes security primitives such as Secrets and RBAC
How to use Kubernetes storage primitives such as Persistent Volumes and StatefulSets
How to use Kubernetes Volumes and Persistent Volumes?
How to use labels and selectors to organize and filter resources?
Knowledge of Kubernetes security features such as RBAC and network policies
Knowledge of Kubernetes troubleshooting and debugging techniques
Managing and maintaining Kubernetes clusters and nodes
Scaling and self-healing capabilities of Kubernetes
Setting up and using Ingress and service meshes
Understanding and implementing Kubernetes security best practices
Understanding and using Kubernetes networking and service discovery
Understanding of best practices for containerization and container orchestration
Understanding of Kubernetes networking and service discovery
Understanding of Kubernetes storage and volume management
Using Kubernetes API objects and kubectl commands
What is a Kubernetes service and how is it used?
What is the difference between a ReplicationController and a ReplicaSet in Kubernetes?
What is the purpose of a Service in Kubernetes and how is it different from a Deployment?
What is the purpose of a Service in Kubernetes?
What is the role of a ConfigMap and how is it used in a Kubernetes cluster?
