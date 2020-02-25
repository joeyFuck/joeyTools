1. 配置启动参数
   tomcat/bin/catalia.sh JAVA_Opts = ...  Xlmx 最大内存 Xlms 最小内存
2. 配置catalina.out日志输出路径
   
   tomcat/bin/catalina.sh 

   if [ -z "$CATALINA_OUT" ] ; then
      CATALINA_OUT="$CATALINA_BASE"/logs/catalina.out
    修改为
   if [ -z "$CATALINA_OUT" ] ; then
      CATALINA_OUT=/dev/null
      
    这样就不会生成catalina.out文件了
    
3. java.util.logging.ConsoleHandler.level = OFF 
   也能不生成catalina.out,不过有时不生效
