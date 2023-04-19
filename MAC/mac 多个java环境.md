## mac下jdk多版本切换（jdk8与jdk11,jdk17）

1.jdk8一直是公司应用的主力，还时要在开发机器上保留双版本（支持到2030，果然是长寿版本）

官方下载地址：https://www.oracle.com/java/technologies/downloads/#java8-mac

2.下载安装jdk11（支持到2026年）

官方下载地址：https://www.oracle.com/java/technologies/downloads/#java11-mac

最新的已经到jdk18了，jdk17（支持到2024年）

国内快速下载地址：清华镜像：https://mirrors.tuna.tsinghua.edu.cn/Adoptium/
华为镜像站：版本比较少 https://repo.huaweicloud.com/java/jdk/

更多地址可以参考：[centos下jdk11及jdk8的环境变量配置](https://www.pomelolee.com/1954.html)

3.配置编辑.bash_profile文件 cd到用户目录

根据自己的路径调整 在 /Library/Java/JavaVirtualMachines 下

```
# 设置 jdk 8 JAVA_8_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_331.jdk/Contents/Home # 设置 jdk 11 JAVA_11_HOME=/Library/Java/JavaVirtualMachines/zulu-11.jdk/Contents/Home   #alias命令动态切换JDK版本 alias jdk8="export JAVA_HOME=$JAVA_8_HOME" alias jdk11="export JAVA_HOME=$JAVA_11_HOME"  export JAVA_HOME="/usr/libexec/java_home" #最后安装的版本，这样当自动更新时，始终指向最新版本 PATH=$PATH:$JAVA_HOME/bin CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar export JAVA_HOME PATH CLASSPATH export PATH="/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:${JAVA_HOME}:${JAVA_HOME}/bin"
```

\3. source ~/.bash_profile 文件使其生效

通过输入jdk8便可以切换到jdk1.8
输入jdk11便可以切换到jdk11