# Definition
(5) Collection Field: Collection fields should use ```Set``` instead of ```List``` due to performance concern.     
(6) Final Entity: Using final classes as entities would disable the lazy loading functionality.     
(7) Missing Identifier: Identifier field should be specified to uniquely determine an entity.    
(8) Missing No Argument Constructor: A no argument constructor should be implemented for Hibernate to generate an entity object using reflection.     
(9) Missing Equals Method: The default equals method compares the reference of objects, which is not ideal for comparing entities especially for collection-related operations.     
(10) Missing HashCode Method: HashCode method is vital for collections such as ```HashSets``` to determine equivalent entities.     
(11) Using Identifier in Equals or HashCode Methods: The identifier should not be used in equals and hashCode since all transient objects will be equal because their identifiers could be null.      
(12) Not Serializable: Entities which would leave the domain of JVM (i.e., detached) should implement the Serializable interface.       
(13) Missing Accessor Methods: JPA specification recommends implementing visible methods to access and to update private fields.    
(14) Local Pagination: Built-in pagination of ORM should be used instead of fetching all data and page locally.     