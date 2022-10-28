---
title: kubernetes/serviceaccount
tags:
- kubernetes
categories:
date: 2022-10-17
lastMod: 2022-10-27
---
`k create serviceaccount dashboard-sa`

Upon creation, the SA generates a toke, then generates a Secret and stored the token in the Secret

`k describe secret dashboard-sa-token-kbbbm`

Each namespace has its own `default` sa



`k exec -it my-kubernetes-dashboard ls /var/run/serets/kubernetes.io/serviceaccount`

`k exec -it my-kubernetes-dashboard cat /var/run/serets/kubernetes.io/serviceaccount/token` to view the token eyJ...

decode the above token `jq -R 'split(".") | select(length > 0) | .[0],.[1] | @base64 | fromjson' <<< eyJ...`
