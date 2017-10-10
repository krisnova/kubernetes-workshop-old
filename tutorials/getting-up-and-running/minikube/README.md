# Getting Started with Minikube

## Install a Hypervisor

If you do not already have a hypervisor installed, install one now.

* For OS X, install
[xhyve driver](https://git.k8s.io/minikube/docs/drivers.md#xhyve-driver),
[VirtualBox](https://www.virtualbox.org/wiki/Downloads), or
[VMware Fusion](https://www.vmware.com/products/fusion).

* For Linux, install
[VirtualBox](https://www.virtualbox.org/wiki/Downloads) or
[KVM](http://www.linux-kvm.org/).

* For Windows, install
[VirtualBox](https://www.virtualbox.org/wiki/Downloads) or
[Hyper-V](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/quick_start/walkthrough_install).

## Install kubectl

* [Install kubectl](/docs/tasks/tools/install-kubectl/).

## Install Minikube

* Install Minikube according to the instructions for the
[latest release](https://github.com/kubernetes/minikube/releases).


# Minikube Quickstart

```

$ minikube start
Starting local Kubernetes v1.7.0 cluster...
Starting VM...
SSH-ing files into VM...
Setting up certs...
Starting cluster components...
Connecting to cluster...
Setting up kubeconfig...
Kubectl is now configured to use the cluster.


$ kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080
deployment "hello-minikube" created
$ kubectl expose deployment hello-minikube --type=NodePort
service "hello-minikube" exposed


# We have now launched an echoserver pod but we have to wait until the pod is up before curling/accessing it
# via the exposed service.
# To check whether the pod is up and running we can use the following:
$ kubectl get pod
NAME                              READY     STATUS              RESTARTS   AGE
hello-minikube-3383150820-vctvh   1/1       ContainerCreating   0          3s
# We can see that the pod is still being created from the ContainerCreating status
$ kubectl get pod
NAME                              READY     STATUS    RESTARTS   AGE
hello-minikube-3383150820-vctvh   1/1       Running   0          13s


# We can see that the pod is now Running and we will now be able to curl it:
$ curl $(minikube service hello-minikube --url)
CLIENT VALUES:
client_address=192.168.99.1
command=GET
real path=/
...


$ minikube stop
Stopping local Kubernetes cluster...
Machine stopped.
```