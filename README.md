
### Minikube setup ####

## prerequisites ##
Craete a VM with any OS like i'm taking ubuntu
  2 CPUs or more
  2GB of free memory
  20GB of free disk space
  Install docker (container runtime)
    https://docs.docker.com/engine/install/ubuntu/

Install minikube on VM
  https://minikube.sigs.k8s.io/docs/start/

Create a jar file 

Before that you have to install the java and maven

sudo apt update

apt install default-jre

Maven Installation

sudo apt install maven


Then clone the git repository

cd systemsenginer
mvn clean pacakge 
docker build -t ashokcgdocker/javaapp:RC1 .

before push please do signup to dockerhub and then docker login to dockerhub

docker login -u <username> -p <password>

docker push ashokcgdocker/javaapp:RC1


in form of docker images and Push into docker hub then update the image into javawebapp-hpa-deployment.yaml file under spec image section 

Then execute the manifest file to deploy an application into a pods 

kubectl apply -f javawebapp-hpa-deployment.yaml

One you have deployed hpa deployment file please check the pods and hpa is running

kubectl get pods,hpa

and then check you can able to see the pod metrics by using below command

kubectl top pods

if not, please install the matrics server on minikube cluster 
kubectl apply -f metrics-server.yaml

and check metrics server pod is running or not if running check the logs as well

 kubectl logs -f metrics-server-8ff8f88c6-hlmv7 -n kube-system

 
Now you can see metrics of pod kubectl top pods and kubectl top hpa 

Once all things as been up and running. Access the application outside use this cmd and copy the url and execute in browser
  
Note: Please open the nodeport into security groups under inbound rules
  
  
minikube service hpaclusterservice  --url
  
  
<img width="580" alt="Screenshot 2022-11-30 at 7 48 23 PM" src="https://user-images.githubusercontent.com/47560900/204819631-042e2454-1273-4f20-a5a0-1558b36b4769.png">

  
  
  
![Javahomepage](https://user-images.githubusercontent.com/47560900/204814593-60d9ab54-6e1b-4970-a189-71aea0046fe3.jpeg)

  Before that please open 2 tabs. In one tab execute watch kubectl top nodes, in another tab watch kubectl get hpa

  And finally monitor the tabs you can see the cpu getting increated on watch pod section and you can also see new pods getting created 
  
  
  <img width="1440" alt="Screenshot 2022-11-30 at 2 47 31 PM" src="https://user-images.githubusercontent.com/47560900/204813350-898f6b0b-2782-471a-8aa8-a2937d729723.png">

  

