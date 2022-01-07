# References
S. Loli, L. Teixeira, B. Cartaxo. A Catalog of Object-Relational Mapping Code Smells for Java. SBES 2020: 82-91.

# Inter-Entity Smells
Inter-entity smells are caused by inappropriate definition of data retrieval strategies in entity relationships.

## Eager Fetch

Problem:     

```EAGER FetchType``` preloads all data when the data class is initialized, even if some of them will never be accessed. To avoid performance issues (i.e., retrieving too much data in advance), data should be retrieved on demand. 

Smelly Example:     
```java
@Entity
class Student {
  @ManyToOne(fetch = FetchType.EAGER)
  private Person person ;
}
```

Solution:
```java
@Entity
class Student {
  @ManyToOne(fetch = FetchType.LAZY)
  private Person person ;
}
```

## Lacking Join Fetch
Problem:      

Fields annotated with ```EAGER FetchType``` should be joined by ```join fetch``` in HQL to be retrieved through one query using join. Otherwise, such fields would be retrieved by N additional queries if the parent object is initialized, resulting in the N+1 problem.

Smelly Example:     
```java
@Entity
class Student {
  @Id
  private Integer id;
  @ManyToOne (fetch = FetchType.EAGER )
  private Person person;
}
```
```java
public List<Student> findStudents(Integer id) {
    EntityManagerFactory emf = Persistence.createEntityManagerFactory(Student.class);
    String hql = " FROM Student d WHERE id = :id ";
    Query q = emf.createEntityManager().createQuery(hql);
    return (List<Student>) q.getResultList();
}
```

Solution:
```java
public List<Student> findStudents(Integer id) {
    EntityManagerFactory emf = Persistence.createEntityManagerFactory(Student.class);
    String hql = " FROM Student d join fetch d.person p WHERE id = :id ";
    Query q = emf.createEntityManager().createQuery(hql);
    return (List<Student>) q.getResultList();
}
```
## One-By-One
Problem:     

A collection annotated with ```@OneToMany``` or ```@ManyToMany``` using ```LAZY FetchType``` will fetched one-by-one in every loop iteration. ```@BatchSize``` should be involved to load  on demand and in batch. 

Smelly Example:
```java
@Entity
class Person {
 @OneToMany(fetch = FetchType.LAZY)
 private List <Student> students;
}
```

Solution:
```java
@Entity 
class Person {
 @OneToMany(fetch = FetchType.LAZY) @BatchSize(size=4)
 private List <Student> students;
}
```

## Missing ManyToOne 
Problem:    
Using ```@OneToMany``` annotation in a field without ```@ManyToOne``` presented in the corresponding field on the other side of the relationship may lead to performance issues such as N+1.      

Smelly Example:
```java
@Entity 
class Person {
 @OneToMany(fetch = FetchType.LAZY) @BatchSize(size=4)
 private List <Student> students;
}
```

```java
@Entity 
class Student {
 private Person person;
}
```

Solution:
```java
@Entity 
class Student {
 @ManyToOne (fetch = FetchType.LAZY)
 private Person person;
}
```

# The N+1 Problem


> The N + 1 problem occurs when an application retrieves a parent entity from the database, and then loops through a collection field of the entity containing N other entities. Hibernate may generate a query for every iteration to retrieve smelly entities, which means we call to the database recurrently. In total, the application will call the database once for every row (i.e., for N times) returned by the original query, and the plus one refers to the original query. This problem could lead to performance issue if the size of N is large. However, reducing N is not acceptable since we may need that large amount of data. The appropriate way to address it is to correctly configure the relationships between entities and the strategies of data fetching. For example, using the ```LAZY FetchType``` with specified ```BatchSize``` for on-demand batch retrieval. 

For implementational details, please visit https://www.brentozar.com/archive/2018/07/common-entity-framework-problems-n-1/ 