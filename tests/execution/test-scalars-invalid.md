# test-scalar-email

#### server:

```graphql
scalar Email
scalar PhoneNumber

schema @server(port: 8000, graphiql: true, hostname: "localhost") {
  query: Query
}

type Query {
  email(value: Email!): Email! @const(data: "{{args.value}}")
  phone(value: PhoneNumber!): PhoneNumber! @const(data: "{{args.value}}")
}
```

#### assert:

```yml
- method: POST
  url: http://localhost:8000/graphql
  body:
    query: '{ email(value: "alo@invalid") }'
- method: POST
  url: http://localhost:8000/graphql
  body:
    query: '{ phone(value: "0") }'
- method: POST
  url: http://localhost:8000/graphql
  body:
    query: '{ phone(value: "1234567890") }'
```