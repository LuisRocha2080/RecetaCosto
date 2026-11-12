# Plan de pruebas — RecetaCosto

## Automáticas (Jest)

La lógica de cálculo vive en `src/lib/` y se prueba sin interfaz.

- [ ] Costo con merma 0 % y con merma 20 %.
- [ ] Recálculo en cadena al cambiar un ingrediente usado en varias recetas.
- [ ] Precio sugerido con margen 30 %, 50 % y 0 %.
- [ ] Escalado con cantidades decimales.
- [ ] Borrado bloqueado de ingrediente en uso.

## Manuales en teléfono real

- [ ] Instalación del APK en Android 10 o superior.
- [ ] Uso completo en modo avión.
- [ ] Cierre abrupto de la app y reapertura sin pérdida de datos.
- [ ] Exportación y apertura del archivo en otra app.

## Comandos

```bash
npm test
npx tsc --noEmit
```
