---
title: "aaaService rozwiązania mapy samodzielnie realizowanych pokaz | Dokumentacja firmy Microsoft"
description: "Mapa usług jest rozwiązaniem w operacji pakietu zarządzania (OMS), który automatycznie odnajduje składniki aplikacji w systemie Windows i systemów Linux i map hello komunikacji między usługami.  Jest to self pokaz realizowanych, który przeprowadzi Cię przez przy użyciu mapy usługi tooidentify i diagnozowania problemu symulowane w aplikacji sieci web."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: 13f26241cd55a9b35c07d6ca52760a968abffc64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a>Samodzielnie realizowany pokaz pakietu Operations Management Suite (OMS) — mapa usługi
To self pokaz realizowanych, który przeprowadzi Cię przez przy użyciu hello [rozwiązania mapy usługi](operations-management-suite-service-map.md) w tooidentify Operations Management Suite (OMS) i diagnozowania problemu symulowane w aplikacji sieci web.  Mapy usług automatycznie odnajduje składniki aplikacji w systemach Windows i Linux oraz mapy hello komunikacji między usługami.  Również konsoliduje dane zebrane przez inne tooassist usług OMS w analizowanie wydajności i identyfikowanie problemów.  Również użyjesz [Zaloguj wyszukiwania analizy dzienników](../log-analytics/log-analytics-log-searches.md) toodrill w dół na zebrane dane w kolejności tooidentify hello główny problem.


## <a name="scenario-description"></a>Opis scenariusza
Po prostu otrzymał powiadomienie, że aplikację portalu klienta xyz hello występują problemy z wydajnością.  Witaj tylko informacje, czy masz jest uruchomienia około 4:00 am PST dzisiaj tych problemów.  Nie masz pewności całkowicie wszystkich składników hello tego portalu hello jest zależny od innego niż zestaw serwerów sieci web.  

