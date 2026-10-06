# Práctica: Validación con Investigador, actualización de proceso_mejorado.md y elaboración de comunicaciones diferenciadas con Copilot en Outlook para equipos técnicos, responsables del proceso y patrocinadores

## Metadatos

| Atributo | Detalle |
| :--- | :--- |
| **Duración** | 25 minutos |
| **Complejidad** | Media |
| **Nivel de Taxonomía de Bloom** | Aplicar (Apply) |

## Descripción General

En este laboratorio práctico, el participante asumirá el rol de un Analista de Procesos de Negocio en una entidad financiera. Utilizará Microsoft 365 Copilot en modo Web para investigar benchmarks globales y latinoamericanos sobre tiempos de aprobación de crédito comercial. 

Con los datos obtenidos, estructurará y documentará el estado futuro del flujo en un archivo local llamado `proceso_mejorado.md` dentro del directorio unificado de trabajo. Finalmente, utilizará Copilot en Microsoft Outlook para redactar comunicaciones altamente diferenciadas y adaptadas a tres audiencias clave de la organización: el equipo técnico de desarrollo, el dueño de proceso (Process Owner) y los patrocinadores ejecutivos (Sponsors).

## Objetivos de Aprendizaje

Al finalizar este laboratorio, el participante será capaz de:
* Investigar estándares de la industria bancaria y benchmarks de tiempos de respuesta en créditos comerciales utilizando Copilot Chat (Web Mode con buscador Bing).
* Estructurar un diseño de proceso futuro deseado en un archivo Markdown (`proceso_mejorado.md`) alineado con los benchmarks obtenidos.
* Redactar correos electrónicos con tonos, enfoques y terminologías diferenciadas para tres audiencias clave utilizando las capacidades integradas de Copilot en Outlook.

## Prerrequisitos

* **Conocimientos Previos**:
  * Familiaridad básica con el formato Markdown (`.md`).
  * Comprensión del proceso general de aprobación de créditos comerciales.
  * Manejo de la interfaz web de Copilot Chat y Microsoft Outlook.

* **Requisitos de Acceso**:
  * Licencia activa de **Microsoft 365 Copilot Premium**.
  * Acceso a internet sin restricciones para búsquedas con Bing en Copilot.
  * Cuenta de correo corporativo configurada en Microsoft Outlook.

## Entorno de Laboratorio

Para garantizar la correcta ejecución del laboratorio, asegúrese de contar con las siguientes especificaciones técnicas de software y hardware:

### Especificaciones de Software

