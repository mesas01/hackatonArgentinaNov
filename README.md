# 🌟 Evento Estelar: Seguimiento de Participación Descentralizada

## 1. Declaración del Problema

### ¿Qué problema del mundo real resuelves?
Estás resolviendo la necesidad de un sistema fiable y transparente para registrar y verificar actividades. Construir esto en Stellar permite crear un sistema de seguimiento de actividad descentralizado, eficiente, verificable y de bajo costo.

### ¿Para quién es este un problema?
Este problema afecta a la **comunidad Stellar** y a los participantes de sus eventos. Ellos necesitan una manera confiable de seguir y verificar sus actividades. También beneficia a proyectos públicos en Stellar que requieren registros de actividad transparentes.

### ¿Por qué es este problema urgente o importante ahora?
Las comunidades y proyectos necesitan urgentemente maneras transparentes, verificables y descentralizadas para rastrear la participación. A medida que el ecosistema Stellar crece, tener un sistema nativo para registrar actividades fortalece la confianza, recompensa la participación y apoya nuevos casos de uso.

## 2. Usuario Objetivo y Necesidad Principal

### ¿Quién es tu usuario principal?
Los **organizadores de eventos** y organizaciones que contratan extras.

### ¿Cuál es su necesidad o problema central?
Necesitan adaptar un modelo existente de seguimiento de participación a Stellar. Esto busca crear una forma unificada y confiable de registrar actividades, organizadores, asistencia y ubicaciones en todos los niveles de la organización.

### ¿Cómo resuelven esto actualmente?
Hoy existen soluciones similares en otras redes. En Stellar, se hace con tokens o contratos inteligentes, pero falta un enfoque estándar y adoptado. Tu objetivo es implementar una solución clara y confiable de seguimiento de participación directamente en la red Stellar.

## 3. Descripción de la Solución

### 3.1 Idea Principal

Quieres crear una herramienta para registrar la asistencia a eventos de la comunidad Stellar. Cuando alguien asiste, puede reclamar un token en la red Stellar como prueba de participación. Las personas pueden recolectar el token con métodos simples como NFC o una palabra secreta. Esto da a la organización un registro claro y verificable de quién participa activamente en los eventos de Stellar.

El organizador de un evento quiere una manera fácil de rastrear la asistencia y obtener métricas. Los asistentes quieren un método simple y divertido para registrarse y recibir una recompensa estilo NFT por participar. El sistema conecta ambas necesidades: permite a los organizadores registrar la asistencia y a los participantes reclamar su token en Stellar.

### 3.2 ¿Por qué Stellar?

Stellar es la mejor opción porque permite la emisión y verificación de registros de participación de forma **rápida, global y con costos extremadamente bajos**. La tarifa de red es mínima, haciendo que el sistema sea totalmente sostenible. La infraestructura de Stellar ofrece alta escalabilidad y fácil integración con billeteras y herramientas existentes.

**Elementos de Stellar que usarás:**
* Red Stellar
* Contratos Inteligentes Soroban

## 4. Características Principales (Planificadas para el Hackathon)

| Característica | Lo que el usuario puede hacer | Criterio de funcionamiento |
| :--- | :--- | :--- |
| 1. Implementado en Mainnet | Tú puedes reclamar y ver tus tokens de asistencia en la red Stellar real. | Las transacciones se muestran correctamente en el libro mayor. |
| 2. Creación y Distribución de NFT | Los organizadores pueden crear y enviar NFT, y los usuarios pueden recibirlos o transferirlos. | Los NFT se acuñan y se entregan sin errores. |
| 3. Experiencia Amigable | Organizadores y asistentes pueden usar la plataforma fácilmente. | Las personas completan las acciones sin problemas y no reportan inconvenientes. |

## 5. Arquitectura MVP (Idea Inicial)

Esta es una primera propuesta, evolucionará durante el hackathon.

* **Frontend:** Una interfaz web sencilla con React. Los organizadores pueden crear eventos y tú puedes reclamar tus tokens.
* **Backend / Servicios:** Una API ligera en Node o Python. Esta gestiona la creación de eventos, la generación de tokens y la comunicación con la red Stellar.
* **Contratos Inteligentes:** Contratos Soroban. Ellos son responsables de acuñar y administrar los tokens de asistencia, además de verificar los reclamos de los usuarios.
* **Datos / Almacenamiento:** Una base de datos básica como Postgres o almacenamiento simple en la nube para metadatos y registros de eventos. Los datos de participación central se registran en la red Stellar.

**Flujo del Sistema:** Tú → Frontend Web → Backend/API → Soroban/Red Stellar → Almacenamiento de Datos del Evento.

## 6. Criterios de Éxito para el Hackathon

Considerarás el MVP exitoso si:

* Un usuario puede **reclamar un token de asistencia simple**.
* Podemos demostrar que **un token fue creado y aparece en la red Stellar**.
* Podemos medir o mostrar **una transacción exitosa en el libro mayor**.

## 7. Equipo

* **Nombre del equipo:** Blockotitos
* **Miembros y roles:**
    * Santiago Mesa – Desarrollador (Dev)
    * Andre Landinez – Desarrollador (Dev)
    * Juliana Lugo – Jefa de Proyecto (PM)
    * Lizeth Rico – Diseñadora
    * Sebastian Verduguez – Tester
