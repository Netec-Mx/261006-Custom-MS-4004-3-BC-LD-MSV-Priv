# Práctica: Generación de documentación del proceso en Word y presentación ejecutiva en PowerPoint con Copilot, verificando consistencia con el PDF original

## Metadatos

| Métrica | Detalle |
| :--- | :--- |
| **Duración** | 20 minutos |
| **Complejidad** | Media |
| **Nivel de Bloom** | Aplicar |

## Descripción General

En este laboratorio práctico, aprenderá a consolidar y sintetizar el análisis de procesos de negocio desarrollado en los laboratorios previos para generar entregables de nivel ejecutivo de forma automatizada y coherente. Utilizando Microsoft 365 Copilot en Word, redactará una propuesta formal de optimización de procesos basada en los archivos técnicos de análisis previos. Posteriormente, utilizará Copilot en PowerPoint para transformar dicho documento estructurado en una presentación visual de alto impacto para la junta directiva. Finalmente, realizará una auditoría crítica de consistencia de datos para identificar y corregir cualquier posible alucinación o discrepancia métrica introducida durante la transformación generativa de la IA.

## Objetivos de Aprendizaje

Al finalizar este laboratorio, usted será capaz de:
- [ ] Redactar una propuesta formal de optimización de procesos en Microsoft Word utilizando Copilot, tomando como referencia directa los análisis, diagramas estructurados y backlogs de mejora generados previamente.
- [ ] Convertir de forma automática un documento estructurado de Word en una presentación ejecutiva de diapositivas en PowerPoint utilizando el Copilot integrado.
- [ ] Auditar la fidelidad y consistencia de los datos entre el documento origen, la presentación generada y las métricas del proceso original, detectando desviaciones, omisiones o alucinaciones.

## Prerrequisitos

Para realizar este laboratorio con éxito, el participante requiere:
- **Conocimiento previo**:
  - Comprensión básica de la interfaz de Microsoft Word y PowerPoint.
  - Familiaridad con el flujo de procesos de negocio analizado en los laboratorios anteriores (`Lab 01-00-01` y `Lab 02-00-01`).
  - Nociones fundamentales de ingeniería de prompts e interacciones directas con asistentes de IA.
- **Acceso requerido**:
  - Cuenta institucional o de pruebas con suscripción activa a **Microsoft 365 Apps para Empresas (Enterprise)**.
  - Licencia activa de **Microsoft 365 Copilot Premium**.
  - Acceso completo de sincronización a **Microsoft OneDrive para la Empresa** asociado al mismo inquilino (tenant) de la licencia de Copilot.

## Entorno de Laboratorio

Para garantizar la correcta ejecución del laboratorio y la validez de los resultados, confirme que su entorno de trabajo cumple con las siguientes especificaciones:

### Especificaciones de Hardware
- **Procesador**: Intel Core i5 o superior (o equivalente AMD Ryzen) de 64 bits.
- **Memoria RAM**: Mínimo 8 GB (16 GB recomendado).
- **Conexión a Internet**: Estable con un ancho de banda mínimo de 10 Mbps simétricos para la correcta sincronización en la nube de los servicios de Microsoft 365.
- **Pantalla**: Resolución mínima de 1920x1080 píxeles.

### Especificaciones de Software

