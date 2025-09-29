# ☀️ Sistema IoT Solar Autónomo - Agricultura Inteligente

<div align="center">
  <img src="https://img.shields.io/badge/Status-In%20Development-yellow" alt="Status"/>
  <img src="https://img.shields.io/badge/Version-1.0.0-blue" alt="Version"/>
  <img src="https://img.shields.io/badge/Platform-ESP8266-red" alt="Platform"/>
  <img src="https://img.shields.io/badge/Architecture-Microservices-purple" alt="Microservices"/>
</div>

## 📋 Descripción

Sistema IoT profesional para monitoreo agrícola con alimentación solar, desarrollado con arquitectura de microservicios. Combina hardware embebido (ESP-01S DHT11) con backend Java Spring Boot, frontend Angular y app móvil Flutter.

## 🎯 Características Principales

- ☀️ **Sistema Solar Autónomo** - Panel solar + batería Li-Ion 18650
- 🌡️ **Monitoreo Ambiental** - Temperatura, humedad y humedad de suelo
- 🔋 **Gestión Inteligente de Energía** - Modos adaptativos según batería
- 📡 **Comunicación MQTT** - Telemetría y comandos en tiempo real
- 🕸️ **Red Mesh** - Comunicación entre múltiples dispositivos ESP
- 📱 **Interfaces Multiplataforma** - Web (Angular) y Móvil (Flutter)
- 🐳 **Infraestructura Docker** - Despliegue de microservicios

## 🛠️ Stack Tecnológico

### Hardware

- **Módulo**: ESP-01S DHT11 v1.0 TB: IOTMCU
- **Panel Solar**: ZW138x82 5V 300mA
- **Controlador**: CN3791 MPPT Solar Charger
- **Batería**: Li-Ion 18650 (2500-3500mAh)
- **Sensor Suelo**: Capacitivo I2C (recomendado)

### Firmware

- **IDE**: PlatformIO
- **Framework**: Arduino + FreeRTOS
- **Lenguaje**: C++ con arrow functions
- **Protocolo**: MQTT

### Backend (Microservicios)

- **Lenguaje**: Java 17
- **Framework**: Spring Boot 3.x
- **Base de Datos**: MySQL 8.0
- **Cache**: Redis
- **Message Broker**: RabbitMQ
- **API Docs**: Swagger/OpenAPI

### Frontend

- **Web**: Angular 16 + TypeScript
- **Mobile**: Flutter 3.x
- **UI**: Angular Material + PrimeNG

### DevOps

- **Contenedores**: Docker + Docker Compose
- **Gateway**: Spring Cloud Gateway
- **Discovery**: Eureka Server
- **Monitoring**: Grafana + Prometheus

## 📊 Diagrama de Arquitectura

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Panel Solar   │───▶│ Controlador MPPT │───▶│ Batería 18650   │
│   ZW138x82      │    │    CN3791        │    │   + Cargador    │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                                        │
                                                        ▼
┌─────────────────┐                              ┌─────────────────┐
│ Sensor Humedad  │◄─────────────────────────────┤ ESP-01S DHT11   │
│    de Suelo     │         I2C/ADC              │ Módulo IOTMCU   │
└─────────────────┘                              └─────────────────┘
                                                        │
                                                    MQTT WiFi
                                                        │
                                                        ▼
┌───────────────────────────────────────────────────────────────────┐
│                    MICROSERVICIOS (Docker)                        │
├───────────────────────────────────────────────────────────────────┤
│  API Gateway │ Eureka │ Device Service │ Sensor Service │ Power  │
└───────────────────────────────────────────────────────────────────┘
                                │
                    ┌───────────┴───────────┐
                    ▼                       ▼
            ┌───────────────┐       ┌─────────────┐
            │   Angular     │       │   Flutter   │
            │   Dashboard   │       │   App       │
            └───────────────┘       └─────────────┘
