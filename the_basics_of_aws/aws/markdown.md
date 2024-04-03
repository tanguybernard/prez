# Basics of AWS

Tanguy Bernard

-----

## Cloud Concept

Le cloud est un vaste réseau de serveurs distants éparpillés tout autour de la planète, reliés entre eux, et destinés à fonctionner comme un écosystème unique.

---

### Modèles de cloud computing


![Iaas, Paas, Saas](./aws/assets/iaas_paas_saas.jpg)


<div style="font-size:small">
source: https://cloud.google.com/learn/paas-vs-iaas-vs-saas?hl=fr
</div>

---

### Infrastructure as a Service

Vous louez le matériel sur lequel exécuter votre application, mais vous êtes responsable de la gestion de l'OS, de l'environnement d'exécution et du scaling, ainsi que de toutes les données.

<div style="font-size:medium; color: #7d889a">
Exemple: Amazon Elastic Compute Cloud (EC2)
</div>
---

### Containers as a Service (CAAS)

Considérer comme une sous catégorie du Iaas. 

A la différence que la ressource fondamentale sont les containers plutôt que les machines virtuelles ou les systèmes d'hébergement matériels.

<div style="font-size:medium; color: #7d889a">
Exemple: Amazon Elastic Container Service (ECS)
</div>

---

###  Platform as a Service (PAAS)

Le fournisseur s'occupent de l'OS et de l'environnement d'execution (Java, Node, Python, Go...)

Vous pouvez vous concentrer sur le déploiement et la gestion de vos applications.

<div style="font-size:medium; color: #7d889a">
Exemple: AWS Elastic Beanstalk
</div>

---
### Beanstalk

![aws-beanstalk-platform.png](./aws/assets/aws-beanstalk-platform.png)


---

### Function as a Service (Faas)

Vous permet d’exécuter du code en réponse à des événements !

Priorité au code et non à l’infrastructure : Avec le FaaS, vous pouvez diviser le serveur en fonctions qui peuvent être mises à l’échelle automatiquement !

<div style="font-size:medium; color: #7d889a">
Exemple: AWS Lambda
</div>

---

### Software as a Service (Saas)

Vous payez pour utiliser une application complète à des fins spécifiques. Elle est gérée, entretenue et sécurisée par le fournisseur cloud. Cependant, vous êtes responsable de la gestion de vos propres données.

<div style="font-size:medium; color: #7d889a">
Exemple: Amazon Cognito
</div>

---

### Cloud Based, On-Premise And Hybrid

- Cloud: 
    - Public: Hebergé par un fournisseur, les ressources peuvent être redistribuées à d'autres clients.
    - Privé: Il peut soit se situer au sein d'une organisation, soit être géré à distance par un tiers et accessible sur Internet (il n'est partagé avec personne)
- On-Premise: Hébergement de son infrastructure IT
- Hybrid: Une combinaison d'au moins 2 environnements de cloud computing

---

### Benefits of AWS cloud

Remplace les dépenses d'investissement initiales (CAPEX) par de faibles dépenses d'exploitation variables (OPEX).

<div style="color: #c141cb">
Vous ne payez que ce que vous utilisez !
</div>

---

### Framework d'adoption du Cloud AWS (AWS CAF)

Votre préparation au cloud via différentes perspectives:

- Entreprise
- Personnes
- Gouvenance
- Plateforme
- Sécurité
- Opérations

---


### Pour se lancer

- <b>Envisager</b>: Identifiez et hiérarchisez les occasions de transformation
- <b>Aligner</b>: Identifiez les déficits de fonctionnalités et les dépendances inter-organisationnelles.
- <b>Lancer</b>: Menez des projets pilotes en production et démontrez la valeur opérationnelle progressive.
- <b>Mettre à l'échelle</b>: Étendez les pilotes et la valeur opérationnelle à l'échelle souhaitée


Exemple:  Tipee ?

