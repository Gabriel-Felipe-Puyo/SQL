# Expresiones en MongoDB

Las expresiones en MongoDB permiten realizar comparaciones y evaluaciones más complejas dentro de las consultas. Se utilizan principalmente con el operador `$expr`, que habilita el uso de variables de agregación (prefijo `$campo`) y operadores del pipeline de agregación dentro de un filtro `find()`. Esto permite comparar dos campos del mismo documento.

#### Uso del Operador `$expr`

El operador `$expr` permite realizar consultas que involucran operaciones aritméticas y comparaciones entre campos de un mismo documento. Esto es útil cuando se necesita evaluar condiciones que no se pueden expresar simplemente con los operadores de comparación estándar.

### Ejemplo 1: Comparar dos campos

Supongamos que tienes una colección `listings` y deseas encontrar propiedades donde el número de cuartos (`bedrooms`) sea igual al número de camas (`beds`).

```javascript
db.listings.find({
  $expr: { $eq: ["$bedrooms", "$beds"] }
});
```

En este ejemplo, `$eq` compara los valores de los campos `bedrooms` y `beds`, y devuelve los documentos donde ambos son iguales.

### Ejemplo 2: Comparar con operaciones aritméticas

Imagina que tienes un campo `price` que representa el precio por noche y un campo `cleaning_fee` que representa la tarifa de limpieza. Si deseas encontrar propiedades donde el precio total (precio por noche más tarifa de limpieza) sea mayor a 150, podrías usar:

```javascript
db.listings.find({
  $expr: { $gt: [{ $add: ["$price", "$cleaning_fee"] }, 150] }
});
```

Aquí, `$add` suma los valores de `price` y `cleaning_fee`, y `$gt` verifica si el resultado es mayor que 150.

### Ejemplo 3: Uso de operadores lógicos con expresiones

Puedes combinar `$expr` con operadores lógicos para crear consultas más complejas. Por ejemplo, si deseas encontrar propiedades donde el puntaje de limpieza (`cleanliness_score`) sea mayor que 8 y el puntaje de comunicación (`communication_score`) sea también mayor que 8, usarías:

```javascript
db.listings.find({
  $expr: {
    $and: [
      { $gt: ["$cleanliness_score", 8] },
      { $gt: ["$communication_score", 8] }
    ]
  }
});
```

### Resumen

- **$expr**: Permite el uso de expresiones para comparar campos dentro de un documento.
- Se pueden utilizar operadores de comparación como `$eq`, `$gt`, `$lt`, etc., junto con operaciones aritméticas como `$add`, `$subtract`, etc.
- Es útil para realizar consultas donde se necesita comparar o evaluar condiciones entre diferentes campos del mismo documento.
