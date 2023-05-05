

```
 ResultSet result = statement.executeQuery(
   "SELECT AVG(pr." + property + ") as AVERAGE FROM PERSONS p1" +
   "INNER JOIN KNOWS K ON k. person1 pl.id +
   "INNER JOIN PERSONS P2 ON p2.id k.person2 +
   "INNER JOIN CREATED C ON c.person = p2.id " +
   "INNER JOIN PROJECTS Pr ON pr.id c.project
   "WHERE p.name " + name + "');
   
 double avg = result.next().getDouble("AVERAGE");
```


```
  double avg = g.V().has("name",name).
         out("knows").out("created").
         values(property).mean().next();
```
