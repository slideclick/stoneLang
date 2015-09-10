# stoneLang



I would never share the .metadata folder. In fact unless you have a particular reason I would not even share the workspace folder but instead share each project separately with git. That way the .metadata folder will always be in the parent folder of your git repository and you dont have to think about whether you need to ignore it anyway:

|-- workspace/
|  \-- .metadata/
|  |-- yourProjectOne/
|  |  \-- .git/
|  |  |-- .project
|  |  |-- src/
|  |  |-- ...
|  |-- yourProjectTwo/
|  |  \-- .git/
|  |  |-- .project/
|  |  |-- src/
|  |  |-- ...
Project Specific

You should probably always share the .project file and never .settings/ files. The .classpath may depend on your environment but I would not suggest to share it either, because it can cause conflicts (for example if one user uses openjdk and the other uses sun-jdk. The .settings contains preferences and settings for eclipse and changes a lot, thus it should not be shared. If you properly import the project after you cloned it from git then you will also not have any problems.

The eclipse documentation states the following about the .project file:

The purpose of this file is to make the project self-describing, so that a project that is zipped up or released to a server can be correctly recreated in another workspace.
and:

If a new project is created at a location that contains an existing project description file, the contents of that description file will be honoured as the project description. One exception is that the project name in the file will be ignored if it does not match the name of the project being created. If the description file on disk is invalid, the project creation will fail.
I also suggest to use Maven as this will save you a lot of problems with the dependency management and .classpath

Maven

The main difference with a Maven project is that you can import the project as Maven->"Existing Maven Projects" and thus only need to share the pom.xml and .project file in git. Eclipse will then create the .classpath, .settings/ files for you automatically. Thus obviously you dont need to share them. If something changes in pom.xml you simply run Maven->"Update project configuration" and Maven->"Update dependencies".

Without Maven

You should share the .project file and not the .settings/ folder. You can considere to share .classpath but it may lead to conflicts as explained above. I would suggest not to share it either. Use the method below to import the project:

After you have cloned the git repository you can simply use Import->"Existing Project from Workspace" eclipse will honor the .project file but recreates the .classpath and .settings/ files. After the import you will need to configure the classpath by hand from Eclipse (and everytime your team wants to use another library).

If you do not share the .project file, then it is not possible to import the project with Eclipse. You will need to create a new project with the project wizard first, and then you can choose import "General->File System", this will copy all the files into your workspace. This is probably not what you want, because it means that you cannot clone the git repository into the workspace, you must clone it somewhere else and then import it from there. Therefore you should always share the .project file.

Please leave a commend if you have suggestions to this explanation or if you dont agree with it. I hope this helps the one or other.