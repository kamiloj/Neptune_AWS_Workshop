## Taller

**Sobre la base de datos Neptuno ubicada en [https://gremlify.com/ilz8s5400hn/7](https://gremlify.com/ilz8s5400hn/7)**

## 1. ¿En qué actividades se encuentra interesado williamsbradley?

**Ejemplo amy81**

```markdown
[
  "Naturaleza",
  "Cocina",
  "Carpintería",
  "Deportes"
]
```

**Ejemplo kennedyjoseph**

```markdown
[
  "Cocina"
]
```

## 2. ¿Quiénes son las 5 personas más populares de la red social y cuántas personas las siguen?

**Ejemplo**

```markdown
El usuario más popular es morenojason con 6 seguidores.

[
  {
    "morenojason": 6
  }
]
```

si order y limit no funciona agregar como primer parámetro la palabra local

order(local)
limit(local,10)

## 3. ¿Cuál es el top 3 de usuarios que me recomiendan seguir?

**Dicho de un modo más específico, ¿cuál es el top 3 de usuarios que tienen más seguidores directos (follows) en común con el usuario williamsbradley y que dicho usuario no está siguiendo actualmente?**

**Ejemplo amy81**

```markdown
[
  {
    "rodriguezjoseph": 9
  },
  {
    "michaelunderwood": 8
  },
  {
    "natasha09": 7
  }
]
```

**Ejemplo kennedyjoseph**

```markdown
[
  {
    "michaelunderwood": 3
  },
  {
    "warrenpaul": 2
  },
  {
    "paullaurie": 2
  }
]
```

**Ejemplo gráfico**

![Texto alternativo](https://d1.awsstatic.com/Getting%20Started/aws-labs-friend-recommendation-engine/friend-rec-diagram.44286a071134c67ce1ad790715d8e689ff3c1507.png)

**Explicación:**

Si soy el usuario MyUser, entonces SimilarSam y MirrorMax son seguidores directos en común con los usuarios que sigo, ellos siguen a InterestingIngrid, por lo cual es posible que también me interese seguir esta cuenta.

Pero no recomendamos a PopularPolly porque actualmente ya la sigo.

