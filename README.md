# dbt-spark-hello-world

Step 1: Create Virtual Environment


```

# Create a virtual environment
python -m venv dbt-env

# Activate the virtual environment
source dbt-env/bin/activate

# Install DBT Core
pip install dbt-core

# Install DBT Spark
pip install dbt-spark

# Install PyHive for Spark integration
pip install 'dbt-spark[PyHive]'

```
Step 2: Launch Thrift Server for Spark


```
# Launch Spark Thrift Server locally
spark-submit \
  --master 'local[*]' \
  --conf spark.executor.extraJavaOptions=-Duser.timezone=Etc/UTC \
  --conf spark.eventLog.enabled=false \
  --conf spark.sql.warehouse.dir=file:///Users/soumilshah/Desktop/soumil/sparkwarehouse \
  --packages 'org.apache.spark:spark-sql_2.12:3.4.0,org.apache.spark:spark-hive_2.12:3.4.0' \
  --class org.apache.spark.sql.hive.thriftserver.HiveThriftServer2 \
  --name "Thrift JDBC/ODBC Server" \
  --executor-memory 512m

```

Step 3: Connect with Beeline
```
# Connect to Spark Thrift Server using Beeline
beeline -u jdbc:hive2://localhost:10000/default

# Show available databases
show databases;

```

Step 4: DBT Commands

After setting up Spark and connecting through Beeline, you can use DBT for data modeling and analytics.

```
# Run DBT in debug mode
dbt debug

# Run DBT models
dbt run


```

![Screenshot 2023-12-09 at 10 46 33 AM](https://github.com/soumilshah1995/dbt-spark-hello-world/assets/39345855/101653d9-fd43-4269-abc0-723ab303fdf6)


# Enjoy
