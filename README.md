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

## Trucos en Java

---------------------------------------

## Trucos en JavaScript

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
