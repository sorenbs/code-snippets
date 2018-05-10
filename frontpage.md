## Basic Resolver

### With Prisma

```js
const Query = {
  userList: (_, args, context, info) => {
    return context.prisma.query.users({}, info)
  }
}
```

### Without Prisma

```js
const Query = {
  userList: (_, args, context, info) => {
    return BlackMagic.getData()
  }
}
```

### Schema

```graphql
type Query {
  userList: [User!]!
}

type User {
  id: ID!
  name: String!
  isAdmin: Boolean
}
```

### Query

```graphql
{
  userList {
    name
    isAfmin
  }
}
```

### Response

```graphql
{
  "data": {
      "userList": [
        {
          "name": "Jane Dixie",
          "isAdmin": true
        },
        {
          "name" : "Arnold Anderson",
          "isAdmin": false
        }
      ]
  }
}
```

# Filtering & Ordering

### With Prisma

```js

```

### Without Prisma

```js

```

### Schema

```graphql

```

### Query

```graphql

```

### Response

```graphql

```

# Mutations

### With Prisma

```js

```

### Without Prisma

```js

```

### Schema

```graphql

```

### Query

```graphql

```

### Response

```graphql

```

