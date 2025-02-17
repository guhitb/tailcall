# expr logic

#### server:

```graphql
schema {
  query: Query
}

type Query {
  andTrue1: Boolean @expr(body: {and: [{const: true}, {const: true}, {const: true}]})
  andTrue2: Boolean @expr(body: {and: [{const: true}, {const: true}]})
  andFalse3: Boolean @expr(body: {and: [{const: true}, {const: false}, {const: true}]})
  andFalse1: Boolean @expr(body: {and: [{const: false}, {const: true}]})
  andFalse2: Boolean @expr(body: {and: [{const: false}, {const: false}]})

  isEmptyTrue1: Boolean @expr(body: {isEmpty: {const: null}})
  isEmptyTrue2: Boolean @expr(body: {isEmpty: {const: ""}})
  isEmptyTrue3: Boolean @expr(body: {isEmpty: {const: []}})
  isEmptyTrue4: Boolean @expr(body: {isEmpty: {const: {}}})
  isEmptyFalse1: Boolean @expr(body: {isEmpty: {const: 10}})
  isEmptyFalse2: Boolean @expr(body: {isEmpty: {const: false}})
  isEmptyFalse3: Boolean @expr(body: {isEmpty: {const: "abc"}})

  notTrue: Boolean @expr(body: {not: {const: false}})
  notFalse1: Boolean @expr(body: {not: {const: true}})
  notFalse2: Boolean @expr(body: {not: {const: 1}})

  orFalse1: Boolean @expr(body: {or: [{const: false}, {const: false}]})
  orFalse2: Boolean @expr(body: {or: [{const: false}, {const: false}, {const: false}]})
  orTrue1: Boolean @expr(body: {or: [{const: false}, {const: true}]})
  orTrue2: Boolean @expr(body: {or: [{const: true}, {const: false}]})
  orTrue3: Boolean @expr(body: {or: [{const: false}, {const: true}, {const: false}]})

  condZero: Int @expr(body: {cond: [{const: 0}, [[{const: false}, {const: 1}], [{const: false}, {const: 2}]]]})
  condOne: Int @expr(body: {cond: [{const: 0}, [[{const: true}, {const: 1}], [{const: true}, {const: 2}]]]})
  condTwo: Int @expr(body: {cond: [{const: 0}, [[{const: false}, {const: 1}], [{const: true}, {const: 2}]]]})

  defaultToZero: Int @expr(body: {defaultTo: [{const: null}, {const: 0}]})
  defaultToTrue: Boolean @expr(body: {defaultTo: [{const: ""}, {const: true}]})

  ifZero: Int @expr(body: {if: {cond: {const: true}, then: {const: 0}, else: {const: 1}}})
  ifOne: Int @expr(body: {if: {cond: {const: false}, then: {const: 0}, else: {const: 1}}})
}
```

#### assert:

```yml
- method: POST
  url: http://localhost:8080/graphql
  body:
    query: query { andTrue1 andTrue2 andFalse3 andFalse1 andFalse2 isEmptyTrue1 isEmptyTrue2 isEmptyTrue3 isEmptyTrue4 isEmptyFalse1 isEmptyFalse2 isEmptyFalse3 notTrue notFalse1 notFalse2 orFalse1 orFalse2 orTrue1 orTrue2 orTrue3 condZero condOne condTwo defaultToZero defaultToTrue ifZero ifOne }
```
