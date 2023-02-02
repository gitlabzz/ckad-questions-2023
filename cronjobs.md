### cron jobs related questions:

Create a Kubernetes cron job that runs every minute and prints current date.

How to scale a Kubernetes cron job replicas based on the number of pending tasks?

How to troubleshoot a failed Kubernetes cron job and view its logs?

What is the recommended way to manage the concurrency of a Kubernetes cron job?

How to set environment variables for a command in a Kubernetes cron job YAML definition?

What is the maximum number of failed retries allowed for a Kubernetes cron job?

How to view the history of a Kubernetes cron job and inspect its past runs?


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

* kubectl create cronjob hello --image=busybox --schedule="*/1 * * * *" --dry-run=client -o yaml > hello-job.yaml