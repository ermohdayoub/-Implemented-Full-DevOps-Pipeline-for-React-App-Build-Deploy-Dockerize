# -Implemented-Full-DevOps-Pipeline-for-React-App-Build-Deploy-Dockerize

This project showcases a complete DevOps pipeline implementation for deploying a React application on AWS. It includes setting up a secure Ubuntu server, building and deploying the application using PM2, and configuring an Nginx reverse proxy for production-level access.

A fully automated CI/CD pipeline was created using Jenkins, enabling automated code pull, build, deployment, and S3 artifact uploading. The application was also Dockerized and deployed using Docker Compose for container-based deployments. Security best practices were applied using UFW firewall rules.

This project demonstrates hands-on experience across DevOps tools such as AWS EC2, Linux, Jenkins, Docker, Nginx, PM2, S3, Git, and automation for real-world deployment workflows.
# Screenshots:
<img width="1919" height="895" alt="Screenshot 2025-11-24 202351" src="https://github.com/user-attachments/assets/235cb632-a65f-4f3e-977d-af4865e20cd2" />
<img width="842" height="232" alt="Screenshot 2025-11-24 185047" src="https://github.com/user-attachments/assets/6ecde389-3c73-4701-8165-5855b1dae990" />

<img width="702" height="53" alt="Screenshot 2025-11-24 185120" src="https://github.com/user-attachments/assets/fa782611-c3a3-47e7-a25a-ec22a28e5bbc" />

<img width="408" height="122" alt="Screenshot 2025-11-24 185334" src="https://github.com/user-attachments/assets/ef88763c-f614-4906-9d5c-5af42e913e20" />
<img width="861" height="200" alt="Screenshot 2025-11-24 185434" src="https://github.com/user-attachments/assets/66899ae9-e2e4-4d4a-b405-2b4d946d56bd" />
<img width="1415" height="363" alt="Screenshot 2025-11-24 185506" src="https://github.com/user-attachments/assets/116cfdc1-27ae-4c0f-a36a-a0de0aee2cc5" />
<img width="753" height="255" alt="Screenshot 2025-11-24 185706" src="https://github.com/user-attachments/assets/0ec02fbc-5f8e-4d9b-ab3a-c54dce85ccc6" />
<img width="909" height="45" alt="Screenshot 2025-11-24 185747" src="https://github.com/user-attachments/assets/76f6f77b-a9eb-44aa-9745-92a174bbddea" />
<img width="1299" height="285" alt="Screenshot 2025-11-24 192117" src="https://github.com/user-attachments/assets/4daed529-f683-40bf-9c13-0349a9e4acb7" />
<img width="1919" height="842" alt="Screenshot 2025-11-24 201949" src="https://github.com/user-attachments/assets/b3e1a0fd-d6a2-4565-9491-69c3c890247d" />
<img width="1919" height="1014" alt="Screenshot 2025-11-24 202107" src="https://github.com/user-attachments/assets/99bfed1e-9abd-45e3-a2ee-384947ff960a" />
<img width="1898" height="1012" alt="Screenshot 2025-11-24 202121" src="https://github.com/user-attachments/assets/945d4d51-5e2d-4d39-8357-b0d2aa8640b2" />
<img width="1919" height="1013" alt="Screenshot 2025-11-24 202146" src="https://github.com/user-attachments/assets/92f791eb-5faa-4a9d-9391-5e2f619203c7" />
<img width="1892" height="73" alt="Screenshot 2025-11-24 202010" src="https://github.com/user-attachments/assets/fa5d59cd-c7cb-474d-a17f-7ac02a2f01dd" />
<img width="1919" height="1011" alt="Screenshot 2025-11-24 201859" src="https://github.com/user-attachments/assets/7c91a698-1463-49a0-8617-f04df95d6740" />
<img width="1906" height="1008" alt="Screenshot 2025-11-24 201917" src="https://github.com/user-attachments/assets/3c05390d-c186-415c-be3f-f12e08e588af" />
<img width="1918" height="1010" alt="Screenshot 2025-11-24 200837" src="https://github.com/user-attachments/assets/9400db8f-dd99-4ca4-ad44-d59080bb8ae1" />
<img width="1915" height="887" alt="Screenshot 2025-11-24 200823" src="https://github.com/user-attachments/assets/8690b66a-8992-4cb3-b0a2-d94f6aa17d1f" />
<img width="1918" height="1012" alt="Screenshot 2025-11-24 201813" src="https://github.com/user-attachments/assets/0f0ba562-6c0f-4e7c-a398-f8fdb3c3d5fe" />
 
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



Author
Mohd Ayoub
AWS & DevOps Engineer 
LinkedIn: (https://www.linkedin.com/in/ermohdayoub)

⭐ If you like this project
Please star ⭐ this repository — it helps a lot!
