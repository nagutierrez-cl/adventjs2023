# Reto 3

En el taller de Santa, **un elfo travieso** ha estado jugando en la cadena de fabricación de regalos, añadiendo o eliminando un paso no planificado.

Tienes la secuencia original de pasos en la fabricación original y la secuencia modificada modified que puede incluir un paso extra o faltar un paso.

Tu tarea es **escribir una función que identifique y devuelva el primer paso extra que se ha añadido o eliminado en la cadena de fabricación**. Si no hay ninguna diferencia entre las secuencias, devuelve una cadena vacía.

```js
const original = 'abcd';
const modified = 'abcde';
findNaughtyStep(original, modified); // 'e'

const original = 'stepfor';
const modified = 'stepor';
findNaughtyStep(original, modified); // 'f'

const original = 'abcde';
const modified = 'abcde';
findNaughtyStep(original, modified); // ''
```

A tener en cuenta:

- Siempre habrá un paso de diferencia o ninguno.
- La modificación puede ocurrir en cualquier lugar de la cadena.
- La secuencia original puede estar vacía

# Solución

Antes de empezar la solución, debemos tener en cuenta que existen 3 posibles casos:

- No se alteró la cadena original.
- Se agregó un paso extra.
- Se eliminó un paso existente.

Con eso en mente podemos concluir que las cadenas de texto tendrán el mismo tamaño, o un carácter de diferencia, teniendo el carácter extra o faltante en la cadena de texto más grande.

La solución parte con retornar directamente el caso ideal, que ambos sean iguales.

Luego se calcula el maxLength, el cual es el tamaño de la cadena de texto más grande. En base a ese número podemos iterar e ir comparando por posición.

Cómo sabemos que solo habrá una diferencia, la retornaremos inmediatamente, se extrae de la cadena de texto original o modificada, dependiendo de cual haya sido la que tenga más carácteres.

```js
if (original === modified) return '';

const maxLength = Math.max(original.length, modified.length);

for (let i = 0; i < maxLength; i++) {
	if (original[i] !== modified[i]) {
		return maxLength === original.length ? original[i] : modified[i];
	}
}
```
