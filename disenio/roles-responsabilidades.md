# Roles y Responsabilidades en el Pipeline de CI/CD

Este documento define los roles y responsabilidades de cada equipo involucrado en el pipeline de CI/CD para la integración SOA, asegurando una colaboración efectiva entre desarrollo, operaciones y seguridad.

## 1. Equipo de Desarrollo (Dev)

### Responsabilidades:
- **Desarrollo de servicios SOA**: Implementación de los servicios siguiendo los contratos definidos en `openapi.yaml`.
- **Pruebas unitarias**: Desarrollo y mantenimiento de pruebas unitarias con cobertura mínima del 90%.
- **Validación de contratos**: Asegurar que el código cumple con el contrato OpenAPI definido (validación con Redocly CLI).
- **Manejo de dependencias**: Gestión de dependencias del proyecto, incluyendo actualizaciones y análisis de vulnerabilidades.
- **Documentación técnica**: Mantenimiento de documentación técnica actualizada (README, diagramas de arquitectura, decisiones de diseño).

### Roles específicos:
- **Desarrollador Backend**: Implementación de servicios RESTful, manejo de DTOs y lógica de negocio.
- **Desarrollador Frontend (si aplica)**: Implementación de clientes que consumen los servicios SOA.
- **Tech Lead**: Revisión de código, aprobación de PRs y alineación con estándares de arquitectura.

### Herramientas:
- IDE (IntelliJ, VSCode)
- Git
- Maven/Gradle
- JUnit/Pytest
- Redocly CLI
- Newman (para pruebas de contrato)

### Métricas de éxito:
- Cobertura de pruebas unitarias > 90%.
- Tiempo promedio de implementación de features < 3 días.
- Número de incidencias post-despliegue relacionadas con código < 1 por sprint.

---

## 2. Equipo de Operaciones (Ops)

### Responsabilidades:
- **Gestión de infraestructura**: Configuración y mantenimiento de la infraestructura en AWS (CodePipeline, CodeBuild, CloudFormation, S3, ECR).
- **Despliegue de servicios**: Ejecución de despliegues en entornos de staging y producción.
- **Monitoreo y logging**: Configuración de CloudWatch para monitoreo de logs, métricas y alertas.
- **Escalabilidad y disponibilidad**: Asegurar que los servicios cumplen con los SLAs de disponibilidad (> 99.9%) y latencia (< 500ms).
- **Gestión de artefactos**: Mantenimiento del bucket S3 para almacenamiento de artefactos y reportes.

### Roles específicos:
- **DevOps Engineer**: Configuración y mantenimiento del pipeline de CI/CD.
- **Cloud Engineer**: Gestión de recursos en AWS (VPC, subnets, IAM, etc.).
- **Site Reliability Engineer (SRE)**: Monitoreo de métricas operativas y gestión de incidentes.

### Herramientas:
- AWS Console/CLI
- Terraform/CloudFormation
- Docker
- Kubernetes (si aplica)
- Prometheus/Grafana
- CloudWatch

### Métricas de éxito:
- Tiempo de despliegue < 5 minutos.
- Disponibilidad de servicios > 99.9%.
- Tiempo de resolución de incidentes < 30 minutos.

---

## 3. Equipo de Seguridad (Sec)

### Responsabilidades:
- **Análisis de seguridad**: Ejecución de escaneos estáticos (SAST) y dinámicos (DAST) en el código y los servicios.
- **Gestión de vulnerabilidades**: Identificación y mitigación de vulnerabilidades en dependencias y código.
- **Configuración de IAM**: Definición de políticas de IAM con mínimo privilegio para roles de CodePipeline y CodeBuild.
- **Cumplimiento normativo**: Asegurar que el pipeline cumple con estándares de seguridad (ISO 27001, GDPR, etc.).
- **Revisión de código seguro**: Participación en revisiones de código para identificar riesgos de seguridad.

### Roles específicos:
- **Security Engineer**: Configuración de herramientas de seguridad (Bandit, Snyk, OWASP ZAP).
- **Compliance Officer**: Verificación de cumplimiento normativo.
- **Incident Responder**: Gestión de incidentes de seguridad.

