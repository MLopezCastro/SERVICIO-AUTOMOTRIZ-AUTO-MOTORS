
# Documentación del Proyecto: Análisis del Impacto de la Pandemia en Auto Motors

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

## 4. Creación de la Columna de Periodo Pandemia
Se creó una nueva columna calculada en Power Query para diferenciar las ventas **Pre Pandemia (2016-2019)** y **Post Pandemia (2020)**:
```M
Periodo_Pandemia = 
IF( YEAR(Ventas_Limpio[Fecha]) < 2020, 
    "Pre Pandemia (2016-2019)", 
    "Post Pandemia (2020)"
)
```

Se identificaron **15 registros con fechas nulas**, los cuales fueron eliminados por falta de información válida.

## 5. Creación de Medidas DAX
Se implementaron las siguientes medidas en Power BI:

### Total Ventas en USD
```DAX
Total_Ventas_USD = SUM(Ventas_Limpio_2[Ventas])
```

### Variación de Ventas por Sede
```DAX
Variación_Ventas_Sede = 
VAR PrePandemia = 
    CALCULATE(SUM(Ventas_Limpio_2[Total_Ventas_USD]), 
        Ventas_Limpio_2[Periodo_Pandemia] = "Pre Pandemia (2016-2019)")
VAR PostPandemia = 
    CALCULATE(SUM(Ventas_Limpio_2[Total_Ventas_USD]), 
        Ventas_Limpio_2[Periodo_Pandemia] = "Post Pandemia (2020)")
VAR Variacion = 
    IF(NOT(ISBLANK(PrePandemia)) && PrePandemia <> 0, 
       DIVIDE(PostPandemia - PrePandemia, PrePandemia), BLANK())
RETURN
    FORMAT(Variacion, "0.00%")
```

### Promedio de Ventas Anuales Pre Pandemia
```DAX
Promedio_Anual_Pre_Pandemia = 
VAR VentasPrePandemia = 
    CALCULATE(SUM(Ventas_Limpio_2[Total_Ventas_USD]), 
        Ventas_Limpio_2[Periodo_Pandemia] = "Pre Pandemia (2016-2019)")
VAR AñosDisponibles = DISTINCTCOUNT(Ventas_Limpio_2[Fecha].[Year])
RETURN
    DIVIDE(VentasPrePandemia, AñosDisponibles)
```

### Estimación de Ventas 2020 Ajustadas a 12 meses
```DAX
Ventas_2020_Ajustadas = 
VAR Ventas2020 = 
    CALCULATE(SUM(Ventas_Limpio_2[Total_Ventas_USD]), 
        Ventas_Limpio_2[Periodo_Pandemia] = "Post Pandemia (2020)")
VAR MesesDisponibles = DISTINCTCOUNT(Ventas_Limpio_2[Fecha].[Month])
RETURN
    DIVIDE(Ventas2020, MesesDisponibles) * 12
```

## 6. Análisis de Impacto de la Pandemia
Tras el análisis de los datos, se identificaron los siguientes hallazgos clave:

1. **Las ventas totales cayeron un 71% en 2020 respecto al período pre-pandemia** (ajustado a 12 meses).
2. **Grandes Flotas fue la sede con menor caída (-84%) y Ventas Externas la más afectada (-96%)**.
3. **El 2020 sólo incluye datos hasta octubre**, lo que infló la caída si se comparaba directamente con cuatro años previos.
4. **El ajuste de ventas 2020 a 12 meses sigue mostrando una caída significativa, pero menor al 94% calculado inicialmente.**

## 7. Respuestas Estratégicas
Dado el impacto de la pandemia en las ventas de Auto Motor S, se proponen tres posibles estrategias:

- **Buscar financiamiento/inversores** para aprovechar la recuperación post-pandemia y expandirse a otros mercados.
- **Focalizarse en la sede de Grandes Flotas**, que demostró mayor resiliencia a la crisis.
- **No tomar decisiones drásticas de cierre inmediato**, dado que el 2020 fue un año atípico con ventas truncadas.

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








