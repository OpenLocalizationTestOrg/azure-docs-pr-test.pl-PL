---
title: "woluminy często zadawane pytania dotyczące przypięty lokalnie aaaStorSimple | Dokumentacja firmy Microsoft"
description: "Udostępnia odpowiedzi toofrequently zadawanych woluminów przypiętych lokalnie pytania dotyczące StorSimple."
services: storsimple
documentationcenter: NA
author: manuaery
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/26/2017
ms.author: manuaery
ms.openlocfilehash: a3a6557ca15e7e1947b45dcfd005640103c09591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-locally-pinned-volumes-frequently-asked-questions-faq"></a>Woluminy przypięte lokalnie StorSimple: często zadawane pytania (FAQ)
## <a name="overview"></a>Omówienie
Hello poniżej przedstawiono pytania i odpowiedzi, że mogą wystąpić podczas tworzenia woluminu StorSimple przypięty lokalnie, konwersja wolumin przypięty lokalnie tooa wolumin warstwowy (i na odwrót), lub kopii zapasowej i przywracania woluminu przypiętego lokalnie.

Pytania i odpowiedzi są rozmieszczone na następujące kategorie hello

* Tworzenie woluminu przypiętego lokalnie
* Tworzenie kopii zapasowych przypiętych lokalnie
* Konwertowanie na wolumin przypięty lokalnie tooa wolumin warstwowy
* Przywracanie woluminu przypiętego lokalnie
* Awarii woluminu przypiętego lokalnie

## <a name="questions-about-creating-a-locally-pinned-volume"></a>Pytania dotyczące tworzenia woluminu przypiętego lokalnie
**PYTANIE** Co to jest maksymalny rozmiar woluminu przypiętego lokalnie, który można utworzyć na powitania 8000 urządzeń z serii hello?

**A** na urządzeniach z systemem StorSimple 8000 serii aktualizacji 3.0 można udostępnić woluminów przypiętych lokalnie too8.5 TB lub woluminy warstwowe się too200 TB na urządzeniu 8100 hello. Na urządzeniu 8600 większych hello można udostępnić woluminów przypiętych lokalnie too22.5 TB lub woluminy warstwowe się too500 TB.

**PYTANIE** Ostatnio jest uaktualniony Mój tooUpdate urządzenie 8100 3.0 i podczas toocreate woluminu przypiętego lokalnie, hello maksymalny rozmiar dostępna jest tylko 6 TB i nie 8,5 TB. Dlaczego nie można utworzyć woluminu 8,5 TB?

**A** Jeśli urządzenie korzysta z aktualizacji 3.0, można alokować woluminy przypięte lokalnie się too8.5 TB lub woluminów warstwowych too200 TB na hello urządzenie 8100. Jeśli urządzenie z woluminami warstwowymi, następnie hello miejsca do utworzenia woluminu przypiętego lokalnie będzie proporcjonalnie niższa niż ten maksymalny limit. Na przykład, jeśli już zostały udostępnione woluminy warstwowe około 106 TB na urządzeniu 8100 (czyli połowy hello warstwowa pojemności), maksymalny rozmiar woluminu lokalnego, który można utworzyć na urządzeniu hello 8100 hello będzie odpowiednio zawężony too4 TB ( około połowy lokalnie maksymalna hello przypięty pojemność woluminu).

Ponieważ lokalne miejsce na urządzeniu hello jest hello używane toohost pracy zestaw woluminów warstwowych, hello dostępnego miejsca w przypadku tworzenia woluminu przypiętego lokalnie ograniczono Jeśli hello urządzenia z woluminami warstwowymi. Z drugiej strony tworzenia woluminu przypiętego lokalnie proporcjonalnie zmniejsza hello dostępne miejsce na woluminach warstwowych. następujące tabele Hello zawiera podsumowanie hello dostępnej pojemności warstwowego na urządzeniach hello 8100 i 8600 podczas tworzenia woluminów przypiętych lokalnie.

