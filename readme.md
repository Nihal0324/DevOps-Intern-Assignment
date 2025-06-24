This project demonstrates a basic reverse proxy setup using NGINX and Docker Compose. It includes two backend services and an NGINX container to route traffic to them via path-based routing.


1. Clone the Repository
  git clone https://github.com/your-username/devops-nginx-reverse-proxy.git
  cd devops-nginx-reverse-proxy


2. Build and Start All Containers
    docker-compose up --build -d


4. Access the Services
   
     Open your browser and visit:

     Service 1:
     http://<your-ec2-ip>:8080/service1/

     Service 2:
     http://<your-ec2-ip>:8080/service2/


 How Routing Works
All HTTP requests hit NGINX on port 8080

NGINX is configured to route:

/service1/ → Docker container service1 on port 8001

/service2/ → Docker container service2 on port 8002

Reverse proxy is configured in nginx/default.conf


For Healthcheck we will add below part in our composefile

healthcheck:

  test: ["CMD", "curl", "-f", "http://localhost:8001"]
  
  interval: 10s
  
  timeout: 5s
  
  retries: 3
  

This health check runs `curl` inside the container every 10 seconds to ensure the service at `localhost:8001` responds successfully. If it fails 3 times in a row or takes longer than 5 seconds, the container is marked as unhealthy.


