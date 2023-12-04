# Reto 4

En el taller de Santa 🎅, algunos mensajes navideños han sido escritos de manera peculiar: las letras dentro de los paréntesis deben ser leídas al revés

Santa necesita que estos mensajes estén correctamente formateados. Tu tarea es escribir una función que tome una cadena de texto y revierta los caracteres dentro de cada par de paréntesis, eliminando los paréntesis en el mensaje final.

Eso sí, ten en cuenta que pueden existir paréntesis anidados, por lo que debes invertir los caracteres en el orden correcto.

```js
const a = decode('hola (odnum)');
console.log(a); // hola mundo

const b = decode('(olleh) (dlrow)!');
console.log(b); // hello world!

const c = decode('sa(u(cla)atn)s');
console.log(c); // santaclaus

// Paso a paso:
// 1. Invertimos el anidado -> sa(ualcatn)s
// 2. Invertimos el que queda -> santaclaus
```

Notas:

- Las cadenas de entrada siempre estarán bien formadas con paréntesis que coinciden correctamente, no necesitas validarlos.
- En el mensaje final no deben quedar paréntesis.
- El nivel máximo de anidamiento es 2.

# Solución

Para enfrentar éste problema debemos identificar los carácteres que estén dentro de parentesis y los debemos invertir. Cómo también se menciona, pueden existir paréntesis anidados.

Para resolver el problema de los paréntesis anidados, primero debemos resolver los de dentro, para eso, utilizaremos lastIndexOf, el cual capturará la posición del último paréntesis (el de más a la derecha).

Flujo de trabajo del algoritmo:

```js
sa(u(cla)atn)s => sa(ualcatn)s => santaclaus
```

Para lograr ésto, tenemos que contemplar un punto de partida y fin, para poder crear un substring y reemplazar los carácteres.

El punto de inicio es el último paréntesis abierto encontrado, y el fin es el primer paréntesis cerrado luego de nuestro punto de inicio.

```js
const inicio = message.lastIndexOf('(');
const fin = message.indexOf(')', inicio);
```

Una vez tenemos nuestro rango a trabajar, podemos hacer el substring, el cual va desde nuestro punto de inicio + 1 (para eliminar el paréntesis) hasta nuestro punto final.

Realizamos la operación de invertir los carácteres del substring y lo reemplazamos en el mensaje original.

```js
const sub = message.substring(inicio + 1, fin);
const reversed = sub.split('').reverse().join('');
message = message.replace(message.substring(inicio, fin + 1), reversed);
```

Finalmente iteramos mientras la cadena de texto contenga un paréntesis, para ejecutar todas las operaciones que sean necesarias.

```js
while (message.includes('(')) {
	const inicio = message.lastIndexOf('(');
	const fin = message.indexOf(')', inicio);

	const sub = message.substring(inicio + 1, fin);
	const reversed = sub.split('').reverse().join('');
	message = message.replace(message.substring(inicio, fin + 1), reversed);
}

return message;
```

### Solución alternativa

Una solución alternativa que ví en la comunidad de discord de midudev, fue utilizando Regex.

Tiene la misma lógica base, solamente que tiene una mayor complejidad cognitiva, por lo que para el desafío resultaba en un menor puntaje.

```js
const regex = /\(([^()]*)\)/;

while (regex.test(message)) {
	message = message.replace(regex, (match, text) => text.split('').reverse().join(''));
}

return message;
```
