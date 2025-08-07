# 🌍 Ingress Configuration VProfile Application

This Kubernetes **Ingress** manifest defines how external HTTP/HTTPS traffic is routed to the VProfile application services inside the Kubernetes cluster using an **NGINX Ingress Controller**.

### 🔍 Field-by-Field Explanation

#### apiVersion: networking.k8s.io/v1

Uses the stable Kubernetes API version for Ingress resources.

#### kind: Ingress

Declares an Ingress resource, which manages external access to services inside the cluster.

#### metadata

- **name: `vpro-ingress`**
  Unique identifier for the Ingress resource.

- **annotations**

  ```yaml
  nginx.ingress.kubernetes.io/use-regex: "true"
  ```

  Enables regex-based path matching (useful for advanced routing rules).

#### spec.ingressClassName: nginx

Specifies that this Ingress is handled by the **NGINX Ingress Controller**.

#### rules

Defines how traffic is routed based on hostnames and paths.

#### Host

```yaml
host: vprofile.devops-prod.xyz
```

Traffic destined for this domain is handled by this Ingress.

#### Path Routing

```yaml
path: /
pathType: Prefix
```

Routes all requests with path `/` or any subpath to the backend service.

#### Backend Service

```yaml
service:
  name: vproapp-service
  port:
    number: 8080
```

Forwards traffic to the application service running on port **8080**.

### ⚙️ How Traffic Flows

```text
User → DNS (GoDaddy) → Ingress Controller (Nginx) → vproapp-service (ClusterIP) → Application Pods
```
