# 🚀 Application Deployment & Service VProfile

These Kubernetes manifests define the **application tier** of the VProfile platform. The deployment ensures the application starts only after all required backend services are available, while the service provides stable internal access within the cluster.

### 📦 Application Deployment

#### 🔍 Deployment Explanation

#### replicas: 1

Runs a single application pod.
(For production, this can be scaled horizontally.)

#### Application Container

- **Image:** `vprocontainers/vprofileapp`
- **Port:** `8080`
- Hosts the VProfile web application.

#### Init Containers (Startup Dependency Checks)

The application depends on **database**, **Memcached**, and **RabbitMQ**.
Init containers ensure the application starts **only after these services are resolvable via DNS**.

| Init Container  | Dependency Checked        |
| --------------- | ------------------------- |
| `init-db`       | MySQL (`vprodb`)          |
| `init-memcache` | Memcached (`vprocache01`) |
| `init-rabbitmq` | RabbitMQ (`vpromq01`)     |

Each init container:

- Uses `nslookup` to check service availability
- Retries every 2 seconds
- Blocks application startup until dependencies are ready

### 🌐 Application Service

#### 🔍 Service Explanation

- **Service Name:** `vproapp-service`
- **Type:** `ClusterIP`
- Exposes the application **internally within the cluster**
- Routes traffic to pods labeled `app: vproapp`

### 🔁 Traffic Flow

```text
Ingress / LoadBalancer
        ↓
vproapp-service (ClusterIP)
        ↓
vproapp Pods
```
