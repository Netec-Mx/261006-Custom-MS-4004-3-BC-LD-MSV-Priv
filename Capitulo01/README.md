# Práctica: Análisis de PDF con diagrama o flujo visual en Copilot Chat, estructuración del proceso y generación de proceso_actual.md

## Metadatos

| Campo | Detalle |
| :--- | :--- |
| **Duración** | 17 minutos |
| **Complejidad** | Media |
| **Nivel de Bloom** | Aplicar |

---

## Descripción General

En este laboratorio práctico, asumirás el rol de un Analista de Procesos de TI. Tu objetivo principal es analizar un flujo visual de negocio que describe el proceso "As-Is" (actual) de aprobación de créditos comerciales en una entidad financiera. Para asegurar la reproducibilidad y evitar fallos por dependencias de archivos externos, utilizarás una especificación semántica estructurada del diagrama visual.

Utilizando **Microsoft 365 Copilot Chat** configurado en modo seguro de **Trabajo (Work/BizChat)**, ejecutarás una estrategia de prompting avanzado para extraer y categorizar de manera exacta los elementos clave del proceso. Finalmente, estructurarás la información y exportarás un entregable técnico en formato Markdown (`proceso_actual.md`) dentro de tu directorio local de trabajo, diferenciando rigurosamente los hechos empíricos de las inferencias y suposiciones técnicas.

---

## Objetivos de Aprendizaje

Al finalizar este laboratorio, serás capaz de:
- [ ] Configurar y utilizar de forma segura la interfaz de **Microsoft 365 Copilot Chat** en modo corporativo (**Trabajo / BizChat**).
- [ ] Aplicar técnicas de ingeniería de prompts estructurados para extraer la estructura semántica de un flujo de proceso.
- [ ] Categorizar con precisión técnica actores, actividades, decisiones, sistemas, entradas, salidas, excepciones y dependencias de un proceso.
- [ ] Diseñar un documento Markdown estructurado (`proceso_actual.md`) que segregue de manera explícita los hechos observados de las inferencias lógicas del modelo de IA.

---

## Prerrequisitos

Para realizar este laboratorio, necesitas:
- Acceso a un navegador web compatible con el tenant corporativo.
- Licencia activa de **Microsoft 365 Copilot Premium** (Product Release 2024).
- Cuenta con acceso habilitado a **Copilot Chat en Modo Trabajo (BizChat)**.
- Conocimientos básicos de sintaxis Markdown y diagramas de flujo estándar.

---

## Entorno de Laboratorio

Este laboratorio requiere la interacción con herramientas de software locales y de nube. A continuación se detallan las versiones específicas requeridas para garantizar la correcta ejecución de los ejercicios:

### Software Requerido

