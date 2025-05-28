# React Web App with Docker and Kubernetes (Minikube)

This project demonstrates how to:

- Create a React app using `create-react-app`
- Containerize it using Docker
- Push Docker images to Docker Hub
- Deploy and update the app on a Kubernetes cluster using Minikube with Docker driver

---

## 📁 Project Structure

kubernetes-react-webapp/
├── testapp/ # React app created via create-react-app
├── Dockerfile # Used to build Docker images
└── README.md


---

## 🚀 Steps I Followed

### 1. Create React App

```
npx create-react-app testapp
cd testapp
```
2. Start Minikube with Docker Driver
```
minikube start --driver=docker
```

🐳 Dockerfile (at root level)

```
FROM node

WORKDIR /myapp

COPY . .

RUN npm install

EXPOSE 3000

CMD ["npm", "start"]
```

📦 Build and Push Docker Image (v1, v2, v3...)
```
# Build Docker image
docker build -t akshaykashyap74/mykubernetestestapprepo:01 .

# Login to Docker Hub (if needed)
docker login

# Push to Docker Hub
docker push akshaykashyap74/mykubernetestestapprepo:01

```

☸️ Kubernetes Deployment (via Minikube)
Create Deployment
``` 
kubectl create deployment my-webapp --image=akshaykashyap74/mykubernetestestapprepo:01
```

Expose Deployment For Accessing App
```
kubectl expose deployment my-webapp --type=LoadBalancer --port=3000
```
Get URL to Access the App
```
minikube service my-webapp --url
```

🔄 Updating to a New Version
After pushing a new image version (e.g., :02 or :03), update your running app with:
```
kubectl set image deployment/my-webapp my-webapp=akshaykashyap74/mykubernetestestapprepo:02
```

✅ What I Learned
  1. How to create and containerize a React app
  2. How to use Docker and Docker Hub for image versioning
  3. How to deploy and expose apps using Kubernetes
  4. How to use Minikube with the Docker driver
  5. How to update a running Kubernetes deployment with a new image version

📸 Checkout The Screenshots Folder
