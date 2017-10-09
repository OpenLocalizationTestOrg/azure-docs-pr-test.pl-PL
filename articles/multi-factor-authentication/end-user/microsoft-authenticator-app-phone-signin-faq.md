---
title: "aaaMicrosoft uwierzytelniania phone logowania — konta platformy Azure i Microsoft | Dokumentacja firmy Microsoft"
description: "Użyj toosign Twojego telefonu w tooyour konta Microsoft, zamiast wpisywania hasła. Ten artykuł zawiera odpowiedzi na często zadawane pytania o tej funkcji."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: a4911ff580b3ffa078299ad706d099330b75a2e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-with-your-phone-not-your-password"></a>Zaloguj się przy użyciu telefonu, nie pamiętasz hasła

aplikacji Microsoft Authenticator Hello pomaga chronić swoje konta, wykonując weryfikację dwuetapową, po wprowadź swoje hasło. Ale czy wiesz, że go całkowicie zastąpić hello hasło dla swojego osobistego konta Microsoft? 

Ta funkcja jest dostępna w systemach iOS i urządzeniach z systemem Android i współpracuje z osobistego konta Microsoft. 

## <a name="how-it-works"></a>Jak to działa

Użyj wielu z aplikacji Microsoft Authenticator hello na potrzeby weryfikacji dwuetapowej po zalogowaniu tooyour konta Microsoft. Wpisz hasło, następnie przejdź tooeither aplikacji toohello zatwierdzić powiadomienie lub kod weryfikacyjny. Z telefonu logowania Pomiń hello hasła i wykonaj weryfikację tożsamości na telefonie. Ponieważ logowanie telefonu jest typem weryfikację dwuetapową, nadal należy tooprovide operacją, której znasz i operacją, masz tooverify Twoją tożsamość. Hello phone jest nadal hello operacją, której masz i numeru PIN lub klucza biometryczne Twój telefon jest hello, co należy wiedzieć. 

## <a name="how-tooget-started"></a>Sposób uruchamiania tooget

toosign w tooyour osobistego konta Microsoft z telefonem, wykonaj następujące kroki: 

1. Włącz logowanie telefonu dla swojego konta. 

  - Jeśli nie masz aplikacji Microsoft Authenticator hello jeszcze, zainstalować i dodać osobistego konta Microsoft, zgodnie z toohello kroki na powitania [strony Microsoft Authenticator](microsoft-authenticator-app-how-to.md). Nowo dodanego konta są włączane automatycznie, dlatego możesz teraz toogo dobra.

  - Jeśli używasz już Authenticator firmy Microsoft na potrzeby weryfikacji dwuetapowej, wybierz konto na stronie głównej aplikacji hello i wybierz **włączyć logowanie phone** z menu rozwijanego hello.

  >[!NOTE] 
  >tooprotect Twojego konta, wymagamy numeru PIN lub blokady biometrycznego na urządzeniu. Jeśli zachowasz telefonu odblokowane aplikacji hello wyskakującej żądanie zapytaniem tooset blokadę przed włączeniem logowania telefonu. 

3. Większość stron, gdzie należy zwykle wprowadzić hasło konta Microsoft ma linku **zamiast tego użyć aplikacji**. Wybierz ten toosign łączy się przy użyciu telefonu. 

4. Firma Microsoft wysyła na telefon tooyour powiadomień. Zatwierdzanie toosign powiadomień hello tooyour konta.   

## <a name="faq"></a>Często zadawane pytania 

### <a name="how-is-signing-in-with-my-phone-more-secure-than-typing-a-password"></a>Jak się zalogować Mój telefon bezpieczniejsze niż wpisanie hasła?  

Obecnie większość użytkowników Zaloguj tooweb witryn lub aplikacji przy użyciu nazwy użytkownika i hasła.  Niestety hasła są często utraty, kradzieży lub odgadnięty przez hakerów. Po skonfigurowaniu toosign aplikacji Microsoft Authenticator hello w możemy wygenerować klucz na telefonie można odblokować konto. Ten klucz z hello numeru PIN są chronione lub biometryczne już użycie w telefonie.  Gdy zalogujesz się przy użyciu telefonu, ten klucz jest używany tooprove tożsamości bezpiecznie przy użyciu dwóch czynniki — Witaj phone sam i toounlock Twojego możliwości go. 

klucz Hello używany jest podobne klawiszy toohello w specyfikacji FIDO Alliance UAF hello i Windows Hello. Informacje o danych jest tylko mnie używane tooprotect hello klucz lokalnie i jest nigdy nie wysyłane do lub przechowywane w chmurze hello. 
 
### <a name="where-can-i-use-my-phone-tooreplace-my-password-and-where-would-i-still-need-hello-password"></a>Gdzie mogę używać mojej tooreplace phone hasła i gdzie nadal potrzebna hello hasło?  

