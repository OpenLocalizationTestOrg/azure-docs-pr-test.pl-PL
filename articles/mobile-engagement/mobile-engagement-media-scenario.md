---
title: "aaaAzure implementacji usługi Mobile Engagement dla aplikacji z nośnika"
description: "Nośnik aplikacji scenariusza tooimplement usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a495eb790993a30d5c03802aa9e6404fea983d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a>Wdrożenie usługi Mobile Engagement z aplikacji z nośnika
## <a name="overview"></a>Omówienie
Jan jest kierownikiem przenośnych projektu firmy big nośnika. Niedawno on uruchomiony nowej aplikacji, która ma liczbę bardzo duże pobierania. On osiągnęła jego cele do pobrania, ale nadal jego wrócić na Investment(ROI) dla każdego użytkownika spełnia jego wymagania. 

Jan zidentyfikował już dlaczego jego ROI jest zbyt niski. Użytkownicy często Zatrzymaj przy użyciu jego aplikacji po tylko 2 tygodnie, a większość z nich nie wrócić. Maciej chce tooincrease hello przechowywania swoich aplikacji.

Po zakończeniu niektórych początkowego testowania on dowiedziała się po zaangażuje jego użytkowników z powiadomień wypychanych mają zwykle toocontinue przy użyciu jego aplikacji. Również użytkowników, które były nieaktywne często zwróci toohello aplikacji, w zależności od tego powiadomienia, który wysyła on je. Jan decyduje tooinvest w rodzaju Program zaangażowania dla swojej aplikacji, która używa zaawansowane korzystających z powiadomień wypychanych.

Jan ostatnio zapoznał hello [usługi Azure Mobile Engagement - Getting Started Guide z najlepszymi rozwiązaniami](mobile-engagement-getting-started-best-practices.md) oraz podjęła tooimplement hello zalecenia z podręcznika hello.

## <a name="objectives-and-kpis"></a>Celów i wskaźników KPI
Spełnia wymagania najważniejszych uczestników Jan w aplikacji. Jak użytkownicy uzyskują dostęp do jego nośnika biznesowa jest generowany na podstawie reklam. Zwiększenie zawartości używane dla każdego użytkownika, Jan zwiększa jego przychodów. Wszystkie zgodzić się na jednym z głównych celów: tooincrease sprzedaży z ads o 25%. Tworzenie one toomeasure firm kluczowych wskaźników wydajności (KPI) i dysk ten cel

* Liczba reklam kliknięty na użytkownika
* Ile strony artykułu odwiedzone (na użytkownika / sesji / tygodniowo / miesięcznie...)
* Co to są Ulubione kategorie

Na podstawie jego Jan spotkania z najważniejszych uczestników został on zdefiniowany jego biznesowe wskaźniki KPI dotyczące. Wykonuje, część 1 hello [usługi Azure Mobile Engagement - Getting Started Guide z najlepszymi rozwiązaniami](mobile-engagement-getting-started-best-practices.md). 

Następnie tworzy powitania po tooensure zaangażowania kluczowych wskaźników wydajności, osiągnięcia celów:

* Monitorowanie przechowywania za pośrednictwem powitania po interwałów: codziennie, co tydzień, co dwa tygodnie i miesięczne.
* Liczba aktywnych użytkowników
* Klasyfikacja aplikacji Hello w aplikacji hello przechowuje

Na podstawie zaleceń z hello zespół IT, powitania po techniczne kluczowych wskaźników wydajności zostały dodane hello tooanswer następujące pytania:

* Co to jest ścieżka do użytkownika (odwiedzenia strony, która ilu użytkowników czas poświęcony na jego)
* Liczba awarii (Crash) i zgłaszanie usterek napotkał na sesję?
* Które wersje systemu operacyjnego działają moich użytkowników?
* Co to jest hello średni rozmiar ekranu dla moich użytkowników?
* Jakiego rodzaju połączenia z Internetem masz moich użytkowników?

Dla poszczególnych wskaźników on klasyfikuje dane hello wymagane i on rejestruje w hello właściwego położenia jego podręcznikowym.

## <a name="engagement-program-and-integration"></a>Program zaangażowania i integracja
Teraz tego Jan zakończył określenie jego wskaźników KPI, przechodzi jego fazy strategia zaangażowania przez definiowanie 4 zaangażowania i ich cele:![][1]

