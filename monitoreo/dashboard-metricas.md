# Dashboard de Métricas para Pipeline CI/CD en Entorno SOA

## Introducción
Este documento define la configuración de dashboards en AWS CloudWatch para monitorear el pipeline CI/CD implementado en un entorno SOA. Las métricas seleccionadas están alineadas con las propiedades operativas del reto: latencia de despliegue (<5 minutos), cobertura de pruebas automatizadas (>90%) y tasa de fallos post-implementación (<1%).

## Dashboards Propuestos

### 1. Dashboard de Estado General del Pipeline
**Objetivo:** Proporcionar una visión global del estado del pipeline, incluyendo etapas, tiempos de ejecución y fallos.

**Métricas Incluidas:**
- **Estado de las etapas del pipeline** (AWS CodePipeline):
  - `PipelineExecutionStatus` (Succeeded/Failed/Cancelled/InProgress)
  - `StageExecutionStatus` por etapa (Planificación, Compilación, Pruebas, Despliegue).
- **Tiempo de ejecución por etapa** (AWS CodeBuild):
  - `BuildDuration` (en segundos) para cada etapa.
  - `StartTime` y `EndTime` para calcular latencia.
- **Tasa de fallos** (AWS CloudWatch Metrics):
  - `FailedExecutions` (contador de ejecuciones fallidas).
  - `SuccessRate` (porcentaje de ejecuciones exitosas).

**Visualizaciones:**
- Gráfico de barras apiladas mostrando el estado de las últimas 20 ejecuciones del pipeline.
- Gráfico de líneas con el tiempo de ejecución por etapa (promedio móvil de 7 días).
- Tabla resumen con métricas clave:
  | Métrica                     | Valor Actual | Umbral de Éxito |
  |-----------------------------|---------------|------------------|
  | Latencia de despliegue      | 3.2 min       | <5 min           |
  | Cobertura de pruebas        | 92%           | >90%             |
  | Tasa de fallos post-despliegue | 0.5%        | <1%              |

---

### 2. Dashboard de Calidad y Seguridad
**Objetivo:** Monitorear la calidad del código y la integración de prácticas de seguridad en el pipeline.

**Métricas Incluidas:**
- **Cobertura de pruebas** (AWS CodeBuild + herramientas de testing):
  - `TestCoverage` (porcentaje de líneas de código cubiertas).
  - `FailedTests` (número de pruebas fallidas).
- **Vulnerabilidades de seguridad** (AWS CodeGuru, SonarQube o equivalente):
  - `CriticalVulnerabilities` (número de vulnerabilidades críticas detectadas).
  - `SecurityScanDuration` (tiempo de ejecución del escaneo de seguridad).
- **Cumplimiento de estándares** (OpenAPI/SOAP):
  - `OpenAPIValidationErrors` (número de errores de validación en el contrato OpenAPI).
  - `BIANComplianceScore` (porcentaje de cumplimiento con estándares BIAN).

**Visualizaciones:**
- Gráfico de líneas con la evolución de la cobertura de pruebas en los últimos 30 días.
- Gráfico de barras mostrando el número de vulnerabilidades críticas por tipo (SQL Injection, XSS, etc.).
- Tabla de alertas con umbrales configurados:
  | Métrica                     | Valor Actual | Umbral de Alerta |
  |-----------------------------|---------------|-------------------|
  | Cobertura de pruebas        | 92%           | <90%              |
  | Vulnerabilidades críticas   | 2             | >0                |
  | Errores de validación OpenAPI | 0           | >0                |

---

### 3. Dashboard de Desempeño Operativo
**Objetivo:** Monitorear el desempeño operativo del pipeline y los servicios desplegados.

**Métricas Incluidas:**
- **Latencia de despliegue** (AWS CloudWatch):
  - `DeploymentLatency` (tiempo desde el inicio del despliegue hasta la confirmación de éxito).
- **Disponibilidad de servicios** (AWS CloudWatch + AWS X-Ray):
  - `ServiceAvailability` (porcentaje de tiempo en que el servicio está disponible).
  - `ErrorRate` (porcentaje de solicitudes fallidas).
- **Uso de recursos** (AWS CloudWatch):
  - `CPUUtilization` (porcentaje de uso de CPU en instancias de despliegue).
  - `MemoryUtilization` (porcentaje de uso de memoria).
