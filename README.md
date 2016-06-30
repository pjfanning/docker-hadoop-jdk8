# Build the image

If you'd like to try directly from the Dockerfile you can build the image as:

```
docker build  -t pjfanning/docker-hadoop-jdk8:2.7.1 .
```
# Pull the image

The image is also released as an official Docker image from Docker's automated build repository - you can always pull or refer the image when launching containers.

```
docker pull pjfanning/docker-hadoop-jdk8:2.7.1
```

# Start a container

In order to use the Docker image you have just build or pulled use:

**Make sure that SELinux is disabled on the host. If you are using boot2docker you don't need to do anything.**

```
docker run -it pjfanning/docker-hadoop-jdk8:2.7.1 /etc/bootstrap.sh -bash
```

```
docker run -it -p 192.168.99.100:9000:9000 -p 192.168.99.100:50070:50070 -p 192.168.99.100:8030-8033:8030-8033 -p 192.168.99.100:31000-31100:31000-31100 pjfanning/docker-hadoop-jdk8:2.7.1 /etc/bootstrap.sh -bash
```

# Hdfs ports
EXPOSE 50010 50020 50070 50075 50090 8020 9000
# Mapred ports
EXPOSE 19888
#Yarn ports
EXPOSE 8030-8033 8040 8042 8088
#Spark Executor ports
EXPOSE 31000-31100
#Other ports
EXPOSE 49707 2122

## Testing

You can run one of the stock examples:

```
cd $HADOOP_PREFIX
# run the mapreduce
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.1.jar grep input output 'dfs[a-z.]+'

# check the output
bin/hdfs dfs -cat output/*
```
