---
title: "aaaStorSimple 8000 składniki sprzętowe serii i stan | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor hello składniki sprzętowe urządzenia StorSimple za pośrednictwem usługi Menedżer StorSimple urządzenia hello."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 85b398e4b1a6b8921792b8945331325940082eb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-hardware-components-and-status"></a>Składniki sprzętowe toomonitor usługi Menedżer StorSimple urządzenia hello i stanu
## <a name="overview"></a>Omówienie
W tym artykule opisano hello różne składniki fizyczne i logiczne w urządzeniu serii StorSimple 8000 lokalnymi. Wyjaśniono tu również, jak toomonitor hello stan składnika urządzenia przy użyciu hello **sprzętu i stan kondycji** bloku w hello usługi Menedżer StorSimple urządzenia.

Witaj **sprzętu i stan kondycji** bloku pokazuje stan sprzętu hello wszystkie składniki urządzenia StorSimple hello.

W obszarze hello listy składników 8100 istnieją trzy sekcje, które opisują:

* **Udostępniane składniki** — te nie są częścią hello kontrolerów, takie jak stacje dysków, obudowy, składniki PCM temperatury PCM napięcia wiersz i czujników bieżącego wiersza.
* **Składniki kontrolera 0** — hello składników, które znajdują się na kontrolerze 0, takie jak kontroler, expander sygnatury dostępu Współdzielonego i łącznika, czujnikami temperatury kontrolera, a hello różnych interfejsów sieciowych.
* **Składniki kontrolera 1** — Witaj składników, które stanowią kontrolera 1 podobne toothose szczegółowe dla kontrolera 0.

Urządzenia 8600 ma dodatkowe składniki, które odpowiadają toohello obudowa rozszerzony Bunch dla dysków (EBOD). W obszarze hello listę składników istnieją pięciu sekcji. Z nich istnieją trzy sekcje, które zawierają hello składniki w obudowie głównej hello i są identyczne toohello firma opisana dla 8100. Istnieją dwa dodatkowe sekcje dla hello obudowa EBOD opisujące:

* **Składniki EBOD kontrolera 0** — Witaj składników, które znajdują się w obudowie EBOD 0, takich jak kontroler EBOD hello, czujnikami temperatury expander i łącznika i kontrolera SAS.
* **Składniki 1 kontrolera EBOD** — Witaj składników, które stanowią obudowa EBOD 1, podobne toothose szczegółowe obudowa EBOD 0.
* **Składniki udostępnione obudowy EBOD** — składniki hello znajdujących się w hello EBOD obudowy i PCM, które nie są częścią hello EBOD kontrolera.

> [!NOTE]
> **Stan sprzętu Hello jest niedostępny dla urządzenia StorSimple w chmurze (8010/8020).**


## <a name="monitor-hello-hardware-status"></a>Monitorowanie stanu sprzętu hello
Wykonaj następujące kroki tooview hello sprzętu stan składnika urządzenia hello:

1. Przejdź za**urządzeń**, wybierz określonego urządzenia StorSimple. Przejdź za**Monitor > kondycji sprzętu**.

    ![](./media/storsimple-8000-monitor-hardware-status/hw-health1.png)

