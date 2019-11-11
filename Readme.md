## Environment set up 
(NOT recommended) Installation on windows: \
https://medium.com/@GalarnykMichael/install-spark-on-windows-pyspark-4498a5d8d66c

### Docker with jupyter: 
https://medium.com/@suci/running-pyspark-on-jupyter-notebook-with-docker-602b18ac4494 \
Need to replace localhost with docker ip by getting `docker-machine ip` on docker terminal \
overview of docker: https://www.dataquest.io/blog/docker-data-science/

#### Running docker
https://fenics.readthedocs.io/projects/containers/en/latest/jupyter.html \
https://medium.com/the-code-review/top-10-docker-commands-you-cant-live-without-54fb6377f481 \
https://towardsdatascience.com/15-docker-commands-you-should-know-970ea5203421

###### Docker commands
get docker ip \
`sudo docker inspect <container-id> | grep '"IPAddress"' | head -n 1`

run new docker container \
`docker run -d -p 8888:8888 jupyter/pyspark-notebook`

check docker \
`docker ps -q`

check docker logs and link \
`docker logs <container-id>`

docker copy to local \
`docker cp <docker-id>:/home/jovyan/<filename> "<path>"`





## Running Spark 
Introduction on Apache Spark: \
https://towardsdatascience.com/a-beginners-guide-to-apache-spark-ff301cb4cd92


### Data manipulation

Pandas to spark dataframe using arrow \
https://gist.github.com/BryanCutler/bc73d573b7e46a984ff8b6edf228e298

spark dataframe basic: \
https://changhsinlee.com/pyspark-dataframe-basics/ \
https://www.analyticsvidhya.com/blog/2016/10/spark-dataframe-and-operations/

joins: \
https://datascience-enthusiast.com/Python/big_data_spark_part2

export csv: \
https://fullstackml.com/how-to-export-data-frame-from-apache-spark-3215274ee9d6

### Tuning Spark 
Spark Submit \
`spark-submit --master yarn --deploy-mode cluster --num-executors 3 --executor-cores 8 --executor-memory 16gb /directory/spark_test2.py`

Spark Submit Configuration \
https://spoddutur.github.io/spark-notes/distribution_of_executors_cores_and_memory_for_spark_application.html

Writing pyspark code \
http://blog.appliedinformaticsinc.com/how-to-write-spark-applications-in-python/


### Recommender on Apache Spark 
good detail on rec on scalability in prod: https://medium.com/criteo-labs/sparkrsvd-open-sourced-by-criteo-for-large-scale-recommendation-engines-6695b649f519 \
pyspark with emr cluster: https://towardsdatascience.com/use-pyspark-with-a-jupyter-notebook-in-an-aws-emr-cluster-e5abc4cc9bdd \
https://www.youtube.com/watch?v=58OjaDH2FI0 \
https://www.slideshare.net/databricks/building-an-implicit-recommendation-engine-with-spark-with-sophie-watson \
https://towardsdatascience.com/large-scale-jobs-recommendation-engine-using-implicit-data-in-pyspark-ccf8df5d910e

## Productionize Spark
[Evaluation of all deploy methods of 2019](https://www.youtube.com/watch?v=APdH91p-lfU) \
[mleap method](https://www.youtube.com/watch?v=KOehXxEgXFM) 

### Spark Conda Environment
Needs to duplicate Conda environment in all the other worker nodes so that occasional pandas code can run. \
[Conda-pack](https://conda.github.io/conda-pack/index.html) to pack up old environment to be install in new environment without internet. \
[Conda with spark](https://www.alkaline-ml.com/2018-07-02-conda-spark/)

##### Steps to replicate:
After packing current conda environment from source machine([Conda-pack](https://conda.github.io/conda-pack/index.html)), go to target machine

``cd /mnt/disk1/davidooi`` \
```mkdir -p andalan``` \
```tar -xzf andalan_env.tar.gz -C andalan``` \
```source bin/activate``` at /mnt/disk1/davidooi/andalan

``source deactivate`` to deactivate environment

##### Spark Submit:
cluster-mode: \
``spark-submit --master yarn --conf spark.yarn.appMasterEnv.PYSPARK_PYTHON=/mnt/disk1/davidooi/andalan/bin/python3 --deploy-mode cluster --executor-cores 7 --num-executors 4 --executor-memory 16g --archives /mnt/disk1/davidooi/andalan_env.tar.gz /mnt/disk1/davidooi/spark_test2s_long.py``

client-mode: \
``PYSPARK_PYTHON=/mnt/disk1/davidooi/andalan/bin/python3 spark-submit --conf spark.yarn.appMasterEnv.PYSPARK_PYTHON=/mnt/disk1/davidooi/andalan/bin/python3    --master yarn --deploy-mode client  --archives /mnt/disk1/davidooi/andalan_env.tar.gz   /mnt/disk1/davidooi/spark_test2s.py``

spark-shell: \
``PYSPARK_DRIVER_PYTHON=/mnt/disk1/davidooi/andalan/bin/python3 PYSPARK_PYTHON=/mnt/disk1/davidooi/andalan/bin/python3 pyspark --conf spark.yarn.appMasterEnv.PYSPARK_PYTHON=/mnt/disk1/davidooi/andalan/bin/python3 --master yarn --deploy-mode client --archives /mnt/disk1/davidooi/andalan_env.tar.gz``
