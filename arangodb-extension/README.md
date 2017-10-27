# ArangoDB-extension

![ArangoDB Project](https://github.com/JNOSQL/jnosql-site/blob/master/assets/img/logos/arangodb.png)


ArangoDB extension has implementations to use specific behavior that is beyond the API such as AQL.

## ArangoDBRepository

ArangoDBRepository is an extension of Repository that allows using AQL annotation that executes AQL.


```java
    interface PersonRepository extends ArangoDBRepository<Person, String> {

        @AQL("select * from Person")
        List<Person> findAll();

        @AQL("select * from Person where name = @name")
        List<Person> findByName(@Param("name") String name);
    }
```

## ArangoDBRepositoryAsync

ArangoDBRepositoryAsync is an extension of RepositoryAsync that allows using AQL annotation that executes AQL.


```java
    interface PersonAsyncRepository extends ArangoDBRepositoryAsync<Person, String> {

        Person findByName(String name);


        @AQL("select * from Person where name= $name")
        void queryName(@Param("name") String name);

        @AQL("select * from Person where name= $name")
        void queryName(@Param("name") String name, Consumer<List<Person>> callBack);
    }
```


## ArangoDBTemplate and ArangoDBTemplateAsync

ArangoDBTemplate is a specialization of Document Template that allows using AQL both synchronous and asynchronous.

```java
        template.aql("select * from Person where name = @name", params);

        String query = "select * from Person where name = ?";
        Consumer<List<Person>> callBack = p -> {
        };
        JsonObject params = JsonObject.create().put("name", "Ada");
        templateAsync.aql(query, params, callBack);

```