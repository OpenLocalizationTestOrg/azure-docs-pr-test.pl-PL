---
title: aaaAzure Mobile Engagement Troubleshooting Guide - wypychanych/Reach
description: "Rozwiązywanie problemów interakcji i powiadomienie użytkownika w usłudze Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3f1886b7-1fdd-47f4-b6b0-d79f158d5ef3
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4ee0b34b9b753a98ccf24863acb28a5dc76bfb95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-push-and-reach-issues"></a>Podręcznik rozwiązywania problemów dotyczących wypychania i dostarczania
Witaj poniżej przedstawiono możliwe problemy, które mogą się pojawić w sposób usługi Azure Mobile Engagement wysyła informacje tooyour użytkownicy.

## <a name="push-failures"></a>Błędy wypychania
### <a name="issue"></a>Problem
* Wypchnięcia nie działają (w aplikacji poza aplikacji lub obie).

### <a name="causes"></a>Powoduje, że
* Wiele razy awarii wypychania jest wskazanie, że usługi Azure Mobile Engagement, zasięg lub innego zaawansowanych funkcji usługi Azure Mobile Engagement nie jest poprawnie zintegrowana lub uaktualnienie jest wymagany w hello SDK toofix znany problem dotyczący nowa platforma systemu operacyjnego lub urządzenia.
* Test tylko wypychania w aplikacji i po prostu toodetermine wypychanych z aplikacji, jeśli wystąpił problem z aplikacji lub w aplikacji.
* Test z zarówno hello interfejsu użytkownika, jak i hello interfejsu API jako rozwiązywania problemów toosee krok, jakie dodatkowe informacje o błędzie jest dostępna obu tych miejscach.
* Poza aplikacją wypchnięć nie będzie działać, chyba że zarówno usługi Azure Mobile Engagement i zasięgu są zintegrowane w hello zestawu SDK.
* Wypchnięcia nie będzie działać, jeśli certyfikaty są nieprawidłowe lub są za pomocą vs produkcyjną. DEV poprawnie (tylko iOS). (**Uwaga:** "poza aplikacją" powiadomień wypychanych nie można dostarczać tooiOS, jeśli masz zarówno programowanie hello (deweloperów) i produkcji (produkcyjną) aplikacji na zainstalowanych wersji hello takie same urządzenia od tokenu zabezpieczającego hello skojarzone przy użyciu certyfikatu może być unieważniona przez firmę Apple. tooresolve ten problem, odinstaluj zarówno produkcyjną wersji aplikacji, jak i hello deweloperów i ponownie zainstalować jedną wersję na urządzeniu tylko jest hello.)
* Poza aplikacją liczby wypychania są obsługiwane inaczej w różnych platform (iOS przedstawia informacje o mniej niż Android Jeśli natywnego wypchnięć są wyłączone na urządzeniu, powitalne interfejsu API może zapewnić więcej informacji niż hello interfejsu użytkownika Statystyka wypychania).
* Poza aplikacją wypchnięć mogą zostać zablokowane przez klientów na poziomie systemu operacyjnego (iOS i Android).
* Poza aplikacją wypchnięć będzie wyświetlana jako wyłączona w hello Azure Mobile Engagement w interfejsie użytkownika, jeśli nie są poprawnie zintegrowane, ale może się nie powieść dyskretnie z hello interfejsu API.
* W aplikacji wypchnięć nie będzie działać, chyba że zarówno usługi Azure Mobile Engagement i zasięgu są zintegrowane w hello zestawu SDK.
* Wypchnięcia usługi GCM i ADM nie będzie działać, chyba że hello SDK (tylko Android) są zintegrowane usługi Azure Mobile Engagement i hello określonego serwera.
* W aplikacji i poza aplikacji wypchnięć powinny być testowane oddzielnie toodetermine Jeśli jest to problem wypychania lub Reach.
* W aplikacji wypchnięć wymagają danej aplikacji hello Otwórz toobe odebrane.
* W aplikacji wypchnięć są często toobe Instalatora filtrowane według znaczników informacje o opcjonalnych lub rezygnacji z aplikacji.
* Jeśli używasz kategorię niestandardową w zasięgu toodisplay w aplikacji powiadomienia, należy toofollow hello poprawne cyklu życia hello powiadomień, w przeciwnym razie hello powiadomień nie może wyczyścić podczas użytkownika hello je zamknąć.
* Uruchamiania bez daty zakończenia kampanii, urządzenie odbiera hello w powiadomienie aplikacji, ale nie wyświetla go jeszcze hello użytkownik będzie nadal odbierać hello powiadomień hello następnym zalogowaniu do aplikacji hello nawet wtedy, gdy zakończysz ręcznie hello kampanii.
* W przypadku problemów z hello Push interfejsu API upewnij się, czy na pewno toouse hello API wypychania zamiast hello interfejsu API Reach (ponieważ jest to częściej stosowana jest hello interfejsu API Reach) i że nie mylące hello "ładunku" i "zgłaszający" parametrów.
* Przetestowanie kampanii wypychania z obu urządzenie podłączone za pośrednictwem sieci Wi-Fi i sieci 3G tooeliminate hello połączenia sieciowego w postaci źródłem problemów.

