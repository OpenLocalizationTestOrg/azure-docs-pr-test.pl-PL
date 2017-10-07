---
title: "używane przez usługi Hadoop w usłudze HDInsight - Azure aaaPorts | Dokumentacja firmy Microsoft"
description: "Lista portów używanych przez usługi Hadoop działające w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd14aed9-ec25-4bb3-a20c-e29562735a7d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 0abc5c1c678aa79816e3e82a74538d2fb6db40ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ports-used-by-hadoop-services-on-hdinsight"></a>Porty używane przez usługi Hadoop w usłudze HDInsight

Ten dokument zawiera listę hello porty używane przez usługi Hadoop działające w klastrach HDInsight opartych na systemie Linux. Zawiera także informacje o portach używanych tooconnect toohello klastra przy użyciu protokołu SSH.

## <a name="public-ports-vs-non-public-ports"></a>Porty publiczny a niepublicznych portów

HDInsight opartych na systemie Linux klastrów udostępniają tylko trzy porty publicznie na hello internet; 22, 23 i 443. Te porty są klastra hello dostępu toosecurely używane przy użyciu protokołu SSH i usługi udostępniane za pośrednictwem protokołu HTTPS bezpiecznego hello.

Wewnętrznie, HDInsight jest implementowany przez kilka maszyn wirtualnych platformy Azure (hello węzłów w klastrze hello) uruchomione na sieć wirtualną platformy Azure. W ramach sieci wirtualnej hello, dostępne porty nie są widoczne za pośrednictwem hello internet. Na przykład jeśli łączysz tooone hello węzłów głównych przy użyciu protokołu SSH, z węzła głównego hello można następnie bezpośrednio uzyskać dostęp usługi działające na powitania węzłów klastra.

> [!IMPORTANT]
> Nie określaj sieci wirtualnej platformy Azure jako opcji konfiguracji dla usługi HDInsight, co jest tworzone automatycznie. Jednak nie można przyłączyć innych sieci wirtualnej toothis maszyny (np. inne maszyny wirtualne Azure lub komputerze deweloperskim klienta).


dodatkowe maszyny toojoin toohello sieci wirtualnej, użytkownik musi najpierw Utwórz sieć wirtualną hello, a następnie określ go podczas tworzenia klastra usługi HDInsight. Aby uzyskać więcej informacji, zobacz [możliwości rozszerzania HDInsight przy użyciu sieci wirtualnej platformy Azure](hdinsight-extend-hadoop-virtual-network.md)

## <a name="public-ports"></a>Porty publiczny

Witaj wszystkie węzły w klastrze HDInsight znajdują się w sieci wirtualnej platformy Azure i nie są bezpośrednio dostępne z hello internet. Publiczny bramy zawiera następujące porty, które są wspólne dla wszystkich typów klastra usługi HDInsight toohello dostęp do Internetu.

| Usługa | Port | Protokół | Opis |
| --- | --- | --- | --- | --- |
| sshd |22 |SSH |Łączy toosshd klientów na powitania headnode podstawowego. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |22 |SSH |Łączy toosshd klientów na powitania węzła krawędzi. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |23 |SSH |Łączy toosshd klientów na powitania headnode dodatkowej. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| Ambari |443 |HTTPS |Ambari web UI. Zobacz [Zarządzanie HDInsight przy użyciu hello Interfejsu sieci Web Ambari](hdinsight-hadoop-manage-ambari.md) |
| Ambari |443 |HTTPS |Interfejs API REST Ambari. Zobacz [Zarządzanie HDInsight przy użyciu hello interfejsu API REST Ambari](hdinsight-hadoop-manage-ambari-rest-api.md) |
| Usługi WebHCat |443 |HTTPS |HCatalog interfejsu API REST. Zobacz [korzystanie z programu Hive z Curl](hdinsight-hadoop-use-pig-curl.md), [korzystanie z języka Pig z Curl](hdinsight-hadoop-use-pig-curl.md), [korzystać z usługi MapReduce z Curl](hdinsight-hadoop-use-mapreduce-curl.md) |
| Serwera HiveServer2 |443 |ODBC |Łączy tooHive za pośrednictwem sterownika ODBC. Zobacz [tooHDInsight łączenie programu Excel ze sterownikiem ODBC firmy Microsoft hello](hdinsight-connect-excel-hive-odbc-driver.md). |
| Serwera HiveServer2 |443 |JDBC |Nawiązuje połączenie przy użyciu JDBC tooHive. Zobacz [połączyć tooHive w usłudze HDInsight przy użyciu sterownik Hive JDBC hello](hdinsight-connect-hive-jdbc-driver.md) |

