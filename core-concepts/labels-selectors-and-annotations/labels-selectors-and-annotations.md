### Core Concepts - basic questions to practice use of "kubectl" command

> Core Concepts: Understand the basic concepts of Kubernetes, such as pods, services, and replication controllers. The
> difficulty level goes up as you proceed ... so, please keep going till very last question!









 






---

> #### Question: Create a new namespace called "production" and label it with the environment="production"

> #### Question: Create a new pod called "mypod" in the "production" namespace. Update the pods to have labels app="myapp" and environment="production"

> #### Question: Create a new service called "myservice" that selects pods with the label app="myapp" and environment="production"

> #### Question: Update the label on the "mypod" pod to environment="staging" Verify that the "myservice" is no longer selecting the "mypod" pod

> #### Question: Create a new service called "stagingservice" that selects pods with the label environment="staging", Verify that the "stagingservice" is now selecting the "mypod" pod

> #### Question: Annotate the "mypod" pod with the annotation "version" and give it a value of "1.0", Verify that the annotation "version" with the value "1.0" has been added to the "mypod" pod

> #### Question: Update the annotation on the "mypod" pod to "version" with the value "2.0", Verify that the annotation on the "mypod" pod has been updated to "version" with the value "2.0"


> #### Question: create a service that only selects pods with label "env=dev" using the kubectl command?

> #### Question: add an annotation "version=1.0" to a deployment named "my-deployment" using the kubectl command?

> #### Question: update the value of an existing annotation "release" to "2.0" on a pod named "my-pod" using the kubectlcommand?

> #### Question: get the annotations of a pod named "my-pod" in namespace "my-ns" using the kubectl command?

> #### Question: delete the annotation "version" from a service named "my-service" using the kubectl command?

> #### Question: list all pods in a namespace that have the annotation "release=2.0" using the kubectl command?








> #### Question:Create a service that selects pods with the label "environment" with value "staging" and a label "tier" with value "frontend".

> #### Question: 
> #### Question: Create a pod with a label "app" with value "myapp" and an annotation "release" with value "v1.0".

> #### Question: Create a service that selects pods with the label "app" with value "myapp" and the annotation "release" with value "v1.0".

> #### Question: Write a command that shows all the pods that have the annotation "release" with value "v1.0" and the label "app" with value "myapp"

 

> #### Question: Write a command that updates the value of the annotation "release" for all pods with label "app" with value "myapp" to "v2.0"

> #### Question: Create a service that selects pods with the label "environment" with value "staging" and a label "tier" with value "frontend" and the label "app" with value "myapp"

 

> #### Question: Create a pod with a label "app" with value "myapp" and an annotation "release" with value "v1.0" and a label "environment" with value "production"

> #### Question: Create a service that selects pods with the label "app" with value "myapp" and the annotation "release" with value "v1.0" and a label "environment" with value "production"

> #### Question: Write a command that shows all the pods that have the annotation "release" with value "v1.0" and the label "app" with value "myapp" and the label "environment" with value "production"

> #### Question: Write a command that updates the value of the label "environment" for all pods with label "app" with value "myapp" and annotation "release" with value "v1.0" to "staging"

> #### Question: Write a command that updates the value of the annotation "release" for all pods with label "app" with value "myapp" and label "environment" with value "production" to "v2.0"

> #### Question: Write a command that shows all the pods that have a label "environment" with value "staging" or "production"

> #### Question: Write a command that shows all the pods that have a label "environment" with value "staging" and a label "tier" with value "frontend" or "backend"

> #### Question: Write a command that shows all the pods that have a label "environment" with value "staging" or "production" and a label "tier" with value "frontend"


> #### Question: How can you use labels to control traffic to a specific version of your application?





> #### Question: 



> #### Question: How can you use annotations to store information about a resource?

> #### Question: How can you use annotations to configure an ingress controller?

> #### Question: How can you use selectors to filter pods by label values?

> #### Question: How can you use selectors to create a service that automatically updates its endpoints?

> #### Question: How can you use labels and selectors to organize your resources in namespaces?

> #### Question: How can you use annotations to configure automatic sidecar injection in a pod?

> #### Question: How can you use annotations to configure automatic certificate provisioning for a service?

> #### Question: How can you use selectors to create a replica set that automatically scales pods?

> #### Question: 

> #### Question: How can you use annotations to configure liveness and readiness probes for a pod?

> #### Question: How can you use selectors to create a service that automatically balances traffic between pods?

> #### Question: How can you use labels and selectors to create a pod that automatically rolls back to a previous version?

> #### Question: How can you use annotations to configure automatic horizontal pod scaling?

> #### Question: How can you use selectors to create a service that automatically configures DNS?

> #### Question: 

> #### Question: How can you use annotations to configure automatic pod prioritization and preemption?

> #### Question: Create a deployment with 3 replicas that has a label app=myapp and a selector that matches pods with that label.

> #### Question: Create a service that selects pods with the label app=myapp and the annotation color=blue.

> #### Question: Update the label app=myapp to app=mynewapp on all pods in a specific namespace.

> #### Question: List all pods in a namespace that have an annotation with the key "release" and value "stable".

> #### Question: Delete all pods with the label "environment" set to "production".

> #### Question: Create a service that selects pods with the label "app" set to "myapp" and exposes it on port 8080.

> #### Question: List all services in a namespace that have a selector with the key "tier" and value "backend".

> #### Question: Update the annotation "version" on all pods in a specific namespace to "v1.2".

> #### Question: Create a pod that has a label "team" set to "development" and an annotation "owner" set to "jane".

> #### Question: Create a deployment that has 3 replicas and a label "environment" set to "production" and a selector that matches pods with that label.


> #### Question: Create a new namespace called "production" and label it with the environment="production"

> #### Question: Create a new pod called "mypod" in the "production" namespace and label it with app="myapp" and environment="production"

> #### Question: Create a new service called "myservice" that selects pods with the label app="myapp" and environment="production"

> #### Question: Update the label on the "mypod" pod to environment="staging"

> #### Question: Verify that the "myservice" is no longer selecting the "mypod" pod

> #### Question: Create a new service called "stagingservice" that selects pods with the label environment="staging"

> #### Question: Verify that the "stagingservice" is now selecting the "mypod" pod

> #### Question: Annotate the "mypod" pod with the annotation "version" and give it a value of "1.0"

> #### Question: Verify that the annotation "version" with the value "1.0" has been added to the "mypod" pod

> #### Question: Update the annotation on the "mypod" pod to "version" with the value "2.0"

> #### Question: Verify that the annotation on the "mypod" pod has been updated to "version" with the value "2.0"


