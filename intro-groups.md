## Entendiendo por grupos

Vamos a cambiar las peras por manzanas para estar seguro que todo esta claro

Vayan al [Link](https://tinkerpop.apache.org/gremlin.html) donde aprenderemos de Gremlin como lenguaje declarativo para consulta de bases de datos orientadas a grafos.

Entendamos como funcionan las consultas que aparecen en la pagina

## Consulta 1
```
g.V().has("name","gremlin").
  out("knows").
  out("knows").
  values("name")
```
What are the names of Gremlin's friends' friends?

1. Get the vertex with name "gremlin."
2. Traverse to the people that Gremlin knows.
3. Traverse to the people those people know.
4. Get those people's names.

## Consulta 2
```
g.V().match(
  as("a").out("knows").as("b"),
  as("a").out("created").as("c"),
  as("b").out("created").as("c"),
  as("c").in("created").count().is(2)).
    select("c").by("name")
```
What are the names of the projects created by two friends?

1. ...there exists some "a" who knows "b".
2. ...there exists some "a" who created "c".
3. ...there exists some "b" who created "c".
4. ...there exists some "c" created by 2 people.
5. Get the name of all matching "c" projects.

## Consulta 3
```
g.V().has("name","gremlin").
  repeat(in("manages")).
    until(has("title","ceo")).
  path().by("name")
```
Get the managers from Gremlin to the CEO in the hierarchy.

1. Get the vertex with the name "gremlin."
2. Traverse up the management chain...
3. ...until a person with the title of CEO is reached.
4. ...Get name of the managers in the path traversed.

## Consulta 4
```
g.V().has("name","gremlin").as("a").
  out("created").in("created").
    where(neq("a")).
  groupCount().by("title")
```
Get the distribution of titles amongst Gremlin's collaborators.

1. Get the vertex with the name "gremlin" and label it "a."
2. Get Gremlin's created projects and then who created them...
3. ...that are not Gremlin.
4. Group count those collaborators by their titles.

## Consulta 5
```
g.V().has("name","gremlin").
  out("bought").aggregate("stash").
  in("bought").out("bought").
    where(not(within("stash"))).
  groupCount().order(local).by(values,desc)
```
Get a ranked list of relevant products for Gremlin to purchase.

1. Get the vertex with the name "gremlin."
2. Get the products Gremlin has purchased and save as "stash."
3. Who else bought those products and what else did they buy...
4. ...that Gremlin has not already purchased.
5. Group count the products and order by their relevance.


