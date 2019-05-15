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



## Recommender on Apache Spark: 
good detail on rec on scalability in prod: https://medium.com/criteo-labs/sparkrsvd-open-sourced-by-criteo-for-large-scale-recommendation-engines-6695b649f519 \
pyspark with emr cluster: https://towardsdatascience.com/use-pyspark-with-a-jupyter-notebook-in-an-aws-emr-cluster-e5abc4cc9bdd \
https://www.youtube.com/watch?v=58OjaDH2FI0 \
https://www.slideshare.net/databricks/building-an-implicit-recommendation-engine-with-spark-with-sophie-watson \
https://towardsdatascience.com/large-scale-jobs-recommendation-engine-using-implicit-data-in-pyspark-ccf8df5d910e
