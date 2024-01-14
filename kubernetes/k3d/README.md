# k3d use

k3 is a light weight kubernets cluster on docker. which means we can run kubernets inside docker. only use K3d for testing purposes.

## Installation

Install k3d by this command

```bash
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

## Quick Start

Create a Cluster `mycluster` with just a single server node:

```bash
k3d cluster create mycluster
```

## Use Case 

### Creating a cluster with open port `30080` to localhost:8082 with 2 agents and runing nginx 

create a cluster, mapping the port `30080` from agent to localhost:8082

```bash
k3d cluster create mycluster -p "8082:30080@agent:0" --agents 2
```

create a NodePort service for it by copying the following manifest to a file and applying it with `kubectl apply -f .`
- deploymen.yml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3  # Number of replicas (pods) to run
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest
        ports:
        - containerPort: 80
```

- service.yml

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: nginx
  name: nginx
spec:
  ports:
  - name: 80-80
    nodePort: 30080
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: nginx
  type: NodePort
```
