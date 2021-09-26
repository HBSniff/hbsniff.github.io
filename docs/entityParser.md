# EntityParser
The entity parser consists of several methods aiming to parse the java files to the ```JavaParser CompilationUnits``` , and parse ```CompilationUnit``` to the HBSniff ```Declaration```.

## Major Attributes
The major attributes of ```EntityParser``` are caches that optimize the program's performance in case it is evaluating a large project.    
```declarationCache```: a map of source code path and its ```Declaration```.    
```packageCache```: a map of package and ```Declarations``` in the package.    
```cusCache```: a list of ```CompilationUnits``` available.    

## Major Methods

```List<CompilationUnit> parseFromDir(String dirPath)```    
Parse all classes in a subdirectories of a path.     
```List<CompilationUnit> getEntities(List<CompilationUnit> cus)```    
Filter the classes without @Entity annotation.     
```List<Declaration> genDeclarationsFromCompilationUnits(List<CompilationUnit> cus)```    
Generate a list of Declaration from a list of CompilationUnits.     
```List<Declaration> findCalledIn(MethodDeclaration md, String typeName, List<CompilationUnit> cus)```    
Check any method is called in a scope CompilationUnits and return the method that calls them.     
```Declaration findTypeDeclaration(String toFind, String fullPath, List<CompilationUnit> cus, Integer level)```    
Locate a type in CompilationUnits and generate a Declaration for it, ad populate the declaration in a level of dependencies.     
```ParametreOrField getIdentifierProperty(final Declaration entity)```    
Get the identifier field of an @Entity.     
```List<Declaration> getSuperClassDeclarations(Declaration dec)```    
Get superclasses of a declaration.     

# Declaration
Declaration is an abstraction of method, constrctor, and class declarations. Currently we use a DeclarationType enumeration to differ the types of Declarations, later they will be refactored to subclasses, and the Declaration would be an abstract method.      

## Major Attributes

The major attributes of the ```Declaration``` model are their names, path, plain code, fields/parametres, members and constructors (for classes only).     

## Major Methods
```Declaration fromPath(String path)```    
Generate new Declaration from a path.    
```List<String> getAnnotations()```     
Get annotations of a Declaration.    
```Set<String> getAccessedFieldNames(List<Declaration> superClasses)```    
Get the names of accessed field (superclasses should be provided to find calls in them).    
```Set<Declaration> getExtendedOrImplementedTypes()```     
Get extended or implemented types.  
```List<String> getSuperClass()```      
Get the name of the parent superclass of the declaration.    
```List<String> getImplementedInterface()```    
Get the name of the implemented interfaces of the declaration.    
```boolean checkMethodCalled(String methodName)```    
Check if method is called in a class.    
```boolean annotationIncludes(String s)```     
Check if annotations includes string.    

# ParametreOrField
This model contains the type, name, modifier, position, annotations, and related typeDeclarations of a parametre of method or a field of class. Similar to Declaration, this model will be refactored to different subclasses.        