## <a name="components-and-features-used"></a>Używane składniki i funkcje
- [Rozwiązanie mapy usługi](operations-management-suite-service-map.md)
- [Przeszukiwanie dzienników w usłudze Log Analytics](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a>Przewodnik

### <a name="1-connect-toohello-oms-experience-center"></a>1. Połącz toohello OMS środowisko Center
Ten krokach związanych z używa hello [Centrum obsługi pakiet zarządzania Operations](https://experience.mms.microsoft.com/) zapewniające kompletne środowisko OMS z przykładowymi danymi. Uruchomić, klikając to łącze, udostępnić informacje, a następnie wybierz hello **szczegółowe dane i analiza** scenariusza.


### <a name="2-start-service-map"></a>2. Uruchamianie mapy usługi
Uruchom hello mapy usługi rozwiązania, klikając hello **mapy usługi** kafelka.

![Kafelek Mapa usługi](media/operations-management-suite-walkthrough-servicemap/tile.png)

zostanie wyświetlona konsola mapy usługi Hello.  W hello w okienku po lewej stronie jest lista komputerów w środowisku z zainstalowanym agentem usługi mapy hello.  Należy wybrać komputer hello, które mają tooview z tej listy.

![Lista komputerów](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a>3. Wyświetl komputer
Wiemy, że serwery sieci web hello są nazywane AcmeWFE001 i AcmeWFE002, to prawdopodobnie toostart uzasadnione miejsce.  Kliknij serwer **AcmeWFE001**.  Spowoduje to wyświetlenie mapy hello AcmeWFE001 i wszystkie jego zależności.  Widać, które procesy są uruchomione na powitania wybranych komputerów, które komunikują się z usług zewnętrznych.

![Serwer sieci Web](media/operations-management-suite-walkthrough-servicemap/web-server.png)

Jesteśmy danych o wydajności hello naszych sieci Web aplikacji kliknij przycisk więc na powitania **AcmeAppPool (puli aplikacji usług IIS)** procesu.  Wyświetla szczegóły hello tego procesu, a wyróżnia jego zależności.  

![Pula aplikacji](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a>4. Zmień przedział czasu

Firma Microsoft znany problem hello rozpoczęte o 4:00:00, więc warto przyjrzeć została co dzieje o tej godzinie. Polecenie **zakres czasu** i zmień too4 czasu hello: 00 AM PST (Zachowaj hello bieżącą datę i dostosować do lokalnej strefy czasowej) o czasie trwania 20 minut.

![Selektor czasu](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a>5. Wyświetl alert

Teraz widzimy tego hello **acmetomcat** zależności ma alertu wyświetlany, więc to naszych potencjalny problem.  Kliknij ikonę alertu hello w **acmetomcat** tooshow hello szczegółów alertu hello.  Widzimy, że mamy krytyczne wykorzystanie procesora CPU, i możemy rozwinąć informacje, aby uzyskać więcej szczegółów.  Prawdopodobnie to jest właśnie przyczyna niskiej wydajności. 

![Alerty](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a>6. Wyświetl wydajność

Przyjrzyjmy się bliżej serwerowi **acmetomcat**.  Kliknij hello górnego rogu **acmetomcat** i wybierz **obciążenia serwera mapy** tooshow hello szczegółów i zależności dla tego komputera. Można następnie szukamy bardziej do tych tooverify liczniki wydajności naszych podejrzenia.  Wybierz hello **wydajności** hello toodisplay kartę [liczniki wydajności zebrane przez analizy dzienników](../log-analytics/log-analytics-data-sources-performance-counters.md) hello zakresu czasu.  Możemy stwierdzić, odbieramy okresowe największego hello procesora i pamięci.

![Wydajność](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a>7. Wyświetl dane śledzenia zmian
Spróbujmy dowiedzieć się, co jest przyczyną tego wysokiego wykorzystania.  Polecenie hello **Podsumowanie** kartę.  Zapewnia informacje, które OMS zebrane z komputera hello takich jak nie powiodła się, połączeń, alerty krytyczne i zmiany oprogramowania.  Sekcje interesujące informacje ostatnie już powinny być rozwijane i można rozszerzyć inne informacje tooinspect sekcje, które zawierają.


Jeśli sekcja **Śledzenie zmian** nie jest jeszcze otwarta, rozwiń ją.  Pokazuje informacje zebrane przez hello [śledzenia zmian rozwiązania](../log-analytics/log-analytics-change-tracking.md).  Wygląda na to, że w tym przedziale czasu nastąpiła zmiana oprogramowania.  Polecenie **oprogramowania** tooget szczegóły.  Proces tworzenia kopii zapasowej został dodany toohello maszyny zaraz po 4:00:00, więc pojawia się culprit hello toobe zasobów nadmiernego hello są używane.

![Śledzenie zmian](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a>8. Wyświetl szczegóły w funkcji przeszukiwania dzienników
Dodatkową weryfikację to analizując hello szczegółowe informacje o wydajności zebrane w repozytorium analizy dzienników hello.  Polecenie hello **alerty** karcie ponownie, a następnie na powitania **Procesora wysokiej** alertów.  Kliknij opcję **Pokaż podczas wyszukiwania dziennika**.  Zostanie otwarte okno wyszukiwania dziennika hello, których można wykonywać [dziennika wyszukiwania](../log-analytics/log-analytics-log-searches.md) względem wszystkich danych przechowywanych w repozytorium hello.  Mapa usług już wypełnione queriy firmie Microsoft alert hello tooretrieve My.  

![Wyszukiwanie w dzienniku](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a>9. Otwórz zapisane wyszukiwanie
Zobaczmy, jeśli możemy pobrać niektórych bardziej szczegółowo na powitania zbierania wydajności, który wygenerował tego alertu i sprawdź naszych podejrzenie, że problemy hello są spowodowane tego procesu tworzenia kopii zapasowej.  Zmień zakres czasu hello zbyt**6 godzin**.  Następnie kliknij polecenie **ulubione** i przewiń w dół toohello zapisane wyszukiwanie **mapy usługi**.  Są to zapytania utworzone specjalnie na potrzeby tej analizy.  Kliknij zapytanie **5 procesów najbardziej obciążających procesor CPU serwera acmetomcat**.

![Zapisane wyszukiwanie](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


To zapytanie zwraca listę hello 5 pierwszych procesy używające procesora na **acmetomcat**.  Możesz sprawdzić hello zapytania tooget język zapytań toohello wprowadzenie wyszukiwań dziennika.  Jeśli planuje się procesów hello na innych komputerach, można zmodyfikować tooretrieve zapytania hello tych informacji.

W takim przypadku zobaczysz, proces tworzenia kopii zapasowej hello spójnie zajmuje około 60% serwera aplikacji hello Procesora.  Jest dość oczywiste, że ten nowy proces jest odpowiedzialny za problem z wydajnością.  Nasze rozwiązaniem byłoby oczywiście tooremove nowy oprogramowania serwera aplikacji hello kopii zapasowej.  Firma Microsoft może faktycznie wykorzystać żądanego stanu konfiguracji (DSC) zarządzana przez zasady toodefine usługi Automatyzacja Azure, które upewnij się, że ten proces nigdy nie uruchamia się w tych systemach krytycznych.


## <a name="summary-points"></a>Punkty podsumowujące
- [Mapa usługi](operations-management-suite-service-map.md) udostępnia widok całej aplikacji nawet wtedy, gdy nie znasz wszystkich jej serwerów i zależności.
- Mapa usług udostępnia dane zbierane przez inne toohelp rozwiązań OMS możesz pokazane problemy z aplikacji i jej podstawowej infrastruktury.
- [Zaloguj się wyszukiwanie](../log-analytics/log-analytics-log-searches.md) pozwalają toodrill w dół do określonych danych zebranych w repozytorium analizy dzienników hello.    

## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej o [mapie usługi](operations-management-suite-service-map.md).
- [Wdróż i skonfiguruj](operations-management-suite-service-map-configure.md) mapę usługi.
- Dowiedz się więcej o usłudze [Log Analytics](../log-analytics/log-analytics-overview.md), która jest wymagana, aby korzystać z mapy usługi, i zawiera dane operacyjne przechowywane przez agentów.