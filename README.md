# -Implemented-Full-DevOps-Pipeline-for-React-App-Build-Deploy-Dockerize

This project demonstrates a complete end-to-end DevOps workflow for a React application, including server setup, CI/CD automation, deployment, reverse proxy configuration, security hardening, and Dockerization.
Project Overview

The objective of this project is to automate the build and deployment process of a React application using modern DevOps tools. The pipeline includes:
 - Linux user setup
 - Application build & deployment
 - PM2 process management
 - Nginx reverse proxy
 - Jenkins CI/CD pipeline
 - Dockerization
 - UFW firewall configuration
 - S3 artifact upload

Technologies Used
 - AWS EC2 (Ubuntu)
 - Linux / Bash
 - Node.js & npm
 - React
 - PM2
 - Nginx
 - Jenkins
 - Docker & Docker Compose
 - UFW Firewall
 - AWS S3
 - Git & GitHub

Steps Implemented
1. Linux Setup & User Management
sudo adduser DevOps
sudo usermod -aG sudo DevOps
sudo apt update && sudo apt upgrade -y

2. Clone & Build React Application
 - sudo apt install nodejs npm -y
 - sudo mkdir -p /opt/checkout/chat-app
 - cd /opt/checkout
 - sudo git clone https://github.com/riyanuddin17/DevOps-Challenge.git chat-app
 - cd chat-app
 - npm install
 - npm run build


Move build output:
 - sudo mkdir -p /opt/deployment/react
 - sudo mv dist /opt/deployment/react/

3. Deploy React App Using PM2
 - sudo npm install pm2 -g
 - pm2 serve /opt/deployment/react/dist 3000 --spa
 - pm2 save
 - pm2 startup

4. Configure Nginx Reverse Proxy
 - Create config file:
 - sudo nano /etc/nginx/sites-available/react


Add:

server {
    listen 80;

    location / {
        proxy_pass http://localhost:3000;
    }
}


Enable:

sudo ln -s /etc/nginx/sites-available/react /etc/nginx/sites-enabled/
sudo systemctl restart nginx

5. Configure UFW Firewall
 - sudo ufw allow 80
 - sudo ufw allow 443
 - sudo ufw allow 22
 - sudo ufw allow 3000
 - sudo ufw enable


CI/CD With Jenkins
Jenkins Installation
 - sudo apt update
 - sudo apt install openjdk-11-jdk -y
 - wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
 - echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
 - sudo apt update
 - sudo apt install jenkins -y
 - sudo systemctl start jenkins


Access Jenkins:
- http://<EC2-IP>:8080

Jenkins Pipeline Workflow
Pipeline performs:

Stop PM2 service
 - Pull latest code
 - Build React app
 - Copy dist folder
 - Restart PM2
 - Upload artifacts to S3

Jenkinsfile
pipeline {
    agent any

    stages {
        stage('Stop Deployment') {
            steps {
                sh 'pm2 stop all || true'
            }
        }
        stage('Pull Code') {
            steps {
                sh 'cd /opt/checkout/chat-app && git pull'
            }
        }
        stage('Build React') {
            steps {
                sh 'cd /opt/checkout/chat-app && npm install && npm run build'
            }
        }
        stage('Deploy') {
            steps {
                sh 'sudo rm -rf /opt/deployment/react/dist'
                sh 'sudo mv /opt/checkout/chat-app/dist /opt/deployment/react/'
                sh 'pm2 restart all'
            }
        }
        stage('Upload to S3') {
            steps {
                sh 'aws s3 cp /opt/deployment/react/dist s3://YOUR_BUCKET_NAME/ --recursive'
            }
        }
    }
}

Dockerization
Dockerfile
 - FROM nginx:alpine
 - COPY dist /usr/share/nginx/html
 - EXPOSE 3000

docker-compose.yml
version: "3"

services:
  react-app:
    build: .
    ports:
      - "3000:80"


Run:

 - docker-compose up --build -d
 - Project Deliverables
 - React app deployed using PM2
 - Reverse proxy via Nginx
 - Jenkins CI/CD pipeline
 - S3 artifact upload
 - Dockerized application running on port 3000
 - Firewall rules configured using UFW

screenshots:


Author
Mohd Ayoub