```

## 🚀 Inicio Rápido

### Requisitos Previos

```bash
# Software necesario
- Java 17+
- Node.js 18+
- Angular CLI 16+
- Flutter 3.x
- PlatformIO IDE
- Docker & Docker Compose
- MySQL 8.0
- Git
```

### Clonar Repositorio

```bash
git clone https://github.com/Shiva0616/smart-agriculture-automation.git
cd smart-agriculture-automation
```

## 📁 Estructura del Proyecto

```
smart-agriculture-ecosystem/
├── 🔧 embedded-firmware/          # Firmware PlatformIO (ESP-01S)
├── ☕ backend-services/           # Microservicios Spring Boot
│   ├── api-gateway/
│   ├── service-discovery/
│   ├── device-management/
│   ├── sensor-data-service/
│   └── power-monitoring/
├── 🌐 web-dashboard/              # Angular Dashboard
├── 📱 mobile-app/                 # Flutter App
├── 🐳 docker/                     # Docker Compose
├── 📊 database/                   # SQL Scripts
└── 📚 docs/                       # Documentación

```

## 🔧 Configuración Inicial del Dispositivo

### Modo AP de Configuración

1. Al primer encendido, el ESP-01S crea un AP WiFi:

   - **SSID**: `ESP-Agriculture-Setup`
   - **IP**: `192.168.4.1`

2. Conectar y abrir navegador en `http://192.168.4.1`

3. Configurar:
   - 📶 **Tipo de conexión**: WiFi / GSM / Mesh
   - 🏷️ **Nombre del dispositivo**
   - 📍 **Ubicación**
   - ⚙️ **Rol**: Standalone / Maestro / Esclavo

## 📡 Comunicación MQTT

### Topics Principales

```
farm/devices/{device_id}/sensors        # Datos de sensores
farm/devices/{device_id}/power          # Métricas de energía
farm/devices/{device_id}/commands       # Comandos al dispositivo
farm/devices/{device_id}/status         # Estado del dispositivo
farm/mesh/discovery                     # Descubrimiento mesh
```

### Ejemplo Payload Sensor

```json
{
  "device_id": "AA:BB:CC:DD:EE:FF",
  "timestamp": "2024-12-17T15:30:00Z",
  "sensors": {
    "temperature": 26.5,
    "humidity": 68.2,
    "soil_moisture": 45.8
  }
}
```

## 🐳 Despliegue con Docker

```bash
# Iniciar todos los servicios
cd docker
docker-compose up -d

# Servicios disponibles:
# - API Gateway: http://localhost:8080
# - Eureka Dashboard: http://localhost:8761
# - Angular App: http://localhost:4200
# - Swagger UI: http://localhost:8080/swagger-ui.html
# - RabbitMQ: http://localhost:15672
```

## 📚 Documentación API

La documentación completa de la API está disponible en Swagger:

```
http://localhost:8080/swagger-ui.html
```

## 🔮 Roadmap de Desarrollo

### ✅ Fase 1: Fundamentos (Actual)

- [x] Estructura de repositorios
- [x] README y documentación base
- [ ] Firmware básico ESP-01S
- [ ] API Gateway + Eureka
- [ ] Servicio de dispositivos

### 🚧 Fase 2: Core Features (Próximo)

- [ ] Gestión de sensores completa
- [ ] Monitoreo de energía
- [ ] Dashboard Angular básico
- [ ] MQTT Broker integrado

### 📅 Fase 3: Avanzado

- [ ] Red Mesh ESP-NOW
- [ ] App móvil Flutter
- [ ] Machine Learning
- [ ] Analytics avanzado

### 🔮 Fase 4: Producción

- [ ] CI/CD Pipeline
- [ ] Kubernetes deployment
- [ ] Monitoreo con Grafana
- [ ] Documentación completa

## 👨‍💻 Autor

**Daniel Alejandro Castañeda Suárez**  
_Ingeniero Electrónico | Full Stack Developer_

