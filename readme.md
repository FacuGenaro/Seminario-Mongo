# Dia 1:

## 1. Instalar MongoDB en ambiente local.

## 2. Conectarse a MongoDB vía CLI.

```
mongo

```

## 3. Crear una nueva base de datos.
```
use futbolfifa
```

## 4. Crear una nueva collection.
db.createCollection("players")

## 5. Insertar 5 documentos en la collection con datos básicos.

```
db.players.insert({name: "lionel",apellido: "messi"})
db.players.insert({name:"riquelme",status:"retirado"})
db.players.insert({name: "sergio", apellido: "aguero"})
db.players.insert([{name: "esteban", apellido: "andrada"}, {name: "lautaro", apellido: "martinez"}, {name: "hernan", apellido: "grana"}])
```

## 6. Listar todos los documentos de la collection.

```
db.players.find()

```

# Dia 2:

```
use Netflix
db.createCollection("movies")

```

## 2- Para cada movie, se debería guardar información como título (String), year (Number), rating (Number, entre 1.0 y 5.0), genre (String), description (String), actors (Array<String>), country (String), income (Number), duration (Number).

## 3- Agregar películas usando insert(), insertOne() & insertMany().

```
db.movies.insert([
    {
        "title": "Lorem",
        "year": 2019,
        "rating": 5.0,
        "genre": "Drama",
        "description": "Lorem ipsum dolor sit amet.",
        "actors": [
            "Lorem ipsum",
            "dolor sit"
        ],
        "country": "USA",
        "income": 12345,
        "duration": 123
    },
    {
        "title": "Lorem 2",
        "year": 2019,
        "rating": 4.5,
        "genre": "Drama",
        "description": "Lorem ipsum dolor sit amet.",
        "actors": [
            "Lorem ipsum",
            "dolor sit"
        ],
        "country": "USA",
        "income": 12345,
        "duration": 123
    },
    {
        "title": "Lorem 3",
        "year": 2019,
        "rating": 4,
        "genre": "Drama",
        "description": "Lorem ipsum dolor sit amet.",
        "actors": [
            "Lorem ipsum",
            "dolor sit"
        ],
        "country": "USA",
        "income": 12345,
        "duration": 123
    },
])

db.movies.insertOne(
    {
    "title": "Movie 4",
    "year": 1993,
    "rating": 3.0,
    "genre": "Comedy",
    "description": "Lorem ipsum dolor sit amet.",
    "actors": [
        "Lorem ipsum",
        "dolor sit"
    ],
    "country": "USA",
    "income": 12345,
    "duration": 123
}
)

db.movies.insertMany([
    {
        "title": "Movie 5",
        "year": 1993,
        "rating": 3.0,
        "genre": "Comedy",
        "description": "Lorem ipsum dolor sit amet.",
        "actors": [
            "Lorem ipsum",
            "dolor sit"
        ],
        "country": "USA",
        "income": 12345,
        "duration": 123
    },
    {
        "title": "Movie 6",
        "year": 2003,
        "rating": 4.0,
        "genre": "Horror",
        "description": "Lorem ipsum dolor sit amet.",
        "actors": [
            "Lorem ipsum",
            "dolor sit"
        ],
        "country": "USA",
        "income": 12345,
        "duration": 123
    },
])

```

## 4- Actualizar películas agregando el field highlighted = true a aquellas con rating > 4.5.

```
db.movies.updateMany(
	{rating: {$gt: 4.5}},
	{$set: {highlighted: true}},
	{upsert: true}
)
```

## 5- Actualizar películas cambiando el genre “drama” por “bored”.

```

db.movies.updateMany(
    { genre: "Drama" },
    { $set: { genre: "Bored"}}
)

```

## 6- Borrar todas las películas que tengan más de 30 años.
```
db.movies.deleteMany({year: {$lt: new Date().getFullYear() - 30}})
```

## 7- Buscar todas las películas argentinas.

```
db.movies.find({country: "Argentina"})
```

## 8- Buscar todas las películas de acción con un buen rating (ej. > 4.0) que hayan salido los últimos 2 años.

```
db.movies.find({
    genre: "Action",
    rating: {$gt: 4.0},
    year: {$gt: new Date().getFullYear() - 2}
})
```

# Dia 3:

## 1- Utilizar la misma base de datos de películas e insertar varias películas con distinto contenido.

```
db.movies.insertMany([
    {
        "title": "Movie 7",
        "year": 1993,
        "rating": 3.0,
        "genre": "Horro",
        "description": "Lorem ipsum dolor sit amet.",
        "actors": [
            "Lorem ipsum",
            "dolor sit"
        ],
        "country": "USA",
        "income": 12345,
        "duration": 123
    },
    {
        "title": "Movie 8",
        "year": 2016,
        "rating": 4.0,
        "genre": "Mistery",
        "description": "Lorem ipsum dolor sit amet.",
        "actors": [
            "Lorem ipsum",
            "dolor sit"
        ],
        "country": "USA",
        "income": 12345,
        "duration": 123
    },
    {
        "title": "Movie 9",
        "year": 2017,
        "rating": 4.5,
        "genre": "Action",
        "description": "Lorem ipsum dolor sit amet.",
        "actors": [
            "Lorem ipsum",
            "dolor sit"
        ],
        "country": "USA",
        "income": 12345,
        "duration": 123
    },
    {
        "title": "Movie 10",
        "year": 2018,
        "rating": 5.0,
        "genre": "Thriller",
        "description": "Lorem ipsum dolor sit amet.",
        "actors": [
            "Lorem ipsum",
            "dolor sit"
        ],
        "country": "USA",
        "income": 12345,
        "duration": 123
    },

])

```

## 2- Listar todas las películas del año 2018.

```
db.movies.find({year: 2018})
```

## 3- Listar las 10 primeras películas de Hollywood.

```
db.movies.find({country: "USA"}).limit(10).sort({year: 1})
```

## 4- Listar las 5 películas más taquilleras.

```
db.movies.find().limit(5).sort({income: -1})
```

## 5- Listar el 2do conjunto de 5 películas más taquilleras.

```
db.movies.find()
.skip(5)
.limit(5)
.sort({income: -1})
```

## 6- Repetir query 3 y 4 pero retornando sólo el título y genre. Mostrar los distintos países que existen en la base de datos.

```
db.movies.find({country: "USA"}, {titulo: 1, genre:1, _id:0})
.limit(10)
.sort({year: 1})

db.movies.find({}, {titulo: 1, genre: 1, _id: 0})
.limit(5)
.sort({income: -1})

```
## 7- Mostrar los distintos países que existen en la base de datos.
```
db.movies.distinct("country")
```

# Dia 4:

## 1. Crear índice en field rating y luego hacer búsquedas usando este campo.

Creo el index
```
db.movies.createIndex({rating: 1})

```
Hago la busqueda
```
db.movies.find({rating: {$gt: 4.5}}, {title: 1, rating: 1, _id: 0})
db.movies.find({rating: {$gt: 3.9, $lt: 4.6}})
```

## 2. Crear índice en title y description, y después hacer búsquedas de texto en estos campos.

Creo el index en title y description
```
db.movies.createIndex({title: "text", description: "text"})
```

Hago la busqueda
```
db.movies.find({$text: {$search: "parasyte"}}, {title: 1, description: 1, _id: 0})
db.movies.find({$text: {$search: "fate"}}).sort({rating: -1})
```
