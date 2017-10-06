---
title: "wzorce użycia usługi Azure CDN aaaAnalyze | Dokumentacja firmy Microsoft"
description: "Można wyświetlić wzorców użycia sieci CDN przy użyciu hello następujące raporty: przepustowości, dane przesyłane, trafień, stany pamięci podręcznej, Stosunek trafień w pamięci podręcznej, przesłanych danych IPV4 i IPV6."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d27e6f60acaed66abb27d860c3a3e2e81c9f60cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Analizować wzorce użycia usługi Azure CDN

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Przewodnik Hello poniżej przechodzi przez hello kroki tooview hello podstawowych raportów za pośrednictwem portalu zarządzania hello Verizon profilów. Można również eksportować core analizy danych toostorage Centrum zdarzeń i analizy dzienników (oms) dla profilów zarówno Verizon i Akamai [za pośrednictwem portalu hello azure](cdn-log-analysis.md).

Można wyświetlić wzorców użycia sieci CDN przy użyciu hello następujące raporty:

* Przepustowość
* Przesyłane dane
* Liczba trafień
* Stany pamięci podręcznej
* Stosunek trafień w pamięci podręcznej
* Przesyłane dane IPv4 i IPV6

## <a name="accessing-core-reports"></a>Uzyskiwanie dostępu do raportów podstawowych
1. Blok profilu CDN hello, kliknij hello **Zarządzaj** przycisku.
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-reports/cdn-manage-btn.png)
   
    Otwiera portalu zarządzania Hello CDN.