następujące Hello są dostępne dla określonego klastra typów:

| Usługa | Port | Protokół | Typ klastra | Opis |
| --- | --- | --- | --- | --- |
| Stargate |443 |HTTPS |HBase |Interfejs API REST HBase. Zobacz [rozpocząć korzystanie z bazy danych HBase](hdinsight-hbase-tutorial-get-started-linux.md) |
| Livy |443 |HTTPS |platforma Spark |Interfejs API REST platformy Spark. Zobacz [Spark przesyłania zadania zdalnie przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md) |
| Storm |443 |HTTPS |Storm |STORM interfejsu użytkownika sieci web. Zobacz [wdrażanie i zarządzanie topologiami Storm w usłudze HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md) |

### <a name="authentication"></a>Authentication

Wszystkie usługi udostępniane publicznie na powitania przez internet, musi zostać uwierzytelniony:

| Port | Poświadczenia |
| --- | --- |
| 22 i 23 |poświadczenia użytkownika SSH Hello określone podczas tworzenia klastra |
| 443 |Nazwa logowania Hello (domyślne: admin) i hasło, które zostały określone podczas tworzenia klastra |

## <a name="non-public-ports"></a>Niepubliczne portów

> [!NOTE]
> Niektóre usługi są dostępne tylko dla typów konkretnego klastra. Na przykład baza danych HBase jest dostępna tylko na typy klastrów HBase.

> [!IMPORTANT]
> Niektóre usługi uruchomić tylko jedną headnode naraz. Jeśli usługa toohello tooconnect na powitania headnode podstawowego próba i wystąpi błąd 404, spróbuj ponownie, używając hello headnode dodatkowej.

### <a name="ambari"></a>Ambari

| Usługa | Węzły | Port | Ścieżka adresu URL | Protokół | 
| --- | --- | --- | --- | --- |
| Interfejs użytkownika sieci web Ambari | HEAD węzłów | 8080 | / | HTTP |
| Interfejs API REST Ambari | HEAD węzłów | 8080 | / api/v1 | HTTP |

Przykłady:

* Interfejs API REST Ambari:`curl -u admin "http://10.0.0.11:8080/api/v1/clusters"`

### <a name="hdfs-ports"></a>System plików HDFS portów

| Usługa | Węzły | Port | Protokół | Opis |
| --- | --- | --- | --- | --- |
| NameNode interfejsu użytkownika sieci web |HEAD węzłów |30070 |HTTPS |Stan tooview interfejsu użytkownika sieci Web |
| NameNode metadanych usługi |HEAD węzłów |8020 |IPC |Metadanych systemu plików |
| DataNode |Wszystkich węzłów procesu roboczego |30075 |HTTPS |Stan tooview interfejsu użytkownika sieci Web, dzienniki, itp. |
| DataNode |Wszystkich węzłów procesu roboczego |30010 |&nbsp; |Transfer danych |
| DataNode |Wszystkich węzłów procesu roboczego |30020 |IPC |Operacji na metadanych |
| NameNode dodatkowej |HEAD węzłów |50090 |HTTP |Punkt kontrolny NameNode metadanych |

### <a name="yarn-ports"></a>YARN portów

| Usługa | Węzły | Port | Protokół | Opis |
| --- | --- | --- | --- | --- |
| Menedżer zasobów interfejsu użytkownika sieci web |HEAD węzłów |8088 |HTTP |Interfejs użytkownika dla Menedżera zasobów sieci Web |
| Menedżer zasobów interfejsu użytkownika sieci web |HEAD węzłów |8090 |HTTPS |Interfejs użytkownika dla Menedżera zasobów sieci Web |
| Interfejs administracyjny Menedżera zasobów |HEAD węzłów |8141 |IPC |Dla aplikacji przesyłania (Hive, Pig, Hive serwera itp.) |
| Menedżer zasobów harmonogramu |HEAD węzłów |8030 |HTTP |Interfejs administracyjny |
| Interfejs aplikacji Menedżera zasobów |HEAD węzłów |8050 |HTTP |Adres interfejsu Menedżera aplikacji hello |
| NodeManager |Wszystkich węzłów procesu roboczego |30050 |&nbsp; |adres Hello hello kontenera Menedżera |
| NodeManager interfejsu użytkownika sieci web |Wszystkich węzłów procesu roboczego |30060 |HTTP |Interfejs Menedżera zasobów |
| Adres osi czasu |HEAD węzłów |10200 |RPC |Witaj osi czasu usługi RPC. |
| Oś czasu interfejsu użytkownika sieci web |HEAD węzłów |8181 |HTTP |Witaj osi czasu usługi interfejsu użytkownika sieci web |

