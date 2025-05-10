# API de Maestros para SAP Business One

Este proyecto implementa un sistema modular y robusto de gestión de maestros (Clientes, Proveedores e Inventarios) usando **Java 21**, **Spring Boot 3.4.5**, **PostgreSQL** y patrones de diseño **Singleton**, **Facade** y **Decorator**. Incluye integración con **Swagger UI** para facilitar el consumo de los servicios.

---

## 🔧 Instalación y Ejecución

### Requisitos

- Java 21
- Maven 3.8+
- PostgreSQL 14+
- Docker (opcional para BD)

### Configuración

Ajusta `src/main/resources/application.yml` con tus credenciales de PostgreSQL.

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/sapdb
    username: postgres
    password: your_password
