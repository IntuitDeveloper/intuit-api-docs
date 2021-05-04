---
layout: default
title: Benefits of GraphQL
nav_order: 8
parent: GraphQL Concepts
---

## Benefits of GraphQL

Why is the Ecosystem API built in GraphQL? Here are some of the reasons that make GraphQL so compelling.

#### Single endpoint

Imagine a use-case where you want to get all the invoices created within a date range along with the items sold and the name and address of the customer for each invoice. You’d need to make several calls to different endpoints to achieve this. One for the Invoice, one for each Customer, and one for each Item. GraphQL has one endpoint for everything, all of this data can be obtained by making one call to a single endpoint.

#### Only get what you need

In the use-case described above, each call would give you all the information about the entity you’ve queried. You may not need the account information or the payment status on the invoice, for example. With a GraphQL query, specify which fields you want and only those will be returned. 

#### Validate your request

Because GraphQL is a type system and everything about it is part of its schema, it’s easy to check if your request is valid or not while it’s being created. You don’t have to wait till runtime to know if your request is invalid. There are multiple ways to validate a request: use a GraphQL tool (which has a built-in parser), use introspection queries to check the schema, or let the server validate the request against the schema version on the server.

#### Everything is documented

Accurate and up-to-date documentation is always available along with the schema. Think of GraphQL as self-documenting. The concept of introspection allows you to have information about the schema, fields (including type and description) and supported operations anytime you need it. 
