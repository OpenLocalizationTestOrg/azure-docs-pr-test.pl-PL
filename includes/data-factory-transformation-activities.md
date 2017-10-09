Fabryka danych Azure obsługuje hello następujące przekształcenie działań, które może być dodany toopipelines indywidualnie lub powiązane z innym działaniem.

| Działanie przekształcania danych | Środowisko obliczeniowe |
|:--- |:--- |
| [Hive](../articles/data-factory/data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](../articles/data-factory/data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](../articles/data-factory/data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Przesyłanie strumieniowe usługi Hadoop](../articles/data-factory/data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Spark](../articles/data-factory/data-factory-spark.md) | HDInsight [Hadoop] |
| [Działania usługi Machine Learning: wykonywanie wsadowe i aktualizacja zasobów](../articles/data-factory/data-factory-azure-ml-batch-execution-activity.md) |Maszyna wirtualna platformy Azure |
| [Procedura składowana](../articles/data-factory/data-factory-stored-proc-activity.md) |Azure SQL, Azure SQL Data Warehouse lub SQL Server |
| [Język U-SQL usługi Data Lake Analytics](../articles/data-factory/data-factory-usql-activity.md) |Azure Data Lake Analytics |
| [DotNet](../articles/data-factory/data-factory-use-custom-activities.md) |Usługa HDInsight [Hadoop] lub usługa Azure Batch |

> [!NOTE]
> Można skorzystać z MapReduce działania toorun Spark programów w klastrze Spark w usłudze HDInsight. Zobacz [Wywoływanie programów platformy Spark z usługi Azure Data Factory](../articles/data-factory/data-factory-spark.md).
> Można tworzyć niestandardowe działania toorun R skrypty w klastrze usługi HDInsight z języka R zainstalowanego. Zobacz [Uruchamianie skryptów języka R przy użyciu usługi Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).
> 
> 