### Herramientas:
- Bandit (SAST)
- Snyk (análisis de dependencias)
- OWASP ZAP (DAST)
- AWS IAM
- CloudTrail

### Métricas de éxito:
- Número de vulnerabilidades críticas identificadas y mitigadas = 0.
- Tiempo promedio de mitigación de vulnerabilidades < 2 días.
- Porcentaje de cumplimiento normativo = 100%.

---

## 4. Responsabilidades Compartidas

### Entre Desarrollo y Operaciones:
- **Definición de entornos**: Colaboración en la definición de entornos de staging y producción.
- **Pruebas de integración**: Desarrollo conjunto de pruebas de integración.
- **Despliegue canary**: Implementación de despliegues canary para validación en producción.

### Entre Desarrollo y Seguridad:
- **Shift-Left Security**: Integración de prácticas de seguridad desde las primeras etapas del desarrollo.
- **Revisión de dependencias**: Análisis conjunto de dependencias del proyecto.
- **Pruebas de penetración**: Participación en pruebas de penetración de servicios.

### Entre Operaciones y Seguridad:
- **Configuración de infraestructura segura**: Definición de políticas de seguridad para recursos en AWS.
- **Monitoreo de seguridad**: Configuración de alertas para eventos de seguridad.
- **Respuesta a incidentes**: Colaboración en la gestión de incidentes de seguridad.

---

## 5. Matriz RACI

A continuación se presenta una matriz RACI para las etapas clave del pipeline:

| Etapa                | Dev       | Ops       | Sec       |
|----------------------|-----------|-----------|-----------|
| Desarrollo de código | R/A       | I         | C         |
| Pruebas unitarias    | R/A       | I         | C         |
| Validación OpenAPI   | R/A       | I         | C         |
| Análisis de seguridad| C         | I         | R/A       |
| Pruebas de integración| R/A      | C         | I         |
| Despliegue           | C         | R/A       | I         |
| Monitoreo            | C         | R/A       | C         |
| Gestión de incidentes | R         | R/A       | R         |

**Leyenda:**
- R: Responsible (Responsable)
- A: Accountable (Aprobador)
- C: Consulted (Consultado)
- I: Informed (Informado)

---

## 6. Proceso de Escalamiento

En caso de bloqueos o incidencias en el pipeline, se sigue el siguiente flujo de escalamiento:

1. **Nivel 1 (Equipo)**: El miembro del equipo que identifica el problema intenta resolverlo con sus pares.
2. **Nivel 2 (Tech Lead/DevOps Lead)**: Si el problema persiste, se escala al Tech Lead o DevOps Lead del equipo.
3. **Nivel 3 (Gerente de Área)**: Si el problema no puede resolverse, se escala al gerente del área (Desarrollo, Operaciones o Seguridad).
4. **Nivel 4 (Comité de DevOps)**: Para problemas transversales que afectan a múltiples equipos, se convoca al comité de DevOps.

**Tiempos de respuesta:**
- Nivel 1: 1 hora.
- Nivel 2: 4 horas.
- Nivel 3: 12 horas.
- Nivel 4: 24 horas.

---

## 7. Capacitación y Habilitación

Para asegurar que todos los equipos estén alineados con las prácticas DevOps, se definen las siguientes capacitaciones:

- **Desarrollo**:
  - Talleres de Shift-Left Security.
  - Capacitación en herramientas de seguridad (Bandit, Snyk).
  - Buenas prácticas de desarrollo seguro.

- **Operaciones**:
  - Talleres de infraestructura como código (IaC).
  - Capacitación en AWS DevOps Tools (CodePipeline, CodeBuild, CloudFormation).
  - Gestión de incidentes y monitoreo.

- **Seguridad**:
  - Talleres de integración continua de seguridad.
  - Capacitación en herramientas de SAST/DAST.
  - Buenas prácticas de configuración segura en AWS.

**Frecuencia:**
- Talleres trimestrales.
- Sesiones de habilitación post-incidentes.