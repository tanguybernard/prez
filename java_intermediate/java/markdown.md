# Java Intermediate

Tanguy Bernard

-----

<div style="color: #dc3f00; font-size: xxx-large">
Input - Output
</div>

---

## Definition

Java's Input/Output (I/O) system is used for managing data flow between a program and external sources or destinations, such as files, the console, or network sockets.

---

## Concepts

- Input: Reading data from a source (e.g., file, keyboard, network).
- Output: Writing data to a destination (e.g., file, screen, network).
- Streams: Abstract representations of data flow, used for reading and writing data sequentially.

---


### Schema


![Input,Output](./java/assets/input-output.jpg)


<div style="font-size:small;color: #7d889a">
source: https://dh-cologne.github.io/java-wegweiser/articles/IO.html
</div>

---

### Scanner


```java
import java.util.Scanner;

public class KeyboardInputExample {
  public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);

    System.out.print("Enter your name: ");
    String name = scanner.nextLine();
    System.out.println("Hello, " + name + "!");
    
  }
}
```

---

## Api

Java provides a comprehensive API for I/O operations through the java.io package.

And java.nio offering non-blocking I/O capabilities.


---

### File Input and Output

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class FileReadExample {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("example.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

###  Stream

---
### Byte Streams for Binary Files

Example: Copying a Binary File


```java
import java.io.*;

public class FileCopyExample {
    public static void main(String[] args) {
        try (FileInputStream input = new FileInputStream("source.jpg");
             FileOutputStream output = new FileOutputStream("destination.jpg")) {
             
            byte[] buffer = new byte[1024];
            int bytesRead;
            while ((bytesRead = input.read(buffer)) != -1) {
                output.write(buffer, 0, bytesRead);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```


---

### Using java.nio

```java
import java.nio.file.*;
import java.io.IOException;

public class NioExample {
    public static void main(String[] args) {
        try {
            String content = Files.readString(Path.of("example.txt"));
            System.out.println(content);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



-----

<div style="color: #dc3f00; font-size: xxx-large">
Serialization
</div>

--- 

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

-----

<div style="color: #dc3f00; font-size: xxx-large">
Sécurité et Conformité
</div>


---

### User Permissions and Access
<ul style="font-size: xx-large">
<li><b>Compte</b>: Un conteneur qui contient des ressources, des utilisateurs, des paramètres.</li>
<li><b>Compte root user</b>: Celui qui controle les ressources du compte.</li>
<li><b>Utilisateur</b>: Une personne ou une application qui intéragit avec les services AWS.</li>
<li><b>Policies</b>: Permissions  d'un utilisateur ou d'un groupe.</li>
<li><b>Groupe</b>: Une collection d'utilisateurs</li>
<li><b>Roles</b>: Permissions temporaire sur du plus ou moins long terme.</li>
<li><b>Organizations</b>: Service de gestion de comptes (Organisation par pole par ex. Web, Data, Rh...)</li>
</ul>
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
<div style="color: #dc3f00; font-size: xxx-large">
Billing, Pricing, and Support
</div>

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

