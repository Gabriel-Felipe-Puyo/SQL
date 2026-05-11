# Agregación

<img width="870" height="600" alt="image" src="https://github.com/user-attachments/assets/0ee0515d-7022-4b89-bcf0-2a9257b88ec1" />


Aquí tienes una explicación detallada de los filtros en MongoDB, con ejemplos, en formato markdown:

# Filtros en MongoDB

Los filtros en MongoDB se utilizan para seleccionar documentos que cumplan con ciertas condiciones. La etapa `$match` es la que se utiliza para aplicar estos filtros en un Aggregation Pipeline. A continuación, se describen los diferentes aspectos de los filtros con ejemplos.

## 1. Uso básico de `$match`

La etapa `$match` permite filtrar documentos basados en una condición específica. Su sintaxis básica es:

```json
{ $match: { <expresión_de_consulta> } }
```

### Ejemplo 1: Filtrar por un campo específico

Supongamos que queremos buscar todas las propiedades cuyo precio sea mayor a 100 dólares.

```javascript
db.listings.aggregate([
    { $match: { price: { $gt: 100 } } }
])
```

## 2. Filtrado con múltiples condiciones

Se pueden combinar múltiples condiciones utilizando operadores lógicos como `$and`, `$or`, y `$not`.

### Ejemplo 2: Usando `$and`

Busquemos propiedades que cuesten entre 50 y 150 dólares y que estén ubicadas en España.

```javascript
db.listings.aggregate([
    { $match: { 
        $and: [
            { price: { $gte: 50, $lte: 150 } },
            { 'address.country': 'Spain' }
        ] 
    }}
])
```

### Ejemplo 3: Usando `$or`

Busquemos propiedades que estén en Portugal o que cuesten menos de 50 dólares.

```javascript
db.listings.aggregate([
    { $match: { 
        $or: [
            { 'address.country': 'Portugal' },
            { price: { $lt: 50 } }
        ] 
    }}
])
```

## 3. Filtrado con condiciones en campos anidados

MongoDB permite filtrar también en campos anidados utilizando la notación de punto.

### Ejemplo 4: Filtrar en un campo anidado

Busquemos propiedades que tengan un servicio específico, como "WiFi", en su lista de amenities.

```javascript
db.listings.aggregate([
    { $match: { 'amenities': { $elemMatch: { $eq: 'WiFi' } } } }
])
```

## 4. Filtrado en combinación con `$group`

Cuando `$match` se coloca después de `$group`, actúa como un filtro sobre los resultados agrupados, similar a `HAVING` en SQL.

### Ejemplo 5: Filtrar después de agrupar

Supongamos que queremos encontrar las ciudades donde el promedio de precios de las propiedades es mayor a 200 dólares.

```javascript
db.listings.aggregate([
    { $group: {
        _id: '$address.city',
        promedioPrecio: { $avg: '$price' }
    }},
    { $match: { promedioPrecio: { $gt: 200 } } }
])
```

## 5. Filtrado de documentos con condiciones complejas

MongoDB permite realizar consultas complejas utilizando operadores de comparación y lógicos.

### Ejemplo 6: Filtrado con condiciones complejas

Busquemos propiedades que tengan un precio entre 100 y 300 dólares, que permitan más de 4 huéspedes y que estén disponibles.

```javascript
db.listings.aggregate([
    { $match: { 
        price: { $gte: 100, $lte: 300 },
        accommodates: { $gt: 4 },
        availability: { $eq: true }
    }}
])
```

## Conclusión

Los filtros en MongoDB son una herramienta poderosa para seleccionar documentos según criterios específicos. Utilizando la etapa `$match`, puedes crear consultas complejas y precisas que te ayuden a extraer la información que necesitas de tus bases de datos.
