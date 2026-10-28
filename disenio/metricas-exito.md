# Métricas de Éxito para el Pipeline de CI/CD

Este documento define las métricas de éxito para evaluar el desempeño del pipeline de CI/CD en el contexto de integración SOA. Las métricas están alineadas con las propiedades operativas descritas en el reto: latencia de despliegue (<5 minutos), cobertura de pruebas automatizadas (>90%) y tasa de fallos post-implementación (<1%).

## 1. Métricas de Eficiencia del Pipeline

### 1.1 Tiempo de Ciclo (Cycle Time)
- **Definición**: Tiempo total desde que se realiza un commit hasta que el cambio está desplegado en producción.
- **Objetivo**: < 30 minutos.
- **Fórmula**: `Tiempo de despliegue - Tiempo de commit`.
- **Herramienta**: AWS CloudWatch (métricas de CodePipeline).
- **Frecuencia de medición**: Por commit.
- **Ejemplo**:
  ```
  Commit a las 10:00 AM → Despliegue completado a las 10:25 AM → Tiempo de ciclo = 25 minutos.
  ```

### 1.2 Tiempo de Despliegue (Deployment Time)
- **Definición**: Tiempo que tarda el pipeline en ejecutar la etapa de despliegue.
- **Objetivo**: < 5 minutos.
- **Fórmula**: `Tiempo de finalización de despliegue - Tiempo de inicio de despliegue`.
- **Herramienta**: AWS CloudWatch (métricas de CodeBuild para la etapa de despliegue).
- **Frecuencia de medición**: Por despliegue.
- **Detalle**:
  - Incluye la ejecución de CloudFormation, despliegue de servicios y pruebas de smoke.
  - Excluye tiempos de espera por aprobación manual (si aplica).

### 1.3 Frecuencia de Despliegue (Deployment Frequency)
- **Definición**: Número de despliegues exitosos a producción por día.
- **Objetivo**: ≥ 3 despliegues/día.
- **Fórmula**: `Número de despliegues exitosos / Número de días`.
- **Herramienta**: AWS CloudWatch (métricas de CodePipeline).
- **Frecuencia de medición**: Semanal.

### 1.4 Tasa de Éxito del Pipeline (Pipeline Success Rate)
- **Definición**: Porcentaje de ejecuciones del pipeline que completan todas las etapas sin errores.
- **Objetivo**: > 95%.
- **Fórmula**: `(Número de ejecuciones exitosas / Número total de ejecuciones) * 100`.
- **Herramienta**: AWS CloudWatch (métricas de CodePipeline).
- **Frecuencia de medición**: Diaria.
- **Ejemplo**:
  ```
  100 ejecuciones en una semana → 98 exitosas → Tasa de éxito = 98%.
  ```

---

## 2. Métricas de Calidad del Código

### 2.1 Cobertura de Pruebas (Test Coverage)
- **Definición**: Porcentaje de código cubierto por pruebas unitarias e de integración.
- **Objetivo**: > 90%.
- **Fórmula**: `(Líneas de código cubiertas / Líneas totales de código) * 100`.
- **Herramienta**: JaCoCo (para Java) / coverage.py (para Python) / Jest (para JavaScript).
- **Frecuencia de medición**: Por build.
- **Detalle**:
  - Se mide en las etapas de **Build** y **IntegrationTests** del pipeline.
  - Se rechaza el despliegue si la cobertura es < 90%.

### 2.2 Número de Fallos en Pruebas (Test Failures)
- **Definición**: Número de pruebas unitarias o de integración que fallan por build.
- **Objetivo**: 0 fallos.
- **Fórmula**: `Número de pruebas fallidas`.
- **Herramienta**: JUnit / Pytest / Newman.
- **Frecuencia de medición**: Por build.
- **Ejemplo**:
  ```
  Ejecución de 50 pruebas → 2 fallidas → Número de fallos = 2.
  ```

### 2.3 Validación de Contrato OpenAPI
- **Definición**: Porcentaje de endpoints definidos en `openapi.yaml` que pasan la validación de contrato.
- **Objetivo**: 100%.
- **Fórmula**: `(Endpoints validados correctamente / Total de endpoints) * 100`.
- **Herramienta**: Redocly CLI / Newman.
- **Frecuencia de medición**: Por build.
- **Detalle**:
  - Se valida en la etapa de **Build** del pipeline.
  - Se rechaza el despliegue si algún endpoint no cumple con el contrato.

### 2.4 Densidad de Defectos (Defect Density)
- **Definición**: Número de defectos identificados por cada 1000 líneas de código.
- **Objetivo**: < 1 defecto / 1000 líneas.
- **Fórmula**: `(Número de defectos / Líneas totales de código) * 1000`.
- **Herramienta**: SonarQube / Bandit.
- **Frecuencia de medición**: Semanal.

