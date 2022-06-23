## Intro
    June 06, 2022
    Ditah, K DevSecOps @ Plotly
## Gist!
    k8s Production & Security Best Practices
##

## k8s(cluster(Node(Pod(Container(image(version))))))
    - Specify a pinned version on each container image
    Why?
        Otherwise, the latest version is fetched, which makes it unpredictable and intransparent as to which versions are deployed in the cluster
  
    - Configure a liveness probe on each container
    Why?
        K8s knows the Pod state, not the application state. Sometimes a pod is running, but the container inside crashed. With a liveness probe, we can let K8s know when it needs to restart the container

    - Configure a readiness probe on each container
    Why? 
        Let's K8s know if an application is ready to receive traffic
    
    - Configure resource limits & requests for each container
    Why? 
        To make sure 1 buggy container doesn't eat up all resources, breaking the cluster

    - Don't use NodePort in production
    Why? 
        NodePort exposes Worker Nodes directly, multiple points of entry to secure. Better alternative: Loadbalancer or Ingress

    - Always deploy more than 1 replica for each application for HA (it is better to split resources between two pods than to have one)
    Why? 
        To make sure your application is always available, no downtime for users!

    - Always have more than 1 Worker Node
    Why?
         Avoid a single point of failure with just 1 Node

    - Label all your K8s resources
    Why?
        To Have an identifier for your components to group pods and reference in Service
        
    - Use namespaces to group your resources
    Why? 
        To organize resources and define access rights based on namespaces e.g.

    - Use namespaces to group your resources
    Why?
        To organize resources and define access rights based on namespaces e.g.

    - Ensure Images are free of vulnerabilities
    Why? 
        Third-party libraries or base images can have known vulnerabilities. You can do manual vulnerability scans or better-automated scans in CI/CD pipeline

    - No root access for containers
    Why?
        With root access, they have access to host-level resources. Much more damage is possible if the container gets hacked!
    
    - Keep the K8s version up to date
    Why & How? 
        The latest versions include patches to previous security issues etc. Upgrade with zero downtime by having multiple nodes and pod replicas on different nodes

        Useful Links:
        ● Git Repo for Best Practices Configuration Files for the Microservices App: https://gitlab.com/nanuchi/online-shop-microservices-deployment
        ● Configure Liveness, Readiness Probes: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
        ● Resource Requests & Limits: https://cloud.google.com/blog/products/containers-kubernetes/kubernetes-best-practices-resource-requests-and-limitsCheck

##