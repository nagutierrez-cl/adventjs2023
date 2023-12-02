# Reto 2

En el taller de Santa, los elfos tienen una **lista de regalos** que desean fabricar y un conjunto limitado de materiales.

Los regalos son cadenas de texto y los materiales son caracteres. Tu tarea es escribir una función que, dada una lista de regalos y los materiales disponibles, devuelva una **lista de los regalos que se pueden fabricar**.

Un regalo se puede fabricar si contamos con todos los materiales necesarios para fabricarlo.

```js
const gifts = ['tren', 'oso', 'pelota'];
const materials = 'tronesa';

manufacture(gifts, materials); // ["tren", "oso"]
// 'tren' SÍ porque sus letras están en 'tronesa'
// 'oso' SÍ porque sus letras están en 'tronesa'
// 'pelota' NO porque sus letras NO están en 'tronesa'

const gifts = ['juego', 'puzzle'];
const materials = 'jlepuz';

manufacture(gifts, materials); // ["puzzle"]

const gifts = ['libro', 'ps5'];
const materials = 'psli';

manufacture(gifts, materials); // []
```

# Solución

Para solucionar este problema debemos verificar que todas las letras contenidas en los regalos se encuentren en el string materials. <br />
Por lo que primeramente separamos el string de gifts, para trabajar con arrays y que sea algo más cómodo de verificar.

```js
g.split('')
```

Agregamos la condición de que todas las letras (w) se encuentren dentro del string materials.

```js
g.split('').every((w) => materials.includes(w))
```

Finalmente agregamos la iteración de todo el array de gifts, retornando directamente con un filter.

```js
function manufacture(gifts, materials) {
	return gifts.filter((g) => g.split('').every((w) => materials.includes(w)));
}
```
