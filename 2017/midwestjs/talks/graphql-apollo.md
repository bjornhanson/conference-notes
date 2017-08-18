# Getting Started with GraphQL, Apollo, and React
- Speaker: [Ryan Glover](https://github.com/rglover), CEO, [Clever Beagle](https://github.com/cleverbeagle/)
- [GitHub repo](https://github.com/cleverbeagle/midwestjs-2017) used during talk with React, Apollo, GraphQL, Meteor

## Example request
```
{
  documents: {
    _id
    title
    body
  }
}
```

## GraphQL
- Get all data queries down to one HTTP GET where client tells server what it wants, not other way around
- Can get /users with their info and then their data all in one request
- Mutations: run in series (queries run in parallel) - helps avoid race conditions on writes
- Subscriptions (upcoming in spec)
- There are a couple GQBAAS (GraphQL back-end as a service)
- Schema (queries, mutations, and subscriptions) sit between data source (ex: MongoDB and UI)
- Resolvers (just a function) call data-storage-related queries
- Can use to update Redux data storage
- GraphQL can save a lot of time by making computed properties instead of having to on client (ex: combine `first_name` and `last_name` to `full_name`)
- You can get the exact data you need from the back-end, and nothing else

## Apollo
- Streamlines process of performing queries and mutations, as well as establishing subscriptions on the client
- `MongoDB <--> GraphQL Server <--> Apollo client`

Use http://localhost:4000/graphql in example repo to browse and test queries on server

## Resources
- [Pup Meteor/React boilerplate repo](https://github.com/cleverbeagle/pup) and [docs](http://cleverbeagle.com/pup/v1/introduction)
- [GraphQL](http://graphql.org)
- [The Meteor Chef](https://themeteorchef.com), a site Ryan runs
- [GraphiQL](https://github.com/graphql/graphiql) in-browser IDE for exploring GraphQL
