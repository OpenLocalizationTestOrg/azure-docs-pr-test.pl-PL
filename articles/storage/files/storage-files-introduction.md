---
title: "tooAzure aaaIntroduction magazyn plików | Dokumentacja firmy Microsoft"
description: "Wprowadzenie tooAzure magazyn plików, co zapewnia plików sieciowych udziałów w hello Microsoft Cloud"
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
ms.openlocfilehash: fe6826e79c364a6956831d2e273c4342a5fd47f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Wprowadzenie tooAzure magazyn plików

Magazyn plików Azure oferuje udziały plików sieciowego w chmurze hello przy użyciu standardu branżowego hello [protokołu bloku komunikatów serwera (SMB)](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) i [pliku System CIFS (Common Internet)](https://technet.microsoft.com/library/cc939973.aspx). Udziały plików platformy Azure mogą być instalowane równolegle przez maszyny wirtualne platformy Azure oraz wdrożenia lokalne z systemem Windows, macOS lub Linux. Konto magazynu ogólnego przeznaczenia zapewnia dostęp tooAzure pliku magazynu, magazynu obiektów Blob platformy Azure i magazynem kolejek Azure.

## <a name="videos"></a>Filmy wideo
| Wprowadzenie do usługi Azure File Storage (27 min) | Samouczek usługi Azure File Storage (5 minut)  |
|-|-|
| [![Screencast wideo magazyn plików Azure wprowadzenie hello — kliknij tooplay!](./media/storage-files-introduction/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![Screencast magazyn plików Azure hello samouczek — kliknij tooplay!](./media/storage-files-introduction/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Na czym polega przydatność usługi Azure File Storage

Magazyn plików Azure umożliwia tooreplace serwera systemu Windows, Linux, lub serwerach plików z systemem NAS obsługiwanego lokalnie lub w chmurze hello przy użyciu pliku chmury systemu operacyjnego bez udostępniania. Magazyn plików Azure ma hello następujące korzyści:

* **Dostęp do udostępnionych** branży hello Obsługa standardowego protokołu SMB, co oznacza można bezproblemowo zastąpić udziałów plików z lokalnymi udziały plików platformy Azure bez obaw o zgodność aplikacji udziały plików platformy Azure. Trwa stanie tooaccess udział plików z wielu komputerów i aplikacji/wystąpienia jest znaczących korzyści z usługi Magazyn plików Azure.

* **Do pełnego zarządzania** bez hello potrzeby toomanage sprzętu lub systemu operacyjnego, który oznacza, że nie masz toodeal z poprawki hello system operacyjny serwera z uaktualnień krytycznych lub wymiana uszkodzone dyski twarde można tworzyć udziały plików platformy Azure.

* **Skrypty i narzędzia** poleceń cmdlet programu PowerShell i interfejsu wiersza polecenia Azure mogą być używane toocreate zainstalować i Zarządzanie udziałami plików Azure w ramach hello administracji aplikacjami platformy Azure. Można tworzyć i zarządzać udziałami plików Azure przy użyciu hello [portalu Azure](https://portal.azure.com) i hello [Eksploratora usługi Storage Azure](https://storageexplorer.com). 

* **Odporność** magazyn plików Azure została utworzona z hello tła się toobe zawsze dostępne. Zastępowanie lokalnymi udziałami plików Azure magazynu oznacza, że nie jest już toowake się toodeal awarie zasilania lokalnego lub problemy z siecią. 

* **Znanych programowania** aplikacje działające na platformie Azure mają dostęp do danych w udziale hello za pośrednictwem [interfejsów API We/Wy systemu plików](https://msdn.microsoft.com/library/system.io.file.aspx). Temu programiści mogą wykorzystać istniejący kod i własne umiejętności toomigrate istniejących aplikacji. Ponadto tooSystem interfejsów API we/wy, możesz można użyć dowolnego klienta magazynu Azure hello biblioteki, takich jak hello jedną do [.NET](/dotnet/api/overview/azure/storage?view=azure-dotnet), lub hello [interfejsu API REST magazynu Azure](/rest/api/storageservices/file-service-rest-api).

Udziałów plików platformy Azure można używać w następujących celach:

* **Zamień lokalnych serwerach plików** magazyn plików Azure może być udziałów plików Zamień toocompletely używane na serwerach plików tradycyjnych, lokalnie lub urządzeniach NAS. Popularnych systemów operacyjnych, takich jak Windows, system macOS i Linux można łatwo zainstalować udziału plików platformy Azure wszędzie tam, gdzie znajdują się w hello world.

* **Migrowanie aplikacji metodą „lift and shift”**

    Magazyn plików Azure ułatwia zbyt "przyrostu i przesunięcia" aplikacje toohello chmurze używane pliku lokalnego udostępnia dane tooshare między częściami aplikacji hello. tooimplement, to każda maszyna wirtualna łączy z udziału plików toohello i następnie może odczytywać i zapisywać pliki, podobnie jak jego czy względem pliku lokalnego udziału.

* **Uproszczenie projektowania aplikacji w chmurze**
    
    Magazyn plików Azure można na wiele sposobów toosimplify nowych chmury rozwoju projektów.
    
    * **Współdzielone ustawienia aplikacji**
    
        Wzorzec wspólne dla aplikacji rozproszonych jest toohave pliki konfiguracji w centralnej lokalizacji, gdzie są one dostępne z wielu różnych maszyn wirtualnych. Takie pliki konfiguracji można teraz przechowywać w udziale plików platformy Azure, skąd mogą być odczytywane przez wszystkie wystąpienia aplikacji. Te ustawienia mogą być także zarządzane za pośrednictwem interfejsu REST hello, co umożliwia dostęp na całym świecie toohello pliki konfiguracji.

    * **Udział diagnostyczny**
    
        Udziału plików platformy Azure mogą być również używane toosave plików diagnostycznych, takich jak dzienniki, metryki i zrzuty awaryjne. O udziałach plików dostępnych za pośrednictwem zarówno hello SMB, jak i interfejs REST umożliwia toobuild aplikacji ani wykorzystywać różnych narzędzi analizy do przetwarzania i analizowania danych diagnostycznych hello.

    * **Projektowanie/testowanie/debugowanie**

        Gdy deweloperzy i Administratorzy działają na maszynach wirtualnych w chmurze hello, często muszą zestaw narzędzi. Instalowanie i rozpowszechnianie tych narzędzi na każdej maszynie wirtualnej, na której są one potrzebne, może być czynnością czasochłonną. Magazyn plików Azure deweloper lub administrator może przechowywać ich ulubionych narzędzi w udziale plików, które mogą być łatwo połączonych toofrom żadnej maszyny wirtualnej.
        
## <a name="how-does-it-work"></a>Jak to działa?

Zarządzanie udziałami plików platformy Azure jest znacznie prostsze niż zarządzanie lokalnymi udziałami plików. powitania po diagram ilustruje konstrukcje zarządzania magazyn plików Azure hello:

![Struktura plików](./media/storage-files-introduction/files-concepts.png)

* **Konto magazynu** wszystkie dostępu tooAzure magazynu odbywa się za pomocą konta magazynu. Aby uzyskać szczegółowe informacje na temat pojemności konta magazynu, zobacz [Cele dotyczące skalowalności i wydajności](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

* **Udział** Udział usługi File Storage jest udziałem plików SMB na platformie Azure. Wszystkie pliki i katalogi muszą być tworzone w udziale nadrzędnym. Konto może zawierać nieograniczoną liczbę udziałów, a udział może przechowywać nieograniczoną liczbę plików w górę toohello 5 TB całkowita pojemność hello udziału plików.

* **Katalog** Opcjonalna hierarchia katalogów.

* **Plik** pliku w udziale hello. Plik może być aktywne TB too1 rozmiar.

* **Format adresu URL** plików mają hello następującego formatu adresu URL:  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```

## <a name="next-steps"></a>Następne kroki

* [Create Azure File Share](storage-how-to-create-file-share.md) (Tworzenie udziału plików platformy Azure)
* [Connect and Mount on Windows](storage-how-to-use-files-windows.md) (Nawiązywanie połączenia i instalowanie w systemie Windows)
* [Connect and Mount on Linux](storage-how-to-use-files-linux.md) (Nawiązywanie połączenia i instalowanie w systemie Linux)
* [Connect and Mount on macOS](storage-how-to-use-files-mac.md) (Nawiązywanie połączenia i instalowanie w systemie macOS)
* [Często zadawane pytania](../storage-files-faq.md)
* [Rozwiązywanie problemów w systemie Windows](storage-troubleshoot-windows-file-connection-problems.md)   
* [Rozwiązywanie problemów w systemie Linux](storage-troubleshoot-linux-file-connection-problems.md)   

<!-- Rena I would remove any articles from here that are more than a year old. - Robin-->
### <a name="conceptual-articles-and-videos"></a>Artykuły koncepcyjne i filmy
* [Azure File Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Azure File Storage: płynnie działający system plików SMB w chmurze dla systemów Windows i Linux)

### <a name="tooling-support-for-azure-file-storage"></a>Narzędzia dostępne dla usługi Azure File Storage
* [Jak toouse AzCopy z usługi Magazyn Microsoft Azure](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Przy użyciu hello wiersza polecenia platformy Azure z usługą Azure Storage](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)

### <a name="blog-posts"></a>Wpisy na blogach
* [Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/) (Usługa Azure File Storage została udostępniona publicznie)
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Za kulisami usługi Azure File Storage)
* [Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx) (Wprowadzenie do usługi plików platformy Microsoft Azure)
* [Migrowanie danych tooAzure pliku](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Dokumentacja
* [Dokumentacja biblioteki klienta usługi Storage dla programu .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Dokumentacja interfejsu API REST usługi plików](http://msdn.microsoft.com/library/azure/dn167006.aspx)
