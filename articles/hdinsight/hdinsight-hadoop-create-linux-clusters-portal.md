---
title: "za pomocą przeglądarki sieci web - Azure HDInsight klastrów Hadoop aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się jak toocreate Hadoop, HBase, Storm i Spark klastrów w systemie Linux dla usługi HDInsight przy użyciu przeglądarki sieci web i hello Azure w wersji zapoznawczej portalu."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 63027e35e2d66dd76218aff3e0c085fc811736ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-azure-portal"></a>Tworzenie klastrów z systemem Linux w usłudze HDInsight przy użyciu hello portalu Azure
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Witaj Azure portal to narzędzie do zarządzania opartych na sieci web dla usług i zasobów przechowywanych w chmurze Microsoft Azure hello. W tym artykule dowiesz się, jak toocreate HDInsight opartych na systemie Linux klastrów za pomocą portalu hello.

## <a name="prerequisites"></a>Wymagania wstępne
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Nowoczesna przeglądarka sieci web**. Hello portalu Azure używa HTML5 i Javascript i mogą nie działać poprawnie w starszych przeglądarek sieci web.

## <a name="create-clusters"></a>Tworzenie klastrów
Hello Azure portal udostępnia większość hello właściwości klastra. Przy użyciu szablonu usługi Azure Resource Manager można ukryć dużej ilości informacji. Aby uzyskać więcej informacji, zobacz [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight przy użyciu szablonów usługi Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk  **+** , kliknij przycisk **analizy i analiza**, a następnie kliknij przycisk **HDInsight**.
   
    ![Tworzenie nowego klastra w portalu Azure hello](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "tworzenia nowego klastra w hello portalu Azure")

3. W hello **HDInsight** bloku, kliknij przycisk **niestandardowe (rozmiar, ustawienia aplikacji)**, kliknij przycisk **podstawowe informacje o**, a następnie wprowadź hello następujących informacji.

    ![Tworzenie nowego klastra w portalu Azure hello](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "tworzenia nowego klastra w hello portalu Azure")

    * Wprowadź wartość w polu **Nazwa klastra**: ta nazwa musi być globalnie unikatowa.

    * Z hello **subskrypcji** listy rozwijanej, wybierz pozycję hello subskrypcji platformy Azure, który będzie używany dla hello klastra.

    * Kliknij przycisk **typ klastra**, a następnie wybierz opcję:
   
        * **Typ klastra**: Jeśli nie wiesz, jakie toochoose, wybierz **Hadoop**. Jest hello najpopularniejszych typ klastra.
     
            > [!IMPORTANT]
            > HDInsight klastry są dostępne w różnych typów, które odpowiadają toohello obciążenia lub technologii, która hello klastra dostosowana pod kątem. Brak toocreate nie obsługiwaną metodą klastra, który łączy wiele typów, takie jak Storm i bazy danych HBase w jednym klastrze. 
            > 
            > 
        
        * **System operacyjny**: wybierz pozycję **Linux**.
        
        * **Wersja**: Użyj hello domyślnej wersji, jeśli nie wiesz, jakie toochoose. Więcej informacji można znaleźć w temacie [HDInsight cluster versions](hdinsight-component-versioning.md) (Wersje klastrów usługi HDInsight).
        * **Klaster warstwy**: Azure HDInsight zapewnia oferty chmury danych big data hello w dwóch różnych kategoriach: warstwy standardowa i Premium warstwy. Więcej informacji można znaleźć w temacie [Cluster tiers](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers) (Warstwy klastrów).

    * Dla **nazwa użytkownika logowania klastra** i **hasło logowania klastra**, podaj hello nazwę użytkownika i hasło dla użytkownika administracyjnego hello.

    * Wprowadź **nazwa użytkownika SSH** i hasło SSH hello toohave identyczny hello określone wcześniej hasło administratora, wybierz opcję hello **Użyj tego samego hasła jak logowania do klastra** pole wyboru. Jeśli nie, wprowadź wartość **hasło** lub **klucz PUBLICZNY**, które będzie używane tooauthenticate hello SSH użytkownika. Za pomocą klucza publicznego jest hello zalecane podejście. Kliknij przycisk **wybierz** na powitania dolnej toosave hello poświadczenia konfiguracji.
   
        Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

    * Aby uzyskać **grupy zasobów**, określ, czy mają toocreate nową grupę zasobów, czy użyć istniejącego.

    * Określ centrum danych **lokalizacji** której zostanie utworzona hello klastra.

    * Kliknij przycisk **Dalej**.

4. Na powitania **magazynu** bloku, określ, czy usługi Azure Storage (WASB) lub usługi Data Lake Store jako domyślnego magazynu. Spójrz na powitania tabelę poniżej, aby uzyskać więcej informacji.

    ![Tworzenie nowego klastra w portalu Azure hello](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "tworzenia nowego klastra w hello portalu Azure")

    | Magazyn                                      | Opis |
    |----------------------------------------------|-------------|
    | **Obiektów blob magazynu Azure jako domyślnego magazynu**   | <ul><li>Dla **typu podstawowego magazynu**, wybierz pozycję **usługi Azure Storage**. Po wykonaniu tej dla **metodę wyboru**, można wybrać **Moje subskrypcje** Jeśli chcesz toospecify konta magazynu, który jest częścią subskrypcji platformy Azure i wybierz opcję hello konto magazynu. W przeciwnym razie kliknij przycisk **klucz dostępu** hello informacje dla konta magazynu hello mają toochoose z poza subskrypcją platformy Azure.</li><li>Aby uzyskać **domyślny kontener**, można wybrać toogo o nazwie kontenera domyślnego hello zasugerowany przez hello portal lub określić własne.</li><li>Jeśli używasz WASB jako domyślny magazyn, (opcjonalnie) można kliknąć **dodatkowych kont magazynu** toospecify dodatkowy magazyn kont tooassociate hello klastra. W hello **klucze magazynu Azure** bloku, kliknij przycisk **Dodaj klucz magazynu**, i można podać konto magazynu z subskrypcjami platformy Azure lub inne subskrypcje (przez dostarczanie hello konta magazynu klucz dostępu).</li><li>Jeśli używasz WASB jako domyślny magazyn, (opcjonalnie) można kliknąć **dostępu do usługi Data Lake Store** toospecify Azure Data Lake Store jako dodatkowego magazynu. Aby uzyskać więcej informacji, zobacz [tworzenia klastra usługi HDInsight z Data Lake Store przy użyciu portalu Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</li></ul> |
    | **Azure Data Lake Store jako domyślnego magazynu** | Dla **typu podstawowego magazynu**, wybierz pozycję **usługi Data Lake Store** , a następnie przeczytaj artykuł toohello [tworzenia klastra usługi HDInsight z Data Lake Store przy użyciu portalu Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) dla instrukcje. |
    | **Zewnętrznych magazynów metadanych**                      | Opcjonalnie można określić SQL bazy danych toosave Hive i Oozie metadane skojarzone z hello klastra. Aby uzyskać **wybierz bazę danych SQL dla gałęzi** wybierz bazę danych SQL, a następnie podaj hello nazwy użytkownika i hasła dla hello bazy danych. Powtórz te kroki dla metadanych Oozie.<br><br>Niektóre kwestie wymagające rozważenia podczas korzystania z bazy danych Azure SQL dla magazynów metadanych. <ul><li>Baza danych Azure SQL Hello używane na potrzeby magazynu metadanych hello muszą zezwalać tooother łączności usług Azure, w tym Azure HDInsight. Na powitania nawigacyjnym bazy danych Azure SQL, na powitania po prawej stronie kliknij nazwę serwera hello. Jest to serwer hello, na które hello SQL jest uruchomione wystąpienie bazy danych. Po przejściu na powitania serwera widok, kliknij przycisk **Konfiguruj**, a następnie **usług Azure**, kliknij przycisk **tak**, a następnie kliknij przycisk **zapisać**.</li><li>Podczas tworzenia potrzeby magazynu metadanych, nie należy używać nazwy bazy danych, która zawiera łączniki lub łączników, ponieważ może to spowodować toofail procesu tworzenia klastra hello.</li></ul>                                                                                                                                                                       |

    Kliknij przycisk **Dalej**. 

    > [!WARNING]
    > Przy użyciu konta, dodatkowe miejsce do magazynowania w innej lokalizacji niż hello klastra usługi HDInsight nie jest obsługiwane.

5. Opcjonalnie kliknij **aplikacji** aplikacji tooinstall, które działają z klastrami usługi HDInsight. Te aplikacje mogą być opracowane przez firmę Microsoft, niezależnych dostawców oprogramowania (ISV) lub samodzielnie. Aby uzyskać więcej informacji, zobacz [HDInsight zainstalować aplikacje](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).


6. Kliknij przycisk **rozmiar klastra** toodisplay informacji o węzłach hello, które zostaną utworzone dla tego klastra. Ustaw hello liczba węzłów procesu roboczego, wymagające hello klastra. Hello szacuje się, że koszt hello klastra będą wyświetlane w bloku hello.
   
    ![Węzeł bloku warstw cenowych](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "Określ liczbę węzłów klastra")
   
   > [!IMPORTANT]
   > Jeśli planujesz na więcej niż 32 węzłami procesów roboczych, pamięci ram na utworzenie klastra lub przez skalowanie klastra hello po utworzeniu, a następnie należy wybrać rozmiar węzła głównego z co najmniej 8 rdzeniami i 14GB.
   > 
   > Aby uzyskać więcej informacji na węzeł rozmiary i koszty, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   > 
   > 
   
   Kliknij przycisk **dalej** węzła hello toosave cennik konfiguracji.

7. Kliknij przycisk **Zaawansowane ustawienia** tooconfigure inne opcjonalne ustawienia, takie jak przy użyciu **akcji skryptu** toocustomize tooinstall klastra niestandardowych składników lub przyłączenie **sieciwirtualnej**. Spójrz na powitania tabelę poniżej, aby uzyskać więcej informacji.

    ![Węzeł bloku warstw cenowych](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "Określ liczbę węzłów klastra")

    | Opcja | Opis |
    |--------|-------------|
    | **Akcje skryptu** | Użyj tej opcji, jeśli chcesz toouse toocustomize skryptu niestandardowego klastra, tworzenia hello klastra. Aby uzyskać więcej informacji na temat akcji skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md). |
    | **Virtual Network** | Wybierz Azure sieci i hello podsieci wirtualnej, jeśli chcesz tooplace hello klastra w sieci wirtualnej. Informacji dotyczących korzystania z usługi HDInsight z sieci wirtualnej, włączając określone wymagania konfiguracji dla hello sieci wirtualnej, zobacz [możliwości rozszerzania HDInsight przy użyciu sieci wirtualnej platformy Azure](hdinsight-extend-hadoop-virtual-network.md). |

    Kliknij przycisk **Dalej**.

8. Na powitania **Podsumowanie** bloku, sprawdź informacje dotyczące hello wprowadzony wcześniej, a następnie kliknij przycisk **Utwórz**.

    ![Węzeł bloku warstw cenowych](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "Określ liczbę węzłów klastra")
    
    > [!NOTE]
    > Upłynąć trochę czasu, zanim toobe klastra hello utworzona, zwykle około 15 minut. Użyj kafelka hello na powitania tablicy startowej lub hello **powiadomienia** wpis na powitania rogu toocheck strony hello na powitania w procesie inicjowania obsługi.
    > 
    > 
12. Po zakończeniu procesu tworzenia powitania kliknij Kafelek hello hello klastra z bloku hello tablicy startowej toolaunch hello klastra. Witaj bloku klastra zawiera hello następujących informacji.
    
    ![Bloku klastra](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "właściwości klastra")
    
    Użyj hello następujące ikony hello toounderstand u góry hello tego bloku.
    
    * **Omówienie** karta zawiera wszystkie informacje niezbędne hello o hello klastra, takie jak nazwa hello, grupy zasobów hello należy on do hello lokalizacji hello systemu operacyjnego, adres URL dla pulpitu nawigacyjnego klastra hello itp.
    * **Pulpit nawigacyjny** kieruje użytkownika portalu Ambari toohello skojarzony z klastrem hello.
    * **Secure Shell**: informacje niezbędne tooaccess hello klastra przy użyciu protokołu SSH.
    * **Klaster w skali** pozwala zwiększyć hello liczba węzłów procesu roboczego związane z klastrem hello.
    * **Usuń**: usuwa hello HDInsight klastra.
    

## <a name="customize-clusters"></a>Dostosowywanie klastrów
* Zobacz [HDInsight dostosować klastry za pomocą początkowego](hdinsight-hadoop-customize-cluster-bootstrap.md).
* Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Usuń klaster hello
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Rozwiązywanie problemów

W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Następne kroki
Po pomyślnym utworzeniu klastra usługi HDInsight, za pomocą powitania po toolearn jak toowork z klastrem:

### <a name="hadoop-clusters"></a>Klastry Hadoop
* [Korzystanie z programu Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
* [Korzystać z usługi MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Klastrów HBase
* [Rozpoczynanie pracy z bazy danych HBase w usłudze HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Tworzenie aplikacji Java bazy danych hbase w usłudze HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Klastry STORM
* [Tworzenie topologii Java dla Storm w usłudze HDInsight](hdinsight-storm-develop-java-topology.md)
* [Użyj składników języka Python w Storm w usłudze HDInsight](hdinsight-storm-develop-python-topology.md)
* [Wdrażanie i monitorowanie topologii z systemu Storm w usłudze HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Klastry Spark
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)