#### <a name="update-30"></a>Aktualizacja 3.0 
| Pojemność udostępnione woluminy przypięte lokalnie | Udostępnione woluminy warstwowe - 8100 toobe dostępnej pojemności | Udostępnione woluminy warstwowe - 8600 toobe dostępnej pojemności |
| --- | --- | --- |
| 0 |200 TB |500 TB. |
| 1 TB |176.5 TB |477.8 TB |
| 4 TB |105.9 TB |411.1 TB |
| 8.5 TB |0 TB |311.1 TB |
| 10 TB |Nie dotyczy |277.8 TB |
| 15 TB |Nie dotyczy |166.7 TB |
| 22.5 TB |Nie dotyczy |0 TB |

**PYTANIE** Dlaczego jest operacji tworzenia woluminu przypiętego lokalnie operacją wymagającą dużo czasu?

**ODPOWIEDŹ** Woluminów przypiętych lokalnie jest alokowany nieelastycznie. toocreate miejsca na hello warstw lokalne powitania urządzenia, dane z istniejące woluminy warstwowe może zostać przeniesiony toohello chmury podczas procesu udostępniania hello. I ponieważ to zależy od rozmiaru woluminu hello obsługiwana administracyjnie hello istniejące dane urządzenie i hello dostępną przepustowość toohello chmury, hello czasu hello toocreate woluminu lokalnego może być kilka godzin.

**PYTANIE** Jak długo trwa toocreate woluminu przypiętego lokalnie?

**ODPOWIEDŹ** Ponieważ woluminów przypiętych lokalnie jest alokowany nieelastycznie, niektóre istniejące dane z woluminów warstwowych może zostać przeniesiony chmury toohello podczas procesu udostępniania hello. W związku z tym hello toocreate czas, który wolumin przypięty lokalnie zależy od wielu czynników, takich jak rozmiar hello woluminu hello hello danych na urządzeniu i hello dostępną przepustowość. Na urządzeniu świeżo zainstalowanym ma nie woluminów toocreate czasu hello wolumin przypięty lokalnie jest około 10 minut na każdą terabajtów danych. Jednak tworzenie lokalnych woluminów może zająć wiele godzin, w oparte na czynnikach hello przedstawionych powyżej na urządzeniu, który jest używany.

**PYTANIE** Chcę toocreate woluminu przypiętego lokalnie. Czy istnieją najlepszych rozwiązań, które toobe należy pamiętać o?

**ODPOWIEDŹ** Woluminów przypiętych lokalnie są odpowiednie dla obciążeń, które wymagają lokalnych gwarancji danych przez cały czas i poufnych toocloud opóźnienia. Rozważając użycie woluminów lokalnych dla każdego z obciążeń, należy mieć świadomość hello następujące:

* Woluminów przypiętych lokalnie jest alokowany nieelastycznie i tworzenia woluminów lokalnych ma wpływ na powitania dostępne miejsce na woluminach warstwowych. W związku z tym zaleca się rozpoczynać mniejszym woluminów i skalowanie w górę wraz ze wzrostem zapotrzebowania Twojego magazynu.
* Inicjowanie obsługi administracyjnej lokalnych woluminów jest operacją wymagającą dużo czasu, które mogą dotyczyć wypychanie istniejących danych z woluminów warstwowych toohello chmury. W związku z tym może wystąpić obniżona wydajność na tych woluminach.
* Inicjowanie obsługi woluminów lokalnych to czasochłonna operacja. Hello czasu rzeczywistego związanych zależy od wielu czynników: hello rozmiaru woluminu hello zainicjowanie obsługi, danych na urządzeniu i dostępną przepustowość. Jeśli nie wykonano kopię zapasową istniejącej chmurze toohello woluminów, tworzenia woluminu jest wolniejsze. Sugerujemy tworzenia migawek chmury istniejących woluminów przed udostępnieniem woluminu lokalnego.
* Możesz przekonwertować istniejące woluminy warstwowe toolocally przypięty woluminy, a ta konwersja wymaga udostępniania miejsca na urządzeniu hello do hello wynikowa woluminu przypiętego lokalnie (w toobringing dodanie dół warstwowych dane, jeśli dowolne z chmury hello). Ponownie jest operacją wymagającą dużo czasu, który jest zależny od czynników, które zostały omówione powyżej. Zaleca się wykonanie kopii zapasowej istniejącej tooconversion wcześniejsze woluminów jako proces hello będzie wolniejsze nawet jeśli istniejące woluminy nie kopii zapasowej. Urządzenia mogą też wystąpić obniżona wydajność podczas tego procesu.

