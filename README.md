# 🦸‍♂️ Vault-M

> Tu Colección de Cómics Marvel, Organizada y Lista para Intercambiar

Vault-M es un sistema integral de gestión de colecciones de cómics diseñado para fans y coleccionistas de Marvel. Construido con principios de Domain-Driven Design (DDD) y patrones de arquitectura de software modernos, proporciona una plataforma robusta para organizar, valorar e intercambiar tu colección de cómics.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![.NET](https://img.shields.io/badge/.NET-8.0-purple.svg)](https://dotnet.microsoft.com/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

---

## ✨ Características

### 📚 Gestión de Colecciones
- **Organiza tus cómics** en colecciones personalizadas con metadata detallada
- **Rastrea la condición física** (Mint, Near Mint, Good, Fair, Poor)
- **Registra precios de adquisición** y sigue el valor de tu colección en el tiempo
- **Colecciones públicas o privadas** - comparte con la comunidad o mantenlas personales
- **Estadísticas inteligentes** - tasas de completitud, seguimiento de series y más

### 🔄 Sistema de Intercambios
- **Propone intercambios** con otros coleccionistas
- **Calculadora de equidad** para asegurar intercambios justos
- **Ciclo de vida completo** desde la propuesta hasta la finalización
- **Sistema de seguimiento** de envíos y confirmaciones
- **Resolución de disputas** para intercambios problemáticos
- **Historial de intercambios** para construir reputación

### 🎯 Lista de Deseos
- **Marca cómics que buscas** con criterios específicos (precio máximo, condición mínima)
- **Notificaciones automáticas** cuando cómics deseados están disponibles para intercambio
- **Priorización inteligente** basada en tus preferencias

### 💰 Sistema de Valuación
- **Estimación de valor de mercado** basada en intercambios reales
- **Reportes de valuación** detallados de tus colecciones
- **Tracking de tendencias** de precios en el tiempo
- **Depreciación automática** según condición física

### 🔍 Catálogo Marvel
- **Integración con Marvel API** para información actualizada
- **Búsqueda avanzada** por título, personaje, año, creador
- **Sincronización automática** de metadata
- **Información detallada** de personajes y sus apariciones

---

## 🏗️ Arquitectura

Este proyecto está diseñado como una aplicación educativa para practicar y demostrar:

### Patrones de DDD Implementados
- **Bounded Contexts** claramente definidos (Catalog, Collection, Trading, Wishlist, Valuation)
- **Aggregates** con raíces bien identificadas
- **Value Objects** para conceptos del dominio
- **Domain Events** para comunicación entre contextos
- **Repository Pattern** con abstracciones claras
- **Domain Services** para lógica de negocio compleja

### Patrones Arquitectónicos
- **Clean Architecture** con separación de capas
- **CQRS** para optimizar lecturas y escrituras
- **Event Sourcing** para auditoría y tracking
- **Unit of Work** para transacciones consistentes
- **Specification Pattern** para consultas complejas
- **Factory Pattern** para creación de entidades complejas

### Bounded Contexts

```
┌─────────────────────────────────────────────────────────┐
│                      Vault-M System                      │
├─────────────┬──────────────┬──────────────┬─────────────┤
│   Catalog   │  Collection  │   Trading    │  Wishlist   │
│             │              │              │             │
│ - Comics    │ - Collections│ - Trades     │ - Wishlist  │
│ - Characters│ - Items      │ - Disputes   │ - Matching  │
│ - Sync      │ - Stats      │ - Shipping   │ - Alerts    │
└─────────────┴──────────────┴──────────────┴─────────────┘
                              │
                      ┌───────┴────────┐
                      │   Valuation    │
                      │                │
                      │ - Market Price │
                      │ - Reports      │
                      │ - Trends       │
                      └────────────────┘
```

---

## 🚀 Tecnologías

- **.NET 8** - Framework principal
- **Entity Framework Core** - ORM y persistencia
- **MediatR** - CQRS y manejo de eventos
- **FluentValidation** - Validaciones de dominio
- **AutoMapper** - Mapeo entre capas
- **Marvel API** - Datos de cómics y personajes
- **PostgreSQL** - Base de datos principal
- **Redis** - Caché distribuido
- **RabbitMQ** - Message broker para eventos
- **Docker** - Contenerización
- **xUnit** - Testing

---

## 📁 Estructura del Proyecto

```
src/
├── Vault-M.Domain/              # Capa de dominio (entidades, value objects, eventos)
│   ├── Aggregates/
│   │   ├── CollectionAggregate/
│   │   ├── TradeAggregate/
│   │   └── WishlistAggregate/
│   ├── Events/
│   ├── Services/
│   └── ValueObjects/
│
├── Vault-M.Application/         # Lógica de aplicación (use cases, CQRS)
│   ├── Commands/
│   ├── Queries/
│   ├── DTOs/
│   └── Interfaces/
│
├── Vault-M.Infrastructure/      # Implementaciones técnicas
│   ├── Persistence/
│   ├── ExternalServices/
│   │   └── MarvelApi/
│   ├── Messaging/
│   └── Caching/
│
└── Vault-M.API/                 # API REST
    ├── Controllers/
    ├── Middleware/
    └── Configuration/

tests/
├── Vault-M.Domain.Tests/        # Tests unitarios de dominio
├── Vault-M.Application.Tests/   # Tests de casos de uso
└── Vault-M.Integration.Tests/   # Tests de integración
```

---

## 🛠️ Instalación y Configuración

### Prerrequisitos

- .NET 8 SDK o superior
- Docker y Docker Compose
- Una API Key de Marvel (obtener en [Marvel Developer Portal](https://developer.marvel.com/))

### Configuración

1. **Clona el repositorio**
```bash
git clone https://github.com/tu-usuario/vault-m.git
cd vault-m
```

2. **Configura las variables de entorno**
```bash
cp .env.example .env
# Edita .env y agrega tu Marvel API Key
```

3. **Levanta los servicios con Docker**
```bash
docker-compose up -d
```

4. **Ejecuta las migraciones**
```bash
dotnet ef database update --project src/Vault-M.Infrastructure
```

5. **Ejecuta la aplicación**
```bash
dotnet run --project src/Vault-M.API
```

La API estará disponible en `https://localhost:5001`

### Configuración de Marvel API

Registra tu aplicación en [Marvel Developer Portal](https://developer.marvel.com/) y obtén:
- Public Key
- Private Key

Agrégalas a tu `appsettings.json` o variables de entorno:

```json
{
  "MarvelApi": {
    "PublicKey": "tu_public_key",
    "PrivateKey": "tu_private_key",
    "BaseUrl": "https://gateway.marvel.com/v1/public"
  }
}
```

---

## 📖 Documentación

### Casos de Uso Principales

#### 1️⃣ Crear una Colección
```http
POST /api/collections
Content-Type: application/json

{
  "name": "Mi Colección de Spider-Man",
  "description": "Todos mis cómics del trepa-muros",
  "isPublic": true
}
```

#### 2️⃣ Agregar un Cómic a la Colección
```http
POST /api/collections/{collectionId}/comics
Content-Type: application/json

{
  "marvelComicId": 12345,
  "condition": "NearMint",
  "purchasePrice": 15.99,
  "notes": "Comprado en Comic-Con 2023",
  "availableForTrade": true
}
```

#### 3️⃣ Proponer un Intercambio
```http
POST /api/trades
Content-Type: application/json

{
  "offeredComicIds": [1, 2, 3],
  "requestedComicIds": [4, 5],
  "message": "Hola! Me interesan tus cómics de Thor"
}
```

#### 4️⃣ Buscar Cómics
```http
GET /api/comics/search?title=spider-man&year=2023&limit=20
```

Para documentación completa de la API, visita `/swagger` cuando la aplicación esté corriendo.

---

## 🧪 Testing

### Ejecutar todos los tests
```bash
dotnet test
```

### Tests por proyecto
```bash
# Tests unitarios de dominio
dotnet test tests/Vault-M.Domain.Tests

# Tests de aplicación
dotnet test tests/Vault-M.Application.Tests

# Tests de integración
dotnet test tests/Vault-M.Integration.Tests
```

### Coverage
```bash
dotnet test /p:CollectCoverage=true /p:CoverletOutputFormat=opencover
```

---

## 🎯 Roadmap

### Fase 1 - MVP ✅
- [x] Definición de bounded contexts
- [x] Modelado de agregados principales
- [x] Casos de uso documentados
- [ ] Implementación de Collection Context
- [ ] Integración con Marvel API
- [ ] API REST básica

### Fase 2 - Trading System
- [ ] Sistema completo de intercambios
- [ ] Calculadora de equidad
- [ ] Sistema de reputación
- [ ] Notificaciones en tiempo real

### Fase 3 - Valuación y Analytics
- [ ] Sistema de valuación de mercado
- [ ] Reportes y estadísticas
- [ ] Tracking de tendencias
- [ ] Gráficas de evolución

### Fase 4 - Funcionalidades Sociales
- [ ] Sistema de seguimiento entre usuarios
- [ ] Reviews y ratings
- [ ] Feed de actividad
- [ ] Comunidad y foros

### Fase 5 - Mobile y Optimizaciones
- [ ] App móvil (React Native)
- [ ] Modo offline
- [ ] Escáner de códigos de barras
- [ ] Optimizaciones de performance

---

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Este es un proyecto educativo diseñado para aprender y practicar DDD y arquitectura de software.

### Cómo contribuir

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

### Guías de Contribución

- Sigue los principios de DDD y Clean Architecture
- Escribe tests para tu código
- Documenta las decisiones arquitectónicas importantes
- Mantén los commits atómicos y descriptivos
- Actualiza la documentación si es necesario

---

## 📚 Recursos de Aprendizaje

Este proyecto implementa conceptos de:

- **Domain-Driven Design** - Eric Evans
- **Implementing Domain-Driven Design** - Vaughn Vernon
- **Clean Architecture** - Robert C. Martin
- **Enterprise Integration Patterns** - Gregor Hohpe

### Artículos y Referencias
- [Microsoft - .NET Microservices Architecture](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/)
- [Martin Fowler - Domain Event](https://martinfowler.com/eaaDev/DomainEvent.html)
- [Marvel API Documentation](https://developer.marvel.com/docs)

---

## 📄 Licencia

Este proyecto está bajo la licencia MIT. Ver el archivo [LICENSE](LICENSE) para más detalles.

---

## ⚖️ Disclaimer

Vault-M es una aplicación independiente y no está afiliada, respaldada o patrocinada por Marvel Entertainment, LLC. Todos los personajes de Marvel y el contenido de los cómics son marcas registradas y derechos de autor de Marvel Entertainment, LLC.

Este proyecto utiliza la API pública de Marvel con fines educativos y de desarrollo de software.

---

## 👨‍💻 Autor

**Tu Nombre**
- GitHub: [@tu-usuario](https://github.com/tu-usuario)
- LinkedIn: [tu-perfil](https://linkedin.com/in/tu-perfil)

---

## 🌟 Agradecimientos

- Marvel por proporcionar su API pública
- La comunidad de DDD y Clean Architecture
- Todos los contribuidores que hacen este proyecto mejor

---

## 📞 Contacto y Soporte

¿Tienes preguntas o sugerencias? 

- 📧 Email: tu-email@ejemplo.com
- 💬 Discussions: [GitHub Discussions](https://github.com/tu-usuario/vault-m/discussions)
- 🐛 Issues: [GitHub Issues](https://github.com/tu-usuario/vault-m/issues)

---

<p align="center">
  Hecho con ❤️ para la comunidad de coleccionistas de Marvel
</p>

<p align="center">
  <sub>Si este proyecto te ayudó, considera darle una ⭐</sub>
</p>
