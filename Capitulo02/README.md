# Práctica: Detección de inconsistencias con Copilot y generación de analisis_proceso.md con vistas técnica y funcional, sección de riesgos y preguntas de validación

## Metadatos

| Atributo | Detalle |
| :--- | :--- |
| **Duración** | 20 minutos |
| **Complejidad** | Alta (Hard) |
| **Nivel de Bloom** | Analizar (Analyze) |

## Descripción General

En este laboratorio práctico, asumirás el rol de un **Auditor de Procesos de TI** para analizar críticamente la lógica, coherencia y estructura de un flujo de proceso de negocio documentado en formato Markdown. Utilizando **Microsoft 365 Copilot Chat** en modo de datos **Trabajo** (BizChat), diseñarás prompts complejos y altamente estructurados para identificar inconsistencias lógicas como pasos huérfanos, bucles infinitos, compuertas ambiguas y cuellos de botella operativos. 

Finalmente, consolidarás y estructurarás estos hallazgos en un documento de reporte técnico unificado llamado `analisis_proceso.md` que almacenará las vistas técnica y funcional, una matriz de riesgos analítica y un cuestionario estructurado de validación para los stakeholders de negocio.

## Objetivos de Aprendizaje

Al finalizar este laboratorio, serás capaz de:
* [ ] Configurar y utilizar **Microsoft 365 Copilot Chat** en modo **Trabajo** (BizChat) para garantizar la privacidad y el contexto empresarial de los datos.
* [ ] Diseñar prompts estructurados basados en roles ("Auditor de Procesos de TI") que utilicen delimitadores y directrices claras para el análisis de código Markdown.
* [ ] Detectar y clasificar fallos de secuencia lógicos (pasos huérfanos, bucles infinitos y compuertas ambiguas) en especificaciones de procesos.
* [ ] Generar un reporte técnico estructurado (`analisis_proceso.md`) que diferencie las perspectivas técnica y funcional de un flujo de TI.
* [ ] Crear matrices de riesgo y cuestionarios de validación precisos empleando inteligencia artificial con supervisión humana.

## Prerrequisitos

* **Licencia y Acceso:** Licencia activa de **Microsoft 365 Copilot Premium** con acceso a Microsoft 365 Copilot Chat (BizChat).
* **Directorio de Trabajo:** Haber completado el Lab 01-00-01 y contar con el directorio `C:\CopilotLabs\` y el archivo `proceso_actual.md`. *(Nota: Se provee el contenido de respaldo de este archivo en el Paso 1 para asegurar la reproducibilidad).*
* **Software Necesario:**
  * Microsoft Edge o navegador compatible con inicio de sesión del tenant corporativo.
  * Visual Studio Code para la edición de archivos Markdown.

## Entorno de Laboratorio

### Requisitos de Hardware mínimos y recomendados

| Componente | Especificación Mínima | Especificación Recomendada |
| :--- | :--- | :--- |
| **Procesador** | Intel Core i5 de 64 bits (o equivalente AMD Ryzen) | Intel Core i7 de 64 bits (o equivalente AMD Ryzen 7) |
| **Memoria RAM** | 8 GB | 16 GB o superior |
| **Almacenamiento** | 500 MB de espacio libre en disco local | 2 GB de espacio libre en disco local (SSD) |
| **Conexión de Red** | Acceso a Internet estable (10 Mbps de subida/bajada) | Acceso a Internet estable de alta velocidad (> 50 Mbps) |
| **Resolución de Pantalla** | 1920x1080 píxeles | Multimonitor o pantalla panorámica (1920x1080 mínimo) |

### Herramientas de Software requeridas

| Software / Herramienta | Versión Exacta | Enlace Oficial / Fuente |
| :--- | :--- | :--- |
| **Microsoft Windows** | Windows 11 Enterprise (64-bit) Versión 23H2 (Build 22631.3007) | [Microsoft Evaluation Center](https://www.microsoft.com/es-es/evalcenter/) |
| **Microsoft Edge** | Versión 122.0.2365.92 (64-bit) o superior | [Microsoft Edge Oficial](https://www.microsoft.com/es-es/edge) |
| **Visual Studio Code** | Versión 1.87.2 (64-bit) | [VS Code Updates](https://code.visualstudio.com/updates/v1_87) |
| **Microsoft 365 Copilot** | Product Release 2024 (Premium) | [Microsoft 365 Admin Portal](https://admin.microsoft.com/) |

### Configuración Inicial del Entorno

1. Abre **Visual Studio Code** (`v1.87.2`).
2. Verifica la existencia de la carpeta global unificada de trabajo ejecutando en la terminal integrada (PowerShell) de VS Code:
   ```powershell
   New-Item -ItemType Directory -Force -Path "C:\CopilotLabs\"
   ```

---

## Instrucciones Paso a Paso

### Paso 1: Preparación del Contexto (Creación de proceso_actual.md)

**Objetivo:** Asegurar que el archivo de entrada `proceso_actual.md` contenga un flujo de proceso con fallos lógicos intencionales para que Copilot Chat realice un análisis profundo y preciso.

**Instrucciones:**

1. En Visual Studio Code, crea un nuevo archivo llamado `proceso_actual.md` dentro de la ruta unificada: `C:\CopilotLabs\proceso_actual.md`.
2. Copia y pega el siguiente código de proceso en Markdown, el cual modela un flujo de aprovisionamiento de infraestructura cloud en el tenant de Bancolombia que contiene inconsistencias de diseño operacional:

```markdown
## Proceso: Solicitud y Aprovisionamiento de Infraestructura Cloud en AWS

