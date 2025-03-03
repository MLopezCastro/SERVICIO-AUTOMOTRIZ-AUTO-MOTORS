# SERVICIO-AUTOMOTRIZ-AUTO-MOTORS

# Documentación del Proyecto: Análisis del Impacto de la Pandemia en Auto Motor S

## 1. Corrección de Datos en Excel
Antes de cargar los datos en Power BI, se identificaron y corrigieron **4 errores en la columna Ventas**, donde los valores tenían puntos separadores incorrectos (por ejemplo, `75.633.620` en lugar de `75633620`).

**Acciones realizadas:**
- Se eliminó la puntuación incorrecta en los valores de ventas.
- Se guardaron los archivos corregidos en formato Excel.

## 2. Carga de Datos en Power BI
Se cargaron las siguientes tablas en Power BI desde los archivos Excel:
- **Empleados_Limpio.xlsx**
- **Ventas_Limpio.xlsx**

## 3. Creación de Relaciones en el Modelo de Datos
Power BI detectó automáticamente la relación entre las tablas:
- **Empleados_Limpio** → `Id_Empleado` (Clave primaria)
- **Ventas_Limpio** → `Empleado` (Clave foránea)

Esta relación permite analizar las ventas por cada empleado y evaluar el rendimiento del personal.

## 4. Creación de Columnas y Medidas Claves
Se generaron nuevas columnas calculadas para segmentar los datos en **Pre Pandemia (2016-2019)** y **Post Pandemia (2020)**. Además, se creó una **medida DAX** para calcular la variación porcentual de ventas entre los periodos.

Se corrigieron problemas de valores nulos en la columna `Fecha`, eliminando 15 filas afectadas.

## 5. Visualización de Datos en Power BI
Se crearon los siguientes gráficos y visualizaciones:
- **Ventas Totales por Año** 📊
- **Comparación de Ventas por Periodo Pandemia**
- **Ventas por Empleado y Sede**
- **Estimación de Ventas Ajustadas en 2020**
- **Variación Porcentual de Ventas Pre/Post Pandemia**

## 6. Conclusiones y Respuesta Estratégica
Después de realizar el análisis ajustado, encontramos que **las ventas cayeron un 71%** en 2020 comparado con el promedio anual de los años pre-pandemia (2016-2019). Sin embargo, esta caída varía según la sede, con algunas ubicaciones sufriendo más que otras.

### 1️⃣ ¿Cerrar la empresa?
**No es recomendable.**
- La pandemia fue un evento excepcional y **2020 no es representativo de la tendencia de la empresa a largo plazo**.
- Antes de tomar una decisión drástica, hay que evaluar la recuperación en 2021 y 2022.

### 2️⃣ ¿Quebrar la empresa?
- **No es una opción inmediata, pero la liquidez puede ser un problema.**
- Con una caída del **71% en ingresos**, la empresa necesita revisar su **flujo de caja** y analizar si puede sostener operaciones a corto plazo.
- **Si los costos fijos son demasiado altos**, puede ser necesario **reestructurar** o **cerrar algunas sedes poco rentables**.

### 3️⃣ ¿Buscar inversores y expandirse?
✅ **Es la opción más viable.**
- La empresa **tiene un historial sólido antes de la pandemia**, lo que demuestra que el modelo de negocio funciona.
- **Las ventas externas fueron las menos afectadas**, lo que indica que hay **oportunidades de digitalización** o expansión a clientes que no dependan de una sede física.
- **América Latina sigue siendo un mercado con demanda de servicios automotrices**, y la caída en 2020 podría ser una oportunidad para **invertir a costos más bajos** en otros países.

### 📌 Recomendación Final
1️⃣ **No cerrar la empresa**: Es un año atípico, y la recuperación puede venir en 2021-2022.
2️⃣ **Optimizar costos**: Cerrar sedes no rentables y fortalecer ventas digitales.
3️⃣ **Buscar inversión**: Presentar el caso a inversores mostrando el **potencial de recuperación** y el **éxito previo a la pandemia**.
4️⃣ **Monitorear la recuperación en 2021**: Si sigue cayendo, reconsiderar el plan de negocios.

