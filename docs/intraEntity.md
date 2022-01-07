# References
[1] S. Loli, L. Teixeira, B. Cartaxo. A Catalog of Object-Relational Mapping Code Smells for Java. SBES 2020: 82-91.       
[2] T. M. Silva, D. Serey, J. C. A. de Figueiredo, J. Brunet. Automated design tests to check Hibernate design recommendations. SBES 2019: 94-103.

# An Example of Hibernate Entity
```java
@Entity @Table ("Person")
class Person {
 @Id @Column(name = id_person)
 private Integer id;
 private String name ;
 @ManyToOne (fetch = FetchType.EAGER)
 private Address address
}
```
Java ORM frameworks implement the Java Persistence API (JPA) in order to map the tables, columns, and relationships of trending RDBMS (Relational DataBase Management Systems) to the OOP-driven classes, attributes, and inheritance. For example, this class annotated with ```@Entity``` indicates that it is a Person entity in the ORM context, while the ```@Table``` annotation specifies its corresponding RDBMS data table Person. Moreover, ```@Id``` could be used to specify the unique identifier (in most cases, the corresponding field of the Primary Key of RDBMS data table, e.g., id_person), and relational annotations like ```@ManyToOne, @OneToMany``` could be used to describe relationships between entities with ```FetchType``` (e.g., ```EAGER, LAZY```) specified to determine whether data should be fetched in advance or on demand. 

# Problems of Intra-Entity Smells
**Collection Field**: Collection fields should use ```Set``` instead of ```List``` due to performance concern, e.g., an insertion after deletion in a ```List``` may cause Hibernate to remove all the entities and re-insert them.       
**Final Entity**: Using ```final``` classes as entities would disable the proxy functionality of Hibernate to enhance the performance of lazy loading. Thus, the ```LAZY FetchType``` will fall back to ```EAGER```, and no warning or error message will be thrown by Hibernate. As a result, the performance will be harmed silently.       
**Missing Identifier**:Identifier field should be specified to uniquely determine an entity. Otherwise, comparators of objects may be confused when dealing with data objects containing identical data from different rows.      
**Missing No Argument Constructor**: A no argument constructor should be implemented for Hibernate to generate an entity object using reflection, otherwise Hibernate will use Java reflection to initialize entities, which will consume more resources. Moreover, if Hibernate is used as a provider of JPA, it will throw an ```org.hibernate.InstantiationException```, and the application may crash since it may not be able to handle it.     
**Missing Equals Method**: The default ```equals``` method compares the reference of objects, which is not ideal for comparing entities especially for collection-related operations. The lack of an appropriate ```equals``` method will cause failure in reconnecting the detached entities, which may cause data persistence problems such as duplication.         
**Missing HashCode Method**: ```hashCode``` method is vital for collections such as ```HashSets``` to determine equivalent entities. The consequence of this smell is similar to Missing Equals Method.          
**Using Identifier in Equals or HashCode Methods**: The identifier should not be used in ```equals``` and ```hashCode``` since all transient objects will be equal because their identifiers could be null. The consequence of this smell is similar to Missing Equals Method.           
**Not Serializable**: Entities which would leave the domain of JVM (i.e., detached) should implement the ```Serializable``` interface.  Otherwise the serialization may fail, and Java will throw an ```exception``` called ```java.io.NotSerializableException```.      
**Missing Accessor Methods**: Although Hibernate does not require accessor methods, JPA specification recommends implementing visible methods to access and to update private fields.    

Remarks. We cover the usage of libraries such as Lombok and Apache Commons to generate ```equals```, ```hashCode```, and accessor (```getter```, ```setter```) methods. We may not be able to detect similar usage if practitioners use other libraries. 
# Local Pagination Smell

Problem:     

Built-in pagination of ORM should be used to fetch the data of each page instead of fetching all data and locally split them for pagination.        

Smelly Example:
```java
public List <Student> findStudents (int year){
  hql = " FROM Student d WHERE year = : year ";
  Query q = entityManager.createQuery (hql) ;...
}
```

```java
public List <Student> students (int year, int page, int limit){
  int fromIndex = (page - 1) * limit ;
  List<Student> students = findStudents(year);
  return students.subList(fromIndex , Math.min(fromIndex + limit , students.size()));
}
```

Solution:
```java
public List <Student> findStudents (int year, int fromIndex, int limit) {
  String hql = " FROM Student d WHERE year = : year ";
  Query q = entityManager.createQuery (hql);
  q.setFirstResult(fromIndex);
  q.setMaxResults(limit);
  return (List<Student>) q.getResultList();
}
```

Remarks: 

We locate the ```setMaxResults``` or ```setFirstResult``` method calls in parent methods with HQL appearance, and we analyze if the code component that called the method defines any ```Integer``` or ```Long``` object whose name contains ```page``` or ```limit```. This complies with the sample code of [1], which may be impractical, and may be improved in future.