# 🗄️ Database Deployment MySQL (VProfile)

This Kubernetes **Deployment** manifest defines the database layer for the VProfile application. It deploys a MySQL container with persistent storage, secure credential management, and an initialization step to ensure clean volume startup.

### 🔍 Detailed Explanation

#### replicas: 1

Runs a single database pod.
Databases are typically deployed as a single instance when using block storage like EBS.

#### selector & template

Ensures the Deployment manages only pods labeled `app: vprodb`.

#### 🐳 Container Configuration

#### Container Image

```yaml
image: vprocontainers/vprofiledb
```

Prebuilt MySQL image containing the VProfile database schema.

#### Ports

```yaml
containerPort: 3306
```

Exposes the MySQL service port inside the cluster.

#### Environment Variables (Secrets)

```yaml
MYSQL_ROOT_PASSWORD
```

- Retrieved securely from a Kubernetes **Secret**
- Avoids hardcoding sensitive credentials

#### 💾 Persistent Storage

#### PersistentVolumeClaim

```yaml
claimName: db-pv-claim
```

- Mounts persistent storage at `/var/lib/mysql`
- Ensures database data survives pod restarts and rescheduling

#### ⚙️ Init Container

```yaml
initContainers:
  - name: busybox
```

#### Purpose

Removes the `lost+found` directory created by some storage backends.

**Why It’s Needed**

- MySQL fails to start if unexpected files exist in its data directory
- Ensures a clean data path before the main container starts
