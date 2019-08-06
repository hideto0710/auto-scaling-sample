# autoscaling-sample

## Setup
```bash
PROJECT=<YOUR PROJECT ID>
ZONE=asia-northeast1-a

gcloud container clusters create autoscale-sample \
    --project ${PROJECT} \
    --zone ${ZONE} \
    --machine-type n1-standard-1 \
    --num-nodes 1 \
    --enable-autoscaling \
    --max-nodes 2 \
    --min-nodes 0
```

### Option 1: Using taints
prevent to schedule `kube-dns` on worker node by adding `taints`

```bash
gcloud container node-pools create medium-pool \
    --project ${PROJECT} \
    --zone ${ZONE} \
    --machine-type n1-standard-4 \
    --cluster autoscale-sample \
    --num-nodes 1 \
    --enable-autoscaling \
    --max-nodes 2 \
    --min-nodes 0 \
    --node-taints=app=job:NoSchedule

gcloud container node-pools create large-pool \
    --project ${PROJECT} \
    --zone ${ZONE} \
    --machine-type n1-standard-8 \
    --cluster autoscale-sample \
    --num-nodes 1 \
    --enable-autoscaling \
    --max-nodes 2 \
    --min-nodes 0 \
    --node-taints=app=job:NoSchedule
```

### Option 2: Using PDB
enable rescheduling `kube-dns` on worker node by adding `pdb`

```bash
kubectl apply -f manifests/pdb.yaml
```

```bash
gcloud container node-pools create medium-pool \
    --project ${PROJECT} \
    --zone ${ZONE} \
    --machine-type n1-standard-4 \
    --cluster autoscale-sample \
    --num-nodes 1 \
    --enable-autoscaling \
    --max-nodes 2 \
    --min-nodes 0

gcloud container node-pools create large-pool \
    --project ${PROJECT} \
    --zone ${ZONE} \
    --machine-type n1-standard-8 \
    --cluster autoscale-sample \
    --num-nodes 1 \
    --enable-autoscaling \
    --max-nodes 2 \
    --min-nodes 0
```

## run jobs
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

## clean up
```bash
gcloud container clusters delete autoscale-sample \
    --project ${PROJECT} \
    --zone ${ZONE}
```
