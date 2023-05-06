Tenemos mucha info podemos limitarla
```
g.E()
limitarlo a 4
g.E()limit(4)
```

Podemos hacer busquedas de diferente forma
```
g.V().has.('GamerAlias','skywalker123')
g.V().has.(label,'person')
g.V().hasId.('luke')
```
Podemos calcular el grado de entrada
grado de entrada= cuantas aristas ingresan
```
g.V().hasId.('MarioKart8').inE()
```

Podemos agrupar por ejemplo por cuantos grados de entrada tiene cada vertice
```
g.V().group().by(inE().count())
```

Podemos mejorar la consulta, agrupando dos veces, 
```
g.V().group().by().by(inE().count())
```

in y out devuelve el vertice, inE y outE retorna los vertices.
```
g.V().group().by().by(outE().count())
```


Calculemos cual es el promedio de gusto por weight del juego mario kart
```
g.V().hasId('MarioKart8').inE('likes').values('weight').mean()
```


Si yo soy mike a quien mas le gusta los juegos que yo juego
```
g.V().hasId('Mike').out('likes').in('likes')
```

Devuelven muchas veces todos. ¿Por que?
entonces dedupliquemos
```
g.V().hasId('Mike').out('likes').in('likes').dedup()
```

Pero no deberia salir yo mismo
```
g.V().hasId('Mike').as("myself").out('likes').in('likes').dedup().where(neq("myself"))
```

que es mas eficiente asi o cambiar el orden de dedup y where
```
g.V().hasId('Mike').as("myself").out('likes').in('likes').where(neq("myself")).dedup()
```

Es mejor lo que reduzca primero, entonces es mejor dedup y luego el where.


Que otros videojuegos me pueden gustar?
```
g.V().hasId('Mike').as("myself").out('likes').in('likes').dedup().where(neq("myself")).out('likes')
```

como quito los que a mi ya me gustan (agregado)
estos son los juegos que le gustan a mike (no borrar solo mostrar)
```
g.V().hasId('Mike').as("myself").out('likes')
```

As funciona con un solo vertice AGGREGATE funciona con una coleccion
```
g.V().hasId('Mike').as("myself").out('likes').aggregate('mygames').in('likes').dedup().where(neq("myself")).out('likes')
```

ahora retiramos los que ya estan en mi coleccion
```
g.V().hasId('Mike').as("myself").out('likes').aggregate('mygames').in('likes').dedup().where(neq("myself")).out('likes').where(neq('mygames'))
```

falla porque mygames no es un vertice es una coleccion
```
g.V().hasId('Mike').as("myself").out('likes').aggregate('mygames').in('likes').dedup().where(neq("myself")).out('likes').where(without('mygames'))
```

por ultimo deduplicamos para que no salga todo
```
g.V().hasId('Mike').as("myself").out('likes').aggregate('mygames').in('likes').dedup().where(neq("myself")).out('likes').dedup().where(without('mygames'))
```

le podemos meter peso, por ejemplo que me recomiende si al otro le gusta le gusta mas del 70%
podemos ordenar por numero de coincidencias
podemos meter autores, y recomendar por autores.
podemos volver las propiedades en vertices, 
entre mas complejo el grafo mas cosas cheveres podemos sacar
