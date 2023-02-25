#  Rapport Projet JEE

## Description

Le projet consiste en la création d'une application basée sur une architecture de micro-services pour gérer les factures contenant des produits appartenant à un client. Les micro-services développés dans le projet sont :

Customer-Service : micro-service permettant de gérer les clients de l'application.

Inventory-Service : micro-service permettant de gérer les produits de l'application.

Gateway-Service : micro-service de passerelle qui gère le routage des requêtes entre les différents micro-services de l'application.

Eureka-Discovery : micro-service de découverte qui permet aux micro-services de s'enregistrer et de découvrir les autres micro-services.

Authentication-Service : micro-service de sécurité qui gère l'authentification et l'autorisation des utilisateurs de l'application.

Billing-Service : micro-service qui utilise OpenFeign pour consommer les API REST des autres micro-services et générer des factures.

Data-Analytics-Service : micro-service qui utilise l'API Kafka Streams pour effectuer du traitement en temps réel sur les données de facturation.

En plus des micro-services, le projet comprend également un client Web Angular qui fournit une interface utilisateur pour interagir avec les micro-services. La sécurité est assurée en utilisant l'adaptateur Keycloak pour sécuriser les micro-services et l'interface utilisateur.


Dans la dernière partie du projet, l'application est intégrée à Kafka pour permettre la production et la consommation de factures en temps réel, ainsi qu'à un service de données analytiques pour effectuer du traitement en temps réel sur les données de facturation.


L'ensemble de l'application est déployé en utilisant des conteneurs Docker.

Customer-Service : ce micro-service est responsable de la gestion des clients. Il permet de créer, lire, mettre à jour et supprimer les informations relatives aux clients. Les clients sont stockés dans une base de données, et le micro-service fournit des API REST pour permettre la manipulation de ces données. Il utilise également le service de découverte Eureka pour l'enregistrement et la localisation des autres micro-services.


Inventory-Service : ce micro-service est responsable de la gestion des produits. Il permet de créer, lire, mettre à jour et supprimer les informations relatives aux produits. Les produits sont stockés dans une base de données, et le micro-service fournit des API REST pour permettre la manipulation de ces données. Il utilise également le service de découverte Eureka pour l'enregistrement et la localisation des autres micro-services.


Billing-Service : ce micro-service est responsable de la gestion des factures. Il utilise le micro-service customer-service pour récupérer les informations sur les clients et le micro-service inventory-service pour récupérer les informations sur les produits. Il utilise également Open Feign pour communiquer avec les autres micro-services. Le micro-service est conçu pour fournir des API REST pour créer, lire, mettre à jour et supprimer des factures, ainsi que pour récupérer des informations sur les factures.


Data-Analytics-Aervice : ce micro-service utilise l'API KAFKA Streams pour effectuer du Real Time Stream Processing en consommant les flux de factures publiées dans le Topic KAFKA. Il est conçu pour fournir une interface utilisateur simple pour visualiser les résultats du traitement en temps réel.


Eureka-Discovery : ce micro-service est responsable de la découverte des micro-services de l'application. Il permet aux micro-services de s'enregistrer et de découvrir les autres micro-services. Les micro-services enregistrés peuvent être retrouvés par leur nom logique plutôt que par leur adresse IP ou leur port. La découverte de services permet de garantir que les micro-services sont découverts de manière dynamique, sans qu'il soit nécessaire de les configurer manuellement.


Authentication-Service : ce micro-service est responsable de la sécurité de l'application. Il utilise Keycloak pour gérer l'authentification et l'autorisation des utilisateurs. Il fournit des API REST pour s'authentifier, se déconnecter et vérifier les informations d'authentification. Les utilisateurs peuvent être créés, mis à jour et supprimés. Les rôles peuvent également être créés, affectés aux utilisateurs et supprimés.


Frontend Angular : il s'agit de l'interface utilisateur de l'application. Il est conçu pour fournir une interface utilisateur conviviale pour interagir avec les micro-services de l'application. Les utilisateurs peuvent accéder aux fonctionnalités suivantes : créer, lire, mettre à jour et supprimer des clients, des produits et des factures. L'interface utilisateur est également sécurisée en utilisant l'adaptateur Keycloak pour assurer la sécurité de l'application.