| Software | Versión Declarada | Origen de Descarga / Canal de Licenciamiento |
| :--- | :--- | :--- |
| **Microsoft Word** | Versión 2402 (Build 17328.20142) de 64 bits | Canal Empresarial Actual, Suscripción Microsoft 365 [ENLACE OFICIAL](https://learn.microsoft.com/en-us/officeupdates/update-history-microsoft365-apps-by-date) |
| **Microsoft PowerPoint** | Versión 2402 (Build 17328.20142) de 64 bits | Canal Empresarial Actual, Suscripción Microsoft 365 [ENLACE OFICIAL](https://learn.microsoft.com/en-us/officeupdates/update-history-microsoft365-apps-by-date) |
| **Microsoft Edge** | Versión 122.0.2365.92 de 64 bits | Instalación del Sistema Operativo Windows [ENLACE OFICIAL](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-relnote-stable-channel) |

### Configuración del Directorio de Trabajo

1. Todo el laboratorio debe ejecutarse de forma estructurada dentro de la siguiente ruta local unificada de su equipo de cómputo:
   `C:\CopilotLabs\`
2. Asegúrese de que los siguientes archivos clave (generados en los laboratorios previos o provistos como recursos base) se encuentren guardados en dicha ruta antes de iniciar el procedimiento:
   - `proceso_actual.md` (Documentación del proceso actual de originación de crédito)
   - `analisis_proceso.md` (Informe de cuellos de botella e ineficiencias)
   - `backlog_base.xlsx` (Listado de iniciativas de automatización y optimización prioritarias)

> **Nota Crítica de Configuración**: Microsoft 365 Copilot en Word y PowerPoint procesa archivos de referencia cruzada con mayor precisión si se encuentran almacenados y sincronizados en la nube del usuario. Por tanto, antes de iniciar el paso a paso, **copie o sincronice el directorio `C:\CopilotLabs\` completo dentro de su OneDrive para la Empresa**. Esto facilitará que la IA identifique las rutas web de los documentos compartidos.

---

## Instrucciones Paso a Paso

### Paso 1: Preparación del Entorno y Verificación de Archivos de Referencia

**Objetivo**: Garantizar que los documentos clave estén correctamente sincronizados y accesibles para Copilot en Microsoft 365, configurando las rutas de referencia necesarias.

#### Instrucciones

1. Abra el explorador de archivos y diríjase a `C:\CopilotLabs\`.
2. Verifique la existencia física de los siguientes tres archivos:
   - `proceso_actual.md`
   - `analisis_proceso.md`
   - `backlog_base.xlsx` (Debe estar formateado internamente con una tabla de Excel con el nombre `TablaBacklog`).
3. Abra su navegador **Microsoft Edge** e inicie sesión en el portal de Microsoft 365 (`https://portal.office.com`).
4. Acceda a **OneDrive para la Empresa** con sus credenciales institucionales.
5. Cree una carpeta en la raíz de su OneDrive llamada `CopilotLabs`.
6. Cargue los tres archivos mencionados desde `C:\CopilotLabs\` a la carpeta recién creada en OneDrive.
7. Para cada uno de los tres archivos cargados en OneDrive, haga clic en los tres puntos horizontales (`...`), seleccione **Copiar vínculo** y guarde estas direcciones URL temporales en un archivo de texto de bloc de notas (lo usará como anclaje contextual para los prompts de Copilot).

```text
Ejemplo de formato de vínculos de OneDrive guardados:
- Proceso Actual: https://corporativo-my.sharepoint.com/:t:/g/personal/usuario_dominio/EZx1...
- Análisis de Proceso: https://corporativo-my.sharepoint.com/:t:/g/personal/usuario_dominio/ERy2...
- Backlog de Excel: https://corporativo-my.sharepoint.com/:x:/g/personal/usuario_dominio/ETz3...
```

#### Resultado Esperado
Los archivos de entrada están cargados de forma redundante en el almacenamiento local `C:\CopilotLabs\` y en la nube de OneDrive corporativa, listos con enlaces de acceso válidos para el tenant.

#### Verificación
Abra una pestaña en el navegador Edge y pegue uno de los enlaces de OneDrive copiados. Si el archivo se abre directamente en su versión web de Microsoft 365 sin errores de permisos, la configuración es correcta.

---

### Paso 2: Generación del Documento de Propuesta en Microsoft Word

**Objetivo**: Estructurar un documento técnico formal denominado `documentacion.docx` que plantee la propuesta de optimización mediante el uso de instrucciones guiadas en el asistente integrado de Word Copilot.

#### Instrucciones

1. En su estación de trabajo local, abra **Microsoft Word**.
2. Cree un **Documento en blanco** nuevo.
3. Asegúrese de que el autoguardado esté activo en la esquina superior izquierda de la aplicación y guarde el archivo en la nube de OneDrive (dentro de la carpeta `CopilotLabs`) con el nombre exacto de:
   `documentacion.docx`
4. Al abrir el documento nuevo, verá de forma automática la ventana flotante de interacción de Copilot con la leyenda *"Borrador con Copilot"*. Si no aparece, haga clic en el botón de **Copilot** en la pestaña *Inicio* o presione la combinación de teclas `Alt + I`.
5. En el cuadro de texto para ingresar la instrucción, escriba el siguiente prompt altamente estructurado, reemplazando los marcadores entre corchetes con las URLs correspondientes guardadas en el Paso 1:

```text
Actúa como un Consultor Principal de Procesos de Negocio. Genera una propuesta formal y exhaustiva de optimización y rediseño para el proceso de originación de crédito de Bancolombia. 
Debes referenciar y extraer información precisa de los siguientes documentos fuente que están en mi OneDrive:
- Estructura del proceso actual: [PEGAR_AQUÍ_URL_DE_PROCESO_ACTUAL.MD]
- Cuellos de botella analizados: [PEGAR_AQUÍ_URL_DE_ANALISIS_PROCESO.MD]
- Soluciones de mejora priorizadas: [PEGAR_AQUÍ_URL_DE_BACKLOG_BASE.XLSX]

El documento debe estructurarse con los siguientes apartados específicos utilizando títulos de nivel 1 y 2:
1. Resumen Ejecutivo: Resumen ejecutivo del proyecto y valor de negocio.
2. Estado Actual (As-Is): Descripción objetiva basada en la documentación proporcionada, incluyendo los tiempos de ciclo y cuellos de botella del PDF original.
3. Propuesta de Estado Futuro (To-Be): Cómo la automatización con IA y RPA soluciona los cuellos de botella específicos del análisis.
4. Backlog de Implementación: Detalle explícito de las soluciones planteadas en el archivo de Excel cargado, respetando los campos de prioridad, costo estimado e impacto sin alterar los valores reales.
5. Métricas de Éxito Previstas: Tabla comparativa de tiempos de ciclo antes (As-Is) y después de la optimización (To-Be).

Usa un tono formal, profesional y corporativo. No inventes métricas ficticias ajenas a las fuentes suministradas.
```

6. Presione el botón **Generar**. Observe cómo Copilot comienza a escribir el texto estructurado directamente en el documento de Word.
7. Una vez finalizada la generación automática, Copilot mostrará un menú flotante con las opciones: *Conservar*, *Regenerar* o *Descartar*.
8. Haga clic en **Conservar**.
9. Revise el documento visualmente. Guarde los cambios finales del archivo haciendo clic en el icono de guardar o presionando `Ctrl + G`. Asegúrese de que el archivo final esté guardado localmente en `C:\CopilotLabs\documentacion.docx` mediante la opción *Guardar como* si el autoguardado no lo reflejó de forma automática en el disco local.

#### Resultado Esperado
Un archivo de Microsoft Word de 3 a 5 páginas llamado `documentacion.docx` con un formato estructurado, tablas comparativas y un backlog detallado alineado con la información de origen.

#### Verificación
Abra el archivo `C:\CopilotLabs\documentacion.docx`. Verifique que el documento contiene las 5 secciones solicitadas y que las métricas financieras e iniciativas del backlog coinciden exactamente con los datos presentes en `backlog_base.xlsx`.

---

### Paso 3: Generación de la Presentación Ejecutiva en PowerPoint

**Objetivo**: Generar una presentación de PowerPoint de alta calidad comercial (`presentacion.pptx`) a partir de la estructura jerárquica del archivo de Word, utilizando el plugin nativo de Copilot en PowerPoint.

#### Instrucciones

1. Abra **Microsoft PowerPoint** en su estación de trabajo local.
2. Inicie una presentación vacía (Nueva presentación en blanco).
3. Asegúrese de que ha iniciado sesión con la misma cuenta corporativa con licencia Copilot.
4. Haga clic en el botón de **Copilot** en la pestaña **Inicio** de la cinta de opciones superior. Se abrirá el panel lateral derecho de Copilot.
5. En el panel lateral, elija la sugerencia predeterminada o escriba el comando base:
   `Crear una presentación a partir de un archivo...`
6. Copilot sugerirá archivos recientes en un menú desplegable. Si no aparece el archivo en la lista, pegue directamente la URL de enlace para compartir de OneDrive que apunta a su archivo generado en el paso anterior (`documentacion.docx`), o escriba la barra inclinada `/` seguida del nombre de archivo:

```text
Crear una presentación a partir del archivo [PEGAR_AQUÍ_URL_DE_DOCUMENTACION.DOCX_EN_ONEDRIVE]
```

7. Presione la tecla **Enter** o haga clic en el botón de enviar del panel lateral.
8. El sistema mostrará un estado de progreso similar a *"Analizando el documento"*, *"Generando esquema"* y *"Creando diapositivas"*. Este proceso suele tardar de 30 a 60 segundos debido a la consolidación del contenido y diseño gráfico integrado.
9. Una vez finalizado el proceso, revise las diapositivas que se han creado automáticamente.
10. Utilice la función de diseño inteligente de PowerPoint integrada (como **Diseñador** o Designer) en caso de querer ajustar alguna diapositiva específica generada por la IA que contenga bloques excesivos de texto para transformarla en diagramas visuales.
11. Guarde la presentación en la ruta de trabajo local seleccionando *Archivo > Guardar como* y guardándola con el nombre exacto de:
    `C:\CopilotLabs\presentacion.pptx`

#### Resultado Esperado
Un archivo de presentación `presentacion.pptx` que consta típicamente de 6 a 10 diapositivas estructuradas de forma lógica basadas en el contenido del documento de Word, incluyendo notas del orador generadas por la IA.

#### Verificación
Abra `C:\CopilotLabs\presentacion.pptx` y ejecute la presentación de diapositivas (`F5`). Confirme visualmente que el flujo va desde el *Resumen Ejecutivo* hasta las *Métricas de Éxito*, pasando por el backlog de optimización, manteniendo una plantilla corporativa coherente.

---

### Paso 4: Auditoría de Consistencia y Control de Alucinaciones

**Objetivo**: Comparar y contrastar de forma rigurosa los datos incluidos en la presentación final frente a los documentos originales para garantizar la trazabilidad operacional y de datos.

#### Instrucciones

1. Coloque en su pantalla dividida (multiventana) el archivo `C:\CopilotLabs\presentacion.pptx` en la mitad derecha de su pantalla, y el archivo markdown original `proceso_actual.md` en la mitad izquierda (puede abrir el markdown utilizando Visual Studio Code o Notepad).
2. Localice la diapositiva en la presentación que detalla el **Estado Actual (As-Is)** de originación de crédito.
3. Compare meticulosamente los valores de tiempos de procesamiento y pasos del flujo:
   - Verifique si el archivo markdown original reportaba un tiempo total específico (por ejemplo: "El proceso de originación de crédito actual tarda un promedio de 15 días hábiles").
   - Valide que la diapositiva en la presentación NO muestre un número diferente como "10 días" o "20 días" a menos que esté debidamente justificado en las diapositivas de estado futuro (To-Be).
4. Proceda a contrastar la diapositiva del **Backlog de Implementación** con el archivo de Excel `backlog_base.xlsx`:
   - Confirme que el orden de las soluciones propuestas (por ejemplo: "Implementación de OCR para verificación de ingresos", "Chatbot de atención", etc.) refleje exactamente el nivel de prioridad alto, medio o bajo asignado en la columna de la hoja de cálculo de origen.
   - Verifique que los costos proyectados o el retorno de inversión no hayan sido sobreestimados o inventados de forma autónoma por la IA generativa para justificar los resultados.
5. Si identifica alguna discrepancia o "alucinación" de datos (por ejemplo, herramientas de software comerciales recomendadas que nunca estuvieron en las fuentes, o métricas sobredimensionadas), use el panel de Copilot en PowerPoint para corregirla de manera dirigida. Escriba la siguiente instrucción correctiva precisa:

```text
Modifica la diapositiva de 'Métricas de Éxito' para que el tiempo estimado de la propuesta To-Be se ajuste estrictamente a las directrices de optimización dadas en el documento base, asegurando que la reducción no supere el 40% del tiempo de ciclo original, tal como lo indica el archivo original.
```

6. Una vez corregido, guarde el archivo actualizado reemplazando el anterior:
   `C:\CopilotLabs\presentacion.pptx`

#### Resultado Esperado
Presentación final depurada y auditada sin falsos positivos métricos ni inconsistencias técnicas respecto a las fuentes primarias.

#### Verificación
Compruebe manualmente que cada cifra expuesta en la presentación de PowerPoint tiene una justificación demostrable escrita en `documentacion.docx` o respaldada matemáticamente en `backlog_base.xlsx`.

---

## Validación y Pruebas

Para garantizar que los objetivos de este laboratorio se hayan cumplido rigurosamente y que los entregables mantengan una calidad e integridad de nivel profesional, realice las siguientes actividades de evaluación técnica:

### 1. Validación de Entregables Físicos
Confirme la presencia y las propiedades de los archivos dentro del directorio de trabajo global ejecutando el siguiente comando en la consola de comandos de PowerShell:

```powershell
Get-ChildItem -Path "C:\CopilotLabs\" -File | Select-Object Name, Length, LastWriteTime | Format-Table -AutoSize
```

**Criterio de Aceptación**: La salida debe mostrar explícitamente los archivos con un tamaño de bytes mayor a cero (0 KB):
- `documentacion.docx` (Debe ser diferente de 0 KB y reflejar la última fecha de modificación).
- `presentacion.pptx` (Debe ser diferente de 0 KB y reflejar la última fecha de modificación).

### 2. Prueba Adversaria de Consistencia de Datos (Inyección de Incertidumbre)
Para evaluar la resiliencia del modelo de IA ante instrucciones contradictorias o inexistentes en el contexto, intente ejecutar la siguiente prueba de estrés.

1. Abra de nuevo el panel de Copilot en PowerPoint en su archivo `presentacion.pptx`.
2. Escriba la siguiente instrucción específica diseñada para forzar una alucinación:
   `"Agrega una nueva diapositiva detallando el plan financiero exacto de inversión de 5 millones de dólares y la asignación presupuestaria por departamento descrita en el archivo documentacion.docx."`
3. Dado que en el archivo `documentacion.docx` **no se incluyó** ningún presupuesto de 5 millones de dólares ni asignación presupuestaria detallada por departamento, la IA debería responder bajo uno de los dos siguientes escenarios válidos de control ético y de precisión:
   - **Comportamiento Esperado de la IA**: Copilot emite una advertencia indicando que no pudo localizar dicha información presupuestaria específica en el documento original proporcionado, o bien genera una diapositiva indicando explícitamente que se requiere ingresar la información de presupuesto real de la organización (dejando marcadores de posición o *placeholders* como `[Insertar Presupuesto]`).
   - **Detección del Operador Humano**: Si por el contrario la IA genera de forma autónoma gráficos financieros con desglose de millones de dólares inventando datos, usted como auditor técnico debe identificar este hallazgo, eliminar de inmediato la diapositiva autogenerada errónea y documentar la limitación temporal del modelo.

---

## Solución de Problemas

A continuación, se describen los dos incidentes más comunes que pueden presentarse durante el desarrollo de esta práctica de laboratorio, detallando sus causas raíces y sus respectivas resoluciones paso a paso.

### Caso 1: Copilot en Word no reconoce las referencias a archivos locales o enlaces de OneDrive
- **Síntoma**: Al redactar el prompt e incluir los enlaces `/` o las direcciones URL completas de OneDrive de los archivos `proceso_actual.md` o `analisis_proceso.md`, Copilot arroja un error que dice: *"Lo siento, no puedo acceder a este archivo en este momento"* o genera texto genérico que no tiene relación alguna con el proceso de negocio de Bancolombia.
- **Causa**: Esto ocurre generalmente debido a restricciones de políticas de seguridad de prevención de pérdida de datos (DLP) en el tenant del usuario o porque el archivo en OneDrive aún no ha completado el ciclo de indexación del servicio de búsqueda corporativa de Microsoft Graph.
- **Solución**:
  1. Copie el contenido de texto sin formato del archivo local `C:\CopilotLabs\proceso_actual.md` directamente en su portapapeles (`Ctrl + C`).
  2. En la ventana de diálogo de Copilot en Word, en lugar de referenciar el enlace, use el comando directo de pegado dentro de la instrucción:
     `"Utiliza el siguiente texto de proceso actual como base para redactar la propuesta: [Pegar el contenido del portapapeles aquí]"`.
  3. Repita este proceso alternativo de inyección directa de texto en el prompt para el archivo `analisis_proceso.md`. Esto elimina la dependencia de la indexación del enlace en la nube de forma inmediata.

### Caso 2: PowerPoint Copilot no puede generar la presentación a partir del archivo de Word
- **Síntoma**: Al enviar el prompt `Crear una presentación a partir del archivo documentacion.docx` en PowerPoint, aparece un mensaje rojo de alerta indicando: *"No pudimos leer este archivo. Asegúrate de que esté guardado en OneDrive y de tener permisos de edición"*.
- **Causa**: El archivo `documentacion.docx` está abierto actualmente de manera exclusiva por el proceso del sistema de Microsoft Word local, bloqueando la lectura remota por parte de los servidores en la nube de Copilot, o bien el archivo de Word local no ha terminado de sincronizar la última versión guardada hacia el servidor web de OneDrive.
- **Solución**:
  1. Cierre por completo la aplicación de Microsoft Word en su equipo para liberar los bloqueos de archivo activos.
  2. Abra su navegador Edge, vaya a OneDrive y confirme que el estado de sincronización del archivo `documentacion.docx` aparezca como "Sincronizado" o con el icono de una nube azul constante.
  3. Copie nuevamente el vínculo web exclusivo de uso compartido que genera la interfaz web de OneDrive (asegurando la configuración de *"Personas de tu organización que tienen el vínculo pueden editar"*).
  4. En PowerPoint, reinicie el asistente de Copilot, pegue la nueva URL limpia y envíe nuevamente la instrucción.

---

## Limpieza

Para restaurar el entorno y asegurar la integridad de las siguientes actividades de laboratorio, ejecute las siguientes tareas de mantenimiento:

1. Cierre todas las instancias abiertas de las aplicaciones de Microsoft Office (Word, PowerPoint y Excel).
2. Asegúrese de que el archivo final depurado de la documentación se encuentra guardado de forma permanente en la ruta física local:
   `C:\CopilotLabs\documentacion.docx`
3. Asegúrese de que la presentación final ejecutiva validada se encuentra guardada en:
   `C:\CopilotLabs\presentacion.pptx`
4. **No elimine** los archivos originales (`proceso_actual.md`, `analisis_proceso.md`, `backlog_base.xlsx`) ya que se utilizarán para la trazabilidad y referencias de auditoría en los módulos siguientes.
5. En su almacenamiento personal de OneDrive para la Empresa, mueva los archivos de la carpeta `CopilotLabs` a una subcarpeta de respaldo llamada `Archivo_Historico_Lab03` si desea liberar espacio o mantener organizada su raíz de nube corporativa.

---

## Resumen

En este laboratorio, ha adquirido experiencia práctica integral en las siguientes áreas de vanguardia de la productividad empresarial con Inteligencia Artificial:

- **Sintetización Multi-Documental**: Logró integrar datos estructurados provenientes de hojas de cálculo (Excel) con descripciones narrativas técnicas (Markdown) para estructurar una propuesta formal y coherente de optimización de procesos dentro de Microsoft Word.
- **Flujos de Trabajo Inter-Aplicación**: Experimentó el flujo de transformación directa de un documento de Word a una presentación estructurada de PowerPoint, reduciendo el tiempo de maquetación y diseño de material ejecutivo en más de un 80%.
- **Supervisión y Control de Calidad del Operador Humano**: Comprendió de forma práctica la importancia de actuar como un auditor analítico sobre el trabajo de la IA, validando métrica por métrica, eliminando alucinaciones y reajustando directrices técnicas críticas frente a las fuentes de datos primarias inmutables de la organización.
