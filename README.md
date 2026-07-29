# hello-world

A multi-module Maven project (`server` + `webapp`) packaged as a WAR and deployed to Tomcat, with Kubernetes manifests to run it as the `regapp` deployment/service.

## Structure

```
.
├── pom.xml                # parent POM, declares the server/webapp modules
├── server/                # Greeter class + unit test
├── webapp/                 # web application module
├── Dockerfile              # copies the built WAR into a Tomcat image
├── regapp-deploy.yml       # Kubernetes Deployment (2 replicas, rolling update)
└── regapp-service.yml      # Kubernetes Service (LoadBalancer, port 8080)
```

## Build

```bash
mvn clean package
```

## Run with Docker

```bash
docker build -t regapp .
docker run -p 8080:8080 regapp
```

## Deploy to Kubernetes

```bash
kubectl apply -f regapp-deploy.yml
kubectl apply -f regapp-service.yml
```
