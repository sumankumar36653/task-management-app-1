# AWS Deployment Guide

## Quick Start

### 1. Install Dependencies
```bash
cd infra && npm install
cd ../backend && npm install
```

### 2. Configure AWS
```bash
aws configure
```

### 3. Bootstrap CDK
```bash
cd infra
npx cdk bootstrap
```

### 4. Deploy Infrastructure
```bash
npx cdk deploy
```

### 5. Build & Push Docker Image
```bash
cd ../backend
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin YOUR_ACCOUNT.dkr.ecr.us-east-1.amazonaws.com
docker build -t task-app .
docker tag task-app:latest YOUR_ACCOUNT.dkr.ecr.us-east-1.amazonaws.com/REPO:latest
docker push YOUR_ACCOUNT.dkr.ecr.us-east-1.amazonaws.com/REPO:latest
```

## Architecture

- **Frontend**: Next.js (can deploy to Vercel or S3+CloudFront)
- **Backend**: Node.js/Express on ECS Fargate
- **Database**: DynamoDB
- **Load Balancer**: Application Load Balancer
- **Container Registry**: Amazon ECR

## Cleanup

```bash
cd infra
npx cdk destroy
```
