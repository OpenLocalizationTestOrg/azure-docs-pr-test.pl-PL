---
title: "aaaDeciding podczas obiektów blob Azure toouse, pliki Azure lub dyski danych Azure"
description: "Informacje o hello różne sposoby toostore i danymi dostępu w Azure toohelp zdecydować, które toouse technologii."
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
ms.openlocfilehash: cd43abde43daf33dd7c43aa2696a9c8d5cd19612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deciding-when-toouse-azure-blobs-azure-files-or-azure-data-disks"></a>Przy wyborze, gdy obiekty BLOB Azure toouse plików Azure i dyski danych Azure

Microsoft Azure udostępnia kilka funkcji w usłudze Azure Storage do przechowywania i uzyskiwania dostępu do danych w chmurze hello. W tym artykule omówiono plików Azure, obiekty BLOB i dysków z danymi i jest zaprojektowana toohelp, wybrać między tymi funkcjami.

## <a name="scenarios"></a>Scenariusze

Witaj w poniższej tabeli porównuje pliki, obiekty BLOB i dysków z danymi i przedstawiono przykładowe scenariusze odpowiednie dla każdego.

| Funkcja | Opis | Gdy toouse |
|--------------|-------------|-------------|
| **Usługa pliki Azure** | Udostępnia interfejs SMB, bibliotek klienckich i [interfejsu REST](/rest/api/storageservices/file-service-rest-api) umożliwiającą dostęp z dowolnego miejsca toostored plików. | Ma zbyt "przyrostu i przesunięcia" chmura toohello aplikacji, która używa już hello natywny plik systemu interfejsów API tooshare danych między nim a inne aplikacje działające na platformie Azure.<br/><br/>Ma toostore rozwoju i narzędzia debugowania, które wymagają toobe użytkowcy wiele maszyn wirtualnych. |
| **Obiekty BLOB platformy Azure** | Udostępnia biblioteki klienta i [interfejsu REST](/rest/api/storageservices/blob-service-rest-api) umożliwiająca danych niestrukturalnych zbyt być przechowywane i dostępne w bardzo dużej skali w blokowych obiektów blob. | Ma Twojej aplikacji toosupport przesyłania strumieniowego i scenariusze dostępie.<br/><br/>Chcesz, aby dane aplikacji może tooaccess toobe z dowolnego miejsca. |
| **Dyski danych Azure** | Udostępnia biblioteki klienta i [interfejsu REST](/rest/api/compute/virtualmachines/virtualmachines-create-or-update) umożliwiająca toobe danych trwale przechowywane i dostępne z dołączonego wirtualnego dysku twardego. | Mają toolift i przesunięcia aplikacje, które Użyj tooread interfejsów API systemu natywny plik i zapisać dane toopersistent dysków.<br/><br/>Ma toostore danych, który nie jest wymagane toobe dostępne z dysku hello toowhich maszyny wirtualnej poza hello jest dołączony. |

## <a name="comparison-files-and-blobs"></a>Porównania: Pliki i obiekty BLOB

Hello w poniższej tabeli porównano plików Azure z obiektami blob Azure.  
  
||||  
|-|-|-|  
|**Atrybut**|**Obiekty BLOB platformy Azure**|**Usługa pliki Azure**|  
|Opcje trwałości|Magazyn LRS, ZRS, GRS (i RA-GRS, aby uzyskać większą dostępność)|MAGAZYN LRS, GRS W WARSTWIE|  
|Ułatwienia dostępu|Interfejsy API REST|Interfejsy API REST<br /><br /> Protokół SMB 2.1 i 3.0 protokołu SMB (systemu plików standardowych interfejsów API)|  
|Łączność|Interfejsy API REST — na całym świecie|Interfejsy API REST - na całym świecie<br /><br /> Protokół SMB 2.1--w obrębie regionu<br /><br /> Protokół SMB 3.0 — na całym świecie|  
|Punkty końcowe|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|Katalogi|Prosty obszar nazw|Obiekty katalogu true|  
|Uwzględniana wielkość liter nazwy|Uwzględniana wielkość liter|Bez uwzględniania wielkości liter, ale w przypadku zachowania|  
|Pojemność|Zapasowej too500 TB kontenerów|Udziały plików 5 TB|  
|Przepływność|Zapasowej too60 MB/s dla blokowych obiektów blob|Zapasowej too60 MB/s na jedną akcję|  
|Rozmiar obiektu|Zapasowej too200 GB/blokowych obiektów blob|Too1TB/pliku|  
|Pojemność rachunku|Oparte na zapisanych bajtów|Na podstawie rozmiaru plików|  
|Biblioteki klienckie|Wiele języków|Wiele języków|  
  
## <a name="comparison-files-and-data-disks"></a>Porównania: Pliki i dyski danych

Usługa pliki Azure uzupełniają dyski danych Azure. Dysk z danymi można tylko dołączone tooone maszyny wirtualnej platformy Azure w czasie. Dyski danych są ustalonym formacie wirtualne dyski twarde, przechowywane jako stronicowe obiekty BLOB w magazynie Azure i są używane przez hello danych trwałych toostore maszyny wirtualnej. Udziały plików w plikach Azure są dostępne w hello sam sposób jak hello dysk lokalny jest dostępny (przy użyciu systemu plików natywnych interfejsów API) i może być współużytkowana przez wiele maszyn wirtualnych.  
 
Hello w poniższej tabeli porównano plików Azure z dyskami danych Azure.  
 
||||  
|-|-|-|  
|**Atrybut**|**Dyski danych Azure**|**Usługa pliki Azure**|  
|Zakres|Wyłączny tooa jednej maszyny wirtualnej|Dostępu współdzielonego między wieloma maszynami wirtualnymi|  
|Migawki i kopii|Tak|Nie|  
|Konfiguracja|Połączone przy uruchamianiu hello maszyny wirtualnej|Połączone po rozpoczęciu hello maszyny wirtualnej|  
|Authentication|Wbudowane|Skonfiguruj za pomocą polecenie net use|  
|Czyszczenie|Automatyczne|Ręcznie|  
|Dostęp za pomocą usługi REST|Nie można uzyskać dostępu do plików znajdujących się w hello wirtualnego dysku twardego|Możliwy jest przechowywana w udziale plików|  
|Maksymalny rozmiar|Dysk 1 TB|5 TB udostępnianie plików i 1 TB, w udziale pliku|  
|Maksymalna liczba IOps 8KB|500 IOps|1000 IOps|  
|Przepływność|Zapasowej too60 MB/s na dysk|Zapasowej too60 MB/s dla udziału plików|  

## <a name="next-steps"></a>Następne kroki

Podczas podejmowania decyzji o sposób przechowywania i uzyskać dostępu do danych, należy również rozważyć hello koszty związane. Aby uzyskać więcej informacji, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/).
  
Niektóre funkcje protokołu SMB nie są stosowane toohello chmury. Aby uzyskać więcej informacji, zobacz [funkcji nie są obsługiwane przez hello usługa plików Azure](/rest/api/storageservices/features-not-supported-by-the-azure-file-service).
  
Aby uzyskać więcej informacji dotyczących dysków z danymi, zobacz [Zarządzanie dyskami i obrazy](../../virtual-machines/windows/about-disks-and-vhds.md) i [jak tooAttach tooa dysku danych maszyny wirtualnej systemu Windows](../../virtual-machines/windows/classic/attach-disk.md).