## <a name="push-testing"></a>Wypychanie testowania
### <a name="issue"></a>Problem
* Wypchnięcia mogą być wysyłane do określonego urządzenia tooa oparte na identyfikatorem urządzenia.

### <a name="causes"></a>Powoduje, że
* Urządzenia testu są skonfigurowane inaczej dla każdej platformy, ale powoduje zdarzenie w aplikacji na urządzeniu testu i wyszukując identyfikator urządzenia w portalu hello powinny działać toofind identyfikator urządzenia dla wszystkich platform.
* Działanie urządzeń testowych z identyfikator IDFA vs. IDFV (tylko iOS).

## <a name="push-customization"></a>Dostosowywanie wypychania
### <a name="issue"></a>Problem
* Zaawansowane wypychania zawartości elementu nie będzie działać (znaczków, pierścienia, Włącz wibrację, obraz, itp.).
* Łącza z wypchnięć nie działają (poza aplikacji w aplikacji, tooa witryny sieci Web, lokalizacji tooa w aplikacji).
* Wypychania Statystyki wskazują, że nie jest wypychanej wysyłane tooas wiele osób zgodnie z oczekiwaniami (zbyt wiele lub zbyt mała liczba).
* Zduplikowany i odebranych dwa razy.
* Nie można zarejestrować urządzenie testowe dla usługi Azure Mobile Engagement wypycha (za pomocą własnych produkcyjną lub deweloperów aplikacji).

### <a name="causes"></a>Powoduje, że
* toolink tooa określonej lokalizacji w aplikacji wymaga "kategorie" (tylko Android).
* Głębokie Konsolidacja systemów tooredirect użytkowników tooan innej lokalizacji po kliknięciu przycisku powiadomienie wypychane muszą toobe utworzone w i zarządzane bezpośrednio przez Twojej aplikacji i hello systemu operacyjnego urządzenia nie przez usługi Mobile Engagement. (**Uwaga:** poza aplikacją powiadomień nie może połączyć bezpośrednio tooin lokalizacje aplikacji z systemem iOS jak w przypadku systemu Android.)
* Serwery zewnętrzne obrazu muszą toouse stanie toobe HTTP "GET" i "HEAD" dla szerszej wypchnięcia toowork (tylko Android).
* W kodzie, można wyłączyć agenta usługi Azure Mobile Engagement powitania po otwarciu hello klawiatury i ponownie uaktywnić hello Azure Mobile Engagement agenta po zamknięciu klawiatury hello tak, aby hello klawiatury nie mają wpływu na wygląd hello kod użytkownika powiadomienie (tylko iOS).
* Niektóre elementy nie działają w symulacji testu, ale tylko rzeczywistych kampanii (znaczków, pierścienia, Włącz wibrację, obraz, itp.).
* Za nie po stronie serwera, którego dane są rejestrowane, korzystając z przycisku hello "test" wypycha. Dane są rejestrowane tylko dla kampanie wypychania prawdziwe.
* toohelp izolowanie problemu, rozwiązywanie problemów z: test, symulować i rzeczywistych kampanii, ponieważ każdy z nich działać nieco inaczej.
* Witaj czas Twoje "w aplikacji" i "w dowolnym momencie" kampanii są zaplanowane toorun może mieć wpływ numery dostarczania ponieważ kampanii tylko będą dostarczane toousers, którzy są "w aplikacji", podczas wykonywania hello kampanii (i użytkowników, którzy mają ich ustawienia urządzenia ustaw tooreceive powiadomienia "poza aplikacją").
* Hello różnice między jak systemy Android i iOS dojścia poza powiadomienia z aplikacji, ułatwia trudne toodirectly porównywanie wypychania danych statystycznych dotyczących wersji dla systemu Android i iOS hello aplikacji. Android zawiera więcej informacji powiadomień z poziomu systemu operacyjnego niż iOS. Android raportów, gdy otrzymano, kliknięty lub usunięte w Centrum powiadomień hello natywnych powiadomień, ale z systemem iOS nie raportuje te informacje, chyba że zostanie kliknięty hello powiadomień. 
* Witaj główną przyczyną numery "wciśnięcia" różnią się od innego niż "dostarczane" numerów osiągnąć kampanii jest czy "w aplikacji" i "poza aplikacją" powiadomienia są zliczane inaczej. "W aplikacji" powiadomienia są obsługiwane przez usługi Mobile Engagement, ale "poza aplikacją" powiadomienia są obsługiwane przez Centrum powiadomień hello na powitania systemu operacyjnego urządzenia.