🔥 **Próximo paso**: Visualizar estos hallazgos en un dashboard final. 

---
📌 *Este documento se irá actualizando con cada nueva acción en Power BI.*



## 1. Corrección de Datos en Excel
Antes de cargar los datos en Power BI, se identificaron y corrigieron **4 errores en la columna Ventas**, donde los valores tenían puntos separadores incorrectos (por ejemplo, `75.633.620` en lugar de `75633620`).

**Acciones realizadas:**
- Se eliminó la puntuación incorrecta en los valores de ventas.
- Se guardaron los archivos corregidos en formato Excel.

## 2. Carga de Datos en Power BI
Se cargaron las siguientes tablas en Power BI desde los archivos Excel:
- **Empleados_Limpio.xlsx**
- **Ventas_Limpio.xlsx**

## 3. Creación de Relaciones en el Modelo de Datos
Power BI detectó automáticamente la relación entre las tablas:
- **Empleados_Limpio** → `Id_Empleado` (Clave primaria)
- **Ventas_Limpio** → `Empleado` (Clave foránea)

Esta relación permite analizar las ventas por cada empleado y evaluar el rendimiento del personal.

## 4. Creación de la Columna `Periodo_Pandemia`
Para clasificar las ventas en períodos antes y después de la pandemia, se creó una columna en Power Query con la siguiente lógica:
- **Pre Pandemia (2016-2019)** para fechas menores a 2020.
- **Post Pandemia (2020)** para fechas desde 2020 en adelante.

## 5. Filtrado y Limpieza de Datos
Se encontraron **15 filas con valores `NULL` en la columna Fecha**. Se aplicó un filtro en Power Query para eliminarlas, asegurando que solo se mantuvieran registros válidos.

## 6. Creación de Medidas DAX
Se desarrollaron medidas en DAX para obtener indicadores clave:

### a) **Total Ventas USD**
Se creó una medida que suma todas las ventas en dólares:
```DAX
Total_Ventas_USD = SUM(Ventas_Limpio_2[Ventas])
```

### b) **Variación de Ventas por Sede**
Se calculó el porcentaje de caída de ventas por sede entre Pre y Post Pandemia:
```DAX
Variación_Ventas_Sede = 
VAR PrePandemia = CALCULATE(SUM(Ventas_Limpio_2[Ventas]), Ventas_Limpio_2[Periodo_Pandemia] = "Pre Pandemia (2016-2019)")
VAR PostPandemia = CALCULATE(SUM(Ventas_Limpio_2[Ventas]), Ventas_Limpio_2[Periodo_Pandemia] = "Post Pandemia (2020)")
RETURN
IF(NOT(ISBLANK(PrePandemia)) && PrePandemia <> 0, (PostPandemia - PrePandemia) / PrePandemia, BLANK())
```

## 7. Creación de Visualizaciones en Power BI
Se diseñaron los siguientes gráficos para analizar el impacto de la pandemia:

### a) **Comparación de Ventas Pre y Post Pandemia**
- Se utilizó un gráfico de columnas para mostrar la caída en ventas.
- Se agregó una medida de ajuste para proyectar el año 2020 completo.

### b) **Ventas por Año y Estimación para 2020**
- Se incluyó una línea de tendencia con ventas anuales y una proyección ajustada de 2020.

### c) **Ventas por Sede**
- Se presentó un gráfico de barras con las ventas por sede en cada período.

### d) **Ventas por Empleado**
- Se utilizó un gráfico de barras horizontales para evaluar el desempeño de los empleados en ventas.

## 8. Consideraciones Finales
- Se detectó que los datos de 2020 solo incluyen registros hasta el **3 de octubre de 2020**.
- Se creó una medida para estimar las ventas anuales ajustadas de 2020 utilizando el promedio mensual.
- Se incorporaron **segmentadores de datos** para permitir filtros dinámicos en los análisis.

📌 *Este documento se irá actualizando con cada nueva acción en Power BI.*

