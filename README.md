# Kubernetes Deployment with Auto-Scaling & Monitoring

## 📌 Overview

This repository contains the Kubernetes deployment setup for a containerized web service, including:

- Dockerized web application (Flask/FastAPI/Node.js)
- Kubernetes (Minikube/K3s) deployment
- Auto-scaling with Horizontal Pod Autoscaler (HPA)
- Load balancing for high availability
- Observability using Prometheus, Grafana
- Resiliency measures for fault tolerance

## 🚀 Technologies Used

- Docker: Containerizes the application
- Kubernetes (Minikube/K3s): Orchestrates containers
- Helm: Manages dependencies
- Prometheus & Grafana: Monitors system metrics

## 🛠️ Setup & Installation

1️⃣ Prerequisites
 - Install Docker, Minikube/K3s, kubectl, and Helm
 - Ensure Kubernetes cluster is running
 - Clone this repository
> git clone https://github.com/Shreyank-S/Scalable-Web-Service.git <br /> 
> cd Scalable-Web-Service

2️⃣ Build & Deploy the Web Service
> eval $(minikube docker-env)  # Use Minikube’s Docker daemon <br /> 
> docker build -t flask-app . <br /> 
> kubectl apply -f deployment.yaml  # Deploy to Kubernetes <br /> 
> kubectl expose deployment flask-app --type=LoadBalancer --port=80 --target-port=5001 <br /> 

3️⃣ Enable Auto-Scaling
> kubectl autoscale deployment flask-app --cpu-percent=50 --min=1 --max=5 <br /> 

4️⃣ Install Monitoring & Logging Stack
> helm repo add prometheus-community https://prometheus-community.github.io/helm-charts <br />  
> helm install prometheus prometheus-community/kube-prometheus-stack <br /> 
> helm install elk-stack elastic/elasticsearch kibana logstash <br />  

## ⚙️ Troubleshooting

🛑 Pod in ImagePullBackOff State?
- Use Minikube’s Docker daemon and rebuild:

> eval $(minikube docker-env) <br /> 
> docker build -t flask-app . <br /> 
> kubectl delete deployment flask-app <br /> 
> kubectl apply -f deployment.yaml <br /> 

🛑 Helm Not Found?
> brew install helm <br /> 
> export PATH=/opt/homebrew/bin:$PATH <br /> 


##  Monitoring & Logs

- Grafana Dashboard: http://<minikube-ip>:3000
- Kibana Logs: http://<minikube-ip>:5601
- Prometheus Metrics: http://<minikube-ip>:9090

## 📄 File Structure

📁 k8s-deployment  
├── deployment.yaml        # Kubernetes deployment config  
├── service.yaml           # Kubernetes service config  
├── Dockerfile             # Containerization  
├── README.md              # Project documentation  
└── helm/                  # Helm charts for monitoring & logging  

## 🤝 Contribution Guidelines

- Fork the repository
- Create a new branch (feature-branch)
- Commit your changes
- Push to GitHub and create a PR

