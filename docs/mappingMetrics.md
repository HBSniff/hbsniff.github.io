# References
[1] S. Holder, J. Buchan, S. G. MacDonell. Towards a Metrics Suite for Object-Relational Mappings. MBSDI 2008. 43-54.     
[2] M. Bouschen. JPA PITFALLS (5): OBJECT-RELATIONAL MAPPING AND INHERITANCE. https://blog.akquinet.de/2020/03/29/jpa-pitfalls-5-object-relational-mapping-and-inheritance/

# Inheritance Mapping Strategies
>Inheritance is undoubtedly the most obvious impedance mismatch between an object-oriented domain model and a relational database schema.   - Vlad Mihalcea

There is a trade-off between data redundancy and performance. 

   ### One Class - One Table (InheritanceType.JOINED)
This strategy distributes object data over multiple tables.    
In order to link these tables, all tables share the same primary key.    
PROS: Non-null, no redundant data.    
CONS: Low performance.    


   ### One Inheritance Tree – One Table (InheritanceType.SINGLE_TABLE)
All classes of an inheritance hierarchy are mapped to the same relational table.      
PROS: Better performance, no join.      
CONS: Null values.     

   ### One Inheritance Path – One Table (InheritanceType.TABLE_PER_CLASS)
This mapping strategy only maps each **concrete** class to a table.    
PROS: Non-null.    
CONS: Redundant data, may result in low performance if superclasses are not abstract [2].     

# Definitions and Goals of the metrics  
Mapping metrics [1] are designed to evaluate data redundancy and performance of entities related to inheritance. Note that the threshold to determine a bad practice should be investigated further.      

**Table Accesses for Type Identification (TATI)**: The number of tables needed to identify the requested type of entity. Higher TATI indicates more queries will be executed to construct an object of the entity.    

**Number of Corresponding Tables (NCT), Deisgned for the JOINED strategy**: The number of tables that contain data of an entity, which measures object retrieval performance. The impact of higher NCT is similar to higher TATI.

**Number of Corresponding Relational Fields (NCRF), Deisgned for the TABLE_PER_CLASS strategy**: The number of relational fields in all tables that correspond to each non-inherited non-key field of an entity, which measures change propagation.  Higher NCRF indicates more queries will be executed to change data of an entity since there exists data redundancy in terms of the relational fields.

**Additional Null Values (ANV), Deisgned for the SINGLE_TABLE strategy**: The number of null values in the row of union superclasses, which measures the data redundancy. Higher ANV indicates more storage space is used to store null values since entities affected by such a problem are likely to be stored with other entities (with nonidentical fields) in the same table.          

# Remarks

Current Hibernate version does not support mixed inheritance strategy, so our implementation is slightly different from paper [1].      
see also: Mixing inheritance is not allowed. https://hibernate.atlassian.net/browse/HHH-7181