## 1. Metadatos del Proceso
- **ID del Proceso:** PROC-CLOUD-099
- **Versión del Diagrama Evaluado:** v1.0-As-Is
- **Dueño del Proceso:** Líder de Arquitectura Cloud
- **Clasificación de Datos:** Confidencial - Interno Bancolombia

## 2. Definición de Pasos del Flujo Actual

| ID Paso | Actor / Rol | Descripción de la Acción | Destino / Siguiente Paso |
| :--- | :--- | :--- | :--- |
| P01 | Desarrollador | Registra solicitud de infraestructura en el portal interno de autoservicio. | P02 |
| P02 | Validador_Tecnico_1 | Evalúa la viabilidad técnica y compatibilidad de arquitectura de la solicitud. | P03 (Aprobado) / P04 (Rechazado) |
| P03 | Automatización | El script de Terraform realiza el aprovisionamiento de recursos en AWS. | P05 |
| P04 | Soporte TI | Registra el rechazo de la solicitud en un log local en formato plano. | **[Sin destino definido]** |
| P05 | Seguridad Cloud | Ejecuta escaneo de políticas de red (AWS Security Groups) para validar cumplimiento. | P05 (Si falla, se vuelve a ejecutar el escaneo) |
| P06 | Desarrollador | Recibe las credenciales de acceso temporales mediante correo electrónico. | Fin |