2. Zlokalizuj hello **składniki sprzętowe** sekcji i wybierz jedną z dostępnych składników hello. Kliknij hello składnika etykiety tooexpand hello listy i wyświetlić stan hello hello różne składniki urządzenia. Zobacz hello [listy szczegółowe części obudowy głównej hello](#component-list-for-primary-enclosure-of-storsimple-device) i hello [listę składników szczegółowe dla hello obudowa EBOD](#component-list-for-ebod-enclosure-of-storsimple-device).

    ![](./media/storsimple-8000-monitor-hardware-status/hw-health2.png)

3. Użyj powitania po stan składnika hello kodowania toointerpret schemat kolorów:
   
   * **Zielone wyboru** — oznacza składnik dobrej kondycji z **OK** stanu.
   * **Żółty** — oznacza składnik obniżeniem **ostrzeżenie** stanu.
   * **Czerwony wykrzyknik** — Denotes nie powiodło się składnika, który **błąd** stanu.
   * **Białe czarny tekst** — określa składnik, który nie jest obecny.
   
   Witaj Poniższy zrzut ekranu przedstawia urządzenie, które zawiera składniki w **OK**, **ostrzeżenie**, i **błąd** stanu.
       
   ![](./media/storsimple-8000-monitor-hardware-status/hw-health3.png)

   Powiększające hello **listy składników Shared**, zobaczysz klastra NVRAM i hello hello są ograniczone.

   ![](./media/storsimple-8000-monitor-hardware-status/hw-health5.png)

   Powiększające hello **składniki kontrolera 1** listy, zobaczysz hello tego węzła nie powiodło się.  

   ![](./media/storsimple-8000-monitor-hardware-status/hw-health4.png)  

4. Jeśli wystąpią składnik, który nie znajduje się w **dobra kondycja** stanu, skontaktuj się z Microsoft Support. Alerty są włączone na urządzeniu, otrzymasz alert e-mail. Jeśli potrzebujesz tooreplace składnik sprzętowy nie powiodło się, zobacz [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).

## <a name="component-list-for-primary-enclosure-of-storsimple-device"></a>Lista składników dla podstawowego Obudowa urządzenia StorSimple
Witaj poniższej tabeli przedstawiono hello składniki fizyczne i logiczne, które są zawarte w hello głównej obudowy (istnieje zarówno w 8100 i 8600) lokalnego urządzenia StorSimple.

| Składnik | Moduł | Typ | Lokalizacja | Pole (jednostkę FRU replaceable unit)? | Opis |
| --- | --- | --- | --- | --- | --- |
| Dysk w gnieździe [0-11] |Stacje dysków |Fizyczne |Udostępniona |Tak |Zobaczy jeden wiersz dla każdego hello SSD lub hello HDD dyski w obudowie głównej hello. |
| Czujnik temperatury otoczenia |Obudowa |Fizyczne |Udostępniona |Nie |Środki hello temperatury w obudowie hello. |
| Czujnik temperatury środkowa |Obudowa |Fizyczne |Udostępniona |Nie |Środki hello temperatury hello pośredniej płaszczyzny. |
| Alarmu |Obudowa |Fizyczne |Udostępniona |Nie |Wskazuje, czy podsystem alarmu hello w obudowie hello jest funkcjonalności. |
| Obudowa |Obudowa |Fizyczne |Udostępniona |Tak |Wskazuje podstawę hello obecność. |
| Obudowa ustawienia |Obudowa |Fizyczne |Udostępniona |Nie |Odwołuje się toohello panelu przedniego hello obudowy. |
| Wiersz czujnikami napięcia |PCM |Fizyczne |Udostępniona |Nie |Wiele czujnikami napięcia wiersz ma ich stanie wyświetlony, wskazuje, czy mierzony hello napięcia w granicach tolerancji. |
| Czujniki bieżącego wiersza |PCM |Fizyczne |Udostępniona |Nie |Wiele czujników bieżący wiersz ma ich stanie wyświetlony, wskazuje, czy hello bieżącego mierzoną w granicach tolerancji. |
| Czujnikami temperatury w PCM |PCM |Fizyczne |Udostępniona |Nie |Wiele czujnikami temperatury takie jak czujniki Inlet i punkt aktywny ich stanie wyświetlony, wskazującą, czy hello mierzony temperatury mieści się w granicach. |
| Zasilacz [0-1] |PCM |Fizyczne |Udostępniona |Tak |Jeden wiersz jest widoczne dla każdego hello zasilacze w hello dwóch PCMs znajduje się w hello obu hello urządzenia. |
| Chłodzenia [0-1] |PCM |Fizyczne |Udostępniona |Tak |Jeden wiersz jest widoczne dla każdego hello cztery wentylatory znajdującej się w hello PCMs dwa. |
| Baterii [0-1] |PCM |Fizyczne |Udostępniona |Tak |Jeden wiersz, jest widoczne dla każdego hello kopii zapasowej baterii modułów, które są umieszczone w hello PCM. |
| Metis |Nie dotyczy |Logiczne |Udostępniona |Nie dotyczy |Wyświetla stan hello baterii hello: Określa, czy należy ładowania i zbliża się koniec życia. |
| Klaster |Nie dotyczy |Logiczne |Udostępniona |Nie dotyczy |Wyświetla hello stanu hello klastra, który jest tworzony między hello dwa moduły zintegrowany kontroler. |
| Węzeł klastra |Nie dotyczy |Logiczne |Udostępniona |Nie dotyczy |Wskazuje stan kontrolera hello jako część klastra hello hello. |
| Kworum klastra |Nie dotyczy |Logiczne | |Nie dotyczy |Wskazuje hello obecność hello większość dysku członkostwo w hello puli magazynów dysku twardego. |
| Miejsce na dysku twardego danych |Nie dotyczy |Logiczne |Udostępniona |Nie dotyczy |Witaj miejsce do magazynowania służy do danych w puli magazynu na dysku twardym (HDD) hello. |
| Miejsce na dysku twardego zarządzania |Nie dotyczy |Logiczne |Udostępniona |Nie dotyczy |zarezerwowano miejsce Hello w hello HDD puli magazynu dla zadań zarządzania. |
| Miejsce na dysku kworum |Nie dotyczy |Logiczne |Udostępniona |Nie dotyczy |zarezerwowano miejsce Hello w hello puli magazynów dysku dla kworum klastra. |
| Dysk twardy zamiany miejsca |Nie dotyczy |Logiczne |Udostępniona |Nie dotyczy |zarezerwowano miejsce Hello w hello puli magazynów dysku twardego do zastąpienia kontrolera. |
| Miejsca na dysku SSD danych |Nie dotyczy |Logiczne |Udostępniona |Nie dotyczy |miejsca do magazynowania Hello używane dla danych w puli magazynu programu hello półprzewodnikowych (SSD) dysku. |
| NVRAM dysków SSD miejsca |Nie dotyczy |Logiczne |Udostępniona |Nie dotyczy |Witaj miejsca do magazynowania w puli magazynów dysków SSD, przeznaczona dla logiki NVRAM hello. |
| Dysk twardy puli magazynu |Nie dotyczy |Logiczne |Udostępniona |Nie dotyczy |Wyświetla hello stan puli magazynu logicznego hello, która jest tworzona na podstawie urządzenia dysków twardych. |
| Puli pamięci masowej SSD |Nie dotyczy |Logiczne |Udostępniona |Nie dotyczy |Wyświetla hello stan puli magazynu logicznego hello, która jest tworzona z urządzenia dyski SSD. |
| Kontroler [0-1] [state] |WE/WY |Fizyczne |Kontrolera |Tak |Wyświetla stan hello hello kontrolera, oraz czy jest w trybie aktywny lub wstrzymania w obudowie hello. |
| Czujnikami temperatury w kontrolerze |WE/WY |Fizyczne |Kontrolera |Nie |Wiele czujnikami temperatury, takich jak moduł we/wy, temperatury procesora CPU, czujników DIMM i PCIe ma ich stanie wyświetlony, wskazuje, czy temperatury hello napotkano mieści się w granicach. |
| SAS expander |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello hello serial dołączone SCSI (SAS) expander, które jest używane tooconnect hello magazynu zintegrowanego toohello kontrolera. |
| Łącznik SAS [0-1] |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello każdy łącznik SAS, czyli tooconnect używane zintegrowane magazynu toohello SAS expander. |
| Między połączeniami wzajemnymi SBB środkowa |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello hello środkowa łącznika, który jest używany tooconnect płaszczyzny pośredniej toohello każdego kontrolera. |
| Rdzeń procesora |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello hello rdzeni procesora w ramach każdego kontrolera. |
| Obudowa electronics zasilania |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello hello zasilania systemu używany przez hello obudowy. |
| Obudowa electronics diagnostyki |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello podsystemów diagnostyki hello podał hello kontrolera. |
| Kontroler zarządzania płytą główną (BMC) |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello hello kontrolera zarządzania płytą główną (BMC), czyli procesor specjalne usług, który monitoruje urządzenia sprzętowego hello przez czujniki i komunikuje się z administratorem systemu hello za pośrednictwem połączenia niezależne. |
| Ethernet |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello każdego hello interfejsów sieciowych, oznacza to, że hello zarządzania i porty danych na powitania kontrolera. |
| NVRAM |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello NVRAM, trwałej pamięci hello baterii, pełniącą tooretain aplikacji ważne informacje w przypadku awarii zasilania hello kopię zapasową. |

## <a name="component-list-for-ebod-enclosure-of-storsimple-device"></a>Lista składników dla obudowa EBOD urządzenia StorSimple
Witaj poniższej tabeli przedstawiono hello składniki fizyczne i logiczne, które są zawarte w hello EBOD obudowę (tylko w modelu 8600) lokalnego urządzenia StorSimple.

| Składnik | Moduł | Typ | Lokalizacja | JEDNOSTKI FRU? | Opis |
| --- | --- | --- | --- | --- | --- |
| Dysk w gnieździe [0-11] |Stacje dysków |Fizyczne |Udostępniona |Tak |Jeden wiersz jest widoczne dla każdego powitalne dysków HDD w hello początku hello EBOD obudowy. |
| Czujnik temperatury otoczenia |Obudowa |Fizyczne |Udostępniona |Nie |Środki hello temperatury w obudowie hello. |
| Czujnik temperatury środkowa |Obudowa |Fizyczne |Udostępniona |Nie |Środki hello temperatury hello pośredniej płaszczyzny. |
| Alarmu |Obudowa |Fizyczne |Udostępniona |Nie |Wskazuje, czy podsystem alarmu hello w obudowie hello jest funkcjonalności. |
| Obudowa |Obudowa |Fizyczne |Udostępniona |Tak |Wskazuje podstawę hello obecność. |
| Obudowa ustawienia |Obudowa |Fizyczne |Udostępniona |Nie |Odnosi się toohello OPS lub hello panelu przedniego hello obudowy. |
| Wiersz czujnikami napięcia |PCM |Fizyczne |Udostępniona |Nie |Wiele czujnikami napięcia wiersz ma ich stanie wyświetlony, wskazuje, czy mierzony hello napięcia w granicach tolerancji. |
| Czujniki bieżącego wiersza |PCM |Fizyczne |Udostępniona |Nie |Wiele czujników bieżący wiersz ma ich stanie wyświetlony, wskazuje, czy hello bieżącego mierzoną w granicach tolerancji. |
| Czujnikami temperatury w PCM |PCM |Fizyczne |Udostępniona |Nie |Wiele czujnikami temperatury takie jak czujniki Inlet i punkt aktywny ich stanie wyświetlony, wskazuje, czy hello mierzony temperatury mieści się w granicach. |
| Zasilacz [0-1] |PCM |Fizyczne |Udostępniona |Tak |Jeden wiersz jest widoczne dla każdego hello zasilacze w hello dwóch PCMs znajduje się w hello obu hello urządzenia. |
| Chłodzenia [0-1] |PCM |Fizyczne |Udostępniona |Tak |Jeden wiersz jest widoczne dla każdego hello cztery wentylatory znajdującej się w hello PCMs dwa. |
| Lokalny magazyn [dysk twardy] |Nie dotyczy |Logiczne |Udostępniona |Nie dotyczy |Wyświetla hello stan puli magazynu logicznego hello, która jest tworzona na podstawie urządzenia dysków twardych. |
| Kontroler [0-1] [state] |WE/WY |Fizyczne |Kontrolera |Tak |Wyświetla hello stan hello kontrolerów w hello EBOD module. |
| Czujnikami temperatury w EBOD |WE/WY |Fizyczne |Kontrolera |Nie |Wiele czujnikami temperatury przez każdy z kontrolerów ma ich stanie wyświetlony, wskazuje, czy temperatury hello napotkano w granicach tolerancji. |
| SAS expander |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello hello expander SAS, które jest używane tooconnect hello magazynu zintegrowanego toohello kontrolera. |
| Łącznik SAS [0-2] |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello każdy łącznik SAS, czyli tooconnect używane zintegrowane magazynu toohello SAS expander. |
| Między połączeniami wzajemnymi SBB środkowa |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello hello środkowa łącznika, który jest używany tooconnect płaszczyzny pośredniej toohello każdego kontrolera. |
| Obudowa electronics zasilania |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello hello zasilania systemu używany przez hello obudowy. |
| Obudowa electronics diagnostyki |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello podsystemów diagnostyki hello podał hello kontrolera. |
| Kontroler toodevice połączenia |WE/WY |Fizyczne |Kontrolera |Nie |Wskazuje stan hello hello połączenia między hello moduł EBOD We/Wy i hello urządzenia kontrolera. |

## <a name="next-steps"></a>Następne kroki
* toouse urządzenia, wybierz pozycje tooadminister usługi Menedżer StorSimple urządzenia są hello zbyt[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).
* Tootroubleshoot składnik urządzenia o stanie działanie lub uszkodzenie należy odwoływać się za[StorSimple wskaźniki monitorowania](storsimple-monitoring-indicators.md).
* tooreplace składnik sprzętowy nie powiodło się, zobacz [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).
* Jeśli będziesz kontynuować tooexperience problemów z urządzeniami, [skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md).

