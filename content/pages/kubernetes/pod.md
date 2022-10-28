---
title: kubernetes/pod
tags:
- kubernetes
categories:
date: 2022-10-17
lastMod: 2022-10-27
---
**apiVersion**: v1,

**kind**: Pod/ReplicaSet/Deployment/Service

**metadata** -- it's a dictionary

  + name: myapp-pod

  + labels: -- any kinda of k-v pairs where you see fit

    + app: myapp

**spec**: -- additional information about this obj, what's inside this obj

  + securityContext:

    + runAsUser: 1000 -- userId to run the pod

  + serviceAccountName: dashboard-sa

  + **containers:** -- list

    + - name: nginx-container 
image: nginx

    + ports:
-containerPort: 8080

    + envFrom:

      + - secretRef:
        name: mysecret

    + securityContext: -- specify under container instead of pod

      + runAsUser: 1000

      + capabilities: -- capabilities are only supported at the container level and not at the POD level

        + add: ["MAC_ADMIN]



`k get pods --selector env=dev` get the pods that has the label `env` set to `dev`

`k get all --selector env=prod --selector bu=finance --selector tier=frontend`
