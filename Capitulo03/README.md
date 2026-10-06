# Práctica: Construcción y priorización de backlog con Analista y Copilot en Excel combinando hallazgos de analisis_proceso.md con datos operativos de ejemplo

## Metadatos
| Atributo | Detalle |
| :--- | :--- |
| **Duración** | 20 minutos |
| **Complejidad** | Media |
| **Nivel de Bloom** | Aplicar (Apply) |

## Descripción General
En esta práctica de laboratorio, asumirás el rol de un Analista de Procesos de Negocio sénior. Utilizarás **Microsoft 365 Copilot en Excel** para integrar datos cualitativos de riesgos extraídos de un informe previo (`analisis_proceso.md`) con un conjunto de datos operativos y cuantitativos alojados en un libro de Excel (`backlog_base.xlsx`). 

A través de prompts estructurados e iterativos, guiarás al motor de IA para realizar cálculos de impacto, formular un modelo de priorización matemática y construir un backlog estructurado de mejoras operativas listo para la toma de decisiones ejecutivas.

## Objetivos de Aprendizaje
Al finalizar este laboratorio, serás capaz de:
- [ ] Integrar hallazgos cualitativos de inconsistencias con métricas cuantitativas utilizando Copilot en Excel.
- [ ] Diseñar y aplicar fórmulas de impacto operativo mediante instrucciones en lenguaje natural interpretadas por Copilot.
- [ ] Generar un backlog de mejoras priorizado basado en un score ponderado de criticidad operativa.
- [ ] Validar la consistencia de las sugerencias de la IA frente a escenarios con datos conflictivos o incompletos.

## Prerrequisitos
Antes de comenzar, asegúrate de cumplir con lo siguiente:
1. **Conocimientos teóricos**: Familiaridad con el diseño de tablas de Excel y conceptos de priorización de procesos (volumen, tiempo de ciclo y criticidad).
2. **Acceso a Licencias**: Cuenta corporativa activa con licencia de **Microsoft 365 Copilot (Premium/Enterprise)**.
3. **Archivos previos**: Haber completado el análisis cualitativo del laboratorio anterior y contar con los archivos en la ruta unificada de trabajo.

## Entorno de Laboratorio

### Requisitos de Hardware y Software
| Componente | Especificación Técnica Requerida |
| :--- | :--- |
| **Sistema Operativo** | Microsoft Windows 11 Enterprise (Versión 23H2, 64-bit) |
| **Software de Productividad** | Microsoft Excel para Microsoft 365 (Versión 2402 Build 17328.20142, 64-bit) |
| **Navegador Web** | Microsoft Edge (Versión 122.0.2365.92, 64-bit) |
| **Directorio de Trabajo** | `C:\CopilotLabs\` |

> **Nota de Configuración Crítica**: Para que Microsoft 365 Copilot pueda interactuar con el archivo de Excel, este debe estar guardado en formato `.xlsx` y almacenado en una biblioteca de **OneDrive para la Empresa** o **SharePoint Online** asociada a tu cuenta activa de Microsoft 365 con el autoguardado habilitado, o bien trabajar de manera local con la información estructurada estrictamente en formato de **Tabla de Excel** (Insertar > Tabla). En este laboratorio utilizaremos el enfoque de tabla estructurada local con sincronización activa.

### Inicialización del Entorno de Trabajo
Abre una terminal de PowerShell (64-bit) para asegurar que el directorio de trabajo exista y prepara el archivo inicial:

```powershell
## Crear directorio de trabajo unificado si no existe
New-Item -ItemType Directory -Force -Path "C:\CopilotLabs\"

