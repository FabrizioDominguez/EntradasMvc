# Respuestas de la práctica MVC

## Recorrido observado

| Momento | Archivo o acción responsable |
| --- | --- |
| El navegador solicita el formulario | `EntradasController.Index` (`[HttpGet]`), que crea una `Cotizacion` y devuelve la vista `Index`. |
| Se reciben el nombre y la cantidad | `EntradasController.Calcular` (`[HttpPost]`), mediante el model binding de `Cotizacion`. |
| Se obtiene el descuento de Bs 25 | La propiedad calculada `Cotizacion.Descuento` en `Models/Cotizacion.cs`. |
| Se presenta el total de Bs 225 | `Views/Entradas/Resultado.cshtml`, que muestra `Model.Total`. |

## Preguntas

1. **¿Qué archivo representa el modelo y qué regla de negocio contiene?**  
   `Models/Cotizacion.cs`. Define los datos del cliente y la cantidad, valida sus límites y calcula subtotal, descuento y total. Aplica un descuento del 10 % cuando se cotizan cinco o más entradas.

2. **¿Qué acción recibe los datos del formulario?**  
   `Calcular` en `EntradasController`, mediante una solicitud HTTP POST. Recibe los campos enlazados a un objeto `Cotizacion`.

3. **¿Por qué la vista Resultado no tiene la fórmula del descuento?**  
   Porque la regla de negocio pertenece al modelo. La vista solo presenta el valor calculado, evitando duplicar la fórmula.

4. **¿Qué diferencia hay entre `View(modelo)` en `Index` y `View("Resultado", modelo)` en `Calcular`?**  
   `View(modelo)` busca por convención la vista `Index` de `Views/Entradas` y le entrega el modelo. `View("Resultado", modelo)` selecciona explícitamente la vista `Resultado` y también le entrega ese modelo.

5. **¿Por qué la validación debe existir también en el servidor?**  
   La validación del navegador puede desactivarse o eludirse. El servidor debe volver a validar los datos antes de generar una cotización para no aceptar valores inválidos.
