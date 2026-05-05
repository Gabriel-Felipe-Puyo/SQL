# Operadores Lógicos en MongoDB

Los operadores lógicos se utilizan para combinar múltiples condiciones en una consulta. Los principales operadores lógicos en MongoDB son:

1. **$and**
2. **$or**
3. **$not**
4. **$nor**

#### 1. Operador `$and`

### Descripción
El operador `$and` se utiliza para combinar múltiples condiciones, y todos deben cumplirse para que un documento sea devuelto.

### Ejemplo
Supongamos que deseas encontrar propiedades que estén ubicadas en "España" y que tengan un precio menor a 100.

```javascript
db.listings.find({
  $and: [
    { "address.country": "Spain" },
    { price: { $lt: 100 } }
  ]
});
```

#### 2. Operador `$or`

### Descripción
El operador `$or` se utiliza para combinar múltiples condiciones, y al menos una de ellas debe cumplirse para que un documento sea devuelto.

### Ejemplo
Si deseas encontrar propiedades que estén ubicadas en "España" o "Francia", usarías:

```javascript
db.listings.find({
  $or: [
    { "address.country": "Spain" },
    { "address.country": "France" }
  ]
});
```

#### 3. Operador `$not`

### Descripción
El operador `$not` se utiliza para invertir una condición. Es útil cuando deseas excluir documentos que cumplen con una condición específica.

### Ejemplo
Si deseas encontrar propiedades que **no** están ubicadas en "Estados Unidos", usarías:

```javascript
db.listings.find({
  "address.country": { $not: { $eq: "United States" } }
});
```

#### 4. Operador `$nor`

### Descripción
El operador `$nor` se utiliza para combinar múltiples condiciones, y ninguno de los documentos debe cumplir con las condiciones especificadas para ser devueltos.

### Ejemplo
Si deseas encontrar propiedades que **no** están ubicadas en "España" ni en "Francia", usarías:

```javascript
db.listings.find({
  $nor: [
    { "address.country": "Spain" },
    { "address.country": "France" }
  ]
});
```

### Resumen

- **$and**: Todos los criterios deben cumplirse.
- **$or**: Al menos uno de los criterios debe cumplirse.
- **$not**: Invierte la condición.
- **$nor**: Ninguno de los criterios debe cumplirse.
