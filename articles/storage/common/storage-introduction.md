---
title: tooAzure aaaIntroduction magazynu | Dokumentacja firmy Microsoft
description: Wprowadzenie tooAzure magazynu, przechowywanie danych firmy Microsoft w chmurze hello.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a>Wprowadzenie tooMicrosoft usługi Azure Storage

Microsoft Azure Storage to zarządzana przez firmę Microsoft usługa w chmurze zapewniająca bezpieczny, trwały, skalowalny i nadmiarowy magazyn o wysokiej dostępności. Firma Microsoft zajmuje się konserwacją oraz rozwiązywaniem krytycznych problemów. 

Usługa Azure Storage składa się z trzech usług danych: Blob Storage, File Storage i Queue Storage. Blob storage obsługuje zarówno warstwy standardowa i premium magazynu, z magazyn w warstwie premium za pomocą tylko dyski SSD dla hello najszybszym możliwą wydajność. Inna funkcja jest magazynu chłodnego, dzięki czemu toostorage dużych ilości danych rzadko używanych obniżenia kosztów.

W tym artykule opisano następujące hello:
* Witaj usług magazynu Azure
* Witaj typy kont magazynu
* Uzyskiwanie dostępu do obiektów blob, kolejek i plików
* Szyfrowanie
* Replikacja 
* Transferowanie danych z lub do magazynu
* Witaj wiele biblioteki klienta magazynu dostępne. 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a>Wprowadzenie do usługi Azure Storage hello

toouse podane hello usług przez usługi Azure Storage — magazynu obiektów Blob, Magazyn plików i magazynu kolejek — należy najpierw utworzyć konto magazynu, a następnie mogą przesłać dane z określonej usługi na tym koncie magazynu. 

## <a name="blob-storage"></a>Blob Storage

Obiekty blob to pliki podobne do tych, które przechowujesz na komputerze (lub tablecie, urządzeniu przenośnym itp.). Mogą to być obrazy, pliki programu Microsoft Excel, pliki HTML, wirtualne dyski twarde (VHD), dane big data, kopie zapasowe baz danych — w zasadzie dowolny rodzaj danych. Obiekty BLOB są przechowywane w kontenerach, które są podobne toofolders. 

Po przechowywanie plików w magazynie obiektów Blob, użytkownik może uzyskiwać do nich dostęp z dowolnego miejsca w Witaj świecie przy użyciu adresów URL, hello interfejsu REST lub jednego z biblioteki klienta magazynu Azure SDK hello. Biblioteki klienta magazynu są dostępne dla wielu języków, w tym Node.js, Java, PHP, Ruby, Python i .NET. 

Istnieją trzy typy obiektów blob: blokowe obiekty blob, uzupełnialne obiekty blob i stronicowe obiekty blob (używane w przypadku plików VHD).

* Blokowe obiekty BLOB są używane toohold zwykłe pliki zapasowej tooabout 4,7 TB. 
* Stronicowe obiekty BLOB są plikami dostęp losowy toohold używane zapasowej TB too8 rozmiar. Są one używane dla hello plików VHD, które wykonują kopie maszyn wirtualnych.
* Dołącz obiekty BLOB składają się z bloków, takich jak hello blokowych obiektów blob, lecz są zoptymalizowane pod kątem operacji dołączania. Są one używane dla elementów, jak rejestrowanie informacji toohello sam obiektu blob z wieloma maszynami wirtualnymi.

Dla bardzo dużych zestawów danych, gdy ograniczenia sieci uniemożliwić przekazanie lub pobranie tooBlob pamięci masowej w wypadku przewodowy hello możesz wysłać zestaw dysków twardych tooMicrosoft tooimport lub Eksportuj dane bezpośrednio z centrum danych hello. Zobacz [Użyj hello usługi Import/Eksport Microsoft Azure tooTransfer danych tooBlob magazynu](../storage-import-export-service.md).

## <a name="file-storage"></a>File Storage

Witaj usługi pliki Azure umożliwia tooset zapasowej udziałów plików sieciowych wysokiej dostępności, które są dostępne przy użyciu standardowego protokołu bloku komunikatów serwera (SMB) hello. Oznacza, że wiele maszyn wirtualnych można udostępniać hello same pliki z odczytu i zapisu. Możesz przeczytać hello plików przy użyciu interfejsu REST hello lub bibliotek klienckich magazynu hello. 

