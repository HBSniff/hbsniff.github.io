# Guide For Users: Perform detection in 4 steps
1. Setup JDK     
Install Java Development Kit version greater than 8.0. Skip if you already have one.     
2. Download JAR     
Download the lastest release (fat jar file with dependencies) to the directory ```$downloadPath$```.    
3. Open Terminal     
Open cmd (Windows) or terminal (macOS, Linux), type ```cd $downloadPath$``` and press enter.     
4. Execute Command with --input and --output path specified  
```java -jar HBSniff-1.6.5.jar -i $<$projectRootPath$>$ -o $<$outputPath$>$```

You will find your Excel report and data in csv and JSON named after ```$<$projectRootPath$>$``` in ```$<$outputPath$>$```.

Remarks 
* $PATH$, the directory of the downloaded JAR.
* $projectRootPath$, the root path of the project to detect.
* $outputPath$, the output path of the exported report / data.

# Guide For Users: Perform detection in 4 steps