## Crear el archivo de hallazgos previos simulado para el ejercicio
Set-Content -Path "C:\CopilotLabs\analisis_proceso.md" -Value @"
## Análisis de Inconsistencias - Proceso de Solicitud de Crédito
- **H001**: Entrada manual redundante en el canal de Sucursal Física. (Riesgo: Alto)
- **H002**: Falta de validación automática de firmas en documentos PDF. (Riesgo: Crítico)
- **H003**: Cuello de botella en la verificación de historial crediticio externo. (Riesgo: Medio)
- **H004**: Ausencia de notificaciones automatizadas de estado al cliente. (Riesgo: Bajo)
"@
```

---

## Instrucciones Paso a Paso

### Paso 1: Preparación del archivo de Excel y formato de tabla estructurada
**Objetivo**: Crear el archivo de trabajo inicial `backlog_base.xlsx` con los datos cuantitativos y asegurar que Copilot pueda leerlo mediante el formato de tabla nativo de Excel.

1. Abre **Microsoft Excel** (Versión 2402).
2. Copia y pega la siguiente matriz de datos en una nueva hoja de cálculo vacía empezando en la celda **A1**:

| ID_Hallazgo | Proceso | Canal | Volumen_Mensual | Tiempo_Retraso_Horas | Complejidad_Estimada |
| :--- | :--- | :--- | :--- | :--- | :--- |
| H001 | Registro Solicitud | Sucursal | 1200 | 1.5 | Media |
| H002 | Validación Documental | Digital | 4500 | 2.0 | Alta |
| H003 | Análisis de Riesgo | API | 850 | 4.0 | Alta |
| H004 | Notificación Cliente | Omnicanal | 5000 | 0.5 | Baja |

3. Selecciona todo el rango de datos ingresado (`A1:F5`).
4. En la pestaña **Inicio**, haz clic en **Dar formato como tabla** y selecciona cualquier estilo de tu preferencia. Asegúrate de marcar la casilla *"La tabla tiene encabezados"*.
5. Cambia el nombre de la tabla a `TablaBacklog` desde la pestaña de diseño de tabla que aparece al seleccionarla.
6. Guarda el archivo con el nombre exacto `backlog_base.xlsx` en la ruta `C:\CopilotLabs\`.

**Resultado Esperado**: Un archivo de Excel guardado localmente con una tabla estructurada llamada `TablaBacklog` conteniendo 4 filas de datos operativos listos para la IA.

**Verificación**: Al hacer clic dentro de cualquier celda con datos, la pestaña **Diseño de tabla** debe estar visible en la cinta de opciones superior de Excel.

---

### Paso 2: Conectar datos cualitativos con cuantitativos usando Copilot
**Objetivo**: Enriquecer los datos cuantitativos de la tabla incorporando la variable cualitativa "Riesgo_Asociado" mapeada desde el archivo `analisis_proceso.md` utilizando prompts contextuales.

1. En la pestaña **Inicio** de Excel, localiza y haz clic en el botón **Copilot** para abrir el panel lateral de chat de Copilot en Excel.
2. Introduce el siguiente prompt estructurado en la caja de chat de Copilot:

```text
Por favor, analiza la columna 'ID_Hallazgo' en nuestra tabla y añade una nueva columna llamada 'Riesgo_Asociado'. Basándote en el archivo 'C:\CopilotLabs\analisis_proceso.md', asigna los valores de riesgo correspondientes: H001 es 'Alto', H002 es 'Crítico', H003 es 'Medio', H004 es 'Bajo'.
```

*Nota: Dado que Copilot en Excel local no lee directamente el sistema de archivos del disco duro durante una sesión de celda aislada, le estamos proporcionando explícitamente la correspondencia en el prompt para asegurar precisión matemática.*

3. Copilot sugerirá una fórmula o la creación de la columna. Haz clic en **Insertar columna** en la interfaz del panel de Copilot.

**Resultado Esperado**: La tabla ahora cuenta con una séptima columna llamada `Riesgo_Asociado` mapeada correctamente con los valores correspondientes.

**Verificación**: Confirma que la fila del ID `H002` contenga el valor `Crítico` en la celda de la nueva columna.

---

### Paso 3: Calcular el Impacto Operativo y Prioridad con Fórmulas de Copilot
**Objetivo**: Guiar a Copilot para diseñar una métrica compuesta que permita cuantificar la urgencia de cada iniciativa.

1. Escribe el siguiente prompt en el chat de Copilot para agregar la columna de pérdida de capacidad operativa mensual:

```text
Añade una nueva columna llamada 'Impacto_Mensual_Horas' que sea el resultado de multiplicar 'Volumen_Mensual' por 'Tiempo_Retraso_Horas'.
```

2. Revisa la sugerencia de fórmula generada por Copilot (debe ser algo similar a `=[@Volumen_Mensual] * [@Tiempo_Retraso_Horas]`) y haz clic en **Insertar columna**.
3. Ahora, calcula la puntuación de prioridad ponderada. Inserta el siguiente prompt complejo en el chat de Copilot:

```text
Necesito calcular un score de prioridad. Añade una columna llamada 'Score_Prioridad'. La fórmula debe calcularse de la siguiente manera: si 'Riesgo_Asociado' es 'Crítico' asignar 4 puntos, si es 'Alto' 3 puntos, si es 'Medio' 2 puntos, y si es 'Bajo' 1 punto. Multiplica este puntaje resultante por 'Impacto_Mensual_Horas'.
```

4. Haz clic en **Insertar columna** cuando Copilot te proponga la fórmula estructurada basada en condicionales `SI` (o `IFS`).

**Resultado Esperado**: Se habrán creado dos columnas calculadas de forma automatizada por el motor de IA de Copilot en Excel: `Impacto_Mensual_Horas` y `Score_Prioridad`.

**Verificación**: 
- Comprueba que para `H002` el `Impacto_Mensual_Horas` sea `9000` (4500 * 2.0).
- Comprueba que el `Score_Prioridad` para `H002` sea `36000` (9000 * 4 puntos por ser 'Crítico').

---

### Paso 4: Generar y ordenar el Backlog priorizado final
**Objetivo**: Estructurar el backlog final de mejoras priorizadas de mayor a menor impacto, listo para su reporte.

1. Envía la siguiente instrucción al chat de Copilot:

```text
Ordena la tabla completa de manera descendente utilizando la columna 'Score_Prioridad' para colocar las iniciativas de mayor urgencia e impacto en la parte superior.
```

2. Copilot procesará la solicitud y aplicará un ordenamiento nativo sobre la tabla Excel activa.
3. Envía un último prompt para formatear visualmente los hallazgos críticos:

```text
Aplica un formato condicional de color rojo suave a las celdas de la columna 'Score_Prioridad' que tengan un valor superior a 5000.
```

**Resultado Esperado**: La tabla estará ordenada de mayor a menor prioridad (`H002` en primer lugar, seguido de `H001`, `H003` y `H004`). Las celdas críticas tendrán formato condicional rojo aplicado de manera automatizada.

**Verificación**:
La fila superior de la tabla debe comenzar con el ID `H002` y mostrar un Score de prioridad de `36000`.

---

## Validación y Pruebas

Para asegurar la robustez de los procesos automatizados mediante IA y evitar sesgos o interpretaciones erróneas de Copilot en Excel, realizaremos pruebas específicas de validación.

### Caso de Prueba 1: Validación Matemática de Integridad
- **Acción**: Compara manualmente los cálculos de la fila `H001`.
- **Cálculo Esperado**: 
  - `Impacto_Mensual_Horas` = $1200 \times 1.5 = 1800$ horas.
  - `Riesgo_Asociado` = Alto (Equivale a factor multiplicador de 3).
  - `Score_Prioridad` = $1800 \times 3 = 5400$.
- **Criterio de Aceptación**: Los valores en la fila de `H001` deben coincidir exactamente con los números calculados arriba.

### Caso de Prueba Adversario: Inyección de datos corruptos y detección de inconsistencias
Para poner a prueba los límites de la IA (Caso Adversario):
1. Añade manualmente una nueva fila al final de tu tabla en la celda **A6** con los siguientes datos:
   - ID_Hallazgo: `H005`
   - Proceso: `Validación Identidad`
   - Canal: `Digital`
   - Volumen_Mensual: `-500` *(Dato corrupto negativo)*
   - Tiempo_Retraso_Horas: `1.5`
   - Complejidad_Estimada: `Baja`
   - Riesgo_Asociado: `Crítico`
2. Abre el chat de Copilot en Excel y escribe el siguiente prompt de auditoría:

```text
Audita la tabla actual en busca de anomalías lógicas o numéricas en los datos operativos y reporta cualquier inconsistencia que encuentres en un párrafo corto.
```

3. **Comportamiento Esperado de la IA**: Copilot debe alertar que el volumen mensual para el hallazgo `H005` es negativo (`-500`), lo cual es físicamente imposible en métricas operativas de volumen de transacciones de crédito.

**Evidencia de Éxito**: Captura el resultado de la auditoría de Copilot y elimina la fila `H005` para limpiar los datos del backlog definitivo.

---

## Solución de Problemas

Aquí se presentan dos de los problemas más comunes que pueden ocurrir durante este laboratorio y cómo resolverlos:

### Problema 1: El panel de Copilot en Excel aparece deshabilitado (en gris) o indica que el archivo no cumple con los requisitos.
* **Síntoma**: No se puede hacer clic en el botón de Copilot o aparece un mensaje indicando que la IA no está disponible para este archivo de Excel.
* **Causa**: El archivo está guardado localmente en una ubicación tradicional que no soporta coautoría, o bien, los datos dentro del archivo no se han convertido en una Tabla de Excel propiamente formateada.
* **Solución**:
  1. Asegúrate de guardar el archivo dentro de tu directorio sincronizado de **OneDrive para la Empresa**.
  2. Selecciona todos tus datos (`A1:G5`), presiona la combinación de teclas `Ctrl + T` (o `Ctrl + Q`) y haz clic en **Aceptar** para forzar la creación de la tabla de manera explícita.

### Problema 2: Copilot escribe mal la fórmula del Score de Prioridad, devolviendo errores de tipo `#¿NOMBRE?` o `#VALUE!`.
* **Síntoma**: Las celdas del `Score_Prioridad` muestran errores lógicos de Excel.
* **Causa**: El idioma de instalación de Excel difiere del idioma en el que se solicitó la fórmula (por ejemplo, solicitando `IFS` en un Excel configurado en Español que requiere `SI.CONJUNTO`).
* **Solución**: Solicita a Copilot que adapte la fórmula al idioma de la aplicación de Excel local utilizando el siguiente prompt correctivo:
  
