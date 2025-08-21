# 📦 PersistentVolumeClaim (PVC) Database Storage

This manifest defines a **PersistentVolumeClaim (PVC)** used by the VProfile application to request persistent storage for the database layer in a Kubernetes cluster.

PersistentVolumeClaims allow Kubernetes workloads to consume storage without needing to know the underlying storage implementation (EBS, EFS, NFS, etc.).

### 🔍 specifications

- **name: `db-pv-claim`**
  Unique name of the PVC within the namespace. Pods will reference this name to mount the storage.

- **labels:**

  ```yaml
  app: vprofile
  ```

  Labels help organize and identify resources related to the VProfile application.

- **resources.requests.storage: 3Gi**

  Kubernetes will bind this claim to a PersistentVolume that can satisfy this size requirement.

- **accessModes: ReadWriteOnce**
  The volume can be mounted as read-write by **a single node** at a time.
  This is the most common access mode for database workloads.

- **storageClassName: Default**

  - On AWS, this typically provisions an **EBS volume**
  - On other platforms, it maps to the default storage backend
