---
title: "Aplikacja uwierzytelniania aaaMicrosoft Pomoc i obsługę techniczną | Dokumentacja firmy Microsoft"
description: "Zawiera listę często zadawanych pytań i odpowiedzi aplikacji Microsoft Authentication toohello pokrewne i Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f04d5bce-e99e-4f75-82d1-ef6369be3402
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: afba9b59ccaac60d022e8516fcf573dcfbf68af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-authenticator-app-faq"></a>Aplikacja uwierzytelniania firmy Microsoft — często zadawane pytania

Ten artykuł zawiera odpowiedzi często zadawane pytania otrzymujących o hello aplikacji Authenticator firmy Microsoft. Jeśli nie widzisz tooyour odpowiedzi na pytanie, przejdź toohello [forum aplikacji Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp). Mamy także innego często zadawane pytania dotyczące określonych funkcji w aplikacji hello [Zaloguj się przy użyciu telefonu — często zadawane pytania](microsoft-authenticator-app-phone-signin-faq.md).

aplikacji Microsoft Authenticator Hello zastępowane hello aplikacji Azure Authenticator, a jest hello zalecane aplikacji, gdy używasz usługi Azure Multi-Factor Authentication. Aplikacja Microsoft Authenticator Hello jest dostępna dla [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), i [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="frequently-asked-questions"></a>Często zadawane pytania

### <a name="what-are-hello-codes-in-hello-app-for-why-does-hello-number-keep-counting-down"></a>Co to są kody hello w aplikacji hello w? Dlaczego zachować zliczania hello liczbę w dół?

Po otwarciu aplikacji Microsoft Authenticator hello Zobacz hello konta, które zostały dodane i numer lub ośmiu sześciocyfrowy przez każde z nich. Może pojawić się czasomierza 30 sekund, licząc w.

Te kody są używane podczas logowania konta tooyour. Po wprowadzeniu nazwy użytkownika i hasła, może być zadawane tooenter kod weryfikacyjny. Otwórz hello Microsoft Authenticator aplikacji i skopiuj hello kod, który jest aktualnie wyświetlany. Wprowadź ten kod w hello toofinish strony logowania.

powód Hello kody hello jest zmiana co 30 sekund, aby nie używać dwukrotnie hello tego samego kodu. Nie jest jak hasło, że w przypadku powinien tooremember. pomysł Hello jest tylko osoby z telefonu tooyour dostępu bez informacji kod weryfikacyjny.

kody Hello nie wymagają internet lub danych, dzięki czemu nie trzeba tooworry o toosign usługę telefoniczna. Po zamknięciu aplikacji hello nie zachować uruchomione w tle hello i nie opróżnienia baterii. Możesz zamknąć aplikacji hello i Ignoruj, dopóki hello następnym logowaniu.  

### <a name="i-only-get-notifications-when-i-have-hello-app-open-if-hello-app-isnt-open-i-dont-get-any-notifications"></a>Gdy aplikacja hello otworzyć tylko uzyskać powiadomienia. Jeśli aplikacja hello nie jest otwarty, nie pojawia się powiadomienia.

Jeśli otrzymywać powiadomień, ale nie należy szumu lub Włącz wibrację pomimo Twojej dzwonka w, sprawdź najpierw hello ustawień aplikacji. Włącz dźwięk toouse aplikacji hello lub też z jego powiadomienia.

Jeśli w ogóle nie otrzymywać powiadomień, sprawdź hello w następujących przypadkach:

- Twój telefon znajduje się w trybie nie przeszkadzać lub cichego? Ten tryb może zapobiec wysyłanie powiadomień aplikacji.
- Możesz otrzymywać powiadomienia z innych aplikacji? Jeśli nie, może być problem z połączeń sieciowych hello na swój telefon lub hello kanału powiadomień systemu Android i Apple. Można rozwiązać pierwsza opcja hello w ustawienia telefonu, ale tootalk tooyour usługodawcy mogą wymagać, aby uzyskać pomoc dotyczącą hello druga opcja.
- Możesz otrzymywać powiadomienia dla niektórych kont w aplikacji hello, ale niekoniecznie? Jeśli tak, Usuń konto problematyczne hello z aplikacji i dodaj go ponownie tooenable powiadomień wypychanych. 

Jeśli nastąpiła sugestie dotyczące rozwiązywania, ale nadal występują problemy, Wyślij do nas dzienniki dla diagnostyki. Przejdź do ustawień aplikacji toohello, a następnie wybierz **— Pomoc i opinie** i **wysyłanie dzienników**. Następnie przejdź toohello [forum aplikacji Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) i Daj nam znać, co problem został wyświetlony i jakie kroki próbowałeś wykonanej do tej pory. 

### <a name="im-already-using-hello-microsoft-authenticator-application-for-verification-codes-how-do-i-switch-tooone-click-push-notifications"></a>Witaj aplikacji Microsoft Authenticator już jest używany do używania kodów weryfikacyjnych. Jak zmienić powiadomienia wypychane kliknij tooone?
Zatwierdzanie logowanie za pomocą powiadomień wypychanych jest dostępna tylko dla osobistego konta Microsoft lub pracy oraz szkolnego konta Microsoft, nie dla kont innych firm, takich jak Google lub usługi Facebook. Jeśli masz służbowe konto Microsoft organizacji można wybrać toodisable tę opcję.

Korzystanie z konta osobistego konta Microsoft i mają tooswitch za pośrednictwem toopush powiadomienia, należy najpierw tooadd konta ponownie. Ponownie zarejestrować urządzenie hello przy użyciu konta i Konfigurowanie powiadomień wypychanych.  

Jeśli używasz Authenticator firmy Microsoft dla swojego konta firmowego lub szkolnego, a następnie organizacji decyduje o tym, czy powiadomienia o jednym kliknięciem tooallow.

### <a name="do-one-click-push-notifications-work-for-non-microsoft-accounts"></a>Powiadomienia wypychane jednym kliknięciem działają dla kont innych niż firmy Microsoft?
Nie, powiadomienia wypychane działa tylko z kontami Microsoft i kontami usługi Azure Active Directory. Konto służbowe używa konta usługi Azure AD, może wyłączyć tę funkcję.  

### <a name="i-restored-my-device-from-a-backup-and-my-account-codes-are-missing-or-not-working-what-happened"></a>Moje urządzenie zostały przywrócone z kopii zapasowej, a kody mojego konta są Brak lub nie działa. Co się stało?
Ze względów bezpieczeństwa firma Microsoft nie należy przywracać kont z kopii zapasowej aplikacji.  Po przywróceniu aplikacji hello usuwanie kont i dodać je ponownie.

### <a name="i-got-a-new-device-how-do-i-remove-hello-microsoft-authenticator-app-from-my-old-device-and-move-toohello-new-one"></a>Otrzymano nowe urządzenie. Jak usunąć aplikację Microsoft Authenticator hello z urządzenie starego i Przenieś toohello nowy
Dodawanie hello Microsoft Authenticator aplikacji tooa nowego urządzenia nie są automatycznie usuwane go od innych urządzeń. toomanage urządzeń, które są skonfigurowane dla Twojego konta, odwiedź stronę hello tę samą witrynę Użyj weryfikacji dwuetapowej toomanage i wybierz tooremove starego aplikacji.

W przypadku osobistego konta Microsoft, jest tej witryny sieci Web z [zabezpieczenia konta](https://account.microsoft.com/security) strony. Dla konta Microsoft służbowe tej witryny sieci Web mogą być [MyApps](https://myapps.microsoft.com) lub niestandardowych portalu, który skonfigurował Twojej organizacji.

### <a name="how-do-i-remove-an-account-from-hello-app"></a>Jak usunąć konto z aplikacji hello?
* iOS: Z ekranu głównego hello, przejdź w lewo na kafelku konta. Wybierz pozycję **Usuń**.
* Windows Phone: Z ekranu głównego hello, wybierz przycisk menu hello, następnie **edycji kont**. Wybierz hello **X** następnej toohello nazwy konta.
* System android: Z ekranu głównego hello, wybierz przycisk menu hello, następnie **edycji kont**. Wybierz hello **X** następnej toohello nazwy konta.

Jeśli masz urządzenie jest zarejestrowane w swojej organizacji, może być konieczne toocomplete tooremove dodatkowego kroku Twoje konto. Na tych urządzeniach aplikacji Microsoft Authenticator hello jest automatycznie dodawane jako administrator urządzenia. Jeśli chcesz, aby aplikacja hello Odinstaluj toocompletely, należy toofirst wyrejestrować aplikacji hello w ustawieniach aplikacji hello.

### <a name="why-does-hello-app-request-so-many-permissions"></a>Dlaczego aplikacji hello zażądać uprawnień tyle?
Pełna lista uprawnień, które firma Microsoft może poprosić o i sposób ich użycia w aplikacji hello. Hello określone uprawnienia, dostępne są zależne od typu hello telefonu, do których masz.

* **Aparat fotograficzny**: korzystamy z kodów tooscan QR aparatu po dodaniu pracy, szkole lub kont innych niż Microsoft.
* **Kontakty i phone**: po zalogowaniu osobiste konto Microsoft spróbujemy toosimplify hello procesu przez wyszukiwanie istniejących kont używanych w telefonie.
* **SMS**: po zalogowaniu swojego osobistego konta Microsoft na powitania po raz pierwszy, mamy toomake się, że wyszukiwania numeru telefonu hello co mamy w rekordzie. Możemy wysyłać telefonu toohello wiadomości tekstowych, którego pobrano aplikacji hello. wiadomość Hello zawiera kod weryfikacyjny 6-8 cyfr. Zamiast monitem toofind tego kodu i wprowadź go w aplikacji hello znaleźliśmy go w wiadomość hello za Ciebie.
* **Rysowanie w innych aplikacjach**: po otrzymaniu tooverify powiadomień swoją tożsamość, wyświetli powiadomienie za pośrednictwem innych aplikacji, która może być uruchomiona.
* **Odbieranie danych z hello internet**: to uprawnienie jest wymagane do wysyłania powiadomień.
* **Uniemożliwić phone uśpiony**: Jeśli zarejestrować urządzenie w Twojej organizacji, mogą zmieniać tych zasad na Twój telefon.
* **Kontrolowanie wibrację**: można wybrać, czy chcesz wibrację zawsze po otrzymaniu tooverify powiadomień Twoją tożsamość.
* **Korzystanie ze sprzętu odcisk palca**: niektóre kont służbowych wymagają dodatkowych numeru PIN przy każdym zweryfikować Twoją tożsamość. proces hello toomake jest łatwiejsze, firma Microsoft pozwala toouse odcisku palca zamiast wprowadzania hello numeru PIN.
* **Wyświetlanie połączeń sieciowych**: podczas dodawania konta Microsoft hello aplikacja wymaga połączenia sieć i internet.
* **Odczytu zawartości hello magazynu**: to uprawnienie jest używana tylko, gdy zgłaszasz problem techniczny za pomocą ustawień aplikacji hello. Niektóre informacje z magazynu są zbierane toodiagnose hello problem.
* **Pełny dostęp do sieci**: to uprawnienie jest wymagane do wysyłania powiadomień tooverify Twoją tożsamość.
* **Uruchom przy uruchamianiu**: należy ponownie uruchomić telefon, to uprawnienie zadba nadal otrzymywać powiadomienia tooverify Twoją tożsamość.

### <a name="why-does-hello-microsoft-authenticator-app-allow-you-tooapprove-a-request-without-unlocking-hello-device"></a>Dlaczego czy hello aplikacji uwierzytelniania firmy Microsoft pozwala tooapprove żądania bez odblokowywania urządzenia hello?

Nie masz toounlock urządzenia tooapprove weryfikację żądań, ponieważ tooprove wystarczy mieć telefon z Tobą. Włączono weryfikację dwuetapową wymaga potwierdzania dwie czynności — element, który znasz i operacją, której masz. Witaj, co wiesz jest Twoje hasło. Witaj, co masz jest Twój telefon (skonfigurować przy użyciu aplikacji Microsoft Authenticator hello i zarejestrowany jako dowód MFA). W związku z tym o hello telefonu i zatwierdzania żądania hello spełnia hello kryteria hello drugiego etapu uwierzytelniania. 

### <a name="what-does-hello-lock-icon-in-hello-account-list-mean"></a>Co oznacza ikoną kłódki hello hello listy kont?

ikona kłódki Hello wskazuje urządzenia hello jest zarejestrowany w usłudze Azure AD i zarejestrowane toohello konta. Rejestracja urządzeń dla systemu iOS odbywa się podczas rejestracji Microsoft Intune.

## <a name="next-steps"></a>Następne kroki

### <a name="contact-us"></a>Skontaktuj się z nami
Jeśli nie został tutaj odpowiedzi na pytanie, chcemy toohear od użytkownika. Przejdź toohello [forum aplikacji Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) toopost pytania i get pomoc od społeczności hello, lub zostaw komentarz na tej stronie.


### <a name="related-topics"></a>Powiązane tematy
* [O weryfikacji dwuetapowej](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) kont Microsoft
* [Wystąpił problem w trakcie weryfikacji dwuetapowej](multi-factor-authentication-end-user-troubleshoot.md) dla swojego konta firmowego lub szkolnego?
* [Użyj toosign Microsoft Authenticator hello w na telefonie](microsoft-authenticator-app-phone-signin-faq.md)

