# Estructura Básica de una Consulta
La estructura general de una consulta en MongoDB se compone de varios elementos. A continuación te muestro cómo se organiza:

```javaScript
db.nombre_colección.find(filtro, proyección)
````
# Componentes

* db:
Hace referencia a la base de datos actual.

* nombre_colección:
El nombre de la colección en la que deseas realizar la consulta.

* find():
Método utilizado para buscar documentos dentro de la colección.

* filtro:
Un objeto que define las condiciones que los documentos deben cumplir para ser devueltos. Este es un argumento obligatorio.
> Ejemplo: { campo: valor } o { campo: { $gt: valor } }.

* proyección:
(Opcional) Un objeto que especifica qué campos deseas incluir o excluir en los documentos devueltos.

> Ejemplo: { campo1: 1, campo2: 0 } (incluye campo1 y excluye campo2).

---

## Ejemplo de Consulta
Supongamos que deseas buscar todos los documentos en la colección listings donde el precio es mayor a 100, y solo quieres incluir los campos name y price en el resultado:

```javaScript
db.listings.find(
  { price: { $gt: 100 } },  // Filtro
  { name: 1, price: 1 }     // Proyección / columnas a mostrar
);
```