Rzecz, która odróżnia magazyn plików Azure z plików w udziale plików firmowych jest, że masz dostęp hello plików z dowolnego miejsca w Witaj świecie przy użyciu adresu URL, który wskazuje plik toohello i zawiera token sygnatury dostępu Współdzielonego dostępu współdzielonego. Można generować tokeny sygnatury dostępu Współdzielonego; umożliwiają one zasobów prywatnej tooa określonym dostępu dla określonego przedziału czasu. 

Udziałów plików można używać w wielu typowych scenariuszach: 

* Wiele aplikacji lokalnych korzysta z udziałów plików. Ta funkcja umożliwia łatwiejsze toomigrate tych aplikacji, które mają tooAzure danych. W przypadku instalowania hello sama litera który hello toohello udziału pliku lokalnego aplikacja używa, hello część aplikacji, który uzyskuje dostęp do udziału plików hello powinien współpracować z minimalne ewentualne zmiany.

* Pliki konfiguracji można przechowywać w udziale plików i uzyskiwać do nich dostęp z wielu maszyn wirtualnych. Narzędzi używanych przez wielu deweloperów w grupie mogą być przechowywane w udziale plików, zapewniając, że każdy można je znaleźć, i że używają one hello tej samej wersji.

* Dzienniki diagnostyczne, metryki i zrzuty awaryjne są tylko trzy przykłady, danych, które jest zapisywane tooa udziału plików i przetwarzany lub przeanalizowane później.

W tym czasie, uwierzytelnianie oparte na usłudze Active Directory i dostępu formantu listy (kontroli dostępu ACL) nie są obsługiwane, ale będzie na pewien czas w przyszłości hello. poświadczenia konta magazynu Hello są używane tooprovide uwierzytelniania dla udziału plików toohello dostępu. Oznacza to, każdy z udziałem hello zainstalowane będzie miał pełne odczytu/zapisu dostępu toohello udziału.

## <a name="queue-storage"></a>Queue Storage

Witaj usługi kolejek platformy Azure jest używana toostore i pobieranie wiadomości. Wiadomości w kolejce może być się o rozmiarze too64 KB, a kolejka może zawierać miliony komunikatów. Kolejki są zazwyczaj używane toostore listę toobe komunikaty przetwarzane asynchronicznie. 

