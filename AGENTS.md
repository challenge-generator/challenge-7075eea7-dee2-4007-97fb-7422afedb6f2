# AGENTS.md

Instrucciones para el agente de IA que abra este repositorio (Claude Code, Cursor, Codex, Copilot, Gemini). Se cargan solas: no hay que pegar nada en ningun chat.

## Que es este repositorio

Es el codigo base de un reto de aprendizaje de Pragma: **Implementación de prácticas DevOps en un entorno SOA**.

| | |
|---|---|
| Tema | Participación activa en pro de la cultura DevOps |
| Nivel | senior-l2 |
| Chapter | Integración — Analista |
| Especialidad | SOA |
| Stack | YAML / CI/CD Pipeline con AWS DevOps Tools |
| Patron arquitectonico | Pipeline de CI/CD con etapas orquestadas (Planificación, Compilación, Pruebas, Despliegue, Monitoreo) y patrones de seguridad integrados (Shift-Left Security) |
| Tiempo estimado | 2 semanas |

## Receta del stack

Esqueleto obligatorio:

- `openapi.yaml`
- `proceso.bpmn.md`
- `mapeo-de-datos.csv`

Dependencias:

- AWS CodePipeline n/a
- AWS CodeBuild n/a
- AWS CloudFormation n/a
- AWS CloudWatch n/a
- Redocly CLI 1.0.0
- BPMN 2.0 n/a
- OpenAPI 3.1 3.1.0
- AWS IAM n/a

## Tu tarea

Dejar este conjunto de artefactos en estado **verificable**: que el comando de verificacion corra sin errores. Escribi los archivos en disco, en este repositorio. No generes ZIPs ni archivos adjuntos.

En orden:

1. Corre `npx --yes @redocly/cli lint openapi.yaml` y mira que falla.
2. Completa lo que falte de la lista de abajo: manifiesto de dependencias, punto de entrada, capa de interfaz y las capas del patron declarado.
3. Arregla SOLO los errores que impiden compilar o arrancar.
4. Volve a correr `npx --yes @redocly/cli lint openapi.yaml` hasta que pase.
5. Pará ahí.

## Regla dura: las fases son trabajo del humano

**PROHIBIDO implementar los entregables de las fases.** El valor del reto esta en que la persona los resuelva. Tu trabajo es que tenga un proyecto que arranca; el hueco pedagogico se queda como esta.

No resuelvas nada de esto:

- **Fase 1 — Evaluación del entorno actual**: Documento de evaluación del entorno actual con identificación de brechas y posibles soluciones.
- **Fase 2 — Diseño de un pipeline de CI/CD**: Diagrama del pipeline de CI/CD con roles y responsabilidades definidos y métricas de éxito establecidas.
- **Fase 3 — Implementación y monitoreo del pipeline**: Pipeline de CI/CD implementado y funcionando, con plan de monitoreo y mejora continua documentado.

Distincion operativa:

- **Arreglar** (si): import faltante, tipo que no existe, dependencia sin declarar, error de sintaxis, archivo referenciado que no existe.
- **No tocar** (no): logica de negocio incompleta, validaciones ausentes, secretos hardcodeados, APIs deprecadas que funcionan, concurrencia insegura, patrones mejorables. Eso es lo que la persona tiene que encontrar.

## Superficie de practica (NO completes)

Estos archivos SON el ejercicio de la persona. No los implementes; deja stubs. No toques la logica que el reto pide completar.

- [ ] `implementacion/security-config.yml` — El topic pide autenticacion/seguridad: este archivo es el ejercicio.
- [ ] `openapi.yaml` — El topic pide el contrato de API: openapi.yaml es el ejercicio.

## Lo que falta y tenes que completar

No se detectaron huecos: estan los archivos declarados, el boilerplate del stack y ninguna referencia quedo colgando. Igual corre el comando de verificacion — que los archivos existan no garantiza que compilen.

### Presentes (14)

- `evaluacion/brechas-comunicacion.md`
- `evaluacion/flujo-trabajo-actual.bpmn.md`
- `disenio/metricas-exito.md`
- `proceso.bpmn.md`
- `mapeo-de-datos.csv`
- `openapi.yaml`
- `README.md`
- `disenio/pipeline-ci-cd.yaml`
- `disenio/roles-responsabilidades.md`
- `implementacion/buildspec.yml`
- `implementacion/security-config.yml`
- `implementacion/deployment-template.yml`
- `monitoreo/dashboard-metricas.md`
- `monitoreo/plan-mejora-continua.md`

### Capas del patron declarado

Cada una tiene que existir como directorio real con al menos un archivo. Codigo plano en la raiz no satisface el patron.

- `evaluacion/`
- `disenio/`
- `implementacion/`
- `monitoreo/`

## Verificacion

```bash
npx --yes @redocly/cli lint openapi.yaml
```

El comando tiene que pasar SIN implementar los archivos de la superficie de practica: solo andamiaje.

Ese comando pasando es la definicion de "terminado" para vos.

## Convenciones que tenes que respetar

- Un solo ecosistema: no declares librerias de otro lenguaje ni mezcles gestores de paquetes.
- Toda libreria que uses tiene que estar declarada en el manifiesto de dependencias.
- Todo import declarado tiene que usarse; todo tipo usado tiene que existir o venir de una dependencia declarada.
- El patron es **Pipeline de CI/CD con etapas orquestadas (Planificación, Compilación, Pruebas, Despliegue, Monitoreo) y patrones de seguridad integrados (Shift-Left Security)**: los contratos (interfaces, puertos) los define la capa interna y los implementa la externa, nunca al revés.
- Los archivos que crees llevan implementacion real, no stubs: sin `TODO`, sin cuerpos vacios, sin `// getters y setters`.

## Contexto del candidato

Sirve para calibrar el nivel del codigo, no para resolver las fases.

- Perfil: Chapter Integración, Especialidad Analista SOA, Tecnología Infraestructura AWS, Senior
- Brecha que el reto ataca: Promueve la comunicación e integración entre equipos de desarrollo, operaciones y seguridad. Comprende el SDLC (Software Development Life Cycle) y su participación como arquitecto en cada parte del ciclo.
- Mision: Candidato con experiencia Senior, trabaja en sistemas de integración SOA con énfasis en arquitectura de software y seguridad

---

*Generado por Challenge Generator — Pragma. `README.md` tiene el enunciado completo del reto para la persona. `PROMPT_MEJORA.md` es la variante para pegar en un chat, si se prefiere ese flujo.*
