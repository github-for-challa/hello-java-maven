## Running  a Simple Java Maven Build Job in Jenkins
Objective
## This task involves building a simple Java HelloWorld application using Maven in Jenkins. The goal is to learn the basic CI/CD principles by automating a Java build process in Jenkins.

Tools Required
Jenkins (installed locally or via Docker)
Java JDK 8 or 11
Maven (to build the Java project)
Git (optional, can run from a local folder)

Deliverables
A basic Java HelloWorld app with a pom.xml file.
A Jenkins Freestyle job configured to build it.
A screenshot of the successful build console output.

Project Setup
Step 1: Create the Java Application
Create a simple Java HelloWorld program in a file named HelloWorld.java:

java

// HelloWorld.java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Jenkins + Maven!");
    }
}

Step 2: Create the pom.xml File
This pom.xml file is used by Maven to build the project. Create it in the root directory of your project.
xml

<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>hello</artifactId>
    <version>1.0</version>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>

Step 3: Install Jenkins (If Not Already Installed)
If you haven’t installed Jenkins, or you can install jenkins in AWS ec2 , or  you can do so by running it in Docker:

docker run -p 8080:8080 jenkins/jenkins:lts
This command will start Jenkins on port 8080. You can access the Jenkins dashboard by navigating to http://localhost:8080 in your web browser.

Step 4: Configure Jenkins for Maven
Go to Manage Jenkins → Global Tool Configuration.
Under Maven, click Add Maven and specify the Maven version (e.g., Maven 3.8.6) that you have installed. You can also choose to install it automatically if it’s not available.

Step 5: Create the Jenkins Freestyle Project
In the Jenkins dashboard, click New Item and select Freestyle project.
Name the project (e.g., Java Maven Build Job), and click OK.

Step 6: Configure the Jenkins Build Steps
In the Build section, click Add build step and choose Invoke top-level Maven targets.
Set the Goals field to clean package (This will clean the previous build and package the Java application).
Save the job.

Step 7: Trigger the Build
Click Build Now to trigger the job.
Once the build finishes, check the Console Output for the build results.

Expected Output:
You should see a BUILD SUCCESS message in the console output, indicating that the build was successful.

Errors and Solutions
Error 1: mvn clean package fails to build the project
This can happen if Jenkins does not have the correct permissions to delete the target/ directory during the build process. Fix:
Ensure that the Jenkins user has the correct permissions to delete files in the workspace.
Run the following command to change the ownership of the workspace to the Jenkins user:
sudo chown -R jenkins:jenkins /var/lib/jenkins/workspace

Error 2: Maven build fails due to missing dependencies
If Maven fails to download dependencies, ensure your Jenkins server has internet access and the Maven repositories are reachable.
Fix:
Check your internet connection and the pom.xml file to ensure all dependencies are correctly specified.
Run the build again after checking the Maven repository URLs in your pom.xml.

Error 3: mvn clean package results in permission issues
If the error message is related to permissions during the cleanup process 
(e.g., Maven failing to delete files from the workspace), you might need to adjust the file permissions or remove files manually.
Fix:
Use the rm -rf command to delete the target/ directory manually:
rm -rf /var/lib/jenkins/workspace/Java\ Maven\ Build\ Job\ in\ Jenkins/target
Ensure that the Jenkins user has appropriate permissions to access and modify the workspace directory.

Error 4: Build failure due to incorrect Maven settings
If the build fails because of an incorrect Maven configuration, ensure that:
The correct Maven version is configured in Jenkins.
The pom.xml file is properly set up with the required build configurations.

## Conclusion
Once all steps are completed successfully, you will have built a simple Java application using Maven in Jenkins. 
This task introduces you to the basic CI/CD workflow in Jenkins and helps you understand the integration of Maven with Jenkins for building Java applications.
