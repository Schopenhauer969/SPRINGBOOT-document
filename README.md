# 🚀 Spring Boot — Beginner to Advanced

> A complete Spring Boot learning guide from **Beginner → Intermediate → Advanced**, with full Java code examples and explanations in **English 🇬🇧 + Khmer 🇰🇭**.

![Java](https://img.shields.io/badge/Java-17%2B-orange)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.1.1-brightgreen)
![Maven](https://img.shields.io/badge/Maven-3.6.3%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📚 Table of Contents

* [1. What is Spring Boot?](#1-what-is-spring-boot)
* [2. Why Spring Boot?](#2-why-spring-boot)
* [3. Prerequisites](#3-prerequisites)
* [4. Create Your First Project](#4-create-your-first-project)
* [5. Project Structure](#5-project-structure)
* [6. Hello World](#6-hello-world)
* [7. Spring Boot Application](#7-spring-boot-application)
* [8. REST API](#8-rest-api)
* [9. HTTP Methods](#9-http-methods)
* [10. Path Variable](#10-path-variable)
* [11. Request Parameter](#11-request-parameter)
* [12. Request Body](#12-request-body)
* [13. DTO](#13-dto)
* [14. Service Layer](#14-service-layer)
* [15. Repository Layer](#15-repository-layer)
* [16. Database with JPA](#16-database-with-jpa)
* [17. MySQL](#17-mysql)
* [18. CRUD API](#18-crud-api)
* [19. Validation](#19-validation)
* [20. Exception Handling](#20-exception-handling)
* [21. Configuration](#21-configuration)
* [22. Profiles](#22-profiles)
* [23. Logging](#23-logging)
* [24. Lombok](#24-lombok)
* [25. Transactions](#25-transactions)
* [26. Relationships](#26-relationships)
* [27. Pagination and Sorting](#27-pagination-and-sorting)
* [28. Spring Security](#28-spring-security)
* [29. Password Hashing](#29-password-hashing)
* [30. JWT Authentication](#30-jwt-authentication)
* [31. Role-Based Authorization](#31-role-based-authorization)
* [32. CORS](#32-cors)
* [33. Testing](#33-testing)
* [34. Integration Testing](#34-integration-testing)
* [35. Actuator](#35-actuator)
* [36. OpenAPI / Swagger](#36-openapi--swagger)
* [37. RestClient](#37-restclient)
* [38. WebClient](#38-webclient)
* [39. Async Processing](#39-async-processing)
* [40. Scheduling](#40-scheduling)
* [41. Caching](#41-caching)
* [42. Events](#42-events)
* [43. File Upload](#43-file-upload)
* [44. Docker](#44-docker)
* [45. Docker Compose](#45-docker-compose)
* [46. Production Configuration](#46-production-configuration)
* [47. Layered Architecture](#47-layered-architecture)
* [48. Clean Architecture](#48-clean-architecture)
* [49. Microservices](#49-microservices)
* [50. Production Checklist](#50-production-checklist)
* [51. Recommended Learning Path](#51-recommended-learning-path)

---

# 1. What is Spring Boot?

## English

Spring Boot is a Java framework used to build:

* REST APIs
* Web applications
* Microservices
* Enterprise applications
* Backend systems
* Cloud applications

Spring Boot simplifies Spring development by providing:

* Auto-configuration
* Embedded servers
* Starter dependencies
* External configuration
* Production features
* Testing support

## ខ្មែរ

Spring Boot គឺជា Framework របស់ Java សម្រាប់បង្កើត៖

* REST API
* Web Application
* Microservices
* Backend
* Enterprise Application
* Cloud Application

Spring Boot ជួយកាត់បន្ថយ Configuration ដែលយើងត្រូវសរសេរដោយខ្លួនឯង។

---

# 2. Why Spring Boot?

## English

Without Spring Boot, configuring a Spring application can require a lot of manual configuration.

Spring Boot provides sensible defaults.

```text
Java
  ↓
Spring Framework
  ↓
Spring Boot
  ↓
REST API
  ↓
Database
  ↓
Security
  ↓
Production
```

## ខ្មែរ

Spring Framework មានសមត្ថភាពខ្លាំង ប៉ុន្តែ Spring Boot ធ្វើឱ្យការបង្កើត Application ងាយស្រួលជាងមុន។

---

# 3. Prerequisites

You should know basic:

* Java
* OOP
* Classes
* Interfaces
* Exceptions
* Collections
* Maven
* HTTP
* JSON
* SQL

Recommended:

```text
Java 17+
Maven 3.6.3+
Git
IDE
Postman
MySQL
Docker
```

Spring Boot 4.1.1 requires Java 17 or newer.

Check Java:

```bash
java -version
```

Check Maven:

```bash
mvn -version
```

---

# 4. Create Your First Project

The easiest way is Spring Initializr.

Open:

```text
https://start.spring.io
```

Choose:

```text
Project: Maven
Language: Java
Spring Boot: 4.1.1
Packaging: Jar
Java: 17
```

Add:

```text
Spring Web MVC
```

Spring Boot's official documentation recommends Spring Initializr for quickly generating projects.

---

# 5. Project Structure

A clean beginner project:

```text
springboot-demo/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/demo/
│   │   │       ├── DemoApplication.java
│   │   │       ├── controller/
│   │   │       ├── service/
│   │   │       ├── repository/
│   │   │       ├── entity/
│   │   │       ├── dto/
│   │   │       ├── exception/
│   │   │       └── config/
│   │   │
│   │   └── resources/
│   │       ├── application.properties
│   │       └── static/
│   │
│   └── test/
│
├── pom.xml
└── README.md
```

## ខ្មែរ

ការបែងចែក Folder ជា Layer ជួយឱ្យ Project ងាយអាន និងងាយថែទាំ។

---

# 6. Hello World

## `DemoApplication.java`

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

## `HelloController.java`

```java
package com.example.demo.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/")
    public String hello() {
        return "Hello, Spring Boot!";
    }
}
```

Run:

```bash
mvn spring-boot:run
```

Open:

```text
http://localhost:8080/
```

Response:

```text
Hello, Spring Boot!
```

---

# 7. Spring Boot Application

The main annotation:

```java
@SpringBootApplication
```

combines important Spring Boot configuration behavior.

```java
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

## ខ្មែរ

`@SpringBootApplication` គឺជា Annotation សំខាន់សម្រាប់ចាប់ផ្តើម Spring Boot Application។

---

# 8. REST API

A REST controller:

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @GetMapping
    public String getUsers() {
        return "All users";
    }
}
```

Request:

```http
GET /api/users
```

Response:

```text
All users
```

---

# 9. HTTP Methods

The main HTTP methods are:

| Method | Purpose        |
| ------ | -------------- |
| GET    | Read           |
| POST   | Create         |
| PUT    | Update         |
| PATCH  | Partial update |
| DELETE | Delete         |

Example:

```java
@RestController
@RequestMapping("/api/products")
public class ProductController {

    @GetMapping
    public String getAll() {
        return "GET";
    }

    @PostMapping
    public String create() {
        return "POST";
    }

    @PutMapping("/{id}")
    public String update(@PathVariable Long id) {
        return "PUT " + id;
    }

    @PatchMapping("/{id}")
    public String patch(@PathVariable Long id) {
        return "PATCH " + id;
    }

    @DeleteMapping("/{id}")
    public String delete(@PathVariable Long id) {
        return "DELETE " + id;
    }
}
```

---

# 10. Path Variable

URL:

```text
/api/users/10
```

Code:

```java
@GetMapping("/{id}")
public String getUser(@PathVariable Long id) {
    return "User ID: " + id;
}
```

Response:

```text
User ID: 10
```

## ខ្មែរ

`@PathVariable` ប្រើសម្រាប់យកតម្លៃពី URL។

---

# 11. Request Parameter

Request:

```text
/api/users?name=Heng
```

Code:

```java
@GetMapping
public String getUser(
        @RequestParam String name
) {
    return "Hello " + name;
}
```

Response:

```text
Hello Heng
```

Optional parameter:

```java
@GetMapping
public String search(
        @RequestParam(defaultValue = "") String name
) {
    return name;
}
```

---

# 12. Request Body

Create DTO:

```java
package com.example.demo.dto;

public record UserRequest(
        String name,
        String email
) {
}
```

Controller:

```java
@PostMapping
public UserRequest create(
        @RequestBody UserRequest request
) {
    return request;
}
```

JSON:

```json
{
  "name": "Heng",
  "email": "heng@example.com"
}
```

---

# 13. DTO

DTO means:

```text
Data Transfer Object
```

Example:

```java
public record UserResponse(
        Long id,
        String name,
        String email
) {
}
```

Request DTO:

```java
public record UserRequest(
        String name,
        String email
) {
}
```

## Why DTO?

Do not expose database entities directly in every API.

Better:

```text
Client
  ↓
Request DTO
  ↓
Controller
  ↓
Service
  ↓
Entity
  ↓
Repository
  ↓
Database
```

## ខ្មែរ

DTO ជួយការពារ Entity និងកំណត់ថា API អាចទទួល/បញ្ជូន Data អ្វីខ្លះ។

---

# 14. Service Layer

```java
package com.example.demo.service;

import org.springframework.stereotype.Service;

@Service
public class UserService {

    public String getUser() {
        return "User from service";
    }
}
```

Controller:

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping
    public String getUser() {
        return userService.getUser();
    }
}
```

## Dependency Injection

Spring creates the `UserService` object and injects it into the controller.

## ខ្មែរ

Dependency Injection មានន័យថា Spring ជាអ្នកបង្កើត Object ហើយបញ្ចូល Object ទៅកន្លែងដែលត្រូវការ។

---

# 15. Repository Layer

```java
package com.example.demo.repository;

import com.example.demo.entity.User;
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository
        extends JpaRepository<User, Long> {
}
```

You automatically get:

```java
findAll()
findById()
save()
deleteById()
count()
existsById()
```

---

# 16. Database with JPA

Add dependencies:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

Entity:

```java
package com.example.demo.entity;

import jakarta.persistence.*;

@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;

    @Column(nullable = false, unique = true)
    private String email;

    public User() {
    }

    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    public Long getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

---

# 17. MySQL

Add MySQL driver:

```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <scope>runtime</scope>
</dependency>
```

`application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/springboot_db
spring.datasource.username=root
spring.datasource.password=password

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

Create database:

```sql
CREATE DATABASE springboot_db;
```

## Warning

Do not use:

```properties
spring.jpa.hibernate.ddl-auto=create
```

in production unless you explicitly understand its destructive behavior.

Recommended production approach:

```text
Flyway
```

or:

```text
Liquibase
```

---

# 18. CRUD API

## Entity

```java
@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @Column(unique = true, nullable = false)
    private String email;

    public User() {
    }

    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    public Long getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

## Repository

```java
public interface UserRepository
        extends JpaRepository<User, Long> {
}
```

## Service

```java
@Service
public class UserService {

    private final UserRepository repository;

    public UserService(UserRepository repository) {
        this.repository = repository;
    }

    public List<User> findAll() {
        return repository.findAll();
    }

    public User findById(Long id) {
        return repository.findById(id)
                .orElseThrow(() ->
                        new RuntimeException("User not found"));
    }

    public User create(User user) {
        return repository.save(user);
    }

    public User update(Long id, User request) {

        User user = findById(id);

        user.setName(request.getName());
        user.setEmail(request.getEmail());

        return repository.save(user);
    }

    public void delete(Long id) {
        User user = findById(id);
        repository.delete(user);
    }
}
```

## Controller

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    private final UserService service;

    public UserController(UserService service) {
        this.service = service;
    }

    @GetMapping
    public List<User> findAll() {
        return service.findAll();
    }

    @GetMapping("/{id}")
    public User findById(@PathVariable Long id) {
        return service.findById(id);
    }

    @PostMapping
    public User create(@RequestBody User user) {
        return service.create(user);
    }

    @PutMapping("/{id}")
    public User update(
            @PathVariable Long id,
            @RequestBody User user
    ) {
        return service.update(id, user);
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> delete(
            @PathVariable Long id
    ) {
        service.delete(id);

        return ResponseEntity.noContent().build();
    }
}
```

---

# 19. Validation

Add:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

DTO:

```java
package com.example.demo.dto;

import jakarta.validation.constraints.Email;
import jakarta.validation.constraints.NotBlank;
import jakarta.validation.constraints.Size;

public record UserRequest(

        @NotBlank(message = "Name is required")
        @Size(min = 2, max = 100)
        String name,

        @NotBlank(message = "Email is required")
        @Email(message = "Invalid email")
        String email

) {
}
```

Controller:

```java
@PostMapping
public User create(
        @Valid @RequestBody UserRequest request
) {
    return service.create(request);
}
```

## ខ្មែរ

Validation គឺសម្រាប់ពិនិត្យថា User បញ្ចូល Data ត្រឹមត្រូវឬអត់។

---

# 20. Exception Handling

Custom exception:

```java
package com.example.demo.exception;

public class UserNotFoundException
        extends RuntimeException {

    public UserNotFoundException(Long id) {
        super("User not found: " + id);
    }
}
```

Global handler:

```java
package com.example.demo.exception;

import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.*;

import java.time.LocalDateTime;
import java.util.Map;

@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public Map<String, Object> handleUserNotFound(
            UserNotFoundException exception
    ) {
        return Map.of(
                "timestamp", LocalDateTime.now(),
                "status", 404,
                "error", "Not Found",
                "message", exception.getMessage()
        );
    }
}
```

Now:

```java
throw new UserNotFoundException(id);
```

returns:

```json
{
  "timestamp": "2026-09-13T20:00:00",
  "status": 404,
  "error": "Not Found",
  "message": "User not found: 100"
}
```

---

# 21. Configuration

`application.properties`:

```properties
server.port=8080

spring.application.name=my-api

app.name=My Application
app.version=1.0.0
```

Read property:

```java
@Component
public class AppConfig {

    @Value("${app.name}")
    private String appName;

    public String getAppName() {
        return appName;
    }
}
```

Better for groups of settings:

```java
@ConfigurationProperties(prefix = "app")
public record AppProperties(
        String name,
        String version
) {
}
```

---

# 22. Profiles

Create:

```text
application.properties
application-dev.properties
application-prod.properties
```

Development:

```properties
spring.profiles.active=dev
```

`application-dev.properties`:

```properties
server.port=8080
spring.jpa.show-sql=true
```

`application-prod.properties`:

```properties
server.port=8080
spring.jpa.show-sql=false
```

Run production profile:

```bash
java -jar app.jar --spring.profiles.active=prod
```

---

# 23. Logging

Use SLF4J:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

@Service
public class UserService {

    private static final Logger log =
            LoggerFactory.getLogger(UserService.class);

    public void execute() {
        log.info("Executing user service");
        log.warn("This is a warning");
        log.error("Something went wrong");
    }
}
```

Never log:

```text
password
JWT token
credit card
secret key
private credentials
```

---

# 24. Lombok

Add:

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
</dependency>
```

Example:

```java
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@Entity
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    private String email;
}
```

Lombok reduces boilerplate.

For educational projects, manually writing constructors/getters/setters can make Java fundamentals easier to understand.

---

# 25. Transactions

Use:

```java
@Transactional
```

Example:

```java
@Service
public class OrderService {

    private final OrderRepository orderRepository;
    private final PaymentRepository paymentRepository;

    public OrderService(
            OrderRepository orderRepository,
            PaymentRepository paymentRepository
    ) {
        this.orderRepository = orderRepository;
        this.paymentRepository = paymentRepository;
    }

    @Transactional
    public void createOrder() {

        Order order = new Order();
        orderRepository.save(order);

        Payment payment = new Payment();
        paymentRepository.save(payment);
    }
}
```

If an exception occurs, the transaction can roll back according to Spring transaction semantics.

## ខ្មែរ

Transaction មានន័យថា Operations ជាច្រើនត្រូវបានគ្រប់គ្រងជាក្រុម។

```text
Operation A
Operation B
Operation C

All success → COMMIT

One fails → ROLLBACK
```

---

# 26. Relationships

## One-to-Many

```java
@Entity
public class Department {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToMany(mappedBy = "department")
    private List<Employee> employees = new ArrayList<>();
}
```

Employee:

```java
@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;
}
```

Relationship:

```text
Department
    |
    | 1
    |
    | *
 Employee
```

Other relationships:

```text
@OneToOne
@OneToMany
@ManyToOne
@ManyToMany
```

---

# 27. Pagination and Sorting

Repository:

```java
public interface UserRepository
        extends JpaRepository<User, Long> {
}
```

Controller:

```java
@GetMapping
public Page<User> getUsers(
        @PageableDefault(size = 10)
        Pageable pageable
) {
    return repository.findAll(pageable);
}
```

Request:

```text
GET /api/users?page=0&size=10&sort=name,asc
```

Response contains:

```json
{
  "content": [],
  "totalElements": 100,
  "totalPages": 10,
  "size": 10,
  "number": 0
}
```

---

# 28. Spring Security

Add:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

Spring Security secures web applications by default when it is on the classpath.

Basic configuration:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    SecurityFilterChain securityFilterChain(
            HttpSecurity http
    ) throws Exception {

        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/public/**")
                .permitAll()
                .anyRequest()
                .authenticated()
            )
            .httpBasic(Customizer.withDefaults());

        return http.build();
    }
}
```

Public endpoint:

```java
@GetMapping("/public/hello")
public String hello() {
    return "Public";
}
```

Protected endpoint:

```java
@GetMapping("/private/hello")
public String privateHello() {
    return "Private";
}
```

---

# 29. Password Hashing

Never store:

```text
password123
```

as plain text.

Use BCrypt:

```java
@Bean
PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder();
}
```

Encode:

```java
String encoded =
        passwordEncoder.encode("password123");
```

Verify:

```java
boolean valid =
        passwordEncoder.matches(
                "password123",
                encoded
        );
```

---

# 30. JWT Authentication

For JWT resource-server APIs, add:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-resource-server</artifactId>
</dependency>
```

Spring Security supports JWT and opaque bearer tokens for OAuth 2.0 Resource Server applications.

Configuration:

```yaml
spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: https://your-auth-server.example.com
```

Security:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    SecurityFilterChain securityFilterChain(
            HttpSecurity http
    ) throws Exception {

        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/public/**")
                .permitAll()
                .anyRequest()
                .authenticated()
            )
            .oauth2ResourceServer(
                oauth2 -> oauth2.jwt(Customizer.withDefaults())
            );

        return http.build();
    }
}
```

Request:

```http
GET /api/users
Authorization: Bearer YOUR_ACCESS_TOKEN
```

> Important: Spring Security Resource Server validates bearer tokens; your authorization server is responsible for issuing tokens. Spring Security does not itself provide a general endpoint for minting JWT access tokens.

---

# 31. Role-Based Authorization

Enable method security:

```java
@Configuration
@EnableMethodSecurity
public class SecurityConfig {
}
```

Controller:

```java
@PreAuthorize("hasRole('ADMIN')")
@DeleteMapping("/{id}")
public void delete(
        @PathVariable Long id
) {
    service.delete(id);
}
```

Another:

```java
@PreAuthorize("hasAnyRole('USER', 'ADMIN')")
@GetMapping
public List<User> users() {
    return service.findAll();
}
```

Concept:

```text
USER
 ├── READ
 └── UPDATE

ADMIN
 ├── READ
 ├── UPDATE
 └── DELETE
```

---

# 32. CORS

Example:

```java
@Configuration
public class CorsConfig {

    @Bean
    WebMvcConfigurer corsConfigurer() {

        return new WebMvcConfigurer() {

            @Override
            public void addCorsMappings(
                    CorsRegistry registry
            ) {

                registry.addMapping("/api/**")
                        .allowedOrigins(
                                "http://localhost:3000"
                        )
                        .allowedMethods(
                                "GET",
                                "POST",
                                "PUT",
                                "PATCH",
                                "DELETE"
                        );
            }
        };
    }
}
```

Do not blindly use:

```java
.allowedOrigins("*")
```

for sensitive production APIs.

---

# 33. Testing

Spring Boot provides testing support through its test starter.

Add:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

Unit test:

```java
class CalculatorTest {

    @Test
    void shouldAddNumbers() {

        int result = 10 + 20;

        assertEquals(30, result);
    }
}
```

Run:

```bash
mvn test
```

---

# 34. Integration Testing

Example:

```java
@SpringBootTest
class DemoApplicationTests {

    @Test
    void contextLoads() {
    }
}
```

This verifies that the Spring application context can start.

---

# 35. Actuator

Add:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Configuration:

```properties
management.endpoints.web.exposure.include=health,info,metrics
```

Health endpoint:

```text
GET /actuator/health
```

Example:

```json
{
  "status": "UP"
}
```

Useful endpoints include:

```text
/actuator/health
/actuator/info
/actuator/metrics
```

Do not expose sensitive actuator endpoints publicly without appropriate security.

---

# 36. OpenAPI / Swagger

A common approach is `springdoc-openapi`.

Maven dependency:

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.8.13</version>
</dependency>
```

Example controller:

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @Operation(
            summary = "Get all users",
            description = "Returns all users"
    )
    @GetMapping
    public List<User> getUsers() {
        return service.findAll();
    }
}
```

Typical Swagger UI URL:

```text
http://localhost:8080/swagger-ui.html
```

> Check the library's compatibility matrix before upgrading versions independently of Spring Boot.

---

# 37. RestClient

For calling another HTTP API:

```java
@Configuration
public class HttpConfig {

    @Bean
    RestClient restClient() {
        return RestClient.builder()
                .baseUrl("https://api.example.com")
                .build();
    }
}
```

Service:

```java
@Service
public class ExternalService {

    private final RestClient restClient;

    public ExternalService(RestClient restClient) {
        this.restClient = restClient;
    }

    public String getData() {

        return restClient.get()
                .uri("/users")
                .retrieve()
                .body(String.class);
    }
}
```

---

# 38. WebClient

For reactive/non-blocking HTTP clients:

```java
@Configuration
public class WebClientConfig {

    @Bean
    WebClient webClient() {
        return WebClient.builder()
                .baseUrl("https://api.example.com")
                .build();
    }
}
```

Use:

```java
@Service
public class ExternalService {

    private final WebClient webClient;

    public ExternalService(WebClient webClient) {
        this.webClient = webClient;
    }

    public Mono<String> getData() {

        return webClient.get()
                .uri("/users")
                .retrieve()
                .bodyToMono(String.class);
    }
}
```

---

# 39. Async Processing

Enable async:

```java
@Configuration
@EnableAsync
public class AsyncConfig {
}
```

Service:

```java
@Service
public class EmailService {

    @Async
    public void sendEmail() {

        System.out.println(
                "Sending email..."
        );
    }
}
```

Controller:

```java
@PostMapping("/send")
public String send() {

    emailService.sendEmail();

    return "Email processing started";
}
```

For production systems, consider dedicated queues such as:

```text
Kafka
RabbitMQ
AWS SQS
```

---

# 40. Scheduling

Enable:

```java
@Configuration
@EnableScheduling
public class SchedulingConfig {
}
```

Scheduled job:

```java
@Component
public class ReportJob {

    @Scheduled(fixedRate = 60000)
    public void run() {

        System.out.println(
                "Running report job..."
        );
    }
}
```

This runs approximately every:

```text
60 seconds
```

---

# 41. Caching

Add cache support:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```

Enable:

```java
@Configuration
@EnableCaching
public class CacheConfig {
}
```

Cache result:

```java
@Cacheable("users")
public User findById(Long id) {

    return repository.findById(id)
            .orElseThrow();
}
```

Clear cache:

```java
@CacheEvict(
        value = "users",
        key = "#id"
)
public void delete(Long id) {

    repository.deleteById(id);
}
```

For distributed production caching:

```text
Redis
```

is a common choice.

---

# 42. Events

Create event:

```java
public record UserCreatedEvent(
        Long userId
) {
}
```

Publish:

```java
@Service
public class UserService {

    private final ApplicationEventPublisher publisher;

    public UserService(
            ApplicationEventPublisher publisher
    ) {
        this.publisher = publisher;
    }

    public void createUser(User user) {

        // Save user...

        publisher.publishEvent(
                new UserCreatedEvent(user.getId())
        );
    }
}
```

Listener:

```java
@Component
public class UserEventListener {

    @EventListener
    public void handle(
            UserCreatedEvent event
    ) {

        System.out.println(
                "User created: " + event.userId()
        );
    }
}
```

---

# 43. File Upload

Controller:

```java
@RestController
@RequestMapping("/api/files")
public class FileController {

    @PostMapping
    public String upload(
            @RequestParam("file")
            MultipartFile file
    ) throws IOException {

        String filename =
                file.getOriginalFilename();

        Path path = Paths.get(
                "uploads",
                filename
        );

        Files.createDirectories(
                path.getParent()
        );

        Files.write(
                path,
                file.getBytes()
        );

        return filename;
    }
}
```

HTML:

```html
<form
    method="post"
    enctype="multipart/form-data"
    action="/api/files"
>
    <input type="file" name="file">

    <button type="submit">
        Upload
    </button>
</form>
```

Production considerations:

```text
File size limit
File type validation
Virus scanning
Unique filenames
Object storage
Access control
```

---

# 44. Docker

Create `Dockerfile`:

```dockerfile
FROM eclipse-temurin:17-jre

WORKDIR /app

COPY target/app.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
```

Build:

```bash
mvn clean package
```

Build image:

```bash
docker build -t springboot-app .
```

Run:

```bash
docker run -p 8080:8080 springboot-app
```

---

# 45. Docker Compose

`compose.yml`:

```yaml
services:

  mysql:
    image: mysql:8.4
    container_name: mysql
    environment:
      MYSQL_DATABASE: springboot_db
      MYSQL_ROOT_PASSWORD: password
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql

  app:
    build: .
    container_name: springboot-app
    depends_on:
      - mysql
    ports:
      - "8080:8080"
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://mysql:3306/springboot_db
      SPRING_DATASOURCE_USERNAME: root
      SPRING_DATASOURCE_PASSWORD: password

volumes:
  mysql_data:
```

Run:

```bash
docker compose up --build
```

Stop:

```bash
docker compose down
```

---

# 46. Production Configuration

Never hard-code secrets:

```properties
spring.datasource.password=MySecretPassword
```

Instead use environment variables:

```properties
spring.datasource.password=${DB_PASSWORD}
```

Run:

```bash
DB_PASSWORD=secret mvn spring-boot:run
```

Windows PowerShell:

```powershell
$env:DB_PASSWORD="secret"
mvn spring-boot:run
```

Use:

```text
Environment Variables
Secret Manager
Vault
Cloud Secret Manager
Kubernetes Secrets
```

for production secrets.

---

# 47. Layered Architecture

Recommended:

```text
Controller
    ↓
Service
    ↓
Repository
    ↓
Database
```

Example:

```text
src/main/java/com/example/app/

├── controller/
│   └── UserController.java
│
├── service/
│   └── UserService.java
│
├── repository/
│   └── UserRepository.java
│
├── entity/
│   └── User.java
│
├── dto/
│   ├── UserRequest.java
│   └── UserResponse.java
│
├── exception/
│   ├── UserNotFoundException.java
│   └── GlobalExceptionHandler.java
│
└── config/
    └── SecurityConfig.java
```

---

# 48. Clean Architecture

For larger applications:

```text
presentation
      ↓
application
      ↓
domain
      ↓
infrastructure
```

Example:

```text
src/main/java/com/example/app/

├── domain/
│   ├── model/
│   └── repository/
│
├── application/
│   ├── service/
│   └── usecase/
│
├── infrastructure/
│   ├── persistence/
│   ├── security/
│   └── external/
│
└── presentation/
    ├── controller/
    └── dto/
```

## ខ្មែរ

Clean Architecture មានគោលបំណងបំបែក Business Logic ចេញពី Database, Framework និង External API។

---

# 49. Microservices

Spring Boot can be used to build microservices.

Example:

```text
                    API Gateway
                         |
          +--------------+--------------+
          |              |              |
          ↓              ↓              ↓
      User Service   Order Service   Payment Service
          |              |              |
          ↓              ↓              ↓
       User DB        Order DB       Payment DB
```

Common technologies:

```text
Spring Boot
Spring Cloud
Spring Security
Kafka
RabbitMQ
Redis
Docker
Kubernetes
```

A microservice should have a clear responsibility.

Bad:

```text
One giant service doing everything
```

Better:

```text
User Service
Order Service
Payment Service
Notification Service
```

---

# 50. Production Checklist

Before deploying a Spring Boot application:

## Security

* [ ] HTTPS enabled
* [ ] Passwords hashed
* [ ] JWT/OAuth2 configured correctly
* [ ] CORS restricted
* [ ] Secrets not committed
* [ ] SQL injection protected
* [ ] Input validation enabled
* [ ] Actuator secured
* [ ] Authentication implemented
* [ ] Authorization implemented

## Database

* [ ] Database indexes reviewed
* [ ] Transactions configured
* [ ] Connection pool configured
* [ ] Migrations configured
* [ ] Backups configured
* [ ] Slow queries monitored

## API

* [ ] DTOs used
* [ ] Global exception handler
* [ ] Validation
* [ ] Pagination
* [ ] API documentation
* [ ] Correct HTTP status codes

## Performance

* [ ] Database queries optimized
* [ ] Caching where appropriate
* [ ] Pagination
* [ ] Connection pool tuned
* [ ] Async processing where appropriate

## Operations

* [ ] Health checks
* [ ] Metrics
* [ ] Logs
* [ ] Monitoring
* [ ] Alerting
* [ ] Docker image
* [ ] CI/CD

---

# 51. Recommended Learning Path

## 🟢 Beginner

Learn in this order:

```text
1. Java
2. Maven
3. Spring Boot
4. Dependency Injection
5. REST API
6. Controller
7. Service
8. Repository
9. DTO
10. HTTP
```

---

## 🟡 Intermediate

Then:

```text
11. JPA
12. Hibernate
13. MySQL/PostgreSQL
14. CRUD
15. Validation
16. Exception Handling
17. Transactions
18. Relationships
19. Pagination
20. Testing
```

---

## 🔴 Advanced

Then:

```text
21. Spring Security
22. JWT
23. OAuth2
24. Caching
25. Redis
26. Kafka
27. RabbitMQ
28. Async
29. Scheduling
30. Docker
31. Kubernetes
32. CI/CD
33. Observability
34. Microservices
35. Clean Architecture
36. System Design
```

---

# 🧠 Complete Spring Boot Request Flow

A professional REST API commonly looks like:

```text
Client
  |
  | HTTP Request
  ↓
Security Filter
  |
  ↓
Controller
  |
  ↓
DTO Validation
  |
  ↓
Service
  |
  ↓
Repository
  |
  ↓
JPA / Hibernate
  |
  ↓
Database
  |
  ↓
Repository
  |
  ↓
Service
  |
  ↓
Response DTO
  |
  ↓
Controller
  |
  | HTTP Response
  ↓
Client
```

---

# 📦 Complete Example Project

A recommended final structure:

```text
springboot-api/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/app/
│   │   │       │
│   │   │       ├── Application.java
│   │   │       │
│   │   │       ├── controller/
│   │   │       │   └── UserController.java
│   │   │       │
│   │   │       ├── service/
│   │   │       │   └── UserService.java
│   │   │       │
│   │   │       ├── repository/
│   │   │       │   └── UserRepository.java
│   │   │       │
│   │   │       ├── entity/
│   │   │       │   └── User.java
│   │   │       │
│   │   │       ├── dto/
│   │   │       │   ├── UserRequest.java
│   │   │       │   └── UserResponse.java
│   │   │       │
│   │   │       ├── exception/
│   │   │       │   ├── UserNotFoundException.java
│   │   │       │   └── GlobalExceptionHandler.java
│   │   │       │
│   │   │       └── config/
│   │   │           └── SecurityConfig.java
│   │   │
│   │   └── resources/
│   │       ├── application.yml
│   │       └── application-prod.yml
│   │
│   └── test/
│       └── java/
│
├── Dockerfile
├── compose.yml
├── pom.xml
└── README.md
```

---

# 📄 Complete `pom.xml`

For a basic REST + JPA + Validation + MySQL + Security application:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project
    xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://maven.apache.org/POM/4.0.0
        https://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>4.1.1</version>
        <relativePath/>
    </parent>

    <groupId>com.example</groupId>

    <artifactId>springboot-api</artifactId>

    <version>0.0.1-SNAPSHOT</version>

    <name>springboot-api</name>

    <description>
        Spring Boot REST API
    </description>

    <properties>

        <java.version>17</java.version>

    </properties>

    <dependencies>

        <!-- Web MVC / REST -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-webmvc</artifactId>
        </dependency>

        <!-- JPA -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>

        <!-- Validation -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
        </dependency>

        <!-- Security -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>

        <!-- MySQL -->
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <scope>runtime</scope>
        </dependency>

        <!-- Actuator -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <!-- Testing -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

    </dependencies>

    <build>

        <plugins>

            <plugin>
                <groupId>
                    org.springframework.boot
                </groupId>

                <artifactId>
                    spring-boot-maven-plugin
                </artifactId>
            </plugin>

        </plugins>

    </build>

</project>
```

Spring Boot's current starter documentation lists `spring-boot-starter-webmvc` as the MVC/Tomcat starter and identifies the older `spring-boot-starter-web` as deprecated in favor of it for the current generation.

---

# 📄 Complete `application.yml`

```yaml
spring:

  application:
    name: springboot-api

  datasource:
    url: jdbc:mysql://localhost:3306/springboot_db
    username: root
    password: ${DB_PASSWORD:password}

  jpa:
    hibernate:
      ddl-auto: update

    show-sql: false

    properties:
      hibernate:
        format_sql: true

server:

  port: 8080

management:

  endpoints:
    web:
      exposure:
        include:
          - health
          - info
          - metrics
```

---

# 📄 Complete Main Application

```java
package com.example.app;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {

        SpringApplication.run(
                Application.class,
                args
        );
    }
}
```

---

# 📄 Complete Entity

```java
package com.example.app.entity;

import jakarta.persistence.*;

@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(
            strategy = GenerationType.IDENTITY
    )
    private Long id;

    @Column(
            nullable = false,
            length = 100
    )
    private String name;

    @Column(
            nullable = false,
            unique = true,
            length = 255
    )
    private String email;

    public User() {
    }

    public User(
            String name,
            String email
    ) {
        this.name = name;
        this.email = email;
    }

    public Long getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

---

# 📄 Complete Repository

```java
package com.example.app.repository;

import com.example.app.entity.User;
import org.springframework.data.jpa.repository.JpaRepository;

import java.util.Optional;

public interface UserRepository
        extends JpaRepository<User, Long> {

    Optional<User> findByEmail(String email);
}
```

---

# 📄 Complete Request DTO

```java
package com.example.app.dto;

import jakarta.validation.constraints.Email;
import jakarta.validation.constraints.NotBlank;

public record UserRequest(

        @NotBlank(
                message = "Name is required"
        )
        String name,

        @NotBlank(
                message = "Email is required"
        )
        @Email(
                message = "Email must be valid"
        )
        String email

) {
}
```

---

# 📄 Complete Response DTO

```java
package com.example.app.dto;

public record UserResponse(

        Long id,

        String name,

        String email

) {
}
```

---

# 📄 Complete Service

```java
package com.example.app.service;

import com.example.app.dto.UserRequest;
import com.example.app.dto.UserResponse;
import com.example.app.entity.User;
import com.example.app.exception.UserNotFoundException;
import com.example.app.repository.UserRepository;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;

@Service
public class UserService {

    private final UserRepository repository;

    public UserService(
            UserRepository repository
    ) {
        this.repository = repository;
    }

    @Transactional(readOnly = true)
    public List<UserResponse> findAll() {

        return repository.findAll()
                .stream()
                .map(this::toResponse)
                .toList();
    }

    @Transactional(readOnly = true)
    public UserResponse findById(Long id) {

        User user = repository.findById(id)
                .orElseThrow(
                        () -> new UserNotFoundException(id)
                );

        return toResponse(user);
    }

    @Transactional
    public UserResponse create(
            UserRequest request
    ) {

        User user = new User(
                request.name(),
                request.email()
        );

        User saved =
                repository.save(user);

        return toResponse(saved);
    }

    @Transactional
    public UserResponse update(
            Long id,
            UserRequest request
    ) {

        User user = repository.findById(id)
                .orElseThrow(
                        () -> new UserNotFoundException(id)
                );

        user.setName(request.name());
        user.setEmail(request.email());

        return toResponse(user);
    }

    @Transactional
    public void delete(Long id) {

        User user = repository.findById(id)
                .orElseThrow(
                        () -> new UserNotFoundException(id)
                );

        repository.delete(user);
    }

    private UserResponse toResponse(
            User user
    ) {

        return new UserResponse(
                user.getId(),
                user.getName(),
                user.getEmail()
        );
    }
}
```

---

# 📄 Complete Exception

```java
package com.example.app.exception;

public class UserNotFoundException
        extends RuntimeException {

    public UserNotFoundException(Long id) {

        super(
                "User not found with id: " + id
        );
    }
}
```

---

# 📄 Complete Global Exception Handler

```java
package com.example.app.exception;

import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.*;

import java.time.LocalDateTime;
import java.util.Map;

@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(
            UserNotFoundException.class
    )
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public Map<String, Object> handleUserNotFound(
            UserNotFoundException exception
    ) {

        return Map.of(
                "timestamp",
                LocalDateTime.now(),

                "status",
                404,

                "error",
                "Not Found",

                "message",
                exception.getMessage()
        );
    }
}
```

---

# 📄 Complete Controller

```java
package com.example.app.controller;

import com.example.app.dto.UserRequest;
import com.example.app.dto.UserResponse;
import com.example.app.service.UserService;

import jakarta.validation.Valid;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;

import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/users")
public class UserController {

    private final UserService service;

    public UserController(
            UserService service
    ) {
        this.service = service;
    }

    @GetMapping
    public ResponseEntity<List<UserResponse>>
    findAll() {

        return ResponseEntity.ok(
                service.findAll()
        );
    }

    @GetMapping("/{id}")
    public ResponseEntity<UserResponse>
    findById(
            @PathVariable Long id
    ) {

        return ResponseEntity.ok(
                service.findById(id)
        );
    }

    @PostMapping
    public ResponseEntity<UserResponse>
    create(
            @Valid
            @RequestBody
            UserRequest request
    ) {

        return ResponseEntity
                .status(HttpStatus.CREATED)
                .body(
                        service.create(request)
                );
    }

    @PutMapping("/{id}")
    public ResponseEntity<UserResponse>
    update(
            @PathVariable Long id,

            @Valid
            @RequestBody
            UserRequest request
    ) {

        return ResponseEntity.ok(
                service.update(
                        id,
                        request
                )
        );
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void>
    delete(
            @PathVariable Long id
    ) {

        service.delete(id);

        return ResponseEntity
                .noContent()
                .build();
    }
}
```

---

# 🧪 API Examples

## Create User

```http
POST /api/users
Content-Type: application/json
```

```json
{
  "name": "Heng",
  "email": "heng@example.com"
}
```

Response:

```json
{
  "id": 1,
  "name": "Heng",
  "email": "heng@example.com"
}
```

---

## Get Users

```http
GET /api/users
```

---

## Get One User

```http
GET /api/users/1
```

---

## Update User

```http
PUT /api/users/1
Content-Type: application/json
```

```json
{
  "name": "Heng Updated",
  "email": "new@example.com"
}
```

---

## Delete User

```http
DELETE /api/users/1
```

Response:

```http
204 No Content
```

---

# 🛠 Useful Maven Commands

Run application:

```bash
mvn spring-boot:run
```

Compile:

```bash
mvn compile
```

Run tests:

```bash
mvn test
```

Package:

```bash
mvn clean package
```

Skip tests:

```bash
mvn clean package -DskipTests
```

Run JAR:

```bash
java -jar target/springboot-api-0.0.1-SNAPSHOT.jar
```

Clean:

```bash
mvn clean
```

---

# 🌳 Git Workflow

Initialize:

```bash
git init
```

Add:

```bash
git add .
```

Commit:

```bash
git commit -m "Initial Spring Boot project"
```

Branch:

```bash
git branch -M main
```

Remote:

```bash
git remote add origin YOUR_GITHUB_REPOSITORY
```

Push:

```bash
git push -u origin main
```

---

# 🔐 `.gitignore`

Use:

```gitignore
# Maven
target/

# IDE
.idea/
*.iml
.vscode/

# Eclipse
.classpath
.project
.settings/

# OS
.DS_Store
Thumbs.db

# Logs
*.log

# Environment
.env

# Secrets
application-local.properties
application-secret.properties
```

Never commit:

```text
passwords
API keys
JWT secrets
private keys
cloud credentials
database credentials
```

---

# 🎯 Spring Boot Cheat Sheet

## Controller

```java
@RestController
@RequestMapping("/api")
```

## GET

```java
@GetMapping
```

## POST

```java
@PostMapping
```

## PUT

```java
@PutMapping
```

## DELETE

```java
@DeleteMapping
```

## Request Body

```java
@RequestBody
```

## URL Variable

```java
@PathVariable
```

## Query Parameter

```java
@RequestParam
```

## Service

```java
@Service
```

## Repository

```java
@Repository
```

## Entity

```java
@Entity
```

## Dependency Injection

```java
@Autowired
```

or preferably constructor injection:

```java
public UserController(
        UserService service
) {
    this.service = service;
}
```

## Validation

```java
@Valid
@NotBlank
@NotNull
@Email
@Size
@Min
@Max
```

## Transactions

```java
@Transactional
```

## Security

```java
@EnableWebSecurity
```

## Method Security

```java
@EnableMethodSecurity
```

---

# 🧭 Spring Boot Architecture Summary

```text
                 ┌──────────────┐
                 │    Client    │
                 └──────┬───────┘
                        │
                        ▼
                 ┌──────────────┐
                 │   Security   │
                 └──────┬───────┘
                        │
                        ▼
                 ┌──────────────┐
                 │  Controller  │
                 └──────┬───────┘
                        │
                        ▼
                 ┌──────────────┐
                 │   Service    │
                 └──────┬───────┘
                        │
                        ▼
                 ┌──────────────┐
                 │  Repository  │
                 └──────┬───────┘
                        │
                        ▼
                 ┌──────────────┐
                 │   Database   │
                 └──────────────┘
```

---

# 🇰🇭 សង្ខេបជាភាសាខ្មែរ

Spring Boot គឺជា Java Framework សម្រាប់បង្កើត Backend និង REST API។

លំដាប់ដែលគួររៀន៖

```text
Java
 ↓
Spring
 ↓
Spring Boot
 ↓
REST API
 ↓
Controller
 ↓
Service
 ↓
Repository
 ↓
JPA / Hibernate
 ↓
MySQL / PostgreSQL
 ↓
Validation
 ↓
Exception Handling
 ↓
Spring Security
 ↓
JWT
 ↓
Testing
 ↓
Docker
 ↓
Redis
 ↓
Kafka
 ↓
Microservices
 ↓
Production
```

ចំណុចសំខាន់បំផុតគឺយល់ពី៖

```text
Controller
    ↓
Service
    ↓
Repository
    ↓
Database
```

បន្ទាប់មករៀន៖

```text
DTO
Validation
Exception
Security
JWT
Testing
Docker
```

បន្ទាប់ពីនោះទើបបន្តទៅ៖

```text
Redis
Kafka
Microservices
Kubernetes
Cloud
System Design
```

---

# ⭐ Final Goal

After completing this guide, you should be able to build:

```text
Frontend
   │
   │ REST / JSON
   ▼
Spring Boot API
   │
   ├── Authentication
   ├── Authorization
   ├── Validation
   ├── Exception Handling
   ├── Logging
   ├── Testing
   ├── Caching
   ├── Async
   └── Monitoring
   │
   ▼
Database
   │
   ├── MySQL
   ├── PostgreSQL
   └── Redis
```

And eventually:

```text
                    ┌──────────────┐
                    │ API Gateway  │
                    └──────┬───────┘
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
    User Service     Order Service    Payment Service
          │                │                │
          ▼                ▼                ▼
       MySQL            MySQL            MySQL
          │                │                │
          └────────────────┼────────────────┘
                           │
                           ▼
                         Kafka
                           │
            ┌──────────────┼──────────────┐
            ▼              ▼              ▼
       Notification     Analytics       Email
```

---

# 📖 Official Documentation

* Spring Boot Documentation: https://docs.spring.io/spring-boot/
* Spring Boot Reference: https://docs.spring.io/spring-boot/reference/
* Spring Security: https://docs.spring.io/spring-security/reference/
* Spring Data JPA: https://spring.io/projects/spring-data-jpa
* Spring Initializr: https://start.spring.io/

---

# 📌 Important Version Note

This README uses **Spring Boot 4.1.1**, which is currently listed by Spring as the latest stable Spring Boot release. Spring Boot 4.2.0-M1 is a preview release and should not be treated as the stable baseline.

For new projects, prefer the current stable release and check the official Spring Boot documentation when upgrading because starter names, supported dependency versions, and APIs can change between major generations.

---

# ❤️ Contributing

Pull requests are welcome.

If you find an error:

1. Fork the repository.
2. Create a branch.
3. Fix the documentation/code.
4. Commit your changes.
5. Open a pull request.

---

# 📜 License

This documentation is available under the MIT License.

---

## 🚀 Keep Learning

```text
Learn Java
    ↓
Learn Spring Boot
    ↓
Build REST APIs
    ↓
Connect Database
    ↓
Add Security
    ↓
Write Tests
    ↓
Dockerize
    ↓
Deploy
    ↓
Learn Microservices
    ↓
Learn System Design
```

**Happy Coding! ☕🚀**
