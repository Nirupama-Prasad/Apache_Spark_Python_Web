# apache_spark_py
Producer consumer demo for spark based mapreduce, with apache spark and kafka streaming (for live events)

Data:
To simulate a live display of storm data, the parameters of humidity, windspeed in miles per
hour, temperature all gathered via a simulator that logs appropriate timestamp in each RDD.
These are received via Kafka events, which are aggregated into different output files

Program pieces:
1. Kafka producer: producer.py (this is the simulator)
2. Kafka consumer: consumer.py (this is the aggregator)
3. Spark RDD processing: new_consumer.py (this is the spark RDD rule machine)
4. Index.html (contains live refresh with data obtained so far)
5. Output files generated (zip contains last run data) : output.txt (produced by kafka
consumer and used by the spark RDD processor, tempJson.json (produced by spark
machine and used by web UI) and avgJson (produced by spark machine, used by
webUI)

To run program and output:
To process Kafka, run this along with the zookeeper module.
1. First, start zookeeper: ./bin/zookeeper­server­start.sh config/zookeeper.properties
2. Next, start kafka server: ./bin/kafka­server­start.sh config/server.properties
3. Next, run kafka producer: python producer.py
4. Next, run kafka consumer: python consumer.py
5. Next, run spark rdd machine (through spark submit):
./spark­1.6.1­bin­hadoop2.6/bin/spark­submit ­­packages
org.apache.spark:spark­streaming­kafka_2.10:1.6.1 spark_consumer.py
6. Optionally, you can see output also streaming through kafka console consumer:
bin/kafka­console­consumer.sh ­­zookeeper localhost:2181 ­­topic test ­­from­beginning
7. Next, start web server by running: python ­m SimpleHTTPServer
8. The web server will run on port 8000, kafka bootstrap on 9092 and kafka console
consumer on 2192 (default port)
