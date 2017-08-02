# Module 01 - Developing on Kubernetes

In this module, you will learn to:
  - Deploy a webapp to Kubernetes
  - Expand the webapp to use other Kubernetes resources and best practices
  - Work with the Tectonic Ingress Controller
  - Stand up your own Ingress Controller

## Requirements
* go 1.8.3
* Kubernetes 1.7+

## Tasks

### Setup - Run Go HTTP Server on Kubernetes

1. Clone the [k8s-demo](https://github.com/metral/k8s-demo) repo
    ```
    $ git clone https://github.com/metral/k8s-demo
    ```

1. Build and Run `k8s-demo`

    https://github.com/metral/k8s-demo#build-and-run

1. Once k8s-demo is running on Kubernetes, your environment is ready.

1. Create an account on [Quay](https://quay.io/signin/) if you don't have one
   already. 

### Exercises

*Note:* For each exercise listed below, do the following where applicable before moving onto the next task:

  * Complete the task
  * Build the container and tag it by exercise number
  * Push the container to your personal `k8s-demo` repo in Quay
  * Redeploy the app to k8s with the latest tag

1. Add a new API endpoint in `k8s-demo` that:

    - Accepts a `GET` request on `/testing`
    - Returns an HTTP 200 and a body of "testing" 

   curl the service within the cluster, and outside of it.

1. Add a new API endpoint in `k8s-demo` that:

    - Accepts a `GET` request on `/healthz`
    - Returns an HTTP 200 and a body of "ok" 

   curl the service within the cluster, and outside of it.

1. Configure [Kubernetes Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) for the `k8s-demo` deployment:
    
    - Create a readiness probe with a TCP socket check on the listening port of the API server
    - Create a liveness probe with an HTTP check on the new `/healthz` endpoint

1. Modify the `/healthz` endpoint in `k8s-demo` to return an HTTP 500. What
   happens during deployment when this change is rolled out?

1. Delete the `k8s-demo` deployment and create the [LimitRange](https://kubernetes.io/docs/tasks/administer-cluster/cpu-memory-limit/) provided:
    ```
    $ kubectl delete deploy/foobar
    $ kubectl create -f https://git.io/v7EoU
    ```

   Now, try redeploying the `k8s-demo` from exercise/tag #2. What happens?

1. Modify the k8s-demo deployment to request 10 mebibytes of RAM and 1/50th of 1 CPU core from the cluster, and have a limit of 2x the amount of each resource requested.

    - [Hint (if needed)](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container#resource-requests-and-limits-of-pod-and-container)

