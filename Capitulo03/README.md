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

