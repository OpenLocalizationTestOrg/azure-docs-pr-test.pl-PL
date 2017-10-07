---
title: "aaaUse toocreate szablony usługi Azure HDInsight i usługi Data Lake Store | Dokumentacja firmy Microsoft"
description: "Użyj toocreate szablonów usługi Azure Resource Manager i klastry usługi HDInsight za pomocą usługi Azure Data Lake Store"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a>Tworzenie klastra usługi HDInsight z Data Lake Store za pomocą szablonu usługi Azure Resource Manager
> [!div class="op_single_selector"]
> * [Korzystanie z portalu](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Przy użyciu programu PowerShell (do magazynu domyślnego)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Przy użyciu programu PowerShell (dla dodatkowego magazynu)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Za pomocą Menedżera zasobów](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Dowiedz się, jak klaster toouse tooconfigure programu PowerShell usługi Azure HDInsight z usługi Azure Data Lake Store, **jako dodatkowego magazynu**.

Dla typów obsługiwanych klastra usługi Data Lake Store można użyć jako domyślnego magazynu lub konto dodatkowego miejsca do magazynowania. W przypadku usługi Data Lake Store jako dodatkowego magazynu hello domyślne konto magazynu dla klastrów hello będzie nadal Azure blob Storage (WASB) i hello plików związanych z klastrem (takich jak dzienniki, itp.) są zapisywane nadal toohello domyślny magazyn, podczas danych hello które Chcę tooprocess mogą być przechowywane w ramach konta usługi Data Lake Store. Za pomocą usługi Data Lake Store jako dodatkowego magazynu konta nie wpływa na wydajność lub pamięć masową toohello tooread/zapisu możliwości hello z hello klastra.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>W magazynie klastra usługi HDInsight przy użyciu usługi Data Lake Store

Poniżej przedstawiono kilka istotnych kwestii dotyczących z usługą Data Lake Store za pomocą usługi HDInsight:

* Klastry HDInsight toocreate opcji z dostępem do tooData Lake Store jako domyślny magazyn jest dostępny dla usługi HDInsight w wersji 3.5 i 3,6.

* Klastry HDInsight toocreate opcji z dostępem do tooData Lake Store jako dodatkowego magazynu jest dostępna dla usługi HDInsight w wersji 3.2, 3.4, 3.5 i 3,6.

W tym artykule możemy zainicjować klastra usługi Hadoop z usługą Data Lake Store jako dodatkowego magazynu. Aby uzyskać instrukcje dotyczące sposobu toocreate usługi Hadoop klaster z usługi Data Lake Store jako domyślnego magazynu, zobacz [tworzenia klastra usługi HDInsight z Data Lake Store przy użyciu portalu Azure](data-lake-store-hdinsight-hadoop-use-portal.md).

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka wymagane są następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Program Azure PowerShell 1.0 lub nowszy**. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
* **Nazwy głównej usługi Azure Active Directory usługi**. Kroki opisane w tym samouczku zawierają instrukcje na temat toocreate nazwy głównej usługi w usłudze Azure AD. Jednak należy usługi Azure AD administratora toobe stanie toocreate nazwy głównej usługi. Jeśli jesteś administratorem usługi Azure AD, możesz pominąć te wymagania wstępne i kontynuować hello samouczka.

    **Jeśli nie jesteś administratorem usługi Azure AD**, nie będą mogli tooperform hello kroki wymagane toocreate nazwy głównej usługi. W takim przypadku administrator usługi Azure AD należy najpierw utworzyć nazwy głównej usługi przed utworzeniem klastra usługi HDInsight z usługą Data Lake Store. Także hello nazwy głównej usługi muszą zostać utworzone za pomocą certyfikatu, zgodnie z opisem w [Tworzenie nazwy głównej usługi o certyfikat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a>Tworzenie klastra usługi HDInsight z usługi Azure Data Lake Store
Hello szablonu usługi Resource Manager i wymagania wstępne hello przy użyciu szablonu hello są dostępne w witrynie GitHub pod [wdrażanie klastra usługi HDInsight Linux z nowej usługi Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage). Wykonaj instrukcje hello podanych w tym toocreate łącze klastra usługi HDInsight z usługi Azure Data Lake Store jako dodatkowego magazynu hello.

instrukcje Hello w wymienionych powyżej łącze hello wymagają programu PowerShell. Przed rozpoczęciem pracy z tych instrukcji upewnij się, że możesz zalogować się w tooyour konto platformy Azure. Na pulpicie otwórz nowe okno programu Azure PowerShell, a następnie wprowadź powitania po fragmentów. Gdy zostanie wyświetlony monit o toolog, upewnij się, że logujesz się jako jeden hello/właścicieli subskrypcji:

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a>Przekaż przykładowe dane toohello Azure Data Lake Store
Szablon usługi Resource Manager Hello tworzy nowe konto usługi Data Lake Store i kojarzy ją z klastrem usługi HDInsight hello. Teraz musi przekazać niektóre przykładowe dane toohello usługi Data Lake Store. Będziesz potrzebować te dane później w zadaniach samouczek toorun hello z klastra usługi HDInsight, które uzyskują dostęp do danych w hello usługi Data Lake Store. Aby uzyskać instrukcje dotyczące tooupload danych, zobacz [przekazać plik tooyour usługi Data Lake Store](data-lake-store-get-started-portal.md#uploaddata). Jeśli szukasz niektórych tooupload dane przykładowe, możesz pobrać hello **Ambulance Data** folderu z hello [repozytorium Git programu Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).

## <a name="set-relevant-acls-on-hello-sample-data"></a>Ustawić odpowiednich list ACL na powitania przykładowe dane
toomake się, że jest dostępny z klastra usługi HDInsight hello hello przykładowe dane, które zostaną przesłane, należy się upewnić, że aplikacji hello Azure AD, która jest używana tooestablish tożsamości między klastrem usługi HDInsight hello i usługi Data Lake Store ma dostęp toohello plik lub folder, który ma w trakcie tooaccess. toodo, wykonaj następujące kroki hello.

1. Znajdź nazwę hello hello aplikacji usługi Azure AD, który jest skojarzony z klastrem usługi HDInsight i hello usługi Data Lake Store. Tooopen hello HDInsight bloku klastra utworzonej przy użyciu szablonu usługi Resource Manager hello jest jednym ze sposobów toolook hello nazwy, kliknij przycisk hello **tożsamość usługi AAD klastra** , a następnie wyszukaj wartość hello **nazwy głównej usługi Nazwa wyświetlana**.
2. Teraz podaj toothis dostępu do aplikacji usługi Azure AD na powitania plik lub folder, które mają tooaccess z klastrem usługi HDInsight hello. list ACL praw hello tooset na powitania plik lub folder, w usłudze Data Lake Store, zobacz [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md#filepermissions).

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Uruchom zadania testowe na powitania HDInsight klastra toouse hello usługi Data Lake Store
Po skonfigurowaniu klastra usługi HDInsight można uruchamiać zadania testowego na powitania klastra tootest tego hello HDInsight klastra mogą uzyskiwać dostęp do usługi Data Lake Store. toodo tak, zostanie uruchomiony przykładowe zadania Hive, która tworzy tabelę przy użyciu hello przykładowych danych, aby przekazać wcześniejszych tooyour Data Lake Store.

W tej sekcji będzie SSH do klastra usługi HDInsight w systemie Linux i uruchamiania hello przykładowe zapytanie Hive. Jeśli używasz klienta z systemem Windows, firma Microsoft zaleca używanie **PuTTY**, który można pobrać z [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Aby uzyskać więcej informacji na temat używania programu PuTTY, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

1. Po nawiązaniu połączenia, należy uruchomić hello Hive interfejsu wiersza polecenia przy użyciu hello następujące polecenie:

   ```
   hive
   ```
2. Używając hello interfejsu wiersza polecenia, wprowadź następujące instrukcje toocreate nowej tabeli o nazwie hello **pojazdów** przy użyciu hello przykładowe dane w hello usługi Data Lake Store:

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   Powinny być widoczne następujące dane wyjściowe podobne toohello:

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a>Dostęp Data Lake Store za pomocą poleceń systemu plików HDFS
Po skonfigurowaniu hello HDInsight klastra toouse Data Lake Store można użyć hello systemu plików HDFS powłoki poleceń tooaccess hello magazynu.

W tej sekcji będzie SSH do klastra usługi HDInsight w systemie Linux i hello wykonywania poleceń systemu plików HDFS. Jeśli używasz klienta z systemem Windows, firma Microsoft zaleca używanie **PuTTY**, który można pobrać z [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Aby uzyskać więcej informacji na temat używania programu PuTTY, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

Po nawiązaniu połączenia użyj hello następujące pliki poleceń systemu plików HDFS hello toolist w hello usługi Data Lake Store.

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

Powinny pojawić się plik hello czy przesłany wcześniejszych toohello Data Lake Store.

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

Można również użyć hello `hdfs dfs -put` polecenia tooupload toohello niektórych plików usługi Data Lake Store, a następnie użyj `hdfs dfs -ls` tooverify czy hello pliki zostały pomyślnie przekazane.


## <a name="next-steps"></a>Następne kroki
* [Kopiowanie danych z usługi Azure magazynu obiektów blob tooData Lake Store](data-lake-store-copy-data-wasb-distcp.md)
