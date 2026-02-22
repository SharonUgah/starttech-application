# StartTech Application Repository 

## Project Overview

This repository contains the full-stack application for StartTech, including:

- Frontend (React)
- Backend API (Golang)
- CI/CD pipelines using GitHub Actions
- Deployment automation scripts

The application is designed to integrate with AWS infrastructure provisioned via Terraform.

---

## Application Architecture

### Frontend
- Built with React
- Compiled into static production files
- Deployed to Amazon S3
- Delivered globally using CloudFront CDN

### Backend
- Developed in Golang
- Packaged as a Docker container
- Deployed to EC2 instances
- Managed by Auto Scaling Group
- Load balanced via Classic Load Balancer
- Logs collected in CloudWatch

### Caching
- Redis (ElastiCache)
- Used for session management and performance optimization

### Database
- MongoDB Atlas (managed cloud database)
- Secure connection string stored in environment variables

---

## CI/CD Pipelines

GitHub Actions is used to automate build, test, security scanning, and deployment processes.

---

### Frontend CI/CD Pipeline

Triggered on push to main branch.

Build Stage:
- Install Node.js dependencies
- Run unit tests
- Perform security scanning using npm audit
- Build optimized production bundle

Deploy Stage:
- Sync build files to S3 bucket
- Invalidate CloudFront cache
- Notify deployment status

This ensures zero manual frontend deployments.

---

### Backend CI/CD Pipeline

Triggered on push to main branch.

Test Stage:
- Run Go unit tests
- Run integration tests
- Perform code quality checks
- Security vulnerability scanning

Build Stage:
- Build Docker image
- Scan Docker image for vulnerabilities
- Tag image with version
- Push image to Amazon ECR

Deploy Stage:
- Run smoke tests
- Perform rolling deployment via Auto Scaling Group
- Update Launch Template if required
- Send logs to CloudWatch
- Monitor deployment health

This ensures safe, automated, and scalable backend deployment.

---

## Environment Variables & Secrets

Sensitive configuration values are securely stored using:

- GitHub Secrets
- AWS IAM Roles
- MongoDB Atlas environment configuration

No secrets are stored in this repository.

Examples of environment variables:

- DATABASE_URL
- REDIS_HOST
- AWS_REGION
- S3_BUCKET_NAME

---

## Deployment Strategy

Frontend:
- Atomic deployment using S3 sync
- CloudFront invalidation ensures immediate content update

Backend:
- Rolling deployment through Auto Scaling Group
- Health checks ensure zero-downtime deployment
- Instances replaced gradually to prevent service interruption

---

## Monitoring & Observability

The application integrates with AWS CloudWatch for:

- Backend log aggregation
- Performance metrics
- Instance health monitoring
- Error tracking

Logs can be analyzed using CloudWatch Logs Insights.

---

## Repository Structure

.github/
└── workflows/
    ├── frontend-ci-cd.yml
    └── backend-ci-cd.yml

frontend/
backend/

scripts/
├── deploy-frontend.sh
├── deploy-backend.sh
├── health-check.sh
└── rollback.sh

---

## Security Practices

- Automated vulnerability scanning in CI pipeline
- Docker image scanning before deployment
- Least-privilege IAM roles
- Secure handling of API keys and credentials
- Network security enforced through security groups

---

## Conclusion

This repository demonstrates:

- Full CI/CD automation
- Scalable cloud deployment
- Secure secret management
- Automated testing and scanning
- Production-ready DevOps practices

The application integrates seamlessly with Terraform-managed infrastructure and follows modern DevOps standards.