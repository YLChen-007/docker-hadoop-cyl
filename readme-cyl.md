docker-compose -f docker-compose-v3.yml up --build

docker-compose -f docker-compose-v3.yml down -v

docker-compose logs resourcemanager

hadoop jar /opt/hadoop-3.1.1/share/hadoop/mapreduce/hadoop-mapreduce-client-uploader-3.1.1.jar org.apache.hadoop.mapred.uploader.FrameworkUploader  /tmp/test.jar 

hadoop jar /opt/hadoop-3.1.1/share/hadoop/mapreduce/hadoop-mapreduce-client-uploader-3.1.1.jar org.apache.hadoop.mapred.uploader.FrameworkUploader -input /tmp/test.jar -target hdfs:///test.tar.gz#mr-framework -fs hdfs://namenode:9000


mapred frameworkuploader -input /opt/hadoop-3.1.1/share/hadoop/mapreduce/lib/hamcrest-core-1.3.jar -target hdfs:///test3.tar.gz#mr-framework -fs hdfs://namenode:9000

hadoop pipes "-Dhadoop.pipes.java.recordreader=true" "-Dhadoop.pipes.java.recordwriter=true" -input pipeInput -output pipeOutput4 -program /upload/wordcount-simple

hadoop pipes "-Dhadoop.pipes.java.recordreader=true" "-Dhadoop.pipes.java.recordwriter=true" -input pipeInput -output pipeOutput -program /upload/wordcount-simple "-Dmapreduce.map.memory.mb=4096" "-Dmapreduce.reduce.memory.mb=4096" 

sed -i '/<\/configuration>/i \
<property>\n\
   <name>yarn.nodemanager.vmem-check-enabled<\/name>\n\
   <value>false<\/value>\n\
   <description>Whether virtual memory limits will be enforced for containers<\/description>\n\
<\/property>\n\
<property>\n\
   <name>yarn.nodemanager.vmem-pmem-ratio<\/name>\n\
   <value>4<\/value>\n\
   <description>Ratio between virtual memory to physical memory when setting memory limits for containers<\/description>\n\
<\/property>' /opt/hadoop-3.1.1/etc/hadoop/yarn-site.xml