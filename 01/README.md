# Reto 1

En la fábrica de juguetes del Polo Norte, cada juguete tiene un número de identificación único.

Sin embargo, debido a un error en la máquina de juguetes, algunos números se han asignado a más de un juguete.

¡Encuentra el primer número de identificación que se ha repetido, donde la segunda ocurrencia tenga el índice más pequeño!

En otras palabras, si hay más de un número repetido, debes devolver el número cuya segunda ocurrencia aparezca primero en la lista. Si no hay números repetidos, devuelve -1.

```js
const giftIds = [2, 1, 3, 5, 3, 2];
const firstRepeatedId = findFirstRepeated(giftIds);
console.log(firstRepeatedId); // 3
// Aunque el 2 y el 3 se repiten
// el 3 aparece primero por segunda vez

const giftIds2 = [1, 2, 3, 4];
const firstRepeatedId2 = findFirstRepeated(giftIds2);
console.log(firstRepeatedId2); // -1
// Es -1 ya que no se repite ningún número

const giftIds3 = [5, 1, 5, 1];
const firstRepeatedId3 = findFirstRepeated(giftIds3);
console.log(firstRepeatedId3); // 5
```

¡Ojo! Los elfos dicen que esto es una prueba técnica de Google.

# Solución

Se debe encontrar la primera repetición dentro del arreglo, para eso utilizamos un filter retornando todos los elementos repetidos.

```js
const repeated = gifts.filter((gift, i) => gifts.indexOf(gift) !== i);
return repeated.length > 0 ? repeated[0] : -1;
```

Una vez tenemos el listado, retornamos el primero, o en su defecto -1.


### Solución alternativa

Para la solución alternativa utilizamos find, ya que solamente necesitamos el valor del primer elemento repetido, en caso de haberlo. <br/> Ofreció menor puntaje por ops/s.

```js
const repeated = gifts.find((gift, i) => gifts.indexOf(gift) !== i)
return repeated ?? -1
```