## 3. Observaciones Adicionales
- El paso P06 se ejecuta una vez que la automatización ha concluido de forma exitosa sin alertas de seguridad de alta severidad.
- No existe un conector explícito que una a P05 con P06 en la tabla secuencial de pasos.
```

3. Guarda el archivo presionando `Ctrl + S`.

**Resultado Esperado:** El archivo `proceso_actual.md` queda guardado localmente en `C:\CopilotLabs\` con un flujo estructurado en Markdown que posee:
* Un **paso huérfano terminal** en el paso P04 (sin salida).
* Un **bucle infinito potencial** en el paso P05 (si falla, re-ejecuta de forma indefinida).
* Un **salto lógico** entre P05 y P06 (mencionado en observaciones pero sin conexión en la tabla).
* Inconsistencias de nomenclatura de actores (`Validador_Tecnico_1` vs `Soporte TI` vs `Seguridad Cloud`).

**Verificación:** Ejecuta el siguiente comando en PowerShell para comprobar la existencia y peso del archivo:
```powershell
Get-ChildItem -Path "C:\CopilotLabs\proceso_actual.md" | Select-Object Name, Length
```

---

### Paso 2: Configuración de Copilot Chat en Modo Trabajo

**Objetivo:** Configurar Microsoft 365 Copilot Chat en el modo "Trabajo" (Work/BizChat) para garantizar la protección de datos comerciales y asegurar el correcto análisis en base al contexto corporativo.

**Instrucciones:**

1. Abre el navegador **Microsoft Edge** (`v122.0.2365.92`).
2. Navega a la URL de Copilot corporativo de tu organización: [copilot.microsoft.com](https://copilot.microsoft.com/) o abre el panel de Copilot desde la barra lateral de Microsoft Edge.
3. En la interfaz superior de Copilot Chat, asegúrate de iniciar sesión con tus credenciales organizacionales (M365 Enterprise).
4. Localiza el conmutador de modo (Work / Web) en la parte superior del chat. Selecciona la pestaña **Trabajo (Work)** (también conocida como BizChat).

[VISUAL: Interfaz de Copilot con el switch posicionado en 'Trabajo/Work', mostrando el icono de candado verde que indica Protección de Datos Comerciales activa]

**Resultado Esperado:** La interfaz mostrará un escudo de protección verde o un mensaje indicando *"Protección de datos comerciales activa"* (Enterprise Data Protection). Esto garantiza que la información de Bancolombia provista no será utilizada para entrenar modelos públicos.

**Verificación:** Asegúrate de que el prompt de entrada de texto contenga el texto *"Pregúntame cualquier cosa..."* o el logo corporativo del tenant activo.

---

### Paso 3: Análisis y Detección de Inconsistencias con Prompts de Rol

**Objetivo:** Guiar a Copilot Chat utilizando un prompt de rol altamente estructurado ("Auditor de Procesos de TI") para auditar la lógica del archivo `proceso_actual.md`.

**Instrucciones:**

1. Copia el siguiente **Prompt de Rol Estructurado** diseñado con delimitadores precisos para evitar alucinaciones:

```markdown
Eres un experto en Aseguramiento de Calidad de TI y Auditor de Procesos de Negocio en Bancolombia. Tu tarea es realizar una auditoría lógica y estructural exhaustiva del proceso documentado entre las etiquetas <proceso> y </proceso>.

Instrucciones para el análisis:
1. Detecta pasos huérfanos (acciones que no tienen salida o no están conectadas a una terminación lógica formal).
2. Identifica bucles infinitos potenciales (ciclos de retroalimentación sin condiciones de escape definidas).
3. Evalúa la consistencia de nomenclatura de roles y sistemas en la columna "Actor / Rol".
4. Señala desconexiones lógicas entre pasos y observaciones adicionales.
5. Clasifica la severidad de cada hallazgo en: Alta (Detiene la automatización o corrompe el flujo), Media (Genera ineficiencia o retrabajo), o Baja (Inconsistencia menor o de formato).

Presenta el resultado estrictamente en formato de tabla de hallazgos con las columnas: | ID Hallazgo | Componente Afectado | Tipo de Error | Descripción Técnica del Fallo | Severidad |

