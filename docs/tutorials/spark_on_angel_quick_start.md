# Spark on Angel Quick Start


## 环境配置
- Spark运行环境
- Angel运行环境


## 本地模型运行
- clone angel代码到本地，编译并install到本地库
- 执行以下脚本
```bash
$SPARK_HOME/bin/spark-submit
--master local
--
```

## Yarn模式运行
- 配置Spark和Angel环境
- 执行一下脚本

```bash
$SPARK_HOME/bin/spark-submit \
    --master yarn-cluster \
    --conf spark.hadoop.hadoop.job.ugi=tesla,supergroup \
    --conf spark.submitter=kevinzwyou \
    --conf spark.ps.jars=$ANGEL_JARS,$ANGEL_UDF \
    --conf spark.ps.instances=10 \
    --conf spark.ps.cores=2 \
    --conf spark.ps.memory=6g \
    --queue g_teg_angel.g_teg_angel-offline \
    --jars $LOCAL_ANGEL_JARS,$SPARK_JARS  \
    --name "BreezeSGD-spark-on-angel" \
    --driver-memory 10g \
    --num-executors 10 \
    --executor-cores 2 \
    --executor-memory 4g \
    --class com.tencent.angel.spark.examples.ml.BreezeSGD \
    spark-on-angel-examples-1.1.8.jar
```
- YARN将会出现两个Application，一个是Spark Application， 一个是Angel-PS Application。
