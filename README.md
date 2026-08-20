# BlockCalc 🧱

Calculadora de bloques para paredes. Permite ingresar medidas manualmente o dibujar un boceto de la pared (incluyendo huecos de puertas y ventanas) para estimar cuántos bloques se necesitan.

## Qué hace

- **Modo Medidas**: ingresa ancho, alto, tipo de bloque (presets o personalizado), huecos de puertas/ventanas, % de desperdicio y grosor de junta de mortero. Calcula el número exacto de bloques necesarios.
- **Modo Boceto**: dibuja la pared directamente sobre una cuadrícula (con escala calibrable), marca los huecos, y obtén el mismo cálculo sin medir a mano.
- **Estimado de materiales (premium)**: bolsas de cemento, arena y varilla aproximadas según el área neta de la pared.
- **Guardar proyectos (premium)**: guarda cálculos anteriores con nombre de proyecto para consultarlos después.

## Modelo freemium

| | Gratis | Premium |
|---|---|---|
| Cálculos por día | 3 | Ilimitados |
| Cálculo de bloques | ✅ | ✅ |
| Estimado de cemento / arena / varilla | ❌ | ✅ |
| Guardar proyectos | ❌ | ✅ |

El límite diario y el estado del plan se guardan de forma persistente (no se resetean al recargar la página). El botón "simular upgrade a premium" es solo para probar el flujo del producto — en una versión real se conectaría a un procesador de pagos (ej. Stripe).

## Cómo se calcula

```
área bruta de la pared = ancho × alto
área neta = área bruta − suma de áreas de huecos
área por bloque = (largo_bloque + junta) × (alto_bloque + junta)
bloques = ceil( (área neta / área por bloque) × (1 + % desperdicio) )
```

En modo boceto, el área se calcula a partir de los rectángulos dibujados, convertidos de píxeles a metros usando la escala que el usuario calibra (metros por cuadro de cuadrícula).

Los estimados de cemento, arena y varilla usan reglas de dedo genéricas por m² de pared — son referenciales, no sustituyen el cálculo de un maestro de obra o ingeniero para una cotización final.

## Stack técnico

- HTML + CSS + JavaScript vanilla, un solo archivo (`calculadora-bloques.html`)
- Sin dependencias externas ni build step
- Persistencia de datos vía `window.storage` (catálogo de plan, contador de uso diario, proyectos guardados)
- Canvas API para el modo boceto

## Estado del proyecto

Prototipo funcional para validación. Próximos pasos sugeridos antes de lanzar:
- [ ] Validar con usuarios reales (contratistas, ferreterías, autoconstructores) si pagarían y cuánto
- [ ] Exportar cotización en PDF con logo del usuario
- [ ] Precios de materiales por región/país
- [ ] Integración de pago real (Stripe u otro procesador)
- [ ] Evaluar modelo B2B (venderlo embebido a ferreterías) en vez de B2C directo

## Notas de negocio

Este prototipo nació como ejercicio de exploración de micro SaaS. La conclusión de la validación inicial: como herramienta aislada de cálculo, compite contra calculadoras gratis ya posicionadas en SEO (ej. Omni Calculator) y el patrón de uso (pocas veces al mes) encaja mal con suscripción recurrente. Las rutas con más potencial identificadas:

1. **B2B**: vender la calculadora embebida con marca blanca a ferreterías/distribuidores de materiales, que sí tienen presupuesto de marketing/tecnología.
2. **Kit completo**: combinarla con otras calculadoras de construcción (pintura, techo, cerámica) para justificar una suscripción de uso más frecuente.
3. **Pago por cotización**: cobro único por generar un PDF de cotización con marca propia, en vez de suscripción mensual.
