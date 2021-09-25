# Definition
(1) Eager Fetch:  ```EAGER FetchType``` preloads all data in advance. However, they could be retrieved on demand to improve performance. 

(2) Lacking Join Fetch: We should join the field annotated with ```EAGER FetchType``` by join fetch presented in HQL to avoid N+1 problems. 

(3) One-By-One: A collection annotated with ```@OneToMany``` or ```@ManyToMany``` using ```LAZY FetchType``` will fetched one-by-one in every loop iteration. ```@BatchSize``` should be involved to load  on demand and in batch. 

(4) Missing ManyToOne: Using ```@OneToMany``` annotation in a field without ```@ManyToOne``` presented in the corresponding field on the other side of the relationship may lead to performance issues such as N+1. 

# The N+1 Problem


> The N + 1 problem occurs when an application gets data from the database, and then loops through the result of that data. That means we call to the database again and again and again. In total, the application will call the database once for every row returned by the first query (N) plus the original query ( + 1). 

For implementational details, please visit https://www.brentozar.com/archive/2018/07/common-entity-framework-problems-n-1/ 