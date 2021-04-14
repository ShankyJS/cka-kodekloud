# High Level Kubernetes Architecture

## Components

# Nodes

A node is a worker machine in Kubernetes (like a VM) and depending on the cluster can be a physical or virtual machine, Each node is managed by the "control plane" and a Node can have multiple pods.

Every Kubernetes Node runs at least:

*Kubelet:* Is responsible for communication between the K8s MAster and the Nodes, it manages The Pods and containers running on each machine.

*A container runtime:* This piece is responsible for pulling the container image from a registry, unpacks the container and run it on the node. (Can be Docker, Packer, Containerd, Cr-io, etc).

*kube-proxy:* kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.

kube-proxy maintains network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster.

kube-proxy uses the operating system packet filtering layer if there is one and it's available. Otherwise, kube-proxy forwards the traffic itself.



## Master Nodes

Master nodes runs the Control Plane components on them.

The control plane's components make global decisions about the cluster (for example, scheduling), as well as detecting and responding to cluster events (for example, starting up a new pod when a deployment's 
replicas

*kube-apiserver:* It's in charge of orchestrate all the pieces and components from a K8s cluster, and validates data for api-objects which include pods, services, replicationcontroller.
The API Server services REST operations and provides the frontend to the cluster's shared state through which all other components interact.

*ETCD Cluster:* DataStore for Kubernetes that creates objects in Key values references in order to save the state of the K8s components, nodes, deployments, and most of the objects.

*Kube-controller-manager:* It's in charge of administrate all the controllers in K8s,  a controller is a control loop that watches the shared state of the cluster through the apiserver and makes changes attempting 
to move the current state towards the desired state. 
Examples of controllers that ship with Kubernetes today are the replication controller, endpoints controller, namespace controller, and 
serviceaccounts controller.

*Kube-scheduler:* The scheduler is the component that prepares and assigns the workloads to the worker nodes, assigns the pods that will run in each node according to the resources settings, allocation and
based on the configs that we marked on the deployment.

## Worker Nodes

*kubelet:* Ensures that the exact quantity of pods / containers are running on each worker node, and it's in charge of destroy and create containers / pods / objects.
