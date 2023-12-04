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

El enfoque de ésta solución será tomar la parte de la cadena de texto que esté contenida en un paréntesis, extraerla, modificarla y reemplazarla, de forma reiteratiba hasta que no hayan más paréntesis.

```js
hola (odnum) => hola mundo
```

Para resolver el problema de los paréntesis anidados, primero debemos resolver los de dentro, para eso, utilizaremos lastIndexOf, el cual capturará la posición del
paréntesis de más a la derecha.

Flujo de trabajo del algoritmo:

```js
sa(u(cla)atn)s => sa(ualcatn)s => santaclaus
```

Éste será nuestro punto de partida.

```js
const inicio = message.lastIndexOf('(');
```

Partiremos desde aquí hasta que encontremos el cierre de paréntesis, lo que envuelve a la palabra que debemos invertir. El punto final de nuestra operación lo calculamos con indexOf.

```js
const fin = message.indexOf(')', inicio);
```

Ahora solamente nos queda quitar los paréntesis, invertir los carácteres de dentro y guardar los cambios en la variable.

Para ello creamos un substring, partiendo desde el punto de inicio + 1 (para eliminar el paréntesis) hasta el último carácter antes del paréntesis. Invertimos el substring y reemplazamos el substring completo del paréntesis original con el que se acaba de crear.

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
