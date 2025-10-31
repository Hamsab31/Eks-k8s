🌐 Nginx Deployment on AWS EKS
This project sets up an AWS EKS (Elastic Kubernetes Service) cluster and deploys an Nginx web server using Kubernetes.
⚙️ Tech Stack
☁️ AWS EKS – Kubernetes cluster on AWS
🧩 eksctl – Creates and manages the cluster
🔧 kubectl – Manages Kubernetes resources
🌍 Nginx – Web server
🚀 Steps to Deploy
🏗️ Create Cluster
eksctl create cluster --name nginx-cluster --region ap-south-1
🔗 Connect to Cluster
aws eks update-kubeconfig --name nginx-cluster --region ap-south-1
📦 Deploy Nginx
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
🌍 Get Access URL
kubectl get svc
Copy the EXTERNAL-IP / LoadBalancer URL and open it in your browser.
📂 Files
File	Purpose
deployment.yaml	Defines Nginx pods and replicas
service.yaml	Exposes the app to the internet
README.md	Project documentation

🧾 Sample YAML Files
🟢 deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
        
🟣 service.yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      
✅ Output
🎉 Nginx application deployed successfully on AWS EKS!
Open your browser with the LoadBalancer URL to see the Nginx welcome page.