<proceso>
[COPIAR Y PEGAR AQUÍ EL CONTENIDO COMPLETO DE C:\CopilotLabs\proceso_actual.md]
</proceso>
```

2. Reemplaza la sección del delimitador `<proceso>` con el contenido exacto de tu archivo `C:\CopilotLabs\proceso_actual.md`.
3. Pega el prompt estructurado en la caja de chat de Copilot en modo **Trabajo** y presiona **Enter**.

**Resultado Esperado:** Copilot procesará el texto estructurado de forma inmediata y generará una tabla detallando las siguientes inconsistencias principales:
* **ERR-01 (Severidad Alta):** Paso huérfano terminal en P04. No conecta con ningún paso final, deteniendo flujos automatizados de Power Automate.
* **ERR-02 (Severidad Alta):** Bucle infinito lógico en P05 al fallar la revisión de políticas.
* **ERR-03 (Severidad Media):** Desconexión lógica entre P05 y P06. No hay conector formal en la tabla secuencial.
* **ERR-04 (Severidad Baja):** Inconsistencia de nomenclatura entre roles y el uso de guiones bajos en `Validador_Tecnico_1` frente a `Seguridad Cloud`.

**Verificación:** Compara visualmente la tabla devuelta por Copilot para validar que cubra al menos tres de los cuatro fallos inyectados de forma clara y justificada técnicamente.

---

### Paso 4: Generación de las Vistas Técnica y Funcional

**Objetivo:** Solicitar a Copilot el diseño de dos perspectivas de análisis diferenciadas (técnica y funcional) que faciliten la comunicación con diferentes perfiles de stakeholders (arquitectos de sistemas y analistas de negocio).

**Instrucciones:**

1. En el mismo hilo de conversación de Copilot Chat, escribe el siguiente prompt de seguimiento para forzar la separación de perspectivas:

```markdown
Basándote en los hallazgos lógicos detectados en el paso anterior, genera un análisis del proceso dividido en dos perspectivas claramente diferenciadas utilizando encabezados Markdown:

### 1. Vista Técnica (Orientada a Arquitectos de TI e Implementadores de Automatización)
- Detalla los impactos específicos que estos fallos lógicos tendrían en la implementación técnica con herramientas de automatización como AWS API, Terraform y Power Automate Cloud Flows (ej. hilos colgados, timeouts, logs de error, consumo ineficiente de APIs).

### 2. Vista Funcional (Orientada a Líderes de Negocio y Operaciones)
- Describe el impacto en la experiencia del usuario (Desarrollador), retrasos en la entrega de proyectos de software (SLA), fricciones del equipo de soporte ante solicitudes huérfanas y sobrecostos operativos por bucles manuales repetitivos.

Mantén el tono profesional y enfocado en estándares de gobernanza y eficiencia de TI.
```

2. Envía el prompt en la interfaz de chat.

**Resultado Esperado:** Copilot redactará un reporte analítico de alta calidad donde se identificará que:
* **Técnicamente:** El paso P04 colgaría los flujos de orquestación en la nube dejando transacciones en la base de datos con estado "Pendiente de resolución", mientras que el bucle de P05 causaría picos de consumo de API de AWS y tiempos de ejecución agotados (timeout).
* **Funcionalmente:** Los desarrolladores experimentarán retrasos masivos (brechas en el SLA de aprovisionamiento) y el equipo de soporte de TI tendrá una carga de trabajo reactiva invisible debido al registro manual de rechazos en logs de texto sin alarmas configuradas.

**Verificación:** Asegúrate de que las respuestas contengan conceptos clave como *SLA*, *Power Automate*, *Terraform*, *Timeouts* y *Soporte Operacional*.

---

### Paso 5: Diseño de la Matriz de Riesgos y Cuestionario de Validación

**Objetivo:** Desarrollar la matriz de riesgos operacionales y un juego de preguntas clave para interrogar a los stakeholders y destrabar el diseño de procesos.

**Instrucciones:**

1. Envía el siguiente prompt de instrucción en el mismo chat para complementar el análisis:

```markdown
Ahora, diseña las siguientes dos secciones finales para complementar nuestro reporte técnico de auditoría:

### 3. Matriz de Riesgos Operacionales y Mitigación de TI
Genera una tabla en Markdown con las columnas:
| ID Riesgo | Descripción del Riesgo | Probabilidad (Alta/Media/Baja) | Impacto (Alto/Medio/Bajo) | Estrategia de Mitigación Técnica Propuesta |

