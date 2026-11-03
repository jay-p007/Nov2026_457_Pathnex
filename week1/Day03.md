# Day 03 - Ansible, Terraform & Kubernetes Basics

## 1. Ansible - Install Apache and Start Service

```yaml
- name: Install and Start Apache
  hosts: all
  become: yes
  tasks:
    - name: Install apache
      yum:
        name: httpd
        state: present

    - name: Start apache
      service:
        name: httpd
        state: started
        enabled: yes
```

## 2. Terraform - EC2 Instance (t3.medium)

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "PathnexEC2" {
  ami           = "ami-0abcd1234abcd1234"
  instance_type = "t3.medium"

  tags = {
    Name = "Pathnex-T3"
  }
}
```

## 3. Kubernetes - create a Replicaset with 3 Replicas

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: pathnex-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: pathnex-app
  template:
    metadata:
      labels:
        app: pathnex-app
    spec:
      containers:
        - name: app
          image: nginx
          ports:
            - containerPortt: 80
```

## 4. Shell Script - User Info

```bash
#!/bin/bash

echo "Current user: $(whoami)"
echo "Current user groups: $(groups)"
```

## 5. Docker - Nginx Web Server

### Dockerfile

```dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
```

### HTML

```html
<h1>Hello Pathnex</h1>
```

### Nginx Web Root Path

```bash
/usr/share/nginx/html
```

### Docker Commands

```bash
docker build -t pathnex-nginx .
docker run -d -p 80:80 pathnex-nginx
```