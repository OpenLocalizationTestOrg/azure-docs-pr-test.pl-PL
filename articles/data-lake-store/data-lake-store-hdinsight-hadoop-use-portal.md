---
title: "klastry aaaUse hello Azure toocreate portalu Azure HDInsight z usługą Data Lake Store | Dokumentacja firmy Microsoft"
description: "Użyj hello toocreate portalu Azure i klastry usługi HDInsight za pomocą usługi Azure Data Lake Store"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a>Tworzenie klastrów usługi HDInsight z usługą Data Lake Store za pomocą hello portalu Azure
> [!div class="op_single_selector"]
> * [Użyj hello portalu Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Przy użyciu programu PowerShell (do magazynu domyślnego)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Przy użyciu programu PowerShell (dla dodatkowego magazynu)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Użyj Menedżera zasobów](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Dowiedz się, jak toouse hello Azure toocreate portalu klastra usługi HDInsight przy użyciu konta usługi Azure Data Lake Store jako magazynu domyślne hello lub dodatkowego magazynu. Mimo że dodatkowe miejsce do magazynowania jest opcjonalne dla klastra usługi HDInsight, jest zalecane toostore danych biznesowych w hello dodatkowych kont magazynu.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka, upewnij się, że zostały spełnione następujące wymagania hello:

* **Subskrypcja platformy Azure**. Przejdź za[Azure Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/).
* **Konto usługi Azure Data Lake Store**. Postępuj zgodnie z instrukcjami hello [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](data-lake-store-get-started-portal.md). Należy również utworzyć folderem głównym na koncie hello.  W tym samouczku folderu głównego o nazwie __/klastrów__ jest używany.
* **Nazwy głównej usługi Azure Active Directory**. Ten samouczek zawiera instrukcje na temat toocreate nazwy głównej usługi w usłudze Azure Active Directory (Azure AD). Jednak toocreate nazwy głównej usługi, musisz być administratorem usługi Azure AD. Jeśli jesteś administratorem, możesz pominąć te wymagania wstępne i kontynuować hello samouczka.

    >[!NOTE]
    >Usługi można utworzyć podmiot, tylko wtedy, gdy administrator usługi Azure AD. Administrator usługi Azure AD należy utworzyć usługę podmiotu zabezpieczeń przed utworzeniem klastra usługi HDInsight z usługą Data Lake Store. Także hello nazwy głównej usługi musi zostać utworzony przy użyciu certyfikatu zgodnie z opisem w [Tworzenie nazwy głównej usługi o certyfikat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).
    >

## <a name="create-an-hdinsight-cluster"></a>Tworzenie klastra usługi HDInsight

W tej sekcji utworzysz klastra usługi HDInsight przy użyciu kont usługi Data Lake Store jako domyślny hello lub hello dodatkowego magazynu. Ten artykuł dotyczy tylko część hello konfigurowania kont usługi Data Lake Store.  Aby uzyskać informacji o tworzeniu klastra ogólne hello i procedury, zobacz [klastrów utworzyć Hadoop w HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a>Tworzenie klastra z usługą Data Lake Store jako domyślnego magazynu

**toocreate HDInsight klaster z usługi Data Lake Store jako hello domyślne konto magazynu**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Postępuj zgodnie z [Tworzenie klastrów](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) hello ogólne informacje na temat tworzenia klastrów usługi HDInsight.
3. Na powitania **magazynu** bloku, w obszarze **typu podstawowego magazynu**, wybierz pozycję **usługi Data Lake Store**, a następnie wprowadź hello następujących informacji:

    ![Dodaj usługi głównej tooHDInsight klastra](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "Dodaj usługi głównej tooHDInsight klastra")

    - **Konto usługi Data Lake Store wybierz**: Wybierz istniejące konto usługi Data Lake Store. Istniejące konto usługi Data Lake Store jest wymagany.  Zobacz [wymagania wstępne](#prereuisites).
    - **Ścieżka katalogu głównego**: wprowadź ścieżkę, w którym pliki specyficznych dla klastra hello są przechowywane toobe. Na zrzucie ekranu pokazano hello jest __/klastrów/myhdiadlcluster/__, w których hello __/klastrów__ folder musi istnieć i hello Portal tworzy *myhdicluster* folderu.  Witaj *myhdicluster* jest nazwą klastra hello.
    - **Dostęp do usługi Data Lake Store**: Konfigurowanie dostępu między hello konto usługi Data Lake Store i klaster usługi HDInsight. Aby uzyskać instrukcje, zobacz [dostępu Konfiguruj Data Lake Store](#configure-data-lake-store-access).
    - **Dodatkowe konta magazynu**: Dodawanie konta magazynu Azure jako dodatkowy magazyn kont hello klastra. tooadd dodatkowe Lake następującą liczbę magazynów danych odbywa się przez nadanie uprawnień klastra hello na danych więcej kont usługi Data Lake Store podczas konfigurowania konta usługi Data Lake Store jako typu podstawowego magazynu hello. Zobacz [Konfigurowanie dostępu do usługi Data Lake Store](#configure-data-lake-store-access).

4. Na powitania **dostępu do usługi Data Lake Store**, kliknij przycisk **wybierz**, a następnie kontynuuj tworzenia klastra, zgodnie z opisem w [klastrów utworzyć Hadoop w HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a>Tworzenie klastra z usługą Data Lake Store jako dodatkowego miejsca do magazynowania

Witaj poniższe instrukcje tworzenia klastra usługi HDInsight z konta usługi Azure Storage jako hello domyślny magazyn i konto usługi Data Lake Store jako dodatkowego magazynu.
**toocreate HDInsight klaster z usługi Data Lake Store jako hello domyślne konto magazynu**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Postępuj zgodnie z [Tworzenie klastrów](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) hello ogólne informacje na temat tworzenia klastrów usługi HDInsight.
3. Na powitania **magazynu** bloku, w obszarze **typu podstawowego magazynu**, wybierz pozycję **usługi Azure Storage**, a następnie wprowadź hello następujących informacji:

    ![Dodaj usługi głównej tooHDInsight klastra](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "Dodaj usługi głównej tooHDInsight klastra")

    - **Wybór metody**: użyj jednej z hello następujące opcje:

        * toospecify konta magazynu, będącej częścią subskrypcji platformy Azure, wybierz **Moje subskrypcje**, a następnie wybierz konto magazynu hello.
        * toospecify konta magazynu znajdującego się poza subskrypcją platformy Azure, wybierz opcję **klucz dostępu**, a następnie udostępnienie informacji hello hello poza konta magazynu.

    - **Domyślny kontener**: Użyj wartości domyślnej albo hello, lub określ własną nazwę.

    - Dodatkowych kont magazynu: dodać więcej kont magazynu Azure jako hello dodatkowego magazynu.
    - Dostęp do usługi Data Lake Store: Konfigurowanie dostępu między hello konto usługi Data Lake Store i klaster usługi HDInsight. Instrukcje można znaleźć [dostępu Konfiguruj Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Konfigurowanie dostępu do usługi Data Lake Store 

W tej sekcji skonfigurujesz dostęp do usługi Data Lake Store z klastrów usługi HDInsight przy użyciu nazwy głównej usługi Azure Active Directory. 

### <a name="specify-a-service-principal"></a>Określ nazwy głównej usługi

Z hello portalu Azure możesz użyć istniejącej nazwy głównej usługi lub Utwórz nową.

**toocreate nazwy głównej usługi z hello portalu Azure**

1. Kliknij przycisk **dostępu do usługi Data Lake Store** z hello magazynu bloku.
2. Na powitania **dostępu do usługi Data Lake Store** bloku, kliknij przycisk **Utwórz nowy**.
3. Kliknij przycisk **nazwy głównej usługi**, a następnie wykonaj hello instrukcje toocreate nazwy głównej usługi.
4. Pobierz certyfikat hello, jeśli użytkownik zdecyduje toouse go ponownie w przyszłości hello. Pobieranie certyfikatu hello jest przydatne, jeśli ma toouse hello sama usługa podmiotu zabezpieczeń podczas tworzenia dodatkowych klastrów usługi HDInsight.

    ![Dodaj usługi głównej tooHDInsight klastra](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "Dodaj usługi głównej tooHDInsight klastra")

4. Kliknij przycisk **dostępu** dostęp do folderu hello tooconfigure.  Zobacz [skonfigurować uprawnienia do pliku](#configure-file-permissions).


**toouse istniejącą usługę podmiotu zabezpieczeń z hello portalu Azure**

1. Kliknij przycisk **dostępu do usługi Data Lake Store**.
1. Na powitania **dostępu do usługi Data Lake Store** bloku, kliknij przycisk **Użyj istniejącego**.
2. Kliknij przycisk **nazwy głównej usługi**, a następnie wybierz nazwę główną usługi. 
3. Przekaż hello certyfikatu (pfx) skojarzoną z Twojej nazwy głównej usługi wybrany, a następnie wprowadź hasło certyfikatu hello.

    ![Dodaj usługi głównej tooHDInsight klastra](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "Dodaj usługi głównej tooHDInsight klastra")

4. Kliknij przycisk **dostępu** dostęp do folderu hello tooconfigure.  Zobacz [skonfigurować uprawnienia do pliku](#configure-file-permissions).


### <a name="configure-file-permissions"></a>Skonfiguruj uprawnienia do pliku

Konfiguruje Hello są różne w zależności od tego, czy konto hello jest używany jako hello domyślnego magazynu lub konta dodatkowego miejsca do magazynowania:

- Używane jako domyślnego magazynu

    - uprawnienia na poziomie głównym hello hello konta usługi Data Lake Store
    - uprawnienia na poziomie głównym hello hello magazynu klastra usługi HDInsight. Na przykład Witaj __/klastrów__ folderu używanego wcześniej w samouczku hello.
- Użyj jako dodatkowego magazynu

    - Uprawnienie hello folderów, której należy plik dostępu.

**uprawnienia tooassign na powitania poziomu głównego konta usługi Data Lake Store**

1. Na powitania **dostępu do usługi Data Lake Store** bloku, kliknij przycisk **dostępu**. Witaj **wybierz uprawnienia do pliku** bloku jest otwarty. Wyświetla listę wszystkich kont usługi Data Lake Store hello w ramach subskrypcji.
2. Umieść kursor (nie klikaj) hello myszą hello nazwę hello toomake hello widoczne, pole wyboru, a następnie wybierz hello pole wyboru konta usługi Data Lake Store.

    ![Dodaj usługi głównej tooHDInsight klastra](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "Dodaj usługi głównej tooHDInsight klastra")

  Domyślnie __odczytu__, __zapisu__, AND __EXECUTE__ wybrane są.

3. Kliknij przycisk **wybierz** na powitania u dołu strony hello.
4. Kliknij przycisk **Uruchom** tooassign uprawnienia.
5. Kliknij przycisk **Gotowe**.

**uprawnienia tooassign na powitania poziomu głównego klastra usługi HDInsight**

1. Na powitania **dostępu do usługi Data Lake Store** bloku, kliknij przycisk **dostępu**. Witaj **wybierz uprawnienia do pliku** bloku jest otwarty. Wyświetla listę wszystkich kont usługi Data Lake Store hello w ramach subskrypcji.
1. Z hello **wybierz uprawnienia do pliku** bloku, kliknij przycisk tooshow nazwy usługi Data Lake Store hello jego zawartości.
2. Wybierz główny magazynu klastra usługi HDInsight hello wybierając hello wyboru po lewej stronie powitania hello folderu. Zgodnie z zrzut ekranu toohello wcześniej, jest katalogu głównego magazynu klastra hello __/klastrów__ folder określony podczas zaznaczania hello Data Lake Store jako domyślnego magazynu.
3. Ustaw uprawnienia hello hello folderu.  Domyślnie do odczytu, zapisu i wykonywania wybrane są.
4. Kliknij przycisk **wybierz** na powitania u dołu strony hello.
5. Kliknij pozycję **Run** (Uruchom).
6. Kliknij przycisk **Gotowe**.

Jeśli korzystasz z usługi Data Lake Store jako dodatkowego magazynu, należy przypisać uprawnienia tylko do folderów hello, które mają tooaccess z klastrem usługi HDInsight hello. Na przykład w poniższym zrzucie ekranu hello, można zapewnić dostęp tylko za**hdiaddonstorage** folderu w ramach konta usługi Data Lake Store.

![Przypisz klastra usługi HDInsight toohello podmiotu zabezpieczeń uprawnienia usługi](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "klastra usługi HDInsight toohello Przypisz usługę podmiotu zabezpieczeń uprawnienia")


## <a name="verify-cluster-set-up"></a>Sprawdź ustawienia klastra

Po zakończeniu instalacji klastra hello, w bloku klastra hello, sprawdź wyniki, wykonując jedną lub obie hello następujące kroki:

* tooverify hello skojarzone magazynu dla klastra hello jest konta usługi Data Lake Store hello określonego, kliknij przycisk **kont magazynu** w okienku po lewej stronie powitania.

    ![Dodaj usługi głównej tooHDInsight klastra](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "Dodaj usługi głównej tooHDInsight klastra")

* tooverify, który hello nazwy głównej usługi jest on prawidłowo skojarzony z klastrem usługi HDInsight hello, kliknij przycisk **dostępu do usługi Data Lake Store** w okienku po lewej stronie powitania.

    ![Dodaj usługi głównej tooHDInsight klastra](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "Dodaj usługi głównej tooHDInsight klastra")


## <a name="examples"></a>Przykłady

Po skonfigurowaniu klastra hello z usługą Data Lake Store jako magazynu można znaleźć przykłady toothese jak toouse HDInsight cluster tooanalyze hello danych przechowywanych w usłudze Data Lake Store.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a>Uruchomienie zapytania programu Hive względem danych w usłudze Data Lake Store (jako podstawowy magazyn)

toorun zapytań programu Hive za pomocą interfejsu widoki Hive hello w portalu Ambari hello. Aby uzyskać instrukcje dotyczące sposobu widoków toouse Hive narzędzia Ambari, zobacz [hello użyj widoku Hive z usługą Hadoop w usłudze HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).

Podczas pracy z danymi w usłudze Data Lake Store, istnieje kilka toochange ciągów.

Jeśli używasz, na przykład klaster hello, utworzony za pomocą usługi Data Lake Store jako podstawowy magazyn danych toohello ścieżki hello jest: *adl: / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*. Toocreate zapytanie Hive tabeli z przykładowych danych, które są przechowywane w hello konta usługi Data Lake Store wygląda hello następującej instrukcji:

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

Opisy:
* `adl://hdiadlstorage.azuredatalakestore.net/`jest głównym hello hello konta usługi Data Lake Store.
* `/clusters/myhdiadlcluster`jest głównym hello hello klastra dane, które można określić podczas tworzenia klastra hello.
* `/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`jest lokalizacja hello hello przykładowy plik, który został użyty w zapytaniu hello.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a>Uruchamianie zapytań programu Hive względem danych w usłudze Data Lake Store (jako dodatkowego magazynu)

Jeśli utworzony klaster hello używa magazynu obiektów Blob jako domyślny magazyn, hello przykładowych danych nie jest zawarta w hello konta Azure Data Lake Store, który jest używany jako dodatkowy magazyn. W takim przypadku najpierw przenieść dane hello z toohello magazynu obiektów Blob usługi Data Lake Store, a następnie uruchom zapytania hello, jak pokazano w hello poprzedzających przykład.

Aby uzyskać informacji na temat sposobu toocopy z magazynu obiektów Blob tooa Data Lake magazynu danych Zobacz hello następujące artykuły:

* [Użyj narzędzia Distcp toocopy danych między obiektów blob magazynu Azure i usługi Data Lake Store](data-lake-store-copy-data-wasb-distcp.md)
* [Użyj AdlCopy toocopy danych z usługi Azure Storage obiektów blob tooData Lake — Magazyn](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a>Użyj Data Lake Store z klastra Spark
Możesz użyć zadań Spark toorun klastra Spark w danych przechowywanych w usłudze Data Lake Store. Aby uzyskać więcej informacji, zobacz [dane tooanalyze klastra HDInsight korzystanie z platformy Spark w usłudze Data Lake Store](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).


### <a name="use-data-lake-store-in-a-storm-topology"></a>Użyj Data Lake Store w topologii Storm
Można użyć danych toowrite usługi Data Lake Store powitania od topologii Storm. Aby uzyskać instrukcje dotyczące tooachieve tego scenariusza, zobacz [użycia usługi Azure Data Lake Store z systemu Apache Storm z usługą HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).

## <a name="see-also"></a>Zobacz też
* [Środowiska PowerShell: HDInsight toouse klastra usługi Data Lake Store utworzyć](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
