
# Agrupaciones en MongoDB

La etapa `$group` en MongoDB se utiliza para agrupar documentos que comparten un campo o conjunto de campos comunes. Es similar a la cláusula `GROUP BY` en SQL y permite aplicar funciones de agregación a los grupos formados. A continuación, se describen los aspectos clave de las agrupaciones con ejemplos.

## 1. Sintaxis básica de `$group`

La sintaxis básica para utilizar `$group` es la siguiente:

```json
{ $group: { 
    _id: <expresión_clave>, 
    <campo1>: { <acumulador>: <expresión> }, 
    <campo2>: { <acumulador>: <expresión> },
    ...
}}
```

- **`_id`**: Es el campo que se utiliza como clave para agrupar. Puede ser un campo existente o una expresión.
- **`<campo>`**: Define los nuevos campos que se crearán en el resultado, donde se aplican funciones de agregación como `$sum`, `$avg`, `$min`, `$max`, etc.

## 2. Ejemplo básico de agrupación

### Ejemplo 1: Agrupar por un campo

Supongamos que queremos encontrar el número total de propiedades por tipo. Podemos agrupar por el campo `property_type`.

```javascript
db.listings.aggregate([
    { $group: {
        _id: '$property_type',
        total: { $sum: 1 }
    }}
])
```

Este comando agrupa todas las propiedades por su tipo y cuenta cuántas hay de cada tipo.

## 3. Funciones de agregación

Las funciones de agregación son utilizadas dentro de `$group` para realizar cálculos sobre los documentos agrupados. Algunas de las más comunes son:

- **`$sum`**: Suma los valores de un campo.
- **`$avg`**: Calcula el promedio de los valores de un campo.
- **`$min`**: Encuentra el valor mínimo de un campo.
- **`$max`**: Encuentra el valor máximo de un campo.
- **`$push`**: Crea un array con todos los valores de un campo.
- **`$first`**: Devuelve el primer valor de un campo en el grupo.
- **`$last`**: Devuelve el último valor de un campo en el grupo.

### Ejemplo 2: Usando varias funciones de agregación

Busquemos el precio promedio, el precio mínimo y el precio máximo de propiedades agrupadas por país.

```javascript
db.listings.aggregate([
    { $group: {
        _id: '$address.country',
        precioPromedio: { $avg: '$price' },
        precioMinimo: { $min: '$price' },
        precioMaximo: { $max: '$price' }
    }}
])
```

## 4. Agrupaciones complejas

Puedes agrupar por múltiples campos utilizando un objeto para definir el `_id`.

### Ejemplo 3: Agrupación por múltiples campos

Supongamos que queremos agrupar por país y tipo de propiedad y contar cuántas propiedades hay en cada combinación.

```javascript
db.listings.aggregate([
    { $group: {
        _id: {
            country: '$address.country',
            type: '$property_type'
        },
        total: { $sum: 1 }
    }}
])
```

## 5. Filtrado después de agrupar

Puedes aplicar un filtro sobre los resultados agrupados utilizando `$match` después de `$group`, similar a `HAVING` en SQL.

### Ejemplo 4: Filtrar agrupaciones

Busquemos las ciudades donde el precio promedio de las propiedades es mayor a 200 dólares.

```javascript
db.listings.aggregate([
    { $group: {
        _id: '$address.city',
        precioPromedio: { $avg: '$price' }
    }},
    { $match: { precioPromedio: { $gt: 200 } } }
])
```

## 6. Ordenar resultados agrupados

Después de agrupar, puedes ordenar los resultados utilizando `$sort`.

### Ejemplo 5: Ordenar agrupaciones

Busquemos el número total de propiedades por tipo y ordenémoslo de mayor a menor.

```javascript
db.listings.aggregate([
    { $group: {
        _id: '$property_type',
        total: { $sum: 1 }
    }},
    { $sort: { total: -1 } }
])
```

## Conclusión

La etapa `$group` en MongoDB es una herramienta poderosa para realizar agrupaciones y aplicar funciones de agregación sobre conjuntos de documentos. Permite resumir datos, obtener estadísticas y realizar análisis complejos sobre la información almacenada en la base de datos.
