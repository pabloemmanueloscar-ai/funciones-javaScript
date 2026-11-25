# Ejercicios de JavaScript

Este directorio contiene cuatro ejercicios HTML que ejecutan JavaScript en el navegador. Los resultados se muestran con `console.log()` en las herramientas de desarrollador, salvo los datos solicitados al usuario, que se ingresan con `prompt()`.

## Archivos

| Archivo | Propósito | Conceptos principales |
|---|---|---|
| [calculadora.html](./calculadora.html) | Mostrar tablas de multiplicar de números ingresados por el usuario. | Funciones, parámetros, ciclos `while`, `prompt()` |
| [contrseña.html](./contrse%C3%B1a.html) | Validar una contraseña con hasta tres intentos. | Funciones, `return`, condicionales, ciclos, valores `true` y `false` |
| [descuento.html](./descuento.html) | Calcular el precio final de tres productos con distintos descuentos. | Funciones, parámetros, `return`, reutilización |
| [refactorizacion.html](./refactorizacion.html) | Calcular y mostrar ventas mediante funciones reutilizables. | Refactorización, principio DRY, parámetros, retorno y funciones flecha |

## 1. Tabla de multiplicar — `calculadora.html`

### ¿Qué hace?

Primero pregunta cuántos números se quieren procesar. Luego solicita cada número y muestra su tabla de multiplicar desde el 1 hasta el 10.

### ¿Cómo funciona?

- `pedirNumeros()` solicita la cantidad de números y controla cuántas veces se repite el proceso.
- En cada repetición pide un número y llama a `tablaMultiplicar(num)`.
- `tablaMultiplicar(num)` recibe ese número y usa un ciclo `while` para mostrar las diez multiplicaciones.
- El ciclo incrementa `i` en cada vuelta y termina cuando `i` supera 10.

Por ejemplo, si se ingresa `7`, la consola muestra operaciones desde `7 x 1 = 7` hasta `7 x 10 = 70`.

Si se ingresa `2` como cantidad y luego los números `7` y `4`, el programa muestra dos tablas: primero la del 7 y después la del 4.

### Conceptos para reconocer

`num` es un parámetro de `tablaMultiplicar`; el valor ingresado por el usuario es el argumento. En este ejercicio la función muestra cada resultado, pero no devuelve un resultado con `return`.

### Detalle a mejorar

`limite` y `num` se asignan sin declararse con `let` o `const`, por lo que pasan a ser variables globales. También el documento indica `lang="en"` aunque los mensajes están en español. Son mejoras posibles, no cambios realizados en este ejercicio.

## 2. Validación de contraseña — `contrseña.html`

### ¿Qué hace?

Solicita una contraseña de hasta tres veces y considera válida cualquier entrada que tenga al menos ocho caracteres. Si se agotan los intentos sin ingresar una válida, informa que se terminaron.

### ¿Cómo funciona?

- `validarPassword(password)` recibe el texto ingresado.
- Si el usuario cancela el cuadro de diálogo, `prompt()` devuelve `null`; la función lo considera inválido.
- Si la contraseña tiene ocho caracteres o más, devuelve `true`. En caso contrario, devuelve `false`.
- El ciclo `while` repite la solicitud mientras queden intentos y no se haya validado una contraseña.
- Después de cada intento se muestra el resultado. Al final se informa si se agotaron los tres intentos.

La función devuelve un valor con `return`; el ciclo usa ese valor para decidir si debe continuar. Esto ejemplifica cómo una función puede validar un dato y comunicar el resultado al resto del programa.

### Alcance de la validación

La única regla implementada es la longitud mínima. No se comprueba si hay números, mayúsculas u otros requisitos.

### Ejemplos de entrada

- Ingresar `abc12345` devuelve `true` porque tiene ocho caracteres; se muestra que la contraseña es válida.
- Ingresar `casa` devuelve `false` porque tiene menos de ocho caracteres; se muestra que no es válida y se permite otro intento.
- Cancelar el cuadro también se considera un intento inválido. Si no se ingresa una contraseña válida en tres intentos, se informa que se agotaron.

