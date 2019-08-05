# pods
## default
```
NAMESPACE     NAME                                                         READY   STATUS    RESTARTS   AGE     IP            NODE           NOMINATED NODE
kube-system   event-exporter-v0.2.4-5f7d5d7dd4-whvbf                       2/2     Running   0          5m2s    10.40.0.5     default-pool   <none>
kube-system   fluentd-gcp-scaler-7b895cbc89-4j6n2                          1/1     Running   0          4m51s   10.40.0.7     default-pool   <none>
kube-system   fluentd-gcp-v3.2.0-mrnxp                                     2/2     Running   0          3m59s   10.146.0.44   default-pool   <none>
kube-system   heapster-v1.6.0-beta.1-6d6cf54646-9qb28                      3/3     Running   0          4m16s   10.40.0.10    default-pool   <none>
kube-system   kube-dns-autoscaler-76fcd5f658-z9jcr                         1/1     Running   0          4m41s   10.40.0.2     default-pool   <none>
kube-system   kube-dns-b46cc9485-2llrn                                     4/4     Running   0          5m3s    10.40.0.3     default-pool   <none>
kube-system   kube-proxy-default-pool                                      1/1     Running   0          4m49s   10.146.0.44   default-pool   <none>
kube-system   l7-default-backend-6f8697844f-vg89t                          1/1     Running   0          5m3s    10.40.0.6     default-pool   <none>
kube-system   metrics-server-v0.3.1-5b4d6d8d98-ls8wt                       2/2     Running   0          4m28s   10.40.0.9     default-pool   <none>
kube-system   prometheus-to-sd-lbhjf                                       1/1     Running   0          4m49s   10.146.0.44   default-pool   <none>
```

## medium
```
NAMESPACE     NAME                                                         READY   STATUS    RESTARTS   AGE   IP            NODE           NOMINATED NODE
kube-system   fluentd-gcp-v3.2.0-lrgq5                                     2/2     Running   0          56s   10.146.0.45   medium         <none>
kube-system   kube-dns-b46cc9485-gkbvd                                     4/4     Running   0          54s   10.40.1.2     medium         <none>
kube-system   kube-proxy-medium                                            1/1     Running   0          55s   10.146.0.45   medium         <none>
kube-system   prometheus-to-sd-mfkv2                                       1/1     Running   0          56s   10.146.0.45   medium         <none>
```

## large with taints
```
NAMESPACE     NAME                                                         READY   STATUS    RESTARTS   AGE    IP            NODE           NOMINATED NODE
kube-system   fluentd-gcp-v3.2.0-dgmkr                                     2/2     Running   0          34s    10.146.0.46   large          <none>
kube-system   kube-proxy-large                                             1/1     Running   0          33s    10.146.0.46   large          <none>
```

## Result
- kube-dns
- prometheus-to-sd
