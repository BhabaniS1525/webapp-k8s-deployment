# 🚀 VProfile Application - Kubernetes Deployment

## 📋 Project Overview

**VProfile** is a multi-tier web application that demonstrates production-grade deployment on Kubernetes clusters. This project provides a complete DevOps workflow for containerizing, orchestrating, and scaling a Spring MVC-based application with multiple backend services.

The application is fully containerized and can be deployed on:

- **AWS EKS** (Elastic Kubernetes Service)
- **KOps** (Kubernetes Operations)
- **kubeadm** (Self-managed Kubernetes)
- **Minikube** (Local development)

## 🏗️ Architecture Overview

### Application Stack

The VProfile application is a **multi-tier architecture** consisting of:

```
┌─────────────────────────────────────────────────┐
│         Ingress / Load Balancer                 │
├─────────────────────────────────────────────────┤
│  VProfile Web App (Spring MVC, Tomcat, Port 8080) │
├─────────────────────────────────────────────────┤
│                                                   │
│  ├─ MySQL Database (Port 3306)                  │
│  ├─ Memcached (Port 11211)                      │
│  └─ RabbitMQ (Port 5672)                        │
│                                                   │
└─────────────────────────────────────────────────┘
```

### Kubernetes Services

- **vproapp** - Main application deployment (Spring MVC)
- **vprodb** - MySQL database with persistent storage
- **vprocache01** - Memcached for caching
- **vpromq01** - RabbitMQ for message queuing
- **Ingress Controller** - External access to the application

## 📦 Technologies & Dependencies

### Backend Framework

- **Spring Framework** 6.0.11
- **Spring Boot** 3.1.3
- **Spring Security** 6.1.2
- **Spring Data JPA** 3.1.2

### Web & Server

- **Apache Tomcat** (WAR deployment)
- **JSP** (Java Server Pages)
- **Maven 3+** (Build automation)

### Databases & Caching

- **MySQL 8** (Relational database)
- **Memcached** (In-memory caching)
- **RabbitMQ** (Message broker)
- **Hibernate** 7.0.0 (ORM)

### Container Orchestration

- **Kubernetes** (Container orchestration)
- **Docker** (Containerization)

### Testing & Logging

- **JUnit 4** (Unit testing)
- **Logback** 1.5.6 (Logging framework)

## 📋 Prerequisites

### Local Development

- **JDK 17+** (Java Development Kit)
- **Maven 3.6+** (Build tool)
- **MySQL 8+** (Local testing)
- **Docker** (Containerization)

### Kubernetes Cluster Setup

- **kubectl** (Kubernetes CLI tool)
- **Kubernetes Cluster** (1.20+ version)
  - AWS EKS, KOps, kubeadm, or Minikube
- **Container Registry** (Docker Hub, ECR, or similar)
- **Persistent Volume Support** (for database storage)

---

## 🗂️ Project Structure

```
02_vprofile_deploy_k8s_cluster/
├── README.md                          # Project documentation
├── Deployment/                        # Kubernetes deployment guides
│   ├── 00_deployment_to_k8s.md       # K8s deployment overview
│   ├── 01_vprofile_code_overview.md  # Application code structure
│   ├── 02_secrets_manifest.md        # Kubernetes secrets configuration
│   ├── 03_pvc_manifest.md            # Persistent volume claims
│   ├── 04_mysql_db_manifest.md       # MySQL deployment
│   ├── 05_mysql_service_manifest.md  # MySQL service
│   ├── 06_memcache_deployment_and_service_manifest.md
│   ├── 07_rabbitmq_deployment_and_service_manifest.md
│   ├── 08_app_deployment_and_service_manifest.md
│   ├── 09_ingress_manifest.md        # Ingress configuration
│   ├── 10_cluster_and_sourcecode_setup.md
│   └── 11_vprofile_live.md           # Live deployment validation
├── k8s_cluster_setup/                # Cluster setup guides
│   ├── AWS_EKS_setup.md              # AWS EKS deployment guide
│   ├── KOps_setup.md                 # KOps deployment guide
│   ├── kubeadm_setup.md              # kubeadm deployment guide
│   └── minikube_setup.md             # Minikube setup guide
├── Images/                            # Screenshot & documentation images
└── vprofile-app/                      # Main application code
    ├── pom.xml                        # Maven configuration
    ├── docker-compose.yml             # Docker Compose for local dev
    ├── Docker-files/                  # Docker container definitions
    │   ├── app/Dockerfile             # Application container
    │   ├── app/multistage/Dockerfile  # Multi-stage build
    │   ├── db/Dockerfile              # MySQL container
    │   └── web/Dockerfile             # Nginx web server
    ├── k8s_defination/                # Kubernetes manifests
    │   ├── secret.yaml                # Database credentials
    │   ├── db_pvc.yaml                # Database persistent volume
    │   ├── db_deployment.yaml         # MySQL deployment
    │   ├── db_service.yaml            # MySQL service
    │   ├── memcache_deployment.yaml   # Memcached deployment
    │   ├── memcache_service.yaml      # Memcached service
    │   ├── rabbitmq_deployment.yaml   # RabbitMQ deployment
    │   ├── rabbitmq_service.yaml      # RabbitMQ service
    │   ├── app_deployment.yaml        # Application deployment
    │   ├── app_service.yaml           # Application service
    │   └── ingress.yaml               # Ingress configuration
    └── src/                           # Application source code
        ├── main/
        │   ├── java/com/visualpathit/ # Java application code
        │   ├── resources/             # Application resources
        │   │   ├── accountsdb.sql     # Database schema
        │   │   ├── db_backup.sql      # Database backup/dump
        │   │   └── application.properties
        │   └── webapp/                # Web resources (JSP, CSS, JS)
        └── test/                      # Test classes
```

