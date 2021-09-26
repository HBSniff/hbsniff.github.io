# HBSniff
HBSniff (**H**i**B**ernate **Sniff**er) is a static analysis tool for Java Hibernate ORM (Object-Relational Mapping) code smell detection.     

GitHub Repository: https://github.com/HBSniff/HBSniff        
Latest Release: https://github.com/HBSniff/HBSniff/releases/tag/v1.6.7        
Example Projects for Evaluation: https://doi.org/10.6084/m9.figshare.16682029.v1

# Motivation
To facilitate Object-Oriented Programming (OOP), and to prevent security attacks such as injection, Hibernate is adopted to automatically generate SQL queries and map data from database to Java classes.    
Despite its flexibility and capability, there exist various challenges in practice, including the metamorphic class and table inheritance , the inconsistency in data structure, and the uncontrollable propagation of relational data retrieval.    
This work aims at providing tool support for large-scale empirical analysis on ORM smells (i.e., sub-optimal design or implementation of ORM entities and queries).

# Highlights
* No Project Compilation Needed ([JavaParser](https://javaparser.org/)-based)
* 14 Detectable Smells
* 4 Mapping Metrics
* Excel Report Visualization

# Usage
Please refer to the "[For users](users.md)" section for execution guide.    
If you're interested in implementations, the "[For developers](developers.md)" section may help.    
Please submit Pull Requests or create issue tickets if any bug is found. Code contribution is also welcomed. 

# Developers

Zijie Huang, Ph.D. candidate, East China University of Science and Technology (ECUST), hzj#mail.ecust.edu.cn    
Homepage: http://hzjdev.github.io/

Kang Yang, Ph.D. candidate, ECUST, 15921709583#163.com   

Ziyi Zhou, Ph.D. candidate, ECUST, zhouziyi#mail.ecust.edu.cn   

# Cite This Tool
Zijie Huang, Zhiqing Shao, Guisheng Fan, Huiqun Yu, Kang Yang, Ziyi Zhou. HBSniff: A Static Analysis Tool for Java Hibernate Object-Relational Mapping Code Smell Detection. Science of Computer Programming. Under Review. https://hbsniff.github.io/paper.pdf     

# Acknowledgement
 This work was partially supported by the National Natural Science Foundation of China under Grant No. 61772200, and the Natural Science Foundation of Shanghai under Grant No. 21ZR1416300.

# Special Thanks
Ziyi (Violette) Zhou from Hardis Group for her valuable comments. 