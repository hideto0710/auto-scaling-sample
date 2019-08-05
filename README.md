# autoscaling-sample

## 1. Using taints
```bash
PROJECT=dev-datad-kubeadm-1729623135
ZONE=asia-northeast1-a

gcloud container clusters create autoscale-sample \
    --project ${PROJECT} \
    --zone ${ZONE} \
    --machine-type n1-standard-1 \
    --num-nodes 1 \
    --enable-autoscaling \
    --max-nodes 2 \
    --min-nodes 0 \
    --enable-autoupgrade \
    --enable-autorepair \
    --no-enable-basic-auth \
    --metadata disable-legacy-endpoints=true

gcloud container node-pools create medium \
    --project ${PROJECT} \
    --zone ${ZONE} \
    --machine-type n1-standard-4 \
    --cluster autoscale-sample \
    --num-nodes 1 \
    --enable-autoscaling \
    --max-nodes 2 \
    --min-nodes 0 \
    --enable-autoupgrade \
    --enable-autorepair \
    --metadata disable-legacy-endpoints=true \
    --node-taints=app=job:NoSchedule

gcloud container node-pools create large \
    --project ${PROJECT} \
    --zone ${ZONE} \
    --machine-type n1-standard-8 \
    --cluster autoscale-sample \
    --num-nodes 1 \
    --enable-autoscaling \
    --max-nodes 2 \
    --min-nodes 0 \
    --enable-autoupgrade \
    --enable-autorepair \
    --metadata disable-legacy-endpoints=true \
    --node-taints=app=job:NoSchedule
```

```bash
kubectl apply -f manifests/small.yaml
kubectl wait --for=condition=complete --timeout=10m job/small-job
# scaling default-pool

kubectl apply -f manifests/medium.yaml
kubectl wait --for=condition=complete --timeout=10m job/medium-job
# scaling medium-pool

kubectl apply -f manifests/large.yaml
kubectl wait --for=condition=complete --timeout=10m job/large-job
# scaling large-pool
```
