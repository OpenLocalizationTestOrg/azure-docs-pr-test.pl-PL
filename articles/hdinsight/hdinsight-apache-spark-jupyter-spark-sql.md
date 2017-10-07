---
title: "klaster aaaCreate Apache Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Szybki Start Spark w usłudze HDInsight w sposób klastra toocreate Apache Spark w usłudze HDInsight."
keywords: spark quickstart,interactive spark,interactive query,hdinsight spark,azure spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a>Tworzenie klastra platformy Apache Spark w usłudze Azure HDInsight

W tym artykule dowiesz się, jak klaster toocreate Apache Spark w usłudze Azure HDInsight. Aby uzyskać informacje na temat klastra Spark w usłudze HDInsight, zobacz [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md).

   ![Diagram szybkiego startu opisujące kroki toocreate klastra Apache Spark w usłudze Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "szybkiego startu Spark przy użyciu platformy Apache Spark w usłudze HDInsight. Przedstawione kroki: tworzenie klastra; uruchamianie interakcyjnych zapytań Spark")

## <a name="prerequisites"></a>Wymagania wstępne

* **Subskrypcja platformy Azure**. Przed rozpoczęciem tego samouczka musisz dysponować subskrypcją platformy Azure. Zobacz [Utwórz bezpłatne konto platformy Azure już dzisiaj](https://azure.microsoft.com/free).

## <a name="create-hdinsight-spark-cluster"></a>Tworzenie klastra HDInsight Spark

W tej sekcji tworzysz klaster HDInsight Spark przy użyciu [szablonu usługi Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/). Aby zapoznać się z innymi metodami tworzenia klastra, zobacz temat [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Kliknij przycisk hello następującego szablonu hello tooopen obrazu w hello portalu Azure.         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Wprowadź hello następujące wartości:

    ![Tworzenie klastra HDInsight Spark przy użyciu szablonu usługi Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Tworzenie klastra Spark w usłudze HDInsight przy użyciu szablonu usługi Azure Resource Manager")

    * **Subskrypcja**: Wybierz swoją subskrypcję platformy Azure dla tego klastra.
    * **Grupa zasobów**: utwórz grupę zasobów lub wybierz istniejącą. Grupa zasobów jest toomanage używanych zasobów Azure dla projektów.
    * **Lokalizacja**: Wybierz lokalizację dla grupy zasobów hello. Szablon Hello używa tej lokalizacji do utworzenia klastra hello również podobnie jak w przypadku magazynu klastra hello domyślne.
    * **ClusterName**: Wprowadź nazwę klastra usługi HDInsight hello, które mają toocreate.
    * **Wersja platformy Spark**: Wybierz **2.0** jako wersja hello, które mają tooinstall na powitania klastra.
    * **Nazwa logowania i hasło klastra**: hello domyślna nazwa logowania to admin.
    * **Nazwa użytkownika i hasło SSH**.

   Zapisz te wartości.  Należy je później w samouczku hello.

3. Wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**, wybierz pozycję **toodashboard numeru Pin**, a następnie kliknij przycisk **zakupu**. Zostanie wyświetlony nowy kafelek zatytułowany Submitting deployment for Template deployment (Przesyłanie wdrożenia dla wdrożenia szablonu). Trwa około 20 minut toocreate hello klastra.

Jeśli napotkasz problem z tworzeniem klastrów usługi HDInsight, może to być, że nie masz hello toodo odpowiednie uprawnienia tak. Aby uzyskać więcej informacji, zobacz [wymagania dotyczące kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).

> [!NOTE]
> W tym artykule tworzy klaster Spark, która używa [obiektach blob magazynu Azure jako hello klastra magazynu](hdinsight-hadoop-use-blob-storage.md). Można również utworzyć klaster Spark, która używa [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) jako hello domyślny magazyn. Aby uzyskać instrukcje, zobacz [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) (Tworzenie klastra HDInsight z usługą Data Lake Store).
>
>

## <a name="run-a-hive-query-using-spark-sql"></a>Uruchomienie zapytania programu Hive za pomocą modułu Spark SQL

Gdy używasz notesu Jupyter skonfigurowane dla klastra Spark w usłudze HDInsight, możesz uzyskać predefiniowanego `sqlContext` służy toorun zapytań Hive przy użyciu programu Spark SQL. W tej sekcji omówiono sposób toostart notesu Jupyter, a następnie uruchom podstawowe zapytania Hive.

1. Otwórz hello [portalu Azure](https://portal.azure.com/).

2. Jeśli zgłoszono toopin hello klastra toohello z pulpitu nawigacyjnego, kliknij Kafelek klastra hello z bloku hello pulpitu nawigacyjnego toolaunch hello klastra.

    Jeśli nie przypiąć hello klastra toohello pulpitu nawigacyjnego, w okienku po lewej stronie powitania kliknij przycisk **klastrów usługi HDInsight**, a następnie kliknij przycisk hello klaster został utworzony.

3. W obszarze **Szybkie łącza** kliknij pozycję **Pulpity nawigacyjne klastra**, a następnie pozycję **Notes Jupyter**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.

   ![Otwórz Jupyter notebook toorun interakcyjne Spark SQL zapytania](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Jupyter Otwórz notesu toorun interakcyjne Spark SQL zapytań")

   > [!NOTE]
   > Mogą również uzyskać dostęp hello Jupyter notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce. Zastąp **CLUSTERNAME** o nazwie hello klastra:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Utwórz notes. Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.

   ![Utwórz Jupyter notebook toorun interakcyjne Spark SQL kwerendę](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "tworzenie Jupyter notebook toorun interakcyjne Spark SQL kwerendy")

   Nowy notes jest utworzony i otwarty o nazwie hello Untitled(Untitled.pynb).

4. Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę, jeśli chcesz.

    ![Podaj nazwę dla hello Jupter notesu toorun interakcyjne Spark zapytania z](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Podaj nazwę dla hello Jupter notesu toorun interakcyjne Spark zapytania z")

5.  Wklej hello następujący kod w pustej komórki, a następnie naciśnij **SHIFT + ENTER** toorun hello kodu. W poniższym kodzie hello `%%sql` (magic sql o nazwie hello) określa, że ustawienia wstępnego hello toouse notesu Jupyter `sqlContext` zapytanie Hive hello toorun. Witaj zapytanie pobiera hello górne 10 wiersze z tabeli programu Hive (**hivesampletable**) nie jest dostępna domyślnie na wszystkich klastrach usługi HDInsight.

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    ![Zapytanie programu Hive na platformie HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Zapytanie programu Hive na platformie HDInsight Spark")

    Aby uzyskać więcej informacji na temat hello `%%sql` magic i hello ustawień kontekstów, zobacz [Jupyter jądra dostępne dla klastra usługi HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

    > [!NOTE]
    > Przy każdym uruchomieniu kwerendy w oprogramowaniu Jupyter tytuł okna przeglądarki sieci web zawiera **(zajęty)** stan wraz z tytułem notesu hello. Zobacz też toohello dalej pełne kółko **PySpark** tekst w hello prawym górnym rogu. Po zakończeniu zadania hello zmienia tooa okrąg.
    >
    >
    
6. ekran Hello należy odświeżyć tooshow hello zapytania w danych wyjściowych.

    ![Wyniki zapytania programu Hive na platformie HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Wyniki zapytania programu Hive na platformie HDInsight Spark")

7. Zamknij zasobów klastra hello toorelease notesu powitania po zakończeniu działania aplikacji hello. toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**.

8. Jeśli planujesz toocomplete hello kolejne kroki w późniejszym czasie, upewnij się, że należy usunąć klaster usługi HDInsight hello utworzony w tym artykule. 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a>Następny krok 

W tym artykule przedstawiono sposób klastra Spark w usłudze HDInsight toocreate i wykonywania podstawowych Spark SQL zapytań. Wcześniejsze toohello dalej toolearn artykuł jak klastra Spark w usłudze HDInsight toouse toorun interakcyjnych zapytań na przykładowych danych.

> [!div class="nextstepaction"]
>[Run interactive queries on an HDInsight Spark cluster (Uruchamianie interakcyjnych zapytań w klastrze HDInsight Spark)](hdinsight-apache-spark-load-data-run-query.md)



