#JVM

- JVM is an abstract machine which provides runtime environment for java bytecode to be executed

- It is a specification and implementation is provided by Oracle and other companies

- Its implementation is known as JRE

- Whenever java command is run to execute a java class, an instance of JVM is created 

- It runs the main method of java code

- Java applications are called WORA (Write Once Run Anywhere)

- Java is platform independent but JVM is platform dependent

#JVM Process

- Java compiler converts .java file into .class files (it contains byte-code)

- The .class file goes into various steps in JVM

#Class Loader--------------------------------------------------------------------------------------------------------------

- Class Loader has 3 activities namely

1. Loading
2. Linking
3. Initialization


# 1. Loading

- Class Loader reads the .class file, generate the corresponding binary data and save it in method area

- for each .class file, JVm stores the following information in method area

1. Fully Qualified name of the loaded class and its intermediate parent class

2. Whether .class file is related to Class or Interface or Enum

3. Modifier, Variables and Method information


- After loading .class file, JVM creates an Object of type Class to represent this file in the heap memory

- Developers can use this Class object to get name of class, parent name, methods and variable information

- For every loaded .class file, only one object of Class is created.

#Eg

Class c1 = s1.getClass();
Method m[] = c1.getDeclaredMethods();
Field f[] = c1.getDeclaredFields(); 


# 2. Linking

- Peforms the following steps

1. Verification
	
	- Verifies the correctness of .class file (for formatting etc)
	- If verification fails, we get run-time exception java.lang.VerifyError

2. Preparation

	- JVM allocates memory for class variables and initializing the memory to default values
	
3. Resolution

	- It is the process of replacing symbolic references from the type with direct references
	- It is done by searching into method area to locate the referenced entity
	

# 3. Initialization

	- All static variables are assigned with their values defined in the code and static block.
	- This is executed from top to bottom in class and from parent to child in class hierarchy
	
	- There are 3 types of class loaders namely
	
	# a. Bootstrap Class Loader
	
	- Every JVM implementation must have a bootstrap class loader which loads trusted classes
	- It loads core java API classes present in JAVA_HOME/jre/lib directory
	- This is based on bootstrap path
	
	# b. Extension Class Loader
	
	- It is a child of bootstrap class loader
	- It loads the classes present in the extensions directories JAVA_HOME/jre/lib/ext(Extension path) or any other directory specified by the java.ext.dirs system  property
	- It is implemented in java by the sun.misc.Launcher$ExtClassLoader class.
	
	# c. System / Application Class Loader
	
	- It is a child of Extension Class Loader 
	- It is responsible to load classes from application class path
	- It internally uses Environment Variable which is mapped to java.class.path
	- This one loads the files created by the developers
	- It is implemented in Java by the sun.misc.Launcher$AppClassLoader class.
	

- JVM follow Delegation-Hierarchy principle to load classes. 

- System class loader delegate load request to extension class loader and extension class loader delegate request to boot-strap class loader.

- If class found in boot-strap path, class is loaded otherwise request again transfers to extension class loader and then to system class loader.

- At last if system class loader fails to load class, then we get run-time exception java.lang.ClassNotFoundException.


#JVM Memory--------------------------------------------------------------------------------------------------------------

# 1. Method Area

- In method area, all class level information like class name, immediate parent class name, methods and variable info etc are stored including static 
variables
- There is only one method area per JVM and it is a shared resource

# 2. Heap Area

- Information of all objects is stored in heap area
- There is only one Heap area per JVM and it is also a shared resource

# 3. Stack Area

- For every thread, JVM creates one run-time stack which is stored here- 
- After a thread terminated, its run-time stack will be destroyed by JVM
- A new frame is created each time a method is invoked. A frame is destroyed when its method invocation completes.
- It is not a shared resource

# 4. PC Registers

- Store address of current execution instruction of a thread
- Each thread has separate PC Registers
- PC (program counter) register contains the address of the Java virtual machine instruction currently being executed.

# 5. Native method stacks 

- For every thread, separate native stack is created. It stores native method information


#Execution Engine--------------------------------------------------------------------------------------------------------------

- Executes the .class(bytecode)
- Reads the bytecode line by line, use data and information present in various memory area and execute instructions
- There are 3 parts namely

# a. Intrepreter

- It intreprets the bytecode line by line and then executes.
- Drawback is that When a method is called mutiple times, every time intrepretation is required

# b. Just-In-Time Compiler (JIT)

- Increases the efficiency of intrepreter.
- It compiles enitre bytecode and changes it to native code whenever intrepreter sees repeated method calss, JIT provides direct native code for that method
- Hence re-intrepretation of the method is not required and hence efficiency is improved

# c. Garbage Collector

- It destroys un-referenced objects


#Java Native Interface--------------------------------------------------------------------------------------------------------------

- An interface which interacts with Native Method Libraries and provides the native libraries required for execution
- It enables JVM to call c/c++ libraries and to be called by C/C++ libraries which may be specific to hardware


#Native Method Libraries :

- Collection of native libraries(C,C++) which are required by Execution Engine


#References

https://www.geeksforgeeks.org/jvm-works-jvm-architecture/
https://www.javatpoint.com/jvm-java-virtual-machine