最近花了幾天將自己的三個電腦叢架上Hadoop([什麼是Hadoop](http://blog.jobbole.com/1321/)) , 其中一個datanode是一代的raspberry pi

而在啟動start-dfs.sh時，遇到了
> Server VM is only supported on ARMv7+ VFP

經過谷歌後，發現是因為java server版本上使用VM， 但不支援ARMv6 因此那晚只好早點睡覺。

隔天上課發現了一個繞道方式解決VM不支援的問題

在raspberry pi 上

    pi@raspberry:~$ java -version

    java version “1.8.0_111”

    Java(TM) SE Runtime Environment (build 1.8.0_111-b14)

    Java HotSpot(TM) Client VM (build 25.111-b14, mixed mode)

    ks@raspberry:~ $ java -server -version

    Error occurred during initialization of VM

    Server VM is only supported on ARMv7+ VFP

因此經過谷歌發現一個work around的方法。那就是先到$HADOOP_HOME/etc/hadoop 中更改

hadoop-env.sh （我的$HADOOP_HOME 為/opt/hadoop/hadoop/, 安裝hadoop的地址)

中更愛HADOOP_DATANODE_OPTS 在最後加上-client

export HADOOP_DATANODE_OPTS=”-Dcom.sun.management.jmxremote $HADOOP_DATANODE_OPTS -client”

這樣便可以避開使用java -server 的指令。

圖源：https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/Hadoop_logo.svg/2000px-Hadoop_logo.svg.png

如果你喜歡我的文章或side projects，可以[捐贈我一杯大熱美（大杯美式咖啡）支持我。](https://www.buymeacoffee.com/theblackcat102)