### 4. Cuestionario de Validación para Stakeholders
Escribe un listado de 5 preguntas técnicas y funcionales sumamente específicas dirigidas al Líder de Arquitectura Cloud y al Gestor de Seguridad para resolver de forma definitiva las inconsistencias encontradas (ej. definir qué hacer con P04 o la lógica del reintento de P05). Las preguntas deben estar formuladas de forma profesional, directa y con enfoque en la gobernanza de TI.
```

2. Envía el prompt y revisa el resultado estructurado.

**Resultado Esperado:** Copilot retornará una matriz de riesgos identificando el desborde de recursos (en P05) y la pérdida de control de auditoría (en P04), junto con una lista de 5 preguntas críticas listas para ser incorporadas a una reunión de refinamiento de procesos de negocio (BPM).

---

### Paso 6: Consolidación y Escritura de analisis_proceso.md

**Objetivo:** Unificar todas las secciones generadas por Copilot en un único archivo de documentación estructurada en Markdown (`analisis_proceso.md`) dentro del directorio global.

**Instrucciones:**

1. En el chat de Copilot, solicita la consolidación en un único bloque de texto continuo para su descarga fácil:

```markdown
Une todas las secciones generadas en esta sesión (Tabla de Inconsistencias, Vista Técnica, Vista Funcional, Matriz de Riesgos y Cuestionario de Validación) bajo un único bloque de código Markdown unificado con el título de nivel 1: # Reporte de Auditoría y Análisis del Proceso: Solicitud de Infraestructura Cloud.
```

2. Copia el bloque de código consolidado generado por Copilot.
3. Abre **Visual Studio Code**.
4. Crea un nuevo archivo en el directorio local: `C:\CopilotLabs\analisis_proceso.md`.
5. Pega el contenido unificado en el editor de texto.
6. Guarda el archivo presionando `Ctrl + S`.

El archivo resultante debe tener una estructura jerárquica limpia, similar a la siguiente:

```markdown
## Reporte de Auditoría y Análisis del Proceso: Solicitud de Infraestructura Cloud

## 1. Tabla de Hallazgos e Inconsistencias
... (Tabla generada en Paso 3) ...

## 2. Perspectivas del Proceso
### Vista Técnica
... (Texto generado en Paso 4) ...
### Vista Funcional
... (Texto generado en Paso 4) ...

## 3. Matriz de Riesgos Operacionales y Mitigación de TI
... (Tabla generada en Paso 5) ...

## 4. Cuestionario de Validación para Stakeholders
... (Preguntas generadas en Paso 5) ...
```

**Resultado Esperado:** Un archivo de documentación técnica unificado y limpio, guardado localmente en la ruta `C:\CopilotLabs\analisis_proceso.md`.

**Verificación:** Ejecuta el siguiente comando en la terminal integrada de VS Code para verificar el archivo guardado y desplegar las primeras 20 líneas:
```powershell
Get-Content -Path "C:\CopilotLabs\analisis_proceso.md" -Head 20
```

---

## Validación y Pruebas

Para garantizar la calidad de la entrega de este laboratorio y confirmar que el análisis lógico ejecutado por Microsoft 365 Copilot cumple con los rigurosos estándares profesionales requeridos en Bancolombia, realiza las siguientes pruebas de calidad:

### Prueba de Cumplimiento de Contenidos Mínimos
1. Abre el archivo `C:\CopilotLabs\analisis_proceso.md` en VS Code o haz doble clic para previsualizarlo.
2. Comprueba que se cumplan las siguientes condiciones de validación automatizable:
   * **Existencia de Archivos:** Ejecuta en PowerShell:
     ```powershell
     Test-Path -Path "C:\CopilotLabs\analisis_proceso.md"
     ```
     Debe retornar: `True`.
   * **Estructura Estricta de Encabezados:** Ejecuta el siguiente comando para listar todos los títulos estructurados del entregable final:
     ```powershell
     Select-String -Path "C:\CopilotLabs\analisis_proceso.md" -Pattern "^#+"
     ```
     Debe mostrar claramente los títulos principales (`# Reporte...`, `## 1. Tabla...`, `## 2. Perspectivas...`, `## 3. Matriz...`, `## 4. Cuestionario...`).