- 📧 Email: [danysuarez1606@gmail.com](mailto:danysuarez1606@gmail.com)
- 📱 WhatsApp: +57 301 388 4905
- 💼 LinkedIn: [Daniel Castañeda](https://linkedin.com/in/daniel-castaneda-dev)
- 🐙 GitHub: [@Shiva0616](https://github.com/Shiva0616)

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver archivo [LICENSE](LICENSE) para detalles.

---

<div align="center">
  <p><strong>🌱 Desarrollado con ☀️ energía solar y ❤️ pasión por la tecnología</strong></p>
</div># ☀️ Sistema IoT Solar Autónomo - Agricultura Inteligente

<div align="center">
  <img src="https://img.shields.io/badge/Status-In%20Development-yellow" alt="Status"/>
  <img src="https://img.shields.io/badge/Version-1.0.0-blue" alt="Version"/>
  <img src="https://img.shields.io/badge/Platform-ESP8266-red" alt="Platform"/>
  <img src="https://img.shields.io/badge/Architecture-Microservices-purple" alt="Microservices"/>
</div>

## 📋 Descripción

Sistema IoT profesional para monitoreo agrícola con alimentación solar, desarrollado con arquitectura de microservicios. Combina hardware embebido (ESP-01S DHT11) con backend Java Spring Boot, frontend Angular y app móvil Flutter.

## 🎯 Características Principales

- ☀️ **Sistema Solar Autónomo** - Panel solar + batería Li-Ion 18650
- 🌡️ **Monitoreo Ambiental** - Temperatura, humedad y humedad de suelo
- 🔋 **Gestión Inteligente de Energía** - Modos adaptativos según batería
- 📡 **Comunicación MQTT** - Telemetría y comandos en tiempo real
- 🕸️ **Red Mesh** - Comunicación entre múltiples dispositivos ESP
- 📱 **Interfaces Multiplataforma** - Web (Angular) y Móvil (Flutter)
- 🐳 **Infraestructura Docker** - Despliegue de microservicios

## 🛠️ Stack Tecnológico

### Hardware

- **Módulo**: ESP-01S DHT11 v1.0 TB: IOTMCU
- **Panel Solar**: ZW138x82 5V 300mA
- **Controlador**: CN3791 MPPT Solar Charger
- **Batería**: Li-Ion 18650 (2500-3500mAh)
- **Sensor Suelo**: Capacitivo I2C (recomendado)

### Firmware

- **IDE**: PlatformIO
- **Framework**: Arduino + FreeRTOS
- **Lenguaje**: C++ con arrow functions
- **Protocolo**: MQTT

### Backend (Microservicios)

- **Lenguaje**: Java 17
- **Framework**: Spring Boot 3.x
- **Base de Datos**: MySQL 8.0
- **Cache**: Redis
- **Message Broker**: RabbitMQ
- **API Docs**: Swagger/OpenAPI

### Frontend

- **Web**: Angular 16 + TypeScript
- **Mobile**: Flutter 3.x
- **UI**: Angular Material + PrimeNG

### DevOps

- **Contenedores**: Docker + Docker Compose
- **Gateway**: Spring Cloud Gateway
- **Discovery**: Eureka Server
- **Monitoring**: Grafana + Prometheus

## 📊 Diagrama de Arquitectura

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Panel Solar   │───▶│ Controlador MPPT │───▶│ Batería 18650   │
│   ZW138x82      │    │    CN3791        │    │   + Cargador    │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                                        │
                                                        ▼
┌─────────────────┐                              ┌─────────────────┐
│ Sensor Humedad  │◄─────────────────────────────┤ ESP-01S DHT11   │
│    de Suelo     │         I2C/ADC              │ Módulo IOTMCU   │
└─────────────────┘                              └─────────────────┘
                                                        │
                                                    MQTT WiFi
                                                        │
                                                        ▼
┌───────────────────────────────────────────────────────────────────┐
│                    MICROSERVICIOS (Docker)                        │
├───────────────────────────────────────────────────────────────────┤
│  API Gateway │ Eureka │ Device Service │ Sensor Service │ Power  │
└───────────────────────────────────────────────────────────────────┘
                                │
                    ┌───────────┴───────────┐
                    ▼                       ▼
            ┌───────────────┐       ┌─────────────┐
            │   Angular     │       │   Flutter   │
            │   Dashboard   │       │   App       │
            └───────────────┘       └─────────────┘
```

## 🚀 Inicio Rápido

### Requisitos Previos

```bash
# Software necesario
- Java 17+
- Node.js 18+
- Angular CLI 16+
- Flutter 3.x
- PlatformIO IDE
- Docker & Docker Compose
- MySQL 8.0
- Git
```

### Clonar Repositorio

```bash
git clone https://github.com/Shiva0616/smart-agriculture-automation.git
cd smart-agriculture-automation
```

## 📁 Estructura del Proyecto

```
smart-agriculture-ecosystem/
├── 🔧 embedded-firmware/          # Firmware PlatformIO (ESP-01S)
├── ☕ backend-services/           # Microservicios Spring Boot
│   ├── api-gateway/
│   ├── service-discovery/
│   ├── device-management/
│   ├── sensor-data-service/
│   └── power-monitoring/
├── 🌐 web-dashboard/              # Angular Dashboard
├── 📱 mobile-app/                 # Flutter App
├── 🐳 docker/                     # Docker Compose
├── 📊 database/                   # SQL Scripts
└── 📚 docs/                       # Documentación

```

## 🔧 Configuración Inicial del Dispositivo

### Modo AP de Configuración

1. Al primer encendido, el ESP-01S crea un AP WiFi:

   - **SSID**: `ESP-Agriculture-Setup`
   - **IP**: `192.168.4.1`

2. Conectar y abrir navegador en `http://192.168.4.1`

3. Configurar:
   - 📶 **Tipo de conexión**: WiFi / GSM / Mesh
   - 🏷️ **Nombre del dispositivo**
   - 📍 **Ubicación**
   - ⚙️ **Rol**: Standalone / Maestro / Esclavo

## 📡 Comunicación MQTT

### Topics Principales

```
farm/devices/{device_id}/sensors        # Datos de sensores
farm/devices/{device_id}/power          # Métricas de energía
farm/devices/{device_id}/commands       # Comandos al dispositivo
farm/devices/{device_id}/status         # Estado del dispositivo
farm/mesh/discovery                     # Descubrimiento mesh
```

### Ejemplo Payload Sensor

```json
{
  "device_id": "AA:BB:CC:DD:EE:FF",
  "timestamp": "2024-12-17T15:30:00Z",
  "sensors": {
    "temperature": 26.5,
    "humidity": 68.2,
    "soil_moisture": 45.8
  }
}
```

## 🐳 Despliegue con Docker

```bash
# Iniciar todos los servicios
cd docker
docker-compose up -d

# Servicios disponibles:
# - API Gateway: http://localhost:8080
# - Eureka Dashboard: http://localhost:8761
# - Angular App: http://localhost:4200
# - Swagger UI: http://localhost:8080/swagger-ui.html
# - RabbitMQ: http://localhost:15672
```

## 📚 Documentación API

La documentación completa de la API está disponible en Swagger:

```
http://localhost:8080/swagger-ui.html
```

## 🔮 Roadmap de Desarrollo

### ✅ Fase 1: Fundamentos (Actual)

- [x] Estructura de repositorios
- [x] README y documentación base
- [ ] Firmware básico ESP-01S
- [ ] API Gateway + Eureka
- [ ] Servicio de dispositivos

### 🚧 Fase 2: Core Features (Próximo)

- [ ] Gestión de sensores completa
- [ ] Monitoreo de energía
- [ ] Dashboard Angular básico
- [ ] MQTT Broker integrado

### 📅 Fase 3: Avanzado

- [ ] Red Mesh ESP-NOW
- [ ] App móvil Flutter
- [ ] Machine Learning
- [ ] Analytics avanzado

### 🔮 Fase 4: Producción

- [ ] CI/CD Pipeline
- [ ] Kubernetes deployment
- [ ] Monitoreo con Grafana
- [ ] Documentación completa

## 👨‍💻 Autor

**Daniel Alejandro Castañeda Suárez**  
_Ingeniero Electrónico | Full Stack Developer_

- 📧 Email: [danysuarez1606@gmail.com](mailto:danysuarez1606@gmail.com)
- 📱 WhatsApp: +57 301 388 4905
- 💼 LinkedIn: [Daniel Castañeda](https://linkedin.com/in/daniel-castaneda-dev)
- 🐙 GitHub: [@Shiva0616](https://github.com/Shiva0616)

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver archivo [LICENSE](LICENSE) para detalles.

---

<div align="center">
  <p><strong>🌱 Desarrollado con ☀️ energía solar y ❤️ pasión por la tecnología</strong></p>
</div>