Na przykład chcesz obrazów stanie tooupload toobe klientów i ma toocreate miniatur dla każdego obrazu. Może mieć klienta oczekuje na miniaturach hello toocreate podczas przekazywania hello obrazów. Alternatywą jest toouse kolejki. Po zakończeniu jego przekazywania powitania klienta zapisu toohello kolejki komunikatów. Następnie ma funkcję platformy Azure Pobierz wiadomość hello z kolejki hello i tworzenie miniatur hello. Elementy hello tego przetwarzania może być skalowana oddzielnie, zapewniając większą kontrolę podczas dostrajania go dla Ciebie.

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a>Magazyn tabel
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
Usługa Azure Table Storage w warstwie Podstawowa jest teraz częścią usługi Cosmos DB. Niemniej usługa Azure Table Storage jest też dostępna w warstwie Premium, która zapewnia tabele zoptymalizowane pod kątem przepływności, globalną dystrybucję i automatyczne indeksy pomocnicze. toolearn więcej i wypróbowywać hello nowe środowisko premium, zapoznaj się [bazy danych Azure rozwiązania Cosmos: Tabela interfejsu API](https://aka.ms/premiumtables).

## <a name="disk-storage"></a>Przechowywanie na dysku

Zespół usługi Azure Storage Hello jest także właścicielem dysków, zawierający wszystkie hello zarządzane i niezarządzane dysku możliwości używanych przez maszyny wirtualne. Aby uzyskać więcej informacji o tych funkcjach, zobacz hello [dokumentację usługi obliczeniowe](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).

## <a name="types-of-storage-accounts"></a>Typy kont magazynu 

W poniższej tabeli przedstawiono hello różne rodzaje kont magazynu i obiekty, które mogą być używane z każdego.

|**Typ konta magazynu**|**Przeznaczenie ogólne w warstwie Standardowa**|**Przeznaczenie ogólne w warstwie Premium**|**Usługa Blob Storage w gorącej i chłodnej warstwie dostępu**|
|-----|-----|-----|-----|
|**Obsługiwane usługi**| Usługi Blob, File i Queue | Usługa Blob | Usługa Blob|
|**Obsługiwane typy obiektów blob**|Blokowe obiekty blob, stronicowe obiekty blob, uzupełnialne obiekty blob | Stronicowe obiekty blob | Blokowe obiekty blob i uzupełnialne obiekty blob|

### <a name="general-purpose-storage-accounts"></a>Konta magazynu ogólnego przeznaczenia

Istnieją dwa rodzaje kont magazynu ogólnego przeznaczenia. 

#### <a name="standard-storage"></a>Standard Storage 

konta magazynu Hello najczęściej używane są konta magazynu w warstwie standardowa, które mogą być używane dla wszystkich typów danych. Konta magazynu w warstwie standardowa używać nośnika magnetycznego toostore danych.

#### <a name="premium-storage"></a>Premium Storage

Usługa Premium Storage zapewnia magazyn o wysokiej wydajności dla stronicowych obiektów blob, które są najczęściej używane w przypadku plików VHD. Konta Premium magazynu używać dysków SSD toostore danych. Firma Microsoft zaleca używanie usługi Premium Storage dla wszystkich maszyn wirtualnych.

### <a name="blob-storage-accounts"></a>Konta usługi Blob Storage

Konto magazynu obiektów Blob Hello to specjalne konto magazynu używane toostore blokowych obiektów blob i uzupełnialnych obiektów blob. Na tych kontach nie można przechowywać stronicowych obiektów blob, a zatem nie można też przechowywać plików VHD. Te konta pozwalają tooset tooHot warstwy dostępu lub chłodnej; Warstwa Hello można zmienić w dowolnym momencie. 

warstwy dostępu dynamicznej Hello jest używany dla plików, których dostęp jest uzyskiwany często — płacisz wyższy koszt dla magazynu, ale koszt hello uzyskiwania dostępu do obiektów blob hello jest znacznie niższa. Dla obiektów blob przechowywanych w warstwie dostępu do chłodnych hello płacisz wyższe koszty dostępu do obiektów blob hello, ale hello koszt magazynowania jest znacznie niższa.

## <a name="accessing-your-blobs-files-and-queues"></a>Uzyskiwanie dostępu do obiektów blob, plików i kolejek

Każde konto magazynu ma dwa klucze uwierzytelniania, przy czym każdego z nich można użyć do dowolnej operacji. Istnieją dwa klucze, aby zebrać na powitania od czasu do czasu kluczy tooenhance zabezpieczeń. Bardzo ważne, aby klucze były przechowywane bezpiecznego ponieważ zapoznały wraz z nazwy konta hello umożliwia nieograniczony dostęp tooall danych na koncie magazynu hello jest. 

W tej sekcji wygląda dwa sposoby toosecure hello konto magazynu i jego dane. Aby uzyskać szczegółowe informacje na temat zabezpieczania konta magazynu i danych, zobacz hello [przewodnik zabezpieczeń usługi Azure Storage](storage-security-guide.md).

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a>Zabezpieczanie dostępu do konta toostorage przy użyciu usługi Azure AD

Jednym ze sposobów toosecure dostępu tooyour magazynu danych jest kontrolowanie klucze konta magazynu toohello dostępu. Za pomocą Menedżera zasobów kontroli dostępu opartej na rolach (RBAC) można przypisać role toousers, grupy lub aplikacji. Te role są również powiązane tooa określony zbiór akcji, które ma być dozwolony lub niedozwolony. Przy użyciu funkcji RBAC konta magazynu tooa dostępu toogrant obsługuje tylko operacje zarządzania powitania dla tego konta magazynu, takich jak zmiana warstwy dostępu hello. Nie można użyć RBAC toogrant dostępu toodata obiektów, takich jak określonego kontenera lub w udziale plików. Można jednak RBAC toogrant dostępu toohello klucze konta magazynu, które mogą być następnie używane tooread hello danych obiektów. 

### <a name="securing-access-using-shared-access-signatures"></a>Zabezpieczanie dostępu przy użyciu sygnatur dostępu współdzielonego 

Można użyć sygnatur dostępu współdzielonego i przechowywane toosecure zasady dostępu do obiektów danych. Sygnatury dostępu współdzielonego (SAS) to ciąg zawierający token zabezpieczający, który może być dołączony toohello identyfikatora URI dla zasobu, który pozwala toodelegate dostępu toospecific magazynu obiektów i ograniczenia toospecify, takich jak uprawnienia i hello daty/godziny zakresu dostępu. Ta funkcja ma rozbudowane możliwości. Aby uzyskać szczegółowe informacje, zobacz zbyt[przy użyciu dostępu sygnatur dostępu Współdzielonego](storage-dotnet-shared-access-signature-part-1.md).

### <a name="public-access-tooblobs"></a>Tooblobs dostępu publicznego

Usługa Blob Hello umożliwia tooprovide dostępu publicznego tooa kontenera i jego obiektów blob lub konkretnego obiektu blob. Po wskazaniu, że kontener lub obiekt blob jest publiczny, dowolny użytkownik może go anonimowo odczytać — uwierzytelnianie nie jest wymagane. Przykład kiedy warto toodo to w przypadku witryny sieci Web korzystających z obrazów, wideo lub dokumentami z magazynu obiektów Blob. Aby uzyskać więcej informacji, zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiektów blob](../blobs/storage-manage-access-to-resources.md) 

