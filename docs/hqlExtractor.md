# HQLExtractor
```List<HqlAndContext> getHqlNodes(List<CompilationUnit> cus)```       
The HQL extractor locate the ```createQuery()``` method call which indicates potential HQL usage, and locate HQL in the context of the method and class containing the method call. Moreover, it finds the method that calls the method containing HQL.      

# HqlAndContext
## Major Attributes of HQL
```List<String> hql```      
A list of hql queries. We use the list expression to keep the original structure of concatenated hql in code (which may be valuable for debugging). To use it practically, this collection is usually joined.       
```List<Declaration> hqlFromType```      
The declarations of the entities presented after the from expression of HQL.       
```Map<String, String> aliasMap```     
The alias of the entities presented after the from expression of HQL. e.g., for the HQL select id from Student s, the related value would be <"Student","s">.      

## Major Attributes of The Method Containing the HQL
```String createQueryPosition```      
The position of the ```createQuery``` method call.    
```String methodName```       
The name of the method containing the HQL expression.      
```String methodBody```      
The code of the method containing the HQL expression.      
```String methodPosition```      
The position of the method containing the HQL expression.      
```String returnExpression```      
The content of the return statement of the method containing the HQL expression.      
```List<ParametreOrField> params```     
The parametres of the method containing the HQL expression.      
```String returnType```      
The name of the returned type of the method containing the HQL expression.      
```Declaration returnTypeDeclaration```      
The ```Declaration``` of the returned type of the method containing the HQL expression if available.      
```List<Declaration> calledIn```       
The list of ```Declarations``` that calls the method containing the HQL.     

## Major Attributes of The Class Containing the HQL
```String fullPath```      
The file path of the class containing the HQL expression.      
```String typeName```      
The type name of the type in the class containing the HQL expression.      