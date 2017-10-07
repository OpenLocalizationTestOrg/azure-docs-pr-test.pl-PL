---
title: "aaaGet wprowadzenie do usług Hadoop i Hive w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate HDInsight clusters i dane zapytań Hive."
keywords: "wprowadzenie do usługi hadoop,hadoop linux,hadoop szybki start,wprowadzenie do usługi hive,hive szybki start"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6a12ed4c-9d49-4990-abf5-0a79fdfca459
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: 3d96d78121200ebda3626dd2c3885e3ddacd546d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hadoop-tutorial-get-started-using-hadoop-in-hdinsight"></a>Samouczek Hadoop: rozpoczęcie korzystania z usługi Hadoop w usłudze HDInsight

Dowiedz się, jak toocreate [Hadoop](http://hadoop.apache.org/) klastrów usługi HDInsight i jak zadania toorun Hive w usłudze HDInsight. [Apache Hive](https://hive.apache.org/) jest hello najbardziej popularnym składnikiem w ekosystemie Hadoop hello. Obecnie usługa HDInsight obejmuje [siedem różnych typów klastrów](hdinsight-hadoop-introduction.md#overview). Każdy typ klastra obsługuje inny zestaw składników. Wszystkie typy klastrów obsługują technologię Hive. Aby uzyskać listę obsługiwanych składników w usłudze HDInsight, zobacz [nowości w wersjach klastra Hadoop hello dostarczanych z usługą HDInsight?](hdinsight-component-versioning.md)  

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka potrzebna będzie:

* **Subskrypcja platformy Azure**: toocreate bezpłatne konto próbne jeden miesiąc, przejdź zbyt[azure.microsoft.com/free](https://azure.microsoft.com/free).

## <a name="create-cluster"></a>Tworzenie klastra

Większość zadań usługi Hadoop to zadania wsadowe. Możesz utworzyć klaster, uruchamiasz pewne zadania, a następnie usuń hello klastra. W tej sekcji tworzysz klaster Hadoop w usłudze HDInsight przy użyciu [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Znajomość szablonów usługi Resource Manager nie jest wymagana do korzystania z tego samouczka. Inne metody tworzenia klastrów i opis właściwości hello używane w tym samouczku, zobacz [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Selektor hello na początku hello hello toochoose strony opcji tworzenia klastra.

Szablon usługi Resource Manager Hello używane w tym samouczku znajduje się w [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/). 

1. Kliknij przycisk hello toosign obrazu w tooAzure i otwórz hello szablonu usługi Resource Manager w hello portalu Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Wprowadź lub wybierz hello następujące wartości:
   
    ![HDInsight Linux wprowadzenie do szablonu usługi Resource Manager w portalu](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "hello wdrażanie klastra usługi Hadoop w HDInsigut przy użyciu portalu Azure i szablon Menedżera zasobów grupy").
   
    * **Subskrypcja**: wybierz subskrypcję platformy Azure.
    * **Grupa zasobów**: utwórz grupę zasobów lub wybierz istniejącą.  Grupa zasobów jest kontenerem składników platformy Azure.  W takim przypadku hello grupa zasobów zawiera hello klastra usługi HDInsight i hello zależne konto magazynu Azure. 
    * **Lokalizacja**: Wybierz Azure lokalizację toocreate klastra.  Wybierz tooyou bliżej lokalizacji, w celu poprawy wydajności. 
    * **Typ klastra**: na potrzeby tego samouczka wybierz opcję **hadoop**.
    * **Nazwa klastra**: Wprowadź nazwę klastra usługi Hadoop hello.
    * **Nazwa logowania i hasło klastra**: hello domyślna nazwa logowania jest **admin**.
    * **Nazwa użytkownika SSH i hasło**: hello domyślna nazwa użytkownika to **sshuser**.  Tę nazwę można zmienić. 
     
    Niektóre właściwości zostały zapisane na stałe w szablonie hello.  Możesz skonfigurować te wartości z hello szablonu.

    * **Lokalizacja**: hello lokalizacji hello klastra i hello udziału konto magazynu zależnego hello tej samej lokalizacji co hello grupy zasobów.
    * **Wersja klastra**: 3.5
    * **Typ systemu operacyjnego**: Linux
    * **Liczba węzłów procesu roboczego**: 2

     Każdy klaster zależy od [konta usługi Azure Storage](hdinsight-hadoop-use-blob-storage.md) lub od [konta usługi Azure Data Lake](hdinsight-hadoop-use-data-lake-store.md). Nazywa hello domyślne konto magazynu. Klaster usługi HDInsight i jego domyślne konto magazynu muszą znajdować się w hello tego samego regionu systemu Azure. Usunięcie klastrów nie powoduje usunięcia konta magazynu hello. 
     
     Aby uzyskać więcej informacji o tych właściwościach, zobacz [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Tworzenie klastrów platformy Hadoop w usłudze HDInsight).

3. Wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano** i **toodashboard numeru Pin**, a następnie kliknij przycisk **zakupu**. Powinien zostać wyświetlony nowy Kafelek zatytułowany **wdrażanie szablonu wdrożenia** na powitania pulpitu nawigacyjnego portalu. Trwa około 20 minut toocreate klastra. Po utworzeniu klastra hello hello podpis kafelka hello jest zmienione toohello Nazwa grupy zasobów, określona. I hello portal automatycznie otwiera hello grupy zasobów w nowym bloku. Widać zarówno hello klastra i hello domyślnego magazynu na liście.
   
    ![Grupa zasobów wprowadzenia do usługi HDInsight Linux](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Grupa zasobów klastra usługi Azure HDInsight").

4. Kliknij przycisk hello klastra hello tooopen nazwy klastra w nowym bloku.

   ![Ustawienia klastra wprowadzenia do usługi HDInsight Linux](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "Właściwości klastra usługi HDInsight")


## <a name="run-hive-queries"></a>Uruchamianie zapytań Hive
[Apache Hive](hdinsight-use-hive.md) jest hello najbardziej popularnym składnikiem używanym w usłudze HDInsight. Istnieje wiele sposobów toorun zadań Hive w usłudze HDInsight. W tym samouczku użyjesz widoku Hive narzędzia Ambari z portalu hello hello. Aby poznać inne metody przesyłania zadań Hive, zobacz temat [Używanie Hive w usłudze HDInsight](hdinsight-use-hive.md).

1. Poprzedni zrzut ekranu powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **pulpit nawigacyjny klastra usługi HDInsight**.  Można również przeglądać za **https://&lt;ClusterName >. azurehdinsight.net**, gdzie &lt;ClusterName > to klaster hello utworzony w sekcji poprzedniej hello tooopen Ambari.
2. Wprowadź nazwę użytkownika Hadoop hello i hasło określone w poprzedniej sekcji hello. Witaj domyślna nazwa użytkownika to **admin**.
3. Otwórz **Hive View** pokazane na powitania po zrzut ekranu:
   
    ![Wybieranie widoków Ambari](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "Menu przeglądarki HDInsight Hive").
4. W hello **edytora zapytań** sekcji hello strony, Wklej hello następujące instrukcje HiveQL do arkusza hello:
   
        SHOW TABLES;
   
   > [!NOTE]
   > Średnik jest wymagany przez Hive.       
   > 
   > 
5. Kliknij przycisk **Execute** (Wykonaj). A **wyniki przetwarzania zapytania** sekcji powinien pojawić się pod hello edytora zapytań i wyświetlania informacji o hello zadania. 
   
    Po zakończeniu hello zapytania, hello **wyniki przetwarzania zapytania** sekcja wyświetla wyniki hello hello operacji. Powinna być widoczna jedna tabela o nazwie **hivesampletable**. Ta przykładowa Tabela składnika Hive jest dostarczany z wszystkie klastry usługi HDInsight hello.
   
    ![Widoki usługi HDInsight Hive](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "Edytor zapytań widoku usługi HDInsight Hive").
6. Powtórz kroki 4 i hello toorun kroku 5, następujące zapytanie:
   
        SELECT * FROM hivesampletable;
   
   > [!TIP]
   > Uwaga hello **Zapisz wyniki** listy rozwijanej w hello górnym lewym rogu hello **wyniki przetwarzania zapytania** sekcji; Użyj tego hello wyniki pobierania tooeither lub zapisać je tooHDInsight magazynu w pliku CSV.
   > 
   > 
7. Kliknij przycisk **historii** tooget listy zadań hello.

Po zakończeniu zadania Hive można [wyeksportować hello wyniki tooAzure SQL database lub SQL Server](hdinsight-use-sqoop-mac-linux.md), możesz również [wizualizacja wyników hello przy użyciu programu Excel](hdinsight-connect-excel-power-query.md). Aby uzyskać więcej informacji o korzystaniu z Hive w usłudze HDInsight, zobacz [używanie Hive i HiveQL z usługą Hadoop w HDInsight tooanalyze przykładowego pliku Apache log4j](hdinsight-use-hive.md).

## <a name="clean-up-hello-tutorial"></a>Wyczyść hello samouczka
Po ukończeniu samouczka hello można toodelete hello klastra. Dzięki usłudze HDInsight dane są przechowywane w usłudze Azure Storage, więc można bezpiecznie usunąć klaster, gdy nie jest używany. Opłaty za klaster usługi HDInsight są naliczane nawet wtedy, gdy nie jest używany. Ponieważ hello opłaty za klaster hello są wielokrotnie większe niż hello opłaty za magazyn, warto gospodarczego toodelete klastrów, gdy nie są używane. 

> [!NOTE]
> Przy użyciu [fabryki danych Azure](hdinsight-hadoop-create-linux-clusters-adf.md), tworzenia klastrów usługi HDInsight na żądanie i skonfigurować TimeToLive ustawienie zbyt usuwać klastry hello automatycznie. 
> 
> 

**toodelete hello klastra i/lub hello domyślne konto magazynu**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Z pulpitu nawigacyjnego portalu hello kliknij Kafelek hello z hello Nazwa grupy zasobów, używane podczas tworzenia klastra hello.
3. Kliknij przycisk **usunąć** na hello zasobów bloku toodelete hello grupę zasobów, zawierającą hello klastra i hello domyślne konto magazynu; lub kliknij nazwę klastra hello na powitania **zasobów** Kafelek, a następnie kliknij przycisk **Usunąć** na powitania bloku klastra. Usunięcie grupy zasobów hello Uwaga usuwa hello konta magazynu. Konto magazynu hello tookeep, wybierz opcję toodelete hello tylko klastra.

## <a name="troubleshoot"></a>Rozwiązywanie problemów

W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Następne kroki
W tym samouczku wiesz już, jak toocreate usługi HDInsight opartej na systemie Linux klastrem, używając szablonu usługi Resource Manager i jak tooperform podstawowe zapytania Hive.

toolearn więcej informacji na temat analizowania danych z usługą HDInsight, zobacz następujące artykuły hello:

* toolearn więcej informacji o korzystaniu z programu Hive z usługą HDInsight, w tym, jak tooperform Hive zapytań z programu Visual Studio, zobacz [używanie Hive z usługą HDInsight][hdinsight-use-hive].
* toolearn temat Pig, języka używany tootransform danych, zobacz [Use Pig z usługą HDInsight][hdinsight-use-pig].
* toolearn o MapReduce, sposób programy toowrite, które przetwarzają dane w usłudze Hadoop, zobacz [Użyj MapReduce z usługą HDInsight][hdinsight-use-mapreduce].
* toolearn o za pomocą hello narzędzi HDInsight Visual Studio tooanalyze danych w usłudze HDInsight, zobacz [rozpocząć korzystanie z narzędzi Visual Studio Hadoop dla usługi HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

Jeśli wszystko gotowe toostart Praca z danych użytkownika i należy tooknow więcej na temat sposobu HDInsight przechowuje dane lub jak tooget dane do usługi HDInsight, zobacz następujące hello:

* Aby uzyskać informacje o sposobie używania usługi Azure Storage przez usługę HDInsight, zobacz [Używanie usługi Azure Storage z usługą HDInsight](hdinsight-hadoop-use-blob-storage.md).
* Aby uzyskać informacje na temat tooupload tooHDInsight danych, zobacz [przekazywanie danych tooHDInsight][hdinsight-upload-data].

Jeśli chcesz toolearn więcej informacji na temat tworzenia i zarządzania nią klastra usługi HDInsight, zobacz następujące hello:

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


