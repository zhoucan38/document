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

```html
3、root账号错误 
由于ElasticSearch可以接收用户输入的脚本并且执行，为了系统安全考虑，建议创建一个单独的用户用来运行ElasticSearch
a、创建elsearch用户组及elsearch用户
groupadd es
useradd es -g es -p es

b、更改Elasticsearch文件夹及内部文件的所属用户及组为es:es 
chown -R es:es /app/elasticsearch-6.8.11

c、切换到elsearch用户再启动
su es
cd /app/elasticsearch-6.8.11/bin
./elasticsearch
```

```html
4、最大虚拟内存过小错误
ERROR: bootstrap checks failed max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
切换至root用户：su root
修改虚拟内存配置至提示的最低值：sysctl -w vm.max_map_count=262144
```

```html
5、max file descriptors [4096] for elasticsearch process is too low, increase to at least [65535]
vi /etc/security/limits.conf，追加以下内容；
* soft nofile 65536
* hard nofile 65536
```

```html
6、max number of threads [3753] for user [XX] is too low, increase to at least [4096] 
vi /etc/security/limits.conf，追加以下内容；
* soft nproc 4096
* hard nproc 4096

vi /etc/sysctl.conf
添加如下配置
vm.max_map_count=655360
并执行
sysctl -p
```

```html
7、关闭防火墙
查看防火墙状态
firewall-cmd --state
not running 或者 running

关闭防火墙
systemctl stop firewalld.service #停止firewall
systemctl disable firewalld.service #禁止firewall开机启动
```

