# Kubernetes Configuration for WordPress and MySQL Deployment 

This repository contains Kubernetes YAML configuration files for deploying WordPress and MySQL with persistent storage in a Kubernetes cluster.

## Files Included

### 1. `PV.yaml`
- **Description:** Defines a PersistentVolume (PV) for MySQL data storage.
- **Namespace:** `<your-namespace>`
- **Capacity:** 3Gi
- **AccessMode:** `ReadWriteOnce`
- **StorageClass:** `local-path`
- **HostPath:** `/mnt/data`

### 2. `Update PV.yaml`
- **Description:** Contains updates or changes made to the `PV.yaml` over time.

### 3. `PVC.yaml`
- **Description:** Defines a PersistentVolumeClaim (PVC) for MySQL data.
- **Namespace:** `<your-namespace>`
- **Requested Storage:** 1Gi
- **AccessMode:** `ReadWriteOnce`
- **StorageClass:** `local-path`

### 4. `Update PVC.yaml`
- **Description:** Contains updates or changes made to the `PVC.yaml`.

### 5. `mysql-deployment.yaml`
- **Description:** Deployment configuration for the MySQL database.
- **Namespace:** `<your-namespace>`
- **MySQL Version:** `8.0`
- **Environment Variables:** Populated from `mysql-secret` and `wordpress-config`.
- **Volumes:** Mounts the `mysql-data` PersistentVolumeClaim.

### 6. `Update mysql-deployment.yaml`
- **Description:** Contains updates or changes made to `mysql-deployment.yaml`.

### 7. `mysql-secret.yaml`
- **Description:** Kubernetes Secret configuration for MySQL credentials (root password and username).
- **Namespace:** `<your-namespace>`
- **Data:** Base64-encoded credentials for `MYSQL_ROOT_PASSWORD` and `MYSQL_ROOT_USER`.

### 8. `Create mysql-secret.yaml`
- **Description:** Instructions or updates regarding the creation or modification of `mysql-secret.yaml`.

### 9. `mysql-service.yaml`
- **Description:** Service configuration for MySQL database.
- **Namespace:** `<your-namespace>`
- **Service Type:** `ClusterIP`
- **Port:** Exposes MySQL on port `3306`.

### 10. `wordpress-deployment.yaml`
- **Description:** Deployment configuration for WordPress.
- **Namespace:** `<your-namespace>`
- **WordPress Version:** `6.3.1` with PHP 8.1.
- **Environment Variables:** Database connection information is set using secrets and ConfigMaps.
- **Volumes:** Mounts the `wordpress-data` PersistentVolumeClaim.

### 11. `Create wordpress-deployment.yaml`
- **Description:** Instructions or updates for the creation or modification of `wordpress-deployment.yaml`.

### 12. `Ingress.yaml`
- **Description:** Nginx Ingress configuration for routing external traffic to WordPress.
- **Namespace:** `<your-namespace>`
- **Host:** `yourdomain-name.com`
- **Service:** Routes traffic to `wordpress-service` on port `80`.

### 13. `Update Ingress.yaml`
- **Description:** Updates or modifications to the `Ingress.yaml`.

### 14. `wordpress-service.yaml`
- **Description:** Service configuration for WordPress.
- **Namespace:** `<your-namespace>`
- **Service Type:** `ClusterIP`
- **Port:** Exposes WordPress on port `80`.

### 15. `Update wordpress-service.yaml`
- **Description:** Updates or modifications to `wordpress-service.yaml`.

## Usage

To deploy the resources in a Kubernetes cluster:

1. Ensure you have a running Kubernetes cluster and `kubectl` configured.
2. Apply the files in the following order:

   ```bash
   kubectl apply -f mysql-secret.yaml
   kubectl apply -f PV.yaml
   kubectl apply -f PVC.yaml
   kubectl apply -f mysql-deployment.yaml
   kubectl apply -f mysql-service.yaml
   kubectl apply -f wordpress-deployment.yaml
   kubectl apply -f wordpress-service.yaml
   kubectl apply -f Ingress.yaml
