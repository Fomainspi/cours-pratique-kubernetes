# Cours pratique Kubernetes — FOMA

**Parcours DevOps : de la théorie à la production**

Ce dépôt contient un cours structuré et un laboratoire Kubernetes illustrant une architecture Frontend Next.js, Backend Node.js et PostgreSQL.

## Contenu
- [Leçon complète](docs/LESSON.md) : Pods, Deployment, StatefulSet, DaemonSet, labels/selectors, probes, stockage, Services, DNS, CoreDNS, EndpointSlices et kube-proxy.
- [Manifestes Kubernetes](k8s/) : namespace, Secret d'exemple, Services, StatefulSet PostgreSQL, Deployments Frontend/Backend, Ingress et DaemonSet Node Exporter facultatif.
- [Illustrations](images/) : architecture et flux réseau.

## Ordre de déploiement
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

## Prérequis et avertissements
- Cluster Kubernetes et kubectl configuré.
- StorageClass fonctionnelle pour le PVC PostgreSQL.
- Remplacer les images applicatives d'exemple par vos images publiées et implémenter les endpoints health.
- Ingress nécessite un contrôleur Ingress.
- Le Secret est strictement pédagogique : ne jamais commiter de vrais identifiants.
- PostgreSQL utilise un replica unique. StatefulSet + PVC ne fournissent pas automatiquement réplication, failover, haute disponibilité ni sauvegarde.
- Le manifeste Node Exporter est facultatif et utilise des accès au système hôte ; auditer avant usage.

## Vérifications
```bash
kubectl get pods,svc,pvc -n foma-shop
kubectl get endpointslices -n foma-shop
kubectl get pods -n foma-shop -o wide
```

**William Foma** — Foundation of Mastering Automation  
https://www.foma.life