| Software / Plataforma | Versión Específica | Enlace Oficial de Referencia |
| :--- | :--- | :--- |
| **Microsoft Edge** | 122.0.2365.92 (64-bit) | [Descargar Edge](https://www.microsoft.com/es-es/edge) |
| **Visual Studio Code** | 1.87.2 (System Installer x64) | [Historial de VS Code v1.87](https://code.visualstudio.com/updates/v1_87) |
| **Copilot Chat (Modo Trabajo)** | Product Release 2024 (Premium) | [Portal de M365 Copilot](https://copilot.microsoft.com/) |

### Directorio de Trabajo

Todas las operaciones locales y el almacenamiento de entregables deben realizarse de forma estricta en la siguiente ruta unificada:

```
C:\CopilotLabs\
```

#### Comando de Configuración Inicial (PowerShell)

Para preparar el entorno de manera consistente, abre una ventana de **PowerShell** (versión 5.1 o superior) y ejecuta el siguiente comando para garantizar la existencia del directorio de trabajo global:

```powershell
New-Item -ItemType Directory -Force -Path "C:\CopilotLabs\"
```

---

## Instrucciones Paso a Paso

El proceso de negocio que vas a analizar simula la extracción visual de un diagrama PDF de "Aprobación de Créditos Comerciales" para una entidad bancaria corporativa. Para garantizar la consistencia en el análisis de la IA, utilizaremos la especificación del diagrama embebida en las instrucciones de los prompts.

### Paso 1: Inicializar el entorno y preparar los datos de origen

**Objetivo:** Crear el espacio de trabajo local y comprender la especificación técnica del diagrama de flujo que procesará la Inteligencia Artificial.

**Instrucciones:**

1. Asegúrate de tener abierta la ventana de PowerShell donde creaste el directorio `C:\CopilotLabs\`.
2. Ejecuta el siguiente comando en PowerShell para abrir Visual Studio Code (v1.87.2) directamente apuntando a tu directorio de trabajo unificado:

   ```powershell
   code "C:\CopilotLabs\"
   ```

3. Mantén la ventana de Visual Studio Code abierta en segundo plano. Volverás a ella para guardar el entregable final.
4. Analiza la siguiente especificación de datos que representa el contenido del "PDF del Diagrama de Crédito Comercial" que procesará el modelo de IA:

```yaml
--- DIAGRAMA DE FLUJO: PROCESO AS-IS DE APROBACIÓN DE CRÉDITO COMERCIAL ---
[Carriles / Swimlanes]
- Solicitante (Ejecutivo de Cuenta)
- Analista de Riesgos (Mesa de Control)
- Comité de Crédito (Aprobadores Senior)

[Sistemas Involucrados]
- CRM Dynamics 365 (Registro de solicitudes de clientes)
- Core Bancario SAP (Validación de saldo e historial del cliente)
- Sistema de Firmas Electrónicas (Adobe Sign)

[Flujo Secuencial de Actividades]
1. INICIO: El Ejecutivo de Cuenta recibe la solicitud física de crédito comercial de parte del cliente.
2. Actividad: Registrar solicitud en CRM Dynamics 365 de forma manual.
   - Entrada: Formulario físico firmado, Estados Financieros del cliente en PDF.
   - Salida: ID de Solicitud generado automáticamente en el CRM.
3. Actividad: Validación preliminar en Core Bancario SAP (Ejecución Semiautomática).
   - Entrada: ID de Solicitud de CRM, Identificador Tributario (NIT/RUT) de la empresa solicitante.
   - Salida: Reporte de historial crediticio del cliente e inconsistencias financieras.
4. Decisión: ¿El cliente presenta historial crediticio negativo o tiene deudas activas superiores al 50% de su patrimonio total?
   - SÍ: Cancelar el flujo de forma automática en el sistema. Notificar al cliente la denegación vía correo del CRM. FIN DEL PROCESO.
   - NO: Continuar con el flujo. Enviar de manera digital el expediente completo de crédito al Analista de Riesgos.
5. Actividad: Análisis detallado de Riesgos de Crédito (Evaluación Manual).
   - Actor: Analista de Riesgos (Mesa de Control).
   - Sistema: CRM Dynamics 365.
   - Detalle: El analista realiza un cruce de datos analizando visualmente los PDF de estados financieros adjuntos y el reporte de SAP.
6. Decisión: ¿El monto total de la solicitud de crédito es superior a USD $500,000?
   - SÍ: Escalar la solicitud. Requiere obligatoriamente la deliberación y aprobación por parte del Comité de Crédito.
   - NO: El Analista de Riesgos puede aprobar de forma directa en CRM Dynamics 365.
7. Actividad (Ruta de Escalamiento): Sesión del Comité de Crédito para evaluar la viabilidad financiera.
   - Actor: Comité de Crédito (Aprobadores Senior).
   - Entrada: Acta de Recomendación de Riesgos (Documento Word compilado manualmente por el Analista).
   - Salida: Acta de Decisión Colegiada firmada físicamente por los miembros.
8. Actividad: Firma del pagaré digital de desembolso.
   - Sistema: Adobe Sign.
   - Actor: Cliente Externo y Representante Legal del Banco.
9. Actividad: Desembolso efectivo del dinero en el Core Bancario SAP.
   - Entrada: Pagaré firmado digitalmente.
   - Salida: Transferencia bancaria interbancaria de fondos al cliente. FIN DEL PROCESO.

[Excepciones Documentadas]
- Excepción A: Si los Estados Financieros en PDF adjuntos en el CRM están ilegibles, el Analista de Riesgos devuelve el caso al Ejecutivo de Cuenta vía CRM para su re-carga de datos. Esto detiene temporalmente el ANS (SLA) por un máximo de 5 días hábiles.
- Excepción B: Si el cliente rechaza explícitamente los términos de la tasa de interés propuestos en el Pagaré dentro de la plataforma Adobe Sign, el proceso se cancela definitivamente.
```

**Resultado Esperado de este Paso:** Directorio de trabajo local configurado y datos fuente listos para ser procesados por la IA.

**Verificación:** Ejecuta `Test-Path "C:\CopilotLabs\"` en tu terminal de PowerShell. Debe retornar `True`.

---

### Paso 2: Configurar Copilot Chat en Modo Trabajo (BizChat)

**Objetivo:** Garantizar la seguridad corporativa y habilitar el contexto adecuado para la protección de datos utilizando la interfaz de Copilot para el trabajo.

**Instrucciones:**

1. Abre tu navegador web **Microsoft Edge** (v122.0.2365.92).
2. Navega a la URL oficial de Microsoft Copilot: [https://copilot.microsoft.com](https://copilot.microsoft.com) o ingresa mediante el portal de Office en [https://microsoft365.com/chat](https://microsoft365.com/chat).
3. Inicia sesión con tus credenciales corporativas que cuenten con la licencia de **Microsoft 365 Copilot Premium**.
4. En la parte superior de la pantalla de chat, localiza el selector de contexto (pestañas de modo).
5. Selecciona la pestaña **Trabajo (Work / BizChat)**. *Nota: Asegúrate de que no esté seleccionada la pestaña "Web"*. Sabrás que estás en el modo correcto porque el color de la interfaz de chat cambia a un tono azul corporativo y se resalta una etiqueta que indica "Protección de datos comerciales activa" o "Los datos corporativos están protegidos".

```
┌────────────────────────────────────────────────────────┐
│  M365 Copilot   [ Web ]  * [ Trabajo ] *               │
├────────────────────────────────────────────────────────┤
│  🛡️ El contenido de tu organización está protegido.   │
└────────────────────────────────────────────────────────┘
```

**Resultado Esperado de este Paso:** Interfaz de Microsoft 365 Copilot Chat iniciada en Modo Trabajo, lista para recibir prompts corporativos de forma segura.

**Verificación:** Confirma visualmente que el escudo verde o azul de protección de datos se muestra al lado de tu foto de perfil o debajo del cuadro de chat.

---

### Paso 3: Diseñar y ejecutar el Prompt de Extracción Estructurada

**Objetivo:** Escribir y enviar un prompt altamente estructurado que ordene a la IA analizar la especificación del proceso, categorizar sus variables estructurales y estructurar los datos bajo un modelo de certezas (Hechos, Inferencias, Dudas).

**Instrucciones:**

1. En el cuadro de diálogo de **Copilot Chat (Modo Trabajo)**, introduce el siguiente prompt estructurado en su totalidad. Este prompt utiliza delimitadores claros, define un rol experto, asigna tareas secuenciales y establece un formato de salida específico:

```text
## ROL Y CONTEXTO
Actúa como un Consultor Senior de Procesos de TI y Arquitectura de Negocio. Tu tarea es analizar detalladamente la especificación de un proceso de negocio "As-Is" correspondiente a la Aprobación de Créditos Comerciales en nuestra banca corporativa.

## INSTRUCCIONES DE PROCESAMIENTO
1. Analiza de forma exhaustiva el flujo, las condiciones y los sistemas descritos en la sección # ESPECIFICACIÓN DEL DIAGRAMA.
2. Extrae e identifica los siguientes 8 elementos estructurales del proceso de manera exacta:
   - Objetivo del proceso
   - Actores involucrados (Roles)
   - Sistemas de software implicados
   - Inventario de Actividades individuales
   - Puntos de Decisión (con sus respectivas condiciones lógicas)
   - Entradas y Salidas específicas de cada actividad
   - Excepciones del proceso (caminos alternativos de error/falla)
   - Dependencias estrictas entre actividades
3. Organiza la información en un documento técnico estructurado en Markdown.
4. Aplica una estricta "Clasificación de Certeza Técnica" para evitar alucinaciones:
   - HECHOS OBSERVADOS: Datos descritos de forma 100% explícita en la especificación.
   - INFERENCIAS LÓGICAS: Suposiciones altamente probables basadas en lógica estándar de TI (por ejemplo, "si se cancela el proceso en CRM, probablemente se envía una llamada de API al sistema de notificaciones, aunque no se dibuje"). Debes etiquetarlas explícitamente como [INFERENCIA].
   - DATOS POR CONFIRMAR: Preguntas críticas y vacíos de información que el equipo de TI debe validar con el dueño del proceso (SME).

## ESPECIFICACIÓN DEL DIAGRAMA
--- DIAGRAMA DE FLUJO: PROCESO AS-IS DE APROBACIÓN DE CRÉDITO COMERCIAL ---
[Carriles / Swimlanes]
- Solicitante (Ejecutivo de Cuenta)
- Analista de Riesgos (Mesa de Control)
- Comité de Crédito (Aprobadores Senior)

[Sistemas Involucrados]
- CRM Dynamics 365 (Registro de solicitudes de clientes)
- Core Bancario SAP (Validación de saldo e historial del cliente)
- Sistema de Firmas Electrónicas (Adobe Sign)

[Flujo Secuencial de Actividades]
1. INICIO: El Ejecutivo de Cuenta recibe la solicitud física de crédito comercial de parte del cliente.
2. Actividad: Registrar solicitud en CRM Dynamics 365 de forma manual.
   - Entrada: Formulario físico firmado, Estados Financieros del cliente en PDF.
   - Salida: ID de Solicitud generado automáticamente en el CRM.
3. Actividad: Validación preliminar en Core Bancario SAP (Ejecución Semiautomática).
   - Entrada: ID de Solicitud de CRM, Identificador Tributario (NIT/RUT) de la empresa solicitante.
   - Salida: Reporte de historial crediticio del cliente e inconsistencias financieras.
4. Decisión: ¿El cliente presenta historial crediticio negativo o tiene deudas activas superiores al 50% de su patrimonio total?
   - SÍ: Cancelar el flujo de forma automática en el sistema. Notificar al cliente la denegación vía correo del CRM. FIN DEL PROCESO.
   - NO: Continuar con el flujo. Enviar de manera digital el expediente completo de crédito al Analista de Riesgos.
5. Actividad: Análisis detallado de Riesgos de Crédito (Evaluación Manual).
   - Actor: Analista de Riesgos (Mesa de Control).
   - Sistema: CRM Dynamics 365.
   - Detalle: El analista realiza un cruce de datos analizando visualmente los PDF de estados financieros adjuntos y el reporte de SAP.
6. Decisión: ¿El monto total de la solicitud de crédito es superior a USD $500,000?
   - SÍ: Escalar la solicitud. Requiere obligatoriamente la deliberación y aprobación por parte del Comité de Crédito.
   - NO: El Analista de Riesgos puede aprobar de forma directa en CRM Dynamics 365.
7. Actividad (Ruta de Escalamiento): Sesión del Comité de Crédito para evaluar la viabilidad financiera.
   - Actor: Comité de Crédito (Aprobadores Senior).
   - Entrada: Acta de Recomendación de Riesgos (Documento Word compilado manualmente por el Analista).
   - Salida: Acta de Decisión Colegiada firmada físicamente por los miembros.
8. Actividad: Firma del pagaré digital de desembolso.
   - Sistema: Adobe Sign.
   - Actor: Cliente Externo y Representante Legal del Banco.
9. Actividad: Desembolso efectivo del dinero en el Core Bancario SAP.
   - Entrada: Pagaré firmado digitalmente.
   - Salida: Transferencia bancaria interbancaria de fondos al cliente. FIN DEL PROCESO.

[Excepciones Documentadas]
- Excepción A: Si los Estados Financieros en PDF adjuntos en el CRM están ilegibles, el Analista de Riesgos devuelve el caso al Ejecutivo de Cuenta vía CRM para su re-carga de datos. Esto detiene temporalmente el ANS (SLA) por un máximo de 5 días hábiles.
- Excepción B: Si el cliente rechaza explícitamente los términos de la tasa de interés propuestos en el Pagaré dentro de la plataforma Adobe Sign, el proceso se cancela definitivamente.

## FORMATO DE SALIDA (GENERAR EXCLUSIVAMENTE SINTAXIS MARKDOWN)
El entregable debe estructurarse estrictamente bajo las siguientes secciones de Markdown:
## 1. Ficha Técnica del Proceso
## 2. Inventario de Componentes (Actores, Sistemas)
## 3. Desglose de Flujo de Actividades y Decisiones
## 4. Excepciones y Dependencias Identificadas
## 5. Matriz de Certeza Técnica (Hechos vs Inferencias vs Dudas)
```

2. Haz clic en el botón de **Enviar** (icono de flecha de envío) en Copilot Chat.
3. Permite que Copilot analice la entrada y genere la respuesta en formato Markdown dentro del hilo de chat.

**Resultado Esperado de este Paso:** Respuesta de Copilot conteniendo el análisis semántico y la clasificación de certezas técnica formateada en bloques Markdown estructurados.

**Verificación:** Asegúrate de que la salida del chat contiene claramente las secciones especificadas y que las inferencias y dudas de TI están claramente identificadas.

---

### Paso 4: Validar, separar Hechos de Inferencias y exportar a Markdown

**Objetivo:** Revisar el análisis generado, asegurar la separación estricta de inferencias y persistir el entregable técnico en un archivo Markdown en tu máquina de desarrollo.

**Instrucciones:**

1. Revisa detenidamente el texto generado por la Inteligencia Artificial. Identifica si hay alguna "alucinación" (por ejemplo, si Copilot infirió que se usa Microsoft Outlook para las alertas de correo, debe estar explícitamente listado en "Inferencias Lógicas" y con la etiqueta `[INFERENCIA]`).
2. Copia todo el contenido Markdown generado por Copilot. Para hacer esto de forma rápida y limpia, haz clic en el botón **Copiar** (icono de dos páginas superpuestas) ubicado en la esquina inferior del bloque de respuesta de Copilot.
3. Cambia a la ventana activa de **Visual Studio Code (v1.87.2)** que abriste en el Paso 1.
4. En el panel lateral de VS Code, haz clic derecho sobre el espacio de trabajo vacío y selecciona **New File** (Nuevo Archivo), o utiliza el atajo de teclado `Ctrl + N`.
5. Nombra el archivo exactamente como:

   ```
   proceso_actual.md
   ```

6. Pega el contenido copiado de Copilot Chat dentro de la ventana de edición de VS Code (`Ctrl + V`).
7. El archivo debe reflejar fielmente la siguiente estructura técnica mínima de Markdown para asegurar la trazabilidad de datos:

   ```markdown
   # Análisis de Proceso: Aprobación de Créditos Comerciales (As-Is)

   ## 1. Ficha Técnica del Proceso
   - **Nombre del Proceso:** Aprobación de Créditos Comerciales
   - **Objetivo:** Resolver y procesar solicitudes de crédito comercial bancario de manera eficiente asegurando que cumplan los criterios de viabilidad del banco.

   ## 2. Inventario de Componentes
   - **Actores (Roles):** Solicitante (Ejecutivo de Cuenta), Analista de Riesgos (Mesa de Control), Comité de Crédito (Aprobadores Senior), Cliente Externo (Representante).
   - **Sistemas:** CRM Dynamics 365, Core Bancario SAP, Adobe Sign.

   ## 3. Desglose de Flujo de Actividades y Decisiones
   *(Aquí debe figurar el listado estructurado de actividades de inicio a fin según el análisis de Copilot, incluyendo entradas y salidas).*

   ## 4. Excepciones y Dependencias Identificadas
   *(Sección con el análisis exacto de las excepciones A y B del proceso y dependencias técnicas).*

   ## 5. Matriz de Certeza Técnica (Hechos vs Inferencias vs Dudas)
   ### Hechos Observados (100% Certeza)
   - El proceso cuenta con 3 carriles de decisión/roles específicos.
   - SAP y Dynamics 365 son los sistemas principales de registro y validación financiera.
   - El límite para el escalamiento obligatorio al Comité de Crédito es de USD $500,000.

   ### Inferencias Lógicas (Requieren Validación de TI)
   - `[INFERENCIA]` El envío digital de expedientes entre el CRM y el Analista de Riesgos se realiza mediante notificaciones del CRM o correos electrónicos automáticos (asume uso de un servidor SMTP corporativo).
   - `[INFERENCIA]` La cancelación automática del flujo en SAP por historial negativo requiere una integración vía API REST o RFC entre Dynamics 365 y SAP.

   ### Datos y Preguntas por Confirmar (SME / TI)
   1. ¿La validación en SAP que genera el reporte financiero es síncrona o asíncrona?
   2. ¿Qué mecanismo utiliza el Comité de Crédito para firmar de manera colegiada el Acta de Decisión (física o digital)?
   3. ¿Cómo se comunican Dynamics 365 y Adobe Sign para enviar el pagaré digital de manera automatizada?
   ```

8. Presiona `Ctrl + S` para guardar el archivo en VS Code. Asegúrate de guardarlo en la ruta exacta: `C:\CopilotLabs\proceso_actual.md`.

**Resultado Esperado de este Paso:** Archivo local `C:\CopilotLabs\proceso_actual.md` correctamente guardado con contenido estructurado que clasifica certeramente los datos del negocio.

**Verificación:** Abre la terminal integrada de VS Code (`Ctrl + Ñ` o `Ctrl + \``) y ejecuta el comando de PowerShell para listar el archivo y su longitud:

```powershell
Get-ChildItem -Path "C:\CopilotLabs\proceso_actual.md"
```

El resultado debe mostrar el archivo con un tamaño mayor a 0 KB, confirmando que la exportación fue exitosa.

---

## Validación y Pruebas

Para garantizar que el laboratorio se ha completado de acuerdo con los criterios de calidad y rigurosidad técnica de grado empresarial, realiza las siguientes comprobaciones estructuradas.

### 1. Validación de Ruta de Almacenamiento
Asegúrate de que el entregable se haya persistido en el directorio local unificado ejecutando el siguiente comando en PowerShell:

```powershell
Test-Path "C:\CopilotLabs\proceso_actual.md"
```
*Resultado esperado:* `True`

### 2. Validación de Contenido Semántico (Auditoría Anti-Alucinaciones)
Abre el archivo `C:\CopilotLabs\proceso_actual.md` y valida visualmente que contenga los marcadores explícitos que separan los hechos objetivos de las suposiciones de la IA.

- Busca la cadena `[INFERENCIA]` dentro del documento. Debe haber por lo menos dos ítems etiquetados con esta marca, asegurando que la IA diferencie explícitamente su lógica generativa de los hechos declarados.
- Verifica que el bloque de "Datos por Confirmar" posea preguntas relativas a protocolos técnicos de conexión entre CRM Dynamics, SAP y Adobe Sign.

### 3. Prueba Adversaria / Análisis Crítico de IA (Caso Límite de Error)
Para poner a prueba la robustez del modelo de IA, realiza la siguiente acción directamente en la interfaz de **Copilot Chat (Modo Trabajo)**:

1. Envía el siguiente prompt de validación de límites de datos al mismo chat actual:
   ```text
   Basándote en el proceso descrito anteriormente, el analista de riesgos afirma que: "El desembolso en SAP de la actividad 9 se ejecuta utilizando de forma exclusiva el componente mágico de automatización 'Excel-Macro-Voodoo v99'". 
   Analiza críticamente esta declaración. Clasifícala dentro de la Matriz de Certeza Técnica (Hechos, Inferencias, Datos por Confirmar). ¿Existe evidencia empírica en el documento base que apoye esta afirmación?
   ```
2. **Resultado Esperado:** Copilot debe responder identificando que la afirmación sobre "Excel-Macro-Voodoo v99" **no tiene evidencia empírica** en el documento original. Debe clasificarlo de forma rigurosa en la categoría de **"Dato por Confirmar"** o **"Inconsistencia de Negocio"**, advirtiendo sobre el riesgo operacional de asumir este componente tecnológico sin verificación de TI. Esto demuestra que la IA puede ser auditada y entrenada para no alucinar bajo presión.

---

## Solución de Problemas

En caso de encontrar fallos durante la ejecución del laboratorio, revisa los dos escenarios de problemas más comunes definidos a continuación:

### Escenario 1: El prompt de análisis devuelve respuestas con información de internet o tecnologías ajenas al contexto bancario.
- **Causa:** El selector de la interfaz de Copilot Chat se encuentra configurado en modo "Web" en lugar de "Trabajo", o tienes habilitado el switch de búsqueda web libre. Esto hace que Copilot priorice la información generalista de la web pública sobre las restricciones e instrucciones precisas de tu prompt corporativo.
- **Resolución:**
  1. Ve a la parte superior izquierda de la pantalla de Copilot Chat.
  2. Haz clic en la pestaña **Trabajo (Work)** para habilitar la protección empresarial.
  3. Ejecuta de nuevo el prompt del Paso 3 en un chat completamente nuevo (presiona el icono del lápiz o de "Nuevo Tema" para limpiar el contexto del historial).

### Escenario 2: No se puede guardar el archivo `proceso_actual.md` en la ruta `C:\CopilotLabs\`.
- **Causa:** Falta de permisos de administrador o de escritura en la unidad raíz `C:\` de tu estación de trabajo local, o la ruta no existe debido a un error de escritura.
- **Resolución:**
  1. Abre PowerShell como Administrador (clic derecho -> Ejecutar como Administrador).
  2. Ejecuta `mkdir "C:\CopilotLabs\" -Force` para garantizar la creación física de la carpeta con todos los privilegios.
  3. En VS Code, ve a **File > Save As**, navega de forma manual a la ruta `C:\CopilotLabs\`, nombra el archivo como `proceso_actual.md` y haz clic en Guardar.

---

## Limpieza

Para mantener el entorno local ordenado y seguro una vez completado el laboratorio:

1. Guarda todos los cambios en tu archivo `proceso_actual.md` dentro de Visual Studio Code y cierra la aplicación (`Ctrl + Q`).
2. Cierra las pestañas de navegación activas de Copilot Chat en Microsoft Edge para liberar memoria RAM del sistema.
3. **No elimines** el directorio `C:\CopilotLabs\` ni su archivo `proceso_actual.md`, ya que este entregable estructurado servirá de base de conocimiento (contexto) para la automatización, generación de plantillas y diseño en los laboratorios posteriores del plan de estudios unificado.

---

## Resumen

En este laboratorio práctico has completado con éxito la extracción técnica y estructuración del proceso de aprobación de créditos comerciales utilizando un enfoque estructurado en **Microsoft 365 Copilot Chat (BizChat)**.

### Conceptos Clave Consolidados
- **Modo Trabajo (BizChat):** Aprendiste a aislar tu contexto dentro de un entorno seguro de protección de datos empresariales de M365 Copilot, previniendo fugas de información y restringiendo las alucinaciones del modelo mediante un contexto empresarial controlado.
- **Estructuración Semántica:** Descompusiste un flujo visual en sus átomos de negocio (actores, sistemas, actividades, decisiones, entradas/salidas, excepciones y dependencias) sin alterar el significado operativo original.
- **Clasificación de Certezas:** Implementaste un método riguroso para categorizar las afirmaciones sobre el proceso en **Hechos Observados**, **Inferencias Lógicas** y **Datos por Confirmar**. Esta separación evita la creación de flujos de automatización basados en suposiciones erróneas, asegurando que solo los hechos verificados de TI se automaticen.

### Recursos para Seguir Aprendiendo
- [Configuración de Microsoft 365 Copilot en modo BizChat](https://learn.microsoft.com/es-es/copilot/)
- [Diseño y optimización de prompts para procesos en Microsoft Power Automate](https://learn.microsoft.com/es-es/power-automate/guidance/planning/identifying-process-bottlenecks)
- [Estándares de diagramación en BPMN de la OMG](https://www.omg.org/spec/BPMN/2.0/)