Jan przejdzie głębiej przez wyszczególnieniem powiadomień wypychanych dla każdego programu. Powiadomienia wypychane są definiowane przez pięć elementów:

1. Cel: co to jest celem hello hello powiadomień
2. Jak można osiągnąć cel hello
3. Cel: kto otrzyma powiadomienie hello?
4. Zawartość: Co to jest treść hello i format hello hello powiadomienia (w App/Out z aplikacji)
5. Po wybraniu: co to jest hello najlepsze toosend obecnie tego powiadomienia wypychane
   
    ![][2]

Aby uzyskać więcej informacji można znaleźć toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).

Według toohello część 2 hello oficjalny dokument Jan używa toodefine sekcji docelowej danych ma toocollect, jak i zapisów jego Tag planowanie wspólnie z rozwiązaniem hello tooimplement zespołu IT. Po 1 tydzień wdrożenia oraz testów akceptacyjnych przez użytkowników Jan na koniec można uruchamiać swoje programy.

## <a name="program-results"></a>Program wyników
później, 4 miesięcy Jan przegląda parametrów programy. Hello Program powitalny i tygodniowego Program hello są spełniane jego celów. zmniejsza liczbę Hello użytkownika z tylko jedną sesję, więcej funkcji aplikacji hello są używane i ma podwójny hello liczbę połączeń na tydzień.

Witaj **nieaktywne Program** pomaga zrozumieć tendencji użytkownika John. Wygląda na to, że 15% hello nieaktywnych użytkowników wróć toohello aplikacji. Jednak większość z nich nie pozostają aktywne więcej niż 1 miesiąc. Jan przewiduje potencjalnych optymalizacji sekwencji przy użyciu dodatkowych powiadomień i rozszerzanie jego wybranej zawartości.

Witaj **odnajdywania Program** nie działa prawidłowo. Zwiększa ona cross sprzedaży, ale nie ma wystarczającej ilości tooreach jego celów. Jan Określa, że nie ma wystarczającej ilości danych toomake odpowiednich elementów docelowych i zaproponować odpowiedniej zawartości. On zatrzymuje ten program i koncentruje się na wysyłanie "powiadomień wypychanych redakcyjne" przy użyciu usługi Azure Mobile Engagement. Powiadomienia wypychane toosend rozwiązanie CMS już jego dziennikarze i nie mają toochange.

Jan decyduje hello toouse interfejsu API Reach czyli interfejsu API REST protokołu HTTP, który umożliwia zarządzanie kampanie Zasięgowe bez konieczności interfejs sieci Web AZME toouse. Wybranie tej metody oznacza Jan może zbierać dane hello on musi i umożliwić jego składniki zapisywania tookeep przy użyciu hello rozwiązanie CMS.

tooensure, że funkcja działa prawidłowo, Jan zapyta czujność toobe zespołu IT na powitania następujące punkty:

1. **Systemy operacyjne** : wszystkie mają własne reguły powiadomień wypychanych tooadministrate, więc Jan decyduje toolist wszystkie przypadki i kontroli jeśli jego obsługa hello interfejsów API.
   Np.: System Android wypychania umożliwia duży obraz, który nie jest hello z systemem iOS.
2. **Przedział czasu**: Jacek chce interfejsu API, który hello przedział czasu i ustaw toocampaigns zakończenia. Maciej chce toopreserve użytkowników z dowolnego sabotaż destrukcyjne powiadomień.
3. **Kategorie**: zespołu marketingu przygotowuje szablonu dla każdego typu alertu. Jan zapyta kategorii tooset zespołu IT w hello interfejsu API.

Po niektórych testów Jan jest spełniony. Interfejs API toothis Dziękujemy, dziennikarze nadal może wysyłać powiadomienia wypychane przy użyciu ich CMS i usługi Azure Mobile Engagement zbiera wszystkie dane behawioralnej dla nich

Po te 4 najpierw miesiące, wyniki odzwierciedlają dobrej ogólnej wydajności oraz zapewnia ufności Jan i jego tablicy ROI na zwiększa użytkownika na 15% i przenośnych sprzedaży reprezentują 17,5 cala % całkowitej sprzedaży, wzrost % 7.5 tylko czterech miesięcy.

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