## <a name="encryption"></a>Szyfrowanie

Brak dostępnych kilka podstawowych typów szyfrowania dla usług magazynu hello. 

### <a name="encryption-at-rest"></a>Szyfrowanie w spoczynku 

Można włączyć szyfrowanie usługi Magazyn (SSE) w usłudze plików albo hello (wersja zapoznawcza) lub hello usługi obiektów Blob dla konta magazynu platformy Azure. Jeśli opcja jest włączona, wszystkie dane zapisane toohello określonej usługi są szyfrowane przed zapisaniem. Podczas odczytu danych hello, zostaje odszyfrowywany przed zwróceniem. 

### <a name="client-side-encryption"></a>Szyfrowania po stronie klienta

Witaj biblioteki klienta magazynu ma można wywołać metody tooprogrammatically szyfrowania danych przed wysłaniem przez hello przewodowy z powitania klienta tooAzure. Przechowywane dane są zaszyfrowane, co oznacza, że w stanie spoczynku również są zaszyfrowane. Podczas odczytywania danych hello Wstecz, odszyfrowywania informacji powitania po jego otrzymania. 

### <a name="encryption-in-transit-with-azure-file-shares"></a>Szyfrowanie podczas transferu przy użyciu udziałów plików platformy Azure

Zobacz [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) (Używanie sygnatur dostępu współdzielonego), aby uzyskać więcej informacji o sygnaturach dostępu współdzielonego. Zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](../blobs/storage-manage-access-to-resources.md) i [uwierzytelniania dla usług magazynu Azure hello](https://msdn.microsoft.com/library/azure/dd179428.aspx) Aby uzyskać więcej informacji na koncie magazynu tooyour bezpiecznego dostępu.

Aby uzyskać więcej informacji na temat zabezpieczania konta magazynu i szyfrowania, zobacz hello [przewodnik zabezpieczeń usługi Azure Storage](storage-security-guide.md).

## <a name="replication"></a>Replikacja

Tooensure kolejności, że dane są trwałe magazyn Azure ma hello możliwości tookeep (i zarządzania nimi) wiele kopii danych. Jest to nazywane replikacją lub czasami nadmiarowością. Podczas konfigurowania konta magazynu należy określić typ replikacji. W większości przypadków można zmodyfikować to ustawienie po skonfigurowaniu hello konta magazynu. 

Wszystkie konta magazynu mają **magazyn lokalnie nadmiarowy (LRS, locally redundant storage)**. Oznacza to, trzy kopie danych są zarządzane przez usługi Azure Storage w centrum danych hello określić, kiedy hello konta magazynu zostały skonfigurowane. Podczas zmiany zostaną zatwierdzone tooone skopiować, Witaj dwie kopie są aktualizowane przed zwróceniem Powodzenie. Oznacza to, że repliki trzy hello zawsze są zsynchronizowane. Ponadto hello trzy kopie znajdują się w domenach awarii oddzielne i uaktualnienia domen, co oznacza, że dane są dostępne, nawet w przypadku awarii węzła Magazyn zawierający dane lub zaktualizowaniu podjęte toobe w trybie offline. 

**Magazyn lokalnie nadmiarowy (LRS)**

Jak wyjaśniono powyżej, dzięki magazynowi LRS masz trzy kopie danych w jednym centrum danych. Obsługuje problem hello danych staje się niedostępny, jeśli węzeł magazynu nie powiedzie się lub jest pobierana w trybie offline toobe zaktualizowane, ale nie hello przypadku całe centrum danych staje się niedostępna.

**Magazyn strefowo nadmiarowy (ZRS, Zone redundant storage)**

Magazyn strefowo nadmiarowy (ZRS) przechowuje trzy kopie lokalne powitania danych, a także innego zestawu trzy kopie danych. Hello drugi zestaw trzy kopie są replikowane asynchronicznie w centrach danych w ramach jednego lub dwóch regionach. Należy pamiętać, że magazyn ZRS jest dostępny tylko w przypadku blokowych obiektów blob na kontach magazynu ogólnego przeznaczenia. Ponadto po utworzeniu konta magazynu i wybraniu magazynu ZRS nie można przekonwertować go toouse tooany innych wpisz replikacji lub na odwrót.

Konta magazynu ZRS zapewniają większą trwałość niż magazyn LRS, ale konta magazynu ZRS nie mają metryk ani funkcji rejestrowania. 

**Magazyn geograficznie nadmiarowy (GRS)**

Magazyn geograficznie nadmiarowy (GRS) przechowuje trzy kopie lokalne powitania danych w regionie podstawowym plus inny zestaw trzy kopie danych w regionie pomocniczym setki odległości od regionu podstawowego hello. W przypadku hello awaria w regionie podstawowym hello usługi Azure Storage zakończy się niepowodzeniem w regionie pomocniczym toohello. 

**Magazyn geograficznie nadmiarowy dostępny do odczytu (RA-GRS)** 

Dostęp do odczytu magazynu geograficznie nadmiarowego jest dokładnie takie same jak grs w warstwie, z wyjątkiem tego, aby uzyskać dostęp do odczytu toohello danych w dodatkowej lokalizacji hello. Jeśli centrum danych podstawowych hello jest tymczasowo niedostępny, można kontynuować tooread hello danych z lokalizacji dodatkowej hello. Może to być bardzo przydatne. Na przykład można masz aplikacji sieci web, której zmiany w trybie tylko do odczytu i wskazuje toohello pomocniczej kopii, nawet jeśli nie są dostępne aktualizacje, dzięki czemu dostęp. 

> [!IMPORTANT]
> Możesz zmienić sposób replikacji danych po utworzeniu konta magazynu, o ile nie określono ZRS, podczas tworzenia konta hello. Jednak należy pamiętać, że może pociągnąć za sobą dodatkowe jednorazowo koszty transferu danych po przełączeniu z LRS tooGRS lub RA-GRS.
>

Aby uzyskać więcej informacji na temat replikacji, zobacz [Replikacja usługi Azure Storage](storage-redundancy.md).

Aby uzyskać informacje odzyskiwania po awarii, zobacz [jakie toodo w przypadku wystąpienia awarii usługi Azure Storage](storage-disaster-recovery-guidance.md).

Na przykład jak tooleverage RA-GRS tooensure wysoka dostępność magazynu, zobacz [projektowania wysokiej dostępności aplikacji przy użyciu RA-GRS](storage-designing-ha-apps-with-ragrs.md).

## <a name="transferring-data-tooand-from-azure-storage"></a>Transfer danych tooand z usługi Azure Storage

Używając blob toocopy narzędzia wiersza polecenia AzCopy hello oraz danych plików w ramach konta magazynu lub wielu kont magazynu. Zobacz jedną z następujących hello artykuły pomocy:

* [Transferowanie danych za pomocą narzędzia AzCopy dla systemu Windows](storage-use-azcopy.md)
* [Transferowanie danych za pomocą narzędzia AzCopy dla systemu Linux](storage-use-azcopy-linux.md)

Narzędzie AzCopy jest oparty na powitania [Biblioteka przenoszenia danych Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), która jest aktualnie dostępna w wersji zapoznawczej.

Witaj usługi Import/Eksport Azure mogą być używane tooimport lub eksportu dużych ilości tooor danych obiektów blob z konta magazynu. Przygotowanie i poczty wielu dysków twardych tooan centrum danych Azure, gdzie zostaną przeniesione hello danych z dysków twardych hello i wysłanie tooyou kopii hello dysków twardych. Aby uzyskać więcej informacji na temat hello usługi Import/eksport, zobacz [Użyj hello usługi Import/Eksport Microsoft Azure tooTransfer danych tooBlob magazynu](../storage-import-export-service.md).

## <a name="pricing"></a>Cennik

Aby uzyskać szczegółowe informacje na temat cen usługi Azure Storage, zobacz hello [strony cennik](https://azure.microsoft.com/pricing/details/storage/blobs/).

## <a name="storage-apis-libraries-and-tools"></a>Narzędzia, biblioteki oraz interfejsy API usługi Storage
Zasoby usługi Azure Storage są dostępne za pomocą dowolnego języka, który obsługuje żądania HTTP/HTTPS. Dodatkowo Magazyn Azure oferuje biblioteki programistyczne dla kilku popularnych języków. Te biblioteki upraszczają wiele aspektów pracy z usługą Azure Storage dzięki obsłudze szczegółów, takich jak wywołania synchroniczne i asynchroniczne, przetwarzanie wsadowe operacji, zarządzanie wyjątkami, automatyczne ponawianie, zachowania podczas działania itd. Biblioteki są obecnie dostępne dla następujących języków hello i platform, a kolejne hello potoku:

### <a name="azure-storage-data-services"></a>Usługi danych usługi Azure Storage
* [Interfejs API REST usług Storage](/rest/api/storageservices/)
* [Biblioteka klienta usługi Storage dla platformy .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Biblioteka klienta usługi Storage dla języka C++](https://github.com/Azure/azure-storage-cpp)
* [Biblioteka klienta usługi Storage dla języka Java w systemie Android](https://azure.microsoft.com/develop/java/)
* [Biblioteka klienta usługi Storage dla oprogramowania Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Biblioteka klienta usługi Storage dla języka PHP](https://azure.microsoft.com/develop/php/)
* [Biblioteka klienta usługi Storage dla języka Python](https://azure.microsoft.com/develop/python/)
* [Biblioteka klienta usługi Storage dla języka Ruby](https://azure.microsoft.com/develop/ruby/)
* [Polecenia cmdlet usługi Storage dla programu PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [Polecenia usługi Storage dla interfejsu wiersza polecenia 2.0](/cli/azure/storage)

## <a name="next-steps"></a>Następne kroki

* [Dowiedz się więcej o usłudze Blob Storage](../blobs/storage-blobs-introduction.md)
* [Dowiedz się więcej o usłudze File Storage](../storage-files-introduction.md)
* [Dowiedz się więcej o usłudze Queue Storage](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Dla administratorów
* [Używanie programu Azure PowerShell z usługą Azure Storage](storage-powershell-guide-full.md)
* [Używanie interfejsu wiersza polecenia platformy Azure z usługą Azure Storage](../storage-azure-cli.md)

### <a name="for-net-developers"></a>Dla deweloperów .NET
* [Rozpoczynanie pracy z usługą Azure Blob Storage przy użyciu platformy .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Rozpoczynanie pracy z usługą Azure Table Storage przy użyciu platformy .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Rozpoczynanie pracy z usługą Azure Queue Storage przy użyciu platformy .NET](../storage-dotnet-how-to-use-queues.md)
* [Rozpoczynanie pracy z usługą Azure File Storage w systemie Windows](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Dla deweloperów języka Java w systemie Android
* [Jak toouse magazynu obiektów Blob w języku Java](../blobs/storage-java-how-to-use-blob-storage.md)
* [Jak toouse magazynu tabel w języku Java](../../cosmos-db/table-storage-how-to-use-java.md)
* [Jak toouse magazynu kolejek w języku Java](../storage-java-how-to-use-queue-storage.md)
* [Jak toouse magazyn plików za pomocą języka Java](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Dla deweloperów oprogramowania Node.js
* [Jak toouse magazynu obiektów Blob w oprogramowaniu Node.js](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Jak toouse magazynu tabel w oprogramowaniu Node.js](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [Jak toouse magazynu kolejek w oprogramowaniu Node.js](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Dla deweloperów języka PHP
* [Jak toouse magazynu obiektów Blob w języku PHP](../blobs/storage-php-how-to-use-blobs.md)
* [Jak toouse magazynu tabel w języku PHP](../../cosmos-db/table-storage-how-to-use-php.md)
* [Jak toouse magazynu kolejek w języku PHP](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Dla deweloperów języka Ruby
* [Jak toouse magazynu obiektów Blob w języku Ruby](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [Jak toouse magazynu tabel w języku Ruby](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [Jak toouse magazynu kolejek w języku Ruby](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Dla deweloperów języka Python
* [Jak toouse magazynu obiektów Blob w języku Python](../blobs/storage-python-how-to-use-blob-storage.md)
* [Jak toouse magazynu tabel w języku Python](../../cosmos-db/table-storage-how-to-use-python.md)
* [Jak toouse magazynu kolejek w języku Python](../storage-python-how-to-use-queue-storage.md)   
* [Jak toouse magazynu plików w języku Python](../storage-python-how-to-use-file-storage.md) 
-->