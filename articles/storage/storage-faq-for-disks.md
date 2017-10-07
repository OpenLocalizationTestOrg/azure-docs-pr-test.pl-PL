---
title: "Dyski maszyn wirtualnych IaaS platformy Azure — często zadawane pytania (FAQ) | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące dysków maszyny Wirtualnej Azure IaaS i dysków w warstwie premium (zarządzanych i niezarządzanych)"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a>Często zadawane pytania dotyczące dyski maszyny Wirtualnej Azure IaaS i zarządzane i niezarządzane — wersja premium

Ten artykuł zawiera odpowiedzi na niektóre często zadawane pytania dotyczące dysków zarządzanych Azure i usługa Azure Premium Storage.

## <a name="managed-disks"></a>Managed Disks

**Co to jest Azure zarządzane dyski?**

Dyski zarządzane jest funkcja, która ułatwia zarządzanie dyskami dla maszyn wirtualnych IaaS platformy Azure dzięki obsłudze Zarządzanie kontem magazynu dla Ciebie. Aby uzyskać więcej informacji, zobacz hello [omówienie dysków zarządzanych](storage-managed-disks-overview.md).

**Jeśli utworzyć standardowych dysków zarządzanych z istniejącego dysku VHD, 80 GB, ile będzie tego koszt mnie?**

Standardowa dysków zarządzanych utworzone na podstawie wirtualny dysk twardy 80 GB jest traktowany jako dalej rozmiaru dysku standardowe hello, który jest dyskiem s10 w warstwie. Są naliczane opłaty zgodnie z toohello s10 w warstwie dysków cennik. Aby uzyskać więcej informacji, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/storage).

**Czy istnieją kosztów transakcji dla standardowych dysków zarządzanych?**

Tak. W przypadku naliczona opłata za każdą transakcję. Aby uzyskać więcej informacji, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/storage).

**Dla standardowych dysków zarządzanych I obciążymy hello rzeczywisty rozmiar hello danych na dysku hello lub hello elastycznie pojemność dysku hello?**

Są naliczane opłaty oparte na powitania elastycznie pojemność dysku hello. Aby uzyskać więcej informacji, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/storage).

**Jak jest inny niż dyski niezarządzane cennik dysków zarządzanych w warstwie premium?**

jak w przypadku dysków premium niezarządzanym jest hello Hello cennik dysków zarządzanych w warstwie premium.

**Czy można zmienić hello typu konta magazynu (standardowa lub Premium) z dysków zarządzanych?**

Tak. Można zmienić typu konta magazynu hello dysków zarządzanych za pomocą hello portalu Azure, programu PowerShell lub hello wiersza polecenia platformy Azure.

**Czy istnieje sposób, aby I skopiuj lub wyeksportować konta magazynu prywatnego tooa dysków zarządzanych w?**

Tak. Dyski zarządzane można wyeksportować za pomocą hello portalu Azure, programu PowerShell lub hello wiersza polecenia platformy Azure.

**Czy można użyć pliku wirtualnego dysku twardego w toocreate konta magazynu Azure dysków zarządzanych z innej subskrypcji?**

Nie.

**Czy można użyć pliku wirtualnego dysku twardego w toocreate konta magazynu Azure dysków zarządzanych w innym regionie?**

Nie.

**Czy istnieją jakiekolwiek ograniczenia skali dla klientów korzystających z zarządzanego dyski?**

Dyski zarządzane eliminuje limity hello skojarzonego z kontami magazynu. Hello liczby zarządzanych dysków dla subskrypcji jest jednak ograniczona too2, 000 domyślnie. Obsługa tooincrease można wywołać ten numer.

**Czy można wykonać przyrostowej migawki dysków zarządzanych?**

Nie. Bieżąca funkcja migawki Hello sprawia, że pełna kopia dysków zarządzanych. Jednak firma Microsoft są planowania toosupport przyrostowe migawki w przyszłości hello.

**Maszyny wirtualne w zestawie dostępności może zawierać kombinację dysków zarządzane i niezarządzane?**

Nie. Hello maszyn wirtualnych w zestawie dostępności muszą używać wszystkich zarządzanych dysków lub wszystkie dyski niezarządzane. Podczas tworzenia zestawu dostępności można wybrać typu dyski mają toouse.

