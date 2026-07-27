# Spring Boot: Beginner to Advanced Guide

A complete, hands-on reference for building production-grade applications with Spring Boot — from your first `@RestController` to caching, security, and Docker deployment.

## Table of Contents

- [1. Introduction](#1-introduction)
- [2. Prerequisites](#2-prerequisites)
- [3. Creating a Project](#3-creating-a-project)
- [4. Project Structure](#4-project-structure)
- [5. Your First REST Controller](#5-your-first-rest-controller)
- [6. Configuration (application.yml)](#6-configuration-applicationyml)
- [7. Layered Architecture: Service Layer](#7-layered-architecture-service-layer)
- [8. Persistence with Spring Data JPA](#8-persistence-with-spring-data-jpa)
- [9. DTOs and Validation](#9-dtos-and-validation)
- [10. Global Exception Handling](#10-global-exception-handling)
- [11. Dependency Injection Explained](#11-dependency-injection-explained)
- [12. Testing](#12-testing)
- [13. Spring Security + JWT](#13-spring-security--jwt)
- [14. Caching](#14-caching)
- [15. Async & Scheduled Tasks](#15-async--scheduled-tasks)
- [16. Actuator & Observability](#16-actuator--observability)
- [17. Dockerizing the App](#17-dockerizing-the-app)
- [18. Best Practices](#18-best-practices)
- [19. Common Pitfalls](#19-common-pitfalls)

---

## 1. Introduction

**Spring Boot** is an opinionated framework built on top of the Spring Framework that removes boilerplate configuration and gives you a production-ready application with minimal setup — embedded server, auto-configuration, and starter dependencies included.

This guide walks through a single evolving example: a **Task Manager API** — starting with a "Hello World" endpoint and ending with a secured, cached, tested, containerized service.

---

## 2. Prerequisites

| Tool | Version | Purpose |
|---|---|---|
| Java (JDK) | 17+ | Language runtime |
| Maven or Gradle | Maven 3.8+ / Gradle 8+ | Build tool |
| IDE | IntelliJ IDEA / VS Code | Development |
| Docker | Optional | Containerization (Section 17) |
| PostgreSQL / MySQL | Optional | Production database |

Check your Java version:

```bash
java -version
```

---

## 3. Creating a Project

Use [Spring Initializr](https://start.spring.io) or the CLI equivalent below.

**Maven `pom.xml`** (core dependencies used throughout this guide):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                              https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.3.4</version>
        <relativePath/>
    </parent>

    <groupId>com.example</groupId>
    <artifactId>task-manager</artifactId>
    <version>1.0.0</version>
    <name>task-manager</name>
    <description>Beginner-to-advanced Spring Boot demo</description>

    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <!-- Core web -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!-- Validation -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
        </dependency>

        <!-- Persistence -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>

        <!-- H2 for local/dev database -->
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <scope>runtime</scope>
        </dependency>

        <!-- PostgreSQL for production -->
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <scope>runtime</scope>
        </dependency>

        <!-- Security -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>

        <!-- JWT -->
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

        <!-- Caching -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-cache</artifactId>
        </dependency>

        <!-- Actuator -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <!-- Lombok -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>

        <!-- Testing -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <excludes>
                        <exclude>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                        </exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

The main application class:

```java
package com.example.taskmanager;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cache.annotation.EnableCaching;
import org.springframework.scheduling.annotation.EnableAsync;
import org.springframework.scheduling.annotation.EnableScheduling;

@SpringBootApplication
@EnableCaching
@EnableAsync
@EnableScheduling
public class TaskManagerApplication {

    public static void main(String[] args) {
        SpringApplication.run(TaskManagerApplication.class, args);
    }
}
```

---

## 4. Project Structure

A clean, layered package structure keeps large codebases maintainable:

```
src/main/java/com/example/taskmanager/
├── TaskManagerApplication.java
├── config/
│   ├── SecurityConfig.java
│   └── CacheConfig.java
├── controller/
│   └── TaskController.java
├── service/
│   ├── TaskService.java
│   └── impl/TaskServiceImpl.java
├── repository/
│   └── TaskRepository.java
├── model/
│   └── Task.java
├── dto/
│   ├── TaskRequest.java
│   └── TaskResponse.java
├── exception/
│   ├── ResourceNotFoundException.java
│   └── GlobalExceptionHandler.java
├── security/
│   ├── JwtService.java
│   └── JwtAuthFilter.java
└── mapper/
    └── TaskMapper.java

src/main/resources/
├── application.yml
├── application-dev.yml
└── application-prod.yml

src/test/java/com/example/taskmanager/
├── controller/TaskControllerTest.java
└── service/TaskServiceTest.java
```

---

## 5. Your First REST Controller

Start simple — no database, just an endpoint returning JSON:

```java
package com.example.taskmanager.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Map;

@RestController
@RequestMapping("/api/hello")
public class HelloController {

    @GetMapping
    public Map<String, String> sayHello() {
        return Map.of("message", "Hello, Spring Boot!");
    }
}
```

Run the app and visit `GET http://localhost:8080/api/hello`:

```json
{ "message": "Hello, Spring Boot!" }
```

**Key annotations:**

| Annotation | Purpose |
|---|---|
| `@RestController` | Combines `@Controller` + `@ResponseBody`; returns data, not views |
| `@RequestMapping` | Base path for all endpoints in the class |
| `@GetMapping` / `@PostMapping` / `@PutMapping` / `@DeleteMapping` | HTTP method shortcuts |

---

## 6. Configuration (application.yml)

Spring Boot supports YAML or `.properties`. YAML is preferred for readability with nested config and profiles.

**`src/main/resources/application.yml`:**

```yaml
spring:
  application:
    name: task-manager
  profiles:
    active: dev

server:
  port: 8080

logging:
  level:
    root: INFO
    com.example.taskmanager: DEBUG
```

**`src/main/resources/application-dev.yml`:**

```yaml
spring:
  datasource:
    url: jdbc:h2:mem:taskdb
    driver-class-name: org.h2.Driver
    username: sa
    password: ""
  h2:
    console:
      enabled: true
      path: /h2-console
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        format_sql: true
```

**`src/main/resources/application-prod.yml`:**

```yaml
spring:
  datasource:
    url: ${DB_URL}
    username: ${DB_USERNAME}
    password: ${DB_PASSWORD}
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: false

logging:
  level:
    root: WARN
```

Activate a profile via environment variable or flag:

```bash
java -jar app.jar --spring.profiles.active=prod
```

---

## 7. Layered Architecture: Service Layer

Never put business logic in controllers. Use an interface + implementation for testability.

```java
package com.example.taskmanager.service;

import com.example.taskmanager.dto.TaskRequest;
import com.example.taskmanager.dto.TaskResponse;

import java.util.List;

public interface TaskService {
    TaskResponse createTask(TaskRequest request);
    TaskResponse getTaskById(Long id);
    List<TaskResponse> getAllTasks();
    TaskResponse updateTask(Long id, TaskRequest request);
    void deleteTask(Long id);
}
```

```java
package com.example.taskmanager.service.impl;

import com.example.taskmanager.dto.TaskRequest;
import com.example.taskmanager.dto.TaskResponse;
import com.example.taskmanager.exception.ResourceNotFoundException;
import com.example.taskmanager.mapper.TaskMapper;
import com.example.taskmanager.model.Task;
import com.example.taskmanager.repository.TaskRepository;
import com.example.taskmanager.service.TaskService;
import lombok.RequiredArgsConstructor;
import org.springframework.cache.annotation.CacheEvict;
import org.springframework.cache.annotation.Cacheable;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;

@Service
@RequiredArgsConstructor
public class TaskServiceImpl implements TaskService {

    private final TaskRepository taskRepository;
    private final TaskMapper taskMapper;

    @Override
    @Transactional
    @CacheEvict(value = "tasks", allEntries = true)
    public TaskResponse createTask(TaskRequest request) {
        Task task = taskMapper.toEntity(request);
        Task saved = taskRepository.save(task);
        return taskMapper.toResponse(saved);
    }

    @Override
    @Cacheable(value = "task", key = "#id")
    public TaskResponse getTaskById(Long id) {
        Task task = taskRepository.findById(id)
                .orElseThrow(() -> new ResourceNotFoundException("Task not found with id: " + id));
        return taskMapper.toResponse(task);
    }

    @Override
    @Cacheable(value = "tasks")
    public List<TaskResponse> getAllTasks() {
        return taskRepository.findAll()
                .stream()
                .map(taskMapper::toResponse)
                .toList();
    }

    @Override
    @Transactional
    @CacheEvict(value = {"task", "tasks"}, allEntries = true)
    public TaskResponse updateTask(Long id, TaskRequest request) {
        Task task = taskRepository.findById(id)
                .orElseThrow(() -> new ResourceNotFoundException("Task not found with id: " + id));

        task.setTitle(request.title());
        task.setDescription(request.description());
        task.setCompleted(request.completed());

        return taskMapper.toResponse(taskRepository.save(task));
    }

    @Override
    @Transactional
    @CacheEvict(value = {"task", "tasks"}, allEntries = true)
    public void deleteTask(Long id) {
        if (!taskRepository.existsById(id)) {
            throw new ResourceNotFoundException("Task not found with id: " + id);
        }
        taskRepository.deleteById(id);
    }
}
```

Now the controller stays thin:

```java
package com.example.taskmanager.controller;

import com.example.taskmanager.dto.TaskRequest;
import com.example.taskmanager.dto.TaskResponse;
import com.example.taskmanager.service.TaskService;
import jakarta.validation.Valid;
import lombok.RequiredArgsConstructor;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/tasks")
@RequiredArgsConstructor
public class TaskController {

    private final TaskService taskService;

    @PostMapping
    public ResponseEntity<TaskResponse> create(@Valid @RequestBody TaskRequest request) {
        TaskResponse response = taskService.createTask(request);
        return ResponseEntity.status(HttpStatus.CREATED).body(response);
    }

    @GetMapping("/{id}")
    public ResponseEntity<TaskResponse> getById(@PathVariable Long id) {
        return ResponseEntity.ok(taskService.getTaskById(id));
    }

    @GetMapping
    public ResponseEntity<List<TaskResponse>> getAll() {
        return ResponseEntity.ok(taskService.getAllTasks());
    }

    @PutMapping("/{id}")
    public ResponseEntity<TaskResponse> update(@PathVariable Long id,
                                                @Valid @RequestBody TaskRequest request) {
        return ResponseEntity.ok(taskService.updateTask(id, request));
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> delete(@PathVariable Long id) {
        taskService.deleteTask(id);
        return ResponseEntity.noContent().build();
    }
}
```

---

## 8. Persistence with Spring Data JPA

**Entity:**

```java
package com.example.taskmanager.model;

import jakarta.persistence.*;
import lombok.*;

import java.time.LocalDateTime;

@Entity
@Table(name = "tasks")
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class Task {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false, length = 150)
    private String title;

    @Column(length = 1000)
    private String description;

    @Column(nullable = false)
    @Builder.Default
    private boolean completed = false;

    @Column(updatable = false)
    private LocalDateTime createdAt;

    @PrePersist
    protected void onCreate() {
        this.createdAt = LocalDateTime.now();
    }
}
```

**Repository** — Spring Data generates the implementation at runtime:

```java
package com.example.taskmanager.repository;

import com.example.taskmanager.model.Task;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;

import java.util.List;

public interface TaskRepository extends JpaRepository<Task, Long> {

    List<Task> findByCompleted(boolean completed);

    List<Task> findByTitleContainingIgnoreCase(String keyword);

    @Query("SELECT t FROM Task t WHERE t.completed = false ORDER BY t.createdAt DESC")
    List<Task> findPendingTasksOrderedByDate();

    @Query("SELECT COUNT(t) FROM Task t WHERE t.completed = :status")
    long countByStatus(@Param("status") boolean status);
}
```

`JpaRepository<Task, Long>` already gives you `save`, `findById`, `findAll`, `deleteById`, `count`, and more — for free.

---

## 9. DTOs and Validation

Never expose entities directly. Use Java `record`s as immutable DTOs.

```java
package com.example.taskmanager.dto;

import jakarta.validation.constraints.NotBlank;
import jakarta.validation.constraints.Size;

public record TaskRequest(
        @NotBlank(message = "Title is required")
        @Size(max = 150, message = "Title must not exceed 150 characters")
        String title,

        @Size(max = 1000, message = "Description must not exceed 1000 characters")
        String description,

        boolean completed
) {}
```

```java
package com.example.taskmanager.dto;

import java.time.LocalDateTime;

public record TaskResponse(
        Long id,
        String title,
        String description,
        boolean completed,
        LocalDateTime createdAt
) {}
```

**Mapper:**

```java
package com.example.taskmanager.mapper;

import com.example.taskmanager.dto.TaskRequest;
import com.example.taskmanager.dto.TaskResponse;
import com.example.taskmanager.model.Task;
import org.springframework.stereotype.Component;

@Component
public class TaskMapper {

    public Task toEntity(TaskRequest request) {
        return Task.builder()
                .title(request.title())
                .description(request.description())
                .completed(request.completed())
                .build();
    }

    public TaskResponse toResponse(Task task) {
        return new TaskResponse(
                task.getId(),
                task.getTitle(),
                task.getDescription(),
                task.isCompleted(),
                task.getCreatedAt()
        );
    }
}
```

---

## 10. Global Exception Handling

Centralize error handling with `@RestControllerAdvice` instead of try/catch in every controller.

```java
package com.example.taskmanager.exception;

public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
```

```java
package com.example.taskmanager.exception;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.validation.FieldError;
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
        body.put("error", "Not Found");
        body.put("message", ex.getMessage());
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(body);
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, Object>> handleValidation(MethodArgumentNotValidException ex) {
        Map<String, String> errors = new HashMap<>();
        for (FieldError error : ex.getBindingResult().getFieldErrors()) {
            errors.put(error.getField(), error.getDefaultMessage());
        }

        Map<String, Object> body = new HashMap<>();
        body.put("timestamp", LocalDateTime.now());
        body.put("status", HttpStatus.BAD_REQUEST.value());
        body.put("error", "Validation Failed");
        body.put("details", errors);
        return ResponseEntity.badRequest().body(body);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<Map<String, Object>> handleGeneric(Exception ex) {
        Map<String, Object> body = new HashMap<>();
        body.put("timestamp", LocalDateTime.now());
        body.put("status", HttpStatus.INTERNAL_SERVER_ERROR.value());
        body.put("error", "Internal Server Error");
        body.put("message", ex.getMessage());
        return ResponseEntity.internalServerError().body(body);
    }
}
```

---

## 11. Dependency Injection Explained

Spring manages object creation and wiring through its **IoC container**. Three ways to inject dependencies:

```java
// 1. Constructor injection (RECOMMENDED — enables immutability & easy testing)
@Service
public class OrderService {
    private final PaymentService paymentService;

    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}

// 2. Lombok shortcut for constructor injection
@Service
@RequiredArgsConstructor
public class OrderService {
    private final PaymentService paymentService;
}

// 3. Field injection (AVOID in production code — hard to test, hides dependencies)
@Service
public class OrderService {
    @Autowired
    private PaymentService paymentService;
}
```

**Bean scopes:**

| Scope | Behavior |
|---|---|
| `singleton` (default) | One instance per Spring container |
| `prototype` | New instance every injection/request |
| `request` | One instance per HTTP request (web apps) |
| `session` | One instance per HTTP session |

---

## 12. Testing

**Unit test (service layer, Mockito):**

```java
package com.example.taskmanager.service;

import com.example.taskmanager.dto.TaskRequest;
import com.example.taskmanager.dto.TaskResponse;
import com.example.taskmanager.mapper.TaskMapper;
import com.example.taskmanager.model.Task;
import com.example.taskmanager.repository.TaskRepository;
import com.example.taskmanager.service.impl.TaskServiceImpl;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import java.util.Optional;

import static org.assertj.core.api.Assertions.assertThat;
import static org.mockito.Mockito.when;

@ExtendWith(MockitoExtension.class)
class TaskServiceTest {

    @Mock
    private TaskRepository taskRepository;

    @Mock
    private TaskMapper taskMapper;

    @InjectMocks
    private TaskServiceImpl taskService;

    private Task task;

    @BeforeEach
    void setUp() {
        task = Task.builder().id(1L).title("Write tests").completed(false).build();
    }

    @Test
    void getTaskById_returnsTask_whenFound() {
        when(taskRepository.findById(1L)).thenReturn(Optional.of(task));
        when(taskMapper.toResponse(task))
                .thenReturn(new TaskResponse(1L, "Write tests", null, false, null));

        TaskResponse result = taskService.getTaskById(1L);

        assertThat(result.title()).isEqualTo("Write tests");
    }
}
```

**Integration test (full context, MockMvc):**

```java
package com.example.taskmanager.controller;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.example.taskmanager.dto.TaskRequest;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.http.MediaType;
import org.springframework.security.test.context.support.WithMockUser;
import org.springframework.test.web.servlet.MockMvc;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.post;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@SpringBootTest
@AutoConfigureMockMvc
class TaskControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Autowired
    private ObjectMapper objectMapper;

    @Test
    @WithMockUser
    void createTask_returns201() throws Exception {
        TaskRequest request = new TaskRequest("New Task", "Description", false);

        mockMvc.perform(post("/api/tasks")
                        .contentType(MediaType.APPLICATION_JSON)
                        .content(objectMapper.writeValueAsString(request)))
                .andExpect(status().isCreated())
                .andExpect(jsonPath("$.title").value("New Task"));
    }
}
```

---

## 13. Spring Security + JWT

**Security configuration:**

```java
package com.example.taskmanager.config;

import com.example.taskmanager.security.JwtAuthFilter;
import lombok.RequiredArgsConstructor;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.config.annotation.authentication.configuration.AuthenticationConfiguration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;

@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class SecurityConfig {

    private final JwtAuthFilter jwtAuthFilter;

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    @Bean
    public AuthenticationManager authenticationManager(AuthenticationConfiguration config) throws Exception {
        return config.getAuthenticationManager();
    }

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf(csrf -> csrf.disable())
            .sessionManagement(sm -> sm.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
            .authorizeHttpRequests(auth -> auth
                    .requestMatchers("/api/auth/**", "/actuator/health").permitAll()
                    .requestMatchers("/api/tasks/**").authenticated()
                    .anyRequest().authenticated()
            )
            .addFilterBefore(jwtAuthFilter, UsernamePasswordAuthenticationFilter.class);

        return http.build();
    }
}
```

**JWT service:**

```java
package com.example.taskmanager.security;

import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.security.Keys;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;

import javax.crypto.SecretKey;
import java.util.Date;
import java.util.function.Function;

@Service
public class JwtService {

    @Value("${jwt.secret}")
    private String secret;

    @Value("${jwt.expiration-ms:3600000}")
    private long expirationMs;

    private SecretKey getSigningKey() {
        return Keys.hmacShaKeyFor(secret.getBytes());
    }

    public String generateToken(String username) {
        return Jwts.builder()
                .subject(username)
                .issuedAt(new Date())
                .expiration(new Date(System.currentTimeMillis() + expirationMs))
                .signWith(getSigningKey())
                .compact();
    }

    public String extractUsername(String token) {
        return extractClaim(token, Claims::getSubject);
    }

    public boolean isTokenValid(String token, String username) {
        return extractUsername(token).equals(username) && !isTokenExpired(token);
    }

    private boolean isTokenExpired(String token) {
        return extractClaim(token, Claims::getExpiration).before(new Date());
    }

    private <T> T extractClaim(String token, Function<Claims, T> resolver) {
        Claims claims = Jwts.parser()
                .verifyWith(getSigningKey())
                .build()
                .parseSignedClaims(token)
                .getPayload();
        return resolver.apply(claims);
    }
}
```

**JWT filter:**

```java
package com.example.taskmanager.security;

import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import lombok.RequiredArgsConstructor;
import org.springframework.lang.NonNull;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.web.authentication.WebAuthenticationDetailsSource;
import org.springframework.stereotype.Component;
import org.springframework.web.filter.OncePerRequestFilter;

import java.io.IOException;

@Component
@RequiredArgsConstructor
public class JwtAuthFilter extends OncePerRequestFilter {

    private final JwtService jwtService;
    private final UserDetailsService userDetailsService;

    @Override
    protected void doFilterInternal(@NonNull HttpServletRequest request,
                                     @NonNull HttpServletResponse response,
                                     @NonNull FilterChain filterChain) throws ServletException, IOException {

        String authHeader = request.getHeader("Authorization");

        if (authHeader == null || !authHeader.startsWith("Bearer ")) {
            filterChain.doFilter(request, response);
            return;
        }

        String token = authHeader.substring(7);
        String username = jwtService.extractUsername(token);

        if (username != null && SecurityContextHolder.getContext().getAuthentication() == null) {
            UserDetails userDetails = userDetailsService.loadUserByUsername(username);

            if (jwtService.isTokenValid(token, username)) {
                UsernamePasswordAuthenticationToken authToken =
                        new UsernamePasswordAuthenticationToken(userDetails, null, userDetails.getAuthorities());
                authToken.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
                SecurityContextHolder.getContext().setAuthentication(authToken);
            }
        }

        filterChain.doFilter(request, response);
    }
}
```

Add to `application.yml`:

```yaml
jwt:
  secret: ${JWT_SECRET:change-this-to-a-long-random-secret-in-production}
  expiration-ms: 3600000
```

---

## 14. Caching

Spring's cache abstraction works with any provider (in-memory `ConcurrentMapCache`, Caffeine, Redis).

```java
package com.example.taskmanager.config;

import com.github.benmanes.caffeine.cache.Caffeine;
import org.springframework.cache.CacheManager;
import org.springframework.cache.caffeine.CaffeineCacheManager;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import java.util.concurrent.TimeUnit;

@Configuration
public class CacheConfig {

    @Bean
    public CacheManager cacheManager() {
        CaffeineCacheManager cacheManager = new CaffeineCacheManager("task", "tasks");
        cacheManager.setCaffeine(Caffeine.newBuilder()
                .expireAfterWrite(10, TimeUnit.MINUTES)
                .maximumSize(500));
        return cacheManager;
    }
}
```

Usage (`@Cacheable`, `@CacheEvict`) is already shown in the service layer in Section 7.

---

## 15. Async & Scheduled Tasks

**Async execution:**

```java
package com.example.taskmanager.service;

import lombok.extern.slf4j.Slf4j;
import org.springframework.scheduling.annotation.Async;
import org.springframework.stereotype.Service;

@Service
@Slf4j
public class NotificationService {

    @Async
    public void sendTaskCompletedNotification(String taskTitle) {
        log.info("Sending notification for completed task: {}", taskTitle);
        // Runs on a separate thread — does not block the caller
    }
}
```

**Scheduled job:**

```java
package com.example.taskmanager.service;

import lombok.RequiredArgsConstructor;
import lombok.extern.slf4j.Slf4j;
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

@Component
@RequiredArgsConstructor
@Slf4j
public class TaskCleanupJob {

    private final TaskRepository taskRepository;

    // Runs every day at 2 AM
    @Scheduled(cron = "0 0 2 * * *")
    public void purgeOldCompletedTasks() {
        log.info("Running scheduled cleanup of old completed tasks");
        // cleanup logic here
    }
}
```

---

## 16. Actuator & Observability

Add production-ready monitoring endpoints:

```yaml
management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus
  endpoint:
    health:
      show-details: when-authorized
```

Key endpoints once enabled:

| Endpoint | Purpose |
|---|---|
| `/actuator/health` | Liveness/readiness checks |
| `/actuator/metrics` | JVM, HTTP, and custom metrics |
| `/actuator/info` | Build/app metadata |
| `/actuator/prometheus` | Prometheus-scrapeable metrics |

---

## 17. Dockerizing the App

**`Dockerfile`** (multi-stage build for a small final image):

```dockerfile
# --- Build stage ---
FROM eclipse-temurin:17-jdk-alpine AS build
WORKDIR /app
COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .
RUN ./mvnw dependency:go-offline -B
COPY src src
RUN ./mvnw clean package -DskipTests

# --- Run stage ---
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

**`docker-compose.yml`** (app + PostgreSQL):

```yaml
version: "3.8"

services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      SPRING_PROFILES_ACTIVE: prod
      DB_URL: jdbc:postgresql://db:5432/taskdb
      DB_USERNAME: taskuser
      DB_PASSWORD: taskpass
      JWT_SECRET: super-secret-production-key-change-me
    depends_on:
      - db

  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_DB: taskdb
      POSTGRES_USER: taskuser
      POSTGRES_PASSWORD: taskpass
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

Build and run:

```bash
docker compose up --build
```

---

## 18. Best Practices

- **Constructor injection only** — avoid `@Autowired` on fields; it hides dependencies and complicates testing.
- **DTOs at the boundary** — never expose JPA entities directly in API responses.
- **Validate at the edge** — use `@Valid` + Bean Validation annotations on request DTOs.
- **Centralize error handling** — one `@RestControllerAdvice`, not scattered try/catch blocks.
- **Profile-based config** — separate `application-dev.yml` / `application-prod.yml`; never hardcode secrets.
- **Stateless auth** — JWT with `SessionCreationPolicy.STATELESS` for horizontally scalable APIs.
- **Transactional boundaries** — put `@Transactional` on service methods, not repositories or controllers.
- **Test both layers** — unit tests for service logic (Mockito), integration tests for the full HTTP flow (MockMvc).
- **Least privilege on endpoints** — default to `authenticated()`, explicitly `permitAll()` only what's public.
- **Externalize secrets** — use environment variables or a secrets manager, never commit them to Git.

---

## 19. Common Pitfalls

| Pitfall | Fix |
|---|---|
| `ddl-auto: update` in production | Use `validate` and manage schema with Flyway/Liquibase migrations |
| Returning entities from controllers | Map to DTOs — avoids lazy-loading exceptions and leaking internal fields |
| Field injection everywhere | Switch to constructor injection (`@RequiredArgsConstructor`) |
| No exception handling | Add a `@RestControllerAdvice` early, not as an afterthought |
| Hardcoded secrets in `application.yml` | Use `${ENV_VAR}` placeholders |
| Blocking calls inside `@Async` without a custom executor | Configure a dedicated `ThreadPoolTaskExecutor` bean |
| Missing `@Transactional` on multi-step writes | Wrap service methods that touch multiple repositories |
| Forgetting CORS config for frontend apps | Add a `CorsConfigurationSource` bean or `@CrossOrigin` |

---

## License

This guide and its code samples are provided under the [MIT License](https://opensource.org/licenses/MIT) — free to use in your own projects.
