# References
S. Loli, L. Teixeira, B. Cartaxo. A Catalog of Object-Relational Mapping Code Smells for Java. SBES 2020: 82-91.

# Inter-Entity Smells
Inter-entity smells are caused by inappropriate definition of data retrieval strategies in entity relationships.

## Eager Fetch

Problem:     

```EAGER FetchType``` preloads all data in advance. However, they could be retrieved on demand to improve performance. 

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

We should join the field annotated with ```EAGER FetchType``` by join fetch presented in HQL to avoid N+1 problems. 

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


> The N + 1 problem occurs when an application gets data from the database, and then loops through the result of that data. That means we call to the database again and again and again. In total, the application will call the database once for every row returned by the first query (N) plus the original query ( + 1). 

For implementational details, please visit https://www.brentozar.com/archive/2018/07/common-entity-framework-problems-n-1/ 