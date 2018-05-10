# code snippets

All code snippets throughout the entire site should relate to each other. The data model in its entirety contains two types with relations to each other. In the cases where only one type is needed, the other one and the relation can simply be removed. We can also remove fields on the types if necessary. We shouldn't _add_ anything though. 

## Data model

```graphql
type User {
  id: ID! @unique
  name: String!
  email: String! @unique
  isAdmin: Boolean @default(value: "false")
  posts: [Post!]!
}

type Post {
  id: ID! @unique
  createdAt: DateTime!
  updatedAt: DateTime!
  title: String!
  author: User!
}
```

## Application schema

```graphql
type Query {
  users(where: UserWhereInput): [User!]!
  userConnection: UserConnection!
}

type Mutation {
  login(email: String!): UserAuthPayload
  signup(name: String!, email: String!): UserAuthPayload
  setAdmin(userId: ID!): User
  writePost(userId: ID!, title: String!): Post
  updateTitle(id: ID!, newTitle: String!): Post
}
```