---

### AWS Well-Architected

Le cadre AWS Well-Architected Framework décrit les concepts clés, les principes de conception et les bonnes pratiques architecturales pour concevoir et exécuter des charges de travail dans le cloud.

---

### Les six piliers

---

### Pilier Excellence opérationnelle

- Organisation
- Préparation
- Opération
- ...

---

### Pilier Sécurité

- Partage des responsabilités
- IAM
- Protection des infrastructures
- ...

---

### Pilier Fiabilité

- Conception de systèmes distribués
- Backup de données
- Plan de reprise après sinistre
- ...

---

### Pilier Efficacité des performances

- Devenir mondial en quelques minutes
- Utilisation des architectures sans serveur
- ...

---

### Pilier Optimisation des coûts

- Mesurer l'efficacité globale
- Adopter un modèle de consommation
- Mesurer le retour sur investissement (ROI)
- ...

---

### Pilier Développement durable

- Mesure de l'impact de la charge de travail
- Maximisation de l'utilisation des ressources
- Fixer des objectifs de durabilité
- ...

---

### AWS Global Infrastructure



<img src="./aws/assets/Region_AZ.png" alt="Texte alternatif" style="width:50vh; height:40vh; border:2px solid black;">

<div style="font-size:medium; color: #7d889a">
source: https://aws.amazon.com/fr/about-aws/global-infrastructure/regions_az/
</div>


---

### Les zones de disponibilité (AZ)
<div style="font-size:medium;">
Les zones de disponibilité sont physiquement séparées par une distance significative, c'est-à-dire plusieurs kilomètres, de toute autre zone de disponibilité.
</div>

<img src="./aws/assets/regions-and-zones.png" alt="Texte alternatif" style="width:50vh; height:40vh; border:2px solid black;">


<div style="font-size:medium; color: #7d889a">
source: https://aws.amazon.com/fr/about-aws/global-infrastructure/regions_az/
</div>

-----

### Cloud Technology and Services

- Machine Learning
- Calcul
- Stockage
- Outils pour les développeurs
- Base de données
- Web et mobile front
- Analyses
- Sécurité, identité et conformité


---

### Calcul

- Elastic Compute Cloud (EC2): Le produit phare, le serveur virtuel.
- Lambda: Service de calcul d'événement sans serveur (serverless).
- Elastic Container Service (ECS): Gestion de conteneurs.
- Elastic Kubernetes Service (EKS): Service Kubernetes géré.
- Fargate: Gestion de conteneurs sans serveur

Note: ECS tu gère provision les instances ec2 sur lequel tourne les conteneurs. Avec fargate tu ne gères pas les instances EC2.

---

### Stockage

<ul style="font-size: xx-large">
<li>Elastic Block Store (EBS): Disque dur SDD ou HDD.</li>
<li>Simple Storage Service (S3): Stockage d'objets (pdf, photos, vidéos...)</li>
<li>Elastic File System (EFS): Stockage très elastique et qui se partage entre différentes instances EC2.</li>
</ul>

---

### S3


<img src="./aws/assets/s3_classes.jpg" alt="Texte alternatif" style="width:45vh; height:65vh; border:2px solid black;">



---

### Base de données

<ul style="font-size: xx-large">
<li><b>Relational Database Service</b> (RDS): Mysql, PostgreSQL, Amazon Aurora, Oracle, Microsoft SQL Server...</li>
<li><b>Aurora</b>: Entierement managé pour MySQL et PostgreSQL</li>
<li><b>DynamoDB</b>: Clé/valeur</li>
<li><b>Redshift</b> (basé sur PostgreSQL): Grands volumes de données</li>
<li><b>Neptune</b>: Base de données graphe</li>
<li><b>Amazon Managed Blockchain</b>: Créer et gérer des réseaux blockchain.</li>
<li><b>Quantum Ledger Database</b> (Amazon QLDB): Base de données de registre, c'est une chaîne de blocs constituant un journal transactionnel.</li>
<li><b>ElastiCache</b>: Service de stockage de données en mémoire et de mise en cache.</li>
</ul>

