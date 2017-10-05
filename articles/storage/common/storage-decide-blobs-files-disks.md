---
title: "Kiedy należy użyć obiektów blob Azure, Azure plików lub dyski danych Azure"
description: "Dowiedz się o różnych sposobach do przechowywania i udostępniania danych na platformie Azure, aby pomóc zdecydować technologii."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: robinsh
ms.openlocfilehash: 452030e2e55ebeae55be2bd858c59e45428c7621
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deciding-when-to-use-azure-blobs-azure-files-or-azure-data-disks"></a>Kiedy należy użyć obiektów blob Azure, Azure plików lub dyski danych Azure

Microsoft Azure udostępnia kilka funkcji w usłudze Azure Storage do przechowywania i uzyskiwania dostępu do danych w chmurze. W tym artykule omówiono plików Azure, obiekty BLOB i dysków z danymi i jest przeznaczony do pomaga wybrać między tymi funkcjami.

## <a name="scenarios"></a>Scenariusze

W poniższej tabeli porównano pliki, obiekty BLOB i dysków z danymi i przedstawiono przykładowe scenariusze odpowiednie dla każdego.

| Funkcja | Opis | Kiedy stosować |
|--------------|-------------|-------------|
| **Usługa pliki Azure** | Udostępnia interfejs SMB, bibliotek klienckich i [interfejsu REST](/rest/api/storageservices/file-service-rest-api) umożliwiającą dostęp z dowolnego miejsca do przechowywanych plików. | Aby "przyrostu i przesunięcia" aplikacji w chmurze, które używa już system plików natywnych interfejsów API do udostępniania danych między nim a inne aplikacje działające na platformie Azure.<br/><br/>Chcesz przechowywać rozwoju i narzędzia debugowania, które muszą być dostępne z wielu maszyn wirtualnych. |
| **Obiekty BLOB platformy Azure** | Udostępnia biblioteki klienta i [interfejsu REST](/rest/api/storageservices/blob-service-rest-api) umożliwiająca danych bez struktury przechowywanych i dostępne w bardzo dużej skali w blokowych obiektów blob. | Ma aplikacji do obsługi przesyłania strumieniowego i scenariusze dostępie.<br/><br/>Chcesz można było uzyskać dostęp do danych aplikacji z dowolnego miejsca. |
| **Dyski danych Azure** | Udostępnia biblioteki klienta i [interfejsu REST](/rest/api/compute/virtualmachines/virtualmachines-create-or-update) umożliwiająca danych trwale przechowywane i uzyskać dostęp z dołączonego wirtualnego dysku twardego. | Chcesz przyrostu lub klawisz shift, aplikacje używające systemu plików natywnych interfejsów API do odczytywania i zapisywania danych na dyski stałe.<br/><br/>Chcesz przechowywać dane, które nie jest wymagane do jako dostępne spoza maszyny wirtualnej, do której jest dołączona dysku. |

## <a name="comparison-files-and-blobs"></a>Porównania: Pliki i obiekty BLOB

W poniższej tabeli porównano plików Azure z obiektami blob Azure.  
  
||||  
|-|-|-|  
|**Atrybut**|**Obiekty BLOB platformy Azure**|**Usługa pliki Azure**|  
|Opcje trwałości|Magazyn LRS, ZRS, GRS (i RA-GRS, aby uzyskać większą dostępność)|MAGAZYN LRS, GRS W WARSTWIE|  
|Ułatwienia dostępu|Interfejsy API REST|Interfejsy API REST<br /><br /> Protokół SMB 2.1 i 3.0 protokołu SMB (systemu plików standardowych interfejsów API)|  
|Łączność|Interfejsy API REST — na całym świecie|Interfejsy API REST - na całym świecie<br /><br /> Protokół SMB 2.1--w obrębie regionu<br /><br /> Protokół SMB 3.0 — na całym świecie|  
|Punkty końcowe|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|Katalogi|Prosty obszar nazw|Obiekty katalogu true|  
|Uwzględniana wielkość liter nazwy|Uwzględniana wielkość liter|Bez uwzględniania wielkości liter, ale w przypadku zachowania|  
|Pojemność|Do 500 TB kontenerów|Udziały plików 5 TB|  
|Przepływność|Do 60 MB/s dla blokowych obiektów blob|Do 60 MB/s dla każdej udziału|  
|Rozmiar obiektu|Maksymalnie 200 GB/blokowych obiektów blob|Maksymalnie 1 TB/pliku|  
|Pojemność rachunku|Oparte na zapisanych bajtów|Na podstawie rozmiaru plików|  
|Biblioteki klienckie|Wiele języków|Wiele języków|  
  
## <a name="comparison-files-and-data-disks"></a>Porównania: Pliki i dyski danych

Usługa pliki Azure uzupełniają dyski danych Azure. Dysk z danymi może zostać dołączona tyko do jednej maszyny wirtualnej Azure naraz. Dyski danych są ustalonym formacie wirtualne dyski twarde, przechowywane jako stronicowe obiekty BLOB w magazynie Azure i są używane przez maszynę wirtualną do przechowywania danych trwałych. Udziały plików w plikach Azure można uzyskać w taki sam sposób jak dysk lokalny jest dostępny (przy użyciu systemu plików natywnych interfejsów API) i może być współużytkowana przez wiele maszyn wirtualnych.  
 
W poniższej tabeli porównano plików Azure z dyskami danych Azure.  
 
||||  
|-|-|-|  
|**Atrybut**|**Dyski danych Azure**|**Usługa pliki Azure**|  
|Zakres|Wyłącznie dla jednej maszyny wirtualnej|Dostępu współdzielonego między wieloma maszynami wirtualnymi|  
|Migawki i kopii|Tak|Nie|  
|Konfiguracja|Połączone podczas uruchamiania maszyny wirtualnej|Połączone po uruchomieniu maszyny wirtualnej|  
|Authentication|Wbudowane|Skonfiguruj za pomocą polecenie net use|  
|Czyszczenie|Automatyczne|Ręcznie|  
|Dostęp za pomocą usługi REST|Nie można uzyskać dostępu do plików w ramach dysku VHD|Możliwy jest przechowywana w udziale plików|  
|Maksymalny rozmiar|Dysk 1 TB|5 TB udostępnianie plików i 1 TB, w udziale pliku|  
|Maksymalna liczba IOps 8KB|500 IOps|1000 IOps|  
|Przepływność|Do 60 MB/s dla każdego dysku|Do 60 MB/s dla każdej udziału plików|  

## <a name="next-steps"></a>Następne kroki

Podczas podejmowania decyzji o sposób przechowywania i uzyskać dostępu do danych, należy również rozważyć koszty związane. Aby uzyskać więcej informacji, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/).
  
Niektóre funkcje protokołu SMB nie mają zastosowania do chmury. Aby uzyskać więcej informacji, zobacz [funkcji nie są obsługiwane przez usługę Azure pliku](/rest/api/storageservices/features-not-supported-by-the-azure-file-service).
  
Aby uzyskać więcej informacji dotyczących dysków z danymi, zobacz [Zarządzanie dyskami i obrazy](../../virtual-machines/windows/about-disks-and-vhds.md) i [jak dołączyć dysku danych do maszyny wirtualnej systemu Windows](../../virtual-machines/windows/classic/attach-disk.md).