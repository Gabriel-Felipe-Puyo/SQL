# Conteo de Documentos en MongoDB

MongoDB proporciona varias formas de contar documentos en una colección. Esto es útil para obtener estadísticas sobre los datos o para realizar operaciones condicionales basadas en la cantidad de documentos.

### Métodos para Contar Documentos

1. **`countDocuments()`**
2. **`count()`**
3. **`estimatedDocumentCount()`**

#### 1. Método `countDocuments()`

El método `countDocuments()` se utiliza para contar el número de documentos que coinciden con un filtro específico. Este método es más preciso que `count()` porque cuenta documentos que coinciden con la consulta actual y no se basa en índices.

##### Ejemplo

Supongamos que tienes una colección `listings` y deseas contar cuántas propiedades están ubicadas en "España":

```javascript
const count = db.listings.countDocuments({ "address.country": "Spain" });
print("Número de propiedades en España: " + count);
```

#### 2. Método `count()`

El método `count()` es similar a `countDocuments()`, pero se considera obsoleto y se recomienda usar `countDocuments()` en su lugar. Sin embargo, si se usa, puede ser más rápido para consultas simples sin filtros.

##### Ejemplo

Puedes contar todos los documentos en la colección `listings` así:

```javascript
const totalCount = db.listings.count();
print("Número total de propiedades: " + totalCount);
```

#### 3. Método `estimatedDocumentCount()`

El método `estimatedDocumentCount()` proporciona una estimación rápida del número total de documentos en una colección. Utiliza información de los índices y es más eficiente que `countDocuments()`, pero no es exacto.

##### Ejemplo

Para obtener una estimación del número total de documentos en la colección `listings`, usarías:

```javascript
const estimatedCount = db.listings.estimatedDocumentCount();
print("Estimación del número total de propiedades: " + estimatedCount);
```

### Resumen

- **`countDocuments()`**: Cuenta documentos que coinciden con un filtro específico; es preciso y se recomienda para conteos basados en condiciones.
- **`count()`**: Método obsoleto que cuenta documentos; se recomienda evitar su uso.
- **`estimatedDocumentCount()`**: Proporciona una estimación rápida del número total de documentos en una colección; es más rápido pero menos preciso.
