---
title: "Akcja aaaScript — Python Zainstaluj pakiety z Jupyter w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Instrukcje krok po kroku na jak notesów Jupyter tooconfigure toouse akcji skryptu, które zostały dostępne z Spark w usłudze HDInsight clusters toouse python zewnętrznych pakietów."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Korzystanie z zewnętrznych pakietów języka Python akcji skryptu tooinstall w notesów Jupyter w klastrach Apache Spark w usłudze HDInsight
> [!div class="op_single_selector"]
> * [Przy użyciu magic komórki](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Za pomocą akcji skryptu](hdinsight-apache-spark-python-package-installation.md)
>
>

Dowiedz się, jak tooconfigure akcji skryptu toouse klastra Apache Spark w zewnętrznej toouse HDInsight (Linux), społeczności-przyczyniły się **python** pakiety, które nie są objęte poza pole hello klastra.

> [!NOTE]
> Można również skonfigurować za pomocą notesu Jupyter `%%configure` Magiczna toouse pakiety zewnętrzne. Aby uzyskać instrukcje, zobacz [korzystanie z zewnętrznych pakietów z notesami Jupyter w klastrach Apache Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).
> 
> 

Możesz przeszukać hello [indeksu pakietów](https://pypi.python.org/pypi) dla hello pełną listę pakietów, które są dostępne. Można również uzyskać listę dostępnych pakietów z innych źródeł. Na przykład można zainstalować pakietów dostępne za pośrednictwem [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) lub [conda forge](https://conda-forge.github.io/feedstocks.html).

W tym artykule przedstawiono sposób tooinstall hello [TensorFlow](https://www.tensorflow.org/) pakietu przy użyciu skryptu Actoin w klastrze i używać go za pomocą notesu Jupyter hello.

## <a name="prerequisites"></a>Wymagania wstępne
Musi mieć następujące hello:

* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

   > [!NOTE]
   > Jeśli nie masz już klastra Spark w usłudze HDInsight w systemie Linux, można uruchomić akcji skryptu podczas tworzenia klastra. Odwiedź stronę dokumentacji hello na [jak niestandardowe toouse skryptu akcji](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a>Korzystanie z zewnętrznych pakietów z notesami Jupyter

1. Z hello [Azure Portal](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej). Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.   

2. W bloku klastra Spark powitania kliknij **akcji skryptu** w obszarze **użycia**. Uruchom hello akcji niestandardowej, która instaluje TensorFlow hello węzłów głównych i węzłów procesu roboczego hello. skrypt bash Hello mogą być przywoływane z: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh odwiedziny hello dokumentacji w [jak niestandardowe toouse skryptu akcji](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

   > [!NOTE]
   > Istnieją dwa python instalacje hello klastra. Platforma Spark użyje instalacji języka python Anaconda hello znajdujący się w `/usr/bin/anaconda/bin`. Odwołanie tę instalację w akcje niestandardowe za pośrednictwem `/usr/bin/anaconda/bin/pip` i `/usr/bin/anaconda/bin/conda`.
   > 
   > 

3. Otwórz notesu PySpark Jupyter

    ![Tworzenie nowego notesu Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Tworzenie nowego notesu Jupyter")

4. Nowy notes jest utworzony i otwarty z hello nazwie Untitled.pynb. Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę.

    ![Podaj nazwę notesu hello](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Podaj nazwę notesu hello")

5. Możesz teraz będzie `import tensorflow` i uruchom przykład Witaj świecie. 

    Toocopy kodu:

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    wynik Hello będzie wyglądać następująco:
    
    ![Wykonanie kodu TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "TensorFlow wykonanie kodu")



## <a name="seealso"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter w klastrach Apache Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)
