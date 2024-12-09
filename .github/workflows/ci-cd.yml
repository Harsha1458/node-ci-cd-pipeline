name: CI/CD Pipeline

on:
  pull_request:
    branches:
      - main
  push:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
        
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'
        
      - name: Install dependencies
        run: npm install
        
      - name: Run tests
        run: npm test

  build-and-deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
        
      - name: Log in to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build Docker image
        run: |
          docker build -t ${{ secrets.DOCKER_USERNAME }}/node-app:${{ github.sha }} .
          docker push ${{ secrets.DOCKER_USERNAME }}/node-app:${{ github.sha }}
      
      - name: Set up kubectl
        uses: azure/setup-kubectl@v3
        with:
          version: 'latest'
      
      - name: Deploy to Kubernetes
        env:
          KUBECONFIG: ${{ secrets.KUBECONFIG }}
        run: |
          kubectl set image deployment/node-app node-app=${{ secrets.DOCKER_USERNAME }}/node-app:${{ github.sha }}
          kubectl rollout status deployment/node-app

  notify:
    needs: build-and-deploy
    runs-on: ubuntu-latest
    steps:
      - name: Notify deployment success
        if: success()
        run: echo "Deployment succeeded."
      
      - name: Notify deployment failure
        if: failure()
        run: echo "Deployment failed."
