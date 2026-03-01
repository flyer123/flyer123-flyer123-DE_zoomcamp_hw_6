how to run
 sudo chmod -R 777 ./data
 sudo docker compose up -d

 if it doesn't work then:
 sudo docker compose down -v
 sudo docker rm -f pyspark-notebook 2>/dev/null
 sudo docker compose up -d

 get tocken from
 - sudo docker logs pyspark-notebook 
 open jupyter
 localhost:8888
 open spark ui
 localhost:8080


in jupyter:
1 - from pyspark.sql import SparkSession
 to test - spark = (
    SparkSession.builder
    .appName("cluster-test")
    .master("spark://spark-master:7077")
    .config("spark.driver.host", "pyspark-notebook")
    .getOrCreate()
)

df = spark.range(10)
df.show()

download file
3 - !wget https://d37ci6vzurychx.cloudfront.net/trip-data/yellow_tripdata_2025-11.parquet -P /data

chech file
4 - spark = (
    SparkSession.builder
    .appName("yellow taxi dataframe")
    .master("spark://spark-master:7077")
    .config("spark.driver.host", "pyspark-notebook")
    .getOrCreate()
)

df = spark.read.parquet("/data/yellow_tripdata_2025-11.parquet")
df.printSchema()
df.show(5)