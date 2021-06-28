### PATH  
```
%JAVA_HOME%\bin;
%M2_HOME%\bin;
%GRADLE_HOME%\bin;
%ANDROID_HOME%\tools;%ANDROID_HOME%\platform-tools;%ANDROID_HOME%\build-tools\28.0.3;
%GROOVY_HOME%\bin;
%Python%\;%Python%\Scripts;
F:\env\cmder;
```
### Java  
```
JAVA_HOME   F:\env\jdk1.8
CLASSPATH   .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;
```
### Maven  
```
M2_HOME     F:\env\maven
MAVEN_HOME  F:\env\maven
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
```
### Gradle  
```
GRADLE_HOME         F:\env\gradle
GRADLE_USER_HOME    F:\env\.gradle
```
### Android  
```
ANDROID_HOME        F:\env\android-sdk-windows
ANDROID_SDK_HOME    F:\env\.android
```
### AndroidStudio  
```
android-studio\bin\idea.properties
idea.config.path=F:/env/.AndroidStudio/config
idea.system.path=F:/env/.AndroidStudio/system

build.gradle的repositories可用阿里替代：
    repositories {
        maven { url 'https://maven.aliyun.com/repository/google' }
        maven { url 'https://maven.aliyun.com/repository/public' }
        google()
        mavenCentral()
    }
```
### Groovy  
```
GROOVY_HOME   F:\env\groovy
```
### Python  
```
Python        F:\env\Python35
```

