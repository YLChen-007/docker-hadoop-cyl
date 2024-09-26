
echo 'Creating test data and running MapReduce jobs'
mkdir -p /tmp/test-input
for i in {1..10}; do
echo 'Hello World Bye World' > /tmp/test-input/file_$i.txt
done
/opt/hadoop-3.1.1/bin/hadoop fs -mkdir -p /user/root/test-input
/opt/hadoop-3.1.1/bin/hadoop fs -put /tmp/test-input/* /user/root/test-input/
for i in {1..10}; do
/opt/hadoop-3.1.1/bin/hadoop jar /opt/hadoop-3.1.1/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.1.1.jar wordcount /user/root/test-input /user/root/output_$i
done

/opt/hadoop-3.1.1/bin/mapred archive-logs -verbose -minNumberLogFiles 1 -maxTotalLogsSize 10
