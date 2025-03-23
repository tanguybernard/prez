<!-- presentation2.md -->
# Java Ecosystem

---


## 1. Project Management with Maven and pom.xml

----

### Maven :

Maven is an open-source build automation and project management tool primarily used for Java projects. It simplifies project management by automating common tasks such as dependency management, compilation, packaging, testing, and deployment.

----

### Basic structure :

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.mycompany</groupId>
    <artifactId>my-project</artifactId>
    <version>1.0.0</version>
</project>
```
- `modelVersion`: POM (Project Object Model) Version
- `groupId`: Identifies the organization (like a reversed domain name)
- `artifactId`: Project name
- `version`: Current project version

----

### **Dependency Management**:

```xml

<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>
  

```
- Maven automatically downloads libraries from public repositories
- Scopes (`test`, `compile`, `runtime`) control dependency availability

----

### **Best practices**:

- Use `<dependencyManagement>` to centralize versions
- Maintain a standard project structure (src/main/java, src/test/java)
- Use **`mvn clean install`** to build the project

---

## 2. Database Access

----

### **JDBC** (Java Database Connectivity):
- Low-level API to execute SQL queries directly
- Requires manual management of connections and results
- Simple example:
```java
Connection conn = DriverManager.getConnection(url, user, password);
Statement stmt = conn.createStatement();
ResultSet rs = stmt.executeQuery("SELECT * FROM customers");
```

----

### **JPA** (Java Persistence API):
- ORM (Object-Relational Mapping) standard to map Java objects to tables
- Key annotations:
    - `@Entity`: Persistent class
    - `@Id`: Primary key
    - `@OneToMany`: Relationships between entities

    
----

**Hibernate**:
- Popular JPA implementation
- Configuration via `persistence.xml` or Spring properties
- Manages caching, lazy loading, and transactions


----

### Example

```java
import javax.persistence.*;

@Entity
@Table(name = "employees")
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "first_name", nullable = false)
    private String firstName;

    public Employee() {
        // Default constructor required by JPA
    }
}
```

----

**Spring Data JPA**:


```java
public interface UserJpaRepository extends JpaRepository {
    List findByLastName(String lastName);
}
```

- Simplifies CRUD operations
- Automatically generates implementations

---

## 3. REST API Development

----

**Basic principles**:
- Stateless client-server architecture
- Uses HTTP verbs (GET, POST, PUT, DELETE)
- Returns data in JSON/XML format

----

**Example with Spring Boot**:

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @Autowired
    private UserRepository userRepository;

    @GetMapping
    public List getAllUsers() {
        return userRepository.findAll();
    }

    @PostMapping
    public User createUser(@RequestBody User user) {
        return userRepository.save(user);
    }
}
```

- `@RestController` marks the class as an API controller
- `@RequestMapping` defines the base path
- HTTP annotations map methods to operations

---

## 4. Other Essential Elements
- **Unit Testing**: JUnit 5 + Mockito
- **Security**: Spring Security for authentication
- **Documentation**: Swagger/OpenAPI for API documentation