### <a name="hive-ports"></a>Porty gałęzi

| Usługa | Węzły | Port | Protokół | Opis |
| --- | --- | --- | --- | --- |
| Serwera HiveServer2 |HEAD węzłów |10001 |Thrift |Usługa podłączania tooHive (Thrift/JDBC) |
| Potrzeby magazynu metadanych hive |HEAD węzłów |9083 |Thrift |Usługa łączącego tooHive metadanych (Thrift/JDBC) |

### <a name="webhcat-ports"></a>Porty WebHCat

| Usługa | Węzły | Port | Protokół | Opis |
| --- | --- | --- | --- | --- |
| Serwer usługi WebHCat |HEAD węzłów |30111 |HTTP |Interfejs API sieci Web na podstawie innych usług Hadoop i HCatalog |

### <a name="mapreduce-ports"></a>Porty MapReduce

| Usługa | Węzły | Port | Protokół | Opis |
| --- | --- | --- | --- | --- |
| JobHistory |HEAD węzłów |19888 |HTTP |MapReduce JobHistory interfejsu użytkownika sieci web |
| JobHistory |HEAD węzłów |10020 |&nbsp; |MapReduce JobHistory serwera |
| ShuffleHandler |&nbsp; |13562 |&nbsp; |Pośredni mapy transferów danych wyjściowych reduktory toorequesting |

### <a name="oozie"></a>Oozie

| Usługa | Węzły | Port | Protokół | Opis |
| --- | --- | --- | --- | --- |
| Oozie serwera |HEAD węzłów |11000 |HTTP |Adres URL usługi Oozie |
| Oozie serwera |HEAD węzłów |11001 |HTTP |Port programu Oozie administratora |

### <a name="ambari-metrics"></a>Metryki Ambari

| Usługa | Węzły | Port | Protokół | Opis |
| --- | --- | --- | --- | --- |
| Oś czasu (Historia aplikacji) |HEAD węzłów |6188 |HTTP |Witaj osi czasu usługi interfejsu użytkownika sieci web |
| Oś czasu (Historia aplikacji) |HEAD węzłów |30200 |RPC |Witaj osi czasu usługi interfejsu użytkownika sieci web |

### <a name="hbase-ports"></a>Porty HBase

| Usługa | Węzły | Port | Protokół | Opis |
| --- | --- | --- | --- | --- |
| HMaster |HEAD węzłów |16000 |&nbsp; |&nbsp; |
| HMaster informacje o interfejsie użytkownika sieci Web |HEAD węzłów |16010 |HTTP |port Hello hello interfejsu użytkownika sieci web głównego HBase |
| Region serwera |Wszystkich węzłów procesu roboczego |16020 |&nbsp; |&nbsp; |
| &nbsp; |&nbsp; |2181 |&nbsp; |port Hello używają tooconnect tooZooKeeper |

### <a name="kafka-ports"></a>Porty Kafka

| Usługa | Węzły | Port | Protokół | Opis |
| --- | --- | --- | --- | --- |
| Broker |Węzłów procesu roboczego |9092 |[Protokół Kafka](http://kafka.apache.org/protocol.html) |Używany do komunikacji z klientem |
| &nbsp; |Węzły dozorcy |2181 |&nbsp; |port Hello używają tooconnect tooZookeeper |

### <a name="spark-ports"></a>Porty Spark

| Usługa | Węzły | Port | Protokół | Ścieżka adresu URL | Opis |
| --- | --- | --- | --- | --- | --- |
| Serwery Spark Thrift |HEAD węzłów |10002 |Thrift | &nbsp; | Usługa podłączania tooSpark SQL (Thrift/JDBC) |
| Serwer programu Livy | HEAD węzłów | 8998 | HTTP | /batches | Usługa uruchamiania instrukcje, zadania i aplikacji |

Przykłady:

* Livy: `curl "http://10.0.0.11:8998/batches"`. W tym przykładzie `10.0.0.11` jest adresem IP hello headnode hello, obsługującym hello Livy usługi.
