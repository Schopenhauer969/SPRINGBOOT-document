# 🌱 Spring Boot Complete Guide | មគ្គុទ្ទេសក៍ពេញលេញ Spring Boot
### From Beginner to Advanced | ពីកម្រិតដំបូងដល់កម្រិតខ្ពស់

> **Language / ភាសា**: Explanations in Khmer 🇰🇭 + English 🇬🇧, all code and keywords in English.
> ការពន្យល់ជាភាសាខ្មែរ និងអង់គ្លេស ខណៈកូដ និងពាក្យគន្លឹះសរសេរជាភាសាអង់គ្លេស។

**Stack used in this guide:** Java 17, Spring Boot 3.3.x, Maven, Spring Data JPA, H2/MySQL, Spring Security (JWT), JUnit 5, Docker.

---

## 📑 Table of Contents | មាតិកា

1. [Introduction | សេចក្តីផ្តើម](#1-introduction--សេចក្តីផ្តើម)
2. [Prerequisites | គ្រឿងបរិក្ខារត្រូវការ](#2-prerequisites--គ្រឿងបរិក្ខារត្រូវការ)
3. [Creating a Project | ការបង្កើតគម្រោង](#3-creating-a-project--ការបង្កើតគម្រោង)
4. [Project Structure | រចនាសម្ព័ន្ធគម្រោង](#4-project-structure--រចនាសម្ព័ន្ធគម្រោង)
5. [Main Application Class | ថ្នាក់កម្មវិធីចម្បង](#5-main-application-class--ថ្នាក់កម្មវិធីចម្បង)
6. [REST Controllers | ការបង្កើត Controller](#6-rest-controllers--ការបង្កើត-controller)
7. [Dependency Injection & Beans](#7-Dependency-Injection-&-Beans-|-ការចាក់-Dependency)
8. [Configuration (application.yml)](#8-configuration--ការកំណត់រចនាសម្ព័ន្ធ)
9. [Spring Data JPA — Entity & Repository](#9-spring-data-jpa--entity--repository)
10. [Service Layer | ស្រទាប់សេវាកម្ម](#10-service-layer--ស្រទាប់សេវាកម្ម)
11. [DTO & Validation | ការត្រួតពិនិត្យទិន្នន័យ](#11-dto--validation--ការត្រួតពិនិត្យទិន្នន័យ)
12. [Global Exception Handling](#12-global-exception-handling--ការគ្រប់គ្រងកំហុសសកល)
13. [Full CRUD REST API Example](#13-full-crud-rest-api-example--ឧទាហរណ៍ crud ពេញលេញ)
14. [Spring Security + JWT (Advanced)](#14-spring-security--jwt-advanced--សុវត្ថិភាពកម្រិតខ្ពស់)
15. [Testing with JUnit & MockMvc](#15-testing-with-junit--mockmvc--ការសាកល្បង)
16. [Logging | កំណត់ហេតុ](#16-logging--កំណត់ហេតុ)
17. [Profiles (dev/prod)](#17-profiles-devprod--ការកំណត់សម្រាប់បរិស្ថានផ្សេងៗ)
18. [API Documentation with Swagger/OpenAPI](#18-api-documentation-with-swaggeropenapi)
19. [Caching, Async & Scheduling (Advanced)](#19-caching-async--scheduling-advanced)
20. [Actuator — Monitoring](#20-actuator--monitoring--ការត្រួតពិនិត្យ)
21. [Dockerizing the App](#21-dockerizing-the-app--ការវេចខ្ចប់ជាមួយ-docker)
22. [Deployment | ការដាក់ឱ្យប្រើប្រាស់ជាក់ស្តែង](#22-deployment--ការដាក់ឱ្យប្រើប្រាស់ជាក់ស្តែង)
23. [Best Practices | ការអនុវត្តល្អបំផុត](#23-best-practices--ការអនុវត្តល្អបំផុត)
24. [Resources | ធនធានបន្ថែម](#24-resources--ធនធានបន្ថែម)

---

## 1. Introduction | សេចក្តីផ្តើម

**English:** Spring Boot is a Java framework that makes it easy to create stand-alone, production-grade Spring applications with minimal configuration. It comes with an embedded server (Tomcat by default), auto-configuration, and a huge ecosystem (Spring Data, Spring Security, Spring Cloud, etc.).

**ខ្មែរ:** Spring Boot គឺជា framework មួយសម្រាប់ភាសា Java ដែលជួយឱ្យការសាងសង់កម្មវិធី Spring កាន់តែងាយស្រួល ដោយមិនចាំបាច់កំណត់រចនាសម្ព័ន្ធច្រើន។ វាមាន server ភ្ជាប់មកជាមួយស្រាប់ (ជាធម្មតា Tomcat) មានលក្ខណៈ auto-configuration និងមាន ecosystem ធំទូលាយដូចជា Spring Data, Spring Security, Spring Cloud ជាដើម។

**Why use Spring Boot? | ហេតុអ្វីត្រូវប្រើ Spring Boot?**

| Feature | English | ខ្មែរ |
|---|---|---|
| Auto-configuration | Automatically configures beans based on dependencies | កំណត់ bean ដោយស្វ័យប្រវត្តិទៅតាម dependency |
| Embedded server | No need to install Tomcat separately | មិនចាំបាច់ដំឡើង Tomcat ដោយឡែក |
| Starter dependencies | Pre-packaged dependency bundles | កញ្ចប់ dependency ដែលរៀបចំរួចជាស្រេច |
| Production-ready | Health checks, metrics via Actuator | មាន health check និង metrics តាមរយៈ Actuator |

---

## 2. Prerequisites | គ្រឿងបរិក្ខារត្រូវការ

**English:** Before starting, install the following:
- **JDK 17+** (Java Development Kit)
- **Maven 3.8+** or **Gradle 8+**
- **IDE**: IntelliJ IDEA, VS Code, or Eclipse
- Basic knowledge of Java (OOP, annotations)

**ខ្មែរ:** មុននឹងចាប់ផ្តើម សូមដំឡើងអ្វីៗខាងក្រោម៖
- **JDK 17+**
- **Maven 3.8+** ឬ **Gradle 8+**
- **IDE**៖ IntelliJ IDEA, VS Code, ឬ Eclipse
- ចំណេះដឹងមូលដ្ឋានអំពី Java (OOP, annotations)

Check your installation | ពិនិត្យការដំឡើង:

```bash
java -version
mvn -version
```

---

## 3. Creating a Project | ការបង្កើតគម្រោង

**English:** The easiest way is via [Spring Initializr](https://start.spring.io).

**ខ្មែរ:** វិធីងាយស្រួលបំផុតគឺប្រើ [Spring Initializr](https://start.spring.io)។

Choose these settings | ជ្រើសរើសការកំណត់ដូចខាងក្រោម:

```
Project: Maven
Language: Java
Spring Boot: 3.3.x
Packaging: Jar
Java: 17
Dependencies:
  - Spring Web
  - Spring Data JPA
  - H2 Database
  - Validation
  - Lombok
```

Or generate from the command line using `curl`:

```bash
curl https://start.spring.io/starter.zip \
  -d dependencies=web,data-jpa,h2,validation,lombok \
  -d javaVersion=17 \
  -d bootVersion=3.3.4 \
  -d name=demo \
  -o demo.zip
unzip demo.zip -d demo
```

---

## 4. Project Structure | រចនាសម្ព័ន្ធគម្រោង

**English:** A typical layered Spring Boot project structure looks like this:

**ខ្មែរ:** រចនាសម្ព័ន្ធគម្រោង Spring Boot ធម្មតាមានទម្រង់ស្រទាប់ដូចខាងក្រោម៖

```
demo/
├── src/
│   ├── main/
│   │   ├── java/com/example/demo/
│   │   │   ├── DemoApplication.java      # Main entry point
│   │   │   ├── controller/               # REST controllers
│   │   │   │   └── ProductController.java
│   │   │   ├── service/                  # Business logic
│   │   │   │   ├── ProductService.java
│   │   │   │   └── impl/ProductServiceImpl.java
│   │   │   ├── repository/               # Data access layer
│   │   │   │   └── ProductRepository.java
│   │   │   ├── model/ (entity)           # JPA entities
│   │   │   │   └── Product.java
│   │   │   ├── dto/                      # Data transfer objects
│   │   │   │   ├── ProductRequest.java
│   │   │   │   └── ProductResponse.java
│   │   │   ├── exception/                # Custom exceptions
│   │   │   │   ├── ResourceNotFoundException.java
│   │   │   │   └── GlobalExceptionHandler.java
│   │   │   └── config/                   # Configuration classes
│   │   │       └── SecurityConfig.java
│   │   └── resources/
│   │       ├── application.yml
│   │       └── static/ , templates/
│   └── test/
│       └── java/com/example/demo/
│           └── ProductControllerTest.java
├── pom.xml
└── README.md
```

> 💡 **Tip / គន្លឹះ:** Group classes by feature/layer, not randomly. This keeps large projects maintainable. | ចាត់ថ្នាក់ class តាមមុខងារ/ស្រទាប់ មិនមែនដោយចៃដន្យ ដើម្បីឱ្យគម្រោងធំៗងាយថែទាំ។

---

## 5. Main Application Class | ថ្នាក់កម្មវិធីចម្បង

**English:** Every Spring Boot app has one main class annotated with `@SpringBootApplication`, which combines `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`.

**ខ្មែរ:** កម្មវិធី Spring Boot គ្រប់មួយមាន class ចម្បងមួយដែលមាន annotation `@SpringBootApplication` ដែលរួមបញ្ចូល `@Configuration`, `@EnableAutoConfiguration`, និង `@ComponentScan` ចូលគ្នា។

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

Run it with | ដំណើរការវាដោយ:

```bash
mvn spring-boot:run
```

---

## 6. REST Controllers | ការបង្កើត Controller

**English:** Controllers handle incoming HTTP requests. Use `@RestController` (combines `@Controller` + `@ResponseBody`) so return values are serialized directly to JSON.

**ខ្មែរ:** Controller ជាកន្លែងទទួល HTTP request។ ប្រើ `@RestController` (ដែលរួម `@Controller` និង `@ResponseBody`) ដើម្បីឱ្យតម្លៃត្រឡប់ត្រូវបានបំលែងទៅជា JSON ដោយផ្ទាល់។

```java
package com.example.demo.controller;

import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/hello")
public class HelloController {

    @GetMapping
    public String sayHello() {
        return "Hello, Spring Boot!";
    }

    @GetMapping("/{name}")
    public String sayHelloTo(@PathVariable String name) {
        return "Hello, " + name + "!";
    }
}
```

**Common annotations | Annotation ទូទៅ:**

| Annotation | Purpose (English) | គោលបំណង (ខ្មែរ) |
|---|---|---|
| `@GetMapping` | Handle GET requests | ដោះស្រាយ GET request |
| `@PostMapping` | Handle POST requests | ដោះស្រាយ POST request |
| `@PutMapping` | Handle PUT (full update) | ដោះស្រាយ PUT (កែទាំងស្រុង) |
| `@PatchMapping` | Handle PATCH (partial update) | ដោះស្រាយ PATCH (កែផ្នែក) |
| `@DeleteMapping` | Handle DELETE requests | ដោះស្រាយ DELETE request |
| `@PathVariable` | Read value from URL path | អានតម្លៃពី URL path |
| `@RequestParam` | Read query parameter | អានតម្លៃ query parameter |
| `@RequestBody` | Bind JSON body to object | ចងទិន្នន័យ JSON ទៅជា object |

---

## 7. Dependency Injection & Beans | ការចាក់ Dependency

**English:** Spring manages objects ("beans") for you and injects them where needed, instead of you calling `new` manually. This is called **Inversion of Control (IoC)**.

**ខ្មែរ:** Spring គ្រប់គ្រង object (ហៅថា "bean") ជំនួសអោយអ្នក ហើយចាក់ (inject) វាទៅកន្លែងដែលត្រូវការ ដោយមិនចាំបាច់ហៅ `new` ដោយផ្ទាល់។ លក្ខណៈនេះហៅថា **Inversion of Control (IoC)**។

```java
package com.example.demo.service;

import org.springframework.stereotype.Service;

@Service
public class GreetingService {
    public String greet(String name) {
        return "Welcome, " + name;
    }
}
```

**Constructor injection (recommended) | ការចាក់តាម Constructor (ណែនាំ):**

```java
package com.example.demo.controller;

import com.example.demo.service.GreetingService;
import org.springframework.web.bind.annotation.*;

@RestController
public class GreetingController {

    private final GreetingService greetingService;

    // Constructor injection — no @Autowired needed since Spring 4.3+ with a single constructor
    public GreetingController(GreetingService greetingService) {
        this.greetingService = greetingService;
    }

    @GetMapping("/api/greet")
    public String greet(@RequestParam String name) {
        return greetingService.greet(name);
    }
}
```

> ⚠️ **Note / កំណត់សម្គាល់:** Prefer constructor injection over field injection (`@Autowired` on a field) — it's easier to test and makes dependencies explicit. | គួរប្រើ constructor injection ជាជាង field injection ព្រោះវាងាយសាកល្បង និងបញ្ជាក់ dependency ច្បាស់លាស់។

---

## 8. Configuration | ការកំណត់រចនាសម្ព័ន្ធ

**English:** Use `application.yml` (or `.properties`) to configure your app — server port, database, logging, etc.

**ខ្មែរ:** ប្រើ `application.yml` (ឬ `.properties`) ដើម្បីកំណត់រចនាសម្ព័ន្ធកម្មវិធី ដូចជា port របស់ server មូលដ្ឋានទិន្នន័យ log ជាដើម។

`src/main/resources/application.yml`:

```yaml
server:
  port: 8080

spring:
  application:
    name: demo

  datasource:
    url: jdbc:h2:mem:testdb
    driver-class-name: org.h2.Driver
    username: sa
    password: ""

  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        format_sql: true

  h2:
    console:
      enabled: true
      path: /h2-console

logging:
  level:
    root: INFO
    com.example.demo: DEBUG
```

Reading custom properties with `@Value` or a typed config class:

```java
package com.example.demo.config;

import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;
import lombok.Data;

@Data
@Component
@ConfigurationProperties(prefix = "app")
public class AppProperties {
    private String name;
    private String version;
}
```

```yaml
app:
  name: "Demo Service"
  version: "1.0.0"
```

---

## 9. Spring Data JPA — Entity & Repository

**English:** JPA lets you map Java classes to database tables using annotations, and `JpaRepository` gives you CRUD methods for free — no SQL needed for basic operations.

**ខ្មែរ:** JPA អនុញ្ញាតឱ្យអ្នកភ្ជាប់ class Java ទៅតារាងក្នុងមូលដ្ឋានទិន្នន័យដោយប្រើ annotation ហើយ `JpaRepository` ផ្តល់ method CRUD ដោយស្វ័យប្រវត្តិ — មិនចាំបាច់សរសេរ SQL សម្រាប់ប្រតិបត្តិការមូលដ្ឋាន។

**Entity class:**

```java
package com.example.demo.model;

import jakarta.persistence.*;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
import java.math.BigDecimal;

@Entity
@Table(name = "products")
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Product {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false, length = 100)
    private String name;

    @Column(precision = 10, scale = 2)
    private BigDecimal price;

    private Integer stock;
}
```

**Repository interface:**

```java
package com.example.demo.repository;

import com.example.demo.model.Product;
import org.springframework.data.jpa.repository.JpaRepository;
import java.util.List;

public interface ProductRepository extends JpaRepository<Product, Long> {

    // Derived query — Spring auto-generates SQL from the method name
    List<Product> findByNameContainingIgnoreCase(String name);

    List<Product> findByStockGreaterThan(Integer stock);
}
```

**Custom query with `@Query`:**

```java
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;

public interface ProductRepository extends JpaRepository<Product, Long> {

    @Query("SELECT p FROM Product p WHERE p.price <= :maxPrice ORDER BY p.price ASC")
    List<Product> findAffordableProducts(@Param("maxPrice") BigDecimal maxPrice);
}
```

---

## 10. Service Layer | ស្រទាប់សេវាកម្ម

**English:** The service layer contains business logic and sits between the controller and the repository. This separation keeps controllers thin.

**ខ្មែរ:** ស្រទាប់សេវាកម្មផ្ទុកតក្កវិជ្ជាអាជីវកម្ម ហើយស្ថិតនៅចន្លោះ controller និង repository។ ការញែកនេះជួយឱ្យ controller មានលក្ខណៈស្រាល និងសាមញ្ញ។

```java
package com.example.demo.service;

import com.example.demo.model.Product;
import java.util.List;

public interface ProductService {
    Product createProduct(Product product);
    Product getProductById(Long id);
    List<Product> getAllProducts();
    Product updateProduct(Long id, Product product);
    void deleteProduct(Long id);
}
```

```java
package com.example.demo.service.impl;

import com.example.demo.exception.ResourceNotFoundException;
import com.example.demo.model.Product;
import com.example.demo.repository.ProductRepository;
import com.example.demo.service.ProductService;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;

@Service
public class ProductServiceImpl implements ProductService {

    private final ProductRepository productRepository;

    public ProductServiceImpl(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    @Override
    public Product createProduct(Product product) {
        return productRepository.save(product);
    }

    @Override
    public Product getProductById(Long id) {
        return productRepository.findById(id)
                .orElseThrow(() -> new ResourceNotFoundException("Product not found with id: " + id));
    }

    @Override
    public List<Product> getAllProducts() {
        return productRepository.findAll();
    }

    @Override
    @Transactional
    public Product updateProduct(Long id, Product updated) {
        Product existing = getProductById(id);
        existing.setName(updated.getName());
        existing.setPrice(updated.getPrice());
        existing.setStock(updated.getStock());
        return productRepository.save(existing);
    }

    @Override
    public void deleteProduct(Long id) {
        Product existing = getProductById(id);
        productRepository.delete(existing);
    }
}
```

---

## 11. DTO & Validation | ការត្រួតពិនិត្យទិន្នន័យ

**English:** Never expose your entity directly in the API. Use **DTOs (Data Transfer Objects)** to control what data goes in/out, and `jakarta.validation` annotations to validate input.

**ខ្មែរ:** កុំបញ្ចេញ entity ដោយផ្ទាល់តាម API។ ប្រើ **DTO (Data Transfer Object)** ដើម្បីគ្រប់គ្រងទិន្នន័យចូល/ចេញ ហើយប្រើ annotation នៃ `jakarta.validation` ដើម្បីត្រួតពិនិត្យទិន្នន័យបញ្ចូល។

```java
package com.example.demo.dto;

import jakarta.validation.constraints.*;
import lombok.Data;
import java.math.BigDecimal;

@Data
public class ProductRequest {

    @NotBlank(message = "Name is required")
    @Size(max = 100, message = "Name must be at most 100 characters")
    private String name;

    @NotNull(message = "Price is required")
    @DecimalMin(value = "0.0", inclusive = false, message = "Price must be greater than 0")
    private BigDecimal price;

    @NotNull(message = "Stock is required")
    @Min(value = 0, message = "Stock cannot be negative")
    private Integer stock;
}
```

```java
package com.example.demo.dto;

import lombok.AllArgsConstructor;
import lombok.Data;
import java.math.BigDecimal;

@Data
@AllArgsConstructor
public class ProductResponse {
    private Long id;
    private String name;
    private BigDecimal price;
    private Integer stock;
}
```

Trigger validation in the controller with `@Valid`:

```java
@PostMapping
public ResponseEntity<ProductResponse> create(@Valid @RequestBody ProductRequest request) {
    // ...
}
```

---

## 12. Global Exception Handling | ការគ្រប់គ្រងកំហុសសកល

**English:** Use `@RestControllerAdvice` to catch exceptions from any controller in one place and return clean, consistent error responses.

**ខ្មែរ:** ប្រើ `@RestControllerAdvice` ដើម្បីចាប់កំហុសពី controller ណាមួយនៅកន្លែងតែមួយ ហើយត្រឡប់ error response ដែលច្បាស់លាស់ និងស៊ីចង្វាក់គ្នា។

```java
package com.example.demo.exception;

public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
```

```java
package com.example.demo.exception;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

import java.time.LocalDateTime;
import java.util.HashMap;
import java.util.Map;

@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<Map<String, Object>> handleNotFound(ResourceNotFoundException ex) {
        Map<String, Object> body = new HashMap<>();
        body.put("timestamp", LocalDateTime.now());
        body.put("status", HttpStatus.NOT_FOUND.value());
        body.put("message", ex.getMessage());
        return new ResponseEntity<>(body, HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, String>> handleValidation(MethodArgumentNotValidException ex) {
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getFieldErrors().forEach(error ->
                errors.put(error.getField(), error.getDefaultMessage())
        );
        return new ResponseEntity<>(errors, HttpStatus.BAD_REQUEST);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<Map<String, Object>> handleGeneral(Exception ex) {
        Map<String, Object> body = new HashMap<>();
        body.put("timestamp", LocalDateTime.now());
        body.put("status", HttpStatus.INTERNAL_SERVER_ERROR.value());
        body.put("message", "Something went wrong");
        return new ResponseEntity<>(body, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

---

## 13. Full CRUD REST API Example | ឧទាហរណ៍ CRUD ពេញលេញ

**English:** Putting it all together — a complete `ProductController` with full CRUD.

**ខ្មែរ:** ដាក់រួមគ្នាទាំងអស់ — `ProductController` ពេញលេញជាមួយ CRUD គ្រប់មុខងារ។

```java
package com.example.demo.controller;

import com.example.demo.dto.ProductRequest;
import com.example.demo.dto.ProductResponse;
import com.example.demo.model.Product;
import com.example.demo.service.ProductService;
import jakarta.validation.Valid;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;
import java.util.stream.Collectors;

@RestController
@RequestMapping("/api/products")
public class ProductController {

    private final ProductService productService;

    public ProductController(ProductService productService) {
        this.productService = productService;
    }

    // CREATE
    @PostMapping
    public ResponseEntity<ProductResponse> create(@Valid @RequestBody ProductRequest request) {
        Product product = new Product(null, request.getName(), request.getPrice(), request.getStock());
        Product saved = productService.createProduct(product);
        return ResponseEntity.status(HttpStatus.CREATED).body(toResponse(saved));
    }

    // READ ALL
    @GetMapping
    public ResponseEntity<List<ProductResponse>> getAll() {
        List<ProductResponse> list = productService.getAllProducts()
                .stream().map(this::toResponse).collect(Collectors.toList());
        return ResponseEntity.ok(list);
    }

    // READ ONE
    @GetMapping("/{id}")
    public ResponseEntity<ProductResponse> getOne(@PathVariable Long id) {
        return ResponseEntity.ok(toResponse(productService.getProductById(id)));
    }

    // UPDATE
    @PutMapping("/{id}")
    public ResponseEntity<ProductResponse> update(@PathVariable Long id,
                                                    @Valid @RequestBody ProductRequest request) {
        Product product = new Product(null, request.getName(), request.getPrice(), request.getStock());
        Product updated = productService.updateProduct(id, product);
        return ResponseEntity.ok(toResponse(updated));
    }

    // DELETE
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> delete(@PathVariable Long id) {
        productService.deleteProduct(id);
        return ResponseEntity.noContent().build();
    }

    private ProductResponse toResponse(Product p) {
        return new ProductResponse(p.getId(), p.getName(), p.getPrice(), p.getStock());
    }
}
```

**Testing with curl | សាកល្បងជាមួយ curl:**

```bash
# Create
curl -X POST http://localhost:8080/api/products \
  -H "Content-Type: application/json" \
  -d '{"name":"Laptop","price":999.99,"stock":10}'

# Get all
curl http://localhost:8080/api/products

# Get one
curl http://localhost:8080/api/products/1

# Update
curl -X PUT http://localhost:8080/api/products/1 \
  -H "Content-Type: application/json" \
  -d '{"name":"Laptop Pro","price":1299.99,"stock":5}'

# Delete
curl -X DELETE http://localhost:8080/api/products/1
```

---

## 14. Spring Security + JWT (Advanced) | សុវត្ថិភាពកម្រិតខ្ពស់

**English:** For stateless authentication, Spring Security combined with JWT (JSON Web Token) is the standard approach in REST APIs.

**ខ្មែរ:** សម្រាប់ការផ្ទៀងផ្ទាត់ភាពត្រឹមត្រូវបែប stateless ការប្រើ Spring Security ជាមួយ JWT (JSON Web Token) គឺជាវិធីស្តង់ដារសម្រាប់ REST API។

**Dependencies (pom.xml):**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-api</artifactId>
    <version>0.12.6</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-impl</artifactId>
    <version>0.12.6</version>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-jackson</artifactId>
    <version>0.12.6</version>
    <scope>runtime</scope>
</dependency>
```

**JWT utility class:**

```java
package com.example.demo.security;

import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.security.Keys;
import org.springframework.stereotype.Component;

import javax.crypto.SecretKey;
import java.util.Date;

@Component
public class JwtUtil {

    private final SecretKey key = Keys.secretKeyFor(io.jsonwebtoken.SignatureAlgorithm.HS256);
    private final long expirationMs = 86_400_000; // 24 hours

    public String generateToken(String username) {
        return Jwts.builder()
                .subject(username)
                .issuedAt(new Date())
                .expiration(new Date(System.currentTimeMillis() + expirationMs))
                .signWith(key)
                .compact();
    }

    public String extractUsername(String token) {
        return Jwts.parser().verifyWith(key).build()
                .parseSignedClaims(token).getPayload().getSubject();
    }

    public boolean isTokenValid(String token) {
        try {
            Jwts.parser().verifyWith(key).build().parseSignedClaims(token);
            return true;
        } catch (Exception e) {
            return false;
        }
    }
}
```

**Security configuration:**

```java
package com.example.demo.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    private final JwtAuthFilter jwtAuthFilter;

    public SecurityConfig(JwtAuthFilter jwtAuthFilter) {
        this.jwtAuthFilter = jwtAuthFilter;
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf(csrf -> csrf.disable())
            .sessionManagement(sm -> sm.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/api/auth/**").permitAll()
                .anyRequest().authenticated()
            )
            .addFilterBefore(jwtAuthFilter, UsernamePasswordAuthenticationFilter.class);

        return http.build();
    }
}
```

> 📌 **Note / កំណត់សម្គាល់:** `JwtAuthFilter` (a `OncePerRequestFilter`) validates the token on each request and sets the `SecurityContext`. This is intentionally left as an exercise — the pattern above gives you the full skeleton to extend. | `JwtAuthFilter` ត្រួតពិនិត្យ token រាល់ request ហើយកំណត់ `SecurityContext`។ ខ្ញុំទុកឱ្យអ្នកបន្ថែមខ្លួនឯង ដោយផ្អែកលើគំរូខាងលើ។

---

## 15. Testing with JUnit & MockMvc | ការសាកល្បង

**English:** Spring Boot includes `spring-boot-starter-test` (JUnit 5, Mockito, AssertJ, MockMvc) out of the box.

**ខ្មែរ:** Spring Boot មាន `spring-boot-starter-test` (JUnit 5, Mockito, AssertJ, MockMvc) ភ្ជាប់មកជាមួយស្រាប់។

**Unit test (Service layer, with Mockito):**

```java
package com.example.demo.service;

import com.example.demo.model.Product;
import com.example.demo.repository.ProductRepository;
import com.example.demo.service.impl.ProductServiceImpl;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import java.math.BigDecimal;
import java.util.Optional;

import static org.assertj.core.api.Assertions.assertThat;
import static org.mockito.Mockito.when;

@ExtendWith(MockitoExtension.class)
class ProductServiceImplTest {

    @Mock
    private ProductRepository productRepository;

    @InjectMocks
    private ProductServiceImpl productService;

    @Test
    void shouldReturnProductWhenFound() {
        Product product = new Product(1L, "Laptop", BigDecimal.valueOf(999.99), 10);
        when(productRepository.findById(1L)).thenReturn(Optional.of(product));

        Product result = productService.getProductById(1L);

        assertThat(result.getName()).isEqualTo("Laptop");
    }
}
```

**Integration test (Controller, with MockMvc):**

```java
package com.example.demo.controller;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.example.demo.dto.ProductRequest;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;

import java.math.BigDecimal;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.post;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@SpringBootTest
@AutoConfigureMockMvc
class ProductControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Autowired
    private ObjectMapper objectMapper;

    @Test
    void shouldCreateProduct() throws Exception {
        ProductRequest request = new ProductRequest();
        request.setName("Mouse");
        request.setPrice(BigDecimal.valueOf(19.99));
        request.setStock(50);

        mockMvc.perform(post("/api/products")
                .contentType(MediaType.APPLICATION_JSON)
                .content(objectMapper.writeValueAsString(request)))
                .andExpect(status().isCreated())
                .andExpect(jsonPath("$.name").value("Mouse"));
    }
}
```

Run tests | ដំណើរការតេស្ត:

```bash
mvn test
```

---

## 16. Logging | កំណត់ហេតុ

**English:** Spring Boot uses SLF4J with Logback by default. Use Lombok's `@Slf4j` for quick access to a logger.

**ខ្មែរ:** Spring Boot ប្រើ SLF4J ជាមួយ Logback ជាលំនាំដើម។ ប្រើ `@Slf4j` របស់ Lombok ដើម្បីទទួលបាន logger ភ្លាមៗ។

```java
import lombok.extern.slf4j.Slf4j;
import org.springframework.stereotype.Service;

@Slf4j
@Service
public class ProductServiceImpl {

    public void doSomething() {
        log.info("Processing started");
        log.warn("Low stock warning for product {}", 42);
        log.error("Failed to process product", new RuntimeException("DB error"));
    }
}
```

---

## 17. Profiles (dev/prod) | ការកំណត់សម្រាប់បរិស្ថានផ្សេងៗ

**English:** Use Spring Profiles to have different configurations for development, testing, and production.

**ខ្មែរ:** ប្រើ Spring Profiles ដើម្បីមានការកំណត់ខុសៗគ្នាសម្រាប់ dev, test, និង production។

`application-dev.yml`:
```yaml
spring:
  datasource:
    url: jdbc:h2:mem:devdb
logging:
  level:
    root: DEBUG
```

`application-prod.yml`:
```yaml
spring:
  datasource:
    url: jdbc:mysql://prod-db:3306/mydb
    username: ${DB_USER}
    password: ${DB_PASSWORD}
logging:
  level:
    root: WARN
```

Activate a profile | ធ្វើឱ្យ profile ដំណើរការ:

```bash
java -jar demo.jar --spring.profiles.active=prod
```

Or in code:

```java
@Service
@Profile("dev")
public class MockPaymentService implements PaymentService { /* ... */ }
```

---

## 18. API Documentation with Swagger/OpenAPI

**English:** Add `springdoc-openapi` to auto-generate interactive API docs.

**ខ្មែរ:** បន្ថែម `springdoc-openapi` ដើម្បីបង្កើត API documentation ដោយស្វ័យប្រវត្តិ។

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.6.0</version>
</dependency>
```

**English:** After adding this and running the app, visit `http://localhost:8080/swagger-ui.html` to see an interactive UI for all your endpoints.

**ខ្មែរ:** បន្ទាប់ពីបន្ថែម ហើយដំណើរការកម្មវិធី សូមចូល `http://localhost:8080/swagger-ui.html` ដើម្បីមើល UI អន្តរកម្មសម្រាប់ endpoint ទាំងអស់។

```java
@Operation(summary = "Get product by ID", description = "Returns a single product")
@GetMapping("/{id}")
public ResponseEntity<ProductResponse> getOne(@PathVariable Long id) {
    return ResponseEntity.ok(toResponse(productService.getProductById(id)));
}
```

---

## 19. Caching, Async & Scheduling (Advanced)

**English:** These features boost performance and support background processing.

**ខ្មែរ:** លក្ខណៈទាំងនេះជួយបង្កើនប្រសិទ្ធភាព និងគាំទ្រដំណើរការផ្ទៃខាងក្រោយ។

**Caching:**

```java
// Enable in main class or a @Configuration class
@EnableCaching
@SpringBootApplication
public class DemoApplication { /* ... */ }
```

```java
@Service
public class ProductServiceImpl {

    @Cacheable(value = "products", key = "#id")
    public Product getProductById(Long id) {
        // Expensive DB call — result is cached after first call
        return productRepository.findById(id)
                .orElseThrow(() -> new ResourceNotFoundException("Not found"));
    }

    @CacheEvict(value = "products", key = "#id")
    public void deleteProduct(Long id) {
        productRepository.deleteById(id);
    }
}
```

**Async processing:**

```java
@EnableAsync
@SpringBootApplication
public class DemoApplication { /* ... */ }
```

```java
@Service
public class EmailService {

    @Async
    public void sendWelcomeEmail(String to) {
        // Runs in a separate thread, doesn't block the caller
        log.info("Sending email to {}", to);
    }
}
```

**Scheduling:**

```java
@EnableScheduling
@SpringBootApplication
public class DemoApplication { /* ... */ }
```

```java
@Component
public class ReportScheduler {

    @Scheduled(cron = "0 0 1 * * ?") // every day at 1 AM
    public void generateDailyReport() {
        log.info("Generating daily report...");
    }
}
```

---

## 20. Actuator — Monitoring | ការត្រួតពិនិត្យ

**English:** Spring Boot Actuator exposes production-ready endpoints for health checks, metrics, and app info.

**ខ្មែរ:** Spring Boot Actuator បញ្ចេញ endpoint ដែលរួចរាល់សម្រាប់ production ដូចជា health check, metrics, និងព័ត៌មានកម្មវិធី។

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

```yaml
management:
  endpoints:
    web:
      exposure:
        include: health, info, metrics
```

```bash
curl http://localhost:8080/actuator/health
curl http://localhost:8080/actuator/metrics
```

---

## 21. Dockerizing the App | ការវេចខ្ចប់ជាមួយ Docker

**English:** Package your app in a Docker container for consistent deployment anywhere.

**ខ្មែរ:** វេចខ្ចប់កម្មវិធីរបស់អ្នកក្នុង Docker container ដើម្បីឱ្យការដាក់ដំណើរការស៊ីចង្វាក់គ្នានៅគ្រប់ទីកន្លែង។

`Dockerfile`:

```dockerfile
# Build stage
FROM maven:3.9-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests

# Run stage
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

`docker-compose.yml`:

```yaml
version: "3.8"
services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      - SPRING_PROFILES_ACTIVE=prod
      - DB_USER=root
      - DB_PASSWORD=secret
    depends_on:
      - db
  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: mydb
    ports:
      - "3306:3306"
```

Build & run | ស្ថាបនា និងដំណើរការ:

```bash
docker build -t demo-app .
docker compose up
```

---

## 22. Deployment | ការដាក់ឱ្យប្រើប្រាស់ជាក់ស្តែង

**English:** Build a production JAR and run it, or deploy the Docker image to a cloud provider (AWS, Render, Railway, etc.).

**ខ្មែរ:** ស្ថាបនា JAR សម្រាប់ production ហើយដំណើរការវា ឬដាក់ Docker image ទៅកាន់ cloud provider (AWS, Render, Railway ។ល។)។

```bash
mvn clean package -DskipTests
java -jar target/demo-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod
```

**Checklist before going live | បញ្ជីត្រួតពិនិត្យមុនដាក់ដំណើរការជាក់ស្តែង:**

- [ ] Use environment variables for secrets (never hardcode passwords) | ប្រើ environment variable សម្រាប់ secret កុំសរសេរ password ដោយផ្ទាល់
- [ ] Set `ddl-auto: validate` (not `update`) in production | កំណត់ `ddl-auto: validate` (មិនមែន `update`) នៅ production
- [ ] Enable HTTPS | បើក HTTPS
- [ ] Configure proper CORS rules | កំណត់ CORS ឱ្យត្រឹមត្រូវ
- [ ] Set up centralized logging & monitoring | រៀបចំ log និង monitoring កណ្តាល

---

## 23. Best Practices | ការអនុវត្តល្អបំផុត

| Practice | English | ខ្មែរ |
|---|---|---|
| Layered architecture | Keep Controller → Service → Repository separated | បំបែក Controller → Service → Repository ឱ្យច្បាស់ |
| Use DTOs | Never expose entities directly | កុំបញ្ចេញ entity ដោយផ្ទាល់ |
| Constructor injection | Easier to test, immutable dependencies | ងាយសាកល្បង dependency មិនប្រែប្រួល |
| Validate input | Always validate `@RequestBody` with `@Valid` | ត្រួតពិនិត្យទិន្នន័យបញ្ចូលជានិច្ច |
| Handle exceptions globally | Use `@RestControllerAdvice` | ប្រើ `@RestControllerAdvice` |
| Write tests | Unit + integration tests for critical logic | សរសេរតេស្តសម្រាប់តក្កវិជ្ជាសំខាន់ៗ |
| Externalize config | Use `application.yml` + env vars, not hardcoded values | ប្រើ config ខាងក្រៅ កុំសរសេរតម្លៃដោយផ្ទាល់ក្នុងកូដ |
| Version your API | e.g. `/api/v1/products` | ដាក់លេខជំនាន់ API ដូចជា `/api/v1/products` |

---

## 24. Resources | ធនធានបន្ថែម

- 📘 Official docs: https://spring.io/projects/spring-boot
- 📘 Spring Data JPA: https://spring.io/projects/spring-data-jpa
- 📘 Spring Security: https://spring.io/projects/spring-security
- 📘 Baeldung tutorials: https://www.baeldung.com/spring-boot

---

### 🙏 Made for the Khmer developer community | បង្កើតឡើងសម្រាប់សហគមន៍អ្នកអភិវឌ្ឍន៍ខ្មែរ

If this guide helped you, consider ⭐ starring the repo!
ប្រសិនបើមគ្គុទ្ទេសក៍នេះមានប្រយោជន៍ សូមចុច ⭐ ជាការគាំទ្រ!
