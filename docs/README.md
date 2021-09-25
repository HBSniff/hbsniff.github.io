# HBSniff
HBSniff (HiBernate Sniffer) is a static analysis tool for Java Hibernate ORM (Object-Relational Mapping) code smell detection.     

# Motivation
To facilitate Object-Oriented Programming (OOP), and to prevent security attacks such as injection, Hibernate is adopted to automatically generate SQL queries and map data from DB to Java classes.    
Despite its flexibility and capability, there exist various challenges in practice  including the metamorphic class and table inheritance , the inconsistency in data structure , and the uncontrollable propagation of relational data retrieval.    
This work aims at providing tool support for further large-scale empirical analysis. 

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


# Acknowledgement
 This work was partially supported by the National Natural Science Foundation of China under Grant No. 61772200, and the Natural Science Foundation of Shanghai under Grant No. 21ZR1416300.

# Special Thanks
Ziyi (Violette) Zhou from Deloitte France for her valuable comments. 