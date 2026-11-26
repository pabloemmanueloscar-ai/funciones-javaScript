# Ejercicios de JavaScript

Este directorio contiene cuatro ejercicios HTML que ejecutan JavaScript en el navegador. Los resultados se muestran con `console.log()` en las herramientas de desarrollador, salvo los datos solicitados al usuario, que se ingresan con `prompt()`.

## Archivos

| Archivo | Propósito | Conceptos principales |
|---|---|---|
| [calculadora.html](./calculadora.html) | Generar la tabla de un número hasta el límite elegido. | Funciones, parámetros, ciclo `for`, validación, `prompt()` |
| [contrseña.html](./contrse%C3%B1a.html) | Validar una contraseña con hasta tres intentos. | Funciones, `return`, condicionales, ciclos, valores `true` y `false` |
| [descuento.html](./descuento.html) | Calcular el precio final de tres productos con distintos descuentos. | Funciones, parámetros, `return`, reutilización |
| [refactorizacion.html](./refactorizacion.html) | Calcular y mostrar ventas mediante funciones reutilizables. | Refactorización, principio DRY, parámetros, retorno y funciones flecha |

## 1. Tabla de multiplicar — `calculadora.html`

### ¿Qué hace?

Solicita un número y un límite de multiplicación. Si ambos son enteros positivos, genera la tabla desde el 1 hasta ese límite.

### ¿Cómo funciona?

- `validarNumero(valor)` comprueba que el dato sea positivo y que el resto de dividirlo por 1 sea cero; así verifica que sea un entero.
- El programa solicita con `prompt()` el número de la tabla y el límite, y convierte ambas entradas a números con `Number()`.
- `generarTabla(numero, limite)` recibe esos valores y utiliza un ciclo `for` para mostrar cada multiplicación.
- Si alguno de los datos no es un entero positivo, muestra un error y no genera la tabla.

Por ejemplo, si se ingresa `5` como número y `5` como límite, la consola muestra desde `5 x 1 = 5` hasta `5 x 5 = 25`.

### Conceptos para reconocer

`numero` y `limite` son parámetros de `generarTabla`; los valores solicitados al usuario son los argumentos. La función muestra cada operación en la consola.

### Validación de datos

La validación también rechaza entradas canceladas, decimales, cero y números negativos. Así se evita iniciar la tabla con valores inválidos.

## 2. Validación de contraseña — `contrseña.html`

### ¿Qué hace?

Solicita una contraseña de hasta tres veces y considera válida cualquier entrada que tenga al menos ocho caracteres. Si se agotan los intentos sin ingresar una válida, informa que se terminaron.

### ¿Cómo funciona?

- `validarPassword(password)` recibe el texto ingresado y utiliza condicionales para decidir si cumple el requisito.
- Si el usuario cancela el cuadro de diálogo, `prompt()` devuelve `null`; la función lo considera inválido.
- Si la contraseña tiene ocho caracteres o más, devuelve `true`. En caso contrario, devuelve `false`.
- El ciclo `while` repite la solicitud mientras queden intentos y no se haya validado una contraseña.
- Después de cada intento se muestra el resultado; si es inválida, se recuerda el requisito de ocho caracteres. Al final se informa si se agotaron los tres intentos.

La función devuelve un valor con `return`; el ciclo usa ese valor para decidir si debe continuar. Esto ejemplifica cómo una función puede validar un dato y comunicar el resultado al resto del programa.

### Alcance de la validación

La única regla implementada es la longitud mínima. No se comprueba si hay números, mayúsculas u otros requisitos.

### Ejemplos de entrada

- Ingresar `abc12345` devuelve `true` porque tiene ocho caracteres; se muestra que la contraseña es válida.
- Ingresar `casa` devuelve `false` porque tiene menos de ocho caracteres; se muestra que no es válida y se permite otro intento.
- Cancelar el cuadro también se considera un intento inválido. Si no se ingresa una contraseña válida en tres intentos, se informa que se agotaron.

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

Calcula el subtotal y el total con descuento de cada producto y muestra el nombre, el subtotal y el total. Cada producto se procesa mediante una llamada a `calcularVenta()`.

### Funciones y responsabilidades

- `calcularSubtotal(precio, cantidad)` multiplica el precio unitario por la cantidad y devuelve el subtotal con `return`.
- `aplicarDescuento(subtotal, porcentajeDescuento)` calcula y devuelve el total luego de aplicar el descuento del 10 %. Está escrita como función flecha.
- `mostrarVenta(producto, subtotal, total)` muestra los datos de una venta en la consola.
- `calcularVenta(producto, precio, cantidad, porcentajeDescuento)` coordina el cálculo: llama a las dos funciones de cálculo y luego a `mostrarVenta()`.

Las variables `subtotal` y `total` de `calcularVenta()` son locales; se utilizan dentro de esa función. Cada función se ocupa de una tarea concreta, lo que hace que el programa sea más fácil de leer y mantener.

### Reutilización y principio DRY

El programa llama a `calcularVenta()` una vez por producto y reutiliza las mismas funciones. Para agregar otro producto, basta con hacer otra llamada con sus datos; no se vuelve a escribir la lógica de cálculo.

`aplicarDescuento()` está escrita como función flecha con llaves y `return` explícito. Así, las dos funciones de cálculo devuelven sus resultados usando `return`, tal como pide la consigna.

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
