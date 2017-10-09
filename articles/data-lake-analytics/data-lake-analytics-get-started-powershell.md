---
title: "wprowadzenie do usługi Azure Data Lake Analytics przy użyciu programu Azure PowerShell aaaGet | Dokumentacja firmy Microsoft"
description: "Użyj programu Azure PowerShell toocreate konto usługi Data Lake Analytics, Utwórz zadanie usługi Data Lake Analytics przy użyciu języka U-SQL i przesłać zadanie hello. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a>Wprowadzenie do pracy z usługą Azure Data Lake Analytics przy użyciu programu Azure PowerShell
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Dowiedz się, jak toouse toocreate programu Azure PowerShell usługi Azure Data Lake Analytics kont, a następnie przesłać i uruchamianie zadań U-SQL. Więcej informacji na temat usługi Data Lake Analytics można znaleźć w artykule [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem tego samouczka, musi mieć hello następujących informacji:

* **Konto usługi Azure Data Lake Analytics**. Zobacz [Wprowadzenie do usługi Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).
* **Stacja robocza z programem Azure PowerShell**. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

W tym samouczku założono, że użytkownik wie już, jak korzystać z programu Azure PowerShell. W szczególności należy tooknow jak toolog w tooAzure. Zobacz hello [wprowadzenie do programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) Jeśli potrzebujesz pomocy.

toolog się przy użyciu nazwy subskrypcji:

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

Zamiast nazwy subskrypcji hello można także użyć toolog identyfikator subskrypcji w:

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

W przypadku powodzenia hello dane wyjściowe tego polecenia wygląda hello następującego tekstu:

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a>Przygotowywanie do samouczka hello

Witaj wstawki programu PowerShell w tym samouczku te informacje służą toostore następujące zmienne:

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a>Uzyskiwanie informacji o koncie usługi Data Lake Analytics

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a>Przesyłanie zadania U-SQL

Utwórz skrypt programu PowerShell zmiennej toohold hello U-SQL.

```
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();

"@
```

Przedstawia hello skryptu.

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

Alternatywnie można zapisać jako plik skryptu hello i przesłać o hello następujące polecenie:

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


Pobierz stan hello danego zadania. Nadal używać tego polecenia cmdlet, aż zobaczysz, że hello pracę.

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

Zamiast samodzielnego wywołanie Get-AdlAnalyticsJob zakończenie zadania, możesz użyć polecenia cmdlet AdlJob oczekiwania hello.

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

Pobierz plik wyjściowy hello.

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a>Zobacz też
* toosee hello sam samouczek przy użyciu innych narzędzi, kliknij przycisk hello selektor karty w górnej części hello hello strony.
* toolearn U-SQL, zobacz [wprowadzenie do języka Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).
* Informacje o zadaniach zarządzania znajdziesz w artykule [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md).
