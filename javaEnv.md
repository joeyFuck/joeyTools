1. jdk 1.8 & Enviroment config(JAVA_HOME PATH)

2. maven & Enviroment config(MAVEN_HOME PATH) & modifiy setting.xml & create new dir named repository

    ```js
    <mirror> 
      <id>alimaven</id> 
      <name>aliyun maven</name> 
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url> 
      <mirrorOf>central</mirrorOf> 
    </mirror>
    ```
    
3. idea download & maven setting(file/build.../build tools/maven)

   home directory: H:/maven(your maven install dir) 
   User setting file: H:\maven\conf\settings.xml
   local repository: H:\repository
  
4. download init spring boot project from http://start.spring.io/

5. open project & init maven repository(5 min)


