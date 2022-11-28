<a href="https://www.mongodb.com/docs/">
    <img src="https://upload.wikimedia.org/wikipedia/commons/9/93/MongoDB_Logo.svg" alt="Monogo Db logo" title="Aimeos" align="right" height="60" />
</a>

# Ejercicio práctico de MongoDB

1. Para resolver este ejercicio se utilizara el 'mongo shell' de MongoDB.

3. Debe conectarse a una instancia activa de mongod, se puede utilizar la base de datos test, o crear una nueva llamada mongo\_movies, o crear otra a elección.

5. Documentar todas sus consultas en un archivo, para usar como referencia y almacenarlo en su repositorio particular.

## Documentos a Insertar

[Link JSON a insertar](https://raw.githubusercontent.com/alcalino-1978/upgrade-mongo-exercises/master/movies.json "Link JSON a insertar")

Insertar los siguientes documentos en una colección llamada **movies**. 

	db.movies.insertMany([
        {
            "title": "Fight Club",
            "writer": "Chuck Palahniuk",
            "year": 1999,
            "actors": [
                "Brad Pitt",
                "Edward Norton"
            ]
        },
        {
            "title": "Pulp Fiction",
            "writer": "Quentin Tarantino",
            "year": 1994,
            "actors": [
                "John Travolta",
                "Uma Thurman"
            ]
        },
        {
            "title": "Inglorious Basterds",
            "writer": "Quentin Tarantino",
            "year": 2009,
            "actors": [
                "Brad Pitt",
                "Diane Kruger",
                "Eli Roth"
            ]
        },
        {
            "title": "The Hobbit: An Unexpected Journey",
            "writer": "J.R.R. Tolkein",
            "year": 2012,
            "franchise": "The Hobbit"
        },
        {
            "title": "The Hobbit: The Desolation of Smaug",
            "writer": "J.R.R. Tolkein",
            "year": 2013,
            "franchise": "The Hobbit"
        },
        {
            "title": "The Hobbit: The Battle of the Five Armies",
            "writer": "J.R.R. Tolkein",
            "year": 2012,
            "franchise": "The Hobbit",
            "synopsis": "Bilbo and Company are forced to engage in a war against an array of combatants and keep the Lonely Mountain from falling into the hands of a rising darkness."
        },
        {
            "title": "Pee Wee Herman's Big Adventure"
        },
        {
            "title": "Avatar"
        }
    ])
	
## Consultas / Buscar documentos

Realizar las siguientes consultas en la colección movies:

**1. Obtener todos los documentos**
```mongo
db.movies.find()
```
[Run code >](https://mongoplayground.net/p/RvjCAgC3g_5 "Abrir ejemplo en Mongo playground")

**2. Obtener documentos con writer igual a *"Quentin Tarantino"***
```mongo
db.movies.find({"writer": "Quentin Tarantino"})
```
[Run code >](https://mongoplayground.net/p/--cPcsd0_sA)

**3. Obtener documentos con actors que incluyan a *"Brad Pitt"***
```mongo
db.movies.find({actors: "Brad Pitt"})
```
[Run code >](https://mongoplayground.net/p/2D6uNEAMRUg)

**4. Obtener documentos con franchise  igual a *"The Hobbit"***
```mongo
db.movies.find({franchise: "The Hobbit"})
```
[Run code >](https://mongoplayground.net/p/C6odyhVKiUh)

**5. Obtener todas las películas de los 90s.**
```mongo
db.movies.find({year: {$gte: 1990,$lt: 2000}})
```
[Run code >](https://mongoplayground.net/p/p_yaihFB_32)

**6. Obtener las películas estrenadas entre el año 2000 y 2010.**
```mongo
db.movies.find({year: {$gte: 2000,$lte: 2010}})
```
[Run code >](https://mongoplayground.net/p/VplcnmCIe6v)

## Actualizar Documentos

**1. Agregar sinopsis a *"The Hobbit: An Unexpected Journey"* : "*A reluctant hobbit, Bilbo Baggins, sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home - and the gold within it - from the dragon Smaug."***
```mongo
db.movies.updateOne({"title": "The Hobbit: An Unexpected Journey"},{$set: {"synopsis": "A reluctant hobbit, Bilbo Baggins, sets out to the Lly Mountain with a spirited group of dwarves to reclaim their mountain home - and the gold within it - from the dragon Smaug."}})
```
[Run code >](https://mongoplayground.net/p/YaIyLT0buWb)

**2. Agregar sinopsis a *"The Hobbit: The Desolation of Smaug"* : *"The dwarves, along with Bilbo Baggins and Gandalf the Grey, continue their quest to reclaim Erebor, their homeland, from Smaug. Bilbo Baggins is in possession of a mysterious and magical ring."***
```mongo
db.movies.updateOne({"title": "The Hobbit: The Desolation of Smaug"},{$set: {"synopsis": "The dwarves, along with Bilbo Baggins and Gandalf the Grey, continue their quest to reclaim Erebor, their homeland, from Smaug. Bilbo Baggins is in possession of a mysterious and magical ring."}})
```
[Run code >](https://mongoplayground.net/p/lYr9kRdBhGF)

**3. Agregar una actor llamado "Samuel L. Jackson" a la película "Pulp Fiction"**
```mongo
db.movies.updateOne({title: "Pulp Fiction"},{$push: {actors: "Samuel L. Jackson"}})
```
[Run code >](https://mongoplayground.net/p/n1YcDSHKDTS)

## Búsqueda por Texto / Text Search

**1. Encontrar las películas que en el título contengan la palabra "Hobbit"**
```mongo
db.movies.find({title: {$regex: "Hobbit"}})
```
[Run code >](https://mongoplayground.net/p/7YhhgvvzRGy)

**2. Encontrar las películas que en la sinopsis contengan la palabra "Gandalf"**
```mongo
db.movies.find({synopsis: {$regex: "Gandalf"}})
```
[Run code >](https://mongoplayground.net/p/AcooZyyWqPP)

**3. Encontrar las películas que en la sinopsis contengan la palabra "Bilbo" y no la palabra "Gandalf"**
```mongo
db.movies.find({$and: [{synopsis: {$regex: "Bilbo"}},{synopsis: {$not: {$regex: "Gandalf"}}}]})
```
[Run code >](https://mongoplayground.net/p/eiX87agnfQl)

**4. Encontrar las películas que en la sinopsis contengan la palabra "dwarves" ó "hobbit"**
```mongo
db.movies.find({$or: [{synopsis: {$regex: "dwarves", $options: "i"}},{synopsis: {$regex: "hobbit", $options: "i"}}]})
```
[Run code >](https://mongoplayground.net/p/OjnB1qBCtJg)

**5. Encontrar las películas que en la sinopsis contengan la palabra "gold" y "dragon"**
```mongo
db.movies.find({$and: [{synopsis: {$regex: "gold", $options: "i"}},{synopsis: {$regex: "dragon", $options: "i"}}]})
```
[Run code >](https://mongoplayground.net/p/6MxsA6-qtRs)

## Eliminar Documentos

**1. Eliminar la película "Pee Wee Herman's Big Adventure"**
```mongo
db.movies.remove({title: "Pee Wee Herman's Big Adventure"})
```

**2. Eliminar la película "Avatar"**
```mongo
db.movies.remove({title: "Avatar"})
```
