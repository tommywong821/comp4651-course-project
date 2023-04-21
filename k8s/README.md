kubectl apply -f
1. zookeeper
2. kafka
3. consumer
4. producer

update ip for each k8s deploy pods ip in both consumer and producer. then gradle build and build docker image again
spring.kafka.bootstrap-servers={IP}:9092

if docker-compose up:
spring.kafka.bootstrap-servers={IP}:9092 <- comment this one

minikube need use local image registry. minikube docker-env <- can get command

redirect localhost:8080 to k8s pod
kubectl port-forward {producer-pods-name} 8080:80