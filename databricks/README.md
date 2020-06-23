## STEPS

### Ref
https://github.com/mspnp/spark-monitoring

### In following sample
- workdir is `/home/azureuser/databricks`
- git repo dir is `/home/azureuser/databricks/spark-monitoring`

### Upload init script and dependency to Databricks cluster

- deploy spark-monitoring.sh 
- `$ dbfs cp /home/azureuser/databricks/spark-monitoring/src/spark-listeners/scripts/spark-monitoring.sh  dbfs:/databricks/spark-monitoring/spark-monitoring.sh`
- deploy lib for log analytics
- `$ dbfs cp --overwrite --recursive /home/azureuser/databricks/spark-monitoring/src/target/ dbfs:/databricks/spark-monitoring/`

### Deploy Sample Job
- Build Sample Job
- `$ docker run -it --rm -v /home/azureuser/databricks/spark-monitoring/sample/spark-sample-job:/spark-monitoring -v "$HOME/.m2":/root/.m2 -w /spark-monitoring maven:3.6.1-jdk-8 mvn clean install -P scala-2.11_spark-2.4.3`

- Get JAR for upload to Databricks
- `$ scp azureuser@138.91.1.209:/home/azureuser/databricks/spark-monitoring/sample/spark-sample-job/target/spark-monitoring-sample-1.0.0.jar`
