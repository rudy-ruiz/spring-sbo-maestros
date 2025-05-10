# API de Maestros para SAP Business One

Este proyecto implementa un sistema modular y robusto de gestión de maestros (**Clientes**, **Proveedores** e **Inventarios**) usando **Java 21**, **Spring Boot 3.4.5**, **PostgreSQL** y patrones de diseño **Singleton**, **Facade** y **Decorator**. Incluye integración con **Swagger UI** para facilitar el consumo de los servicios.

---

## 🔧 Instalación y Ejecución

### Requisitos

- Java 21
- Maven 3.8+
- PostgreSQL 14+
- Docker (opcional para base de datos)

### Configuración

Edita el archivo `src/main/resources/application.yml`:

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/sapdb
    username: postgres
    password: your_password
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        dialect: org.hibernate.dialect.PostgreSQLDialect
server:
  port: 8080
```

### Ejecutar la aplicación

```bash
mvn spring-boot:run
```

### Acceso a Swagger UI

> http://localhost:8080/swagger-ui.html

---

## 🔄 Endpoints Disponibles

### Clientes
- `POST /api/maestros/clientes`
- `PUT /api/maestros/clientes/{id}`
- `GET /api/maestros/clientes/{id}`
- `GET /api/maestros/clientes`
- `DELETE /api/maestros/clientes/{id}`

### Proveedores
- `POST /api/maestros/proveedores`
- `PUT /api/maestros/proveedores/{id}`
- `GET /api/maestros/proveedores/{id}`
- `GET /api/maestros/proveedores`
- `DELETE /api/maestros/proveedores/{id}`

### Inventarios
- `POST /api/maestros/inventarios`
- `PUT /api/maestros/inventarios/{id}`
- `GET /api/maestros/inventarios/{id}`
- `GET /api/maestros/inventarios`
- `DELETE /api/maestros/inventarios/{id}`

---

## 📦 Swagger Integration

### Dependencia (añadir en `pom.xml`):
```xml
<dependency>
  <groupId>org.springdoc</groupId>
  <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
  <version>2.2.0</version>
</dependency>
```

### URL Swagger
http://localhost:8080/swagger-ui.html

---

## 🧠 Patrones de Diseño Usados

### ✅ Singleton
Cada clase de gestión (`ClienteManager`, `ProveedorManager`, `InventarioManager`) se implementa como Singleton dentro del contexto de Spring para asegurar una única instancia por entidad, evitando inconsistencias.

### ✅ Facade
`MaestroFacade` es la única puerta de entrada a las operaciones sobre los maestros, facilitando el uso del sistema desde los controladores y desacoplando la lógica.

### ✅ Decorator
`*ValidationDecorator` se usa para validar datos antes de la persistencia (duplicados, consistencia, reglas SAP), sin modificar la lógica original del servicio.

---

## 🧱 Justificación de la Arquitectura

- **Modularidad:** cada maestro está encapsulado en su propia lógica y servicio.
- **Extensibilidad:** fácilmente se pueden incorporar nuevos maestros.
- **Desacoplamiento:** separación clara entre controladores, lógica, validación y persistencia.
- **Reutilización:** lógica común encapsulada en servicios y decoradores reutilizables.
- **Seguridad de Datos:** validaciones previas y patrón Singleton para garantizar consistencia.

---

## 🔍 Análisis Técnico

- Uso de **Java 21** y **Spring Boot 3.4.5** aprovecha mejoras de rendimiento, seguridad y simplificación del código (ej. `record`, `Pattern Matching`).
- Spring Context gestiona los Singletons automáticamente.
- Se evita lógica duplicada gracias a la estructura base/decorator.
- La arquitectura promueve prácticas SOLID, separación de responsabilidades y bajo acoplamiento.
- PostgreSQL garantiza integridad de datos y es compatible con los modelos contables de SAP B1 (ej. `codigoSAP`).

---

## 📦 Futuras Mejoras

- Integración con SAP Service Layer o DI API
- Control global de excepciones (handler)
- DTOs + mapeo con MapStruct o ModelMapper
- Autenticación con JWT + roles
- Pruebas unitarias y de integración con JUnit y Testcontainers
- Configuración con Profiles (`dev`, `prod`)
- Contenerización con Docker + docker-compose

---

## 🧪 Docker (Base PostgreSQL Opcional)

```yaml
version: '3.1'
services:
  postgres:
    image: postgres:14
    restart: always
    environment:
      POSTGRES_DB: sapdb
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: your_password
    ports:
      - "5432:5432"
```

---

## 👨‍💻 Autor

Desarrollado por el equipo de PE - Rudy Ruiz  
📧 rudy.ruiz@
