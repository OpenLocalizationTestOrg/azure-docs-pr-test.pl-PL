---
title: "aaaGet pracy z przykładem bazy danych HBase w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Postępuj zgodnie z tym toostart przykład bazy danych Apache HBase przy użyciu platformy hadoop w usłudze HDInsight. Tworzenie tabel na podstawie hello powłoki HBase i wyszukiwać w nich przy użyciu aplikacji Hive."
keywords: "hbasecommand,przykład hbase"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a>Rozpoczynanie pracy z przykładem bazy danych Apache HBase w usłudze HDInsight

Dowiedz się, jak toocreate klaster HBase w usłudze HDInsight, tworzenia tabel HBase i wykonywać zapytania dotyczące tabel za pomocą aplikacji Hive. Aby uzyskać ogólne informacje o bazie danych HBase, zobacz [Omówienie bazy danych HBase w usłudze HDInsight][hdinsight-hbase-overview].

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem próby w tym przykładzie HBase, musi mieć hello następujące elementy:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Bezpieczna powłoka (SSH)](hdinsight-hadoop-linux-use-ssh-unix.md). 
* [Program curl](http://curl.haxx.se/download.html).

## <a name="create-hbase-cluster"></a>Tworzenie klastra HBase
Hello poniższej procedury używa toocreate szablonu usługi Azure Resource Manager wersji 3.4 HBase opartych na systemie Linux klaster i hello zależnych domyślne Azure konto magazynu. Parametry hello toounderstand używany w procedurze hello oraz innymi metodami tworzenia klastra, zobacz [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Kliknij przycisk hello następującego szablonu hello tooopen obrazu w hello portalu Azure. Szablon Hello znajduje się w publicznym kontenerze obiektów blob. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Z hello **wdrożenie niestandardowe** bloku, wprowadź hello następujące wartości:
   
   * **Subskrypcja**: Wybierz subskrypcji platformy Azure, która jest używana toocreate hello klastra.
   * **Grupa zasobów**: utwórz grupę usługi Azure Resource Management lub użyj istniejącej.
   * **Lokalizacja**: Określ lokalizację hello hello grupy zasobów. 
   * **ClusterName**: Wprowadź nazwę klastra HBase hello.
   * **Nazwa logowania i hasło klastra**: hello domyślna nazwa logowania jest **admin**.
   * **Nazwa użytkownika SSH i hasło**: hello domyślna nazwa użytkownika to **sshuser**.  Tę nazwę można zmienić.
     
     Inne parametry są opcjonalne.  
     
     Każdy klaster zależy od konta usługi Azure Storage. Po usunięciu klastra dane hello pozostają zachowane na koncie magazynu hello. klastra Hello domyślna nazwa konta magazynu jest nazwą klastra hello z dołączany "store". Jest zapisane na stałe w sekcji zmiennych szablonu hello.
3. Wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**, a następnie kliknij przycisk **zakupu**. Trwa około 20 minut toocreate klastra.

> [!NOTE]
> Po usunięciu klastra HBase można utworzyć inny klaster HBase przy użyciu hello tego samego domyślnego kontenera obiektów blob. nowy klaster Hello przejmuje hello tabele bazy danych HBase utworzone w oryginalnym klastrze hello. tooavoid niespójności, zaleca się wyłączyć hello tabel HBase, przed usunięciem hello klastra.
> 
> 

## <a name="create-tables-and-insert-data"></a>Tworzenie tabel i wstawianie danych
Można za pomocą protokołu SSH tooconnect tooHBase klastrów i następnie używać tabel HBase toocreate powłoki HBase, wstawiania danych i zapytania o dane. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Dla większości użytkowników dane są wyświetlane w formacie tabelarycznym hello:

![Dane tabelaryczne usługi HDInsight HBase][img-hbase-sample-data-tabular]

W bazie danych HBase (implementacją BigTable) hello tego samego danych wygląda jak:

![Dane BigTable usługi HDInsight HBase][img-hbase-sample-data-bigtable]


**Witaj toouse powłoki HBase**

1. Z SSH uruchom następujące polecenie HBase hello:
   
    ```bash
    hbase shell
    ```

2. Utwórz bazę danych HBase z dwiema rodzinami kolumn:

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. Wstaw dowolne dane:
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Powłoka HBase HDInsight Hadoop][img-hbase-shell]
4. Pobierz pojedynczy wiersz:
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    Zostanie wyświetlona hello takie same wyniki jak za pomocą polecenia scan hello, ponieważ istnieje tylko jeden wiersz.
   
    Aby uzyskać więcej informacji na temat schematu tabeli HBase hello, zobacz [tooHBase wprowadzenie projektu schematu][hbase-schema]. Więcej poleceń bazy danych HBase można znaleźć w [Podręczniku bazy danych Apache HBase][hbase-quick-start].
5. Zakończ hello powłoki
   
    ```hbaseshell
    exit
    ```

**toobulk ładowanie danych do tabeli hello kontaktów HBase**

Baza danych HBase obsługuje kilka metod ładowania danych do tabel.  Aby uzyskać więcej informacji, zobacz temat [Ładowanie zbiorcze](http://hbase.apache.org/book.html#arch.bulk.load).

Przykładowy plik danych znajduje się w publicznym kontenerze obiektów blob, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.  zawartość pliku danych hello Hello jest:

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

Można opcjonalnie utworzyć plik tekstowy i przekaż hello pliku tooyour magazynu własne konto. Witaj instrukcje, zobacz [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight][hdinsight-upload-data].

> [!NOTE]
> Ta procedura wykorzystuje tabela kontaktów HBase hello utworzony w poprzedniej procedurze hello.
> 

1. Z SSH uruchom następujące polecenie tootransform hello danych pliku tooStoreFiles i przechowywać w ścieżce względnej określonej przez parametr Dimporttsv.bulk.output hello.  Powłoka HBase, za pomocą tooexit polecenie zakończenia hello.

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. Uruchom następujące polecenie tooupload hello danych z tabeli HBase toohello /example/data/storeDataFileOutput hello:
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. Otwórz hello powłoki HBase i użyj hello skanowania polecenia toolist hello tabeli zawartości.

## <a name="use-hive-tooquery-hbase"></a>Użyj Hive tooquery HBase

Korzystając z programu Hive, można wykonywać zapytania dotyczące danych w tabelach HBase. W tej sekcji utworzysz tabeli programu Hive który mapuje toohello tabeli HBase i używa go tooquery hello danych w tabeli HBase.

1. Otwórz **PuTTY**i połącz toohello klastra.  Zobacz instrukcje hello w poprzedniej procedurze hello.
2. W sesji SSH hello Użyj następującego polecenia toostart Beeline hello:

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Aby uzyskać więcej informacji o usłudze Beeline, zobacz [Używanie technologii Hive z usługą Hadoop w usłudze HDInsight z usługą Beeline](hdinsight-hadoop-use-hive-beeline.md).
       
3. Uruchom tabeli programu Hive, który mapuje tabeli HBase toohello powitania po toocreate skrypt HiveQL. Upewnij się, że utworzono hello Przykładowa tabela odwołuje się do wcześniej w tym samouczku przy użyciu hello powłoki HBase przed uruchomieniem tej instrukcji.

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. Uruchom następujące HiveQL skryptu tooquery hello danych w tabeli HBase hello hello:

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a>Korzystanie z interfejsów API REST HBase przy użyciu programu Curl

Witaj interfejsu API REST jest zabezpieczony za pomocą [uwierzytelnianie podstawowe](http://en.wikipedia.org/wiki/Basic_access_authentication). Są zawsze tworzyć żądania przy użyciu HTTPS (HTTP Secure) toohelp upewnij się, że poświadczenia są bezpiecznie wysyłane toohello serwera.

2. Użyj hello następujące polecenie toolist hello istniejących tabel HBase:

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. Użyj hello następujące polecenia toocreate nową tabelę HBase z rodziny dwie kolumny:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    Witaj schemat jest podany w formacie JSon hello.
4. Użyj następującego polecenia tooinsert hello niektóre dane:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    Należy najpierw base64 hello wartości podanych w przełączniku -d hello kodowania. W przykładzie hello:
   
   * MTAwMA==: 1000
   * UGVyc29uYWw6TmFtZQ==: Personal:Name
   * Sm9obiBEb2xl: John Dole
     
     [FALSE wiersz klucza](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) pozwala tooinsert wiele wartości (wsadów).
5. Użyj hello następujące polecenia tooget wiersza:
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

Aby uzyskać więcej informacji o interfejsie Rest HBase, zobacz [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest) (Podręcznik referencyjny Apache HBase).

> [!NOTE]
> Platforma Thrift nie jest obsługiwana przez bazę danych HBase w usłudze HDInsight.
>
> Po za pomocą Curl lub innego połączenia REST z usługą WebHCat, zapewniając hello nazwę użytkownika i hasło administratora klastra usługi HDInsight hello musi uwierzytelnić się hello żądania. Należy również użyć nazwy klastra hello jako część hello identyfikator URI (Uniform Resource) używane toosend hello żądań toohello serwera:
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    Powinien zostać wyświetlony odpowiedzi toohello podobne, po odpowiedzi:
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a>Sprawdzanie stanu klastra
Baza danych HBase w usłudze HDInsight jest dostarczana z interfejsem użytkownika sieci Web służącym do monitorowania klastrów. Przy użyciu hello interfejsu użytkownika sieci Web, możesz poprosić statystyk lub informacji o regionach.

**Witaj tooaccess głównego HBase interfejsu użytkownika**

1. Zaloguj się na powitania hello Interfejsu sieci Web Ambari w https://&lt;Clustername >. azurehdinsight.net.
2. Kliknij przycisk **HBase** z menu po lewej stronie powitania.
3. Kliknij przycisk **szybkie linki** na hello górnej części strony hello, toohello punktu aktywnego dozorcy węzła łącza, a następnie kliknij przycisk **interfejsu użytkownika głównego HBase**.  Witaj interfejsu użytkownika jest otwarty w innej karty przeglądarki:

  ![Główny interfejs użytkownika HDInsight HBase](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  Witaj interfejsu użytkownika głównego HBase zawiera hello następujące sekcje:

  - serwery regionów
  - wzorce kopii zapasowej
  - tabele
  - zadania
  - atrybuty oprogramowania

## <a name="delete-hello-cluster"></a>Usuń klaster hello
tooavoid niespójności, zaleca się wyłączyć hello tabel HBase, przed usunięciem hello klastra.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Rozwiązywanie problemów

W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono sposób toocreate klaster HBase oraz jak toocreate tabele i widoki hello danych w tych tabelach z hello powłoki HBase. Przedstawiono również sposób toouse gałąź zapytania na danych w tabelach HBase oraz jak toouse hello toocreate C# interfejsów API REST HBase tabeli HBase i pobierania danych z tabeli hello.

toolearn więcej, zobacz:

* [Przegląd bazy danych HBase w usłudze HDInsight][hdinsight-hbase-overview]: HBase jest bazą danych Apache NoSQL typu open source opartą na platformie Hadoop, która zapewnia dostęp losowy i wysoki poziom spójności w przypadku dużych ilości danych z częściową strukturą i bez struktury.

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
