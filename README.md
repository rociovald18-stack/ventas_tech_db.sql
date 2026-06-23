# Ventas_Tech_DB — README

Script SQL para crear y cargar una base de datos de **ventas de tecnología** con un modelo relacional normalizado (dimensiones + tabla de hechos) e integridad referencial.

## Contenido del script
El script genera cuatro tablas:

- **categorias**: catálogo de categorías.
- **clientes**: datos de clientes.
- **productos**: productos asociados a una categoría (FK a `categorias`).
- **ventas**: hechos de ventas que conectan cliente y producto (FK a `clientes` y `productos`).

Incluye:
- **DDL** (CREATE TABLE)
- **Restricciones**:
  - `PRIMARY KEY` en cada tabla
  - `FOREIGN KEY` desde `productos` hacia `categorias` y desde `ventas` hacia `clientes` y `productos`
  - campos `NOT NULL` en columnas críticas (nombre, email, cantidad, precio, fecha, etc.)
  - `activo` como `TINYINT(1)` en SQL Server (0/1) con default `1`
- **DML**:
  - carga inicial de categorías (4)
  - carga de clientes (5, mínimo requerido 3)
  - carga de productos (6, mínimo requerido 5)
  - carga de ventas (10, mínimo requerido 10)
- **Verificación** con `SELECT *` sobre las 4 tablas.

## Requisitos
- Motor: **Microsoft SQL Server**
- Permite ejecutar `CREATE DATABASE` y `USE` en el entorno donde se corre el script.

## Instrucciones de uso
1. Ejecutar el script completo en SQL Server (SQL Server Management Studio o similar).
2. Al finalizar, el script ejecuta:
   - `SELECT * FROM categorias;`
   - `SELECT * FROM clientes;`
   - `SELECT * FROM productos;`
   - `SELECT * FROM ventas;`

## Estructura (resumen)
- `categorias(id_categoria, nombre_categoria, descripcion)`
- `clientes(id_cliente, nombre, email, ciudad, fecha_registro)`
- `productos(id_producto, nombre_producto, id_categoria, precio, stock, activo)`
- `ventas(id_venta, id_cliente, id_producto, cantidad, precio_unitario, fecha_venta)`

## Notas
- El orden de creación y carga está definido para respetar dependencias:
  - primero **categorias** y **clientes**
  - luego **productos**
  - al final **ventas**
- Se eliminan tablas al inicio con `DROP TABLE IF EXISTS` en orden inverso para no romper FKs.

## Consultas sugeridas (para validar)
Probar relaciones mediante JOIN (cuando estés en el módulo de consultas/BI):
- Ventas con nombre del cliente y producto.
- Ventas por categoría.
- Totales por fecha o por cliente.
