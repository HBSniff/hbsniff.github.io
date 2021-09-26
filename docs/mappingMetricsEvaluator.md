# MappingMetrics
The detection of 4 metrics, i.e., TATI, NCT, NCRF, ANV, is implemented in this class since they are all related to the complexity of inheritance. The structure of this class is the ```initInheritance()``` method calculates the maps of class-level inheritance for every metric, and a overlapping field map for NCRF specifically. Then, the 4 methods ```TATI, NCT, NCRF, ANV``` calculate the metric value according to the maps. Finally, they are called in the ```exec()``` method.              

# The Metric Class for Output     
Currently, there is not much metric in HBSniff, so we basically adapt the metric evaluation to the rule-based smell detection system, i.e., the Metric class is a subclass of Smell which includes an additional ```intensity``` field to save metric value.     

# Remarks      
These classes will be refactored to a similar but independant strategy like the Smell system, e.g., a static factory, an abstact class, and independent code for every metric. 