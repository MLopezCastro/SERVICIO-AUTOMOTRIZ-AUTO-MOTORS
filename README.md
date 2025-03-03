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
- **Ventas_Limpio_2.xlsx**

## 3. Creación de Relaciones en el Modelo de Datos
Power BI detectó automáticamente la relación entre las tablas:
- **Empleados_Limpio** → `Id_Empleado` (Clave primaria)
- **Ventas_Limpio_2** → `Empleado` (Clave foránea)

Esta relación permite analizar las ventas por cada empleado y evaluar el rendimiento del personal.

## 4. Próximo Paso: Creación de Medidas DAX
El siguiente paso consiste en **crear medidas en Power BI** utilizando DAX para calcular los indicadores clave, tales como:
- **Total de Ventas**
- **Cantidad de Productos Vendidos**
- **Comparación de Ventas por Año**

---
📌 *Este documento se irá actualizando con cada nueva acción en Power BI.*

