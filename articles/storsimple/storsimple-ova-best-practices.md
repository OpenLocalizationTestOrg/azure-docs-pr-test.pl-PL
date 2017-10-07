---
title: "aaaBest wskazówki dotyczące tablicy wirtualnego StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello najlepsze rozwiązania dotyczące wdrażania i zarządzania nimi hello tablicy wirtualne StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 57ac6eeb-c47c-442d-a5f4-b360d81a76a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2017
ms.author: alkohli
ms.openlocfilehash: f242364365e07f86b78e2f9bb2acfb3aa98e83e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-best-practices"></a>Najlepsze rozwiązania w zakresie tablicy wirtualnego StorSimple
## <a name="overview"></a>Omówienie
Microsoft Azure StorSimple wirtualnego tablicy to rozwiązanie zintegrowanego magazynu zarządzanego zadań magazynu między lokalnymi urządzenia wirtualnego działający w funkcji hypervisor i magazynu w chmurze Microsoft Azure. Tablica wirtualne StorSimple jest tablicą fizycznych serii wydajne i ekonomiczne toohello alternatywnych 8000. Hello wirtualnego tablicy można uruchomić w istniejącej infrastrukturze funkcji hypervisor, obsługuje zarówno hello iSCSI i protokoły SMB hello i dobrze nadaje się do scenariuszach dotyczących biura zdalnego/oddział. Aby uzyskać więcej informacji na temat rozwiązań StorSimple hello Przejdź zbyt[Przegląd usługi Microsoft Azure StorSimple](https://www.microsoft.com/en-us/server-cloud/products/storsimple/overview.aspx).

W tym artykule omówiono hello najlepsze rozwiązania w zakresie zaimplementowana podczas początkowej konfiguracji hello, wdrażania i zarządzania hello tablicy wirtualne StorSimple. Następujące najlepsze rozwiązania zamieszczono wytyczne zweryfikowanych hello Konfiguracja i zarządzanie macierzy wirtualnego. W tym artykule jest przeznaczona kierunku hello IT administratorów, którzy wdrażania i zarządzania nimi hello tablice wirtualnych w swoich centrach danych.

Zalecamy okresowe analizy hello najlepszych praktyk toohelp upewnij się, że urządzenie jest nadal zgodności podczas wprowadzania zmian konfiguracji toohello lub operacji przepływu. Należy wystąpią problemy podczas implementowania następujące najlepsze rozwiązania w sieci wirtualnej macierzy [skontaktuj się z Microsoft Support](storsimple-virtual-array-log-support-ticket.md) Aby uzyskać pomoc.

## <a name="configuration-best-practices"></a>Najlepsze rozwiązania w zakresie konfiguracji
Następujące najlepsze rozwiązania obejmują hello wskazówki, które wymagają toobe zostały wykonane podczas początkowej konfiguracji hello i wdrażania wirtualnego tablic hello. Następujące najlepsze rozwiązania obejmują tych pokrewne toohello udostępniania hello maszyny wirtualnej, ustawienia zasad grupy, zmienianie rozmiaru, konfigurowanie hello sieci, konfigurowania kont magazynu i tworzenie udziałów i woluminów na potrzeby hello wirtualnego tablicy. 

### <a name="provisioning"></a>Inicjowanie obsługi
Tablica wirtualne StorSimple jest maszynę wirtualną (VM) udostępniane na powitania hypervisor (Hyper-V lub programu VMware) serwera hosta. Podczas inicjowania obsługi administracyjnej hello maszyny wirtualnej, upewnij się, że host jest możliwe toodedicate wystarczające zasoby. Aby uzyskać więcej informacji, przejdź zbyt[minimalnych wymagań dotyczących zasobów](storsimple-virtual-array-deploy2-provision-hyperv.md#step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements) tooprovision tablicy.

Implementowanie hello następujące najlepsze rozwiązania w zakresie podczas inicjowania obsługi administracyjnej hello wirtualnego tablicy:

|  | Funkcja Hyper-V | VMware |
| --- | --- | --- |
| **Typ maszyny wirtualnej** |**Generacja 2** maszyny Wirtualnej do użytku z systemem Windows Server 2012 lub nowszym i *vhdx* obrazu. <br></br> **Generacja 1** maszyny Wirtualnej do użytku z systemem Windows Server 2008 lub nowszym i *VHD* obrazu. |Użyj maszyn wirtualnych w wersji 8-11, jeśli korzystasz z *.vmdk* obrazu. |
| **Typ pamięci** |Należy skonfigurować jako **pamięci statycznej**. <br></br> Nie używaj hello **pamięci dynamicznej** opcji. | |
| **Typ dysku danych** |Ustanowić jako **dynamicznie powiększających się**.<br></br> **Stały rozmiar** zajmuje dużo czasu. <br></br> Nie używaj hello **różnicowych** opcji. |Użyj hello **elastycznej udostępniania** opcji. |
| **Modyfikowanie dysku danych** |Rozszerzenie lub zmniejszanie jest niedozwolone. Próba toodo tak powoduje utratę hello wszystkie dane lokalne powitania na urządzeniu. |Rozszerzenie lub zmniejszanie jest niedozwolone. Próba toodo tak powoduje utratę hello wszystkie dane lokalne powitania na urządzeniu. |

### <a name="sizing"></a>Zmiana rozmiaru
Podczas zmiany rozmiaru wirtualnych tablica StorSimple, należy wziąć pod uwagę następujące czynniki hello:

* Lokalne rezerwacji woluminy lub udziały. Około 12% miejsca hello jest zarezerwowana w warstwie lokalne powitania dla każdego woluminu warstwowego elastycznie lub udziału. Około 10% miejsca hello również jest zarezerwowana dla woluminu przypiętego lokalnie systemu plików.
* Narzut migawki. Około 15% miejsca na warstwie lokalnej hello jest zarezerwowana dla migawki.
* Potrzebę operacji przywracania. Jeśli podczas przywracania jako nową operację, potrzebne do przywrócenia miejsce hello należy uwzględnić zmiany rozmiaru. Przywracania odbywa się tooa udziału lub wolumin hello sam rozmiar.
* Niektóre buforu powinna zostać przydzielona dla dowolnego nieoczekiwany wzrostu.

Oparte na powitania poprzedzających czynników, hello zmiany rozmiaru wymagań może być reprezentowany przez hello następujące równanie:

`Total usable local disk size = (Total provisioned locally pinned volume/share size including space for file system) + (Max (local reservation for a volume/share) for all tiered volumes/share) + (Local reservation for all tiered volumes/shares)`

`Data disk size = Total usable local disk size + Snapshot overhead + buffer for unexpected growth or new share or volume`

Witaj poniższe przykłady przedstawiają rozmiaru wirtualnego tablicy, w zależności od wymagań.

#### <a name="example-1"></a>Przykład 1:
W sieci wirtualnej macierzy mają toobe stanie

* Zapewnij 2 TB warstwowych woluminu lub udziału.
* Zapewnij 1 TB warstwowych woluminu lub udziału.
* Zapewnij 300 GB miejsca woluminu przypiętego lokalnie lub udziału.

Dla hello poprzedniego woluminy lub udziały, NAS obliczyć hello wymagania dotyczące miejsca na warstwie lokalne powitania.

Najpierw dla każdego warstwowych woluminu i udostępniania, rezerwacji lokalne będą too12 równy % rozmiaru woluminu i udostępniania hello. Wolumin przypięty lokalnie hello/udziału lokalne rezerwacji jest 10% lokalne powitania przypięty rozmiar woluminu i udostępniania (oprócz toohello elastycznie rozmiar). W tym przykładzie należy

* Zastrzeżenie lokalnego 240 GB (dla 2 TB warstwowa woluminu i udostępniania)
* Zastrzeżenie lokalnego 120 GB (dla 1 TB warstwowa woluminu i udostępniania)
* 330 GB dla woluminu przypiętego lokalnie lub w udziale (Dodawanie 10% rozmiaru 300 GB elastycznie toohello rezerwacji lokalnych)

Witaj wymagane w warstwie lokalne powitania wykonanej do tej pory całkowita ilość miejsca jest: 240 GB + 120 GB + 330 GB = 690 GB.

Po drugie potrzebujemy co najmniej tyle miejsca w warstwie lokalne powitania jako hello największy rezerwacji pojedynczego. Kwota dodatkowa ta jest używana w razie potrzeby toorestore z migawka w chmurze. W tym przykładzie największy rezerwacji lokalne powitania jest 330 GB (w tym zastrzeżenie dotyczące systemu plików), dlatego należy dodać ten toohello 690 GB: 690 GB + 330 GB = 1020 GB.
Jeśli wykonane kolejne dodatkowe operacji przywracania, możemy zawsze zwolnić miejsce hello z hello poprzedniej operacji przywracania.

Trzecie, potrzebujemy 15% całkowitej lokalne miejsce do tej pory toostore migawki lokalne, tak aby była dostępna tylko 85%. W tym przykładzie, który będzie wokół 1020 GB = 0.85&ast;elastycznie danych na dysku TB. Tak, będzie dysk danych elastycznie hello (1020&ast;(1/0.85)) = 1200 GB = 1,20 TB ~ 1,25 TB (zaokrąglania kwartyl toonearest)

Factoring w nieoczekiwany wzrostu i przywraca nowe, należy udostępnić dysku lokalnym wokół 1,25-1,5 TB.

> [!NOTE]
> Zaleca się również, że tego dysku lokalnego hello jest alokowany elastycznie. To zalecenie wynika hello przywracania tylko miejsca można toorestore danych, która jest starsza niż pięć dni. Odzyskiwanie na poziomie elementu pozwala toorestore dane hello ostatnich pięciu dni bez konieczności hello dodatkowe miejsce do przywrócenia.


#### <a name="example-2"></a>Przykład 2:
W sieci wirtualnej macierzy mają toobe stanie

* Zapewnij 2 TB wolumin warstwowy
* Obsługiwanie woluminu 300 GB przypięty lokalnie

W oparciu o 12% rezerwacji lokalne miejsce w przypadku woluminów warstwowych/udziałów i 10% dla woluminów przypiętych lokalnie/udziałów, potrzebujemy

* Zastrzeżenie lokalnego 240 GB (dla 2 TB warstwowa woluminu i udostępniania)
* 330 GB dla woluminu przypiętego lokalnie lub w udziale (Dodawanie 10% lokalnego rezerwacji toohello 300 GB udostępnione miejsca)

Jest wymagane w warstwie lokalne powitania całkowita ilość miejsca: 240 GB + 330 GB = 570 GB

Witaj minimalna lokalne miejsce potrzebne do odzyskiwania jest 330 GB.

15% całkowitej dysku używane toostore migawek, jest tylko 0.85 jest dostępna. Dlatego rozmiar dysku hello jest (900&ast;(1/0.85)) = 1.06 TB ~ 1,25 TB (zaokrąglania kwartyl toonearest)

Factoring wszelkie nieoczekiwane wzrostu, można udostępnić dysk lokalny 1,25-1,5 TB.

### <a name="group-policy"></a>Zasady grupy
Zasady grupy to infrastruktura umożliwiająca tooimplement konfiguracji określonych dla użytkowników i komputerów. Ustawienia zasad grupy są zawarte w obiektach zasad grupy (GPO), które są połączone toohello następujących kontenerów usług domenowych w usłudze Active Directory (AD DS): lokacje, domeny i jednostki organizacyjne (OU). 

Jeśli tablica wirtualnego jest przyłączony do domeny, obiektów zasad grupy można tooit zastosowane. Te obiekty zasad grupy można zainstalować aplikacje, takie jak oprogramowanie antywirusowe, które może niekorzystnie wpływać na działanie hello hello tablicy wirtualne StorSimple.

Dlatego zaleca się, że możesz:

* Upewnij się, jest tablica wirtualnego w jego własnej jednostce organizacyjnej (OU) usługi Active Directory.
* Upewnij się, że żadne obiekty zasad grupy (GPO) są zastosowane tooyour wirtualnego tablicy. Możesz zablokować dziedziczenie tooensure, który hello wirtualnego tablicy (węzła podrzędnego) nie automatycznie dziedziczy wszystkie obiekty zasad grupy nadrzędnej hello. Aby uzyskać więcej informacji, przejdź zbyt[zablokować dziedziczenie](https://technet.microsoft.com/library/cc731076.aspx).

### <a name="networking"></a>Sieć
Witaj konfigurację sieci dla wirtualnego tablica odbywa się za pośrednictwem lokalne powitania interfejsu użytkownika sieci web. Interfejs sieci wirtualnej jest włączona za pośrednictwem hello funkcji hypervisor, w którym zostanie zainicjowana hello wirtualnego tablicy. Użyj hello [ustawienia sieciowe](storsimple-virtual-array-deploy3-fs-setup.md) strony adres IP interfejsu sieci wirtualnej hello tooconfigure, podsieci i bramy.  Można również skonfigurować hello podstawowego i pomocniczego serwera DNS, ustawienia czasu i opcjonalne ustawienia serwera proxy dla danego urządzenia. W większości konfiguracji sieciowej hello jest jednorazowej konfiguracji. Przejrzyj hello [StorSimple wymagań sieciowych](storsimple-ova-system-requirements.md#networking-requirements) toodeploying wcześniejsze hello wirtualnego tablicy.

W przypadku wdrażania wirtualnego tablica, firma Microsoft zaleca, należy stosować następujące najlepsze rozwiązania:

* Upewnij się, że ta sieć hello, w których hello tablicy wirtualnych jest wdrażane w zawsze ma hello pojemności toodedicate 5 przepustowości połączenia z Internetem MB/s (lub więcej).
  
  * Konieczność przepustowości Internetu różni się w zależności od właściwości obciążenia, a hello szybkość zmian danych.
  * Hello zmiany danych, które mogą być obsługiwane jest wprost proporcjonalny tooyour przepustowości połączenia z Internetem. Na przykład podczas wykonywania kopii zapasowej 5 MB/s przepustowości może obsłużyć zmiana danych około 18 GB 8 godzin. Cztery razy większe wartości przepustowości (20 MB/s) może obsługiwać cztery razy więcej zmian danych (72 GB).
* Upewnij się, że toohello połączenie internetowe jest zawsze dostępna. Sporadyczne lub zawodnych urządzeń toohello połączenia internetowego może doprowadzić do utraty toodata dostęp w chmurze hello i może skutkować nieobsługiwaną konfiguracją.
* Jeśli planujesz toodeploy urządzenia iSCSI na serwerze:
  
  * Firma Microsoft zaleca, aby wyłączyć hello **uzyskać adres IP automatycznie** opcji (DHCP).
  * Skonfiguruj statyczne adresy IP. Należy skonfigurować podstawowy i pomocniczy serwer DNS.
  * Jeśli definiowane wiele interfejsów sieciowych w sieci wirtualnej macierzy, hello tylko pierwszy interfejsu sieciowego (domyślnie ten interfejs jest **Ethernet**) może nawiązać połączenie hello chmury. Typ hello toocontrol ruchu, można tworzyć wiele interfejsów sieci wirtualnej na wirtualny tablica (skonfigurowany jako serwer iSCSI) i łączących te podsieci toodifferent interfejsów.
* przepustowość chmury hello toothrottle tylko (wykorzystywane przez hello tablicy wirtualnego), skonfigurować ograniczenie na powitania routera lub hello zapory. W przypadku definiowania ograniczania przepustowości w Twojej funkcji hypervisor, zostanie ograniczenie przepustowości wszystkie protokoły hello tym iSCSI i SMB zamiast tylko przepustowości hello w chmurze.
* Upewnij się, że synchronizacja czasu jest włączona w funkcji hypervisor. Jeśli za pomocą funkcji Hyper-V, należy wybrać wirtualnego tablica hello Menedżera funkcji Hyper-V, należy przejść za**ustawienia &gt; usług integracji**i upewnij się, że hello **synchronizacja czasu** jest zaznaczony.

### <a name="storage-accounts"></a>Konta magazynu
Tablica wirtualnego StorSimple może być skojarzony z kontem magazynu jednego. To konto magazynu może być kontem magazynu automatycznie generowanych, konto w hello subskrypcji tooanother związane z tej samej subskrypcji co usługa hello lub konto magazynu. Aby uzyskać więcej informacji, zobacz temat jak zbyt[Zarządzanie kontami magazynu dla wirtualnego tablica](storsimple-virtual-array-manage-storage-accounts.md).

Użyj hello następujące zalecenia dotyczące konta magazynu skojarzone z sieci wirtualnej tablicy.

* Podczas łączenia wielu wirtualnych tablic z kontem magazynu pojedynczego, współczynnik hello maksymalnej pojemności (64 TB) dla tablicy wirtualnego i hello maksymalny rozmiar (500 TB) dla konta magazynu. To ogranicza liczbę hello w pełnym rozmiarze tablice wirtualnych, które mogą być skojarzone z tym tooabout konta magazynu 7.
* Podczas tworzenia nowego konta magazynu
  
  * Zaleca się utworzenie w hello region najbliższy toohello pakietu office/oddziału zdalnego tablica wirtualnego StorSimple w przypadku wdrożonej toominimize opóźnienia.
  * Przy tym pamiętać, że nie można przenieść konto magazynu w różnych regionach. Ponadto nie można przenieść usługi różnych subskrypcji.
  * Użyj konta magazynu implementujący nadmiarowość między hello centrami danych. Magazyn geograficznie nadmiarowy (GRS), strefy magazyn geograficznie nadmiarowy (ZRS) i lokalnie nadmiarowego magazynu (LRS) są obsługiwane do użytku z sieci wirtualnej tablicy. Aby uzyskać więcej informacji na powitania różne typy kont magazynu, przejdź zbyt[replikacji usługi Azure storage](../storage/common/storage-redundancy.md).

### <a name="shares-and-volumes"></a>Woluminów i udziałów
Dla macierzy wirtualnego StorSimple można udostępnić udziałów, gdy jest on skonfigurowany jako serwer plików i woluminy, gdy jest skonfigurowany jako serwer iSCSI. Witaj najlepsze rozwiązania dotyczące tworzenia woluminów i udziałów są powiązane typ rozmiar i hello toohello skonfigurowany.

#### <a name="volumeshare-size"></a>Rozmiar woluminu i udostępniania
W sieci wirtualnej tablicy można udostępnić udziałów, gdy jest on skonfigurowany jako serwer plików i woluminy, gdy jest skonfigurowany jako serwer iSCSI. Witaj najlepsze rozwiązania dotyczące tworzenia woluminów i udziałów odnoszą się rozmiar toohello i hello typ skonfigurowany. 

Należy pamiętać hello następujące najlepsze rozwiązania w zakresie podczas inicjowania obsługi administracyjnej udziały lub woluminy na urządzeniu wirtualnym.

* rozmiar względną toohello elastycznie rozmiary pliku Hello warstwowych udziału może wpłynąć na wydajność warstw hello. Praca z dużych plików może spowodować wolne warstwy w poziomie. Podczas pracy z dużymi plikami, zaleca się czy plik największy hello jest mniejszy niż rozmiar udziału hello % 3.
* Maksymalnie 16 woluminów/udziały mogą być tworzone na powitania wirtualnego tablicy. Limity rozmiaru hello hello lokalnie przypięty i woluminy/udziałów do warstwy, zawsze można znaleźć toohello [ogranicza tablicy wirtualnego StorSimple](storsimple-ova-limits.md).
* Podczas tworzenia woluminu czynnikiem hello oczekiwano danych użycia, a także rozwój w przyszłości. Nie można później rozwijać Hello woluminu.
* Po utworzeniu hello woluminu, nie można zmniejszyć rozmiar hello hello woluminu na StorSimple.
* Podczas zapisywania tooa do warstwy woluminu na StorSimple, gdy hello wolumin danych osiągnie określony próg (względną toohello lokalne miejsce zarezerwowane dla woluminu hello), jest ograniczany hello we/wy. Kontynuowanie woluminu toothis toowrite spowalnia hello we/wy znacznie. Chociaż można napisać tooa woluminu ponad jego pojemność elastycznie (Firma Microsoft nie aktywnie zatrzymywać użytkownika hello zapisywaniu poza pojemność hello obsługi administracyjnej) do warstwy, zobacz efektu toohello powiadomień o alertach, który ma oversubscribed. Gdy zostanie wyświetlony hello alert, konieczne jest wykonanie środki zaradcze, takich jak dane woluminu hello delete (wolumin rozwijanie aktualnie nie jest obsługiwane).
* Dla przypadków użycia odzyskiwania po awarii hello liczbę dopuszczalnych udziałów/woluminów jest 16 i hello maksymalną liczbę udziałów/woluminów, które mogą być przetwarzane równolegle jest również 16, hello liczbę udziałów/woluminów nie ma wpływu na RPO i Objective, RTO.

#### <a name="volumeshare-type"></a>Typ woluminu i udostępniania
StorSimple obsługuje dwa typy woluminu i udostępniania, na podstawie użycia hello: lokalnie przypięty i warstwy. Woluminów przypiętych lokalnie/udziały są alokowany nieelastycznie, podczas gdy hello woluminów warstwowych/udziały są alokowane elastycznie. Nie można przekonwertować tootiered woluminu przypiętego lokalnie i udostępniania lub *odwrotnie* raz utworzony.

Firma Microsoft zaleca, aby zaimplementować hello następujące najlepsze rozwiązania w przypadku konfigurowania woluminów StorSimple/udziałów:

* Określ typ woluminu hello oparte na powitania obciążeń mają toodeploy, aby utworzyć wolumin. Użyj woluminów przypiętych lokalnie dla obciążeń, które wymagają lokalnych gwarancji danych (nawet podczas awarii chmury) i które wymagają opóźnienia niski chmury. Po utworzeniu woluminu w sieci wirtualnej macierzy, nie można zmienić hello typ woluminu przypiętego lokalnie tootiered lub *odwrotnie*. Na przykład tworzenie woluminów przypiętych lokalnie, podczas wdrażania obciążeń SQL lub obciążeń hostowania maszyn wirtualnych (VM); Użyj woluminy warstwowe dla obciążeń udziału plików.
* Zaznacz opcję powitania dla rzadziej używanych danych archiwalnych, podczas pracy nad duże rozmiary plików. Większy rozmiar fragmentu deduplikacji 512 KB jest używany, gdy ta opcja jest włączona transferu danych hello tooexpedite toohello chmury.

#### <a name="volume-format"></a>Formatowanie woluminu
Po utworzeniu woluminy StorSimple na serwerze sieci iSCSI, należy tooinitialize, instalacji i format hello woluminów. Ta operacja odbywa się na urządzeniu StorSimple tooyour hosta połączony hello. Następujące najlepsze rozwiązania jest zalecany w przypadku instalowania i formatowanie woluminów na powitania StorSimple hosta.

* Przeprowadź szybkie formatowanie na wszystkich woluminów StorSimple.
* Podczas formatowania woluminu StorSimple, użyj rozmiaru jednostki alokacji (AUS) 64 KB (wartość domyślna to 4 KB). Witaj 64 KB AUS opiera się na testowania wykonywane we własnym zakresie typowych obciążeń StorSimple oraz innych obciążeń.
* Jeśli przy użyciu hello tablicy wirtualnego StorSimple, skonfigurowany jako serwer iSCSI, nie używaj łączony woluminy lub dyski dynamiczne woluminy te lub dyski nie są obsługiwane przez StorSimple.

#### <a name="share-access"></a>Dostęp do udziału
Podczas tworzenia udziałów na serwerze plików wirtualnych tablicy, skorzystaj z następujących wskazówek:

* Podczas tworzenia udziału, Przypisz grupę użytkowników jako administrator udziału zamiast pojedynczego użytkownika.
* Po utworzeniu udziału hello edytując udziałów hello za pomocą Eksploratora Windows, można zarządzać hello uprawnienia systemu plików NTFS.

#### <a name="volume-access"></a>Dostęp do woluminu
Podczas konfigurowania woluminów iSCSI hello tablica wirtualnego StorSimple, jest ważne toocontrol dostępu tam, gdzie jest to konieczne. toodetermine, które serwery hosta można uzyskać dostęp do woluminów, tworzenie i kojarzenie rekordy kontroli dostępu (ACRs) z woluminów StorSimple.

Użyj hello następujące najlepsze rozwiązania w przypadku konfigurowania ACRs woluminów StorSimple:

* Zawsze należy skojarzyć ACR co najmniej jeden z woluminu.

* Podczas przypisywania więcej niż jednego woluminu tooa ACR, upewnij się, hello wolumin nie jest uwidaczniana w taki sposób, w którym jest jednocześnie dostępny przez więcej niż jednego hosta z systemem innym niż w klastrze. Jeśli przypisano wiele woluminów tooa ACRs komunikat ostrzegawczy wyskakującej dla tooreview możesz konfiguracji.

### <a name="data-security-and-encryption"></a>Bezpieczeństwo danych i szyfrowania
Tablica wirtualnego StorSimple ma funkcje zabezpieczeń i szyfrowania danych, które zapewnić poufności hello i integralność danych. Korzystając z tych funkcji, zalecane jest, należy stosować następujące najlepsze rozwiązania: 

* Zdefiniuj szyfrowanie toogenerate klucza AES 256 szyfrowania magazynu w chmurze przed wysłaniem danych hello z toohello chmury wirtualne tablicy. Ten klucz nie jest wymagane, jeśli dane są szyfrowane toobegin z. Witaj klucza może być wygenerowany i były bezpieczne, przy użyciu systemu zarządzania kluczami, takich jak [usługi Azure key vault](../key-vault/key-vault-whatis.md).
* Podczas konfigurowania konta magazynu hello za pomocą usługi Menedżer StorSimple hello, upewnij się, że włączenie toocreate tryb SSL hello bezpiecznego kanału komunikacji sieciowej między urządzenie StorSimple i hello chmury.
* Regenerate hello klucze kont magazynu (uzyskując dostęp do usługi Azure Storage hello) okresowo tooaccount dla dowolnego zmienia tooaccess na podstawie listy hello zmienić administratorów.
* Dane dotyczące wirtualnych tablica jest skompresowany i deduplikowany przed wysłaniem tooAzure. Nie zaleca się przy użyciu usługi roli deduplikacji danych hello na hoście z systemem Windows Server.

## <a name="operational-best-practices"></a>Najlepsze rozwiązanie w zakresie
Witaj operacyjne najlepsze rozwiązania oznaczają wskazówki, które należy wykonać podczas operacji hello wirtualnego tablicy lub hello bieżące zarządzanie. Praktyki te obejmują zarządzanie określonych zadań, takich jak wykonywania kopii zapasowych, przywracania z zestawu kopii zapasowych, wykonywania pracy awaryjnej, dezaktywacja i usuwanie hello tablic, monitorowania użycia systemu i kondycji, i uruchamianie wirusów skanów w sieci wirtualnej macierzy.

### <a name="backups"></a>Tworzenie kopii zapasowych
dane Hello na wirtualnych tablica jest kopii zapasowej toohello chmury na dwa sposoby, domyślnie automatycznego tworzenia codziennej kopii zapasowej hello uruchamiania wszystkich danych z urządzenia po 22:30 lub za pomocą ręcznej kopii zapasowej na żądanie. Domyślnie urządzenia hello automatycznie tworzy codzienne migawki w chmurze wszystkie dane hello znajdującymi się w nim. Aby uzyskać więcej informacji, przejdź zbyt[kopię zapasową tablica wirtualnego StorSimple](storsimple-virtual-array-backup.md).

Witaj częstotliwości i przechowywania skojarzonych z hello domyślnego tworzenia kopii zapasowych nie można zmienić, ale możesz skonfigurować czas hello, w których hello codzienne kopie zapasowe są inicjowane każdego dnia. Podczas konfigurowania czas rozpoczęcia hello hello automatycznego tworzenia kopii zapasowych, zalecamy:

* Harmonogram kopii zapasowych dla poza godzinami szczytu. Czas rozpoczęcia tworzenia kopii zapasowej należy pokrywa się z wielu hostów we/wy.
* Zainicjuj ręczne kopii zapasowej na żądanie podczas planowania tooperform urządzenia trybu failover lub toohello poprzedniego okna konserwacji, tooprotect hello danych w sieci wirtualnej macierzy.

### <a name="restore"></a>Przywracanie
Można przywrócić z kopii zapasowej Ustaw na dwa sposoby: Przywróć tooanother woluminu lub udziału lub odzyskiwanie na poziomie elementu (dostępne tylko dla wirtualnych tablicy, skonfigurowany jako serwer plików). Odzyskiwanie na poziomie elementu umożliwia toodo szczegółowego odzyskiwanie plików i folderów z kopii zapasowej chmury wszystkich udziałów hello hello urządzenia StorSimple. Aby uzyskać więcej informacji, przejdź zbyt[przywrócić z kopii zapasowej](storsimple-virtual-array-clone.md).

Podczas przywracania, należy zachować hello następujące wytyczne pamiętać:

* Tablica wirtualnego StorSimple nie obsługuje przywracania w miejscu. Może to jednak być łatwo osiągnąć przez dwuetapowy proces: zwiększyć ilość miejsca na powitania wirtualnego tablicy, a następnie przywróć tooanother woluminu i udostępniania.
* Podczas przywracania z woluminu lokalnego, należy uwzględnić hello przywracania będzie operacją wymagającą dużo czasu. Jeśli wolumin hello mogą szybko przejść w tryb online, hello danych nadal toobe uwodniony w tle hello.
* pozostaje typ woluminu Hello hello sam podczas procesu przywracania hello. Wolumin warstwowy jest przywracany tooanother warstwowej wolumin i wolumin przypięty lokalnie tooanother woluminu przypiętego lokalnie.
* Podczas próby toorestore wolumin lub udział z zestawu kopii zapasowych, jeśli zadanie przywracania hello zakończy się niepowodzeniem, wolumin docelowy lub udziału nadal można tworzyć w portalu hello. Należy usunąć tego woluminu docelowego nieużywanych, lub udostępnianie w portalu toominimize hello wszystkie przyszłe problemy wynikające z tego elementu.

### <a name="failover-and-disaster-recovery"></a>Tryb failover i odzyskiwanie po awarii
Urządzenia trybu failover umożliwia toomigrate danych z *źródła* urządzenia w hello datacenter tooanother *docelowej* urządzenia znajdujące się w hello tej samej lub innej lokalizacji geograficznej. Witaj urządzenia z trybu failover jest hello wszystkich danych z urządzenia. Podczas pracy w trybie failover hello danych w chmurze dla urządzenia źródłowego hello zmienia toothat własność hello urządzenia docelowego.

W przypadku tablica wirtualnego StorSimple, możesz tylko tryb failover tooanother tablicy wirtualnych zarządzanych przez hello takie same usługi Menedżer StorSimple. Urządzenie serii tooan 8000 pracy awaryjnej lub tablicy zarządzane przez inną usługę Menedżer StorSimple (niż hello jedną dla urządzenia źródłowego hello) nie jest dozwolone. toolearn więcej dotyczących hello trybu failover, przejdź zbyt[wymagania wstępne dotyczące pracy awaryjnej urządzenia hello](storsimple-virtual-array-failover-dr.md).

Podczas wykonywania błędu za pośrednictwem wirtualnej tablica, pamiętać o następujących hello:

* W przypadku planowanego trybu failover jest zalecanym najlepszym rozwiązaniem tootake wszystkie hello woluminów/udziałów w trybie offline przed tooinitiating hello trybu failover. Wykonaj instrukcje dotyczące systemu operacyjnego hello tootake hello woluminów/udziałów w tryb offline na powitania najpierw hosta, a następnie podjęcia tych w trybie offline na urządzeniu wirtualnym.
* Do pliku serwer odzyskiwania awaryjnego (DR) zaleca się przyłączyć się toohello urządzenia docelowego hello tej samej domenie co hello źródła, która hello uprawnienia udziału zostały automatycznie rozwiązane. Tylko hello trybu failover tooa urządzenie hello tej samej domenie jest obsługiwana w tej wersji.
* Po hello DR pomyślnie urządzenia źródłowego hello są automatycznie usuwane. Chociaż hello urządzenie nie jest już dostępna, hello maszyny wirtualnej, która udostępniane w systemie hosta hello nadal korzysta z zasobów. Firma Microsoft zaleca, aby usunąć tę maszynę wirtualną z Twojej tooprevent systemu hosta opłaty od naliczania.
* Należy pamiętać, że nawet jeśli hello trybu failover zakończy się niepowodzeniem, **danych hello jest zawsze bezpieczne w chmurze hello**. Należy wziąć pod uwagę hello następujące trzy scenariusze, w których hello trybu failover nie powiodło się:
  
  * Wystąpił błąd w hello początkowych etapów hello trybu failover, takie jak kiedy odbywać wstępne sprawdzanie hello odzyskiwania po awarii. W takiej sytuacji urządzenia docelowego jest nadal możliwe. Możesz ponowić próbę pracy awaryjnej hello na powitania urządzenia docelowego.
  * Wystąpił błąd podczas procesu rzeczywistej pracy awaryjnej hello. W takim przypadku urządzenie docelowe hello jest oznaczony jako bezużyteczne. Należy udostępnić i skonfigurować innej docelowej tablicy wirtualnej i użyj jej w trybie failover.
  * trybu failover Hello jest kompletna, po którego urządzenia źródłowego hello został usunięty, ale urządzenie docelowe hello ma problemy i nie masz dostępu do żadnych danych. dane Hello jest nadal bezpieczne w chmurze hello i można łatwo pobrać tworzenia innej tablicy wirtualnego, a następnie użyć go jako urządzenie docelowe dla hello odzyskiwania po awarii.

### <a name="deactivate"></a>Dezaktywowanie
Po dezaktywowaniu tablicą wirtualne StorSimple jest sever hello połączenie między urządzeniem hello a hello odpowiedniej usługi Menedżer StorSimple. Dezaktywacja jest **stałe** operacji i nie można cofnąć. Dezaktywować urządzenie nie może zostać zarejestrowane hello usługi Menedżer StorSimple ponownie. Aby uzyskać więcej informacji, przejdź zbyt[zdezaktywować i usunąć tablica wirtualnego StorSimple](storsimple-virtual-array-deactivate-and-delete-device.md).

Zachowaj hello następujące najlepsze rozwiązania w uwadze podczas dezaktywacji tablica wirtualnego:

* Utwórz migawkę chmury wszystkich hello danych przed toodeactivating urządzenia wirtualnego. Po dezaktywowaniu wirtualnego tablicy wszystkie dane urządzenie lokalne powitania zostaną utracone. Tworzenie migawki chmury pozwoli toorecover danych na późniejszym etapie.
* Przed dezaktywacją tablicą wirtualnego StorSimple, upewnij się, że toostop lub usunąć klientów i hosty, które są zależne od tego urządzenia.
* Usunąć dezaktywować urządzenie, jeśli już używasz tak, aby nie naliczania opłat.

### <a name="monitoring"></a>Monitorowanie
tooensure, że tablica wirtualne StorSimple jest w dobrej kondycji ciągłego, należy toomonitor hello tablicy i upewnij się, otrzymywanie informacji z systemu hello między innymi alertów. toomonitor hello ogólną kondycję hello wirtualnego tablicy hello wdrożenie następujące najlepsze rozwiązania:

* Konfigurowanie monitorowania użycia dysku hello tootrack Twojego tablicy wirtualnego dysku danych, a także hello dysku systemu operacyjnego. Jeśli z funkcją Hyper-V, można użyć kombinacji System Center Virtual Machine Manager (SCVMM) i System Center Operations Manager (SCOM) toomonitor hosty wirtualizacji.
* Konfigurowanie powiadomień e-mail na alerty toosend wirtualnego tablicy w niektórych poziomy użycia.                                                                                                                                                                                                

### <a name="index-search-and-virus-scan-applications"></a>Indeks wyszukiwania i wirusów skanowanie aplikacji
Macierz wirtualnego StorSimple można automatycznie warstwy danych z toohello warstwy lokalne powitania chmury Microsoft Azure. Gdy aplikacji, takich jak wyszukiwania indeksu lub skanowanie w poszukiwaniu wirusów jest używane tooscan hello danych przechowywanych na StorSimple, należy tootake szczególną uwagę, że hello danych w chmurze nie uzyskać dostęp do i pobierane ponownie toohello warstwie lokalnej.

Firma Microsoft zaleca implementowanie hello następujące najlepsze rozwiązania w zakresie podczas konfigurowania wirtualnych tablica hello indeksu wyszukiwania lub wirusa skanowania:

* Wyłącz wszystkie operacje automatycznie pełnego skanowania.
* W przypadku woluminów warstwowych należy skonfigurować hello indeksu wyszukiwania lub wirusa skanowanie aplikacji tooperform skanowanie przyrostowe. Spowoduje to skanowanie tylko hello nowych danych prawdopodobnie znajdującej się na warstwie lokalne powitania. dane Hello warstwowych toohello chmury nie są dostępne podczas operacji przyrostowe.
* Upewnij się, hello wyszukiwania poprawne filtry i ustawienia są skonfigurowane tak, aby pobrać skanowane hello przeznaczonych tylko typy plików. Na przykład pliki (JPEG, GIF i TIFF) obrazów i inżynierów rysunki, nie należy przeskanować podczas odbudowywania indeksu pełnych lub przyrostowych hello.

Jeśli przy użyciu systemu Windows, proces indeksowania, zgodna z tymi wytycznymi:

* Nie należy używać indeksatora Windows hello dla woluminów warstwowych, zgodnie z jego przypomina dużych ilości danych (tabel) z chmury hello Jeśli indeks hello musi toobe odbudować często. Odbudowanie indeksu hello czy pobrać wszystkie tooindex typy plików ich zawartość.
* Użyj Windows hello indeksowania procesu dla woluminów przypiętych lokalnie, ponieważ spowoduje to tylko dostęp do danych na powitania warstwach lokalnych toobuild hello indeksu (hello chmury. nie będzie można uzyskać dostępu do danych).

### <a name="byte-range-locking"></a>Blokowanie zakresu bajtów
Aplikacje można zablokować określony zakres bajtów w plikach hello. Jeśli w przypadku aplikacji hello pisania tooyour StorSimple jest włączone blokowanie zakresu bajtów, następnie dodając funkcje warstw nie działa na wirtualnych macierzy. Dla hello toowork warstw pliki hello dostęp do wszystkich obszarów ma zostać odblokowana. Blokowanie zakresu bajtów nie jest obsługiwane z woluminów warstwowych w sieci wirtualnej macierzy.

Zalecane środki blokowania zakresu bajtów tooalleviate obejmują:

* Wyłącz zakresu bajtów blokowania w logiki aplikacji.
* Woluminy przypięte lokalnie użyj (zamiast warstwowa) hello danych skojarzonych z tą aplikacją. Woluminów przypiętych lokalnie nie warstwy do chmury hello.
* Przy użyciu przypięty lokalnie woluminów z włączoną blokowania zakresu bajtów, hello woluminu można do trybu online przed hello Przywracanie zostało ukończone. W takich przypadkach należy poczekać toobe przywracania hello jest pełny.

## <a name="multiple-arrays"></a>Wiele tablic
Wiele tablic wirtualnych mogą być potrzebne tooaccount toobe wdrożone rosnącym zestaw roboczy danych, które można zostaną przeniesione na powitania chmury, co wpływa na wydajność hello hello urządzenia. W takich przypadkach jest najlepszym urządzeń tooscale wraz z rozwojem hello zestaw roboczy. Wymaga to co najmniej jeden toobe urządzeń dodane w centrum danych lokalne powitania. Podczas dodawania urządzeń hello, można:

* Podziel hello bieżącego zestawu danych.
* Wdrażanie nowych urządzeń toonew obciążeń.
* W przypadku wdrażania wielu wirtualnych tablic, zaleca się z równoważeniem obciążenia perspektywy, rozpowszechniają tablicy hello innej funkcji hypervisor hostów.
* Wiele wirtualnych tablic (jeśli jest skonfigurowany jako serwer plików lub serwera iSCSI) można wdrożyć w Namespace rozproszonego systemu plików. Aby uzyskać szczegółowy opis kroków, przejdź zbyt[rozproszonych pliku System Namespace rozwiązania z hybrydowe chmury magazynu Deployment Guide](https://www.microsoft.com/download/details.aspx?id=45507). Obecnie rozproszonej replikacji systemu plików nie jest zalecane do użycia z tablicy wirtualnego hello. 

## <a name="see-also"></a>Zobacz też
Dowiedz się, jak za[administrowania tablica wirtualnego StorSimple](storsimple-virtual-array-manager-service-administration.md) za pośrednictwem hello usługi Menedżer StorSimple.