Obecnie funkcja logowania telefonu hello działa tylko z aplikacji sieci web i usług, które są obsługiwane przez osobistego konta Microsoft, iOS lub aplikacje dla systemu Android korzystających z osobistego konta Microsoft i aplikacji w systemie Windows 10, które używają osobistego konta Microsoft. Po zarejestrowaniu tooone tych witryn sieci web lub aplikacji, na stronie hello, w którym zwykle wprowadzić hasło to łącze, które mówi **zamiast tego użyć aplikacji**. 

Logowanie telefonu nie może być używane toounlock komputera z systemem Windows, konsoli XBOX lub wszystkie pulpitu wersje aplikacji firmy Microsoft, takich jak aplikacje pakietu Office w tej chwili. 
 
### <a name="does-this-replace-two-step-verification-should-i-turn-it-off"></a>To zastępuje weryfikację dwuetapową? Należy wyłączyć go?   

Czasami. Pracujemy nad rozszerzania zakresu hello logowania telefon, ale obecnie nadal istnieją miejsca w ekosystemie Microsoft hello, które nie obsługują tego. W tych miejscach nadal używamy weryfikacji dwuetapowej dla bezpieczne logowanie. Z tego powodu nie, użytkownik nie należy wyłączyć weryfikację dwuetapową dla konta. 
 
### <a name="okay-if-i-keep-two-step-verification-turned-on-for-my-account-do-i-have-tooapprove-two-notifications"></a>Zgoda Jeśli aktualizować włączona dla mojego konta włączono weryfikację dwuetapową, są dostępne dwa powiadomienia tooapprove?

Nie, nie. Logowanie konta Microsoft z telefonem tooyour traktowana jako weryfikacji dwuetapowej. Zamiast wpisywać swoje hasło, a następnie zatwierdzanie powiadomienie potwierdzenia tożsamości wiadomo, jak toounlock telefonie, a następnie zatwierdzanie powiadomienie. Firma Microsoft nie wyśle drugi tooapprove powiadomień.

### <a name="what-if-i-lose-my-phone-or-dont-have-it-with-me-how-can-i-access-my-account"></a>Co w przypadku utraty Mój telefon, lub nie ma go przy użyciu elementu me, jak można uzyskać dostęp Moje konto?  

Zawsze można kliknąć przycisk **zamiast tego użyć hasła** na powitania strony logowania tooswitch kopii toousing hasła. Należy pamiętać, że jeśli używasz weryfikację dwuetapową, nadal należy drugi tooverify — metoda logowanie. Dlatego zdecydowanie zalecamy toomake upewnić się, że informacje dodatkowe, aktualne zabezpieczeń na Twoim koncie. Możesz zarządzać informacje zabezpieczające pod https://account.live.com/proofs/manage. 
 
### <a name="how-do-i-stop-using-this-feature-and-go-back-tooentering-my-password"></a>Jak zatrzymać za pomocą tej funkcji i wrócić do poprzedniej strony tooentering hasło?

Kliknij przycisk **zamiast tego użyć hasła** po zalogowaniu. Firma Microsoft Pamiętaj najnowszych wybór i ofertę, która przez domyślny hello następnym logowaniu. Kiedykolwiek toosigning wstecz toogo się przy użyciu telefonu, kliknij przycisk **zamiast tego użyć aplikacji**. 
 
### <a name="can-i-use-hello-app-toosign-in-tooall-my-accounts-with-microsoft"></a>Można używać toosign aplikacji hello w tooall mojego konta Microsoft?   
Ta funkcja jest dostępna dla osobistego konta Microsoft tylko w tej chwili. 
 
### <a name="can-i-sign-into-my-pc-with-my-phone"></a>Można zarejestrować na komputer z Mój telefon?  
Dla komputera zaleca się logowanie się przy użyciu usługi Windows Hello w systemie Windows 10 przy użyciu Twojej krój, odcisk palca lub numeru PIN.   
 
### <a name="can-i-sign-in-with-my-windows-phone"></a>Można zalogować się przy użyciu mojej Windows Phone?  
W tej chwili nie opracowywana tę funkcję dla hello Authenticator firmy Microsoft na Windows Phone. 

## <a name="next-steps"></a>Następne kroki
Jeśli nie zostały pobrane hello aplikacji Authenticator firmy Microsoft, należy go wyewidencjonować. Aplikacja Hello jest dostępna dla [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), i logowania telefonu jest dostępny w aplikacji Microsoft Authenticator powitania dla [Android](http://go.microsoft.com/fwlink/?Linkid=825072) i [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

Jeśli masz pytania dotyczące aplikacji hello ogólnie rzecz biorąc, Przyjrzyjmy się hello [uwierzytelniania firmy Microsoft — często zadawane pytania](microsoft-authenticator-app-faq.md)
