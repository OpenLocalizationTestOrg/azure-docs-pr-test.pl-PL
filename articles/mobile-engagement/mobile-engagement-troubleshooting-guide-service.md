---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - usługi"
description: "Rozwiązywanie problemów z przewodniki dotyczące usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a>Przewodnik rozwiązywania problemów dotyczących usługi
Witaj poniżej przedstawiono możliwe problemy, które mogą się pojawić w sposób uruchamiania usługi Azure Mobile Engagement.

## <a name="service-outages"></a>Awarie usługi
### <a name="issue"></a>Problem
* Problemy, które są wyświetlane toobe spowodowane awarie usługi systemu Azure Mobile Engagement.

### <a name="causes"></a>Powoduje, że
* Problemy, które pojawiają się toobe spowodowane Azure Mobile Engagement usługi awarii może być spowodowana przez kilka różnych problemów:
  * Izolowane problemy, które pierwotnie pojawiają się tooall systemowe usługi Azure Mobile Engagement
  * Znane problemy spowodowane awarii serwera (nie zawsze pokazuje stan serwera):
  * Planowanie opóźnienia, błędy docelowych, problemy aktualizacja wskaźnika, statystyki zatrzymania zbierania wypychania przestanie działać, interfejsu API przestają działać, nowe aplikacje lub użytkowników nie można utworzyć, błędy DNS i błędy przekroczenia limitu czasu w hello aplikacji, interfejsu API lub interfejsu użytkownika na urządzeniu.
  * Awarie zależności w chmurze [stan usługi Azure](http://status.azure.com/)
  * Awarie zależności usług (PNS) powiadomień wypychanych
  * Awarie sklepu z aplikacjami

1) toosee tootest, jeśli hello problem jest systemowych można przetestować hello sam funkcji z innego

* Usługa Azure Mobile Engagement zintegrowanych aplikacji
* Urządzenie testowe
* Wersja systemu operacyjnego urządzenia testu
* Kampanii
* Konta administratora
* Przeglądarka (tj., Firefox Chrome, itp.)
* Computer (Komputer)

2) tootest Jeśli hello problem wpływa tylko na powitania interfejsu użytkownika lub hello interfejsu API:

* Przetestuj hello sam funkcji z obu hello Azure Mobile Engagement w interfejsie użytkownika i hello Azure Mobile Engagement API.

3) tootest, jeśli jest hello problem z siecią telefon komórkowy:

* Testowanie podczas połączonych toohello Internetu za pośrednictwem sieci Wi-Fi i za pośrednictwem sieci 3G telefonu komórkowego.
* Upewnij się, czy Zapora nie blokuje tych portów lub adresy IP hello Azure Mobile Engagement.

4) tootest, jeśli jest hello problem z urządzeniem:

* Należy sprawdzić, czy urządzenie jest w stanie tooconnect tooAzure Mobile Engagement z innej aplikacji zintegrowane usługi Azure Mobile Engagement.
* Test, który może generować zdarzenia, zadań i awarii (Crash) na telefonie, którą można wyświetlić w hello Azure Mobile Engagement w interfejsie użytkownika. 
* Sprawdzić, czy można wysyłać powiadomienia wypychane z hello Azure Mobile Engagement UI tooyour urządzenia, zależnie od jego identyfikator urządzenia. 

5) tootest, jeśli jest hello problem z aplikacją:

* Instalowanie i testowanie aplikacji w emulatorze zamiast z fizycznego urządzenia:

6) tootest Jeśli hello problem dotyczy użytkownika tooend uaktualnień systemu operacyjnego urządzenia, które wymagają uaktualnienia tooresolve zestawu SDK:

* Przetestować aplikację na różnych urządzeniach z różnymi wersjami hello systemu operacyjnego.
* Upewnij się, że używasz najnowszej wersji hello hello zestawu SDK.

## <a name="connectivity-and-incorrect-information-issues"></a>Łączność i problemy nieprawidłowe informacje
### <a name="issue"></a>Problem
* Logowanie do problemów hello Azure Mobile Engagement w interfejsie użytkownika.
* Błędy połączenia z hello interfejsu API usługi Azure Mobile Engagement.
* Problemy z przekazywaniem tagi informacje o aplikacji za pośrednictwem hello interfejsu API urządzenia.
* Pobieranie dzienników lub wyeksportowanych danych z usługi Azure Mobile Engagement problemów.
* Niepoprawne informacje wyświetlone w hello Azure Mobile Engagement w interfejsie użytkownika.
* Niepoprawne informacje widoczne w dziennikach usługi Azure Mobile Engagement.

### <a name="causes"></a>Powoduje, że
* Upewnij się, że konto użytkownika ma wystarczające uprawnienia tooperform hello zadań.
* Potwierdź, że hello problem nie jest izolowane tooone komputera lub sieci lokalnej.
* Sprawdź, czy ten hello usługi Azure Mobile Engagement ma nie zgłoszone przerwy w działaniu.
* Upewnij się, czy pliki Tag informacje o aplikacji wykonaj wszystkie te reguły:
  * Użyj hello tylko zestaw znaków UTF8 (zestaw znaków ANSI hello nie jest obsługiwane).
  * Użyj przecinka "," jako separatora hello (przecinka można otworzyć usługi żądania toorequest toochange hello CSV znak separatora "," znak tooanother, np. średnikiem ";").
  * Użyj małe litery logiczna wartości "true" i "false".
  * Użyj pliku, który jest mniejszy niż hello maksymalny rozmiar pliku 35 MB.

