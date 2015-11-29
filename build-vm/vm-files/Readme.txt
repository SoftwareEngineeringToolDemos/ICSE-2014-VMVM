How to use VMVM
----------------
________________

The purpose of VMVM (reads vroom-vroom) is speeding up Junit tests for large test suites.

How to use the examples provided in this machine:
____________________________________________

Example 1: Using VMVM with Apache Commons IO
____________________________________________

1) From Terminal, navigate to folder /Desktop/Examples/

2) There are two sub-directories there: 
	commons-io  - contains source code of Apache Commons IO, downloaded from Github
and	
	commons-io-vmvm - same source code, but modified to use VMVM.

3) First, in the /commons-io directory run commands: mvn compile, mvn test-compile, mvn test. Tests will run. Please take note of time it will take to execute all tests)

4) Second, from Terminal, navigate to modified "commons-io-vmvm" directory and run same commands. Please note time to execute tests using VMVM.

5) Compare results. In our tests, VMVM improved build time by 25-30%

____________________________________________

Example 2: Using VMVM with Apache Tomcat 8.0
____________________________________________

(Note: on our machine, it took 73 minutes to execute tomcat test suite without VMVM, and about 42-50 minutes with VMVM)

1) For the purpose of reducing size and boot time of this VM, tomcat source code is not included. It needs to be downloaded from Github. In terminal window, run command 

  $git clone https://github.com/apache/tomcat80.git "Desktop/tomcat80"

2) In Terminal, navigate to /home/vagrant/Desktop/tomcat80/ folder

3) First, Tomcat is built using Ant. Therefore, in order to run unit tests, use following commands in terminal:
	ant compile (Ant will compile project)
	ant test (Ant will run tests)
  Please note time it takes to run tests in the original tomcat.

4) Second, we modify the tomcat so that it will use VMVM
	4.1 Navigate to tomcat80 folder on Desktop
	4.2 Create "lib" directory in it 
	4.3 Navigate to folder /ICSE-2014-VMVM/bin/ on Desktop
	4.2 Copy files vmvm-1.0.0-SNAPSHOT.jar and vmvm-ant-junit-formatter-1.0.0-SNAPSHOT.jar into /Desktop/tomcat80/lib/
	4.3 From Desktop, navigate to /Desktop/ICSE-2014-VMVM/build-vm/vm-files/tomcat80/ and locate build.xml
	4.4 Copy file build.xml to /Desktop/tomcat80/, replacing the existing build.xml
	4.5 In terminal window, navigate to /Desktop/tomcat80/ and use same commands to run tests:
		ant compile
		ant test
  Please note time it takes to execute tests using VMVM

5) Compare results. In our tests, VMVM improved test time by 25-30%

_________________________________

How to use VMVM on a new project:
_________________________________

1) download the source of Java project

2) on the desktop, in ICSE-2014-VMVM/lib directory, there are 2 files that are needed to run the tool:
	vmvm-1.0.0-SNAPSHOT.jar
	mvm-ant-junit-formatter-1.0.0-SNAPSHOT.jar
3) copy these 2 files into the /lib directory of the source code
4.a.1) If it is a Maven build, following needs to be added to junit task in pom.xml file in the project directory of the source code:

<dependency>
<groupId>edu.columbia.cs.psl.vmvm</groupId>
<artifactId>vmvm</artifactId>
<version>1</version>
<scope>system</scope>
<systemPath>${project.basedir}/lib/vmvm-1.0.0-SNAPSHOT.jar</systemPath>
</dependency>
<dependency>
<groupId>edu.columbia.cs.psl.vmvm</groupId>
<artifactId>ant-mvn-formatter</artifactId>
<version>1</version>
<scope>system</scope>
<systemPath>${project.basedir}/lib/vmvm-ant-junitformatter-
1.0.0-SNAPSHOT.jar</systemPath>
</dependency>

4.a.2) Also, add this to the same pom.xml file in the surefire plugin:

<properties>
<property>
<name>listener</name>
<value>edu.columbia.cs.psl.vmvm.MvnVMVMListener</value>
</property>
</properties>

4.b) If it is an Ant build, modify the build.xml - make sure that <junit … forkMode="once"> and add this to Junit task:

<classpath>
<pathelement path="${project.home}/lib/vmvm-ant-junitformatter-1.0.0-SNAPSHOT.jar" />
<pathelement location="${project.home}/lib/vmvm-1.0.0-SNAPSHOT.jar"/>
<pathelement location="${project.home}/gen/"/>
</classpath>
<formatter classname="edu.columbia.cs.psl.vmvm.AntJUnitTestListener"
extension=".xml"/>
<jvmarg value="-Xbootclasspath/a:vmvm-1.0.0-SNAPSHOT.jar"/>

where “project.home” and "project.basedir" points to the source's main directory

4.c) If the project does not use neither Ant nor Maven, from directory one level above the project directory, run vmvm instrumenter using vmvm-1.0.0-SNAPSHOT.jar 
To do that, in Terminal, run 

$java -jar vmvm-1.0.0-SNAPSHOT.jar <project directory> <output directory>

where <project directory> is the folder to be instrumented, and <output directory> (which vmvm will create) is the folder with the instrumented code.

5.a) For Maven builds, from the Terminal, run mvn compile, mvn test-compile and mvn test in the Java project's main directory
5.b) For Ant builds, run ant test-compile and ant test
5.c) For builds that don't use Ant or Maven run tests in the instrumented <output directory>
