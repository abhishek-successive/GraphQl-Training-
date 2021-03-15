<h3>What is GraphQl?</h3>

**GraphQL** is a query Language  for your API and a Server Side runtime for executing queries by using a type system you define for your data . GraphQl isn't tied to any specific database  or storage  engine and is instead by your existing code and data. 
      A GraphQL service is created by defining types and fields on those types, then providing functions for each field on each type. For example, a GraphQL service that tells us who the logged in user is (me) as well as that user's name might look something like this:

      type Query {
          me : User
      }
      type : User {
          id:ID 
          name:String
      }


<h3>Difference between Rest and GraphQL?</h3>


**REST API**:

    REST (Representational State Transfer) is an API design architecture used to implement web services. REST-compliant web services allow the requesting systems to access and manipulate textual representations of web resources by using a uniform and predefined set of stateless operations. When HTTP is used, the most common operations available are GET, POST, PUT, and DELETE.
        The core concept of REST is that everything is a resource. While REST was a great solution when it was first proposed, there are some pretty significant issues that the architecture suffers from right now.
 
    Rest API Aprroach:
    {
    "title":"DaudGang",
    "description":"Underworld Gang",
    "category": "criminal"
    }


**GraphQL** : 

    As REST, GraphQL is an API design architecture, but with a different approach which is much flexible. The main and most important difference is that GraphQL is not dealing with dedicated resources. Instead everything is regarded as a graph and therefore is connected. This means that you can tailor the request (query) to your exact needs by using the GraphQL query language and describing what you would like to get as an answer. You can combine different entities in one query and you are able to specific which attributes should be included in the response on every level, e.g.:
{
     post(id: 1) {
        title
        user {
            name
            email
            courses {
                title
            }
        }
     }
}

<h3>GraphQL Schema?</h3>

  Your GraphQL server uses a schema to describe the shape of your data graph. This schema defines a hierarchy of types with fields that are populated from your back-end data stores. The schema also specifies exactly which queries and mutations are available for clients to execute against your data graph.

This article describes the fundamental building blocks of a schema and how to create one for your GraphQL server.

The GraphQL specification includes a human-readable schema definition language (or SDL) that you use to define your schema and store it as a string.

Here's a short example schema that defines two object types: Book and Author:

    type Book {
  title: String
  author: Author
}

type Author {
  name: String
  books: [Book]
}

<h3>What is Queries and Mutations</h3>

 **Queries and Mutations consists of Fields,Arguments,Aliases,Fragments,Operation,Name,Variables,Directives,Mutations,Inline Fragments.**

a)Fields : At its simplest, GraphQL is about asking for specific fields on objects. Let's start by looking at a very simple query and the result we get when we run it:

    GraphQL Aprroach:
{
      hero {
    name    
  }
}

    Rest Aprroach:

{
  "data": {
    "hero": {
      "name": "R2-D2"
    }
  }
}

b)Arguments :If the only thing we could do was traverse objects and their fields, GraphQL would already be a very useful language for data fetching. But when you add the ability to pass arguments to fields, things get much more interesting.

GraphQL Aprroach:
{
  human(id: "1000") {
    name
    height
  }
}

 Rest Aprroach:
{
  "data": {
    "human": {
      "name": "Luke Skywalker",
      "height": 1.72
    }
  }
}

c)Aliases: If you have a sharp eye, you may have noticed that, since the result object fields match the name of the field in the query but don't include arguments, you can't directly query for the same field with different arguments. That's why you need aliases - they let you rename the result of a field to anything you want.

GraphQl Aprroach:

{
  empireHero: hero(episode: EMPIRE) {
    name
  }
  jediHero: hero(episode: JEDI) {
    name
  }
}

Rest Aprroach:

{
  "data": {
    "empireHero": {
      "name": "Luke Skywalker"
    },
    "jediHero": {
      "name": "R2-D2"
    }
  }
}

d) Mutations : Most discussions of GraphQL focus on data fetching, but any complete data platform needs a way to modify server-side data as well.

In REST, any request might end up causing some side-effects on the server, but by convention it's suggested that one doesn't use GET requests to modify data. GraphQL is similar - technically any query could be implemented to cause a data write. However, it's useful to establish a convention that any operations that cause writes should be sent explicitly via a mutation.

Just like in queries, if the mutation field returns an object type, you can ask for nested fields. This can be useful for fetching the new state of an object after an update. Let's look at a simple example mutation:


GraphQl Aprroach:

mutation CreateReviewForEpisode($ep: Episode!, $review: ReviewInput!) {
  createReview(episode: $ep, review: $review) {
    stars
    commentary
  }
}

variables : {
  "ep": "JEDI",
  "review": {
    "stars": 5,
    "commentary": "This is a great movie!"
  }
}

Rest Approach :
{
  "data": {
    "createReview": {
      "stars": 5,
      "commentary": "This is a great movie!"
    }
  }
}

