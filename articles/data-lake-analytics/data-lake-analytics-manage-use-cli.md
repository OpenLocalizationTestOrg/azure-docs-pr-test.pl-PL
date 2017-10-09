---
title: "aaaManage Azure Data Lake Analytics przy użyciu interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zadania konta usługi Data Lake Analytics toomanage, źródła danych i użytkowników przy użyciu wiersza polecenia platformy Azure"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a>Zarządzanie Azure Data Lake Analytics przy użyciu interfejsu wiersza polecenia platformy Azure (CLI)
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Dowiedz się, jak toomanage kont usługi Azure Data Lake Analytics, źródeł danych użytkowników i zadań za pomocą hello wiersza polecenia platformy Azure. Tematy dotyczące zarządzania toosee przy użyciu innych narzędzi, kliknij przycisk Wybierz kartę hello powyżej.


**Wymagania wstępne**

Przed rozpoczęciem tego samouczka wymagane są następujące hello:

* **Subskrypcja platformy Azure**. Zobacz artykuł [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Interfejs wiersza polecenia platformy Azure**. Zobacz temat [Instalowanie i konfigurowanie interfejsu wiersza polecenia platformy Azure](../cli-install-nodejs.md).
  * Pobierz i zainstaluj hello **wstępną** [narzędzia wiersza polecenia platformy Azure](https://github.com/MicrosoftBigData/AzureDataLake/releases) w celu toocomplete tego pokazu.
* **Uwierzytelnianie**za pomocą hello następujące polecenie:
  
        azure login
    Aby uzyskać więcej informacji na temat uwierzytelniania przy użyciu konta służbowego, zobacz [połączyć tooan subskrypcji platformy Azure z hello Azure CLI](../xplat-cli-connect.md).
* **Przełącz tryb usługi Azure Resource Manager toohello**za pomocą hello następujące polecenie:
  
        azure config mode arm

**polecenia usługi Data Lake Store i usługi Data Lake Analytics toolist hello:**

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a>Zarządzanie kontami
Przed uruchomieniem zadania usługi Data Lake Analytics, musisz mieć konto usługi Data Lake Analytics. W przeciwieństwie do usługi Azure HDInsight nie płatności dla konta usługi Analytics zadania nie jest uruchomiona.  Płacisz tylko za czas hello, gdy jest uruchomione zadanie.  Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).  

### <a name="create-accounts"></a>Tworzenie kont
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a>Aktualizowanie kont
Witaj następujące polecenie aktualizuje hello właściwości istniejącego konta Data Lake Analytics

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a>Wyświetlanie listy kont
Lista Data Lake Analytics kont 

    azure datalake analytics account list

Lista Data Lake Analytics kont w ramach określonej grupy zasobów

    azure datalake analytics account list -g "<Azure Resource Group Name>"

Uzyskiwanie szczegółowych informacji z określonego konta usługi Data Lake Analytics

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a>Usuwanie konta usługi Data Lake Analytics
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a>Zarządzaj źródłami danych konta
Data Lake Analytics obsługuje obecnie hello następujące źródła danych:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage](../storage/common/storage-introduction.md)

Podczas tworzenia konta usługi Analytics należy wyznaczyć usługi Azure Data Lake Storage konta toobe hello domyślne konto magazynu. Witaj domyślne konto magazynu ADL służy toostore zadania metadanych i zadania dziennika inspekcji. Po utworzeniu konta usługi Analytics można dodać dodatkowe konta usługi Data Lake Storage i/lub konta usługi Magazyn Azure. 

### <a name="find-hello-default-adl-storage-account"></a>Znajdź hello domyślne konto magazynu ADL
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

wartość Hello jest na liście właściwości: datalakeStoreAccount:name.