```text
Corrige la columna de 'Score_Prioridad'. Genera la fórmula adecuada asegurándote de usar las funciones nativas en Español (como SI o SI.CONJUNTO) que correspondan con la configuración regional de mi aplicación.
```

---

## Limpieza
Para mantener el orden de la estación de trabajo y asegurar la trazabilidad de los artefactos:

1. Guarda el archivo final en Excel asegurándote de que la tabla esté ordenada por prioridad.
2. Cierra la aplicación de Microsoft Excel.
3. Abre una terminal de PowerShell y ejecuta las siguientes instrucciones para consolidar los archivos finales y limpiar temporales:

```powershell
## Verificar que el entregable final se encuentre en la ruta unificada
Get-ChildItem -Path "C:\CopilotLabs\backlog_base.xlsx"

## Limpiar cualquier archivo temporal de Excel que empiece con ~$
Get-ChildItem -Path "C:\CopilotLabs\" -Filter "~$*" -Force | Remove-Item -Force
```

---

## Resumen
En este laboratorio has aprendido a combinar análisis cualitativo y cuantitativo mediante un flujo de trabajo asistido por IA:
1. Diseñaste y estructuraste una tabla de datos operativos compatible con el motor de **Microsoft 365 Copilot**.
2. Integraste de forma contextual hallazgos de severidad cualitativa (`analisis_proceso.md`) con métricas de volumen transaccional mensual en Excel.
3. Utilizaste prompts estructurados para calcular fórmulas complejas de impacto y prioridad ponderada sin necesidad de escribir código manualmente.
4. Ejecutaste pruebas de auditoría y análisis adversarial para validar el comportamiento del asistente ante datos erróneos de entrada.

**Recursos Adicionales**:
- [Documentación oficial de Microsoft 365 Copilot en Excel](https://learn.microsoft.com/es-es/copilot/microsoft-365/copilot-in-excel)
- [Guía de diseño de fórmulas y tablas en Microsoft Excel](https://support.microsoft.com/es-es/excel)

---

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