---

## 3. Métricas de Seguridad

### 3.1 Vulnerabilidades Críticas (Critical Vulnerabilities)
- **Definición**: Número de vulnerabilidades críticas identificadas en el código o dependencias.
- **Objetivo**: 0 vulnerabilidades críticas.
- **Fórmula**: `Número de vulnerabilidades críticas`.
- **Herramienta**: Bandit (SAST) / Snyk (dependencias) / OWASP ZAP (DAST).
- **Frecuencia de medición**: Por build.
- **Detalle**:
  - Se mide en la etapa de **SecurityScan** del pipeline.
  - Se rechaza el despliegue si se detectan vulnerabilidades críticas.

### 3.2 Tiempo de Mitigación de Vulnerabilidades (Vulnerability Mitigation Time)
- **Definición**: Tiempo promedio desde que se identifica una vulnerabilidad hasta que se mitiga.
- **Objetivo**: < 2 días.
- **Fórmula**: `Tiempo de mitigación - Tiempo de identificación`.
- **Herramienta**: Jira / AWS Security Hub.
- **Frecuencia de medición**: Mensual.

### 3.3 Cumplimiento de Estándares de Seguridad (Security Compliance)
- **Definición**: Porcentaje de controles de seguridad que cumplen con los estándares definidos (ISO 27001, GDPR, etc.).
- **Objetivo**: 100%.
- **Fórmula**: `(Controles cumplidos / Total de controles) * 100`.
- **Herramienta**: AWS Config / AWS Security Hub.
- **Frecuencia de medición**: Trimestral.

---

## 4. Métricas de Estabilidad Operativa

### 4.1 Tasa de Fallos Post-Despliegue (Change Failure Rate)
- **Definición**: Porcentaje de despliegues que resultan en fallos en producción.
- **Objetivo**: < 1%.
- **Fórmula**: `(Número de despliegues fallidos / Número total de despliegues) * 100`.
- **Herramienta**: AWS CloudWatch / PagerDuty.
- **Frecuencia de medición**: Mensual.
- **Ejemplo**:
  ```
  100 despliegues en un mes → 1 fallido → Tasa de fallos = 1%.
  ```

### 4.2 Tiempo Medio de Recuperación (Mean Time to Recovery - MTTR)
- **Definición**: Tiempo promedio para recuperar un servicio después de un fallo en producción.
- **Objetivo**: < 30 minutos.
- **Fórmula**: `Tiempo total de recuperación / Número de incidentes`.
- **Herramienta**: AWS CloudWatch / PagerDuty.
- **Frecuencia de medición**: Mensual.

### 4.3 Disponibilidad del Servicio (Service Availability)
- **Definición**: Porcentaje de tiempo en el que el servicio está disponible y funcionando correctamente.
- **Objetivo**: > 99.9%.
- **Fórmula**: `(Tiempo total de disponibilidad / Tiempo total) * 100`.
- **Herramienta**: AWS CloudWatch / Prometheus.
- **Frecuencia de medición**: Mensual.

### 4.4 Latencia de Respuesta (Response Latency)
- **Definición**: Tiempo promedio de respuesta de los servicios SOA.
- **Objetivo**: < 500ms.
- **Fórmula**: `Tiempo total de respuesta / Número de solicitudes`.
- **Herramienta**: AWS CloudWatch / New Relic.
- **Frecuencia de medición**: Diaria.

---

## 5. Métricas de Colaboración y Cultura DevOps

### 5.1 Número de Incidentes por Falta de Comunicación (Communication Issues)
- **Definición**: Número de incidentes causados por falta de comunicación entre equipos.
- **Objetivo**: 0 incidentes.
- **Fórmula**: `Número de incidentes atribuidos a falta de comunicación`.
- **Herramienta**: Jira / Postmortems.
- **Frecuencia de medición**: Mensual.

### 5.2 Participación en Revisiones de Código (Code Review Participation)
- **Definición**: Porcentaje de PRs que reciben al menos una revisión de otro equipo (Dev, Ops o Sec).
- **Objetivo**: 100%.
- **Fórmula**: `(PRs revisados por otro equipo / Total de PRs) * 100`.
- **Herramienta**: GitHub / GitLab / Bitbucket.
- **Frecuencia de medición**: Semanal.

### 5.3 Número de Capacitaciones Realizadas (Training Sessions)
- **Definición**: Número de capacitaciones realizadas para alinear a los equipos en prácticas DevOps.
- **Objetivo**: ≥ 4 capacitaciones/año.
- **Fórmula**: `Número de capacitaciones`.
- **Herramienta**: LMS / Confluence.
- **Frecuencia de medición**: Anual.

