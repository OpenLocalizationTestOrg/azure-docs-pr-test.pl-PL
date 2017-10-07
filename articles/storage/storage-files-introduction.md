---
title: "tooAzure aaaIntroduction magazyn plików | Dokumentacja firmy Microsoft"
description: "Omówienie usługi Magazyn plików Azure to usługa umożliwiająca możesz toocreate i używanie plików sieciowych udziałów w hello firmy Microsoft w chmurze przy użyciu standardu branżowego hello."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: a0a6a80a2ccd9742aa470bdd02ff375387a1629b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Wprowadzenie tooAzure magazyn plików
Magazyn plików Azure oferuje udziały plików sieciowego w chmurze hello przy użyciu standardu branżowego hello [protokołu bloku komunikatów serwera (SMB)](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) i [pliku System CIFS (Common Internet)](https://technet.microsoft.com/library/cc939973.aspx). Udziały plików platformy Azure mogą być instalowane równolegle przez klientów, takich jak wdrożenia lokalne systemu Windows, macOS i Linux, oraz przez usługę Azure Virtual Machines. Konto magazynu ogólnego przeznaczenia zapewnia dostęp tooAzure magazynu plików i innych usług, takich jak obiekty BLOB, dyski maszyny wirtualnej Azure, kolejek w ramach jednego konta.



## <a name="videos"></a>Filmy wideo
| Wprowadzenie do usługi Azure File Storage (27 min) | Samouczek usługi Azure File Storage (5 minut)  |
|-|-|
| [![Screencap wideo magazyn plików Azure wprowadzenie hello — kliknij tooplay!](media/storage-file-storage/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![Screencap magazyn plików Azure hello samouczek — kliknij tooplay!](media/storage-file-storage/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Na czym polega przydatność usługi Azure File Storage
Magazyn plików Azure umożliwia tooreplace serwera systemu Windows, Linux, lub serwerach plików z systemem NAS obsługiwanego lokalnie lub w chmurze hello przy użyciu pliku chmury systemu operacyjnego bez udostępniania. To ustawienie hello następujące korzyści:

* **Dostęp współdzielony**. Branży hello Obsługa standardowego protokołu SMB, co oznacza można bezproblemowo zastąpić udziałów plików z lokalnymi udziały plików platformy Azure bez obaw o zgodność aplikacji udziały plików platformy Azure. Trwa stanie tooshare system plików na wielu komputerach, aplikacje/wystąpień jest znaczących korzyści z magazynem plików Azure w przypadku aplikacji wymagających shareability. 
* **Pełne zarządzanie**. Udziały plików platformy Azure mogą być tworzone bez hello potrzeby toomanage sprzętu lub systemu operacyjnego. Oznacza to, że nie masz toodeal z poprawki hello system operacyjny serwera z uaktualnień krytycznych lub wymiana uszkodzone dyski twarde.
* **Skrypty i narzędzia**. Polecenia cmdlet programu PowerShell i interfejsu wiersza polecenia Azure mogą być używane toocreate instalacji oraz zarządzania nimi udziałów magazynu plików jako część hello administracji aplikacjami platformy Azure. Można tworzyć i zarządzać udziałami plików na platformę Azure przy użyciu portalu Azure i usługi Azure storage Eksploratora. 
* **Odporność**. Magazyn plików Azure został skompilowany z hello tła się toobe zawsze dostępne. Zastępowanie lokalnymi udziałami plików Azure magazynu oznacza, że nie jest już toowake się toodeal awarie zasilania lokalnego lub problemy z siecią. 
* **Znajomy sposób programowania**. Aplikacje działające na platformie Azure mają dostęp do danych w udziale hello za pomocą pliku [interfejsów API We/Wy systemu](https://msdn.microsoft.com/library/system.io.file.aspx). Temu programiści mogą wykorzystać istniejący kod i własne umiejętności toomigrate istniejących aplikacji. Ponadto tooSystem interfejsów API we/wy, można użyć [biblioteki klienta magazynu Azure](https://msdn.microsoft.com/library/azure/dn261237.aspx) lub hello [interfejsu API REST magazynu Azure](/rest/api/storageservices/file-service-rest-api).

Udziałów plików platformy Azure można używać w następujących celach:

* **Zastąpienie lokalnych serwerów plików**:  
    Magazyn plików Azure można udziałów plików Zamień toocompletely używane na serwerach plików tradycyjnych, lokalnie lub urządzeniach NAS. Popularnych systemów operacyjnych, takich jak Windows, system macOS i Linux można łatwo zainstalować udziału plików platformy Azure wszędzie tam, gdzie znajdują się w hello world.

* **Migrowanie aplikacji metodą „lift and shift”**:  
    Magazyn plików Azure ułatwia zbyt "przyrostu i przesunięcia" aplikacje toohello chmurze używane pliku lokalnego udostępnia dane tooshare między częściami aplikacji hello. toomake się to zdarzyć, każda maszyna wirtualna połączenie toohello udziału plików i następnie może odczytywać i zapisywać pliki, podobnie jak jego czy względem pliku lokalnego udziału.

* **Uproszczenie projektowania aplikacji w chmurze**:  
    Magazyn plików Azure można na wiele sposobów toosimplify nowych chmury rozwoju projektów.
    * **Współdzielone ustawienia aplikacji**:  
        Wzorzec wspólne dla aplikacji rozproszonych jest toohave pliki konfiguracji w centralnej lokalizacji, gdzie są one dostępne z wielu różnych maszyn wirtualnych. Takie pliki konfiguracji można teraz przechowywać w udziale plików platformy Azure, skąd mogą być odczytywane przez wszystkie wystąpienia aplikacji. Te ustawienia mogą być także zarządzane za pośrednictwem interfejsu REST hello, co umożliwia dostęp na całym świecie toohello pliki konfiguracji.

    * **Udział diagnostyczny**:  
        Udziału plików platformy Azure mogą być również używane toosave plików diagnostycznych, takich jak dzienniki, metryki i zrzuty awaryjne. O tych, które są dostępne za pośrednictwem interfejsu REST i hello SMB pozwala toobuild aplikacji i korzystać z różnych narzędzi analizy do przetwarzania i analizowania danych diagnostycznych hello.

    * **Projektowanie/testowanie/debugowanie**:  
        Gdy deweloperzy i Administratorzy działają na maszynach wirtualnych w chmurze hello, często muszą zestaw narzędzi. Instalowanie i rozpowszechnianie tych narzędzi na każdej maszynie wirtualnej, na której są one potrzebne, może być czynnością czasochłonną. Magazyn plików Azure deweloper lub administrator może przechowywać ich ulubionych narzędzi w udziale plików, które mogą być łatwo połączonych toofrom żadnej maszyny wirtualnej.
        
## <a name="how-does-it-work"></a>Jak to działa?
Zarządzanie udziałami plików platformy Azure jest znacznie prostsze niż zarządzanie lokalnymi udziałami plików. powitania po diagram ilustruje konstrukcje zarządzania magazyn plików Azure hello:

![Struktura plików](../../includes/media/storage-file-concepts-include/files-concepts.png)

* **Konto magazynu**: wszystkie dostępu tooAzure magazynu odbywa się za pomocą konta magazynu. Aby uzyskać szczegółowe informacje na temat pojemności konta magazynu, zobacz temat Cele usługi Azure Storage dotyczące skalowalności i wydajności.
* **Udział**: udział usługi File Storage jest udziałem plików SMB na platformie Azure. Wszystkie pliki i katalogi muszą być tworzone w udziale nadrzędnym. Konto może zawierać nieograniczoną liczbę udziałów, a udział może przechowywać nieograniczoną liczbę plików w górę toohello 5 TB całkowita pojemność hello udziału plików.
* **Katalog**: opcjonalna hierarchia katalogów.
* **Plik**: plik w udziale hello. Plik może być aktywne TB too1 rozmiar.
* **Format adresu URL**: plików mają hello następującego formatu adresu URL:  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```
## <a name="next-steps"></a>Następne kroki
* [Create Azure File Share](storage-file-how-to-create-file-share.md) (Tworzenie udziału plików platformy Azure)
* [Connect and Mount on Windows](storage-file-how-to-use-files-windows.md) (Nawiązywanie połączenia i instalowanie w systemie Windows)
* [Connect and Mount on Linux](storage-how-to-use-files-linux.md) (Nawiązywanie połączenia i instalowanie w systemie Linux)
* [Connect and Mount on macOS](storage-file-how-to-use-files-mac.md) (Nawiązywanie połączenia i instalowanie w systemie macOS)
* [Często zadawane pytania](storage-files-faq.md)
* [Rozwiązywanie problemów](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Artykuły koncepcyjne i filmy
* [Azure File Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Azure File Storage: płynnie działający system plików SMB w chmurze dla systemów Windows i Linux)

### <a name="tooling-support-for-azure-file-storage"></a>Narzędzia dostępne dla usługi Azure File Storage
* [Używanie programu Azure PowerShell z usługą Azure Storage](storage-powershell-guide-full.md)
* [Jak toouse AzCopy z usługi Magazyn Microsoft Azure](storage-use-azcopy.md)
* [Przy użyciu hello wiersza polecenia platformy Azure z usługą Azure Storage](storage-azure-cli.md#create-and-manage-file-shares)

### <a name="blog-posts"></a>Wpisy na blogach
* [Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/) (Usługa Azure File Storage została udostępniona publicznie)
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Za kulisami usługi Azure File Storage)
* [Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx) (Wprowadzenie do usługi plików platformy Microsoft Azure)
* [Migrowanie danych tooAzure pliku](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Dokumentacja
* [Dokumentacja biblioteki klienta usługi Storage dla programu .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Dokumentacja interfejsu API REST usługi plików](http://msdn.microsoft.com/library/azure/dn167006.aspx)
