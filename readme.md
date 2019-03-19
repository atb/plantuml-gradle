# Simple Calculator Application

**This project is for educational purposes only**

** This project is based on https://github.com/H4rryp0tt3r/Calculator by Nageswara Rao Podilapu **

This projects demonstrates how to integrate Plantuml with Gradle in order to integrate 
technical diagrams produced with Plantuml in javadoc.

**Attention!!**

**See the section [PlantUML dependency on Graphviz](#requirements) of this file for how to install Grahviz, a tool required by 
Plantuml that is not automatically installed!**

## Plantuml Diagrams

Plantuml diagrams are, by default, located in the folder **src/main/puml**

The tasks that renders images from the Plantuml diagram specifications is called **renderPlantUml**  

To execute this task simple type (in a terminal/console):

    ./gradlew renderPlantUml

By default, the images are produced into the folder **build/puml**

## Source Code for the renderPlantUml Task

The renderPlantUml task is implemented in groovy and its code is located in the **buildSrc** 
folder. This folder contains code that is pre-built by gradle and available for the 
tasks.

If you take a look at the file **buildSrc/build.gradle** you see that there is a dependency 
for the plantuml library.

Take a look at the **RenderPlantUmlTask** (file buildSrc/src/main/groovy/RenderPlantUmlTask.groovy). This 
class extends **DefaultTask** and includes a method with the annotation **@TaskAction** 
that implements the behavior of the task.

## Integration of Plantuml and Javadoc

Since the project is a java project there is a **javadoc** task that can be executed 
to generate javadoc.

    ./gradlew javadoc

This tasks will generate javadoc documentation in **build/docs/javadoc**. 

The task in build.gradle includes an overview page **src/main/javadoc/overview.html**. 
This page references 2 plantuml diagrams.

Also, the javadoc for the package **com.twu.calculator** (file **src/main/java/com/twu/calculator/package-info.java**) 
references a plantuml diagram.

However, if you open (in a browser) the javadoc (i.e., **build/docs/javadoc/index.html**) you 
will see broken links to the images! This is because the images are been generated 
to the folder **build/puml** and should be generated into the javadoc output folder!

If you manually copy the image files from **build/puml** into **build/docs/javadoc** 
(do not forget the subfolders) and refresh the browser you will see the diagrams. **How 
could this task be automated with gradle?**

## <a name="requirements"></a>PlantUML dependency on Graphviz

To properly work on all types of diagrams PlantUML depends on Graphviz. This is something that the gradle build does not solve automatically.

Please refer to page [plantuml-graphviz-dot](http://plantuml.com/graphviz-dot) for further information on this issue and on instructions to install Graphviz on your system.

You may also find instructions for installation in [Graphviz](https://graphviz.gitlab.io/download/)