### 5.4 Satisfacción del Equipo (Team Satisfaction)
- **Definición**: Nivel de satisfacción de los equipos con la colaboración DevOps (escala del 1 al 10).
- **Objetivo**: ≥ 8/10.
- **Fórmula**: `Promedio de respuestas en encuestas de satisfacción`.
- **Herramienta**: Encuestas anónimas (Google Forms, Typeform).
- **Frecuencia de medición**: Trimestral.

---

## 6. Dashboard de Métricas

Para visualizar estas métricas, se configura un dashboard en **AWS CloudWatch** y **Grafana** con los siguientes paneles:

### 6.1 Panel de Eficiencia
- Tiempo de ciclo.
- Tiempo de despliegue.
- Frecuencia de despliegue.
- Tasa de éxito del pipeline.

### 6.2 Panel de Calidad
- Cobertura de pruebas.
- Número de fallos en pruebas.
- Validación de contrato OpenAPI.
- Densidad de defectos.

### 6.3 Panel de Seguridad
- Vulnerabilidades críticas.
- Tiempo de mitigación de vulnerabilidades.
- Cumplimiento de estándares de seguridad.

### 6.4 Panel de Estabilidad
- Tasa de fallos post-despliegue.
- Tiempo medio de recuperación (MTTR).
- Disponibilidad del servicio.
- Latencia de respuesta.

### 6.5 Panel de Colaboración
- Número de incidentes por falta de comunicación.
- Participación en revisiones de código.
- Número de capacitaciones realizadas.
- Satisfacción del equipo.

---

## 7. Umbrales de Alerta

Se configuran alertas en **AWS CloudWatch** y **PagerDuty** para notificar cuando las métricas no cumplen con los objetivos:

| Métrica                          | Umbral de Alerta | Frecuencia de Notificación |
|---------------------------------|------------------|----------------------------|
| Tiempo de ciclo                 | > 30 minutos     | Por ejecución              |
| Tiempo de despliegue            | > 5 minutos      | Por despliegue             |
| Tasa de éxito del pipeline      | < 95%            | Diaria                     |
| Cobertura de pruebas            | < 90%            | Por build                  |
| Vulnerabilidades críticas       | > 0              | Por build                  |
| Tasa de fallos post-despliegue  | > 1%             | Mensual                    |
| Tiempo medio de recuperación    | > 30 minutos     | Mensual                    |
| Disponibilidad del servicio     | < 99.9%          | Mensual                    |
| Latencia de respuesta           | > 500ms          | Diaria                     |

---

## 8. Plan de Mejora Continua

Para asegurar que las métricas se mantengan dentro de los objetivos, se implementa un **plan de mejora continua** con las siguientes acciones:

- **Reuniones de revisión de métricas**: Semanalmente, los equipos revisan las métricas y proponen acciones correctivas.
- **Retrospectivas post-incidentes**: Después de cada incidente, se realiza una retrospectiva para identificar causas raíz y definir acciones de mejora.
- **Actualización de objetivos**: Trimestralmente, se revisan los objetivos de las métricas para alinearlos con las necesidades del negocio.
- **Capacitación continua**: Se programan capacitaciones periódicas para mantener a los equipos actualizados en prácticas DevOps.
- **Automatización de métricas**: Se automatiza la recolección y visualización de métricas para reducir el esfuerzo manual.

---

## 9. Ejemplo de Métricas en un Sprint

A continuación, se presenta un ejemplo de métricas registradas durante un sprint de 2 semanas:

| Métrica                          | Valor Registrado | Objetivo | Estado       |
|---------------------------------|------------------|----------|--------------|
| Tiempo de ciclo                 | 28 minutos       | < 30 min | ✅ Cumple     |
| Tiempo de despliegue            | 4 minutos        | < 5 min  | ✅ Cumple     |
| Frecuencia de despliegue        | 5/día            | ≥ 3/día  | ✅ Cumple     |
| Tasa de éxito del pipeline       | 97%              | > 95%    | ✅ Cumple     |
| Cobertura de pruebas            | 92%              | > 90%    | ✅ Cumple     |
| Vulnerabilidades críticas       | 0                | 0        | ✅ Cumple     |
| Tasa de fallos post-despliegue  | 0.5%             | < 1%     | ⚠️ Alerta     |
| Tiempo medio de recuperación     | 25 minutos       | < 30 min | ✅ Cumple     |
| Disponibilidad del servicio     | 99.95%           | > 99.9%  | ✅ Cumple     |
| Latencia de respuesta           | 450ms            | < 500ms  | ✅ Cumple     |
| Participación en revisiones     | 100%             | 100%     | ✅ Cumple     |

**Acciones correctivas propuestas:**
- Investigar la causa de la tasa de fallos post-despliegue (0.5%) y definir acciones para reducirla.
- Realizar una capacitación en buenas prácticas de despliegue para el equipo de Operaciones.