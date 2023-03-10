# ckad-questions-2023

> Core Concepts: Understand the basic concepts of Kubernetes, such as pods, services, and replication controllers.

* Understanding and using labels, selectors, and annotations
* Creating and configuring services, including ClusterIP, NodePort, and LoadBalancer services
* Understanding and using service discovery
* Understanding and using health checks
* Understanding and using service accounts
* Understanding and using network policies

---



How do you configure a multi-container pod in Kubernetes?
How do you configure a service to expose multiple ports for a single pod?
How do you configure a service to load balance traffic across multiple pods?
How do you configure a service to only expose certain endpoints to specific IP addresses or CIDR ranges?
How do you configure a service to automatically update its endpoints when pods are added or removed?
How do you configure a service to use a specific type of load balancer (e.g. external or internal)?
How do you configure a service to use a specific type of network (e.g. ClusterIP, NodePort, LoadBalancer)?
How do you configure a service to use a specific type of selector (e.g. label or field)?
How do you configure a service to use a specific type of health check (e.g. TCP or HTTP)?
How do you configure a service to use a specific type of session affinity (e.g. client IP or None)?
How do you configure a service to use a specific type of scaling (e.g. ReplicaSet or Deployment)?
How do you configure a service to use a specific type of rolling update strategy (e.g. RollingUpdate or Recreate)?
How do you configure a service to use a specific type of readiness check (e.g. HTTP or TCP)?
How do you configure a service to use a specific type of liveness check (e.g. HTTP or TCP)?
How do you configure a service to use a specific type of backup and restore strategy (e.g. etcd or snapshot)?
How do you configure a service to use a specific type of security (e.g. NetworkPolicy or PodSecurityPolicy)?
How do you configure a service to use a specific type of logging and monitoring (e.g. Fluentd or Prometheus)?
How do you configure a service to use a specific type of resource allocation (e.g. CPU or Memory)?
How do you configure a service to use a specific type of rolling update strategy (e.g. RollingUpdate or Recreate)?
How do you configure a service to use a specific type of storage class (e.g. standard or premium)?

How would you configure a Pod to have a specific hostname, rather than the default generated by Kubernetes?
How would you configure a service to only be accessible on the internal network, rather than being exposed externally?
How would you configure a Pod to use a specific DNS server, rather than the default?
How would you configure a service to load balance traffic across multiple Pods in multiple availability zones?
How would you configure a service to route traffic to different Pods based on the URL path?
How would you configure a service to encrypt all traffic using SSL/TLS?
How would you configure a service to route traffic to different Pods based on the client IP address?
How would you configure a service to route traffic to different Pods based on the request headers?
How would you configure a service to route traffic to different Pods based on the request cookies?
How would you configure a service to route traffic to different Pods based on the request method?
How would you configure a service to only allow traffic from specific IP addresses?
How would you configure a service to route traffic to different Pods based on the client's geographic location?
How would you configure a service to route traffic to different Pods based on the client's user agent?
How would you configure a service to route traffic to different Pods based on the client's accept-language header?
How would you configure a service to route traffic to different Pods based on the client's accept-encoding header?
How would you configure a service to route traffic to different Pods based on the client's referrer header?
How would you configure a service to route traffic to different Pods based on the client's x-forwarded-for header?
How would you configure a service to route traffic to different Pods based on the client's x-forwarded-proto header?
How would you configure a service to route traffic to different Pods based on the client's x-forwarded-port header?
How would you configure a service to route traffic to different Pods based on the client's x-forwarded-host header?

How can you configure a pod to run multiple containers at the same time?
How can you configure a service to load balance traffic across multiple pods?
How can you configure a service to be accessible only within the cluster?
How can you configure a service to be externally accessible through a specific hostname or IP address?
How can you configure a pod to run with specific resource constraints, such as memory and CPU?
How can you configure a pod to automatically restart if it crashes?
How can you configure a service to automatically scale the number of replicas based on traffic?
How can you configure a service to roll out a new version of the application without any downtime?
How can you configure a service to run with a specific type of load balancer?
How can you configure a pod to run with a specific security context?
How can you configure a pod to run with specific environment variables?
How can you configure a pod to run with a specific user and group?
How can you configure a service to run with a specific port?
How can you configure a service to run with a specific protocol (TCP or UDP)?
How can you configure a service to run with a specific external IP address?
How can you configure a service to run with a specific internal IP address?
How can you configure a pod to run with a specific label?
How can you configure a pod to run with a specific annotation?
How can you configure a service to run with a specific selector?
How can you configure a pod to run with a specific readinessProbe and livenessProbe?

