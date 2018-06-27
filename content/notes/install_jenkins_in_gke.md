---
title: Run jenkins in GKE cluster
date: 2018-03-03
nopaging: true
noread: true
tags:
 - jenkins
 - kubernetes
 - gke
---


helm install --name jenkins stable/jenkins --set Master.Memory="640Mi" --set Cpu="100" --set Master.ServicePort=8080 --set Master.TLS.secretName=jenkins-tls --set Master.TLS.hosts="{jenkins.cluster.local}" --set Master.HostName=jenkins.bilor.us

apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: jenkins
spec:
  tls:
  - secretName: jenkins-tls
  backend:
    serviceName: jenkins
    servicePort: 8080

