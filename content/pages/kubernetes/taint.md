---
title: kubernetes/taint
tags:
- kubernetes
categories:
date: 2022-10-19
lastMod: 2022-10-27
---
Taint -> Node

Tolerant -> Pod

Defines if we are allowed to place a certain pod to a certain node

It tells the NODE if he should accept a pod, it doesn't not guarantee that typed of pods will definitely end up in this node





### Taint a Node

`k taint nodes node-name key-value:taint-effect`

  + **taint-effect** defines what happens to the PODs that DO NOT TOLERATE this taint

    + NoSchedule: won't place this pod on this node

    + PreferNoScheule: will try not to place but no guarantee

    + NoExecute: won't place this pod, and evict any similar existing pods already on the node that doesn't tolerate



### Give PODs Tolerations

spec: -- additional information about this obj, what's inside this obj

  + containers: -- list

    + - name: nginx-container 
image: nginx

    + ports:
-containerPort: 8080

  + **tolerations**:

    + - key: "app"
operator: "Equal"

    + value: "blue"

    + effect: "NoSchedule"
