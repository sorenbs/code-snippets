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
    isAdmin
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
        "name": "Arnold Anderson",
        "isAdmin": false
      }
    ]
  }
}
```

# Filtering & Ordering

### With Prisma

```js
const Query = {
  searchAdminPosts: (_, args, context, info) => {
    return context.prisma.query.posts(
      {
        where: {
          title_contains: args.title,
          author: {
            isAdmin: true,
          },
        },
        orderBy: id_DESC,
      },
      info
    )
  },
}
```

### Without Prisma

```js
const Query = {
  searchAdminPosts: (_, args, context, info) => {
    return BlackMagic.getPosts()
  }
}
```

### Schema

```graphql
type Query {
  searchAdminPosts: [Post!]!
}

type User {
  id: ID!
  name: String!
  isAdmin: Boolean
}

type Post {
  id: ID! @unique
  createdAt: DateTime!
  title: String!
  author: User!
}
```

### Query

```graphql
{
  searchAdminPosts(title: "Content Marketing") {
    title
    author: {
      name
    }
  }
}
```

### Response

```graphql
{
  "data": {
    "searchAdminPosts": [
      {
        "title": "Strategic memo on Content Marketing",
        "author": {
          "name": "John Schmidt"
        }
      }
    ]
  }
}
```

# Mutations

### With Prisma

```js
const Mutation = {
  createPost: (_, args, context, info) => {
    return context.prisma.mutation.craetePost(
      {
        data: {
          title: args.title,
          author: {
            connect: { email: args.authorEmail },
          },
        },
        orderBy: id_DESC,
      },
      info
    )
  },
}
```

### Without Prisma

```js

```

### Schema

```graphql
type Mutation {
  craetePost: [Post!]!
}

type User {
  id: ID!
  name: String!
  isAdmin: Boolean
}

type Post {
  id: ID! @unique
  createdAt: DateTime!
  title: String!
  author: User!
}
```

### Query

```graphql
mutation {
  createPost(data: {
    title: "The power of Content Marketing"
    authorEmail: "marketing@company.com"
  }) {
    id
  }
}
```

### Response

```graphql
{
  "data": {
    "createPost": [
      {
        "id": "cjh0puo0b0000dvpi7b2e87c7",
        "title": "The power of Content Marketing",
        "authorEmail": "marketing@company.com"
      }
    ]
  }
}
```