### Detalle a revisar

El archivo contiene etiquetas HTML duplicadas y algunas etiquetas iniciales incompletas antes de la estructura principal del documento. Los navegadores pueden intentar corregirlas al mostrar la página, pero convendría limpiar esa estructura si se trabaja luego en la validez del HTML.

## 3. Cálculo de descuentos — `descuento.html`

### ¿Qué hace?

Calcula el precio final de tres productos a partir de su precio original y un porcentaje de descuento, y muestra los datos de cada cálculo.

### ¿Cómo funciona?

- `calcularDescuento(precioOriginal, porcentajeDescuento)` calcula el importe descontado, lo resta del precio original y devuelve el precio final con `return`.
- `mostrarPrecio(precioOriginal, porcentajeDescuento, precioFinal)` muestra el precio inicial, el porcentaje aplicado y el precio final.
- El programa llama a esas funciones para cada producto; así reutiliza la misma lógica sin repetir las operaciones matemáticas.

### Resultados

| Precio original | Descuento | Precio final |
|---:|---:|---:|
| $20.000 | 15 % | $17.000 |
| $15.000 | 10 % | $13.500 |
| $10.000 | 5 % | $9.500 |

Las funciones reciben datos mediante parámetros. `calcularDescuento()` devuelve un valor para que el programa pueda guardarlo y pasárselo a `mostrarPrecio()`.

## 4. Refactorización de ventas — `refactorizacion.html`

### ¿Qué hace?

Calcula el subtotal y el total con descuento de cada producto y muestra el nombre, el subtotal y el total. Los productos están organizados en una lista llamada `ventas`.

### Funciones y responsabilidades

- `calcularSubtotal(precio, cantidad)` multiplica el precio unitario por la cantidad y devuelve el subtotal con `return`.
- `aplicarDescuento(subtotal, porcentajeDescuento)` calcula y devuelve el total luego de aplicar el descuento del 10 %. Está escrita como función flecha.
- `mostrarVenta(producto, subtotal, total)` muestra los datos de una venta en la consola.
- `calcularVenta(producto, precio, cantidad, porcentajeDescuento)` coordina el cálculo: llama a las dos funciones de cálculo y luego a `mostrarVenta()`.

Las variables `subtotal` y `total` de `calcularVenta()` son locales; se utilizan dentro de esa función. Cada función se ocupa de una tarea concreta, lo que hace que el programa sea más fácil de leer y mantener.

### Reutilización y principio DRY

La lista contiene los datos de cada producto y `forEach()` recorre sus elementos. Para agregar otro producto basta con añadir sus datos a la lista: se reutilizan las mismas funciones sin duplicar la lógica de cálculo.

`aplicarDescuento()` utiliza retorno implícito: al ser una función flecha con una sola expresión, JavaScript devuelve el resultado automáticamente. Si la consigna exige la palabra `return` escrita de forma explícita en ambas funciones de cálculo, se puede escribir esa función flecha con llaves y `return`.

### Resultados

| Producto | Precio unitario | Cantidad | Subtotal | Total con 10 % de descuento |
|---|---:|---:|---:|---:|
| Teclado | $25.000 | 2 | $50.000 | $45.000 |
| Mouse | $15.000 | 3 | $45.000 | $40.500 |
| Auriculares | $20.000 | 1 | $20.000 | $18.000 |

Los valores del teclado y del mouse conservan los resultados originales. Los auriculares son el tercer producto agregado como desafío adicional.

## Cómo ejecutar los ejercicios

1. Abrir el archivo HTML deseado en un navegador.
2. Abrir las herramientas de desarrollador del navegador, por ejemplo, con `F12`.
3. Seleccionar la pestaña **Consola** para ver los resultados de `console.log()`.
4. En los ejercicios que usan `prompt()`, responder los cuadros de diálogo que aparecen.

Los ejercicios están pensados para practicar JavaScript y funciones; no generan una interfaz visual con los resultados.
