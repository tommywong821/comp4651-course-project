First cd to k8s folder:
kubectl apply -f
1. zookeeper + tab
2. kafka 
kubectl.exe describe pods {kafak pod} to find the pod ip 
e.g.{kubectl.exe describe pods kafka-deployment-7985656cd5-hbp9g}
e.g {
    Name:             kafka-deployment-7985656cd5-hbp9g
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Mon, 08 May 2023 18:52:58 +0800
Labels:           app=kafka
                  pod-template-hash=7985656cd5
Annotations:      <none>
Status:           Running
IP:               10.244.0.14
}

Do following for 3 and 4:
1. update ip for each k8s deploy pods ip in both consumer and producer. 
spring.kafka.bootstrap-servers={IP}:9092
2. gradle build for every file change
./gradlew build
3. minikube need use local image registry.  (type once as long as the terminal not close)
minikube docker-env <- can get command
e.g.{
     & minikube -p minikube docker-env --shell powershell | Invoke-Expression
}
4.  (type once as long as the terminal not close)
& minikube -p minikube docker-env --shell powershell | Invoke-Expression
5. cd to producer/consumer folder and build docker image 
docker build -t {image_name e.g: comp4651/producer} .
to check image in local:
minikube image ls
6. cd to k8s folder deploy to k8s
kubectl apply/delete -f producer.yaml
to check:
kubectl.exe get pods
to check log:
e.g. 
{kubectl.exe logs -f producer-deployment-7bcdc5448c-dv8ht}
7. do same thing to consumer 

3. consumer
4. producer
"kubectl get pods" to see


final:
5. get pod first and redirect localhost:8080 to k8s pod
kubectl get pods
kubectl port-forward {producer-pods-name} 8080:8080

6. keep this terminal and open two new terminal for consumer and producer
kubectl get pods
kubectl.exe logs -f {producer-deployment-7bcdc5448c-dv8ht}

7. use thunder client
new request
http://localhost:8080/order
body -> json
{
  "item": "orange",
  "amount": 1
}
send

8. check log
should see producer produce item with amount
and see consumer sonsume item with amount

End:
1. kubectl.exe get deployment
2. kubectl.exe delete --all deployment