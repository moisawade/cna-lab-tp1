# cna-lab-tp1 : CNA Lab 


# 1- Création d’un namespace
kubectl create ns catalogue

# 2- Créer un pod à partir d’une image docker
kubectl run  sunu-catalogue -n catalogue --restart=Never  --image freemanpolys/catalogue-dsi --port 8080

# 3-Vérifier le status du pod sunu-catalogue
kubectl get pod sunu-catalogue -n catalogue

#4- Supprimer le pod sunu-catalogue
kubectl delete pod sunu-catalogue -n catalogue

#5- Liste des pods dans le namespace
kubectl get pod -n catalogue

#6-Créer un fichier de manfest pour le déploiement à partir d’une image docker
kubectl create deployment catalogue --image=freemanpolys/catalogue-dsi --dry-run=client -o yaml > cna-catalogue.yaml

#7 Créer le déploiement à partir du fichier de manifest
kubectl apply cna-catalogue.yaml

#8 Lister tous les objets dans le namespace
kubectl get all -n catalogue

#9 Créer un service de type ClusterIP
kubectl expose  deployment.apps/sunu-catalogue --name service1  --port 8080 -n catalogue

#10 Créer un service de type NodePort
kubectl expose  deployment.apps/sunu-catalogue --name service2 --type NodePort  --port 8080 -n catalogue

#11 Lister les services
kubectl get services -n catalogue

#12 Tester le service

curl http://172.17.0.72:30066