---


### Networking & Content Delivery
<ul style="font-size: xx-large">
<li><b>Virtual Private Cloud (VPC)</b>: Création d'un réseau virtuel isolé</li>
<li><b>Route 53</b>: DNS</li>
<li><b>CloudFront</b>: Content Delivery Network</li>
<li><b>Api Gateway</b>: Création d'API RESTful et WebSocket</li>
<li><b>Elastic Load Balancers (ELB)</b>: Distribution du traffic</li>
<li><b>Internet Gateway (IGW)</b>: Communication avec internet</li>
</ul>

---

### Autres

- Amazon Textract (Machine Learning)
- AWS Glue (Analytics): ETL
- Amazon Cognito (Security, Identity & Compliance)
- AWS AppSync: GraphQL API

---

## Sécurité et Conformité

---

### User Permissions and Access

- Compte: Un conteneur qui contient des ressources, des utilisateurs, des paramètres.
- Compte root user: Celui qui controle les ressources du compte.
- Utilisateur: Une personne ou une application qui intéragit avec les services AWS.
- Policies: Permissions  d'un utilisateur ou d'un groupe.
- Groupe: Une collection d'utilisateurs
- Roles: Permissions temporaire sur du plus ou moins long terme.
- Organizations: Service de gestion de comptes (Organisation par pole par ex. Web, Data, Rh...)

---

### Sécurité

- Amazon WAF: Web application firewall
- AWS Shield: Contre les attaques DDoS
- GuardDuty: Detection de menaces (intrusion, changement de conf, anomalies...)
- Amazon Inspector: Vulnérabilitées dans les applications
- AWS Key Management Service: Gestion de clés, chiffrement
- AWS Secrets Manager: Gestion de secrets (clés API, password), Rotation, Audit

---

### Focus ressources

- <b>VPC</b>: un réseau virtuel qui constitue une section du cloud isolée
- <b>Ressource</b>: Instance EC2, Lambda, S3, VPC...
- <b>Subnet</b>: Des segments d'un VPC
- <b>NACL</b>: Firewall au niveau du subnet
- <b>Security group</b>: contrôle le trafic autorisé à atteindre et à quitter les ressources


---

### Focus sur la sécurité des ressources


<img src="./aws/assets/NACLvsSG-Applied-VPC-1.png" alt="X-ray screenshot" style="width:60vh; height:50vh; ">


<div style="font-size:medium; color: #7d889a">
source: https://myaws.rocks/nacl-vs-security-group/
</div>

---

### Monitoring

- CloudWatch: CPU utilization, Nombre de requetes...
- CloudTrail: Traque l'activité des utilisateurs au sein de l'infra AWS
- Trusted Advisor: Outil qui inspecte et donne des conseils (cout, perf, secu...)
- AWS X-Ray: Analyse et debug vos apps

---

### x-Ray


<img src="./aws/assets/xray-getpost-trace-view.png" alt="X-ray screenshot" style="width:85vh; height:65vh; ">



-----

## Billing, Pricing, and Support

---

### Services

- AWS Pricing Calculator: Création d'une estimation
- AWS Budgets: Creation d'un budget
- Cost Explorer: Comprendre les couts


---

### Support plans


<img src="./aws/assets/support-plans.jpeg" alt="X-ray screenshot" style="width:85vh; height:65vh; ">

-----

## Conclusion 


- Échangez les dépenses initiales contre des dépenses variables.
- Bénéficiez d'économies d'échelle massives.
- Arrêtez de deviner les capacitées.
- Augmentez la vitesse et l'agilité.
- Arrêtez de dépenser de l'argent pour faire fonctionner et entretenir des centres de données.
- Devenez mondial en quelques minutes.