Enfin, la Gateway Spring cloud Gateway est responsable de la gestion de la communication entre les micro-services et du routage des demandes entrantes vers les micro-services correspondants. Elle est configurée pour utiliser une configuration statique du système de routage, puis pour passer à une configuration dynamique des routes de la gateway.



## Première Partie 
On a commencé par créer les microservices Product-Service et Customer-Service , ensuite la passerelle (Gateway) et eureka 

### Actuator : 
![actuator](https://user-images.githubusercontent.com/86847138/200059853-129d8fe5-891a-4bd1-9646-207b3034a034.PNG)


### Actuator Beans : 
![actuator beans](https://user-images.githubusercontent.com/86847138/200059870-33c4bbf7-8912-48c5-aa20-63d0dbd44e1a.PNG)


### Actuator Env :
![actuator env](https://user-images.githubusercontent.com/86847138/200059925-311548f7-4965-4381-975e-04323f7c6b2b.PNG)


### Customer H2 Console :
![h2 console](https://user-images.githubusercontent.com/86847138/200059608-07b33ed6-96cd-444d-83ff-79a1e6b5cabb.PNG)


### Product H2 Console :

![h2 console inventory](https://user-images.githubusercontent.com/86847138/200059654-8b5662ca-fee2-4b70-b1ef-666083d05435.PNG)


### Customers with gateway : 
![customers 8888](https://user-images.githubusercontent.com/86847138/200060024-cdac0216-3801-4944-bf5f-3157a8980def.PNG)


### Products with gateway : 
![products 8888](https://user-images.githubusercontent.com/86847138/200060063-dc514efb-1641-44bc-9e37-1f7d0ffa6180.PNG)


### Id :

![products 8888 id](https://user-images.githubusercontent.com/86847138/200060118-2a85d4f4-27c2-45bf-8276-861e5d1f1f8b.PNG)



### Eureka before enabling Discovery Service :
![eureka before](https://user-images.githubusercontent.com/86847138/200060276-bff3e8ad-383f-46c7-b8de-fa1f53b46f7e.PNG)



### Eureka after enabling Discovery Service :
![eureka after](https://user-images.githubusercontent.com/86847138/200060309-644371cc-e1a7-40cb-a9ea-4e83ba7bff12.PNG)


### Customers with id using the Web Service :

![CUSTOMER SERVICE](https://user-images.githubusercontent.com/86847138/200060405-2f2684d3-92c3-41fb-88a8-4d3910bc5c69.PNG)



## Deuxième Partie : 

Création du microservice Billing-Service responsable de la facturation.

### H2 Console Bill :
![h2 console bill](https://user-images.githubusercontent.com/86847138/200087300-68a674d4-4308-4775-8363-2fb78ac3cded.PNG)




### H2 Console Product Item : 
![h2 console product item](https://user-images.githubusercontent.com/86847138/200087326-069e0b07-5d23-473f-9fb3-4c4810432c91.PNG)



### Billing Service toutes les données :
![billing-service all data](https://user-images.githubusercontent.com/86847138/200087372-36bbc5a6-3876-47dd-827a-5068c19c7640.PNG)



### Billing Service selon la donnée dont on a besoin (name dans le screenshot) : 
![billing-service selo le besoin (name)](https://user-images.githubusercontent.com/86847138/200087460-274e02b2-2c3a-4e82-8319-53d9494e7404.PNG)





## Troisième Partie : 

### Liaison entre Frontend et Backend dans la partie Backend :
![liaison](https://user-images.githubusercontent.com/86847138/209448838-05393df4-d551-499e-bf54-2b2cc59788c9.PNG)




### Angular Products :
![products](https://user-images.githubusercontent.com/86847138/209448854-97d36df0-542d-4c94-873c-d5589c25eb22.PNG)



### Angular Customers :

![customers](https://user-images.githubusercontent.com/86847138/209448873-a51f6331-ade0-4570-929d-57e420118c9d.PNG)



