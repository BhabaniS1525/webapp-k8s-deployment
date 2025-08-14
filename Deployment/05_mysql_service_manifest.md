# 🌐 Database Service MySQL (VProfile)

This Kubernetes **Service** manifest exposes the MySQL database deployed by the `vprodb` Deployment to other application components **within the Kubernetes cluster** using a stable internal network endpoint.

### 🔍 Field-by-Field Explanation

#### kind: Service

Declares a Kubernetes Service, which provides **service discovery and load balancing** for a set of pods.

#### spec.selector

```yaml
app: vprodb
```

Selects all pods labeled `app: vprodb`, ensuring traffic is routed only to database pods.

---

#### ports

| Field        | Description                        |
| ------------ | ---------------------------------- |
| `port`       | Port exposed by the Service (3306) |
| `targetPort` | Container port (`vprodb-port`)     |
| `protocol`   | TCP (required for MySQL)           |

#### type: ClusterIP

- Exposes the Service **internally only**
- Not accessible from outside the cluster
- Ideal for backend services like databases

#### ⚙️ How This Service Is Used

- Application pods connect to MySQL using:

  ```text
  vprodb:3306
  ```

- Kubernetes handles pod IP changes automatically
- Ensures reliable service discovery and connectivity

#### ✅ Key Benefits

- Stable internal endpoint for the database
- Decouples application from pod IPs
- Secure, internal-only access
- Native load balancing (if multiple replicas exist)
