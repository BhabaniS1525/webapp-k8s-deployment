# 🧠 Memcached Deployment & Service VProfile

These Kubernetes manifests define the **Memcached caching layer** for the VProfile application. Memcached is used to improve application performance by caching frequently accessed data and reducing database load.

### 📦 Memcached Deployment

#### 🔍 Deployment Explanation

- **replicas: 1**
  Runs a single Memcached instance.
  (Can be scaled horizontally if needed.)

- **container image: `memcached`**
  Uses the official Memcached container image.

- **containerPort: 11211**
  Exposes the standard Memcached port inside the pod.

#### 🔍 Service Explanation

- **Service Name:** `vprocache01`
  Creates a stable internal DNS entry and should match the application properties file

  ```
  vprocache01.default.svc.cluster.local
  ```

- **selector:**
  Routes traffic to pods labeled `app: vpromc`.

- **port mapping:**

  - Service Port: `11211`
  - Target Port: `vpromc-port` (container port)

- **type: ClusterIP**
  Exposes Memcached **only within the cluster**, making it inaccessible externally.

### ⚙️ How the Application Uses Memcached

Application pods connect to Memcached using:

```text
vprocache01:11211
```

Kubernetes handles:

- Pod IP changes
- Service discovery
- Load balancing (if scaled)

### ✅ Key Benefits

- Improves application performance
- Reduces database load
- Internal-only access for security
- Easy scaling via replica count
