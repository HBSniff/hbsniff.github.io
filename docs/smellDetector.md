# SmellDetector
To implement a new smell, a new class that extends a ```SmellDetector abstract class``` should be created. The abstract class contains populated contextual information of all entities and classes, as well as HQLs to make sure developers could develop detection logic freely.          

You may use the populated ```List``` of JavaParser ```CompilationUnit``` called ```cus``` (all available classes) and ```entities``` (classes annotated with ```@Entity```), as well as the ```declarations``` and ```entityDeclarations``` variables containing the tool's simplified abstraction of the raw ```CompilationUnit```. 

**Do not forget to add the detected smells to the ```ProjectSmellReport``` instance named ```psr```. Otherwise they will not appear in the final report.** 

# SmellDetectorFactory     
Every instance of SmellDetector is initialized and populated in a static factory called ```SmellDetectorFactory``` by its ```createAll``` method.      
Specifically, the ```SmellType``` enumeration is a subclass of this static factory, and we use the name of the enum to locate the corresponding SmellDetector in ```io.github.hzjdev.hbsniff.detector.rules``` by ```Java Reflection```.      

# The Smell Class for Output       
This class (```io.github.hzjdev.hbsniff.model.output.Smell```) is used for data output, which contains the name, filepath, position, comment, as well as the affected class name of the smell.      
There is also a ```ProjectSmellReport``` class which contains a ```Map<Declaration, List<Smell>>``` of affected class (presented by their ```Declarations```) and a list of all smells identified. 