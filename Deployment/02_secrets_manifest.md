# 🔐 Kubernetes Secret Application Credentials

This manifest defines a **Kubernetes Secret** used to securely store sensitive credentials required by the VProfile application, such as database and RabbitMQ passwords.

Secrets allow sensitive data to be managed separately from application code and configuration files.

### 🔍 Field-by-Field Explanation

- **name: `app-secret`**
  Unique name of the Secret within the namespace.
  Pods reference this name to consume the secret values.

- **labels:**

  ```yaml
  app: vprofile
  ```

  Used for grouping and identifying resources associated with the VProfile application.

- **type: Opaque**

  - Used for arbitrary key-value pairs
  - Data is base64-encoded
  - Most commonly used Secret type in Kubernetes

- **data**

  Contains the sensitive information stored as **base64-encoded values**.

  > ⚠️ Kubernetes Secrets are **base64-encoded, not encrypted** by default.
  > For production, consider encryption at rest and secret managers (AWS Secrets Manager, Vault).

  ```bash
  echo -n 'your_string_here' | base64
  ```
