# kubernetes

Working With Pods
-
- In Virtualization world the atomic unit of scheduling is `VM`, in docker it is the `container`, whereas in kubernetes it is `pod`.
- Pod is a highlevel construct than a container, but it is much simpler(or smaller) than a VM.
- A pod consists of one or more containers. If multiple services need to be coupled, then having multiple containers in a pod is better.
- We deploy a pod to a cluster by defining it in a manifest file. Manifest file is passed to the api-server using cli to the scheduler. Scheduler deploy the pods to a node.
- Depending on the manifest file, a pod may container one or more containers.
- A pod gets a single ip, irrespective of how many containers are present in the pod. So, ports have to be unique between the containers.
- All the containers in a pod share the same cgroup limit, access to same volumes, same network, ipc namespaces etc.
- Inter-pod communication is possible because all pod ipaddresses are routable on the pod network.
- Intra-pod communication happens directly through `localhost` interface.
- Deployment in a pod is atomic. If 2 containers are present in a pod, then a pod will be accessible only when both containers are up and running.
- Lifecyle of Pod
  - Define the manifest.
  - Send the manifest to api server.
  - Api server schedules it to a node.
  - Pod goes to `Pending` state while the node download the images and start the containers.
  - Pod stays in `Pending` state until all containers are up and running.
  - Once all containers are up, pod state changes to `Running`. Incase of failure, pod goes to `Failed` state.
  - Failed, stopped Pods can't be restarted. They are discarded and new ones are started inplace of failed nodes.
  
