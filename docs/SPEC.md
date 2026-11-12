# Especificación — RecetaCosto

Requisitos escritos con el patrón EARS («Cuando…, el sistema deberá…»). Cada uno es verificable con una prueba (ver [PRUEBAS.md](PRUEBAS.md)).

## Alcance de la versión 1.0

Costeo de recetas para panaderías, pastelerías y cocinas: costo por porción, merma y precio de venta sugerido. Funciona en un solo dispositivo, sin cuentas de usuario y sin servidor.

## Requisitos funcionales

| ID | Requisito |
|---|---|
| R01 | El sistema deberá calcular el costo unitario de un ingrediente como precio de compra dividido entre la cantidad comprada, ajustado por su merma. |
| R02 | Cuando cambia el precio de un ingrediente, el sistema deberá recalcular el costo de todas las recetas que lo usan. |
| R03 | Cuando cambia el precio de un ingrediente, el sistema deberá guardar el precio anterior en el historial. |
| R04 | El sistema deberá sugerir el precio de venta como costo por porción dividido entre uno menos el margen objetivo. |
| R05 | Si el margen actual de una receta cae por debajo del objetivo, el sistema deberá mostrarla en alertas. |
| R06 | Cuando el usuario escala una receta, el sistema deberá multiplicar las cantidades y listar el total por ingrediente. |
| R07 | Cuando se elimina un ingrediente usado en recetas, el sistema deberá impedirlo e indicar qué recetas lo usan. |
| R08 | El sistema deberá funcionar completo sin conexión. |

## Requisitos no funcionales

| ID | Requisito |
|---|---|
| N01 | La app deberá abrir en menos de 3 segundos en un teléfono Android de gama baja (2 GB de RAM). |
| N02 | Todos los datos deberán almacenarse en SQLite local y no enviarse a ningún servidor. |
| N03 | La interfaz deberá estar en español con montos en bolivianos (Bs) y fechas dd/mm/aaaa. |
| N04 | Los botones táctiles deberán medir al menos 48 dp. |
| N05 | La app deberá operar completa sin conexión a internet. |
| N06 | El costo de licencias de cualquier dependencia deberá ser cero. |

## Fuera de alcance (v1.0)

- Los costos indirectos (gas, luz, alquiler) se ingresan manualmente en la primera versión.
- No gestiona inventario de insumos.
- El precio sugerido es una referencia: no reemplaza el estudio de mercado.

## Criterios de aceptación globales

1. Un usuario nuevo registra su primer dato útil en menos de 5 minutos.
2. Ningún dato se pierde al cerrar la app de forma abrupta.
3. Los totales coinciden con un cálculo manual en los casos de prueba de [PRUEBAS.md](PRUEBAS.md).
