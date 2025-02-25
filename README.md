# ci-cd-local

🚀 Real-World DevOps Projects Without Cloud Providers
Since you want DevOps projects without using AWS, Azure, or any cloud provider, we'll focus on local environments using:
✅ GitHub Actions for CI/CD
✅ Docker & Docker Compose for containerization
✅ Terraform for local VMs (using VirtualBox & Vagrant)
✅ Kubernetes with Minikube

🔥 Project 1: CI/CD Pipeline with GitHub Actions & Docker (Local Deployment)
🎯 Objective:
Automate testing, building, and deploying a Node.js app using GitHub Actions.
Deploy the containerized app locally using Docker Compose.
🛠️ Tools Used:
GitHub Actions (CI/CD)
Docker & Docker Compose (Containerization)
NGINX (Reverse Proxy)

🔹 Step 1: Set Up a Local Git Repository
Create a GitHub repository: ci-cd-local
Clone it:
git clone https://github.com/your-username/ci-cd-local.git
cd ci-cd-local



🔹 Step 2: Write a Simple Node.js App
📌 Create server.js
const express = require("express");
const app = express();
app.get("/", (req, res) => res.send("Hello from Local CI/CD! 🚀"));
app.listen(3000, () => console.log("Server running on port 3000"));

📌 Create Dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["node", "server.js"]
EXPOSE 3000

📌 Create docker-compose.yml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"


🔹 Step 3: Configure GitHub Actions for CI/CD
📌 Create .github/workflows/main.yml
name: CI/CD Pipeline
on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set Up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: "18"

      - name: Install Dependencies
        run: npm install

      - name: Build Docker Image
        run: docker build -t my-local-app .

      - name: Run Tests
        run: npm test

📌 Push the Code to GitHub
git add .
git commit -m "Initial commit"
git push origin main

✅ Now, every push triggers GitHub Actions to build & test the app!

🔹 Step 4: Deploy Locally with Docker Compose
Run this command to deploy locally:
docker-compose up -d

🔹 Open http://localhost:3000 → See the app running! 🎉