How would you configure a Kubernetes Service to load balance between multiple pods of a Deployment that are running on
different nodes?
How would you configure a Kubernetes Service to route traffic to a specific pod based on the hostname in the HTTP
request?
How would you configure a Kubernetes Service to route traffic to a specific pod based on the path in the HTTP request?
How would you configure a Kubernetes Service to route traffic to multiple versions of a Deployment based on a specific
header in the HTTP request?
How would you configure a Kubernetes Service to route traffic to a specific pod based on a specific cookie in the HTTP
request?
How would you configure a Kubernetes Service to route traffic to a specific pod based on the source IP address of the
request?
How would you configure a Kubernetes Service to route traffic to a specific pod based on the request's TLS SNI?
How would you configure a Kubernetes Service to route traffic to multiple pods based on the request's HTTP method?
How would you configure a Kubernetes Service to route traffic to multiple pods based on a specific query parameter in
the HTTP request?
How would you configure a Kubernetes Service to route traffic to multiple pods based on a specific HTTP header in the
request?
How would you configure a Kubernetes Service to route traffic to multiple pods based on a specific cookie in the HTTP
request?
How would you configure a Kubernetes Service to route traffic to multiple pods based on the request's source IP address?
How would you configure a Kubernetes Service to route traffic to multiple pods based on the request's TLS SNI?
How would you configure a Kubernetes Service to route traffic to multiple pods based on the request's HTTP method?
How would you configure a Kubernetes Service to route traffic to multiple pods based on a specific query parameter in
the HTTP request?
How would you configure a Kubernetes Service to route traffic to multiple pods based on a specific HTTP header in the
request?
How would you configure a Kubernetes Service to route traffic to multiple pods based on a specific cookie in the HTTP
request?
How would you configure a Kubernetes Service to route traffic to multiple pods based on the request's source IP address?
How would you configure a Kubernetes Service to route traffic to multiple pods based on the request's TLS SNI?
How would you configure a Kubernetes Service to route traffic to multiple pods based on the request's HTTP method?

Create a multi-container pod using a YAML file that includes two containers, one running nginx and another running
redis. The nginx container should have a readiness probe that checks for the existence of a specific file, and the redis
container should have a liveness probe that checks for the ability to connect to the redis service.
Create a service that exposes a deployment running a stateful application. The service should use a selector to route
traffic to pods with a specific label, and it should also use a headless service to allow for stable network connections
to the pods.
Create a service that exposes a deployment running a stateless application. The service should use a LoadBalancer type
to route traffic to pods, and it should also use a ClusterIP to allow for internal communication between pods.
Create a service that exposes a deployment running a web application. The service should use a NodePort type to route
traffic to pods, and it should also use a ExternalName type to allow for external access to the pods from outside the
cluster.
Create a service that exposes a deployment running a database. The service should use a ExternalName type to route
traffic to a specific external endpoint, and it should also use a ClusterIP to allow for internal communication between
pods.
Create a service that exposes a deployment running a message queue. The service should use a ExternalName type to route
traffic to a specific external endpoint, and it should also use a ClusterIP to allow for internal communication between
pods.
Create a service that exposes a deployment running a caching service. The service should use a ExternalName type to
route traffic to a specific external endpoint, and it should also use a ClusterIP to allow for internal communication
between pods.
Create a service that exposes a deployment running a stateful application. The service should use a ExternalName type to
route traffic to a specific external endpoint, and it should also use a ClusterIP to allow for internal communication
between pods.
Create a service that exposes a deployment running a stateless application. The service should use a LoadBalancer type
to route traffic to pods, and it should also use a ClusterIP to allow for internal communication between pods.
Create a service that exposes a deployment running a web application. The service should use a NodePort type to route
traffic to pods, and it should also use a ExternalName type to allow for external access to the pods from outside the
cluster.
Create a service that exposes a deployment running a database. The service should use a ExternalName type to route
traffic to a specific external endpoint, and it should also use a ClusterIP to allow for internal communication between
pods.
Create a service that exposes a deployment running a message queue. The service should use a ExternalName type to route
traffic to a specific external endpoint, and it should also use a ClusterIP to allow for internal communication between
pods.
Create a service that exposes a deployment running a caching service. The service should use a ExternalName type to
route traffic to a specific external endpoint, and it should also use a ClusterIP to allow for internal communication
between pods.