### <a name="add-additional-azure-blob-storage-accounts"></a>Dodawanie dodatkowych kont magazynu obiektów Blob platformy Azure
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> Są obsługiwane tylko obiektu Blob magazynu krótkiej nazwy.  Nie używaj nazwy FQDN, na przykład "myblob.blob.core.windows.net".
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a>Dodawanie dodatkowych kont usługi Data Lake Store
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

[-d] jest opcjonalnym przełącznikiem tooindicate czy hello Data Lake dodawane jest konto usługi Data Lake domyślne hello. 

### <a name="update-existing-data-source"></a>Aktualizowanie istniejącego źródła danych
tooset istniejącej domyślnej hello toobe konta usługi Data Lake Store:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

tooupdate istniejącego klucza konta magazynu obiektów Blob:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a>Lista źródeł danych:
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Data Lake Analytics listy źródła danych](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a>Usuń źródła danych:
Konto usługi Data Lake Store toodelete:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

toodelete konta magazynu obiektów Blob:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a>Zarządzanie zadaniami
Aby można było utworzyć zadanie, musisz mieć konto usługi Data Lake Analytics.  Aby uzyskać więcej informacji, zobacz [kont zarządzania usługi Data Lake Analytics](#manage-accounts).

### <a name="list-jobs"></a>Lista zadań
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Data Lake Analytics listy źródła danych](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a>Uzyskiwanie szczegółów zadania
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a>Przesyłanie zadań
> [!NOTE]
> Hello domyślny priorytet zadania wynosi 1000, a hello domyślne stopień równoległości zadania jest 1.
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a>Anulowanie zadań
Użyj identyfikator zadania hello toofind hello listy poleceń, a następnie użyj anulowania toocancel hello zadania.

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a>Zarządzanie katalogiem
wykaz Hello U-SQL jest toostructure używanych danych i kod, aby mogły być udostępniane przez skrypty U-SQL. wykaz Hello umożliwia hello najwyższym możliwym poziomie wydajności z danymi w usłudze Azure Data Lake. Więcej informacji znajduje się w temacie [Używanie katalogu U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-catalog-items"></a>Lista elementów katalogu
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

typy Hello zawierają bazy danych, schematów, zestawu, zewnętrzne źródło danych, tabeli, funkcji zwracającej tabelę lub statystyk tabeli.

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a>Użyj grup ARM
Aplikacje składają się zazwyczaj z wielu składników, na przykład aplikacji sieci Web, bazy danych, serwera bazy danych, magazynu i usług firm zewnętrznych. Usługa Azure Resource Manager (ARM) umożliwia toowork z zasobami hello w aplikacji jako grupę, określonym tooas grupy zasobów platformy Azure. Można wdrożyć, zaktualizować, monitorować lub usunąć wszystkie zasoby hello aplikacji w jednej, skoordynowanej operacji. Wdrażanie wykonuje się przy użyciu szablonu, którego można następnie używać w różnych środowiskach (testowanie, etap przejściowy i produkcja). Można również uprościć rozliczenia w organizacji, wyświetlając hello zestawienia kosztów całej grupy hello. Aby uzyskać więcej informacji, zobacz temat [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). 

Usługa Data Lake Analytics może zawierać hello następujące składniki:

* Usługa Azure Data Lake Analytics konta
* Wymagane domyślne konto usługi Azure Data Lake Storage
* Dodatkowe usługi Azure Data Lake kont magazynu
* Dodatkowe konta usługi Azure Storage

Wszystkie te składniki w jednym toomake grupy ARM można tworzyć ich toomanage łatwiejsze.

![Usługa Azure Data Lake Analytics konta i magazynu](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

Konto usługi Data Lake Analytics i kont magazynu zależnego hello muszą być umieszczone w hello sam centrum danych Azure.
jednak Hello ARM grupy może znajdować się w centrum danych.  

## <a name="see-also"></a>Zobacz też
* [Omówienie usługi Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu portalu Azure](data-lake-analytics-get-started-portal.md)
* [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md)
* [Monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów przy użyciu witryny Azure Portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

