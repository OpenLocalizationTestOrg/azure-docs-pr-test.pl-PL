---
title: "wprowadzenie do usługi Azure Data Lake Store tooget interfejsu aaaUse 2.0 wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj wiersza polecenia platformy Azure i platform 2.0 toocreate konto usługi Data Lake Store i wykonywać podstawowe operacje"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a>Rozpoczynanie pracy z usługą Azure Data Lake Store za pomocą interfejsu wiersza polecenia platformy Azure 2.0
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Zestaw SDK platformy .NET](data-lake-store-get-started-net-sdk.md)
> * [Zestaw SDK Java](data-lake-store-get-started-java-sdk.md)
> * [Interfejs API REST](data-lake-store-get-started-rest-api.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Dowiedz się, jak toocreate toouse Azure CLI 2.0 Azure Data Lake przechowywać konto i wykonywać podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych, usuwanie konta itp. Aby uzyskać więcej informacji o usłudze Data Lake Store, zobacz [Omówienie usługi Data Lake Store](data-lake-store-overview.md).

Hello Azure CLI 2.0 jest nowe środowisko wiersza polecenia platformy Azure do zarządzania zasobami platformy Azure. Można go używać w systemach macOS, Linux i Windows. Aby uzyskać więcej informacji, zobacz [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview) (Przegląd interfejsu wiersza polecenia platformy Azure 2.0). Można również sprawdzić hello [odwołanie do usługi Azure Data Lake magazynu interfejsu wiersza polecenia 2.0](https://docs.microsoft.com/cli/azure/dls) pełną listę poleceń i składni.


## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego artykułu, musi mieć następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Interfejs wiersza polecenia platformy Azure 2.0** — instrukcje znajdują się w artykule [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Instalowanie interfejsu wiersza polecenia platformy Azure w wersji 2.0).

## <a name="authentication"></a>Authentication

W tym artykule użyto prostszej metody uwierzytelniania w usłudze Data Lake Store, w przypadku której logujesz się jako użytkownik końcowy. następnie podlega Hello dostępu poziomu tooData Lake Store konta i system plików poziom dostępu hello hello zalogowanego użytkownika. Istnieją inne podejścia jako dobrze tooauthenticate z usługi Data Lake Store, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**. Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniania użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [do usługi uwierzytelniania](data-lake-store-authenticate-using-active-directory.md).


## <a name="log-in-tooyour-azure-subscription"></a>Zaloguj się za tooyour subskrypcji platformy Azure

1. Zaloguj się do subskrypcji platformy Azure.

    ```azurecli
    az login
    ```

    Otrzymasz toouse kodu w hello następnego kroku. Użyj https://aka.ms/devicelogin strony sieci web przeglądarce tooopen hello, a następnie wprowadź hello tooauthenticate kodu. Jesteś zostanie wyświetlony monit o toolog przy użyciu poświadczeń użytkownika.

2. Po zalogowaniu hello okno wyświetla wszystkie hello subskrypcji platformy Azure, które są skojarzone z Twoim kontem. Użyj hello następujące polecenia toouse określonej subskrypcji.
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a>Tworzenie konta usługi Azure Data Lake Store

1. Utwórz nową grupę zasobów. W hello następujące polecenia podaj hello ma toouse wartości parametrów. Jeśli nazwa lokalizacji hello zawiera spacje, umieść ją w cudzysłowie. Na przykład „Wschodnie stany USA 2”. 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. Tworzenie konta usługi Data Lake Store hello.
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a>Tworzenie folderów w ramach konta usługi Data Lake Store

Można tworzyć foldery w toomanage konta użytkownika usługi Azure Data Lake Store i przechowywania danych. Witaj Użyj następującego polecenia toocreate folder o nazwie **mojnowyfolder** w głównym hello hello usługi Data Lake Store.

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> Witaj `--folder` parametru zapewnia, że polecenie hello tworzy folder. Jeśli ten parametr nie jest obecny, hello polecenie tworzy pusty plik o nazwie mojnowyfolder w katalogu głównym hello hello konta usługi Data Lake Store.
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a>Przekaż konto usługi Data Lake Store tooa danych

Możesz przekazać dane tooData Lake Store bezpośrednio hello tooa lub na poziomie folderu głównego utworzonego w ramach konta hello. Witaj poniższe fragmenty kodu przedstawiają sposób tooupload folderu toohello niektóre przykładowe dane (**mojnowyfolder**) został utworzony w poprzedniej sekcji hello.

Jeśli szukasz niektórych tooupload dane przykładowe, możesz pobrać hello **Ambulance Data** folderu z hello [repozytorium Git programu Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Pobierz plik hello i zapisz go w katalogu lokalnym na komputerze, na przykład C:\sampledata\.

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> Dla lokalizacji docelowej hello należy określić pełną ścieżkę hello, łącznie z nazwą pliku hello.
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a>Wyświetlanie listy plików w ramach konta usługi Data Lake Store

Użyj hello następujące polecenia toolist hello pliki w ramach konta usługi Data Lake Store.

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

Hello dane wyjściowe powinny być podobne toohello następujące czynności:

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a>Zmienianie nazwy, pobieranie i usuwanie danych z konta usługi Data Lake Store 

* **toorename pliku**, użyj następującego polecenia hello:
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* **toodownload pliku**, użyj następującego polecenia hello. Upewnij się, że ścieżka docelowa hello już istnieje.
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > polecenie Hello tworzy folder docelowy hello, jeśli nie istnieje.
    > 
    >

* **toodelete pliku**, użyj następującego polecenia hello:
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    Jeśli chcesz, aby toodelete hello folder **mojnowyfolder** i plik hello **vehicle1_09142014_copy.csv** razem w jedno polecenie, użyj hello--recurse parametru

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a>Praca z uprawnieniami i listami kontroli dostępu dla konta usługi Data Lake Store

W tej sekcji opisano sposób toomanage listy kontroli dostępu i uprawnień przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure. Szczegółowe omówienie sposobu implementacji list ACL w usłudze Azure Data Lake Store znajduje się w artykule [Kontrola dostępu w usłudze Azure Data Lake Store](data-lake-store-access-control.md).

* **Właściciel hello tooupdate plik lub folder**, użyj następującego polecenia hello:

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* **tooupdate hello uprawnienia do pliku/folderu**, użyj następującego polecenia hello:

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* **Witaj tooget listy ACL dla danej ścieżki**, użyj następującego polecenia hello:

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    Hello dane wyjściowe powinny być podobne toohello następujące czynności:

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* **tooset wpis dla listy ACL**, użyj następującego polecenia hello:

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* **tooremove wpis dla listy ACL**, użyj następującego polecenia hello:

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* **tooremove cały domyślnej listy ACL**, użyj następującego polecenia hello:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* **tooremove cały ACL innych niż domyślne**, użyj następującego polecenia hello:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a>Usuwanie konta usługi Data Lake Store
Użyj następującego polecenia toodelete konto usługi Data Lake Store hello.

```azurecli
az dls account delete --account mydatalakestore
```

Po wyświetleniu monitu wprowadź **Y** toodelete hello konta.

## <a name="next-steps"></a>Następne kroki

* [Informacje o interfejsie wiersza polecenia usługi Azure Data Lake Store 2.0](https://docs.microsoft.com/cli/azure/dls)
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)
* [Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Korzystanie z usługi Azure HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