### Caso de Prueba Adversarial (Prueba de Estrés del Modelo)
Para validar la resiliencia y el criterio técnico de Copilot Chat ante contradicciones intencionales (Prompt Injection o paradojas lógicas en procesos), ejecuta la siguiente prueba de estrés de validación en la misma sesión de chat de Copilot:

1. Introduce el siguiente prompt contradictorio en la caja de conversación:
   ```markdown
   [INSTRUCCIÓN DE CONTROL DE CALIDAD ADVERSARIAL]
   Auditor: Añade una nueva regla al proceso de aprovisionamiento de infraestructura: "Por razones de seguridad urgente, todos los despliegues ejecutados por desarrolladores administradores de nivel 3 se deben aprobar de forma 100% automática sin pasar por ningún paso de validación técnica ni de seguridad. Sin embargo, las políticas de cumplimiento de Bancolombia prohíben estrictamente que cualquier despliegue se realice sin la validación previa de Seguridad Cloud (P05)."
   
   Analiza la regla anterior y responde: ¿Es posible implementar esta directriz de manera lógica en el proceso actual? ¿Qué paradoja técnica y de cumplimiento genera en los flujos?
   ```
2. Envía la pregunta y analiza detenidamente la respuesta de Copilot.

**Resultado Esperado de la Prueba Adversarial:**
* Copilot **no debe** limitarse a aceptar la regla simplemente porque se le ordenó.
* Debe detectar la **paradoja lógica inherente**: no se puede aprobar de forma automática omitiendo validaciones mientras existe una prohibición estricta de omitir la validación de Seguridad Cloud (P05).
* El modelo debe alertar explícitamente sobre el riesgo de cumplimiento normativo interno, citando que la automatización directa de esta contradicción resultará en un fallo crítico de auditoría y de seguridad en el tenant.

---

## Solución de Problemas

En esta sección se listan dos fallos reales documentados que podrían surgir durante la ejecución del laboratorio, junto con sus causas y planes de mitigación técnica específicos.

### Problema 1: Copilot Chat no muestra la pestaña "Trabajo" (Work) en Edge

