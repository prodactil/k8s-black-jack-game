## 🃏 Kubernetes BlackJack Deployment
---

## 📘 Overview
I created a containerized terminal-based Blackjack game in Python and deployed it in a Kubernetes cluster using Deployment, Service, and Ingress. The project demonstrates skills in configuring YAML manifests, managing containerized applications, and enabling interactive terminal access in the browser via `ttyd`.

---

## 🧱 Project Structure
```bash
k8s-black-jack-game/  
├── terminal-game/
│   ├── blackjack.py
│   ├── art.py
│   ├── Dockerfile
│   └── requirements.txt
├── k8s-game/
│   ├── deployment.yaml
│   ├── ingress.yaml
│   └── service.yaml
└── README.md
```
---
## ⚙️ Tech Stack
•	Python 3.11 (CLI Game)  
•	Docker  
•	Kubernetes (Docker Desktop / Minikube / Kind)  
•	NGINX Ingress Controller  
•	ttyd (terminal to browser)  

---
## 🌐 Access
•	Via port-forward: http://localhost:7681  
•	Via Ingress: http://blackjack.local  
(Add 127.0.0.1 blackjack.local to /etc/hosts for local testing)  

---
### 📝 Notes
•	The game uses Python’s standard library only, no external dependencies.  
•	ttyd enables interactive terminal access in browser.  
•	Deployment manifest uses tty: true and stdin: true to ensure input works.  
•	All output is unbuffered using python3 -u for live terminal updates  