Więcej informacji na temat zbyt[tworzenia woluminu przypiętego lokalnie](storsimple-8000-manage-volumes-u2.md#add-a-volume)

**PYTANIE** Można utworzyć wiele woluminów przypiętych lokalnie na powitania jednocześnie?

**ODPOWIEDŹ** Tak, ale wszystkie zadania tworzenia i rozszerzania woluminów przypiętych lokalnie są przetwarzane sekwencyjnie.

Woluminów przypiętych lokalnie jest alokowany nieelastycznie i wymaga utworzenia lokalne miejsce na urządzeniu hello, (co może doprowadzić do istniejących danych z woluminów warstwowych toobe wypychana chmury toohello podczas procesu udostępniania hello). W związku z tym jeśli zadanie inicjowania obsługi administracyjnej jest w toku, inne zadania tworzenia woluminu lokalnego zostaną umieszczone w kolejce do momentu zakończenia tego zadania.

Podobnie jeśli jest rozszerzana istniejącego woluminu lokalnego lub wolumin warstwowy jest przekształcany wolumin przypięty lokalnie tooa, a następnie hello tworzenia nowego woluminu przypiętego lokalnie znajduje się w kolejce ukończenie poprzedniego zadania hello. Rozszerzanie hello rozmiar woluminu przypiętego lokalnie obejmuje hello rozszerzenia istniejącej przestrzeni lokalne powitania dla tego woluminu. Konwersja z woluminu warstwowego toolocally przypięty również wymaga utworzenia hello lokalne miejsce dla hello wynikowa woluminu przypiętego lokalnie. W obu tych operacji, tworzenie lub rozszerzenie lokalne miejsce długi działa zadanie.

Te zadania można wyświetlać w hello **zadania** bloku hello usługi Menedżer StorSimple urządzenia. Witaj zadanie jest aktywnie przetwarzanych jest stale aktualizowane tooreflect hello postęp inicjowania obsługi miejsca. Hello pozostałych zadań woluminu przypiętego lokalnie została oznaczona jako uruchomiona, ale ich postępu został wstrzymany i pobrane w kolejności hello umieszczonych w kolejce.

**PYTANIE** Po usunięciu woluminu przypiętego lokalnie. Dlaczego nie widzę hello odzyskać miejsce udział w hello dostępne miejsce podczas toocreate nowego woluminu?

**ODPOWIEDŹ** Jeśli usuniesz woluminu przypiętego lokalnie hello miejsca dla nowych woluminów mogły nie zostać zaktualizowane od razu. Witaj usługi Menedżer StorSimple urządzenia aktualizuje hello lokalne miejsce dostępne mniej więcej co godzinę. Sugerujemy poczekaj godziny przed podjęciem próby toocreate hello nowego woluminu.

**PYTANIE** Woluminów przypiętych lokalnie są obsługiwane na powitania urządzenia chmury?

**ODPOWIEDŹ** Woluminów przypiętych lokalnie nie są obsługiwane na powitania urządzenia chmury (8010 i 8020 urządzenia wcześniej określony tooas hello urządzenia wirtualnego StorSimple).

**PYTANIE** Można I Użyj toocreate poleceń cmdlet programu Azure PowerShell hello i zarządzać nimi woluminów przypiętych lokalnie?

**ODPOWIEDŹ** Nie, nie można utworzyć woluminów przypiętych lokalnie za pomocą poleceń cmdlet programu Azure PowerShell (warstwowa każdym woluminie tworzonych za pomocą programu Azure PowerShell). Również Sugerujemy że nie używasz toomodify poleceń cmdlet programu Azure PowerShell hello wszystkie właściwości woluminu przypiętego lokalnie, jak będą mieć hello niepożądane skutki modyfikowanie hello woluminu typu tootiered.

## <a name="questions-about-backing-up-a-locally-pinned-volume"></a>Pytania dotyczące tworzenia kopii zapasowej woluminu przypiętego lokalnie
**PYTANIE** Czy lokalne migawek woluminów przypiętych lokalnie obsługiwane?

**ODPOWIEDŹ** Tak, można wykonać migawki lokalnych woluminów przypiętych lokalnie. Zaleca się jednak, należy regularnie kopii zapasowych woluminów przypiętych lokalnie z tooensure migawki w chmurze, który dane są chronione w tekst hello możliwości awarii.

Zauważ, że inaczej lokalnymi migawkami woluminów przypiętych lokalnie może również warstwy limit toohello chmury i nie ma gwarancji toostay w warstwie lokalne powitania hello urządzenia.

**PYTANIE** Czy są jakieś wskazówki dotyczące zarządzania lokalnego migawek dla woluminów przypiętych lokalnie?

**ODPOWIEDŹ** Częste migawki lokalne obok wysokie tempo zmian danych w hello lokalnie woluminu przypiętego może spowodować lokalne miejsce na powitania toobe urządzenia używane szybko i spowodować danych z woluminów warstwowych przekazywanej toohello chmury. W związku z tym sugerujemy zminimalizować hello liczby migawek lokalnych.

**PYTANIE** Dotarło do mnie alert informujący, czy Moje migawki lokalne woluminów przypiętych lokalnie może unieważniona. Gdy to się zdarzyć?

**ODPOWIEDŹ** Częste migawki lokalne obok wysokie tempo zmian danych w hello lokalnie woluminu przypiętego może spowodować lokalne miejsce na powitania toobe urządzenia używane szybko. Jeśli używane są mocno hello warstw lokalne powitania urządzenia, awarii rozszerzonej chmurze może spowodować urządzenia hello zapełnianiu i przychodzące zapisy toohello woluminu może spowodować unieważnienie hello migawek (jak miejsce nie istnieje tooupdate hello migawki toorefer toohello starsze bloki danych, które zostały zastąpione). W hello sytuacji zapisy toohello woluminu będzie toobe obsługiwane, ale migawki lokalne powitania może być nieprawidłowy. Nie ma żadnych wpływ tooyour istniejących migawki w chmurze.

ostrzeżenie alertu Hello jest toonotify tego takiej sytuacji można wystąpić i upewnij się, że adres hello takie same w odpowiednim czasie, przeglądając z migawki lokalne planuje tootake mniej częste migawki lokalne lub Trwa usuwanie starszych migawki lokalne, które nie są już Wymagane.

Jeśli migawki lokalne powitania zostały unieważnione, zostanie wyświetlony alert informacji powiadamianie o tym, że hello migawki lokalne powitania określonych zasad tworzenia kopii zapasowej zostały unieważnione obok listy hello sygnatury czasowe hello migawek lokalnych, które zostały unieważnione. Te migawki zostaną usunięte automatycznie i nie będzie możliwe tooview je hello **katalogi kopii zapasowej** bloku w hello portalu Azure.

## <a name="questions-about-converting-a-tiered-volume-tooa-locally-pinned-volume"></a>Pytania dotyczące konwertowania wolumin przypięty lokalnie tooa wolumin warstwowy
**PYTANIE** Jestem I obserwowania niektórych powolność na urządzeniu hello podczas konwertowania wolumin przypięty lokalnie tooa woluminu warstwowego. Dlaczego jest sytuacja?

**ODPOWIEDŹ** proces konwersji Hello obejmuje dwa kroki:

1. Inicjowanie obsługi administracyjnej miejsca na urządzeniu hello do hello tylko do--skonwertowania przypięty lokalnie woluminu.
2. Pobieranie warstwowych danych z lokalnego tooensure chmury hello gwarancji.

Oba te kroki są za długie długotrwałych operacji, które są zależne od hello rozmiar woluminu hello konwertowanej danych na urządzeniu hello i dostępną przepustowość. Jak dane z istniejące woluminy warstwowe może zostaną przeniesione toohello chmury w ramach procesu udostępniania hello, urządzenie może wystąpić zmniejszenie wydajności w tym czasie. Ponadto procesu konwersji hello może przebiegać wolniej jeśli:

* Istniejące woluminy nie utworzone kopie zapasowe chmury toohello; Dlatego zalecamy wykonywać kopie zapasowe z poprzednich tooinitiating woluminów konwersji.
* Zastosowano zasady ograniczania przepustowości, który może stanowić ograniczenie hello dostępną przepustowość toohello chmurze; Firma Microsoft zaleca w związku z tym, że masz dedykowane MB/s 40 lub więcej chmur toohello połączenia.
* proces konwersji Hello może zająć kilka godzin powodu toohello wiele czynników przedstawionych powyżej; Dlatego zaleca się wykonanie tej operacji w czasie bez szczytów lub tooavoid weekendowe hello wpływ na użytkowników końcowych.

Więcej informacji na temat zbyt[skonwertować wolumin przypięty lokalnie tooa wolumin warstwowy](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)

**PYTANIE** Czy można anulować operacji konwersji woluminu hello?

**ODPOWIEDŹ** Nie, nie hello operacji konwersji hello Anuluj raz zainicjowane. Zgodnie z opisem w hello poprzedniego pytania, należy mieć świadomość hello potencjalne problemy z wydajnością czy może wystąpić podczas procesu hello i stosować najlepsze rozwiązania hello wymienionych powyżej, planując z konwersji.

**PYTANIE** Co w przypadku woluminu toomy operacji konwersji hello zakończy się niepowodzeniem?

**ODPOWIEDŹ** Konwersja woluminu może zakończyć się niepowodzeniem ze względu na problemy z łącznością toocloud. urządzenie Hello ostatecznie może przestać procesu konwersji hello po kilku nieudanych prób toobring warstwowych danych z chmury hello w dół. W takiej sytuacji hello typ woluminu będzie toobe hello źródła woluminu typu wcześniejsze tooconversion, oraz:

* Alert krytyczny zostanie podniesiony toonotify o błąd konwersji hello woluminu. Więcej informacji na temat [alerty powiązane toolocally przypięty woluminów](storsimple-8000-manage-alerts.md#locally-pinned-volume-alerts)
* Jeśli zmieniasz wolumin warstwowy tooa przypięty lokalnie hello woluminu będzie tooexhibit właściwości woluminu warstwowego jako danych może nadal znajdować się w chmurze hello. Zalecamy, aby rozwiązać problemy z łącznością hello, a następnie ponów operację konwersji hello.
* Podobnie jeśli konwersja z tooa przypięte lokalnie do warstwy woluminu kończy się niepowodzeniem, mimo że wolumin hello zostaną oznaczone jako woluminu przypiętego lokalnie, będzie działać jako wolumin warstwowy (ponieważ danych może mieć rozrzucone toohello chmury). Jednak będzie toooccupy miejsce w warstwach lokalne powitania hello urządzenia. Ta przestrzeń nie będą dostępne dla innych woluminów przypiętych lokalnie. Zaleca się, ponów próbę wykonania tej operacji tooensure, czy konwersji woluminu hello są kompletne i będzie można odzyskać hello lokalne miejsce na urządzeniu hello.

## <a name="questions-about-restoring-a-locally-pinned-volume"></a>Pytania dotyczące przywracania woluminu przypiętego lokalnie
**PYTANIE** Woluminów przypiętych lokalnie natychmiast przywrócona?

**ODPOWIEDŹ** Tak, woluminów przypiętych lokalnie zostaną przywrócone natychmiast. Jak hello informacji o metadanych dla woluminu hello są pobierane z chmury hello w ramach operacji przywracania hello, wolumin hello jest przełączany w tryb online i są dostępne dla hosta hello. Jednak lokalnych gwarancji dla woluminu hello się, że dane nie będą obecne, dopóki wszystkie dane hello została pobrana z hello chmury i może wystąpić zmniejszenie wydajności na tych woluminach na czas trwania hello hello przywracania.

**PYTANIE** Jak długo trwa toorestore woluminu przypiętego lokalnie?

**ODPOWIEDŹ** Woluminów przypiętych lokalnie są natychmiast przywrócona i trybu online, jak hello woluminu metadane są pobierane z chmury hello danych woluminu hello kontynuuje toobe pobierany w tle hello. Ten ostatni część operacji przywracania hello — odzyskać hello lokalnych gwarancji dla danych woluminu hello — jest operacją wymagającą dużo czasu i może potrwać kilka godzin dla wszystkich toobe danych hello wprowadzone ponownie lokalnego. Witaj czas toocomplete Witaj sam zależy od wielu czynników, takich jak hello rozmiar woluminu hello przywracana i hello dostępną przepustowość. Usunięcie hello oryginalnego woluminu, który jest przywracana dodatkowy czas zostaną wykonane toocreate hello lokalne miejsce na urządzeniu hello w ramach operacji przywracania hello.

**PYTANIE** Potrzebuję toorestore Mój istniejący lokalnie przypięty woluminu tooan starsze migawką (gdy wolumin hello został warstwowej). Hello woluminu będzie można przywrócić ponieważ w takim przypadku do warstwy?

**ODPOWIEDŹ** Nie, zostaną przywrócone hello woluminu jako woluminu przypiętego lokalnie. Mimo że hello migawki czasu toohello dat po hello wolumin został do warstwy, podczas przywracania istniejące woluminy StorSimple zawsze używa hello typ woluminu na powitania dysku, ponieważ istnieje aktualnie.

**PYTANIE** Moje woluminu przypiętego lokalnie I rozszerzony ostatnio, ale teraz jest konieczne toorestore hello tooa czas danych podczas hello wolumin był mniejszy rozmiar. Zmieni rozmiar przywracania hello bieżącego woluminu i będzie konieczne tooextend hello rozmiar woluminu powitania po zakończeniu przywracania hello?

**ODPOWIEDŹ** Tak, przywracania hello zmieni się rozmiar woluminu hello i konieczne będzie tooextend hello rozmiar woluminu powitania po ukończeniu przywracania hello.

**PYTANIE** Podczas przywracania można zmienić typu hello woluminu?

**A.**nie, nie można zmienić typ woluminu hello podczas przywracania.

* Woluminy, które zostały usunięte zostaną przywrócone jako typ hello przechowywane w migawce hello.
* Istniejące woluminy są przywracane na podstawie ich bieżącego typu, niezależnie od typu hello przechowywane w migawce hello (zobacz toohello dwoma poprzednimi pytania).

**PYTANIE** Potrzebuję toorestore Moje woluminu przypiętego lokalnie, ale wybrano niepoprawny punkt w czasie migawki. Czy można anulować bieżącą operację przywracania hello?

**ODPOWIEDŹ** Tak, możesz anulować operacji przywracania w toku. Stan Hello hello woluminu zostanie wycofana toohello stanu na początku hello hello przywracania. Jednak wszystkie zapisy, które zostały dokonane toohello woluminu, podczas przywracania hello jest w toku, zostaną utracone.

**PYTANIE** Rozpoczęciu operacji przywracania na jednym z mojej woluminów przypiętych lokalnie, a teraz wyświetlać migawki w katalogu Moje zaległości nie zebrać tworzenia. To do czego służy?

**ODPOWIEDŹ** Jest to migawka tymczasowego hello jest tworzony toohello poprzednich operacji przywracania, który jest używany na potrzeby wycofywania na wypadek hello przywracania została anulowana lub nie powiedzie się. Nie należy usuwać tej migawki; go zostaną automatycznie usunięte po zakończeniu przywracania hello. Ten problem może wystąpić, jeśli zadanie przywracania ma przypięty tylko lokalnie woluminów lub mieszane lokalnie woluminów przypiętych i warstwowego. Jeśli zadanie przywracania hello zawiera tylko woluminów warstwowych, ten problem nie zostanie przeprowadzona.

**PYTANIE** Czy można sklonować woluminu przypiętego lokalnie?

**ODPOWIEDŹ** Tak, można. Jednak wolumin przypięty lokalnie hello zostaną sklonowane jako wolumin warstwowy domyślnie. Więcej informacji na temat zbyt[sklonować woluminu przypiętego lokalnie](storsimple-8000-clone-volume-u2.md)

## <a name="questions-about-failing-over-a-locally-pinned-volume"></a>Pytania dotyczące awarii woluminu przypiętego lokalnie
**PYTANIE** Potrzebuję toofail przez urządzenie fizyczne tooanother urządzenia. Moje woluminów przypiętych lokalnie nie powiedzie się powyżej przypięty lokalnie lub do warstwy?

**ODPOWIEDŹ** woluminy przypięte lokalnie Hello są Failover przypięty lokalnie, jeśli urządzenie docelowe hello działa StorSimple 8000 z aktualizacją update 3 lub nowszej.

Więcej informacji na temat [trybu failover i odzyskiwania po awarii z przypięty lokalnie woluminach między wersjami](storsimple-8000-device-failover-disaster-recovery.md#device-failover-across-software-versions)

**PYTANIE** Woluminów przypiętych lokalnie natychmiast przywrócono podczas odzyskiwania awaryjnego (DR)?

**ODPOWIEDŹ** Tak, woluminów przypiętych lokalnie zostaną przywrócone natychmiast podczas pracy awaryjnej. Jak hello informacji o metadanych dla woluminu hello są pobierane z chmury hello w ramach operacji trybu failover hello, wolumin hello jest przełączany w tryb online na urządzeniu docelowym hello i są dostępne dla hosta hello. W tym samym czasie hello danych woluminu będzie toodownload w tle hello i mogą wystąpić zmniejszenie wydajności na tych woluminach na czas trwania hello hello trybu failover.

**PYTANIE** Widać hello trybu failover zadanie zostało ukończone, jak śledzić postęp hello woluminu przypiętego lokalnie, która jest przywracana na urządzeniu docelowym hello?

**ODPOWIEDŹ** Podczas operacji trybu failover zadanie trybu failover hello jest oznaczone jako zakończone, po wszystkich woluminów hello w zestawie trybu failover hello zostały natychmiast przywrócona i przełączony w tryb online na urządzeniu docelowym hello. Dotyczy to również wszelkich woluminów przypiętych lokalnie, które mogą nie jednak gwarancji lokalne powitania danych tylko będą dostępne po pobraniu wszystkich danych hello hello woluminu. Możesz śledzić postępy, to dla każdego woluminu przypiętego lokalnie, który nie powiodło się przez monitorowanie hello odpowiednich zadań przywracania utworzone jako część hello trybu failover. Te zadania przywracania poszczególnych zostanie utworzone tylko dla woluminów przypiętych lokalnie.

**PYTANIE** Podczas pracy awaryjnej można zmienić typu hello woluminu?

**ODPOWIEDŹ** Nie, nie można zmienić typ woluminu hello podczas pracy w trybie failover. Jeśli kończą się niepowodzeniem przez tooanother urządzenia fizycznego, który działa z serii StorSimple 8000 z aktualizacją 3, woluminy hello są awaryjnie na podstawie typu woluminu hello przechowywane w migawce hello.

**PYTANIE** I w trybie Failover kontener woluminów z urządzenia chmury toohello woluminów przypiętych lokalnie?

**ODPOWIEDŹ** Tak, można. woluminy Hello przypięty lokalnie będzie można przełączyć jako woluminy warstwowe. Więcej informacji na temat [trybu failover i odzyskiwania po awarii z przypięty lokalnie woluminach między wersjami](storsimple-8000-device-failover-disaster-recovery.md#common-considerations-for-device-failover)