- **Tiempo de respuesta de servicios** (AWS X-Ray):
  - `AverageResponseTime` (tiempo promedio de respuesta de los endpoints SOA).

**Visualizaciones:**
- Gráfico de líneas con la latencia de despliegue en los últimos 14 días (con umbral de 5 minutos).
- Gráfico de líneas con la disponibilidad de servicios (objetivo: 99.95%).
- Tabla resumen de métricas operativas:
  | Métrica                     | Valor Actual | Umbral de Éxito |
  |-----------------------------|---------------|------------------|
  | Disponibilidad del servicio | 99.98%        | >99.95%          |
  | Tiempo de respuesta promedio | 120 ms      | <200 ms          |
  | Uso de CPU                  | 45%           | <70%             |

---

## Configuración Técnica

### Fuentes de Datos
- **AWS CodePipeline:** Métricas de estado y ejecución del pipeline.
- **AWS CodeBuild:** Métricas de tiempo de ejecución y resultados de pruebas.
- **AWS CloudWatch:** Métricas personalizadas para latencia, disponibilidad y uso de recursos.
- **AWS X-Ray:** Trazas de rendimiento de los servicios SOA.
- **Herramientas de seguridad (SonarQube/CodeGuru):** Métricas de vulnerabilidades y calidad de código.

### Pasos para Configurar el Dashboard en AWS CloudWatch
1. **Crear un nuevo dashboard** en AWS CloudWatch con el nombre `SOA-CI-CD-Pipeline-Metrics`.
2. **Agregar widgets** para cada métrica utilizando las fuentes de datos mencionadas:
   - Usar el tipo de widget adecuado (gráfico de líneas, barras, tabla, etc.).
   - Configurar los umbrales de alerta para métricas críticas (ej: latencia >5 minutos, cobertura <90%).
3. **Configurar alarmas** para métricas clave:
   - Alarma para `FailedExecutions` (envía notificación a SNS cuando se supera el umbral).
   - Alarma para `CriticalVulnerabilities` (envía notificación inmediata al equipo de seguridad).
   - Alarma para `DeploymentLatency` (notifica si la latencia supera los 5 minutos).
4. **Compartir el dashboard** con los equipos de desarrollo, operaciones y seguridad.

### Ejemplo de Configuración de Alarma (AWS CLI)
```yaml
# Configuración de alarma para latencia de despliegue
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  DeploymentLatencyAlarm:
    Type: AWS::CloudWatch::Alarm
    Properties:
      AlarmName: "SOA-Pipeline-DeploymentLatency-High"
      ComparisonOperator: GreaterThanThreshold
      EvaluationPeriods: 1
      MetricName: "DeploymentLatency"
      Namespace: "SOA/CICD"
      Period: 300
      Statistic: "Average"
      Threshold: 300  # 5 minutos en segundos
      AlarmDescription: "Alarma activada cuando la latencia de despliegue supera los 5 minutos"
      AlarmActions:
        - !Ref NotificationTopic
      Dimensions:
        - Name: "PipelineName"
          Value: "SOA-Service-Pipeline"
```

---

## Métricas Adicionales Recomendadas
- **Tiempo de resolución de incidentes:** Tiempo promedio desde la detección de un fallo hasta su resolución.
- **Frecuencia de despliegues:** Número de despliegues exitosos por semana.
- **Feedback del equipo:** Métricas cualitativas recopiladas mediante encuestas o retrospectivas (ej: satisfacción del equipo con el proceso de despliegue).

## Acciones Automáticas Basadas en Métricas
- **Fallo en pruebas:** Detener el pipeline y notificar al equipo de desarrollo.
- **Vulnerabilidades críticas:** Bloquear el despliegue hasta que se resuelvan las vulnerabilidades.
- **Latencia alta:** Notificar al equipo de operaciones para investigar cuellos de botella.

---

## Responsables
| Equipo               | Responsabilidad                                                                 |
|----------------------|---------------------------------------------------------------------------------|
| Desarrollo           | Monitorear métricas de calidad (cobertura, pruebas) y corregir fallos.         |
| Operaciones          | Monitorear métricas operativas (latencia, disponibilidad) y optimizar recursos. |
| Seguridad            | Monitorear métricas de seguridad y resolver vulnerabilidades.                  |
| DevOps               | Mantener y mejorar la configuración de los dashboards y alarmas.               |