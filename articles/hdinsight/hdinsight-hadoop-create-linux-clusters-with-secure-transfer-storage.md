---
title: "Tworzenie klastra usługi Hadoop z kontami magazynu z bezpiecznym transferem w usłudze Azure HDInsight | Microsoft Docs"
description: "Dowiedz się, jak tworzyć klastry usługi HDInsight z kontami magazynu platformy Azure z bezpiecznym transferem."
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
ms.openlocfilehash: 370b2f081930fe88527436a1a127309aed6681f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>Tworzenie klastra usługi Hadoop z kontami magazynu z bezpiecznym transferem w usłudze Azure HDInsight

Funkcja [Wymagany bezpieczny transfer](../storage/common/storage-require-secure-transfer.md) poprawia bezpieczeństwo konta usługi Azure Storage poprzez wymuszanie kierowania wszystkich zapytań do konta przez zabezpieczone połączenie. Funkcja ta oraz schemat wasbs są obsługiwane tylko w klastrze usługi HDInsight w wersji 3.6 lub nowszym. 

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka potrzebna będzie:

* **Subskrypcja platformy Azure**: aby utworzyć bezpłatne konto próbne na jeden miesiąc, przejdź do [azure.microsoft.com/free](https://azure.microsoft.com/free).
* **Konto usługi Azure Storage z włączonym bezpiecznym transferem**. Aby uzyskać instrukcje, zobacz [Tworzenie konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) oraz [Wymaganie bezpiecznego transferu](../storage/common/storage-require-secure-transfer.md).
* **Kontener obiektów blob na koncie magazynu**. 
## <a name="create-cluster"></a>Tworzenie klastra

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


W tej sekcji tworzysz klaster Hadoop w usłudze HDInsight przy użyciu [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Szablon znajduje się w witrynie [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/). Znajomość szablonów usługi Resource Manager nie jest wymagana do korzystania z tego samouczka. Inne metody tworzenia klastrów i opis właściwości używanych w tym samouczku znajdziesz w artykule [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Kliknij poniższy obraz, aby zalogować się do platformy Azure i otworzyć szablon usługi Resource Manager w witrynie Azure Portal. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. Postępuj zgodnie z instrukcjami, aby utworzyć klaster o następujących specyfikacjach: 

    - Określ wersję usługi HDInsight na 3.6.  Domyślna wersja to 3.5. Wymagana jest wersja 3.6 lub nowsza.
    - Określ konto magazynu z włączonym bezpiecznym transferem.
    - Użyj krótkiej nazwy konta magazynu.
    - Konto magazynu i kontener obiektów blob należy utworzyć wcześniej. 

    Aby uzyskać instrukcje, zobacz [Tworzenie klastra](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). 

Jeśli użyjesz akcji skryptu do udostępnienia własnych plików konfiguracyjnych, musisz użyć rozwiązania wasbs w następujących ustawieniach:

- fs.defaultFS (lokacja podstawowa)
- spark.eventLog.dir 
- spark.history.fs.logDirectory

## <a name="add-additional-storage-accounts"></a>Dodawanie kolejnych kont magazynu

Dostępnych jest kilka opcji dodawania kolejnych kont magazynu z bezpiecznym transferem:

- Zmodyfikuj szablon usługi Azure Resource Manager w ostatniej sekcji.
- Utwórz klaster przy użyciu witryny [Azure Portal](https://portal.azure.com) i określ połączone konto magazynu.
- Użyj akcji skryptu, aby dodać kolejne konta magazynu z bezpiecznym transferem do istniejącego klastra usługi HDInsight.  Aby uzyskać więcej informacji, zobacz [Dodawanie kolejnych kont magazynu do usługi HDInsight](hdinsight-hadoop-add-storage.md).

## <a name="next-steps"></a>Następne kroki
W tym samouczku zawarto informacje dotyczące tworzenia klastra usługi HDInsight oraz włączania bezpiecznego transferu na kontach magazynu.

Aby dowiedzieć się więcej na temat analizowania danych za pomocą usługi HDInsight, zobacz następujące artykuły:

* Aby dowiedzieć się więcej o korzystaniu z programu Hive z usługą HDInsight, w tym poznać sposoby wykonywania zapytań Hive z programu Visual Studio, zobacz artykuł [Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive].
* Aby dowiedzieć się więcej na temat języka Pig, używanego do przekształcania danych, zobacz [Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig].
* Aby dowiedzieć się więcej o MapReduce, sposobie pisania programów przetwarzających dane w usłudze Hadoop, zobacz [Używanie MapReduce z usługą HDInsight][hdinsight-use-mapreduce].
* Aby dowiedzieć się więcej o używaniu narzędzi HDInsight Tools for Visual Studio do analizowania danych w usłudze HDInsight, zobacz [Wprowadzenie do używania narzędzi Visual Studio Hadoop dla usługi HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

Aby dowiedzieć się więcej o sposobie przechowywania danych przez usługę HDInsight lub sposobie przesyłania danych do usługi HDInsight, zobacz następujące artykuły:

* Aby uzyskać informacje o sposobie używania usługi Azure Storage przez usługę HDInsight, zobacz [Używanie usługi Azure Storage z usługą HDInsight](hdinsight-hadoop-use-blob-storage.md).
* Aby uzyskać informacje na temat przekazywania danych do usługi HDInsight, zobacz [Przekazywanie danych do usługi HDInsight][hdinsight-upload-data].

Aby dowiedzieć się więcej o tworzeniu klastra usługi HDInsight i zarządzaniu nim, zobacz następujące artykuły:

* Aby uzyskać więcej informacji na temat zarządzania opartym na systemie Linux klastrem usługi HDInsight, zobacz [Zarządzanie klastrami usługi HDInsight za pomocą narzędzia Ambari](hdinsight-hadoop-manage-ambari.md).
* Aby dowiedzieć się więcej na temat opcji, które można wybrać podczas tworzenia klastra usługi HDInsight, zobacz [Tworzenie klastra usługi HDInsight w systemie Linux przy użyciu niestandardowych opcji](hdinsight-hadoop-provision-linux-clusters.md).
* Jeśli znasz system Linux i usługę Hadoop, ale chcesz poznać szczegóły dotyczące usługi Hadoop w usłudze HDInsight, zobacz [Praca z usługą HDInsight w systemie Linux](hdinsight-hadoop-linux-information.md). Artykuł zawiera następujące informacje:
  
  * Adresy URL dla usług uruchamianych w klastrze, takich jak Ambari i WebHCat
  * Lokalizacja plików usługi Hadoop oraz przykłady lokalnego systemu plików
  * Korzystanie z usługi Azure Storage (WASB) zamiast systemu plików HDFS jako domyślnego magazynu danych

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


