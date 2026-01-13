# Eureka Server

## 📌 Overview

This repository contains the **Eureka Server**, a **service registry** used for **service discovery** in a microservices architecture.

All microservices register themselves with Eureka and discover other services dynamically, eliminating the need for hard-coded service endpoints.

---

## 🎯 Key Responsibilities

* Central service registry
* Service instance registration & deregistration
* Health-based service availability tracking
* Enables client-side load balancing
* Supports dynamic scaling of microservices

---

## 🧱 Architecture Role

```
┌─────────────┐      Register / Heartbeat
│  Service A  │ ─────────────────────────▶
└─────────────┘                            │
┌─────────────┐                            │
│  Service B  │ ─────────────────────────▶ │  Eureka Server
└─────────────┘                            │
┌─────────────┐                            │
│  Service C  │ ◀───────────────────────── │  Service Discovery
└─────────────┘      Discover Services     └──────────────────
```

---

## 🛠 Technology Stack

* Java 17
* Spring Boot
* Spring Cloud Netflix Eureka
* Maven

---

## 🚀 Running the Eureka Server

### 1️⃣ Build the Application

```bash
mvn clean package
```

---

### 2️⃣ Run Locally

```bash
mvn spring-boot:run
```

or

```bash
java -jar target/eureka-server.jar
```

---

### 3️⃣ Access Eureka Dashboard

```
http://localhost:8761
```

---

## ⚙ Configuration

### `application.yml`

```yaml
server:
  port: 8761

spring:
  application:
    name: eureka-server

eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
  server:
    enable-self-preservation: true
```

---

## 🔗 Registering Client Services

### Add Dependency

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

---

### Client Configuration

```yaml
spring:
  application:
    name: order-service

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka
```

---

### Enable Client

```java
@EnableEurekaClient
@SpringBootApplication
public class OrderServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(OrderServiceApplication.class, args);
    }
}
```

---

## 🧠 Best Practices

* Do not deploy a single Eureka node in production
* Enable security in non-trusted networks
* Keep self-preservation enabled in production
* Avoid running Eureka in auto-scaled pods without persistence
* Prefer stable hostnames for Eureka nodes

---

## 🚨 Common Issues

| Issue                  | Cause             | Fix                      |
| ---------------------- | ----------------- | ------------------------ |
| Instances disappear    | Heartbeats missed | Check network / timeouts |
| Registry not updating  | Self-preservation | Verify configs           |
| Client not registering | Wrong URL         | Validate `defaultZone`   |

---

## 👥 Ownership & Support

Maintained by the **Platform / Architecture Team**.

For:

* Configuration changes
* Production issues

Please raise a Pull Request or contact the platform team.

---

## 📄 License

Internal use only.
Not intended for public distribution.
