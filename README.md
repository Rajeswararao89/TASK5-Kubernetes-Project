# 🐳 Kubernetes Project with Minikube - Task 5

This is my Task 5 from the DevOps Internship program where I had to deploy and manage an application using **Kubernetes** locally with **Minikube**.  
I decided to go a bit beyond the basic requirements and implement extra Kubernetes features like **ConfigMaps, Secrets, scaling, and rolling updates** to make the project more realistic and closer to production scenarios.

---

## 📌 Objective
- Set up a local Kubernetes cluster with Minikube (Docker driver).
- Deploy a simple Nginx-based web application.
- Expose it through a NodePort service.
- Manage configuration using ConfigMap and Secret.
- Demonstrate scaling and rolling updates.

---

## 🛠 Tools & Technologies
- **Kubernetes** (v1.33.1 in my setup)
- **Minikube** (Docker driver)
- **kubectl**
- **Docker**
- **Nginx** container image
- YAML manifests

---

## 📂 Project Structure
k8s-minikube-project/
│── manifests/
│ ├── deployment.yaml # Deployment definition
│ ├── service.yaml # NodePort service
│ ├── configmap.yaml # App configuration
│ ├── secret.yaml # Sensitive data
│── README.md
│── screenshots/ # Proof of implementation


---

## 🚀 Steps I Followed

### 1️⃣ Started Minikube
I used the Docker driver to keep things lightweight and avoid extra VMs.
```bash
minikube start --driver=docker
kubectl get nodes
This gave me a single-node Kubernetes cluster ready to use.

2️⃣ Created ConfigMap & Secret
To make the deployment more realistic, I created a ConfigMap for non-sensitive configs and a Secret for sensitive data.
kubectl apply -f manifests/configmap.yaml
kubectl apply -f manifests/secret.yaml

3️⃣ Deployed the Application
I wrote a Deployment manifest for an Nginx container, linked it to the ConfigMap & Secret, and exposed it using a NodePort service.
kubectl apply -f manifests/deployment.yaml
kubectl apply -f manifests/service.yaml
kubectl get pods
kubectl get svc

4️⃣ Accessed the Application
Since I was running in Vagrant, I used:
minikube service my-app-service --url
This gave me a working Nginx welcome page.
which is http://192.168.49.2:30414/

5️⃣ Scaled the Application
To test Kubernetes scaling, I increased replicas from 2 to 3:
kubectl scale deployment my-app --replicas=3
kubectl get pods

6️⃣ Performed Rolling Updates
I updated the Nginx version twice to simulate production updates:
kubectl set image deployment/my-app my-app-container=nginx:1.27-alpine
kubectl rollout status deployment/my-app

Later, I did another update:
kubectl set image deployment/my-app my-app-container=nginx:1.26-alpine
kubectl rollout status deployment/my-app

📸 Screenshots
I took screenshots of:
Minikube cluster start & kubectl get nodes
Pods running
Services with NodePort
Application output (Nginx welcome page)
Scaling in action
Rolling update progress

📚 Key Learnings
How to set up and run a Kubernetes cluster locally with Minikube.
The difference between Pods, Deployments, and Services.
How to manage environment configuration using ConfigMaps and Secrets.
Scaling deployments and performing rolling updates without downtime.
The importance of keeping manifests in a safe location outside the cluster for reusability.

## 📸 Screenshots

![Cluster Start](screenshots/Screenshot%20(120).png)  
![Pods Running](screenshots/Screenshot%20(121).png)  
![Service Details](screenshots/Screenshot%20(122).png)  
![Nginx Page](screenshots/Screenshot%20(123).png)  
![Scaling](screenshots/Screenshot%20(124).png)  





