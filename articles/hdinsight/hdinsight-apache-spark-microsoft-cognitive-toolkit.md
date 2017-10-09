---
title: "aaaMicrosoft kognitywnych Toolkit z usługi Azure HDInsight Spark dla głębokości learning | Dokumentacja firmy Microsoft"
description: "Dowiedzieć się, jak przeszkolone kognitywnych zestaw narzędzi firmy Microsoft głębokie uczenie modelu mogą być zastosowane tooa zestawu danych za pomocą hello interfejsu API języka Python Spark w klastrze usługi Azure HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a>Użyj głębokiego uczenie modelu z klastrem usługi Azure HDInsight Spark Toolkit kognitywnych firmy Microsoft

W tym artykule hello następujące kroki.

1. Uruchomienie skryptu niestandardowego tooinstall kognitywnych zestaw narzędzi firmy Microsoft w klastrze Spark w usłudze HDInsight Azure.

2. Jak przekazać toosee klastra Spark toohello Jupyter notebook tooapply przeszkolone kognitywnych zestaw narzędzi firmy Microsoft głębokie uczenia modelu toofiles na koncie magazynu obiektów Blob Azure przy użyciu hello [interfejsu API języka Python Spark (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)

## <a name="prerequisites"></a>Wymagania wstępne

* **Subskrypcja platformy Azure**. Przed rozpoczęciem tego samouczka musisz dysponować subskrypcją platformy Azure. Zobacz [Utwórz bezpłatne konto platformy Azure już dzisiaj](https://azure.microsoft.com/free).

* **Azure klastra Spark w usłudze HDInsight**. W tym artykule należy utworzyć klaster Spark 2.0. Aby uzyskać instrukcje, zobacz [klastra Utwórz Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-does-this-solution-flow"></a>Jak przepływu tego rozwiązania?

To rozwiązanie jest dzielona między w tym artykule i notesu Jupyter, który należy przekazać w ramach tego samouczka. W tym artykule możesz wykonać hello następujące kroki:

* Uruchom akcję skryptu w klastrze Spark w usłudze HDInsight tooinstall pakietów kognitywnych zestaw narzędzi firmy Microsoft i Python.
* Przekaż notesu Jupyter hello uruchomioną hello toohello rozwiązanie klastra Spark w usłudze HDInsight.

Witaj następujące pozostałe kroki są objęte hello notesu Jupyter.

- Załaduj przykładowe obrazy do Spark Resiliant dystrybuowane w zestawie danych lub RDD
   - Ładowanie modułów i zdefiniować ustawienia
   - Pobierz zestaw danych hello lokalnie w klastrze Spark hello
   - Konwertowanie hello dataset RDD
- Wynik hello obrazów za pomocą uczonego modelu kognitywnych Toolkit
   - Pobierz klastra Spark toohello hello uczony kognitywnych Toolkit modelu
   - Zdefiniuj toobe funkcje używane przez węzłów procesu roboczego
   - Obrazy hello wynik w węzłów procesu roboczego
   - Ocena dokładności modelu


## <a name="install-microsoft-cognitive-toolkit"></a>Zainstaluj kognitywnych zestaw narzędzi firmy Microsoft

Kognitywnych zestaw narzędzi firmy Microsoft można zainstalować w klastrze Spark przy użyciu akcji skryptu. Akcja skryptu używa niestandardowych skryptów tooinstall składników w klastrze hello, które nie są domyślnie dostępne. Przy użyciu zestawu .NET SDK usługi HDInsight lub przy użyciu programu Azure PowerShell, można użyć skryptu niestandardowego hello z hello portalu Azure. Umożliwia także hello skryptu tooinstall hello toolkit albo w ramach tworzenia klastra, lub po hello klastrowania jest uruchomiona. 

W tym artykule używamy zestawu narzędzi hello portalu tooinstall hello, po utworzeniu klastra hello. Inne sposoby toorun hello niestandardowego skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

### <a name="using-hello-azure-portal"></a>Przy użyciu hello portalu Azure

Aby uzyskać instrukcje dotyczące sposobu toorun Azure Portal hello toouse skryptu akcji, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation). Upewnij się, że podajesz hello następujące dane wejściowe tooinstall kognitywnych zestaw narzędzi firmy Microsoft.

* Podaj wartość dla nazwy akcji skryptu hello.

* Aby uzyskać **Bash skryptu URI**, wprowadź `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.

* Upewnij się, uruchamiasz skryptu hello na powitania head i proces roboczy węzłów i usuń zaznaczenie wszystkich hello inne pola wyboru.

* Kliknij przycisk **Utwórz**.

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a>Przekaż tooAzure notesu Jupyter hello klastra Spark w usłudze HDInsight

Witaj toouse kognitywnych zestaw narzędzi firmy Microsoft hello Azure HDInsight Spark klastra, należy załadować notesu Jupyter hello **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark klastra. Ten notes jest dostępna w witrynie GitHub pod [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).

1. Repozytorium GitHub hello w klonowania [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration). Aby tooclone instrukcje, zobacz [klonowanie repozytorium](https://help.github.com/articles/cloning-a-repository/).

2. Z hello portalu Azure, otwórz hello bloku klastra Spark, który już zainicjowano obsługę administracyjną, kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Jupyter**.

    Można również uruchomić notesu Jupyter hello korzystając z adresu toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`. Zastąp \<clustername > o nazwie hello klastra usługi HDInsight.

3. Z notesu Jupyter hello, kliknij przycisk **przekazać** w prawym górnym rogu Witaj, a następnie przejdź toohello lokalizacji, gdzie sklonować repozytorium GitHub hello.

    ![Przekaż tooAzure notesu Jupyter klastra Spark w usłudze HDInsight](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "tooAzure notesu Jupyter przekazać klastra Spark w usłudze HDInsight")

4. Kliknij przycisk **przekazać** ponownie.

5. Po przekazaniu notesu hello kliknij nazwę notesu hello hello, a następnie wykonaj instrukcje hello w notesie hello, sam na jak tooload hello zestawu danych i wykonywać hello samouczka.

## <a name="see-also"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Analiza danych telemetrycznych usługi Application Insight przy użyciu platformy Spark w usłudze HDInsight](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