| Software | Versión Requerida | Enlace de Referencia Oficial |
| :--- | :--- | :--- |
| **Microsoft Outlook** | Microsoft 365 Apps para Empresas Versión 2402 (Build 17328.20142) de 64 bits | [Microsoft 365 Enterprise](https://www.microsoft.com/es-es/microsoft-365/enterprise/microsoft-365-apps-for-enterprise) |
| **Microsoft Edge** | Versión 122.0.2365.92 (o superior) de 64 bits | [Microsoft Edge](https://www.microsoft.com/es-es/edge) |
| **Visual Studio Code** | Versión 1.87.2 de 64 bits | [VS Code Download](https://code.visualstudio.com/) |
| **Licencia Copilot** | Microsoft 365 Copilot Premium (Habilitada en Tenant) | [Copilot para M365](https://learn.microsoft.com/es-es/copilot/microsoft-365/) |

### Configuración Inicial

1. Abra una terminal de PowerShell y ejecute el siguiente comando para garantizar la existencia del directorio global unificado:

```powershell
New-Item -ItemType Directory -Force -Path "C:\CopilotLabs\"
```

2. Asegúrese de que Microsoft Outlook esté abierto con la sesión iniciada en su cuenta corporativa donde se encuentra activa la licencia de Microsoft 365 Copilot.

---

## Instrucciones Paso a Paso

### Paso 1: Investigación de Benchmarks del Sector Financiero usando Copilot Chat (Modo Web)

**Objetivo**: Obtener datos empíricos sobre tiempos de procesamiento y automatización en la aprobación de créditos comerciales en el sector financiero bancario utilizando la funcionalidad de búsqueda web.

1. Abra el navegador **Microsoft Edge**.
2. Diríjase a [copilot.microsoft.com](https://copilot.microsoft.com) e inicie sesión con su cuenta corporativa.
3. En la parte superior de la interfaz de chat, asegúrese de que el selector de modo esté configurado en **"Web"** (asegurando que el switch de búsqueda web o Bing Search esté **Habilitado**).
4. Escriba el siguiente prompt estructurado en la caja de chat de Copilot:

```text
Usa tu función de búsqueda web para investigar los benchmarks actuales (años 2023-2024) sobre el ciclo de vida y tiempos de respuesta (SLA) para la aprobación de créditos comerciales o corporativos en el sector bancario de Latinoamérica. 
Específicamente, necesito:
1. El tiempo de respuesta promedio tradicional (manual) vs. el tiempo de respuesta de bancos líderes digitalizados (automatizados).
2. Los 3 principales cuellos de botella identificados en el proceso tradicional.
3. Los porcentajes de reducción de tiempos esperados al implementar flujos de integración de datos vía APIs y validación automatizada de riesgos.

Por favor, proporciona las fuentes o el contexto de la industria donde aplique de forma concisa.
```

5. Presione **Enter** y espere a que Copilot realice la búsqueda y consolide la información.
6. Copie los datos clave y las métricas obtenidas (por ejemplo: reducción de tiempos de 15 días a 48 horas, o automatización del 60% de los pasos de validación) y guárdelas temporalmente en un bloc de notas.

*Resultado esperado*: Copilot Chat generará una respuesta detallada citando fuentes, con métricas específicas de reducción de tiempos (SLAs) de créditos comerciales mediante automatización y APIs en el sector bancario latinoamericano.

*Verificación*: Confirme que la respuesta de Copilot incluya íconos de fuentes web o enlaces de Bing que evidencien que se realizó una búsqueda en tiempo real, y que contenga métricas numéricas explícitas.

---

### Paso 2: Creación y Actualización de `proceso_mejorado.md`

**Objetivo**: Consolidar el diseño del flujo futuro (To-Be) del proceso de aprobación de créditos comerciales en un documento Markdown estructurado localizado en `C:\CopilotLabs\proceso_mejorado.md`, incorporando las métricas de benchmark obtenidas.

1. Abra **Visual Studio Code**.
2. Presione `Ctrl + N` para crear un nuevo archivo y guárdelo inmediatamente (`Ctrl + S`) en la ruta exacta: `C:\CopilotLabs\proceso_mejorado.md`.
3. Copie y pegue la siguiente plantilla base dentro del archivo:

```markdown
## Propuesta de Proceso Optimizado: Aprobación de Crédito Comercial

## 1. Visión General del Proceso (To-Be)
El nuevo proceso optimizado reduce los tiempos de validación y análisis de riesgo mediante la automatización de flujos y la integración directa de datos a través de APIs financieras, alineándose con las mejores prácticas del sector en Latinoamérica.

## 2. Benchmarks de la Industria (Validación Web)
* **SLA Tradicional de Mercado**: [Insertar tiempo tradicional obtenido en el Paso 1]
* **SLA de Bancos Digitalizados**: [Insertar tiempo automatizado obtenido en el Paso 1]
* **Meta de Nuestro Proyecto**: Reducción del [Insertar % de reducción obtenido] en el tiempo total de ciclo de aprobación.

## 3. Flujo Detallado del Proceso
1. **Solicitud Digital**: El cliente ingresa la información en el portal web corporativo.
2. **Extracción y Validación (API)**: Consumo inmediato de servicios de Score de Crédito e información fiscal del cliente.
3. **Pre-evaluación Automática**: Motor de reglas de riesgo determina viabilidad en menos de 10 minutos.
4. **Análisis de Analista Senior (Solo Excepciones)**: Desviaciones o montos mayores a $500,000 USD son revisados manualmente.
5. **Aprobación y Desembolso**: Integración con el core bancario para generación automática de contratos y transferencia.

## 4. Tecnologías Clave de Integración
* REST APIs para buró de crédito.
* Motor de Decisiones de Riesgo (BPMN).
* Firma Electrónica Avanzada.
```

4. Reemplace los marcadores de posición entre corchetes `[...]` en la sección **2. Benchmarks de la Industria** con los datos reales que obtuvo de la búsqueda en el **Paso 1**.
5. Guarde el archivo `C:\CopilotLabs\proceso_mejorado.md`.

*Resultado esperado*: Un archivo markdown estructurado con datos reales de mercado bancario guardado en la ruta unificada local.

*Verificación*: En Visual Studio Code, presione `Ctrl + Shift + V` para visualizar el preview de Markdown y confirmar que la estructura del documento sea correcta, legible y contenga los datos integrados.

---

### Paso 3: Redacción del Correo para el Equipo Técnico en Outlook

**Objetivo**: Utilizar Copilot en Outlook para redactar un correo electrónico técnico y detallado enfocado en las especificaciones tecnológicas del nuevo proceso para los desarrolladores.

1. Abra la aplicación de escritorio de **Microsoft Outlook**.
2. Haga clic en **Nuevo correo** (New Email).
3. Coloque el cursor en el cuerpo del mensaje y haga clic en el icono de **Copilot** (Redactar con Copilot / Draft with Copilot).
4. Introduzca la siguiente instrucción de redacción dentro del cuadro de diálogo de Copilot:

```text
Escribe un correo formal pero directo dirigido al equipo de Arquitectura y Desarrollo de Software. 
Asunto: Especificaciones técnicas de integración para el proyecto de Aprobación de Crédito Comercial Optimizado.
Contenido:
Explica que hemos definido el diseño de proceso optimizado en el archivo "C:\CopilotLabs\proceso_mejorado.md". 
Necesitamos que se enfoquen en el desarrollo de las REST APIs para interactuar con el motor de reglas de riesgo y los servicios de validación de identidad del buró de crédito.
Establece que el objetivo técnico principal es lograr tiempos de respuesta sub-segundo en la validación inicial para cumplir con el benchmark de pre-aprobación en menos de 10 minutos.
Solicita una reunión técnica para revisar el mapeo de campos API el próximo martes a las 10:00 AM.
Tono: Técnico, preciso y profesional.
```

5. Haga clic en **Generar** (Generate).
6. Revise la propuesta de Copilot. Si es necesario, ajuste el tono seleccionando "Opciones de redacción" (formal, directo) y haga clic en **Mantener** (Keep).

*Resultado esperado*: Un correo estructurado en borrador que mencione de manera precisa la ruta del archivo local `C:\CopilotLabs\proceso_mejorado.md`, los requisitos de la API REST, la meta de los 10 minutos de pre-aprobación y la convocatoria para la reunión del martes.

*Verificación*: Confirme que el borrador del correo no contenga marcadores de posición genéricos y que mantenga el enfoque técnico solicitado antes de guardarlo en la carpeta de borradores (Drafts).

---

### Paso 4: Redacción del Correo para el Responsable del Proceso (Process Owner) en Outlook

**Objetivo**: Generar un mensaje enfocado en la mejora de indicadores de negocio, SLAs, mitigación de riesgos y eficiencia operativa.

1. En Outlook, haga clic en **Nuevo correo**.
2. En el cuerpo del correo, inicie el asistente **Redactar con Copilot**.
3. Ingrese el siguiente prompt enfocado en el negocio en la interfaz de Copilot:

```text
Redacta un correo dirigido a la Gerencia de Operaciones de Crédito (Dueño del Proceso).
Asunto: Presentación de la propuesta de optimización de SLAs de Crédito Comercial basada en benchmarks de mercado.
Contenido:
Infórmale que hemos analizado las brechas operativas del proceso actual frente a los líderes digitalizados de la región, documentando la propuesta en "C:\CopilotLabs\proceso_mejorado.md".
Destaca cómo este rediseño reducirá los cuellos de botella en la fase de análisis manual de riesgos y mejorará de manera radical nuestro SLA general de aprobación, aproximándonos a los estándares de la industria (reducción significativa de días a horas).
Explica que la automatización liberará un 40% de la carga operativa de los analistas senior para que se concentren exclusivamente en casos complejos de montos elevados.
Pide su aprobación del flujo To-Be propuesto para iniciar la fase de pruebas piloto.
Tono: Persuasivo, enfocado en el negocio y métricas de desempeño (KPIs).
```

4. Haga clic en **Generar**.
5. Revise el contenido generado. Asegúrese de que el tono esté orientado al beneficio operativo y la optimización de recursos. Haga clic en **Mantener**.

*Resultado esperado*: Un borrador de correo formal que se enfoca en el ROI operativo, reducción de carga de analistas, mitigación de cuellos de botella y metas de nivel de servicio (SLA).

*Verificación*: Verifique que el correo electrónico resalte la métrica del "40% de liberación de carga operativa" y haga referencia directa al archivo `proceso_mejorado.md` de la carpeta `C:\CopilotLabs\`.

---

### Paso 5: Redacción del Correo para los Patrocinadores (Sponsors) en Outlook

**Objetivo**: Elaborar un comunicado de nivel ejecutivo de alta visibilidad enfocado en los impactos macroeconómicos, ROI y ventaja competitiva.

1. Cree un **Nuevo correo** en Outlook.
2. Inicie la herramienta **Redactar con Copilot**.
3. Ingrese la siguiente instrucción detallada para estructurar la comunicación ejecutiva:

```text
Escribe un correo sumamente ejecutivo dirigido al Comité de Dirección y Patrocinadores del Proyecto.
Asunto: Actualización estratégica e impacto en el ROI: Proyecto de Transformación del Crédito Comercial.
Contenido:
Presenta de manera sintética la propuesta de valor basada en el benchmark sectorial elaborado en "C:\CopilotLabs\proceso_mejorado.md".
Destaca los beneficios estratégicos principales:
1. Incremento estimado en la colocación de cartera de crédito comercial en un 15% debido a la reducción del abandono de clientes durante el ciclo de aprobación.
2. Disminución del costo operativo de procesamiento por solicitud.
3. Posicionamiento del banco como líder regional en agilidad digital.
Aclara que la inversión estimada inicial se recuperará en un plazo proyectado menor a 14 meses (ROI).
Solicita un espacio de 10 minutos en la próxima sesión de junta directiva para formalizar el aval presupuestal.
Tono: Ejecutivo, estratégico, enfocado en crecimiento de negocio y ROI. Corto y al grano.
```

4. Haga clic en **Generar**.
5. Evalúe el texto propuesto. Si el borrador inicial resulta demasiado extenso, seleccione la opción de longitud "Corto" en los ajustes de Copilot y regenere el contenido. Haga clic en **Mantener**.

*Resultado esperado*: Un correo conciso, de alta gama ejecutiva, estructurado en puntos clave (bullet points) destacando la colocación del 15% de cartera, retorno de inversión en 14 meses y la solicitud de espacio en la junta directiva.

*Verificación*: Confirme la precisión del tono y guarde el borrador en su carpeta de borradores de Outlook.

---

## Validación y Pruebas

Para garantizar que el laboratorio se ha completado de forma correcta y que se ha cumplido con la trazabilidad y la disciplina de ingeniería de prompts requerida, complete la siguiente validación.

### Criterio de Medición Operativa
* El archivo `proceso_mejorado.md` debe existir en el directorio exacto `C:\CopilotLabs\` y poseer un tamaño superior a 1 KB.
* Debe haber un total de 3 correos guardados en estado de "Borrador" (Drafts) en Microsoft Outlook, cada uno con un enfoque diferenciado (Técnico, Operaciones, Comité Directivo).

### Ejecución de Pruebas en PowerShell
Abra una consola de PowerShell y ejecute el siguiente bloque de comandos para auditar el resultado del laboratorio de forma automatizada:

```powershell
## 1. Validar la existencia del archivo de proceso optimizado
$filePath = "C:\CopilotLabs\proceso_mejorado.md"
if (Test-Path $filePath) {
    Write-Host "VALIDACIÓN EXITOSA: El archivo proceso_mejorado.md existe." -ForegroundColor Green
    $size = (Get-Item $filePath).Length
    Write-Host "Tamaño del archivo: $size bytes" -ForegroundColor Cyan
} else {
    Write-Warning "FALLO: El archivo proceso_mejorado.md no se encuentra en el directorio unificado C:\CopilotLabs\"
}
```

### Caso Adversario (Validación de Limitaciones de IA y Control de Alucinaciones)

Como prueba de control humana, se debe realizar una validación cruzada para evitar la propagación de datos alucinados por la Inteligencia Artificial:

1. Abra el archivo `C:\CopilotLabs\proceso_mejorado.md` en VS Code.
2. Copie los números de SLA exactos y el porcentaje de reducción que obtuvo de Copilot Chat en el **Paso 1**.
3. Abra el borrador de correo creado en el **Paso 5** (dirigido a Patrocinadores) en Outlook.
4. **Instrucción de control**: Verifique si el correo de patrocinadores contiene alguna cifra monetaria específica de inversión total (por ejemplo: *"el costo del proyecto es de $250,000 USD"*).
5. **Acción requerida**: Si Copilot incluyó números específicos de inversión que **no** estaban contemplados en los prompts o en el archivo `proceso_mejorado.md`, **bórrelos o modifíquelos inmediatamente**. Reemplácelos por una variable tipo `[Insertar Inversión Estimada]` para garantizar la veracidad del entregable y evitar la presentación de información financiera ficticia ante el Comité Directivo.

---

## Solución de Problemas

A continuación se presentan los dos problemas más comunes que pueden ocurrir durante la ejecución de este laboratorio, junto con sus causas raíz y soluciones verificadas:

### Problema 1: El botón "Redactar con Copilot" no aparece habilitado en la interfaz de Outlook

* **Síntoma**: Al redactar un correo nuevo en Microsoft Outlook, el icono o menú contextual de Copilot no se muestra en la cinta de opciones ni en el cuerpo del mensaje.
* **Causa Raíz**: El usuario está ejecutando la versión clásica de Outlook desactualizada o la cuenta corporativa activa en el perfil de Outlook no corresponde al Tenant de M365 que tiene asignada la licencia de **Microsoft 365 Copilot Premium**.
* **Solución**: 
  1. En la esquina superior derecha de Outlook, active el interruptor **"Probar el nuevo Outlook"** (New Outlook).
  2. Vaya a **Archivo > Cuenta de Office** y valide que la cuenta principal sea la cuenta con la licencia Copilot activa.
  3. Si persiste, cierre Outlook de forma completa, ejecute el comando `outlook.exe /cleanviews` desde la ventana de Ejecutar (`Win + R`) y vuelva a iniciar la aplicación para forzar la sincronización de licencias de M365.

### Problema 2: El modo web de Copilot Chat no retorna resultados de búsqueda en tiempo real de Bing

* **Síntoma**: Al enviar el prompt en el Paso 1, Copilot Chat responde indicando que no puede buscar en tiempo real o genera información histórica desactualizada sin enlaces de referencias.
* **Causa Raíz**: El switch de búsqueda web ("Web Search" o "Bing Search") se encuentra desactivado en la interfaz, o las directivas de seguridad corporativa del Tenant impiden la consulta de datos hacia la red externa.
* **Solución**:
  1. Verifique en la interfaz de Copilot Chat (en la esquina inferior de la caja de texto o en el encabezado) que el selector o botón de **Búsqueda Web** (icono de planeta o lupa) esté encendido (en color verde o activado).
  2. Si la cuenta empresarial tiene restringido el acceso web por políticas estrictas, abra una pestaña de Microsoft Edge en modo de navegación Privada (InPrivate), acceda a [copilot.microsoft.com](https://copilot.microsoft.com), inicie sesión con sus credenciales y ejecute la consulta desde el perfil público de Copilot.

---

## Limpieza

Para mantener el entorno limpio y respetar el ciclo de vida de desarrollo de TI, realice los siguientes pasos al finalizar el laboratorio:

1. **Gestión de Borradores**: En Microsoft Outlook, mantenga los 3 correos creados en su carpeta de borradores únicamente para fines de evaluación. Si no requiere conservarlos, puede eliminarlos seleccionando cada correo y presionando `Shift + Del`.
2. **Archivos Locales**: No elimine el directorio `C:\CopilotLabs\` ni el archivo `proceso_mejorado.md`, ya que este entregable será requerido como contexto de entrada y trazabilidad para los laboratorios subsecuentes del curso.
3. **Cierre de Sesiones**: Si utilizó una ventana de navegación privada o perfiles temporales de Edge, cierre todas las pestañas para limpiar las cookies de autenticación de forma segura.

---

## Resumen

En este laboratorio, ha experimentado con la potencia de la integración de herramientas de Microsoft 365 Copilot para optimizar el ciclo de diseño de procesos de negocio:

* **Investigó con precisión quirúrgica** estándares bancarios de la industria global de servicios financieros utilizando el modo de búsqueda web de Copilot Chat.
* **Documentó la brecha operativa** entre los procesos analógicos tradicionales de otorgamiento de crédito y los flujos modernos basados en APIs de integración, estructurando estos hallazgos directamente en `C:\CopilotLabs\proceso_mejorado.md`.
* **Desarrolló una estrategia de comunicación diferenciada y multinivel** al redactar de manera automatizada tres correos electrónicos en Microsoft Outlook adaptando el tono, las métricas clave y el nivel de tecnicismos para audiencias técnicas (desarrolladores), tácticas (dueño de proceso) y estratégicas (patrocinadores del proyecto), garantizando así un flujo ágil de adopción en la organización.
