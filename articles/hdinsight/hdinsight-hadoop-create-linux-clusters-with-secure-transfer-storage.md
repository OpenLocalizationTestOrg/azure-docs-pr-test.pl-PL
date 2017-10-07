---
title: "aaaCreate Hadoop klaster z zapewnienia bezpiecznego transferu kont magazynu w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate klastrów usługi HDInsight z zapewnienia bezpiecznego transferu włączone konta magazynu platformy Azure."
keywords: hadoop getting started,hadoop linux,hadoop quickstart,secure transfer,azure storage account
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>Tworzenie klastra usługi Hadoop z kontami magazynu z bezpiecznym transferem w usłudze Azure HDInsight

Witaj [bezpieczny transfer wymagane](../storage/common/storage-require-secure-transfer.md) funkcji zwiększa bezpieczeństwo hello konta magazynu Azure, wymuszając wszystkich żądań tooyour konta za pośrednictwem bezpiecznego połączenia. Ten schemat wasbs funkcji i hello są obsługiwane tylko przez wersja klastra usługi HDInsight 3,6 lub nowszej. 

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka potrzebna będzie:

* **Subskrypcja platformy Azure**: toocreate bezpłatne konto próbne jeden miesiąc, przejdź zbyt[azure.microsoft.com/free](https://azure.microsoft.com/free).
* **Konto usługi Azure Storage z włączonym bezpiecznym transferem**. Witaj instrukcje, zobacz [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) i [wymaga zapewnienia bezpiecznego transferu](../storage/common/storage-require-secure-transfer.md).
* **Kontener obiektów Blob na koncie magazynu hello**. 
## <a name="create-cluster"></a>Tworzenie klastra

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


W tej sekcji tworzysz klaster Hadoop w usłudze HDInsight przy użyciu [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Szablon Hello znajduje się w [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/). Znajomość szablonów usługi Resource Manager nie jest wymagana do korzystania z tego samouczka. Inne metody tworzenia klastrów i opis właściwości hello używane w tym samouczku, zobacz [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Kliknij przycisk hello toosign obrazu w tooAzure i otwórz hello szablonu usługi Resource Manager w hello portalu Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Wykonaj hello instrukcje toocreate hello klastra z hello następujące specyfikacje: 

    - Określ wersję usługi HDInsight na 3.6.  Wersja domyślna Hello jest 3.5. Wymagana jest wersja 3.6 lub nowsza.
    - Określ konto magazynu z włączonym bezpiecznym transferem.
    - Krótka nazwa używana dla konta magazynu hello.
    - Zarówno hello konta magazynu i kontener obiektów blob hello musi zostać utworzony wcześniej. 

    Witaj instrukcje, zobacz [Utwórz klaster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). 

Jeśli używasz tooprovide akcji skryptu w plikach konfiguracji, należy użyć wasbs w hello następujące ustawienia:

- fs.defaultFS (lokacja podstawowa)
- spark.eventLog.dir 
- spark.history.fs.logDirectory

## <a name="add-additional-storage-accounts"></a>Dodawanie kolejnych kont magazynu

Istnieje kilka opcji tooadd dodatkowe zapewnienia bezpiecznego transferu włączone kont magazynu:

- Szablon usługi Azure Resource Manager hello w ostatniej sekcji hello zmodyfikować.
- Tworzenie klastra przy użyciu hello [portalu Azure](https://portal.azure.com) i określ połączonym koncie magazynu.
- Użyj skryptu akcji tooadd dodatkowe zapewnienia bezpiecznego transferu włączyć magazyn kont tooan istniejącym klastrze usługi HDInsight.  Aby uzyskać więcej informacji, zobacz [dodać dodatkowy magazyn kont tooHDInsight](hdinsight-hadoop-add-storage.md).

## <a name="next-steps"></a>Następne kroki
W tym samouczku uzyskanych jak toocreate klastra usługi HDInsight, a następnie włączyć bezpieczny transfer toohello kont magazynu.

toolearn więcej informacji na temat analizowania danych z usługą HDInsight, zobacz następujące artykuły hello:

* toolearn więcej informacji o korzystaniu z programu Hive z usługą HDInsight, w tym, jak tooperform Hive zapytań z programu Visual Studio, zobacz [używanie Hive z usługą HDInsight][hdinsight-use-hive].
* toolearn temat Pig, języka używany tootransform danych, zobacz [Use Pig z usługą HDInsight][hdinsight-use-pig].
* toolearn o MapReduce, sposób programy toowrite, które przetwarzają dane w usłudze Hadoop, zobacz [Użyj MapReduce z usługą HDInsight][hdinsight-use-mapreduce].
* toolearn o za pomocą hello narzędzi HDInsight Visual Studio tooanalyze danych w usłudze HDInsight, zobacz [rozpocząć korzystanie z narzędzi Visual Studio Hadoop dla usługi HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

więcej informacji na temat sposobu HDInsight przechowuje dane toolearn lub tooget danych do usługi HDInsight, zobacz temat hello następujące artykuły:

* Aby uzyskać informacje o sposobie używania usługi Azure Storage przez usługę HDInsight, zobacz [Używanie usługi Azure Storage z usługą HDInsight](hdinsight-hadoop-use-blob-storage.md).
* Aby uzyskać informacje na temat tooupload tooHDInsight danych, zobacz [przekazywanie danych tooHDInsight][hdinsight-upload-data].

toolearn więcej informacji na temat tworzenia i zarządzania nią klastra usługi HDInsight, zobacz następujące artykuły hello:

* toolearn o zarządzaniu klaster usługi HDInsight opartej na systemie Linux, zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md).
* toolearn więcej informacji na temat opcji hello można wybrać podczas tworzenia klastra usługi HDInsight, zobacz [tworzenia HDInsight w systemie Linux przy użyciu niestandardowych opcji](hdinsight-hadoop-provision-linux-clusters.md).
* Jeśli zapoznali się z systemem Linux i usługę Hadoop, ale mają tooknow szczegóły dotyczące usługi Hadoop na powitania HDInsight, zobacz [pracy z usługą HDInsight w systemie Linux](hdinsight-hadoop-linux-information.md). Artykuł zawiera następujące informacje:
  
  * Adresy URL dla usług uruchamianych w klastrze hello, takich jak Ambari i WebHCat
  * Witaj lokalizację plików usługi Hadoop oraz przykłady hello lokalnego systemu plików
  * Użyj Hello z usługi Azure Storage (WASB) zamiast systemu plików HDFS jako hello domyślnego magazynu danych

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


