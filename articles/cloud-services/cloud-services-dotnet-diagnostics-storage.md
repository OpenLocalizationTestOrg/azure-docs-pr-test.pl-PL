---
title: "aaaStore i widoku danych diagnostycznych w usłudze Azure Storage | Dokumentacja firmy Microsoft"
description: "Pobierz dane diagnostyczne platformy Azure do usługi Azure Storage i wyświetlić"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a>Magazyn i widoku danych diagnostycznych w usłudze Azure Storage
Dane diagnostyczne nie są trwale przechowywane, chyba że transfer emulatora magazynu Microsoft Azure toohello lub pamięci masowej tooAzure. Raz w magazynie, można je wyświetlić jeden z kilku dostępnych narzędzi.

## <a name="specify-a-storage-account"></a>Określ konto magazynu
Należy określić hello konta magazynu, które mają toouse w pliku pliku ServiceConfiguration.cscfg hello. informacje o koncie Hello jest zdefiniowany jako parametry połączenia w ustawieniu konfiguracji. Witaj poniższy przykład przedstawia hello domyślnego ciągu połączenia utworzone dla nowego projektu usługi w chmurze w programie Visual Studio:

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

Możesz zmienić ten tooprovide konta informacje o parametrach połączenia dla konta magazynu platformy Azure.

W zależności od typu hello zbieranych danych diagnostycznych diagnostyki Azure korzysta z usługi Blob hello lub hello usługi tabel. Witaj poniższej tabeli przedstawiono hello źródeł danych, które są zachowywane i ich format.

| Źródło danych | Formatu magazynowania |
| --- | --- |
| Dzienniki platformy Azure |Tabela |
| Dzienniki usług IIS 7.0 |Obiekt blob |
| Dzienników infrastruktury Diagnostyka Azure |Tabela |
| Nie można zażądać dzienników |Obiekt blob |
| Dzienniki zdarzeń systemu Windows |Tabela |
| Liczniki wydajności |Tabela |
| Zrzuty awaryjne |Obiekt blob |
| Dzienniki błędów niestandardowych |Obiekt blob |

## <a name="transfer-diagnostic-data"></a>Transfer danych diagnostycznych
Dla zestawu SDK, 2.5 lub nowszego oraz danych diagnostycznych hello żądania tootransfer może występować hello pliku konfiguracji. Można przenieść dane diagnostyczne w zaplanowanych odstępach czasu określonych w konfiguracji hello.

2.4 zestawu SDK i poprzednich można zażądać danych diagnostycznych hello tootransfer za pomocą pliku konfiguracji hello również jako programowo. rozwiązanie programowe Hello umożliwia również toodo na żądanie transferu.

> [!IMPORTANT]
> Podczas transferu danych diagnostycznych tooan kontem magazynu platformy Azure, możesz pociągnąć za sobą koszty hello zasobów magazynu, które używa danych diagnostycznych.
> 
> 

## <a name="store-diagnostic-data"></a>Przechowywanie danych diagnostycznych
W magazynie obiektów Blob lub tabel są przechowywane dane dziennika o hello następujące nazwy:

**Tabele**

* **WadLogsTable** — dzienniki zapisywane w kodzie za pomocą hello nasłuchującego śledzenia.
* **WADDiagnosticInfrastructureLogsTable** -diagnostycznych zmiany monitora i konfiguracji.
* **WADDirectoriesTable** — katalogów monitora diagnostycznego hello jest monitorowanie.  Obejmuje to dzienniki programu IIS, usługi IIS nie powiodło się, dzienniki żądań i niestandardowych katalogów.  Hello lokalizację pliku dziennika blob hello jest określony w polu kontenera hello i pole RelativePath hello jest nazwa hello hello obiektu blob.  pole ŚcieżkaBezwględna Hello wskazuje hello lokalizację i nazwę pliku hello znajdowały się na powitania maszyny wirtualnej platformy Azure.
* **WADPerformanceCountersTable** — liczniki wydajności.
* **WADWindowsEventLogsTable** — dzienniki zdarzeń systemu Windows.

**Obiekty blob**

* **wad formantu kontenera** — (tylko w przypadku 2.4 zestawu SDK i poprzedniego) zawiera pliki konfiguracji XML hello sterujących hello diagnostycznych platformy Azure.
* **wad — usługi iis-failedreqlogfiles** — zawiera informacje z dzienników usług IIS nie powiodło się żądanie.
* **wad — usługi iis-logfiles** — zawiera informacje o dziennikach usług IIS.
* **"niestandardowe"** — niestandardowe kontenera oparte na Konfigurowanie katalogów, które są monitorowane przez monitor diagnostyczny hello.  Nazwa Hello tego kontenera obiektu binarnego zostanie określona w WADDirectoriesTable.

## <a name="tools-tooview-diagnostic-data"></a>Dane diagnostyczne tooview narzędzia
Kilka narzędzi są dostępne tooview hello danych po toostorage przeniesione. Na przykład:

* Eksploratora serwera w programie Visual Studio — Jeśli zainstalowano hello Azure Tools dla programu Microsoft Visual Studio, służy hello Azure Storage węzła w Eksploratorze serwera tooview tylko do odczytu obiektów blob i tabeli danych z kontami magazynu Azure. Można wyświetlić dane z Twojego konta emulatora magazynu lokalnego, a także z kont magazynu utworzonym dla platformy Azure. Aby uzyskać więcej informacji, zobacz [przeglądanie i zarządzanie zasobami magazynu za pomocą Eksploratora serwera](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).
* [Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest aplikacją autonomiczną, która umożliwia tooeasily pracy z danymi usługi Azure Storage w systemach Windows, OS x i Linux.
* [Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) zawiera Menedżera diagnostyki Azure, dzięki czemu można tooview, pobierania i zarządzania hello danych diagnostycznych zebranych aplikacji hello działających na platformie Azure.

## <a name="next-steps"></a>Następne kroki
[Przepływ hello śledzenia w aplikacji usługi w chmurze Diagnostyka Azure](cloud-services-dotnet-diagnostics-trace-flow.md)

