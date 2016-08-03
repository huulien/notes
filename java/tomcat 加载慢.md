# tomcat加载慢

* 发现问题
如果加载时间都耗在Creation of SecureRandom instance for session ID generation
[localhost-startStop-1] 
org.apache.catalina.util.SessionIdGeneratorBase.createSecureRandom Creation of SecureRandom instance for session ID generation using [SHA1PRNG] took [232,830] milliseconds。

* 解决问题
修改：
$JAVA_HOME/jre/lib/security/java.security
securerandom.source=file:/dev/urandom
替换成    
securerandom.source=file:/dev/./urandom

