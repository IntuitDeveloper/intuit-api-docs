---
layout: default
title: Fragments
nav_order: 6
parent: GraphQL Concepts
---

# Fragments

Fragments are sets of fields. Instead of specifying a list of field names whenever you use them, create a fragment once and reuse it everywhere. 

```
query queryName {
  fieldName1
  fieldName2 {
    ...fragmentName
  }
}

fragment fragmentName on FieldName {
  field1
  field2
  field3
}
```