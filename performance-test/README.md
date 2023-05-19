# Performance Test

## Obejctive

Find out the performance of Kafka with multiple replications deployed in Kubernetes.

## Testing Environment

OS: Windows 10, CPU: AMD Ryzen 5 5600X (6 Core, 12 Thread, 3.7Ghz), RAM: 32GB (3200MHz), Kubernetes: v1.25.4, k3d: v5.5.1, Docker Desktop: v4.18.0

## Kafka Setup

1. Install [Docker Desktop](https://docs.docker.com/desktop/install/mac-install/), [Kubernetes](https://kubernetes.io/docs/setup/), [k3d](https://k3d.io/v5.5.1/#installation)

2. Open powershell and create multi replications (3 in this example) of kafka with this command.
   `k3d cluster create kube-cluster --agents 3 --k3s-node-label topology.kubernetes.io/zone=zone-a@agent:0 --k3s-node-label topology.kubernetes.io/zone=zone-b@agent:1  --k3s-node-label topology.kubernetes.io/zone=zone-c@agent:2`

3. Remeber to append `--k3s-node-label topology.kubernetes.io/zone=zone-{name}@agent:{index}` according to the replications number at the end
4. Update the `- name: REPLICAS value: '3'` in env section of kafka.yaml
5. use k8s command to create the kafka service for loadbalancing the multi replication kafka `kubectl apply -f kafka.yaml`
6. User `kubectl get pods` to make sure all the pods are running
7. Use `kubectl describe service kafka-svc` to get all the ip of the kafka pod
8. Update the ip in `--bootstrap-server ` and `--producer-props bootstrap.servers=` in kafka-consumer-script.txt and kafka-producer-script.txt
9. Create a new Kafka client and control it using bash to performance test `kubectl run kafka-client --rm -ti --image bitnami/kafka:3.1.0 -- bash`
10. Navigate to the scripts provide by Apache `cd /opt/bitnami/kafka/bin`
11. Copy and Paste either the script in kafka-consumer-script.txt or kafka-producer-script.txt to execute the performance test
