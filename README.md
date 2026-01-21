# ESIEA_S7_CICD_wordpress_mariadb

Projet de pipeline CI/CD pour déployer WordPress avec MariaDB sur Kubernetes.

Le workflow GitHub Actions convertit automatiquement la configuration Docker Compose en manifests Kubernetes, génère les secrets depuis les secrets GitHub, et upload le package final sur un serveur FTP. 

## Configuration

Avant d'utiliser le pipeline, configurez les secrets suivants dans les paramètres GitHub de votre repository :

- `MARIADB_ROOT_PASSWORD` : Mot de passe root de MariaDB
- `MARIADB_DATABASE` : Nom de la base de données
- `MARIADB_USER` : Nom d'utilisateur MariaDB
- `MARIADB_PASSWORD` : Mot de passe de l'utilisateur MariaDB

- `FTP_HOST` : Adresse du serveur FTP
- `FTP_USER` : Utilisateur FTP
- `FTP_PASSWORD` : Mot de passe FTP
- `FTP_PATH` : Chemin du répertoire FTP de destination

## Utilisation

Le pipeline se déclenche automatiquement lors d'un push sur la branche `main`, ou manuellement via l'action `workflow_dispatch` dans l'onglet Actions de GitHub.

Une fois le workflow terminé, récupérez le fichier `PaulineSoubrieWordpress.zip` depuis le serveur FTP et décompressez-le. Les manifests Kubernetes sont prêts à être déployés :

```bash
kubectl apply -f PaulineSoubrieWordpress/
```

## Structure

Le projet contient :
- `docker-compose.yml` : Configuration des services WordPress et MariaDB
- `.github/workflows/cicd.yml` : Pipeline CI/CD GitHub Actions
- Le workflow génère un dossier `PaulineSoubrieWordpress/` contenant tous les manifests Kubernetes (deployments, services, secrets, PVCs)