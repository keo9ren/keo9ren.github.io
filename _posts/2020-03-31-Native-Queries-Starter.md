---
layout: post
title: What no one told me about JPA Native Queries
--- 

Working with Java and JPA, this is the absolute minimum no need to know to start with _Native Queries_ 
and actually no one really told me.

Let's start with the definition of a simple Table as a JPA Entity called Pet. The table has three columns,
name (which is also the primary key), owner and color, both which are not terrible important for the example.

```java 

@Entity
@Table(name="PET")
class Pet { @Id public String name; public String owner; public String color; }

```

Basically you can now start and persist that Entity to a database. I used [H2][1] 
database for this example, because it comes bundled with the Wildfly application server, used.
E.g. like this:
```java
    class CreatePet {  
   
            @Inject
            EntityManager em;

            public Pet insert(String name) {
                Pet pet = new Pet();
                pet.name = name;
                em.persist(pet);
                return pet;
            }
    }
```

Retrieving all Pets from the database, with a _Native Queriy_, could be achieved with code like this.


```java
class GetPet {    
    
    @Inject
    EntityManager em;
    
    List<Pet> execute () {
        return (List<Pet>) em.createNativeQuery("Select PET.name from PET",Pet.class);
    }


}
```

Now, what if you only want to retrieve, the pets name only from the database, but are not interested in the other columns?
The simplest, shortest, possible solution is this: Write a new Pet entity with 
another name e.g. PetName and put in the fields you want to get from the database only.

```java 

@Entity
@Table(name="PET")
class PetName { @Id public String name; }

```

Then write the select like this.
```java

class Query {    
    @Inject
    EntityManager em;
    
    List<PetName> execute () {
        return (List<PetName>) em.createNativeQuery("Select PET.name from PET",Pet.class);
    }


}

```

The one thing you really have to take care of is, that the fields the entity must exactly match the fields selected.
So let's say you also want to select the pets color, because your requirements changed, put it in the PetName entity, as well as, in the select. 
Later on your requirements changing again and you don't want to have the color in your select remove the color from your select, as well as, from the PetName entity.

Just remember, always keep the two exactly in sync.

Most of this content should apply to all SQL databases, but it's actually only tested with the big O ones.
So due to the native nature of _Native Queries_ there might be small differences.

[1]: https://www.h2database.com/html/main.html
