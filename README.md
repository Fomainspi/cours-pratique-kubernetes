# Cours pratique Kubernetes — FOMA

Formation DevOps en français : Workloads, probes, stockage persistant et networking Kubernetes.

Le cours complet et les manifestes YAML sont organisés dans `docs/LESSON.md`, `k8s/` et `images/`.

## Déploiement

```bash
kubectl apply -f k8s/00-namespace.yaml
kubectl apply -f k8s/01-postgres-secret.example.yaml
kubectl apply -f k8s/02-postgres-headless-service.yaml
kubectl apply -f k8s/03-postgres-service.yaml
kubectl apply -f k8s/04-postgres-statefulset.yaml
kubectl rollout status statefulset/postgres -n foma-shop
kubectl apply -f k8s/05-backend-deployment.yaml
kubectl apply -f k8s/06-backend-service.yaml
kubectl apply -f k8s/07-frontend-deployment.yaml
kubectl apply -f k8s/08-frontend-service.yaml
```

Les images Backend/Frontend et les endpoints de santé sont des exemples à adapter. Le Secret est réservé à la démonstration : ne commitez jamais de vrais identifiants. PostgreSQL utilise un seul replica ; StatefulSet seul ne fournit pas la haute disponibilité de la base.

## Auteur

**William Foma** — Foundation of Mastering Automation (FOMA)  
https://www.foma.life
