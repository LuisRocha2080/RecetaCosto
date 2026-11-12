<div align="center">

<img src="docs/assets/logo.svg" alt="Logo de RecetaCosto" width="120" />

# 🥐 RecetaCosto

**Costeo de recetas para panaderías, pastelerías y cocinas: costo por porción, merma y precio de venta sugerido.**

[![Licencia: MIT](https://img.shields.io/badge/licencia-MIT-blue.svg)](LICENSE)
[![CI](https://github.com/LuisRocha2080/RecetaCosto/actions/workflows/ci.yml/badge.svg)](https://github.com/LuisRocha2080/RecetaCosto/actions/workflows/ci.yml)
![Estado](https://img.shields.io/badge/estado-fase%20inicial-orange)
![React Native](https://img.shields.io/badge/React%20Native-Expo-0a7ea4)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178c6)
![SQLite](https://img.shields.io/badge/SQLite-local-003b57)
![Offline](https://img.shields.io/badge/offline-first-2ea44f)
![Costo de licencias](https://img.shields.io/badge/licencias-%240-success)

[Inicio rápido](#-inicio-rápido) · [Características](#-características) · [Arquitectura](#️-arquitectura) · [Roadmap](#️-roadmap) · [Pruebas](#-pruebas) · [Limitaciones](#-lo-que-todavía-no-existe) · [Contribuir](#-contribuir)

</div>

Los insumos suben de precio cada semana y el dueño sigue vendiendo al mismo precio: no sabe cuánto le cuesta realmente cada producto ni qué margen deja. **RecetaCosto** es una app móvil (Android) hecha con React Native + Expo y SQLite local, pensada para panaderías, pastelerías, cafeterías, salteñerías y emprendimientos de comida casera. Funciona sin internet, sin servidores y sin licencias de pago. **Todavía no es una app lista para usar:** hoy el repositorio contiene la especificación, el plan, el modelo de datos, el diseño de pantallas y la base de configuración; el código de la app llega por fases (ver [Roadmap](#️-roadmap) y [Lo que todavía no existe](#-lo-que-todavía-no-existe)).

## 🎬 Vista rápida

> Aún no hay capturas: la app no está implementada. Las pantallas planificadas están descritas en [docs/PANTALLAS.md](docs/PANTALLAS.md) y se agregarán capturas reales al cerrar la primera fase.

Flujo principal:

```
Ingredientes → Receta → Producción → Alertas de margen → Historial de precios → Ficha técnica
```

| Pantalla | Qué muestra |
|---|---|
| Ingredientes | Listado con precio vigente y fecha de la última actualización. |
| Receta | Ingredientes, cantidades, porciones, costo y precio sugerido. |
| Producción | Escala una receta y genera la lista de compras. |
| Alertas de margen | Recetas cuyo margen actual queda bajo el objetivo. |
| Historial de precios | Evolución del precio de un ingrediente. |
| Ficha técnica | Vista previa y exportación a PDF. |

## ✨ Características

| Característica | Detalle |
|---|---|
| Ingredientes con precio | Ingredientes con precio de compra, unidad y porcentaje de merma. |
| Recetas con cantidades | Recetas con cantidades y número de porciones. |
| Costo por porción | Costo por porción que se recalcula solo cuando cambia un ingrediente. |
| Precio de venta | Precio de venta sugerido según el margen objetivo. |
| Escalado de recetas | Escalado de recetas (de 12 a 120 unidades) y lista de compras de la producción. |
| Ficha técnica en | Ficha técnica en PDF y alerta cuando el margen cae bajo el objetivo. |

Todos los datos viven en el dispositivo (SQLite): sin cuentas, sin suscripciones y sin servicios de pago.

## 🏗️ Arquitectura

```mermaid
flowchart LR
    U[Usuario] --> UI[Pantallas Expo Router]
    UI --> L[Lógica y validaciones]
    L --> DB[(SQLite local)]
    L --> X[Exportar CSV / PDF]
    L --> W[Enlaces wa.me y mapas]
```

| Capa | Tecnología |
|---|---|
| App | React Native + Expo (TypeScript) |
| Datos | SQLite local (`expo-sqlite`) |
| Navegación | Expo Router |
| Pruebas | Jest + `tsc --noEmit` |
| Distribución | APK directo / EAS Build local |

**Modelo de datos**

| Tabla | Campos |
|---|---|
| `ingredientes` | id, nombre, unidad, precio_compra, cantidad_compra, merma_pct, actualizado_en |
| `recetas` | id, nombre, porciones, margen_objetivo_pct, precio_venta_actual, notas |
| `receta_items` | id, receta_id, ingrediente_id, cantidad |
| `historial_precios` | id, ingrediente_id, fecha, precio_unitario |

<details>
<summary>Estructura de carpetas</summary>

```
RecetaCosto/
├── app/                 # pantallas (Expo Router)
├── src/
│   ├── components/      # componentes de interfaz
│   ├── db/              # esquema y consultas SQLite
│   └── lib/             # lógica y validaciones
├── docs/                # especificación, roadmap, planificación, datos, pantallas, pruebas, backlog y negocio
├── .github/             # CI, CodeQL, Dependabot, plantillas de issues y PR
├── app.json · package.json · tsconfig.json
└── LICENSE · CHANGELOG.md · CONTRIBUTING.md · SECURITY.md · SUPPORT.md
```

</details>

## 🗺️ Roadmap

1. **Base y navegación:** Proyecto Expo + TypeScript, Esquema SQLite
2. **Ingredientes:** CRUD con merma, Historial de precios
3. **Recetas y costo:** Recetas con items, Costo por porción, Precio sugerido
4. **Producción y alertas:** Escalado, Lista de compras, Alertas de margen
5. **Ficha y piloto:** PDF de ficha técnica, Exportación CSV, APK de prueba con 5 panaderías o pastelerías piloto

Detalle fase por fase en [docs/ROADMAP.md](docs/ROADMAP.md). Documentación completa: [SPEC](docs/SPEC.md) · [PLANNING](docs/PLANNING.md) · [DATOS](docs/DATOS.md) · [PANTALLAS](docs/PANTALLAS.md) · [PRUEBAS](docs/PRUEBAS.md) · [BACKLOG](docs/BACKLOG.md) · [NEGOCIO](docs/NEGOCIO.md).

## 💼 Modelo comercial

| Aspecto | Detalle |
|---|---|
| Cómo se vende | Pago único por negocio o plan anual con soporte de configuración inicial. |
| Precio de partida | Hipótesis a validar: Bs 120–200 pago único. |
| Canal | Panaderías y pastelerías del barrio, cursos de repostería y grupos de emprendedores de comida. |
| Piloto | 5 negocios por 30 días, midiendo cuántos ajustan algún precio de venta tras ver su margen. |

Los precios son hipótesis para validar con clientes reales, no resultados medidos.

## 🚀 Inicio rápido

| Requisito | Versión |
|---|---|
| Node.js | 18+ |
| npm | 9+ |
| Android | Expo Go o emulador |

Clona el repositorio y entra a la carpeta.

```bash
git clone https://github.com/LuisRocha2080/RecetaCosto.git
cd RecetaCosto
```

Cuando exista el código de la app (fase 1 del roadmap), se instalará y arrancará así:

```bash
npm install
npm start        # Expo; escanea el QR con Expo Go
npm run android  # o en el emulador
```

> **No verificado:** `package.json` todavía no declara dependencias, así que `npm install` y `npm start` aún no levantan una app. Los scripts `npm test` y `npm run typecheck` sí están definidos y pasan sin pruebas todavía.

<details>
<summary>Variables de entorno</summary>

RecetaCosto no usa variables de entorno ni claves de API: todo funciona en el dispositivo. `.env.example` queda como plantilla vacía por si se agrega una integración (declarala sin valores reales).

</details>

## 🧪 Pruebas

Casos que la suite debe cubrir (definidos en [docs/PRUEBAS.md](docs/PRUEBAS.md)):

- Costo con merma 0 % y con merma 20 %.
- Recálculo en cadena al cambiar un ingrediente usado en varias recetas.
- Precio sugerido con margen 30 %, 50 % y 0 %.
- Escalado con cantidades decimales.
- Borrado bloqueado de ingrediente en uso.

Hoy `npm test` corre Jest sin pruebas (`--passWithNoTests`) y `npm run typecheck` ejecuta `tsc --noEmit`. El pipeline de CI y el análisis CodeQL corren en GitHub Actions en cada push y PR a `main`.

## 🔒 Seguridad

**Implementado:** no hay cuentas, contraseñas ni servidores; no se envían datos a terceros. El repositorio tiene activados el reporte privado de vulnerabilidades, Dependabot y la protección de secretos, y hay un workflow de CodeQL.

**Avisos importantes:**

- La base SQLite local no está cifrada: quien tenga acceso al dispositivo desbloqueado puede ver los datos.
- No hay copia de respaldo en la nube; si se pierde el teléfono se pierden los datos (la exportación a CSV/PDF está prevista en el diseño, ver [docs/SPEC.md](docs/SPEC.md)).
- Los problemas de seguridad se reportan según [SECURITY.md](SECURITY.md).

## 🚧 Lo que todavía no existe

- **La app en sí:** el repositorio es la base documental y de configuración; las pantallas, la base de datos y la lógica se construyen fase por fase (ver Roadmap).
- Los costos indirectos (gas, luz, alquiler) se ingresan manualmente en la primera versión.
- No gestiona inventario de insumos.
- El precio sugerido es una referencia: no reemplaza el estudio de mercado.
- Sin capturas de pantalla, sin pruebas automáticas reales y sin APK publicado.
- Los precios y el piloto del modelo comercial son hipótesis sin validar.

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Leé la [guía de contribución](CONTRIBUTING.md) y el [código de conducta](CODE_OF_CONDUCT.md) antes de abrir un PR. Para bugs o ideas usá las plantillas de issues; los problemas de seguridad se reportan según la [política de seguridad](SECURITY.md). ¿Dudas? Mirá [SUPPORT.md](SUPPORT.md). Los cambios por versión están en el [CHANGELOG](CHANGELOG.md).

## 📄 Licencia

Distribuido bajo la licencia MIT. Ver [LICENSE](LICENSE).

---

<div align="center">Hecho por <a href="https://github.com/LuisRocha2080">LuisRocha2080</a> · costeo de recetas para panaderías, pastelerías y cocinas con React Native, Expo y SQLite</div>
