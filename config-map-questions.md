# ckad-questions-2023

just some questions from my practice about ConfigMap
---

# Practice Question 29th Jan 2023

## Question:1

### 







You have a ConfigMap named "app-config" in Namespace "production" that contains several key-value pairs. 
You need to update a specific key in the ConfigMap with a new value. How can you do this using kubectl?

You have a ConfigMap named "app-config" in Namespace "staging" that contains several key-value pairs. 
You need to create a new ConfigMap with the same data in Namespace "production". How can you do this using kubectl?

You have a ConfigMap named "app-config" in Namespace "production" that contains several key-value pairs. 
You need to create a new ConfigMap in Namespace "production" with the same data, but with a different name. 
How can you do this using kubectl?

You have a ConfigMap named "app-config" in Namespace "staging" that contains several key-value pairs. 
You need to create a new ConfigMap in Namespace "production" with the same data, but with a different name. 
Additionally, you need to create a new key-value pair in the new ConfigMap. 
How can you do this using kubectl?

You have a ConfigMap named "app-config" in Namespace "production" that contains several key-value pairs. 
You need to create a new ConfigMap in Namespace "production" with the same data, but with a different name. 
Additionally, you need to delete a specific key from the new ConfigMap. 
How can you do this using kubectl?

You have a ConfigMap named "app-config" in Namespace "production" that contains several key-value pairs. 
You need to create a new ConfigMap in Namespace "production" with a subset of the key-value pairs from the original ConfigMap. 
How can you do this using kubectl?

You have a ConfigMap named "app-config" in Namespace "production" that contains several key-value pairs. 
You need to update a specific key in the ConfigMap with a new value and also update a specific key in the ConfigMap with a new value using a kubectl patch command. 
How can you do this?

You have a ConfigMap named "app-config" in Namespace "staging" that contains several key-value pairs. 
You need to create a new ConfigMap with the same data in Namespace "production" and you need to update the new ConfigMap with a new key-value pair using kubectl edit command. 
How can you do this?










Your company has a microservices based application running on a Kubernetes cluster. 
The application uses several ConfigMaps for different services in the "production" Namespace to store its configuration. 
You have been asked to update the database connection string in the ConfigMap named "db-config" in the "production" Namespace. 
Additionally, you need to create a new ConfigMap with the same data, but with a different name and also update the Deployment with the new ConfigMap. 
How can you do this?

Your company has a distributed application running on a Kubernetes cluster. 
The application uses a ConfigMap named "app-config" in the "production" Namespace to store its configuration. 
You need to update a specific key in the ConfigMap and roll out the change to the Deployment with zero downtime. 
Additionally, you need to update the ConfigMap in all the existing pods of the Deployment with the new ConfigMap. 
How can you do this?


Your company has a web application running on a Kubernetes cluster. 
The application uses a ConfigMap named "web-config" in the "production" Namespace to store its configuration. 
You need to update the app version to the latest release in the ConfigMap and roll out the change to the Deployment with zero downtime. 
Additionally, you need to create a new ConfigMap with the same data, but with a different name and also update the Deployment with the new ConfigMap. 
Additionally, you need to update the ConfigMap in all the existing pods of the Deployment with the new ConfigMap 
and also you need to rollback to the previous version of the ConfigMap if any errors occur during the update. 
How can you do this?
