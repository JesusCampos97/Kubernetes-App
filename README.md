# Kubernetes-App

1. Se crea un cluster con todo por defecto en GCP (GCK)
2. Conectamos mediante cloud console con el cluster.
![image](https://user-images.githubusercontent.com/29258769/121071522-551cae00-c7d0-11eb-8c16-e6e7e2863b26.png)

3. Dentro de el cloud console:
 <br>
  3.1. git clone https://github.com/jluisalvarez/k8s-vote-app
  <br>
  3.2. cd k8s-vote-app
  <br>
  3.3. kubectl apply -f .
  <br>
  3.4. Entramos en los ficheros de vote-service.yaml y result-service.yaml
  <br>
  3.5. Cambiamos los tipos de NodePort a LoadBalancer para que nos de las ips externas
  <br>
  ![image](https://user-images.githubusercontent.com/29258769/121072091-0e7b8380-c7d1-11eb-97c5-e27bc28fc7bb.png)
  3.6. Esperamos a que nos de las ip externas con kubectl get services
  <br>
  ![image](https://user-images.githubusercontent.com/29258769/121072172-2521da80-c7d1-11eb-9ba3-a74eecd81ed2.png)
  ![image](https://user-images.githubusercontent.com/29258769/121072320-5d291d80-c7d1-11eb-998a-7e14d9bd8181.png)

4. Necesitamos abrir los puertos TCP del 5000 al 30001 para los nodos para 0.0.0.0/0 dentro de Redes VPC<br>
5. Entramos en las ips que nos porporciona con los puertos 5001 para el result y 5000 para la app de votaciones:
 ![image](https://user-images.githubusercontent.com/29258769/121072459-88ac0800-c7d1-11eb-8b57-38c15bb8dbd7.png)
![image](https://user-images.githubusercontent.com/29258769/121072474-8cd82580-c7d1-11eb-92fe-c3913e9a1d99.png)
6. Para escalar la aplicación y color el numero de nodos para mi cluster que se llama cluster-1:<br>
  6.1. gcloud container clusters resize cluster-1 --region us-central1-c --num-nodes=0<br>
  6.2. gcloud container clusters resize cluster-1 --region us-central1-c --num-nodes=3<br>
  ![image](https://user-images.githubusercontent.com/29258769/121072810-f6583400-c7d1-11eb-9a4e-25e239604691.png)

7. Para escalar el cluster: kubectl scale deployments/vote --replicas=4<br>
8. Para actualizar la imagen de redis: kubectl set image deployments/redis redis=redis:6.0.3-alpine<br>
 ![image](https://user-images.githubusercontent.com/29258769/121072857-0bcd5e00-c7d2-11eb-9d05-117b1fccde9d.png)
