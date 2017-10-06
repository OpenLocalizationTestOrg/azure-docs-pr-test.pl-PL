---
title: aaaUse Apache Phoenix i SQuirreL z HBase - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Apache Phoenix w usłudze HDInsight i w jaki sposób tooinstall i skonfigurować SQuirreL na stacji roboczej klastra HBase tooan tooconnect w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>Apache Phoenix za pomocą klastrów HBase opartych na systemie Linux w usłudze HDInsight
Dowiedz się, jak toouse [Apache Phoenix](http://phoenix.apache.org/) w usłudze HDInsight i w jaki sposób toouse SQLLine. Aby uzyskać więcej informacji na temat Phoenix, zobacz [Phoenix w ciągu 15 minut lub mniej](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Aby hello Phoenix gramatyki, zobacz [gramatyki Phoenix](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Aby hello Phoenix informacje o wersji w usłudze HDInsight, zobacz [nowości w wersjach klastra Hadoop hello dostarczanych z usługą HDInsight?](hdinsight-component-versioning.md).
>
>

## <a name="use-sqlline"></a>Użyj SQLLine
[SQLLine](http://sqlline.sourceforge.net/) jest tooexecute narzędzia wiersza polecenia SQL.

### <a name="prerequisites"></a>Wymagania wstępne
Przed użyciem SQLLine, musi mieć następujące hello:

* **Klaster HBase w usłudze HDInsight**. Aby uzyskać informacje dotyczące udostępniania bazy danych HBase klastra, zobacz [Rozpoczynanie pracy z bazy danych Apache HBase w usłudze HDInsight][hdinsight-hbase-get-started].
* **Połącz klaster HBase toohello za pośrednictwem protokołu RDP hello**. Aby uzyskać instrukcje, zobacz [klastrów zarządzania Hadoop w usłudze HDInsight przy użyciu hello portalu Azure][hdinsight-manage-portal].

Po ustanowieniu połączenia klastra HBase tooan należy tooone tooconnect z hello dozorcy. Każdy klaster usługi HDInsight ma trzy dozorcy.

**toofind limit nazwy hosta dozorcy hello**

1. Otwórz Ambari, przeglądając zbyt**https://<ClusterName>. azurehdinsight.net**.
2. Wprowadź HTTP (klaster) hello toologin nazwy użytkownika i hasła.
3. Kliknij przycisk **dozorcy** z menu po lewej stronie powitania. Zobacz trzy **serwera dozorcy** na liście.
4. Kliknij jeden z hello **serwera dozorcy** na liście. W okienku podsumowania hello Znajdź hello **Hostname**. Podobnie jest zbyt*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**toouse SQLLine**

1. Połącz toohello klastra przy użyciu protokołu SSH. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Z SSH uruchom następujące polecenia toorun SQLLine hello:

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. Uruchom następujące polecenia toocreate hello tabeli HBase i wstawić dane:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Aby uzyskać więcej informacji, zobacz [ręcznego SQLLine](http://sqlline.sourceforge.net/#manual) i [gramatyki Phoenix](http://phoenix.apache.org/language/index.html).

## <a name="next-steps"></a>Następne kroki
W tym artykule wiesz już, jak toouse Apache Phoenix w usłudze HDInsight.  toolearn więcej, zobacz:

* [Przegląd bazy danych HBase w usłudze HDInsight][hdinsight-hbase-overview]: HBase jest bazą danych Apache NoSQL typu open source opartą na platformie Hadoop, która zapewnia dostęp losowy i wysoki poziom spójności w przypadku dużych ilości danych z częściową strukturą i bez struktury.
* [Udostępnianie klastrów HBase w sieci wirtualnej Azure][hdinsight-hbase-provision-vnet]: Z integracji sieci wirtualnej klastrów HBase może być wdrożone toohello sam wirtualnych sieci jako aplikacje tak aplikacje mogą komunikować się z HBase bezpośrednio.
* [Konfigurowanie replikacji bazy danych HBase w usłudze HDInsight](hdinsight-hbase-replication.md): Dowiedz się, jak replikacji bazy danych HBase tooconfigure między dwoma centrami danych Azure.
* [Analizowanie Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight][hbase-twitter-sentiment]: Dowiedz się, jak toodo w czasie rzeczywistym [analizy wskaźniki nastrojów klientów](http://en.wikipedia.org/wiki/Sentiment_analysis) dużych danych przy użyciu bazy danych HBase w klastra usługi Hadoop w usłudze HDInsight.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
