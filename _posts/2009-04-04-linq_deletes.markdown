---
layout: post
title: "Linq Deletes"
---

# Linq Deletes

# Summary

You can use the goodness that is the Linq syntax to delete data from your database. It's important to note that SubSonic IS NOT AN ORM - it's a query tool (subtle difference) and therefore it doesn't do object tracking. There's nothing stopping you from creating a. This is fine and dandy if you like working that way - but we think this is a Big Lie.   The web is a stateless medium - this sort of "contextual tracking" is just not the Real World and we don't drink that beer.  

## Setup

Make sure you configure SubSonic by adding a reference, setting up your DB connection, and then adding the templates to your project.  

## Simple Deletes

You can work with the 
This creates the following SQL: 

 ```sql
DELETE FROM [dbo].[Products]  WHERE [dbo].[Products].[ProductID] = 1
``` 

### Using the Repository

There are 2 ways to delete using the IRepository generated for you: 

 ```csharp
var repo = new NorthwindRepository<Product>();
repo.Delete(1);
```

or

 ```csharp
var repo = new NorthwindRepository<Product>();
var product = repo.GetByKey(1);
repo.Delete(product); 
```

### Multiple Deletes

You can delete multiple objects transactionally using Batch Query: 

 ```csharp
var repo = new NorthwindRepository<Product>();
var queue = new List<Product>();
for (int i = 1; i < 10; i++)
  {
    var product = repo.GetByKey(i);
    queue.Add(product);
   }
repo.Delete(queue);
```