**Jest opcja domyślna hello dysków zarządzanych w portalu Azure hello?**

Aktualnie nie ale będzie gotowa do domyślnego hello w przyszłości hello.

**Można utworzyć pusty dysk zarządzany?**

Tak. Możesz utworzyć pusty dysk. Dysk zarządzany można tworzyć niezależnie od maszyny Wirtualnej, na przykład bez podłączany tooa maszyny Wirtualnej.

**Co to jest liczba domen błędów hello obsługiwane dla zestawu dostępności używającym dysków zarządzanych?**

W zależności od hello regionu, w którym znajduje się zestaw dostępności hello, który używa dysków zarządzanych liczba domen błędów hello obsługiwane jest 2 lub 3.

**W jaki sposób hello konta standard storage dla diagnostyki Konfigurowanie?**

Skonfiguruj konto magazynu prywatne dla diagnostyki maszyny Wirtualnej. W przyszłości hello, planujemy diagnostyki tooswitch również tooManaged dysków.

**Jakiego rodzaju obsługi kontroli dostępu opartej na rolach jest dostępna dla dysków zarządzanych?**

Zarządzane dysków obsługuje trzy kluczowe domyślne role:

* Właściciel: Mogą zarządzać wszystkim łącznie z dostępem
* Współautor: Mogą zarządzać wszystkim poza dostępem
* Czytnik: Można przeglądać wszystko, ale nie można wprowadzić zmian

**Czy istnieje sposób, aby I skopiuj lub wyeksportować konta magazynu prywatnego tooa dysków zarządzanych w?**

Możesz uzyskać sygnatury dostępu współdzielonego tylko do odczytu identyfikator URI dla hello zarządzane na dysku i korzystać z niego toocopy hello zawartość tooa prywatnego składowania konta lub lokalnego magazynu.

**Można utworzyć kopię dysku zarządzanego?**

Klienci mogą migawki dysków zarządzanych, a następnie użyj toocreate migawki hello dysków zarządzanych w innym.

**Niezarządzane dyski nadal są obsługiwane?**

Tak. Firma Microsoft obsługuje dyski niezarządzane i zarządzane. Zalecamy dysków zarządzanych dla nowych obciążeń, a następnie migracji dysków toomanaged bieżącego obciążenia.


**Jeśli. Utwórz dysk 128 GB i dopiero potem zwiększyć jej hello rozmiar too130 GB, będzie I naliczona opłata za hello dalej rozmiar dysku (512 GB)?**

Tak.

**Magazyn lokalnie nadmiarowy, Magazyn geograficznie nadmiarowy, można utworzyć i dyskach zarządzanych przez Magazyn strefowo nadmiarowy?**

Dyskach zarządzanych platformy Azure obsługuje obecnie tylko lokalnie nadmiarowego magazynu zarządzane dyski.

**Można zmniejszyć lub downsize dysków zarządzanych?**

Nie. Ta funkcja nie jest obecnie obsługiwana. 

**Właściwość Nazwa komputera hello można zmienić, gdy specjalistycznej (nie utworzone przy użyciu narzędzia przygotowywania systemu hello lub uogólniony) dysku systemu operacyjnego jest używany tooprovision maszyny Wirtualnej?**

Nie. Nie można zaktualizować właściwości Nazwa komputera hello. Hello nowej maszyny Wirtualnej dziedziczy on hello nadrzędna maszyna wirtualna, będącą dysku systemu operacyjnego hello toocreate używane. 

