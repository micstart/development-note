# development-environment
my development environment

1.Java
JAVA_HOME    D:\env\jdk1.8
CLASSPATH    .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;

2.Maven
M2_HOME       F:\env\maven
MAVEN_HOME    F:\env\maven
F:\env\maven\conf\settings.xml
  <localRepository>F:/env/.m2/repository</localRepository>
  ...
  <mirrors>
    <mirror>
      <id>alimaven</id>
      <name>aliyun maven</name>
      <mirrorOf>central</mirrorOf>
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    </mirror>
  </mirrors>

3.Gradle
GRADLE_HOME         F:\env\gradle
GRADLE_USER_HOME    F:\env\.gradle

4.Android
ANDROID_HOME        F:\env\android-sdk-windows
ANDROID_SDK_HOME    F:\env\.android

5.AndroidStudio
android-studio\bin\idea.properties
idea.config.path=F:/env/.AndroidStudio/config
idea.system.path=F:/env/.AndroidStudio/system

6.Python
F:\env\Python35

