---
title: "Użyj Apache Phoenix i SQuirreL z HBase - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak za pomocą Apache Phoenix w usłudze HDInsight oraz jak zainstalować i skonfigurować SQuirreL na stacji roboczej do nawiązania połączenia klastra HBase w usłudze HDInsight."
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
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>Apache Phoenix za pomocą klastrów HBase opartych na systemie Linux w usłudze HDInsight
Dowiedz się, jak używać [Apache Phoenix](http://phoenix.apache.org/) w usłudze HDInsight i sposobu użycia SQLLine. Aby uzyskać więcej informacji na temat Phoenix, zobacz [Phoenix w ciągu 15 minut lub mniej](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Dla gramatyki Phoenix [gramatyki Phoenix](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Aby uzyskać informacje o wersji Phoenix w usłudze HDInsight, zobacz [nowości w wersjach klastra Hadoop dostarczanych z usługą HDInsight?](hdinsight-component-versioning.md).
>
>

## <a name="use-sqlline"></a>Użyj SQLLine
[SQLLine](http://sqlline.sourceforge.net/) to narzędzie wiersza polecenia do wykonania SQL.

### <a name="prerequisites"></a>Wymagania wstępne
Przed użyciem SQLLine, należy dysponować następującymi elementami:

* **Klaster HBase w usłudze HDInsight**. Aby uzyskać informacje dotyczące udostępniania bazy danych HBase klastra, zobacz [Rozpoczynanie pracy z bazy danych Apache HBase w usłudze HDInsight][hdinsight-hbase-get-started].
* **Połącz się z klastrem HBase przy użyciu protokołu remote desktop protocol**. Aby uzyskać instrukcje, zobacz [klastrów zarządzania Hadoop w usłudze HDInsight przy użyciu portalu Azure][hdinsight-manage-portal].

Po podłączeniu do klastra HBase, należy połączyć się z jedną dozorcy. Każdy klaster usługi HDInsight ma trzy dozorcy.

**Aby dowiedzieć się, dozorcy nazwy hosta**

1. Otwórz Ambari, przechodząc do **https://<ClusterName>. azurehdinsight.net**.
2. Wprowadź nazwę protokołu HTTP (klaster) użytkownika i hasło do logowania.
3. Kliknij przycisk **dozorcy** z menu po lewej stronie. Zobacz trzy **serwera dozorcy** na liście.
4. Kliknij jeden z **serwera dozorcy** na liście. W okienku podsumowania znaleźć **Hostname**. Jest on podobny do *zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**Aby użyć SQLLine**

1. Połącz z klastrem przy użyciu protokołu SSH. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Z SSH uruchom następujące polecenia, aby uruchomić SQLLine:

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. Uruchom następujące polecenia, aby utworzyć tabelę HBase i wstawić dane:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Aby uzyskać więcej informacji, zobacz [ręcznego SQLLine](http://sqlline.sourceforge.net/#manual) i [gramatyki Phoenix](http://phoenix.apache.org/language/index.html).

## <a name="next-steps"></a>Następne kroki
W tym artykule ma przedstawiono sposób użycia Apache Phoenix w usłudze HDInsight.  Aby dowiedzieć się więcej, zobacz:

* [Przegląd bazy danych HBase w usłudze HDInsight][hdinsight-hbase-overview]: HBase jest bazą danych Apache NoSQL typu open source opartą na platformie Hadoop, która zapewnia dostęp losowy i wysoki poziom spójności w przypadku dużych ilości danych z częściową strukturą i bez struktury.
* [Udostępnianie klastrów HBase w sieci wirtualnej Azure][hdinsight-hbase-provision-vnet]: Z integracji sieci wirtualnej klastrów HBase można wdrożyć w tej samej sieci wirtualnej jako aplikacje, dzięki czemu aplikacje mogą komunikować się z bazą danych HBase bezpośrednio.
* [Konfigurowanie replikacji bazy danych HBase w usłudze HDInsight](hdinsight-hbase-replication.md): Dowiedz się, jak skonfigurować replikację bazy danych HBase między dwoma centrami danych Azure.
* [Analizowanie Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight][hbase-twitter-sentiment]: Dowiedz się, jak to zrobić w czasie rzeczywistym [analizy wskaźniki nastrojów klientów](http://en.wikipedia.org/wiki/Sentiment_analysis) dużych danych przy użyciu bazy danych HBase w klastra usługi Hadoop w usłudze HDInsight.

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
