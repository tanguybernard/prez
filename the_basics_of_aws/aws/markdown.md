# Basics of AWS

Tanguy Bernard

-----

## Cloud Concept

Le cloud est un vaste réseau de serveurs distants éparpillés tout autour de la planète, reliés entre eux, et destinés à fonctionner comme un écosystème unique.

---

## Modèles de cloud computing


![Iaas, Paas, Saas](./aws/assets/iaas-paas-saas.jpg)


<div style="font-size:small">
source: https://cloud.google.com/learn/paas-vs-iaas-vs-saas?hl=fr
</div>

---

## Infrastructure as a Service

Vous louez le matériel sur lequel exécuter votre application, mais vous êtes responsable de la gestion de l'OS, de l'environnement d'exécution et du scaling, ainsi que de toutes les données.

Exemple: Amazon Elastic Compute Cloud (EC2)

---

## Containers as a Service (CAAS)

Considérer comme une sous catégorie du Iaas. 

A la différence que la ressource fondamentale sont les containers plutôt que les machines virtuelles ou les systèmes d'hébergement matériels.

Exemple: Amazon Elastic Container Service (ECS)

## Platform as a Service (PAAS)

Le fournisseur s'occupent de l'OS et de l'environnement d'execution (Java, Node, Python, Go...)

Vous pouvez vous concentrer sur le déploiement et la gestion de vos applications.

Exemple: AWS Elastic Beanstalk

## Beanstalk

![aws-beanstalk-platform.png](./aws/assets/Faws-beanstalk-plateform.png)

Exemple: AWS Elastic Beanstalk

---

## Function as a Service (Faas)

Vous permet d’exécuter du code en réponse à des événements !

Priorité au code et non à l’infrastructure : Avec le FaaS, vous pouvez diviser le serveur en fonctions qui peuvent être mises à l’échelle automatiquement !

Exemple: AWS Lambda

---

## Software as a Service (Saas)

Vous payez pour utiliser une application complète à des fins spécifiques. Elle est gérée, entretenue et sécurisée par le fournisseur cloud. Cependant, vous êtes responsable de la gestion de vos propres données.

Ex: Amazon Cognito

---

## Cloud Based, On-Premise And Hybrid

- Cloud: 
    - Public: Hebergé par un fournisseur, les ressources peuvent être redistribuées à d'autres clients.
    - Privé: Il peut soit se situer au sein d'une organisation, soit être géré à distance par un tiers et accessible sur Internet (il n'est partagé avec personne)
- On-Premise: Hébergement de son infrastructure IT
- Hybrid: Une combinaison d'au moins 2 environnements de cloud computing

---

## Benefits of AWS cloud

Remplace les dépenses d'investissement initiales (CAPEX) par de faibles dépenses d'exploitation variables (OPEX).

Vous ne payez que ce que vous utilisez !

---

## Framework d'adoption du Cloud AWS (AWS CAF)

AWS CAF fournit des conseils sur les bonnes pratiques qui améliore votre préparation au cloud.

Les perspective :

- Entreprise
- Personnes
- Gouvenance
- Plateforme
- Sécurité
- Opérations

---


## Pour se lancer

- Envisager: Identifiez et hiérarchisez les occasions de transformation
- Aligner: Identifiez les déficits de fonctionnalités et les dépendances inter-organisationnelles.
- Lancer: Menez des projets pilotes en production et démontrez la valeur opérationnelle progressive.
- Mettre à l'échelle: Étendez les pilotes et la valeur opérationnelle à l'échelle souhaitée


Exemple:  Tipee, Trackelec ?

---

## AWS Well-Architected

Le cadre AWS Well-Architected Framework décrit les concepts clés, les principes de conception et les bonnes pratiques architecturales pour concevoir et exécuter des charges de travail dans le cloud.

---

## Les six piliers

## Pilier Excellence opérationnelle

- Organisation
- Préparation
- Opération
- ...

## Pilier Sécurité

- Partage des responsabilités
- IAM
- Protection des infrastructures
- ...

## Pilier Fiabilité

- Conception de systèmes distribués
- Backup de données
- Plan de reprise après sinistre
- ...

## Pilier Efficacité des performances

- Devenir mondial en quelques minutes
- Utilisation des architectures sans serveur
- ...

## Pilier Optimisation des coûts

- Mesurer l'efficacité globale
- Adopter un modèle de consommation
- Mesurer le retour sur investissement (ROI)
- ...

## Pilier Développement durable

- Mesure de l'impact de la charge de travail
- Maximisation de l'utilisation des ressources
- Fixer des objectifs de durabilité
- ...

---


## AWS Global Infrastructure

![Regions at AZ](./aws/assets/Region_AZ.png)

source: https://aws.amazon.com/fr/about-aws/global-infrastructure/regions_az/

---

## Les zones de disponibilité (AZ)

Les zones de disponibilité sont physiquement séparées par une distance significative, c'est-à-dire plusieurs kilomètres, de toute autre zone de disponibilité.

![regions-and-zones.png](./aws/assets/regions-and-zones.png)


source: https://aws.amazon.com/fr/about-aws/global-infrastructure/regions_az/

---

## Cloud Technology and Services

- Machine Learning
- Calcul
- Stockage
- Outils pour les développeurs
- Base de données
- Blockchain
- Web et mobile front
- Analyses
- Sécurité, identité et conformité

---

## Calcul

- Elastic Compute Cloud (EC2): Le produit phare, le serveur virtuel.
- Lambda: Service de calcul d'événement sans serveur (serverless).
- Elastic Container Service (ECS): Gestion de conteneurs.
- Elastic Kubernetes Service (EKS): Service Kubernetes géré.
- Fargate: Gestion de conteneurs sans serveur


Note: ECS tu gère provision les instances ec2 sur lequel tourne les conteneurs. Avec fargate tu ne gères pas les instances EC2.

---

## Stockage

- Elastic Block Store (EBS): Disque dur SDD ou HDD.
- Simple Storage Service (S3): Stockage d'objets (pdf, photos, vidéos...)
- Elastic File System (EFS): Stockage très elastique et qui se partage entre différentes instances EC2.

---

## S3


---

## Security and Compliance

-----

## Billing, Pricing, and Support
