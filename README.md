# Kubernetes Voting App

A multi-container **voting application** deployed on Kubernetes using **Minikube**, showcasing container orchestration, microservice communication, and service exposure.

This project demonstrates how to use Kubernetes core concepts — Deployments, Services, Namespaces, and networking — to run a distributed application locally.

---

## 🗳️ Architecture Overview

The application consists of the following components:

- **Vote App** — A frontend service where users cast votes.  
- **Redis** — An in-memory data store acting as a queue.  
- **Worker** — A background service that reads votes from Redis and updates the database.  
- **Database (Postgres)** — Persistent storage for vote counts.  
- **Result App** — A frontend service that displays vote results.  

These are deployed as separate Kubernetes Deployments with appropriate Services to expose them. The Vote and Result apps are exposed externally via **NodePort**, while Redis and the database use **ClusterIP** for internal communication.  [oai_citation:1‡GitHub](https://github.com/dockersamples/example-voting-app?utm_source=chatgpt.com)

---

## 🚀 Getting Started

### Prerequisites

Make sure you have:

- [kubectl](https://kubernetes.io/docs/tasks/tools/) installed  
- Minikube installed and running

Start Minikube:

```bash
minikube start
```
## 📦 Deploy to Kubernetes
### 1.	Create a new namespace:
  
  ```
kubectl create namespace voting

```
### 2.	Apply all Kubernetes manifests:
   ```
 kubectl apply -f k8s/ --namespace=voting
```
   Replace k8s/ with the actual directory containing your YAML manifests.
### 3.	Verify the Pods and Services are running:
      ```
      kubectl get pods,svc -n voting
      ```

## 🌐 Access the App

Expose the Vote service externally:
```
minikube service vote --namespace=voting
```
Open the provided URL in your web browser to interact with the voting UI.
Similarly, you can access the results app:
```
minikube service result --namespace=voting
```
## 🛠️ What You’ll Learn

By deploying this project, you’ll get hands-on experience with:
	•	Kubernetes Deployments and ReplicaSets
	•	Service types (ClusterIP, NodePort)
	•	Inter-service communication via DNS
	•	Namespace isolation
	•	Running a multi-component microservices app

## 📁 Repository Structure
```
Kubernetics_Voting_App/
├── k8s/                     # Kubernetes deployment & service manifests
├── .gitignore
└── README.md
```
## 🧠 Tips & Notes
	•	The Worker pod does not require a Service because it does not receive traffic — it only communicates internally.
	•	Ensure your Kubernetes cluster has enough resources to schedule all pods.
	•	Minikube often exposes NodePorts via a URL when you use minikube service.
  