**Gdzie można znaleźć przykładowe usługi Azure Resource Manager toocreate szablony maszyn wirtualnych z dyskami zarządzanych**
* [Lista szablonów przy użyciu dysków zarządzanych](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* https://github.com/chagarw/MDPP

## <a name="managed-disks-and-storage-service-encryption"></a>Zarządzane dysków i szyfrowanie usługi magazynu 

**Jest szyfrowanie usługi Magazyn Azure domyślnie podczas tworzenia dysków zarządzanych?**

Tak.

**Kto zarządza hello klucze szyfrowania?**

Firma Microsoft zarządza hello kluczy szyfrowania.

**Do zarządzanych dysków można wyłączyć szyfrowanie usługi Magazyn?**

Nie.

**Jest szyfrowanie usługi Magazyn dostępna tylko w określonych regionach?**

Nie. Jest dostępna we wszystkich regionach hello, gdzie dostępna jest opcja dysków zarządzanych. Dyski zarządzane jest dostępna we wszystkich regionach publicznego i Niemczech.

**Jak można sprawdzić w przypadku zarządzanych dysku są szyfrowane?**

Można ustalić hello godzina utworzenia dysków zarządzanych z hello portalu Azure, hello wiersza polecenia platformy Azure i programu PowerShell. Jeśli godzina powitania po 9 czerwca 2017 dysku są szyfrowane. 

**Jak można zaszyfrować Moje istniejących dysków, które zostały utworzone przed 10 czerwca 2017 r.**

Począwszy od 10 czerwca 2017 nowych danych tooexisting zarządzane dysków jest szyfrowane automatycznie. Firma Microsoft są także planowania tooencrypt istniejących danych i szyfrowania hello nastąpi asynchronicznie w tle hello. Jeśli musi teraz zaszyfrować dane, należy utworzyć kopię dysku. Nowe dyski zostaną zaszyfrowane.

* [Kopiowanie dysków zarządzanych za pomocą hello wiersza polecenia platformy Azure](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [Kopiowanie dysków zarządzanych za pomocą programu PowerShell](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

**Są zarządzane migawki i obrazy szyfrowane?**

Tak. Wszystkie zarządzane migawki i obrazy utworzone po 9 czerwca 2017 r są szyfrowane automatycznie. 

**Z niezarządzanego dysków, które znajdują się na kontach magazynu, które są lub toomanaged wcześniej zaszyfrowanych dysków można przekonwertować maszyny wirtualne?**

Tak

**Wyeksportowane wirtualnego dysku twardego z zarządzanego dysku lub migawka także będą zaszyfrowane?**

Nie. Jeśli możesz wyeksportować tooan wirtualnego dysku twardego, ale szyfrowane konta magazynu z zaszyfrowanych dysków zarządzanych lub migawki, a następnie jest on zaszyfrowany. 

## <a name="premium-disks-managed-and-unmanaged"></a>Dyski Premium: zarządzanych i niezarządzanych

**Jeśli maszyna wirtualna używa rozmiar serii, która obsługuje magazyn w warstwie Premium, takich jak DSv2, można dołączyć zarówno premium i dyski standardowe danych?** 

Tak.

**Czy mogę dołączyć zarówno premium i standardowa danych dysków tooa rozmiar serii, która nie obsługuje usługi Premium Storage, takich jak seria D, Dv2, G lub F?**

Nie. Można dołączać tylko tooVMs dyski standardowe danych, który nie należy używać serii rozmiar, który obsługuje magazyn w warstwie Premium.

**Jeśli dysk danych — warstwa premium można utworzyć z istniejącego dysku VHD, który był 80 GB, ile będzie tego koszt?**

Dysk z danymi premium utworzone na podstawie wirtualny dysk twardy 80 GB jest traktowany jako rozmiar dysku dostępny dalej premium hello, który jest dyskiem P10. Jest naliczane opłaty zgodnie z toohello P10 dysku cennik.

**Czy istnieją toouse kosztów transakcji magazynu Premium?**

Brak koszt stały rozmiar każdego dysku, które pojawia się z określonym limity udostępnionym IOPS i przepustowość. Witaj innych kosztów są przepustowości wychodzącej i pojemności migawki, jeśli ma to zastosowanie. Aby uzyskać więcej informacji, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/storage).

**Jakie są limity hello IOPS i przepływność, którą można pobrać z pamięci podręcznej dysku hello?**

Witaj łączne limity dla pamięci podręcznej i lokalny dysk SSD dla serii DS są 4000 IOPS na podstawowe i 33 MB na sekundę na podstawowe. Witaj serii GS oferuje 5000 IOPS na podstawowe i 50 MB na sekundę na podstawowe.

**To jest hello obsługiwany przez lokalny dysk SSD dla maszyny Wirtualnej, zarządzane dyski?**

Witaj lokalny dysk SSD jest tymczasowego magazynu, który jest dołączony do maszyny Wirtualnej dysków zarządzanych. Jest nie żadnymi dodatkowymi kosztami dla tego magazynu tymczasowego. Firma Microsoft zaleca, aby używać tego toostore lokalnych dysków SSD dane aplikacji, ponieważ nie jest on utrwalane w magazynie obiektów Blob platformy Azure.

**Są dostępne wszelkie następstwa dla hello używać TRIM na dysków w warstwie premium?**

Nie jest używana toohello wadą interfejsu TRIM na dyskach platformy Azure w warstwie premium albo lub dyski standardowe.

## <a name="new-disk-sizes-managed-and-unmanaged"></a>Nowy rozmiar dysku: zarządzanych i niezarządzanych

**Co to jest hello największy rozmiar dysku systemu operacyjnego i dysków z danymi obsługiwane?**

Typ partycji Hello Azure obsługuje dla dysku systemu operacyjnego jest hello główny rekord rozruchowy (MBR). Hello MBR format obsługuje rozmiaru dysku too2 TB. Witaj największy rozmiar, który Azure obsługuje dla dysku systemu operacyjnego jest 2 TB. Azure obsługuje too4 TB dla dysków z danymi. 

**Co to jest hello największy blob rozmiar strony jest obsługiwana?**

Hello największy strony rozmiar obiektu blob Azure obsługującym jest 8 TB (8191 GB). Nie obsługujemy stronicowe obiekty BLOB większych niż 4 TB (4,095 GB) dołączona tooa maszyny Wirtualnej jako dane lub dysków systemu operacyjnego.

**Należy toouse nowej wersji z toocreate narzędzi platformy Azure, Dołącz, zmienianie rozmiaru i przekazać dysków większych niż 1 TB?**

Nie ma potrzeby tooupgrade Twojego istniejących toocreate narzędzia Azure, Dołącz lub zmieniać rozmiar dysków większych niż 1 TB. tooupload dysk VHD plik z lokalnymi bezpośrednio tooAzure jako stronicowy obiekt blob lub niezarządzane dysku, należy toouse hello najnowsze narzędzia zestawów:

|Narzędzia platformy Azure      | Obsługiwane wersje                                |
|-----------------|---------------------------------------------------|
|Azure PowerShell | Numer wersji 4.1.0: czerwiec 2017 wersji lub nowszy|
|Interfejs wiersza polecenia platformy Azure w wersji 1     | Numer wersji 0.10.13: 2017 może zwolnić lub nowszy|
|Narzędzie AzCopy           | Numer wersji 6.1.0: czerwiec 2017 wersji lub nowszy|

Witaj obsługę wiersza polecenia platformy Azure w wersji 2 i Eksploratora usługi Storage platformy Azure będzie dostępna wkrótce. 

**P4 i P6 rozmiary dysków są obsługiwane dla niezarządzanego dysków lub stronicowych obiektów blob?**

Nie. P4 (32 GB) i P6 rozmiary dysków (64 GB) są obsługiwane tylko w przypadku dysków zarządzanych. Obsługa dysków niezarządzane i stronicowe obiekty BLOB będzie dostępna wkrótce.

**Jeśli Mój istniejący premium zarządzane na dysku z mniej niż 64 GB został utworzony przed włączeniem hello małego dysku (około 15 czerwca 2017 r), jak jest on rozliczany?**

Istniejące dyski premium małych mniej niż 64 GB nadal toobe rozliczane zgodnie z toohello P10 warstwę cenową. 

**Jak można zmienić warstwy dysku hello dyski premium małych mniejsze niż 64 GB P10 tooP4 lub P6?**

Można utworzyć migawkę małe dyski, a następnie utworzyć dysku hello przełącznika tooautomatically tooP4 warstwy cenowej lub P6 na podstawie hello elastycznie rozmiaru. 


## <a name="what-if-my-question-isnt-answered-here"></a>Co zrobić, jeśli mojego pytania nie ma odpowiedzi w tym miejscu?

Jeśli Twoje pytanie nie ma na liście w tym miejscu, Daj nam znać, a pomożemy Ci znaleźć odpowiedź. W komentarzach hello można Zadaj pytanie na końcu hello w tym artykule. tooengage z zespołem usługi Azure Storage hello i innymi członkami społeczności informacje w tym artykule, należy użyć hello MSDN [forum usługi Azure Storage](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).

Funkcje toorequest przesłać toohello Twojego żądania i pomysły [forum opinii usługi Azure Storage](https://feedback.azure.com/forums/217298-storage).
