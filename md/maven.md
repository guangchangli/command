## maven

1. #### 依赖冲突

   ```
   依赖了不同版本的jar ,maven会根据最短优先/最先声明 选取唯一jar使用
   ```

2. #### 解决依赖冲突

   - ##### 排除依赖

   ```
     <exclusions>
           <exclusion>
           <artifactId>log4j-api</artifactId>
           <groupId>org.apache.logging.log4j</groupId>
           </exclusion>
     </exclusions>
   ```

   - ##### 锁定版本号

     ```
     <properties></>
     ```

   - ##### Terminal

   - ```
      mvn dependency:tree -Dverbose
     ```

   - ##### plugin

   ```
   mavenHelper
   ```

3. #### 生命周期

   ```
   clean--default--site
   ```

   - ##### clean

     ```
     pre clean 执行清理前的工作
     clean 清理target
     post clean 执行清理后的工作
     ```

   - ##### core

     ```
     validate
     compile
     test
     package
     verify
     install
     deploy
     
     ```

   
   ##### idea 项目启动
   
   ```
   /Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home/bin/java 
   -Dmaven.multiModuleProjectDirectory=/Users/lgc/zkr/P11 
   -Dmaven.home=/Users/lgc/soft/apache-maven-3.6.3 
   -Dclassworlds.conf=/Users/lgc/soft/apache-maven-3.6.3/bin/m2.conf
   "-Dmaven.ext.class.path=/Applications/IntelliJ IDEA.app/Contents/plugins/maven/lib/maven-event-listener.jar" 
   "-javaagent:/Applications/IntelliJ IDEA.app/Contents/lib/idea_rt.jar=49805:/Applications/IntelliJ IDEA.app/Contents/bin" 
   -Dfile.encoding=UTF-8 
   -classpath /Users/lgc/soft/apache-maven-3.6.3/boot/plexus-classworlds.license:/Users/lgc/soft/apache-maven-3.6.3/boot/plexus-classworlds-2.6.0.jar org.codehaus.classworlds.Launcher 
   -Didea.version2019.3 -s /Users/lgc/.m2/settings.xml -Dmaven.repo.local=/Users/lgc/.m2/repository clean install 
   -Dmaven.test.skip=true
   ```
   
   