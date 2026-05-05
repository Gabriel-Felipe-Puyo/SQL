# Cursores en MongoDB

Un **cursor** es un apuntador a un conjunto de resultados devueltos por una consulta en MongoDB. Cuando realizas una consulta utilizando el método `find()`, MongoDB no devuelve los resultados directamente. En su lugar, devuelve un cursor que permite iterar sobre los resultados.

#### Características de los Cursores

- **Evaluación Perezosa**: Los cursores operan con evaluación perezosa, lo que significa que la consulta no se ejecuta hasta que se itera el cursor. Esto permite encadenar modificadores sin costo adicional.
- **Encadenamiento**: Puedes encadenar métodos adicionales como `sort()`, `limit()`, y `skip()` al cursor para modificar el conjunto de resultados.

### Ejemplo de Uso de Cursores

Supongamos que tienes una colección `listings` y deseas obtener todos los documentos. Puedes hacerlo así:

```javascript
const cursor = db.listings.find();
```

Para iterar sobre los resultados, puedes usar un bucle:

```javascript
cursor.forEach(doc => {
  printjson(doc);
});
```

### Ordenamiento en MongoDB

El método `.sort()` se utiliza para ordenar los resultados devueltos por una consulta. Puedes especificar el campo por el cual deseas ordenar y el orden (ascendente o descendente).

#### Sintaxis del Método `.sort()`

```javascript
db.nombre_colección.find().sort({ campo: 1|-1 })
```

- **1**: Orden ascendente.
- **-1**: Orden descendente.

### Ejemplo de Ordenamiento

Supongamos que deseas obtener una lista de propiedades ordenadas por precio de forma descendente:

```javascript
db.listings.find().sort({ price: -1 });
```

Si deseas obtener una lista de propiedades ordenadas por nombre de forma ascendente, usarías:

```javascript
db.listings.find().sort({ name: 1 });
```

### Combinando Cursores y Ordenamiento

Puedes combinar el uso de cursores y ordenamiento en una sola consulta. Por ejemplo, si deseas obtener las 5 propiedades más caras, puedes usar `limit()` junto con `sort()`:

```javascript
db.listings.find().sort({ price: -1 }).limit(5);
```

### Resumen

- **Cursores**: Son apuntadores a un conjunto de resultados devueltos por una consulta y permiten iterar sobre los resultados.
- **Ordenamiento**: Se realiza utilizando el método `.sort()`, donde puedes especificar el campo y el orden (ascendente o descendente).
- **Combinación**: Puedes encadenar métodos como `sort()` y `limit()` para modificar el conjunto de resultados.
