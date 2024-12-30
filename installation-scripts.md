# Installation Scripts

## Installing and Configuring a Java Development Kit (JDK)

### Search for JDK

The winget search command should return a list of Oracle JDKs. Grab the Id for latest release.

```powershell
winget search --query Oracle.JDK
```

### Install JDK

The WinGet install command will handle downloading the application package for the JDK and installing it for you.

```powershell
winget install --id Oracle.JDK.23 --winget source --accept-package-agreements --silent
```

### Set Environment Variables

Set the `JAVA HOME` Environment Variable

```powershell
setx /M JAVA_HOME "C:\Program Files\Java\jdk-23"
```

Set the `Path` Environment Variable

```powershell
setx /M Path "%Path%;C:\Program Files\Java\jdk-23\bin"
```

### Verify the Installation

After installing the JDK and setting the environment variables we are ready to verify that the Java commands can be accessed.

Enter this command to verify that Java is correctly installed and identify which version is being used:

```powershell
java -version
```

And this command verifies the details about the specific build and version of the Java compiler:

```powershell
javac -version
```

## Installing and Configuring a Build Tool

Navigate to the download page the official Apache Maven website to download the binary zip file.

[Maven – Download Apache Maven](https://maven.apache.org/download.cgi)

Scroll down to the **Files** section. Download the following files:

1. Choose the latest binary zip file (e.g., apache-maven-3.9.9-bin.zip)
2. Click the Checksum for that file to get the file hash value

### Verify File Hash

> ℹ️ **File Hash** File hashes are used to verify the integrity and authenticity of files. They ensure that the file has not been altered or corrupted.

```powershell
certUtil -hashfile apache-maven-3.9.9-bin.zip SHA512
```

The hash returned should match the Checksum hash from the downloads page.

### Extract Maven Files

Navigate to the Windows Downloads folder where your Maven zip file is located. 

Remember to change `USER` to your Windows username.

```powershell
cd c:\Users\USER\Downloads
```

With the JDK installed, you're all set to use the jar command to unzip the Maven zip file.

```powershell
jar xf apache-maven-3.9.9-bin.zip
```

After you've successfully run the command to unzip the Maven zip file, the next step is to organize your development environment. Start by creating a dedicated directory where you'll store all of Java’s essential tools. This centralized folder will help keep everything tidy and easily accessible.

Use this command to create a new folder specifically for Java’s tools:

```powershell
md c:\tools\Java
```

Now that you have created the dedicated folder, it's time to move Maven into it. Use the mv (move) command to transfer the extracted Maven files to the new directory. 

```powershell
mv apache-maven-3.9.9 c:\Java\tools
```

Double-check that Maven has been successfully moved to the tools directory. 

```powershell
dir c:\tools\Java
```

You should see the Maven files and folders returned in the output.


### Set Environment Variables

Set the `MAVEN HOME` Environment Variable

```powershell
setx /M MAVEN_HOME "C:\tools\Java\apache-maven-3.9.9"
```

Set the `Path` Environment Variable

```powershell
setx /M Path "%Path%;C:\tools\Java\apache-maven-3.9.9\bin"
```

### Verify the Installation

Verify that Maven is installed and configured correctly by running the following command:

```powershell
mvn -version
```

This command should display Maven's version information along with the details of your JDK installation:

## Install an IDE

### IntelliJ IDEA

You can easily install it using WinGet, the command-line tool for Windows  Package Manager.

It is as simple  as entering this command and letting WinGet do  the work of locating the installer package, downloading it, and installing the app.

```powershell
winget install --id JetBrains.IntelliJIDEA.Community --source winget --accept-package-agreements --silent
```

### Visual Studio Code

As with IntelliJ we are installing Visual Studio Code  using WinGet:

```powershell
winget install --id Microsoft.VisualStudioCode --source winget --accept-package-agreements --silent
```
## Configure JVM Options

The `MAVEN_OPTS` environment variable is a handy tool that allows you to pass custom JVM options to Maven, optimizing its performance and behavior. This allows fine-tuning Maven’s performance, making your build process faster and more efficient.

```powershell
setx /M MAVEN_OPTS "-Xms512m -Xmx1024m -XX:MaxPermSize=512m -Xss1m -XX:+PrintGCDetails"
```

The `MAVEN_ARGS` environment variable defines default command-line options that Maven will automatically apply to every build, saving you time and effort. 

```powershell
setx \M MAVEN_ARGS= "-DskipTests -X -Dmaven.test.failure.ignore"
```
