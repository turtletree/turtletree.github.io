---
title: kubernetes/secret
tags:
- kubernetes
categories:
date: 2022-10-17
lastMod: 2022-10-27
---
```
k create secret generic \
     mysecret --from-literal=DB_Host=mysql
                      --from-literal=DB_User=root
                      --from-literal=DB_Password=password
```

```
k create secret generic \
   mysecret --from-file=mysecret.properties
```



`k get secret mysecret -o yaml` will show the hashed values



## secret-data.yaml

apiVersion: v1

kind: Secret

metadata -- it's a dictionary

  + name: app-secret

  + labels: -- any kinda of k-v pairs where you see fit

    + app: myapp

data -- similar to ConfigMaps

  + DB_Host: mysql -> encoding with `echo -n 'mysql' | base64`

  + DB_User:

  + DB_Password:

  + 

## Inject to a [kubernetes/pod]({{< ref "/pages/kubernetes/pod" >}})

**apiVersion**: v1,

**kind**: Pod/ReplicaSet/Deployment/Service

**metadata** -- it's a dictionary

  + name: myapp-pod

  + labels: -- any kinda of k-v pairs where you see fit

    + app: myapp

**spec**: -- additional information about this obj, what's inside this obj

  + **containers:** -- list

    + - name: nginx-container 
image: nginx

    + ports:

    + - containerPort: 8080

    + envFrom:

      + - secretRef:
        name: mysecret