## 📚 Documentation

Complete deployment documentation is available in the `Deployment/` directory:

| Document                                                                                                    | Purpose                                         |
| ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| [00_deployment_to_k8s.md](Deployment/00_deployment_to_k8s.md)                                               | Kubernetes deployment overview & best practices |
| [01_vprofile_code_overview.md](Deployment/01_vprofile_code_overview.md)                                     | Application code structure & components         |
| [02_secrets_manifest.md](Deployment/02_secrets_manifest.md)                                                 | Kubernetes secrets configuration                |
| [03_pvc_manifest.md](Deployment/03_pvc_manifest.md)                                                         | Persistent volume setup                         |
| [04_mysql_db_manifest.md](Deployment/04_mysql_db_manifest.md)                                               | MySQL deployment manifest                       |
| [05_mysql_service_manifest.md](Deployment/05_mysql_service_manifest.md)                                     | MySQL service configuration                     |
| [06_memcache_deployment_and_service_manifest.md](Deployment/06_memcache_deployment_and_service_manifest.md) | Memcached setup                                 |
| [07_rabbitmq_deployment_and_serivce_manifest.md](Deployment/07_rabbitmq_deployment_and_serivce_manifest.md) | RabbitMQ setup                                  |
| [08_app_deployment_and_service_manifest.md](Deployment/08_app_deployment_and_service_manifest.md)           | Application deployment                          |
| [09_ingress_manfiest.md](Deployment/09_ingress_manfiest.md)                                                 | Ingress controller configuration                |
| [10_cluster_and_sourcecode_setup.md](Deployment/10_cluster_and_sourcecode_setup.md)                         | Cluster & source code preparation               |
| [11_vprofile_live.md](Deployment/11_vprofile_live.md)                                                       | Live deployment validation & screenshots        |

---

## 🔐 Security

### Kubernetes Security Features

- **Secrets Management**: Database credentials stored as K8s secrets (not in code)
- **RBAC**: Role-based access control (can be configured)
- **Network Policies**: Pod-to-pod communication restrictions (optional)
- **Resource Limits**: CPU and memory constraints on containers

### Application Security

- **Spring Security**: User authentication and authorization
- **HTTPS/TLS**: Should be configured at Ingress layer
- **Database Encryption**: Configure at storage level

---

## 📈 Scaling & Performance

### Horizontal Scaling

```bash
# Scale application replicas
kubectl scale deployment vproapp --replicas=3

# Scale other services as needed
kubectl scale deployment vprodb --replicas=1
kubectl scale deployment vprocache01 --replicas=2
```

### Resource Management

Configure in deployment manifests:

- **CPU Requests/Limits**: Define in container spec
- **Memory Requests/Limits**: Define in container spec
- **Startup/Shutdown Timeouts**: Configure graceful termination

---

## 🔍 Troubleshooting

### Common Issues & Solutions

1. **Pod Not Starting**: Check logs with `kubectl logs <pod-name>`
2. **Database Connection Failures**: Verify secrets and service DNS
3. **Persistent Volume Issues**: Check PVC status with `kubectl get pvc`
4. **Service Discovery**: Use `kubectl get svc` to verify service endpoints

### Useful Commands

```bash
# View cluster status
kubectl cluster-info

# List all pods
kubectl get pods -A

# Check pod details
kubectl describe pod <pod-name>

# View logs
kubectl logs <pod-name>

# Execute command in pod
kubectl exec -it <pod-name> -- /bin/bash

# Port forward for testing
kubectl port-forward svc/vproapp 8080:8080
```

## 🎯 Key Features

✅ **Multi-tier Architecture**: Web app, database, caching, message queue
✅ **Production-Ready**: High availability, scalability, fault tolerance
✅ **Containerized**: Docker images for all components
✅ **Kubernetes-Native**: Complete K8s manifests for all services
✅ **Persistent Storage**: Database data survives pod restarts
✅ **Service Discovery**: Automatic DNS-based service resolution
✅ **Security**: Secrets management, secure credential handling
✅ **Flexible Deployment**: Works on EKS, KOps, kubeadm, or Minikube
✅ **Comprehensive Docs**: Step-by-step guides for each cluster type
✅ **Validation**: Live deployment verification with screenshots

## 📞 Support Resources

For detailed setup instructions, refer to:

- [Cluster Setup Guides](k8s_cluster_setup/)
- [Deployment Documentation](Deployment/)
- [Kubernetes Official Docs](https://kubernetes.io/docs/)
- [Spring Framework Docs](https://spring.io/projects/spring-framework/)
