# Modelo de datos — RecetaCosto

Base SQLite local (`expo-sqlite`). Fechas en formato ISO `AAAA-MM-DD`; montos en bolivianos con dos decimales (guardados como enteros en centavos).

## `ingredientes`

Columnas: id, nombre, unidad, precio_compra, cantidad_compra, merma_pct, actualizado_en

## `recetas`

Columnas: id, nombre, porciones, margen_objetivo_pct, precio_venta_actual, notas

## `receta_items`

Columnas: id, receta_id, ingrediente_id, cantidad

## `historial_precios`

Columnas: id, ingrediente_id, fecha, precio_unitario

## Reglas generales

- Cada tabla tiene `id` entero autoincremental.
- Los borrados con historial son **lógicos** (campo `activo`) para no romper reportes.
- Cambios de esquema mediante migraciones numeradas en `src/db/migraciones/`.
