---
layout: post
title: Kubernetes CLI Logs
description: "Logs the basic commands for interacting with Minikube and Kubernetes"
headline:
imagefeature:
modified: 2017-05-12
category: articles
tags: [kubernetes]
published: true
comments: true
share: true
---

# Install kubectl

* http://kubernetes.io/docs/tasks/tools/install-kubectl

# Setup minikube

Download the latest release:

http://github.com/kubernetes/minikube/releases

Minikube v0.19.0 can communicate with hyperkit via its xhyve driver which needs to be installed:

    $ brew install docker-machine-driver-xhyve
    $ sudo chown root:wheel $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve
    $ sudo chmod u+s $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve

Then start minikube with the appropriate driver switch:

    $ minikube start --vm-driver=xhyve

* [Reference](https://github.com/zchee/docker-machine-driver-xhyve#install)

# Interacting with the cluster

Get cluster info:

    $ kubectl cluster-info

Deploy an app from a docker image:

    $ kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080

Get deployments

    $ kubectl get deployments

Get pod status:

    $ kubectl get pod

Create a service to expose the pod in the external network

    $ kubectl expose deployment hello-minikube --type=NodePort

[Pod overview](https://kubernetes.io/docs/tutorials/kubernetes-basics/explore-intro/)

Interacting with the service:

    $ curl $(minikube service hello-minikube --url)

[Reference](https://kubernetes.io/docs/getting-started-guides/minikube/)

Troubleshooting with kubectl

* `kubectl get` - list resources
* `kubectl describe` - show detailed information about a resource
* `kubectl logs` - print the logs from a container in a pod
* `kubectl exec` - execute a command on a container in a pod

Example:

    $ kubectl describe service SERVICE_NAME

Streaming logs

    $ kubectl log -f POD_NAME

# Scaling

TODO https://kubernetes.io/docs/tutorials/kubernetes-basics/scale-intro/


