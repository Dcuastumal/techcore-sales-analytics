# TechCore Sales Analytics

![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=000)
![Python](https://img.shields.io/badge/Python-Data%20Modeling-3776AB?logo=python&logoColor=fff)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Processing-150458?logo=pandas&logoColor=fff)
![Status](https://img.shields.io/badge/Status-Completed-2EA44F)

Proyecto integral de analítica comercial desarrollado para **TechCore**, una cadena nacional de tiendas especializada en la venta de computadores. La solución transforma datos transaccionales sin procesar en un modelo relacional validado y un dashboard interactivo de Power BI orientado a la toma de decisiones.

El proyecto cubre el flujo analítico completo: **limpieza y transformación de datos, modelado relacional con Python, validación de integridad, creación de medidas DAX y visualización ejecutiva en Power BI**.

## Objetivos del proyecto

- Centralizar y depurar la información histórica de ventas de TechCore.
- Estandarizar ciudades, sucursales, productos, métodos de pago y datos de clientes.
- Diseñar un modelo relacional con claves primarias y foráneas válidas.
- Validar la consistencia de importes, relaciones y registros.
- Crear indicadores comerciales mediante DAX.
- Desarrollar un dashboard interactivo para analizar ventas por ciudad, marca, periodo, método de pago y edad del cliente.

## Estructura del repositorio

```text
techcore-sales-analytics/
├── Avance_1/
│   ├── Avance_1_Limpieza_Transformacion.pbix
│   ├── ventas.csv
│   └── ventasTransformed.csv
├── Avance_2/
│   ├── Avance_2_Modelo_Relacional.ipynb
│   ├── Avance_2_Modelo_Relacional.pbix
│   ├── modeloVentas.xlsx
│   └── modelo_relacional.png
├── Avance_3/
│   └── Avance_3_Dashboard_Interactivo.pbix
├── LICENSE
└── README.md
```

### Guía de carpetas

| Carpeta | Contenido | Propósito |
|---|---|---|
| `Avance_1` | Dataset original, dataset transformado y archivo PBIX | Limpieza, estandarización y transformación reproducible con Power Query. |
| `Avance_2` | Notebook, modelo Excel, diagrama relacional y archivo PBIX | Construcción y validación del modelo relacional con Python y Power BI. |
| `Avance_3` | Dashboard final en Power BI | KPIs, medidas DAX, filtros, jerarquías y visualizaciones interactivas. |

## Desarrollo por etapas

### 1. Limpieza y transformación

El archivo original se procesó con Power Query para garantizar consistencia y calidad antes del análisis.

Principales transformaciones:

- Corrección de tipos de datos para fechas, horas, cantidades y valores monetarios.
- Eliminación de registros duplicados.
- Tratamiento de valores vacíos o no especificados.
- Normalización de nombres de ciudades, sucursales, productos y categorías.
- Estandarización de métodos de pago.
- Corrección de caracteres y tildes en direcciones de correo electrónico.
- Creación de campos temporales auxiliares como año y mes.
- Exportación del resultado como `ventasTransformed.csv`.

### 2. Modelo relacional

El dataset transformado se procesó con **Python y pandas** para convertir la tabla transaccional en un modelo relacional preparado para Power BI.

#### Tablas generadas

| Tabla | Registros | Función |
|---|---:|---|
| `Facturas` | 30,000 | Cabecera de cada venta. |
| `DetalleFacturas` | 60,059 | Productos incluidos en cada factura. |
| `Productos` | 40 | Catálogo único de productos y precios. |
| `Clientes` | 17,453 | Información demográfica y de contacto. |
| `Sucursales` | 6 | Tiendas asociadas a cada ciudad. |
| `Ciudades` | 4 | Catálogo geográfico de ciudades. |
| `Vendedores` | 30 | Catálogo de vendedores. |

#### Relaciones del modelo

- `Ciudades[CiudadID]` → `Sucursales[CiudadID]`
- `Sucursales[SucursalID]` → `Facturas[SucursalID]`
- `Clientes[ClienteID]` → `Facturas[ClienteID]`
- `Vendedores[VendedorID]` → `Facturas[VendedorID]`
- `Facturas[FacturaID]` → `DetalleFacturas[FacturaID]`
- `Productos[ProductoID]` → `DetalleFacturas[ProductoID]`

Todas las claves primarias fueron verificadas como únicas y no nulas. Las seis relaciones fueron validadas sin registros huérfanos. También se comprobó que los subtotales y totales de las facturas fueran consistentes.

El resultado se exportó a `modeloVentas.xlsx`, que contiene las tablas del modelo, reportes de control y validaciones de integridad.

### 3. Dashboard interactivo

El modelo relacional fue importado en Power BI Desktop para construir el dashboard ejecutivo `Avance_3_Dashboard_Interactivo.pbix`.

#### Indicadores DAX

| KPI | Definición |
|---|---|
| **Ventas Totales** | Suma de los subtotales aplicando el descuento correspondiente a cada factura. |
| **Ticket Promedio** | Ventas totales divididas entre la cantidad de facturas únicas. |
| **Productos Vendidos** | Suma total de unidades vendidas. |
| **Cantidad Facturas** | Conteo distinto de facturas. |
| **% Participación Ciudad** | Participación de cada ciudad sobre las ventas totales. |
| **% Venta Neta** | Proporción de ventas después de descuentos sobre el subtotal bruto. |

> **Nota:** el dataset no contiene costos de adquisición ni costos operativos. Por esta razón, no es posible calcular un margen de utilidad real; `% Venta Neta` se utiliza como una aproximación transparente basada en descuentos.

#### Visualizaciones implementadas

- Tarjetas con ventas totales, ticket promedio, productos vendidos y cantidad de facturas.
- Gráfico de barras con ventas por marca.
- Línea temporal con la evolución mensual de las ventas.
- Mapa geográfico con ventas y participación por ciudad.
- Página adicional con conclusiones e insights estratégicos.

#### Segmentadores dinámicos

- Ciudad.
- Marca del producto.
- Método de pago.
- Rango de fechas.
- Rango de edad del cliente.

#### Jerarquías

- **Fecha:** Año → Mes → Día.
- **Ubicación:** Ciudad → Sucursal.

## Principales resultados

- **Lenovo** lidera las ventas netas y el volumen total de unidades.
- **HP Spectre x360** es el producto con mayor cantidad de unidades vendidas.
- Las claves primarias y foráneas presentan integridad completa en el modelo generado.
- Los importes calculados en el detalle coinciden con los totales registrados en las facturas.
- El dashboard permite comparar el desempeño por ciudad, marca, periodo, método de pago y rango de edad.

## Tecnologías utilizadas

- **Power BI Desktop** — Power Query, modelado, DAX y dashboard.
- **Python** — procesamiento y validación del modelo relacional.
- **pandas** — transformación y generación de tablas.
- **NumPy** — validaciones numéricas.
- **Matplotlib** — diagrama del modelo relacional.
- **OpenPyXL** — exportación del modelo a Excel.
- **Jupyter Notebook / VS Code** — desarrollo reproducible y documentación.
- **Git y GitHub** — control de versiones y publicación.

## Cómo ejecutar el proyecto

### Requisitos

- Python 3.10 o superior.
- Power BI Desktop.
- Jupyter Notebook o la extensión Jupyter para VS Code.

Instala las dependencias de Python:

```bash
pip install pandas numpy matplotlib openpyxl jupyter
```

### Ejecución

1. Clona el repositorio:

   ```bash
   git clone https://github.com/Dcuastumal/techcore-sales-analytics.git
   cd techcore-sales-analytics
   ```

2. Abre `Avance_2/Avance_2_Modelo_Relacional.ipynb` y ejecuta las celdas en orden para reproducir el modelo relacional.

3. Verifica la generación de:

   - `Avance_2/modeloVentas.xlsx`
   - `Avance_2/modelo_relacional.png`

4. Abre `Avance_3/Avance_3_Dashboard_Interactivo.pbix` con Power BI Desktop para explorar el dashboard final.

> Los archivos `.pbix` no se visualizan directamente desde GitHub; deben descargarse y abrirse con Power BI Desktop.

## Flujo del proyecto

```mermaid
flowchart LR
    A[ventas.csv] --> B[Power Query]
    B --> C[ventasTransformed.csv]
    C --> D[Python y pandas]
    D --> E[modeloVentas.xlsx]
    E --> F[Modelo Power BI]
    F --> G[Dashboard interactivo]
```

## Autor

**David Cuastumal**  
Proyecto desarrollado como parte del Módulo 3 del programa de Data Science de SoyHenry.

## Licencia

Este proyecto se distribuye bajo los términos definidos en el archivo [LICENSE](LICENSE).
