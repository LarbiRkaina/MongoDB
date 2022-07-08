# Laboratorio 2 -- Mongodb 🍃

## Restaurar backup
  - La base de datos a restaurar [airbnb](https://drive.google.com/drive/folders/1gAtZZdrBKiKioJSZwnShXskaKk6H_gCJ?usp=sharing)
  
  - Para restaurarlo puede seguir las instrucciones de este videopost: [restaurando backup en mongo](https://www.lemoncode.tv/curso/docker-y-mongodb/leccion/restaurando-backup-mongodb)

> Acuerdate de mirar si en opt/app hay contenido de backups previos que tengas que borrar


## General

En este base de datos puedes encontrar un montón de apartementos y sus reviews, esto está sacado de hacer webscrapping.

Pregunta Si montarás un sitio real, ¿Qué posible problemas pontenciales les ves a como está almacenada la información?

## Consultas
### Básico

1. Saca en una consulta cuantos apartamentos hay en España.

```javascript
//TODO pegar consulta prueba subida trabajo

db.listingsAndReviews.countDocuments(
{
"address.country": "Spain"
}  
)

```

2. Lista los 10 primeros:
        Sólo muestra: nombre, camas, precio, government_area
        Ordenados por precio.

```javascript
//TODO pegar consulta
db.listingsAndReviews.find(
  {
  "address.country": "Spain"
  },
  {
    _id:0,
    name:1,
    beds:1,
    price:1,
    "address.government_area":1
  }
).limit(10).sort("price")

```

### Filtrando

1. Queremos viajar comodos, somos 4 personas y queremos:
        4 camas.
        Dos cuartos de baño.

```javascript
//TODO pegar consulta
db.listingsAndReviews.find(
 {
  $and:[
    {beds:4},
    {bathrooms: 2}
  ]
 }
)
```

2. Al requisito anterior,hay que añadir que nos gusta la tecnología queremos que el apartamento tenga wifi.

```javascript
//TODO pegar consulta
db.listingsAndReviews.find(
 {
  $and:[
    {beds:4},
    {bathrooms: 2},
    {amenities: 'Wifi'}
  ]
 },
)
```

3. Y bueno, un amigo se ha unido que trae un perro, así que a la query anterior tenemos que buscar que permitan mascota Pets Allowed

```javascript
//TODO pegar consulta
db.listingsAndReviews.find(
 {
  $and:[
    {beds:4},
    {bathrooms: 2},
    {amenities: 
      {
        "$all": ["Wifi","Pets allowed"]
      }
    
    }
  ]
 },
)

```

### Operadores lógicos

1. Estamos entre ir a Barcelona o a Portugal, los dos destinos nos valen, peeero... queremos que el precio nos salga baratito (50 $), y que tenga buen rating de reviews

```javascript
//TODO pegar consulta
```

## Agregaciones
### Basico

1. Queremos mostrar los pisos que hay en España, y los siguiente campos:
        Nombre.
        De que ciudad (no queremos mostrar un objeto, sólo el string con la ciudad)
        El precio (no queremos mostrar un objeto, sólo el campo de precio)

```javascript
//TODO pegar consulta
```

2. Queremos saber cuantos alojamientos hay disponibles por pais.

```javascript
//TODO pegar consulta
```

## Opcional

1. Queremos saber el precio medio de alquiler de airbnb en España.

```javascript
//TODO pegar consulta
```

2. ¿Y si quisieramos hacer como el anterior, pero sacarlo por paises?

```javascript
//TODO pegar consulta
```

3. Repite los mismos pasos pero agrupando también por numero de habitaciones.

```javascript
//TODO pegar consulta
```

## Desafío

1. Queremos mostrar el top 5 de apartamentos más caros en España, y sacar los siguentes campos:

    Nombre.
    Ciudad.
    Amenities, pero en vez de un array, un string con todos los ammenities.

```javascript
//TODO pegar consulta
```