Create a Pod with multiple containers that need to share a volume. Configure the Pod to ensure that the containers can
access the shared volume simultaneously.
Create a Service that exposes a deployment running in a specific namespace. Ensure that the Service is only accessible
within the namespace and not externally.
Create a Pod that runs multiple containers that need to communicate with each other over a specific network interface.
Configure the Pod to ensure that the containers can communicate over the specified network interface.
Create a Service that load balances traffic to multiple Pods in a deployment. Configure the Service to use a specific
algorithm for load balancing, such as round robin or least connections.
Create a deployment with two replicas of a Pod. Configure the deployment to automatically scale up to four replicas when
CPU usage exceeds a certain threshold.
Create a Service that exposes a deployment running in a specific namespace. Use a label selector to ensure that only
Pods with a specific label are exposed by the Service.
Create a Pod that runs a container that needs to listen on a specific host port. Configure the Pod to ensure that the
container can listen on the specified host port.
Create a deployment that runs a stateful application, such as a database. Use a StatefulSet to ensure that the
deployment maintains the desired number of replicas and that each replica has a unique hostname.
Create a Service that load balances traffic to multiple Pods in a deployment. Use an external load balancer to balance
traffic to the Service.
Create a deployment that runs a state

Create a StatefulSet with 3 replicas that uses a custom image and a specific tag. The StatefulSet should also have a
unique hostname for each replica.
Create a Deployment with 5 replicas and a custom image. Scale the Deployment to have 10 replicas.
Create a Pod that runs a container and exposes two ports, one for HTTP and one for HTTPS. The container should be able
to read a specific ConfigMap and use the data from it.
Create a Service that exposes a Deployment and uses a specific type of load balancing. Use a selector to target the pods
in the Deployment.
Create a Pod that runs two containers. One container should be able to read a specific ConfigMap and use the data from
it, the other should be able to read a Secret and use the data from it.
Create a Kubernetes cluster with a specific version and using a specific network plugin. The cluster should have at
least 3 nodes, one of which should be a master node.
Create a Kubernetes cluster with a specific version and using a specific network plugin. The cluster should have at
least 3 nodes, one of which should be a master node. Deploy a stateful application on it and configure it to use a
Persistent Volume
Create a Kubernetes cluster with a specific version and using a specific network plugin. The cluster should have at
least 3 nodes, one of which should be a master node. Deploy a stateful application on it and configure it to use a
Persistent Volume Claim
Create a Pod that runs a container and uses a specific resource limit and a specific resource request. The container
should be able to read a specific ConfigMap and use the data from it.
Create a Kubernetes cluster with a specific version and using a specific network plugin. The cluster should have at
least 3 nodes, one of which should be a master node. Deploy a stateful application on it and configure it to use a
Persistent Volume Claim and configure it to use a ReadWriteMany access mode
Create a Deployment that runs a container and uses a specific resource limit and a specific resource request. Use a
rolling update strategy to update the container image to a new version.
Create a Kubernetes cluster with a specific version and using a specific network plugin. The cluster should have at
least 3 nodes, one of which should be a master node. Deploy a stateful application on it and configure it to use a
Persistent Volume Claim and configure it to use a ReadWriteOnce access mode
Create a Pod that runs a container and uses a specific resource limit and a specific resource request. The container
should be able to read a specific ConfigMap and use the data from it. Use a readiness probe and a liveness probe to
check the health of the container.
Create a Kubernetes cluster with a specific version and using a specific network plugin. The cluster should have at
least 3 nodes, one of which should be a master node. Deploy a stateful application on it and configure it to use a
Persistent Volume Claim and configure it to use a ReadOnlyMany access mode
Create a Deployment that runs a container and uses a specific resource limit and a specific resource request. Use a
rolling update strategy to update the container image to a new version. Use a readiness probe and a liveness probe to
check the health of the container.
Create a Service that exposes a Deployment and uses a specific type of load balancing. Use a selector to target the pods
in the Deployment



---




Configuration: Learn how to create and manage the configuration of Kubernetes resources, including YAML and JSON.
Multi-Container Pods: Understand how to create and manage multi-container pods, including how to use init containers and
sidecars.
Observability: Learn how to monitor and troubleshoot Kubernetes clusters and applications, including using tools like
logs, events, and metrics.
Pod Design: Understand best practices for designing and deploying pods, including how to use labels, selectors, and
resource requests/limits.
Services & Networking: Learn how to create and manage services and networking in a Kubernetes cluster, including how to
use services, service discovery, and ingress.
State Persistence: Understand how to use persistent storage in Kubernetes, including how to use persistent volumes,
claims, and storage classes.
Security: Learn about Kubernetes security best practices, including how to use secrets, service accounts, and secure
communication.
Extending Kubernetes: Understand how to extend Kubernetes, including how to use custom resources, controllers, and
operators.
Scaling: Learn how to scale both the control plane and worker nodes of a Kubernetes cluster, as well as how to scale
individual applications.

However, I can give you an idea of the areas that the CKAD exam focuses on, which include:
Configuring Pods and Services
Writing Configurations
Networking
Ingress
State Persistence
Scaling Applications
Debugging and Troubleshooting
Multi-Container Pods
Pod Design
Service Mesh