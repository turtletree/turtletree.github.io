---
tags:
- kubernetes
title: kubernetes
categories:
date: 2022-10-13
lastMod: 2022-10-27
---
# Component Structures

Cluster

  + Node

    + Pod: single instance of an application

      + Container

    + Pod2:

      + Container

    + More pods to scale up

  + Node2

    + Pod: can have multiple containers but mostly different types, share same storage, fate, etc. But it is a RARE situation.

      + Container A

      + Container helper

# Kubectl Cheat Sheet

`k run nginx --image nginx --n devNamespace` (downloaded from Docker hub, public registry)

`kubectl run nginx --image=nginx --dry-run=client -o yaml`

`k get pods` list all pods available in the current namespace

`k get pods --all-namespaces`

`k describe pod myapp-pod` more info

`--dry-run` : By default as soon as the command is run, the resource will be created. If you simply want to test your command , use the  `--dry-run=client`  option. This will not create the resource, instead, tell you whether the resource can be created and if your command is right.


`kubectl get pod <pod-name> -o yaml > pod-definition.yaml` extract the definition to a file

`kubectl edit pod <pod-name>` to edit pod properties

Scale up

  + `k replace -f replicaset-def.yml` after updating the yml

  + `k scale --replicas=6 -f replicaset-def.yml` but this won't update the yml file

  + `k scale --replicas=6 replicaset myapp-replicaset`

`k delete replicaset myapp-replicaset` --> also deletes all underlying PODs

`k replace -f replicaset-def.yml` update

`k create -f rc-definition.yml`

`k get replicationcontroller`

`k get all`

`-o json` Output a JSON formatted API object.

`-o name` Print only the resource name and nothing else.

`-o wide` Output in the plain-text format with any additional information.

`-o yaml` Output a YAML formatted API object.

`k get pods --namespace=somenamespace`

`kubectl create deployment --image=nginx nginx`

`kubectl create deployment --image=nginx nginx --dry-run -o yaml`

`k rollout status deployment/myapp-deployment`

`k rollout history deployment/myapp-deployment`

# YAML

## Pod as an example

top/root level fields -- required

  + **apiVersion**: v1,

  + **kind**: Pod/ReplicaSet/Deployment/Service

  + **metadata** -- it's a dictionary

    + name: myapp-pod

    + labels: -- any kinda of k-v pairs where you see fit

      + app: myapp

  + **spec**: -- additional information about this obj, what's inside this obj

    + **containers:** -- list

      + - name: nginx-container
  image: nginx

      + command --> corresponding to Docker ENTRYPOINT

      + args --> corresponding to Docker CMD



## Replica Set

### Replication Controller vs Replica Set

  + RC: can scale up to different nodes, older term

  + RS: newer term



### YAML

apiVersion: v1/ **apps/v1**

kind: ReplicationController/**ReplicaSet**

metadata:

  + name:

  + labels:

spec:

  + template: -- for the pod, so can move the above yaml directly here. They're nested now.

    + **metadata** -- it's a dictionary

      + name: myapp-pod

      + labels: -- any kinda of k-v pairs where you see fit

        + app: myapp

        + type: frontend

    + **spec**: -- additional information about this obj, what's inside this obj

      + **containers:** -- list

        + - name: nginx-container
  image: nginx

  + replicas: 3

  + **selector**(required): (major differences between rc and rs)

    + **matchLabels**:

      + type: frontend



## Deployment

a deployment can automatically create a ReplicaSet



### YAML

apiVersion: apps/v1

kind: Deployment

metadata:

  + name:

  + labels:

spec:

  + template: -- for the pod, so can move the above yaml directly here. They're nested now.

    + **metadata** -- it's a dictionary

      + name: myapp-pod

      + labels: -- any kinda of k-v pairs where you see fit

        + app: myapp

        + type: frontend

    + **spec**: -- additional information about this obj, what's inside this obj

      + **containers:** -- list

        + - name: nginx-container
  image: nginx

  + replicas: 3

  + **selector**(required): (major differences between rc and rs)

    + **matchLabels**:

      + type: frontend



## Namespace

apiVersion: v1

kind: Namespace

metadata:

  + name:

  + labels:

`k create -f namespace-dev.yml`

`k config set-context $(kubectl config current-context) --namespace=dev` switch to dev env

`k get pods --all-namespaces`

To access pods in another namespace: `redis-db.dev.svc.cluster.local` --> `serviceName.namespace.type.cluster.local`



## ConfigMap

apiVersion: v1

kind: ConfigMp

metadata:

  + name: app-config

**data**:

  + key: value

  + anotherKey: another value

### ConfigMap in Pods

**apiVersion**: v1

**kind**: Pod

**metadata** -- it's a dictionary

  + name: myapp-pod

  + labels: -- any kinda of k-v pairs where you see fit

    + app: myapp

**spec**: -- additional information about this obj, what's inside this obj

  + **containers:** -- list

```
- name: simple-webapp-color 
  image: simple-webapp-color
  ports:
    - containerPort: 8080
      envFrom:
   		- configMapRef:
			name: app-config <-----injection of the configMap
```

    + 







{{< logseq/orgNOTE >}}Up-to-date valid coupon codes for the CKAD exam: https://devopscube.com/kubernetes-certification-coupon/
{{< / logseq/orgNOTE >}}






