# MsApiGateway

API Gateway (YARP) con Service Discovery vía Consul — parte del proyecto **NurTricenter** (Diplomado de Arquitectura de Microservicios).

Enruta las peticiones externas hacia los microservicios `MsPacientesEvaluacion.Api` y `MsProduccionAlimentos.Api` por prefijo de ruta (`/pacientes/**`, `/produccion/**`), resolviendo los destinos reales en tiempo real contra Consul — sin direcciones hardcodeadas. Un `BackgroundService` consulta a Consul cada N segundos y actualiza la configuración de YARP en caliente.

## Tecnología

.NET 8, ASP.NET Core (Minimal Hosting), Yarp.ReverseProxy, Consul (cliente .NET).

## Cómo correrlo con Docker

```
docker build -t nurtricenter-gateway .
docker run -p 5000:8080 nurtricenter-gateway
```

Requiere la variable de configuración `ServiceDiscovery:ConsulAddress` apuntando a una instancia de Consul accesible (ver `appsettings.json`).

## Rutas

| Ruta de entrada | Destino |
|---|---|
| `/pacientes/**` | `MsPacientesEvaluacion.Api` (resuelto vía Consul) |
| `/produccion/**` | `MsProduccionAlimentos.Api` (resuelto vía Consul) |