2. Przesuń kursor myszy hello **Analytics** kartę, a następnie przesuń kursor myszy hello **raporty Core** wysuwane okno.  Polecenie hello żądanego raportu w hello menu.
   
    ![Portal zarządzania CDN — menu Raporty podstawowe](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>Przepustowość
Raport przepustowości Hello składa się z tabeli wykres i dane wskazujące hello przepustowości dla protokołu HTTP i HTTPS w określonym czasie. Możesz wyświetlić hello przepustowości przez wszystkie POP w sieci CDN lub określonego protokołu POP. Dzięki temu można tooview hello ruchu wzrostów i dystrybucji w sieci CDN POP w MB/s.

* Wybierz wszystkie węzły krawędzi toosee ruch ze wszystkich węzłów lub określonego regionu/węzła z listy rozwijanej hello.
* Wybierz danych Data zakresu tooview dzisiaj/ten tydzień/w tym miesiącu, itp. lub wprowadź niestandardowe daty, a następnie kliknij przycisk "Przejdź" toomake się, że wybór jest aktualizowany.
* Można wyeksportować i pobierania danych hello klikając hello programu excel znajdujący się obok ikony arkusza za "Przejdź".

Raport Hello jest aktualizowany co 5 minut.

![Raport przepustowości](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>Przesyłane dane
Ten raport składa się z tabeli wykres i dane wskazujące hello obciążenie ruchu HTTP i HTTPS w określonym czasie. Obciążenie ruchu hello można wyświetlić wszystkie POP w sieci CDN lub określonego protokołu POP. Dzięki temu można tooview hello ruchu wzrostów i dystrybucji w sieci CDN POP w GB.

* Wybierz wszystkie węzły krawędzi toosee ruch z wszystkich notatek lub określonego regionu/węzła z listy rozwijanej hello.
* Wybierz danych Data zakresu tooview dzisiaj/ten tydzień/w tym miesiącu, itp. lub wprowadź niestandardowe daty, a następnie kliknij przycisk "Przejdź" toomake się, że wybór jest aktualizowany.
* Można wyeksportować i pobierania danych hello klikając hello programu excel znajdujący się obok ikony arkusza za "Przejdź".

Raport Hello jest aktualizowany co 5 minut.

![Dane przesyłane raportu](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>Trafienia (kodów stanu)
Ten raport zawiera opis dystrybucji hello kodów stanu żądania dla zawartości. Każde żądanie zawartości wygeneruje kod stanu HTTP. Kod stanu Hello opisuje obsługi żądania hello POP krawędzi. Na przykład kody stanu 2xx wskazująca, że hello żądanie zostało obsłużone pomyślnie klienta tooa, podczas kod stanu 4xx oznacza, że wystąpił błąd. Aby uzyskać więcej informacji na temat kod stanu HTTP, zobacz [kodów stanu](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

* Wybierz danych Data zakresu tooview dzisiaj/ten tydzień/w tym miesiącu, itp. lub wprowadź niestandardowe daty, a następnie kliknij przycisk "Przejdź" toomake się, że wybór jest aktualizowany.
* Można wyeksportować i pobierania danych hello klikając hello programu excel arkusza znajdujący się obok zbyt "Przejdź".

![Liczba raportów](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>Stan pamięci podręcznej
Ten raport zawiera opis dystrybucji hello trafień w pamięci podręcznej i Chybienia w pamięci podręcznej dla żądania klienta. Ponieważ hello największą wydajność pochodzi z trafień w pamięci podręcznej, aby zoptymalizować szybkości dostarczania danych, minimalizując Chybienia pamięci podręcznej i trafień w pamięci podręcznej wygasła. Chybienia pamięci podręcznej można zmniejszyć przez skonfigurowanie sieci tooavoid serwera pochodzenia przypisywanie nagłówki odpowiedzi "no-cache", unikając buforowanie ciągu zapytania z wyjątkiem, w razie potrzeby ściśle i dzięki unikaniu kody odpowiedzi buforowalnej. Ważność dokonując zasobów max wieku tak długo, jak możliwe toominimize hello liczbę żądań toohello pochodzenia serwera można uniknąć trafień w pamięci podręcznej.

![Raport stany pamięci podręcznej](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>Stany głównej pamięci podręcznej obejmują:
* TCP_HIT: Obsługiwane od krawędzi. Hello obiektu w pamięci podręcznej, a nie przekroczył jego maksymalny wiek.
* TCP_MISS: Obsługiwane pochodzenia. Obiekt Hello nie był w pamięci podręcznej i hello odpowiedź była tooorigin Wstecz.
* TCP_EXPIRED _MISS: źródłem pochodzenia po ponowna Walidacja ze źródła. Obiekt Hello się w pamięci podręcznej, ale przekroczył jego maksymalny wiek. Ponowna Walidacja ze źródła spowodowała hello obiektu pamięci podręcznej zostanie zastąpiony nową odpowiedź od źródła.
* TCP_EXPIRED _HIT: pochodzący z krawędzi po ponowna Walidacja ze źródła. Obiekt Hello się w pamięci podręcznej, ale przekroczył jego maksymalny wiek. Ponowna Walidacja z serwera źródłowego hello spowodowała obiektu pamięci podręcznej hello jest nie mają być modyfikowane.
* Wybierz danych Data zakresu tooview dzisiaj/ten tydzień/w tym miesiącu, itp. lub wprowadź niestandardowe daty, a następnie kliknij przycisk "Przejdź" toomake się, że wybór jest aktualizowany.
* Można wyeksportować i pobierania danych hello klikając hello programu excel znajdujący się obok ikony arkusza za "Przejdź".

### <a name="full-list-of-cache-statuses"></a>Pełna lista stanów pamięci podręcznej
* TCP_HIT — ten stan jest zgłaszany, gdy żądanie jest udostępniany bezpośrednio z klienta toohello hello POP. Zasób natychmiast jest obsługiwana z POP, gdy są buforowane na kliencie toohello najbliższego punktu obecności hello i ma on prawidłowej, time-to-live lub czas wygaśnięcia. Czas wygaśnięcia jest określany przez hello następujące nagłówki odpowiedzi:
  
  * Cache-Control: s-maxage
  * Cache-Control: Maksymalna liczba wieku
  * Wygasa
* TCP_MISS — ten stan wskazuje, że buforowanej wersji hello żądanego zasobu nie został znaleziony na powitania POP najbliższego toohello klienta. Witaj zasobów będzie wymagane z serwera pochodzenia lub serwer tarczy pochodzenia. Jeśli serwer pochodzenia hello lub serwer tarczy pochodzenia hello zwraca zasób, zostanie obsłużone toohello klienta i buforowane na powitania klienta i serwera krawędzi hello. W przeciwnym razie wartość Kod stanu – 200 (np. 403 Zabroniony, nie można odnaleźć 404, itp.) zostaną zwrócone.
* _HIT TCP_EXPIRED — ten stan jest zgłaszany, gdy żądanie docelowe zasób wygasłe TTL, np. gdy zasobów hello max wieku wygasła, zostało obsłużone bezpośrednio z klienta toohello hello POP.
  
    Wygasłe żądanie zwykle powoduje serwer pochodzenia toohello żądanie ponownego sprawdzania poprawności. Aby TCP_EXPIRED _HIT toooccur powitania serwera źródłowego musi wskazywać, że nie istnieje nowsza wersja zasobów hello. Taka sytuacja zwykle spowoduje zaktualizowanie Cache-Control i Expires headers elementu zawartości.
* _MISS TCP_EXPIRED — ten stan jest zgłaszany, gdy nowszej wersji elementu wygasłe zawartości pamięci podręcznej jest udostępniane przez klienta toohello hello POP. Dzieje się tak, gdy wygaśnie hello TTL do buforowanych zasobów (np. ważność maksymalny wiek) i serwera pochodzenia hello zwraca nowsza wersja tego zasobu. Nowa wersja trwałego hello zostanie obsłużona klienta toohello zamiast hello wersja buforowana. Ponadto będą buforowane na serwerze granicznym hello i powitania klienta.
* CONFIG_NOCACHE — ten stan wskazuje, że odbiorcy konfiguracyjne na naszych krawędzi POP uniemożliwił hello zasobów pamięci podręcznej.
* Brak — ten stan wskazuje, czy Sprawdzanie aktualności zawartości pamięci podręcznej nie została wykonana.
* _MISS TCP_ CLIENT_REFRESH — ten stan jest zgłaszany, gdy klient HTTP (np. przeglądarki) wymusza tooretrieve krawędzi POP nowej wersji starych zasobów z serwera źródłowego hello.
  
    Domyślnie serwery zapobiega HTTP klienta wymuszania naszych tooretrieve serwerów krawędzi nowej wersji hello zasobów z serwera źródłowego hello.
* PARTIAL_HIT TCP_ — ten stan jest zgłaszany, gdy żądanie zakresu bajtów powoduje trafień dla częściowo buforowane zasobów. Witaj zażądał zakresu bajtów natychmiast jest udostępniany z hello POP toohello klienta.
* UNCACHEABLE — ten stan jest zgłaszany, gdy Cache-Control i Expires headers zasobów wskazują, że go mają nie być buforowane punktu obecności lub hello HTTP klienta. Te typy żądań są udostępniane z serwera źródłowego hello

## <a name="cache-hit-ratio"></a>Stosunek trafień w pamięci podręcznej
Ten raport wskazuje hello odsetek żądań z pamięci podręcznej, które były przekazywane bezpośrednio z pamięci podręcznej.

Raport Hello zawiera hello poniższe informacje:

* Witaj zażądał zawartości był buforowany w najbliższej żądający toohello hello POP.
* Witaj żądanie zostało obsłużone bezpośrednio z krawędzi hello naszej sieci.
* Żądanie hello nie wymagało ponownego sprawdzania poprawności z serwera źródłowego hello.

Witaj raportu nie zawiera:

* Żądań odrzuconych z powodu toocountry opcje filtrowania.
* Żądania dotyczące zasobów, których nagłówki wskazują, że nie powinny one zapisywane. Na przykład Cache-Control: prywatny, Cache-Control: nie-cache lub Pragma: nagłówków pamięci podręcznej nie uniemożliwi zasobów pamięci podręcznej.
* Żądania zakresu bajtów częściowo buforowane zawartości.

Formuła Hello jest: (TRAFIEŃ TCP_ / (TCP_ TRAFIEŃ + TCP_MISS)) * 100

* Wybierz danych Data zakresu tooview dzisiaj/ten tydzień/w tym miesiącu, itp. lub wprowadź niestandardowe daty, a następnie kliknij przycisk "Przejdź" toomake się, że wybór jest aktualizowany.
* Można wyeksportować i pobierania danych hello klikając hello programu excel znajdujący się obok ikony arkusza za "Przejdź".

![Raport Stosunek trafień w pamięci podręcznej](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>Przesyłane dane IPv4 i IPV6
Ten raport przedstawia rozkład użycia hello ruchu IPV4 vs IPV6.

![Przesyłane dane IPv4 i IPV6](./media/cdn-reports/cdn-ipv4-ipv6.png)

* Wybierz dane tooview zakres daty dla bieżącej/ten tydzień/tego miesiąca, itp., lub wprowadź niestandardowe daty.
* Następnie kliknij przycisk "Przejdź" toomake się, że wybór jest aktualizowany.

## <a name="considerations"></a>Zagadnienia do rozważenia
Raporty można tylko generowane w hello ostatnich 18 miesięcy.

