---
title: Getting started
path: /docs/
---

# Getting started

Strawberry is a Python library for building [GraphQL APIs](https://graphql.org).

This guide will help you to create your first GraphQL API using Strawberry.

## Installation

To install Strawberry you can use your favourite dependency manager (pip, poetry
or pipenv). In this guide we’ll assume you’re working in a
[virtual env and using pip](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/).

To install Strawberry run the following command:

```shell
pip install strawberry-graphql
```

## Creating our first schema

Every GraphQL API has a schema, which defines all the types and fields available
in the API. There’s only one type that’s mandatory in a GraphQL API: `Query`.
This is where all the data of our API will come from.

Strawberry takes a code-first approach, where you use python code to define the
schema, as opposed to a schema-first approach where you write the schema first.

Strawberry uses [type hints](https://docs.python.org/3/library/typing.html) to
declare the types for the GraphQL fields.

Let’s create our first type. As mentioned we need to create a `Query` type. To
keep this example short let’s have only one field, called `hello`.

```python
import strawberry

@strawberry.type
class Query:
    hello: str
```

once we have our `Query` type we can create our GraphQL schema, Strawberry
provides a Schema class that can be used to create a schema from a `Query` type:

```python
schema = strawberry.Schema(Query)
```

So our full code will look like this:

```python
import strawberry

@strawberry.type
class Query:
    hello: str


schema = strawberry.Schema(Query)
```

The last step is try to the API, to quickly spin a server, you can use
Strawberry's builtin server command:

```shell
strawberry server schema
```

this will run a debug server on
[http://0.0.0.0:8000/graphql](http://0.0.0.0:8000/graphql). You will see the
GraphQL Playground an IDE for testing GraphQL APIs.

Let's run our first query! Copy the following code and paste into the
playground:

```gql
{
  hello
}
```

This is basically telling our server to fetch the value of the field `hello`.
