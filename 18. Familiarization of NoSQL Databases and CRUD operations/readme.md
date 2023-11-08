# Familiarization of NoSQL Databases and CRUD Operations

## Aim
Familiarization of NoSQL Databases and CRUD operations.

## Introduction
CRUD is an acronym for CREATE, READ, UPDATE & DELETE, which are rudimentary operations in the database. In this post, MongoDB is used as the primary database, a NoSQL database that stores data in a JSON format. CRUD operations are performed using Node.js, a language known for asynchronous, non-blocking operations. Both synchronous and asynchronous methods of performing CRUD operations are demonstrated.

## 2. Setting up MongoDB (NoSQL)
MongoDB is a document database that stores data in JSON-like documents. Two components are needed to set up MongoDB:
1. MongoDB Community Server
2. MongoDB Compass (GUI Viewer)

### MongoDB Compass (GUI Viewer for MongoDB)
After installing both applications, add the MongoDB server path to your environment variables. This is typically found in the MongoDB installation directory (e.g., `C:\Program Files\MongoDB\Server\4.4\bin`).

## 3. Synchronous Vs Asynchronous Execution
CRUD operations in Node.js can be performed in both synchronous (blocking) and asynchronous (non-blocking) ways. The choice depends on the use case.

## 4. Creating a Schema, Model, Object
A schema is like a blueprint that specifies what to store in the database and in which format. In this example, a movie database schema is created, defining properties such as movie name, director, IMDB rating, cast, release date, genre, and sequel.

## 5. CREATE (Synchronous)
A function `insertMovie` is created to insert movie data into the database synchronously. Function calls with input parameters update the database, and the inserted document is returned.

```javascript
const movieClass = require('./movieSchema')

// CREATE
async function insertMovie(name_, director_, rating_, cast_, date_, genre_, sequel_){
    const movieObject = new movieClass({
        movieName : name_,
        director: director_,
        imdbRating: rating_,
        cast: cast_,
        releaseDate: date_,
        genre: genre_,
        sequel: sequel_
    });
    result = await movieObject.save()
    return result
}

let output_1 = insertMovie('Inception', 'Christopher Nolan', 7, ['Leonardo DiCaprio', 'Cillian Murphy'], new Date('2010-07-16'),
    'science-fiction', false)
output_1.then(function(response) {
    console.log(response, 'output response')
})
```

## 6. CREATE (Asynchronous)
Documents can be inserted into the MongoDB database asynchronously, without waiting or blocking code execution.

```javascript
const movieClass = require('./movieSchema')

// CREATE
var theDarkKnight = new movieClass({
    movieName: "The dark knight",
    director: "Christopher Nolan",
    imdbRating: 8,
    cast: ["Christian Bale", "Heath Ledger"],
    releaseDate: new Date('2008-01-14'),
    genre: "superhero",
    sequel: true
})
console.log('DB Updated');
theDarkKnight.save()

var djangoUnchained = new movieClass({
    movieName: "Django Unchained",
    director: "Quentin Tarantino",
    imdbRating: 8,
    cast: ["Christoph Waltz", "Jamie Foxx"],
    releaseDate: new Date('2012-12-12'),
    genre: "revisionist Western",
    sequel: false
})
console.log('DB Updated');
djangoUnchained.save()

var theNun = new movieClass({
    movieName: "The Nun",
    director: "Corin Hardy",
    imdbRating: 6,
    cast: ["Taissa Farmiga", "Demián Bichir"],
    releaseDate: new Date('2018-09-04'),
    genre: "supernatural horror",
    sequel: false
})
console.log('DB Updated');
theNun.save()
```

In this way, three sets of movies are added without blocking code execution.