## <a name="push-targeting"></a>Wypychanie elementów docelowych
### <a name="issue"></a>Problem
* Wbudowane elementów docelowych nie działa zgodnie z oczekiwaniami.
* Informacje o aplikacji Tag przeznaczonych dla nie działa zgodnie z oczekiwaniami.
* Lokalizacja geograficzna elementów docelowych nie działa zgodnie z oczekiwaniami.
* Opcje języka nie działają zgodnie z oczekiwaniami.

### <a name="causes"></a>Powoduje, że
* Upewnij się, że zostały przekazane tagi informacje o aplikacji za pośrednictwem hello Azure Mobile Engagement w interfejsie użytkownika lub interfejsu API.
* Ograniczenia przepustowości hello szybkości lub wypychanej przydział wypychania na poziomie aplikacji hello lub ograniczanie odbiorców hello na poziomie kampanii hello uniemożliwia osoby odbieranie wypychanych określonych nawet wtedy, gdy spełniają innych kryteriów określania wartości docelowej. 
* Ustawienie "Język" jest inny niż docelowy na podstawie kraju lub ustawień regionalnych, które może również inne niż docelowy na podstawie lokalizacji geograficznej na podstawie lokalizacji telefonu lub GPS lokalizacji.
* Witaj w "domyślny język" hello jest wysyłany komunikat tooany klienta, który nie ma swojego urządzenia, ustaw tooone hello alternatywne języki, które określisz.

## <a name="push-scheduling"></a>Wypychanie planowania
### <a name="issue"></a>Problem
* Planowanie wypychania nie działa zgodnie z oczekiwaniami (wysyłane zbyt wczesny lub opóźnione).

### <a name="causes"></a>Powoduje, że
* Strefy czasowe można problemy związane z planowaniem, zwłaszcza w przypadku korzystania z użytkownicy końcowi hello strefy czasowej.
* Funkcje zaawansowane wypychania można opóźnić wypchnięć.
* Celem oparte na numer telefonu, którego ustawienia (zamiast znaczniki informacje o aplikacji) może opóźnić wypycha od usługi Azure Mobile Engagement może mieć toorequest danych czasu rzeczywistego telefonu hello przed wysłaniem wypychania.
* Kampanie utworzone bez daty zakończenia przechowywania wypychania hello lokalnie na urządzeniu hello i pokazać hello następnym otwarciu aplikacji hello nawet wtedy, gdy kończy się ręcznie hello kampanii.
* Uruchamianie więcej niż jednej kampanii na powitania jednocześnie może trwać dłużej tooscan czas bazy użytkowników (spróbuj tooonly start jednej kampanii w czasie z maksymalnie cztery, również docelowych tylko tooyour aktywnych użytkowników, dzięki czemu użytkownicy nie mają toobe skanowane).
* Jeśli używasz opcji "Ignoruj odbiorców, powiadomienia wypychane będą wysyłane toousers za pośrednictwem interfejsu API hello" hello w sekcji "Kampanii" hello kampanii Reach kampanii hello nie będzie automatycznie wysyłać, konieczne będzie toosend go ręcznie za pomocą interfejsu API Reach hello.
* Jeśli używasz kategorię niestandardową w zasięgu toodisplay w aplikacji powiadomienia, należy toofollow hello poprawne cyklu powiadomienia, w przeciwnym razie hello powiadomień nie może wyczyścić podczas użytkownika hello je zamknąć.

