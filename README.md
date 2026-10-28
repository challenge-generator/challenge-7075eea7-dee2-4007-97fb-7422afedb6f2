# Implementación de prácticas DevOps en un entorno SOA

En un entorno de integración de servicios orientados a arquitectura (SOA), la implementación de prácticas DevOps es crucial para asegurar la comunicación y colaboración efectiva entre equipos de desarrollo, operaciones y seguridad. El objetivo es promover una cultura DevOps que integre de manera fluida el ciclo de vida del desarrollo de software (SDLC), desde la planificación hasta la implementación y mantenimiento, con un enfoque en la seguridad y la calidad del software. Los actores involucrados incluyen el equipo de desarrollo de servicios, el equipo de operaciones de infraestructura AWS y el equipo de seguridad. Las propiedades operativas incluyen la latencia de despliegue de servicios (<5 minutos), la cobertura de pruebas automatizadas (>90%) y la tasa de fallos post-implementación (<1%). El problema a abordar es la falta de integración y comunicación entre estos equipos, lo que resulta en retrasos y fallos en el despliegue de servicios.

## Informacion General

| Campo | Valor |
|-------|-------|
| **Tema** | Participación activa en pro de la cultura DevOps |
| **Nivel** | senior-l2 |
| **Tipo** | mixed |
| **Tiempo estimado** | 2 semanas |

## Fases del Reto

### Fase 0: Configuración del Proyecto

**Objetivo:** Obtener el proyecto base funcional enviando el Código Base a un asistente de IA, que lo analizará, corregirá errores y generará un ZIP listo para usar.

**Tiempo estimado:** 15-30 minutos

**Instrucciones:**

- Asegúrate de tener instalado para ejecutar el proyecto: Un IDE o editor de código.
- Copia todo el contenido del campo **Código Base** de este reto — incluyendo el texto de instrucciones que aparece al inicio.
- Abre un asistente de IA (Claude en claude.ai, ChatGPT o Gemini — se recomienda Claude), pega el contenido copiado en el chat y envíalo.
- El asistente analizará los archivos, corregirá errores y generará un archivo ZIP descargable. Descárgalo y extráelo en la carpeta donde quieras trabajar.
- Verifica que el proyecto arranca sin errores.

**Entregable:** El proyecto compila/arranca sin errores.

<details>
<summary>Pistas de conocimiento</summary>

- Copia el Código Base completo incluyendo el texto de instrucciones al inicio — esas instrucciones le indican al asistente exactamente qué hacer con los archivos.
- Si el asistente no genera el ZIP automáticamente al terminar el análisis, escríbele: "genera el ZIP ahora".
- Si el proyecto tiene errores al arrancar, comparte el mensaje de error con el mismo asistente para que lo corrija.

</details>

### Fase 1: Evaluación del entorno actual

**Objetivo:** Identificar las brechas en la comunicación y colaboración entre equipos.

**Tiempo estimado:** 3 días

**Instrucciones:**

- Analiza el flujo actual de trabajo entre equipos de desarrollo, operaciones y seguridad.
- Identifica las áreas de mejora en la comunicación y colaboración.
- Documenta las brechas encontradas y las posibles soluciones.

**Entregable:** Documento de evaluación del entorno actual con identificación de brechas y posibles soluciones.

<details>
<summary>Pistas de conocimiento</summary>

- Considera el uso de herramientas de comunicación y colaboración.
- Evalúa la madurez actual de las prácticas DevOps en el equipo.

</details>

### Fase 2: Diseño de un pipeline de CI/CD

**Objetivo:** Diseñar un pipeline de CI/CD que integre las prácticas de desarrollo, operaciones y seguridad.

**Tiempo estimado:** 5 días

**Instrucciones:**

- Diseña un pipeline de CI/CD que incluya etapas de compilación, prueba, despliegue y monitoreo.
- Define los roles y responsabilidades de cada equipo en el pipeline.
- Establece métricas de éxito para el pipeline.

**Entregable:** Diagrama del pipeline de CI/CD con roles y responsabilidades definidos y métricas de éxito establecidas.

<details>
<summary>Pistas de conocimiento</summary>

- Considera la automatización de pruebas y despliegues.
- Evalúa la integración de herramientas de seguridad en el pipeline.

</details>

### Fase 3: Implementación y monitoreo del pipeline

**Objetivo:** Implementar el pipeline de CI/CD y establecer un plan de monitoreo y mejora continua.

**Tiempo estimado:** 6 días

**Instrucciones:**

- Implementa el pipeline de CI/CD diseñado en la fase anterior.
- Establece un plan de monitoreo para el pipeline, incluyendo métricas de rendimiento y calidad.
- Define un plan de mejora continua basado en las métricas y feedback del equipo.

**Entregable:** Pipeline de CI/CD implementado y funcionando, con plan de monitoreo y mejora continua documentado.

<details>
<summary>Pistas de conocimiento</summary>

- Considera el uso de dashboards para visualizar las métricas del pipeline.
- Evalúa la retroalimentación del equipo para identificar áreas de mejora.

</details>

## Dimensiones Evaluadas

- **queEs**: ¿Qué es un pipeline de CI/CD y por qué es importante en un entorno SOA?
- **paraQueSirve**: ¿Para qué sirve la integración de prácticas DevOps en un entorno SOA?
- **comoSeUsa**: ¿Cómo se puede utilizar un pipeline de CI/CD para mejorar la comunicación y colaboración entre equipos?
- **erroresComunes**: ¿Cuáles son los errores comunes al implementar prácticas DevOps en un entorno SOA?
- **queDecisionesImplica**: ¿Qué decisiones implica el diseño y la implementación de un pipeline de CI/CD en un entorno SOA?

## Criterios de Evaluacion

- Identificación de brechas en la comunicación y colaboración entre equipos.
- Diseño de un pipeline de CI/CD que integre prácticas de desarrollo, operaciones y seguridad.
- Implementación y monitoreo efectivo del pipeline de CI/CD.
- Establecimiento de un plan de mejora continua basado en métricas y feedback.

## Como trabajar con un asistente de IA

Hay dos caminos, elegi uno:

- **AGENTS.md** (recomendado) — instrucciones nativas del repo. Abri esta carpeta con tu agente local (Claude Code, Cursor, Codex, Copilot, Gemini) y las carga solo. Sabe que archivos faltan y con que comando se verifica, y completa el scaffold escribiendo en disco.
- **PROMPT_MEJORA.md** — para copiar y pegar en un chat (claude.ai, ChatGPT). Devuelve un ZIP con el proyecto. Sirve si no tenes un agente en el IDE.

Ninguno de los dos resuelve las fases del reto: eso es tu trabajo.

## Verificacion

El proyecto esta listo para trabajar cuando este comando corre sin errores:

```bash
npx --yes @redocly/cli lint openapi.yaml
```

---

*Reto generado automaticamente por Challenge Generator - Pragma*
