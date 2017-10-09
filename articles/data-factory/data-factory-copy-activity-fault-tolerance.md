---
title: "aaaAdd odporność na uszkodzenia w przypadku działania kopiowania fabryki danych Azure przez pominięcie niezgodne wierszy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd odporność na uszkodzenia w przypadku działania kopiowania fabryki danych Azure przez pominięcie niezgodne wierszy podczas kopiowania"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>Dodaj odporność na uszkodzenia w przypadku działania kopiowania przez pominięcie niezgodne wierszy

Fabryka danych Azure [działanie kopiowania](data-factory-data-movement-activities.md) oferuje dwa sposoby toohandle niezgodne wierszy podczas kopiowania danych między źródłowy i odbiorczy magazynów danych:

- Możesz przerwać i niepowodzenie kopiowania hello działanie w przypadku niezgodnych danych napotkało (domyślnie).
- Można kontynuować toocopy wszystkich danych hello odporności na uszkodzenia i pomijanie niezgodne dane wierszy. Ponadto możesz zalogować się niezgodny wierszy hello magazynu obiektów Blob platformy Azure. Można następnie zbadać hello dziennika toolearn hello Przyczyna niepowodzenia hello, Usuń dane hello na powitania źródła danych i spróbuj ponownie hello działanie kopiowania.

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
Działanie kopiowania obsługuje trzy scenariusze wykrywanie, pomijanie i rejestrowanie danych niezgodne:

- **Niezgodność między hello źródłowego typu danych i typ macierzysty ujścia hello**

    Na przykład: kopiowanie danych z pliku CSV w tooa magazynu obiektów Blob SQL bazy danych z definicji schematu, która zawiera trzy **INT** kolumny o typie. Witaj wierszy pliku CSV, które zawierają dane liczbowe, takich jak `123,456,789` została pomyślnie skopiowana toohello ujścia magazynu. Jednak hello wiersze zawierające wartości nieliczbowe, takich jak `123,456,abc` zostały wykryte jako niezgodna ale są pomijane.

- **Niezgodność hello liczby kolumn między hello źródłowy i odbiorczy hello**

    Na przykład: kopiowanie danych z pliku CSV w tooa magazynu obiektów Blob SQL bazy danych z definicji schematu, który zawiera sześć kolumn. Witaj pliku CSV, który wierszy zawierających sześć kolumn została pomyślnie skopiowana toohello ujścia magazynu. wiersze pliku CSV Hello, które zawierają więcej lub mniej niż sześć kolumn są wykrywane niezgodne i są pomijane.

- **Naruszenia dotyczącego klucza podstawowego podczas zapisywania tooa relacyjnej bazy danych**

    Na przykład: kopiowanie danych z bazy danych programu SQL server tooa SQL. W bazie danych SQL zbiornika hello jest zdefiniowany klucz podstawowy, ale żaden klucz podstawowy jest zdefiniowany w hello źródła programu SQL server. Hello zduplikowane wiersze, które istnieją w źródle hello nie może być zbiornika toohello skopiowane. Działanie kopiowania kopiuje tylko hello pierwszy wiersz hello źródła danych do zbiornika hello. Witaj źródła kolejnych wierszy, które zawierają hello zduplikowane wartości klucza podstawowego są wykrywane niezgodne i są pomijane.

## <a name="configuration"></a>Konfiguracja
Witaj poniższym przykładzie przedstawiono tooconfigure definicji JSON, pomijanie hello niezgodne wierszy w przypadku działania kopiowania:

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| **enableSkipIncompatibleRow** | Włącz pomijanie niezgodne wierszy podczas kopiowania lub nie. | True<br/>Wartość FAŁSZ (ustawienie domyślne) | Nie |
| **redirectIncompatibleRowSettings** | Grupy właściwości, które mogą być określone, kiedy mają niezgodne wierszy hello toolog. | &nbsp; | Nie |
| **linkedServiceName** | Witaj połączonej usługi magazynu Azure toostore hello dziennika, który zawiera wiersze hello pominięte. | Nazwa Hello [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) lub [element AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) połączonej usługi, która odwołuje się toohello magazynu wystąpienia, które mają plik dziennika hello toostore toouse. | Nie |
| **Ścieżka** | Ścieżka Hello hello pliku dziennika, który zawiera hello pominięte wierszy. | Określ, które mają niezgodne dane hello toolog toouse ścieżki do magazynu obiektów Blob hello. Jeśli ścieżka nie zostanie określona, usługa hello tworzy kontener dla Ciebie. | Nie |

## <a name="monitoring"></a>Monitorowanie
Po zakończeniu uruchamiania działania kopiowania hello, można wyświetlić hello Liczba pominiętych wierszy w sekcji monitorowanie hello:

![Monitor pominięte niezgodne wierszy](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

Jeśli skonfigurujesz toolog hello niezgodne wiersze pliku dziennika hello na tej ścieżce można znaleźć: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` w pliku dziennika hello, można zobaczyć hello wierszy, które zostały pominięte i hello główną przyczynę hello niezgodności.

Zarówno hello oryginalnych danych, jak i odpowiednie błąd hello są rejestrowane w pliku hello. Oto przykład zawartości pliku dziennika hello jest następujący:
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat działania kopiowania fabryki danych Azure, zobacz [przenoszenia danych za pomocą działania kopiowania](data-factory-data-movement-activities.md).
