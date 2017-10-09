---
title: "wprowadzenie do usługi Azure Data Lake Analytics przy użyciu usługi Azure CLI 2.0 aaaGet | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć zadanie usługi Data Lake Analytics przy użyciu języka U-SQL toouse hello 2.0 interfejsu wiersza polecenia Azure toocreate konto usługi Data Lake Analytics i przesłać zadanie hello. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a>Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu interfejsu wiersza polecenia platformy Azure 2.0
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

W ramach tego samouczka utworzysz zadanie, które odczytuje zawartość pliku z wartościami rozdzielanymi tabulatorami (TSV) i konwertuje je do pliku z wartościami rozdzielanymi przecinkami (CSV). toogo za pośrednictwem hello obsługiwane tego samouczka przy użyciu innych narzędzi, użyj listy rozwijanej hello na powitania górnej części tej sekcji.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka, musi mieć hello następujące elementy:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Interfejs wiersza polecenia platformy Azure 2.0**. Zobacz temat [Instalowanie i konfigurowanie interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

toolog w tooyour subskrypcji platformy Azure:

```
azurecli
az login
```

Są żądane toobrowse tooa URL, a następnie wprowadź kod uwierzytelniania.  A następnie wykonaj tooenter instrukcje hello swoje poświadczenia.

Po zalogowaniu, hello logowania polecenie wyświetla listę subskrypcji.

toouse określonej subskrypcji:

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a>Tworzenie konta usługi Data Lake Analytics
Aby można było uruchomić jakiekolwiek zadanie, musisz mieć konto usługi Data Lake Analytics. toocreate konto usługi Data Lake Analytics, należy określić hello następujące elementy:

* **Grupa zasobów platformy Azure**. W grupie zasobów platformy Azure należy utworzyć konto usługi Data Lake Analytics. [Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) pozwala toowork z zasobami hello w aplikacji jako grupa. Można wdrożyć, zaktualizować lub usunąć wszystkie zasoby hello aplikacji w jednej, skoordynowanej operacji.  

toolist hello istniejącej grupy zasobów w ramach Twojej subskrypcji:

```
az group list
```

toocreate nową grupę zasobów:

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* **Nazwa konta usługi Data Lake Analytics**. Każde konto usługi Data Lake Analytics ma nazwę.
* **Lokalizacja**. Użyj jednej z hello centrach danych platformy Azure, obsługiwanych przez usługę Data Lake Analytics.
* **Domyślne konto usługi Data Lake Store**: każde konto usługi Data Lake Analytics ma domyślne konto usługi Data Lake Store.

toolist hello istniejącego konta Data Lake Store:

```
az dls account list
```

toocreate nowe konto usługi Data Lake Store:

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

Użyj następującej składni toocreate konto usługi Data Lake Analytics hello:

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

Po utworzeniu konta można użyć hello następujące polecenia toolist hello kont i Pokaż szczegóły konta:

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a>Przekaż tooData data Lake — Magazyn
W ramach tego samouczka przetworzysz wybrane dzienniki wyszukiwania.  Dziennik wyszukiwania Hello mogą być przechowywane w usłudze Data Lake store lub magazynu obiektów Blob platformy Azure.

Hello Azure portal udostępnia interfejs użytkownika do kopiowania niektórych przykładowych danych plików toohello domyślnego konta Data Lake Store, obejmujące plik dziennika wyszukiwania. Zobacz [Przygotowanie danych źródłowych](data-lake-analytics-get-started-portal.md) konta Data Lake Store domyślne toohello tooupload hello danych.

pliki tooupload przy użyciu interfejsu wiersza polecenia 2.0, hello Użyj następującego polecenia:

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

Usługa Data Lake Analytics może także uzyskiwać dostęp do usługi Azure Blob Storage.  Do przekazywania danych tooAzure obiektu Blob magazynu, zobacz [hello używanie interfejsu wiersza polecenia Azure z usługą Azure Storage](../storage/common/storage-azure-cli.md).

## <a name="submit-data-lake-analytics-jobs"></a>Przesyłanie zadań usługi Data Lake Analytics
zadania usługi Data Lake Analytics Hello są zapisywane w hello języka U-SQL. toolearn więcej informacji o języku U-SQL, zobacz [wprowadzenie do języka U-SQL](data-lake-analytics-u-sql-get-started.md) i [eence języka U-SQL](http://go.microsoft.com/fwlink/?LinkId=691348).

**toocreate skrypt zadania usługi Data Lake Analytics**

Utwórz plik tekstowy z poniższy skrypt U-SQL, a następnie zapisz hello tekstu pliku tooyour w stacji roboczej:

```
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
```

Ten skrypt U-SQL odczytuje hello źródła danych pliku przy użyciu **Extractors.Tsv()**, a następnie tworzy plik csv przy użyciu **Outputters.Csv()**.

Nie należy modyfikować Witaj dwie ścieżki, chyba że skopiować plik źródłowy hello do innej lokalizacji.  Data Lake Analytics tworzy folder wyjściowy hello, jeśli nie istnieje.

Jest prostsze ścieżek względnych toouse dla plików przechowywanych na domyślnych kont usługi Data Lake Store. Można także użyć ścieżek bezwzględnych.  Na przykład:

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

Należy użyć ścieżek bezwzględnych tooaccess plików w połączonych kontach magazynu.  Składnia Hello plików przechowywanych w połączonego konta usługi Azure Storage jest następująca:

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> Kontenery obiektów blob platformy Azure zawierające publiczne obiekty blob nie są obsługiwane.      
> Kontenery obiektów blob platformy Azure zawierające publiczne kontenery nie są obsługiwane.      
>

**zadania toosubmit**

Użyj hello następującej składni toosubmit zadania.

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

Na przykład:

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

**zadania toolist i Pokaż szczegóły zadania**

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

**zadania toocancel**

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a>Pobieranie wyników zadania

Po zakończeniu zadania można użyć hello następujące pliki wyjściowe hello toolist polecenia i pobierania plików hello:

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

Na przykład:

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a>Potoki i cykle

**Uzyskaj informacje na temat potoków i cykli**

Użyj hello `az dla job pipeline` polecenia toosee hello potoku informacji wcześniej zgłoszonych zadania.

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

Użyj hello `az dla job recurrence` polecenia toosee hello cyklu informacje dla poprzednio przesłany zadań.

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a>Następne kroki

* toosee hello dokumencie referencyjnym Data Lake Analytics CLI 2.0, zobacz [usługi Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).
* toosee hello dokumencie referencyjnym Data Lake magazynu CLI 2.0, zobacz [usługi Data Lake Store](https://docs.microsoft.com/cli/azure/dls).
* toosee bardziej złożonego zapytania, zobacz [witryny sieci Web analizowanie dzienników przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
