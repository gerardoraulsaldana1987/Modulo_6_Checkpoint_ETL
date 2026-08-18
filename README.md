# Modulo_6_Checkpoint_ETL
# Checkpoint - Pipeline ETL con Power Query y Lenguaje M

## Descripción

Este proyecto corresponde al checkpoint del Módulo 6 y tiene como objetivo construir un pipeline ETL en Power BI utilizando Power Query y lenguaje M.

Se trabajó con el dataset `Pipeline_ETL_Dataset.xlsx`, compuesto por información de clientes, productos, categorías y ventas de TechStore.

## Transformaciones realizadas

### Dim_Clientes
- Eliminación de registros duplicados utilizando `id_cliente` como clave.
- Reemplazo de valores nulos en `email` y `ciudad` por `"sin datos"`.
- Conversión de `fecha_registro` al tipo Fecha.
- Resultado final: 11 clientes únicos.

Se conservaron los clientes con email o ciudad faltantes porque estos campos no forman parte de la clave del modelo y eliminarlos hubiera provocado pérdida innecesaria de información.

### Dim_Productos
- Eliminación de duplicados utilizando `id_producto`.
- Reemplazo de categoría nula por `"Sin Categoría"`.
- Corrección de tipos de datos.
- Imputación del precio faltante del producto 109 con un valor de 130.
- Resultado final: 12 productos únicos.

El precio 130 no fue asignado arbitrariamente. Se verificaron las cinco ventas históricas correspondientes al producto 109 y todas registraban un `precio_unitario` de 130.

### Fact_Ventas
- Verificación de calidad de datos.
- Corrección de tipos de datos.
- `fecha_venta` convertida al tipo Fecha.
- 50 transacciones sin errores ni valores nulos.

### Dim_Categorias
- Verificación de tipos y calidad de datos.
- 4 categorías únicas sin errores ni valores nulos.

### Fact_Ventas_Enriquecida
Se realizó un Merge de tipo Left Outer entre `Fact_Ventas` y `Dim_Productos` utilizando `id_producto` como clave.

Se incorporaron:
- `nombre_producto`
- `categoria`

El resultado conserva las 50 transacciones originales y permite enriquecer el análisis de ventas con información descriptiva de los productos.

## Documentación en Lenguaje M

Se agregaron comentarios técnicos en el Editor Avanzado de Power Query para documentar las principales decisiones de transformación, incluyendo:

- Eliminación de duplicados.
- Tratamiento de valores nulos.
- Conservación de registros relevantes.
- Imputación del precio faltante basada en datos históricos.

## Resultado final

El modelo contiene las siguientes consultas:

- `Dim_Clientes`: 11 filas
- `Dim_Productos`: 12 filas
- `Dim_Categorias`: 4 filas
- `Fact_Ventas`: 50 filas
- `Fact_Ventas_Enriquecida`: 50 filas

El pipeline queda limpio, tipado y documentado para continuar con la construcción del modelo analítico en Power BI.

## Entregable

`Pipeline_ETL_Saldana_Gerardo.pbix`Checkpoint - Pipeline ETL con Power Query y lenguaje M
