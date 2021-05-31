```html
1、java环境变量
JAVA_HOME=/app/jdk1.8.0_191
CLASSPATH=$JAVA_HOME/lib/
PATH=$PATH:$JAVA_HOME/bin
export PATH JAVA_HOME CLASSPATH
vi /etc/profile
source /etc/profile
```

```html
2、jdk、es目录权限都设置为777
es和id版本必须一致
es下载目录
https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.8.11.zip
elasticsearch-analysis-ik下载
https://github.com/medcl/elasticsearch-analysis-ik
```