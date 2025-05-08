# 🍬 Dulce y truco de programacion 🍬

Tips y Trucos de programacion en diferentes lenguajes para mejorar como dev.
Importante: De momento voy agregando trucos con forme subo los videos a la plataforma de tiktok 🤙

* [Trucos en C++](#trucos-en-c)
* [Trucos en Java](#trucos-en-java)
* [Trucos en JavaScript](#trucos-en-javascript)
* [Trucos en Python](#trucos-en-python)
* [Trucos en Kotlin](#trucos-en-kotlin)
* [Trucos en Golang](#trucos-en-golang)
* [Trucos en Typescript](#trucos-en-typescript)
* [Trucos en Swift](#trucos-en-swift)

---------------------------------------

## Trucos en C++

### Bucles `for` basados en rangos

Un bucle for basado en rango es una versión mejorada del bucle for tradicional y se introdujo en C++ 11.

La sintaxis de un bucle for basado en rango es:

`for( declaracion_rango : expresion_rango )`


Como ejemplo, puede recorrer una matriz de números usando un bucle for basado en rango de la siguiente manera:


``` C++
int numeros[] = {1,2,3,4,5};
for (auto numero: numeros){
    cout << numero << endl;
}
```

O puede recorrer los caracteres en una cadena de manera similar usando un bucle for basado en rango:

``` C++
string nombre = "EllaNoTeAma";
for (auto letra: nombre){
    cout << letra << endl;
}
```

### Usar Auto para omitir el tipo de datos de una variable

Podemos omitir el tipo de datos de una variable utilizando la palabra AUTO en C++ apartir de la version 11. 
Esto es extremadamente útil cuando necesita declarar una variable en tiempo de ejecución, por ejemplo, cuando usamos iteradores.

Como ejemplo, los tipos de datos de las siguientes variables se declaran durante el tiempo de ejecución.

``` C++
auto a = 'Hola';
auto t = true;
auto x = 1;
auto y = 2.0;
```


---------------------------------------

## 🔥 Trucosde Programación en React.js

### 1️⃣ **Usar `useMemo` para evitar cálculos costosos en cada render**

Cuando necesitamos realizar cálculos con grandes volúmenes de datos, podemos hacer:

```javascript
const resultado = datos.filter(filtrarDatosPesados);
```

**Pero esto no es muy óptimo** porque cada vez que el componente se renderiza, se recalcula.

**La mejor solución sería usar `useMemo`:**

```javascript
const resultado = useMemo(() => datos.filter(filtrarDatosPesados), [datos]);
```

**Esto debido a que** `useMemo` solo recalcula el valor si `datos` cambia, evitando trabajo innecesario.

---

### 2️⃣ **Evitar re-creación de funciones con `useCallback`**

Cuando pasamos funciones como props a componentes hijos, podemos hacer:

```javascript
const handleClick = () => hacerAlgo();
```

**Pero esto no es muy óptimo**, porque se crea una nueva función en cada render.

**La mejor solución sería usar `useCallback`:**

```javascript
const handleClick = useCallback(() => hacerAlgo(), []);
```

**Esto debido a que** mantiene la misma referencia de función entre renders, evitando renders innecesarios en los hijos.

---

### 3️⃣ **Renderizado condicional limpio usando operadores lógicos**

Cuando hacemos condicionales podemos escribir:

```javascript
if (cargando) {
    return <Spinner />;
} else {
    return <Contenido />;
}
```

**Esto es verboso.**

**La mejor solución sería usar operadores lógicos:**

```javascript
{cargando ? <Spinner /> : <Contenido />}
```

**Esto debido a que** simplifica el código y mejora la legibilidad.

---

### 4️⃣ **Dividir el código con `React.lazy` y `Suspense`**

Cuando cargamos todos los componentes de golpe:

```javascript
import ComponentePesado from './ComponentePesado';
```

**Esto no es óptimo**, especialmente en apps grandes.

**La mejor solución sería usar `React.lazy`:**

```javascript
const ComponentePesado = React.lazy(() => import('./ComponentePesado'));
```

Y envolverlo con `Suspense`:

```javascript
<Suspense fallback={<Spinner />}>
    <ComponentePesado />
</Suspense>
```

**Esto debido a que** carga los componentes solo cuando se necesitan (*code splitting*), mejorando el rendimiento inicial.

---

### 5️⃣ **Actualizar arrays/objetos de forma inmutable**

Cuando modificamos un array directamente:

```javascript
lista.push(nuevoElemento);
```

**No es óptimo** porque muta el estado directamente.

**La mejor solución sería crear una nueva copia:**

```javascript
setLista([...lista, nuevoElemento]);
```

**Esto debido a que** React detecta mejor los cambios si el estado es inmutable.

---

### 6️⃣ **Usar `key` únicas y estables en listas**

Cuando renderizamos listas sin clave única:

```javascript
{lista.map((item) => <Elemento item={item} />)}
```

**Esto no es óptimo** y puede causar errores de renderizado.

**La mejor solución sería usar claves únicas:**

```javascript
{lista.map((item) => <Elemento key={item.id} item={item} />)}
```

**Esto debido a que** React necesita las `key` para identificar qué elementos han cambiado, agregado o eliminado.

---

### 7️⃣ **Evitar renders innecesarios con `React.memo`**

Cuando un componente hijo siempre recibe las mismas props, pero se re-renderiza igual:

```javascript
function Hijo(props) {
    return <div>{props.valor}</div>;
}
```

**Esto no es óptimo**.

**La mejor solución sería envolverlo con `React.memo`:**

```javascript
const Hijo = React.memo(function Hijo(props) {
    return <div>{props.valor}</div>;
});
```

**Esto debido a que** evita renders si las props no cambiaron.

---

### 8️⃣ **Evitar pasar objetos/arrays nuevos como props directamente**

Cuando hacemos:

```javascript
<Hijo config={{ tema: 'oscuro' }} />
```

**Esto no es óptimo**, porque se crea un nuevo objeto en cada render y React piensa que cambió.

**La mejor solución sería usar `useMemo`:**

```javascript
const config = useMemo(() => ({ tema: 'oscuro' }), []);
<Hijo config={config} />
```

**Esto debido a que** mantiene la misma referencia entre renders y evita renders innecesarios.

---

### 9️⃣ **Usar el operador spread para props dinámicas**

Cuando pasamos muchas props manualmente:

```javascript
<Boton color="azul" tamaño="grande" borde="redondo" />
```

**Esto es repetitivo.**

**La mejor solución sería usar spread:**

```javascript
const props = { color: 'azul', tamaño: 'grande', borde: 'redondo' };
<Boton {...props} />
```

**Esto debido a que** simplifica el código y facilita pasar props dinámicamente.

---

### 🔟 **Evitar estados innecesarios**

Cuando guardamos valores derivados en el estado:

```javascript
const [total, setTotal] = useState(items.length * precioUnitario);
```

**Esto no es óptimo**, porque obliga a actualizar el estado cada vez que cambian `items` o `precioUnitario`.

**La mejor solución sería calcularlo directamente:**

```javascript
const total = items.length * precioUnitario;
```

**Esto debido a que** reduce la complejidad y evita inconsistencias en el estado.

---------------------------------------

## 🔧 Trucos de Programación en Node.js

### 1️⃣ **Streams para procesar archivos grandes sin colapsar la memoria**

Cuando necesitamos trabajar con archivos grandes, algunos hacen:

```js
const fs = require('fs');
const data = fs.readFileSync('archivo.txt', 'utf8');
console.log(data);
```

Esto **no es óptimo**, porque `fs.readFileSync()` carga todo el archivo en memoria, lo que puede romper tu app si el archivo es muy grande.

**La mejor solución sería usar `streams`**:

```js
const fs = require('fs');
const stream = fs.createReadStream('archivo.txt', 'utf8');
stream.on('data', chunk => console.log(chunk));
```

**Esto debido a que** los *streams* leen los datos en pequeños bloques y los procesan conforme van llegando, lo cual es mucho más eficiente para manejar grandes volúmenes de información.

---

### 2️⃣ **Uso de `cluster` para aprovechar todos los núcleos del procesador**

Por defecto, una app Node.js corre en un solo núcleo, así que si tienes un servidor con varios, los demás quedan sin usar:

```js
// servidor tradicional en Node.js usa solo un hilo
```

**Esto no es óptimo para alto rendimiento.**

**La mejor solución sería usar el módulo `cluster`**:

```js
const cluster = require('cluster');
const os = require('os');

if (cluster.isPrimary) {
  const cpus = os.cpus().length;
  for (let i = 0; i < cpus; i++) cluster.fork();
} else {
  require('./servidor'); // aquí corre tu app real
}
```

**Esto debido a que** puedes crear múltiples procesos que trabajen en paralelo, uno por cada núcleo, mejorando el rendimiento en producción.

---

### 3️⃣ **Manejo global de errores con `process.on()`**

Cuando usamos promesas y funciones asíncronas, a veces olvidamos manejar errores:

```js
someAsyncFunction(); // sin try/catch ni .catch()
```

**Esto puede hacer que la app se caiga silenciosamente.**

**La mejor solución sería usar eventos globales para capturar errores no manejados**:

```js
process.on('unhandledRejection', (reason, promise) => {
  console.error('Rechazo no manejado:', reason);
});

process.on('uncaughtException', (err) => {
  console.error('Excepción no capturada:', err);
});
```

**Esto debido a que** permite registrar o actuar ante errores inesperados y mantener tu app estable.

---

### 4️⃣ **Evitar bloqueos usando funciones asíncronas y `await`**

Cuando usamos operaciones lentas de forma síncrona, como:

```js
const data = fs.readFileSync('archivo.txt');
```

**Esto detiene todo el hilo de ejecución**, lo cual es un problema si tienes múltiples usuarios conectados.

**La mejor solución sería usar `async/await` con funciones no bloqueantes**:

```js
const fs = require('fs/promises');
const data = await fs.readFile('archivo.txt', 'utf8');
```

**Esto debido a que** Node.js es de un solo hilo, y usar I/O asíncrono mantiene la app rápida y reactiva.

---

### 5️⃣ **Uso de `dotenv` para separar configuración sensible del código**

Cuando incluimos claves de API o configuraciones directamente en el código:

```js
const apiKey = 'MI_CLAVE_SECRETA';
```

**Esto no es seguro ni profesional.**

**La mejor solución sería usar variables de entorno con `dotenv`**:

```js
// .env
API_KEY=MI_CLAVE_SECRETA
```

```js
// app.js
require('dotenv').config();
const apiKey = process.env.API_KEY;
```

**Esto debido a que** facilita el manejo de configuraciones entre entornos (dev, prod) y protege datos sensibles del código fuente.


---------------------------------------

## Trucos en Java

---------------------------------------

## 🔥 Trucos de Programación en JavaScript

### 1️⃣ **Usar `map()` en lugar de `forEach()` para transformar arreglos**

Cuando necesitamos transformar todos los elementos de un arreglo, muchos usan:

```javascript
let resultado = [];
[1, 2, 3].forEach(x => resultado.push(x * 2));
```

Pero esto **no es muy óptimo** porque requiere crear y manipular manualmente un nuevo arreglo.

**La mejor solución sería usar `map()`**:

```javascript
let resultado = [1, 2, 3].map(x => x * 2);
```

**Esto debido a que** `map()` devuelve automáticamente un nuevo arreglo sin modificar el original, con mejor rendimiento y código más limpio.

---

### 2️⃣ **Uso de `filter()` en lugar de bucles para filtrar datos**

Cuando queremos obtener solo ciertos elementos:

```javascript
let filtrados = [];
for (let x of datos) {
    if (x.activo) filtrados.push(x);
}
```

**No es óptimo.**

**La mejor solución**:

```javascript
let filtrados = datos.filter(x => x.activo);
```

**Esto debido a que** `filter()` es más declarativo, evita errores y facilita la lectura.

---

### 3️⃣ **Evitar bucles anidados usando `reduce()`**

Cuando sumamos valores o agrupamos datos:

```javascript
let suma = 0;
for (let x of numeros) suma += x;
```

**Esto funciona pero no es óptimo.**

**La mejor solución**:

```javascript
let suma = numeros.reduce((a, b) => a + b, 0);
```

**Esto debido a que** `reduce()` permite manejar grandes volúmenes de datos con una sola función, sin necesidad de múltiples bucles.

---

### 4️⃣ **Uso de `Set` para eliminar duplicados**

Cuando eliminamos duplicados manualmente:

```javascript
let unicos = [];
for (let x of arreglo) {
    if (!unicos.includes(x)) unicos.push(x);
}
```

**No es eficiente.**

**La mejor solución**:

```javascript
let unicos = [...new Set(arreglo)];
```

**Esto debido a que** `Set` no permite duplicados y realiza búsquedas más rápidas que `includes`.

---

### 5️⃣ **Desestructuración para extraer valores fácilmente**

Cuando accedemos repetidamente a propiedades:

```javascript
let nombre = persona.nombre;
let edad = persona.edad;
```

**Esto es repetitivo.**

**La mejor solución**:

```javascript
let { nombre, edad } = persona;
```

**Esto debido a que** la desestructuración hace el código más limpio y evita repeticiones.

---

### 6️⃣ **Uso de parámetros por defecto en funciones**

Cuando asignamos valores por defecto así:

```javascript
function saludar(nombre) {
    nombre = nombre || 'Invitado';
    console.log(`Hola, ${nombre}`);
}
```

**Esto es antiguo y puede fallar si el valor es falsy (como 0 o "").**

**La mejor solución**:

```javascript
function saludar(nombre = 'Invitado') {
    console.log(`Hola, ${nombre}`);
}
```

**Esto debido a que** los parámetros por defecto son más seguros y modernos (desde ES6).

---

### 7️⃣ **Encadenamiento opcional (`?.`) para evitar errores en propiedades anidadas**

Cuando accedemos a propiedades anidadas:

```javascript
let ciudad = usuario && usuario.direccion && usuario.direccion.ciudad;
```

**Este enfoque es engorroso.**

**La mejor solución**:

```javascript
let ciudad = usuario?.direccion?.ciudad;
```

**Esto debido a que** el encadenamiento opcional evita errores si alguna propiedad intermedia no existe.

---

### 8️⃣ **Uso del operador rest (`...`) para combinar listas y objetos**

Cuando combinamos arreglos:

```javascript
let combinado = lista1.concat(lista2);
```

**Puede ser menos intuitivo.**

**La mejor solución**:

```javascript
let combinado = [...lista1, ...lista2];
```

**Esto debido a que** el operador spread/rest es más flexible y también permite combinar objetos:

```javascript
let nuevoObjeto = { ...objeto1, ...objeto2 };
```

---

### 9️⃣ **Funciones flecha (`=>`) para mantener el contexto de `this`**

Cuando usamos funciones normales:

```javascript
function Persona() {
    this.edad = 0;
    setInterval(function() {
        this.edad++;
    }, 1000);
}
```

**Aquí `this` no se comporta como esperamos.**

**La mejor solución**:

```javascript
function Persona() {
    this.edad = 0;
    setInterval(() => {
        this.edad++;
    }, 1000);
}
```

**Esto debido a que** las arrow functions no crean su propio `this`, usan el del contexto donde fueron creadas.

---

### 🔟 **Uso de `Promise.all()` para múltiples promesas en paralelo**

Cuando manejamos varias promesas una por una:

```javascript
let resultado1 = await promesa1;
let resultado2 = await promesa2;
```

**Esto es secuencial y lento.**

**La mejor solución**:

```javascript
let [resultado1, resultado2] = await Promise.all([promesa1, promesa2]);
```

**Esto debido a que** `Promise.all()` ejecuta todas las promesas en paralelo, reduciendo el tiempo de espera.


---------------------------------------

## Trucos en Python

---------------------------------------

## Trucos en Kotlin

---------------------------------------

## Trucos en Golang

---------------------------------------

## Trucos en Typescript

---------------------------------------

## Trucos en Swift

---------------------------------------


## Author

Created by Leon Martin ([Malvabombom](https://github.com/malvabombom)).

[![in]][in-link] [![ig]][ig-link] [![tt]][tt-link]

Thank you for reading. <3


[fg]: https://img.shields.io/badge/Figma-F24E1E?style=flat-square&logo=figma&logoColor=white
[in]: https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white
[ig]: https://img.shields.io/badge/Instagram-E4405F?style=flat-square&logo=instagram&logoColor=white
[fb]: https://img.shields.io/badge/Facebook-1877F2?style=flat-square&logo=facebook&logoColor=white
[tt]: https://img.shields.io/badge/tiktok-000000?style=flat-square&logo=tiktok&logoColor=white

[as]: https://holasoymalva.xyz/
[in-link]: https://www.linkedin.com/in/martin-manriquez-899877177/
[ig-link]: https://www.instagram.com/holasoymalva/
[tt-link]: https://www.tiktok.com/@holasoymalva
