# Microservices-based E-Commerce Backend on AWS (Flask + ECS Fargate + ALB)

This project demonstrates how to build, containerize, and deploy a microservices-based e-commerce backend using **Flask**, **Docker**, and **AWS services** including **ECR, ECS (Fargate), CodeBuild**, and **Application Load Balancer (ALB)**.

Each service — Product, User, and Order — is built and deployed independently with its own container, and traffic is routed via ALB to appropriate endpoints.

---

## Project Structure
```

├── product-service/
│ ├── app.py
│ └── Dockerfile
├── user-service/
│ ├── app.py
│ └── Dockerfile
├── order-service/
│ ├── app.py
│ └── Dockerfile
├── buildspec.yml
└── README.md
```

Each service has its own:
- Flask API (`app.py`)
- Dockerfile
- Endpoint (e.g., `/users`, `/products`, `/orders`)

---

## Technologies Used

- **Flask** (Python Microservice Framework)
- **Docker** (Containerization)
- **AWS ECR** (Elastic Container Registry)
- **AWS CodeBuild** (CI)
- **AWS ECS with Fargate** (Container Orchestration)
- **ALB (Application Load Balancer)** (Routing traffic)
- **CloudWatch** (Logging and Monitoring)

---

## Setup Instructions

### 1. Clone the Repository
```
git clone <git url>
cd Microservices-E-Commerce-Backend
```
2. Create Flask Microservices
Each service has an app.py
3. Dockerize the Services
Each service has its own Dockerfile:
4. Create ECR Repositories
    - product-service
    - user-service
    - order-service
Use AWS Console or CLI.

5. Set Up AWS CodeBuild
    - refere the buildspec.yml in source code.

7. Deploy on ECS Fargate
- For each service:
    - Create a Task Definition
    - Set container port (5000/5001/5002)
    - Set memory/CPU as needed
    - Create an ECS Service using Fargate and connect to the ALB

7. Configure ALB (Application Load Balancer)
    - Create an ALB with a listener on port 80
    - Create Target Groups for each service

Set routing rules:
```
Path	Target Group
/users/*	tg-user
/products/*	tg-product
/orders/*	tg-order
```

Health checks should point to correct route /users, /products, etc.

Test Endpoints
Once deployed, access:

- http://ecommerce-alb-793475105.us-east-1.elb.amazonaws.com/users
- http://ecommerce-alb-793475105.us-east-1.elb.amazonaws.com/product
- http://ecommerce-alb-793475105.us-east-1.elb.amazonaws.com/order


Each should return a JSON response like:

{ "message": "Welcome to Product Service!" }

Common Issues & Fixes
```
| Issue                       | Fix                                                             |
| --------------------------- | --------------------------------------------------------------- |
| ECS service fails to deploy | Flask may not bind to `0.0.0.0`                                 |
| ALB health check fails      | Check target group path, port, and Flask route                  |
| Docker builds fail          | Ensure `buildspec.yml` is in root and Dockerfiles are valid     |
| ALB URL not accessible      | Check security groups and SG rules between ALB and ECS services |
```
Acknowledgements
Built as a hands-on project to practice real-world AWS DevOps deployment of microservices. Special thanks to the AWS docs and Flask community.

<img width="1837" height="933" alt="Screenshot from 2025-07-12 17-52-34" src="https://github.com/user-attachments/assets/cf38f58f-66e9-4bc3-a56d-20118ec25b7a" />