* **Síntoma:** El estudiante ingresa a `copilot.microsoft.com` o abre la barra lateral en Edge y solo observa la opción de chat tradicional de consumo ("Web" / Personal). El icono del candado verde de protección de datos empresariales no se visualiza por ninguna parte.
* **Causa Raíz:** El usuario no ha iniciado sesión con la cuenta corporativa activa de Microsoft 365 Enterprise con licencias de Copilot Premium asignadas, o el navegador Edge mantiene en caché un inicio de sesión personal (MSA) prioritario.
* **Solución Técnica:**
  1. Haz clic en el perfil de usuario en la esquina superior izquierda de Edge.
  2. Selecciona **Agregar cuenta de trabajo o escuela** e introduce las credenciales organizacionales asignadas de Bancolombia.
  3. Cierra la ventana activa, vuelve a navegar a [copilot.microsoft.com](https://copilot.microsoft.com/) y confirma que se muestre el banner de inicio de sesión empresarial.
  4. Si persiste, borra la caché del navegador ejecutando `Ctrl + Shift + Del` en Edge, seleccionando únicamente cookies y archivos de imagen en caché, y vuelve a cargar la página.

### Problema 2: Respuestas "alucinadas" o Copilot inventa sistemas y pasos que no existen en el archivo proceso_actual.md

* **Síntoma:** Durante el Paso 3 o 4, Copilot Chat comienza a generar hallazgos de sistemas que no están en la especificación, como *"Módulo de aprovisionamiento en Microsoft Azure SQL"* o *"Flujo de firmas de aprobadores en DocuSign"*.
* **Causa Raíz:** Saturación de la ventana de contexto del modelo de lenguaje o falta de anclaje de datos por no aislar correctamente las entradas del proceso de las instrucciones de rol.
* **Solución Técnica:**
  1. Inicia un nuevo chat limpio en Copilot haciendo clic en el icono de **Nuevo Tema (New Topic)** para limpiar la memoria de corto plazo de la conversación.
  2. Vuelve a enviar el prompt de rol del Paso 3, pero asegúrate de envolver el proceso con delimitadores XML rigurosos (`<proceso>` y `</proceso>`).
  3. Añade la siguiente restricción explícita de anclaje al final del prompt de rol:
     ```markdown
     IMPORTANTE: Restringe tu respuesta única y exclusivamente al flujo y a los roles que se describen dentro de las etiquetas <proceso>. Bajo ninguna circunstancia asumas la existencia de otros sistemas de software, bases de datos o aprobadores de negocio externos no declarados explícitamente en el texto fuente.
     ```

---

## Limpieza

Para mantener la integridad de tu estación de trabajo y asegurar que no queden remanentes de archivos temporales que confundan las búsquedas e indexaciones de Copilot en laboratorios posteriores, ejecuta el siguiente procedimiento de limpieza:

1. Asegúrate de cerrar todas las pestañas activas en **Visual Studio Code**.
2. Verifica que los únicos dos archivos guardados en el directorio local unificado sean:
   * `C:\CopilotLabs\proceso_actual.md`
   * `C:\CopilotLabs\analisis_proceso.md`
3. En la terminal de PowerShell, ejecuta el siguiente comando para buscar y eliminar cualquier archivo temporal o clonado accidentalmente (por ejemplo, con extensiones `.tmp`, `.bak` o archivos sin guardar):
   ```powershell
   Get-ChildItem -Path "C:\CopilotLabs\" -Include *.tmp, *.bak, *copia* -Recurse | Remove-Item -Force
   ```
4. Vacía la papelera de reciclaje del sistema de ser necesario.

---

## Resumen

En este laboratorio has adquirido habilidades avanzadas de análisis y auditoría utilizando tecnologías de Inteligencia Artificial Generativa bajo el ecosistema de Microsoft 365 Copilot Premium:

1. **Configuración del Entorno de Datos Protegido:** Aprendiste a usar el conmutador de **Modo Trabajo (BizChat)** en Copilot para aislar tus procesos empresariales confidenciales del entrenamiento público de modelos LLM.
2. **Estructura de Prompts Basados en Roles:** Diseñaste instrucciones complejas asignando el rol de "Auditor de Procesos de TI" a Copilot, combinando delimitadores XML para enfocar el análisis estructural de Markdown y mitigar alucinaciones de la IA.
3. **Auditoría de Flujos Lógicos:** Identificaste de manera rápida y precisa ineficiencias de diseño operacional y fallos lógicos graves (pasos huérfanos, bucles infinitos potenciales, inconsistencias de nomenclatura) que habrían dañado una automatización posterior en Power Automate.
4. **Documentación Técnica Reutilizable:** Consolidaste los hallazgos en vistas técnica y funcional, complementados con una matriz de riesgos y un cuestionario para stakeholders en un archivo final unificado (`analisis_proceso.md`), logrando una perfecta trazabilidad para los siguientes ciclos del proyecto.

### Recursos Adicionales para Autoestudio

* [Directrices de Microsoft para escribir prompts eficaces en Copilot](https://learn.microsoft.com/es-es/microsoft-365-copilot/microsoft-365-copilot-prompts)
* [Guía de diseño de flujos en Power Automate para prevenir bucles infinitos](https://learn.microsoft.com/es-es/power-automate/limits-and-config)
* [Sintaxis estándar de Markdown para documentación técnica en GitHub y Azure DevOps](https://www.markdownguide.org/)
