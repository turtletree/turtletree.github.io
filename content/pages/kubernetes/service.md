---
tags:
- kubernetes
title: kubernetes/service
categories:
date: 2022-10-26
lastMod: 2022-10-27
---
NodePort

  + Range: 30000 - 32767

ClusterIP

  + 

LoadBalancer





apiVersion: v1

kind: Service

metadata:

  + name: myapp-service

spec:

  + type: NodePort/ClusterIP (default)

  + ports:

    + -targetPort: 80 --- if not specify, gonna be the same as port
port: 80 --- only required field
nodePort: 30008 --- any number in the valid range, if not specify, it's going to be random

  + selector:

    + app: myapp

    + type: front-end



`k create -f service-def.yaml`

Access with `curl http://192.168.1.2:30008`
