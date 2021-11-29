# Guide for Users: Smell detection in 4 steps
1. Setup JDK     
Install [Java Development Kit](https://www.oracle.com/java/technologies/downloads/) version greater than 8.0. Skip if you already have one.     
2. Download JAR     
Download [the current release](https://github.com/HBSniff/HBSniff/releases/tag/v1.6.8) (HBSniff-1.6.8-jar-with-dependencies.jar) to the directory ```$downloadPath$```.    
3. Open Terminal     
Open cmd (Windows) or terminal (macOS, Linux).   
4. Execute Command with ```--input``` and ```--output``` path specified  
```bash
cd $downloadPath$
java -jar HBSniff-1.6.8-jar-with-dependencies.jar -i $projectRootPath$ -o $outputPath$
```

Excel report and data in csv and JSON named after ```$projectRootPath$``` will be placed in ```$outputPath$```.

Remarks 
* $PATH$, the directory of the downloaded JAR.
* $projectRootPath$, the root path of the project to detect.
* $outputPath$, the output path of the exported report / data.

# Exclude Smells
An optional ```--exclude``` or ```-e``` could be provided to discard the detection of specific smells.       
To exclude multiple smells/metrics, split the smells by ','.       

Names of Smells: 
CollectionField,
FinalEntity,
GetterSetter,
HashCodeAndEquals,
MissingIdentifier,
MissingNoArgumentConstructor,
NotSerializable,
Fetch,
OneByOne,
MissingManyToOne,
Pagination.       
To exclude metrics, simply append "MappingMetrics" to the content of this parameter.      

# Specify Export Filetypes
An optional ```--type``` or ```-t``` could be provided to specify the file types of exportation. Available values are xls,csv,json. To export multiple types of fles, split the types by ','. For examples of export data, please refer to the [Output](./output.md) section.       