# Maven常用命令

## 一、maven依赖树

```properties
mvn dependency:tree
```

## 二、maven依赖列表

```properties
mvn dependency:list
```

## 三、下载依赖包的源码

```properties
mvn dependency:sources
```

## 四、安装本地jar到本地仓库

```properties
mvn install:install-file \
-Dfile=D:/taobao-sdk-java-auto-20160607.jar  \
-DgroupId=com.ganshane.specs  \
-DartifactId=taobao-sdk-java-auto-20160607  \
-Dversion=1.0.0  \
-Dpackaging=jar
```

- 例如：

  mvn install:install-file -Dfile=springfox-swagger-ui-2.9.2.jar  -DgroupId=io.springfox  -DartifactId=nvx-springfox-swagger-ui  -Dversion=2.9.2  -Dpackaging=jar

## 五、将本地的jar发布到私服

```properties
mvn 
deploy:deploy-file 
-Dmaven.test.skip=true 
-Dfile=C:\Users\dev\Desktop\调试文件\swagger\springfox-swagger-ui-2.9.2\springfox-swagger-ui-2.9.2.jar 
-DgroupId=io.springfox 
-DartifactId=nvx-springfox-swagger-ui 
-Dversion=2.9.2 
-Dpackaging=jar 
-DrepositoryId=Releases //这个为maven setting.xml配置私服账号密码上server节点的id
-Durl=http://192.168.10.16:8081/repository/maven-releases/ 
--settings F:\java-soft\apache-maven-3.5.2\conf\settings.xml 
```

- 例如

  mvn deploy:deploy-file -Dmaven.test.skip=true -Dfile=C:\Users\dev\Desktop\调试文件\swagger\springfox-swagger-ui-2.9.2\springfox-swagger-ui-2.9.2.jar -DgroupId=io.springfox -DartifactId=nvx-springfox-swagger-ui -Dversion=2.9.2 -Dpackaging=jar -DrepositoryId=Releases -Durl=http://192.168.10.16:8081/repository/maven-releases/ --settings F:\java-soft\apache-maven-3.5.2\conf\settings.xml 

- -DrepositoryId

```properties
<server>
    <id>Releases</id>
    <username>dev</username>
    <password>hz_dev</password>
</server>
<server>
    <id>Snapshots</id>
    <username>dev</username>
    <password>hz_dev</password>
</server>
```

## 六、修改jar源码，本地解压打包成jar

```properties
jar -cvf test.jar ./dir   
```

- test.jar将要达成jar包的名称
- dir本地目录

## 七、缺少依赖包，强制更新依赖命令：
```properties
mvn clean install -e -U -Dmaven.test.skip=true
```













