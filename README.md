# 🐘 MySQL Kubernetes Deployment using StatefulSet

This project deploys a **MySQL database** using a **Kubernetes StatefulSet** in a dedicated namespace. It uses **Secrets**, **ConfigMaps**, **Persistent Volumes**, and a **Headless Service** to manage a production-like database setup.

---

## 📂 Project Structure

```
mysql-k8s-statefulset/
├── k8s/
│   ├── namespace.yml        # Creates 'mysql' namespace
│   ├── statefulset.yml      # Defines the StatefulSet for MySQL
│   ├── service.yml          # Headless service for MySQL access
│   ├── configmap.yml        # Stores environment configuration
│   └── secrets.yml          # Stores sensitive data like root password
└── README.md
```

---

## 🧰 Tools & Concepts Used

- Kubernetes (KIND cluster or any cluster)
- StatefulSet
- Headless Service (`clusterIP: None`)
- ConfigMaps & Secrets
- PersistentVolumeClaims
- Namespaces

---

## 🚀 Deployment Steps

### 1. Clone the repository
```bash
git clone https://github.com/singh-gauravv/mysql-k8s-statefulset.git
cd mysql-k8s-statefulset/k8s
```

### 2. Apply Kubernetes manifests
```bash
kubectl apply -f namespace.yml
kubectl apply -f configmap.yml
kubectl apply -f secrets.yml
kubectl apply -f service.yml
kubectl apply -f statefulset.yml
```

### 3. Verify the deployment
```bash
kubectl get all -n mysql
kubectl get pods -n mysql
kubectl get pvc -n mysql
```

---

## 🔐 Security Note

The password in `secrets.yml` is base64-encoded and **not encrypted**. For production, use Kubernetes Secrets with external secret management tools like HashiCorp Vault or Sealed Secrets.

---

## 📌 Important Notes

- StatefulSet ensures each MySQL pod gets a stable identity (`mysql-0`, `mysql-1`, etc.)
- `PersistentVolumeClaims` ensure data is not lost when pods restart
- `Headless Service` (`clusterIP: None`) enables stable DNS names for MySQL pods

---

## 🤝 Contributions

Feel free to fork this repo and suggest improvements!

---

## 📄 License

This project is open-sourced under the MIT License.
