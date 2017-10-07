---
title: "aaaProblem Konfigurowanie hasła logowanie jednokrotne dla aplikacji w galerii Azure AD | Dokumentacja firmy Microsoft"
description: "Zrozumienie hello typowych problemów osób krój, podczas konfigurowania haseł logowanie jednokrotne dla aplikacji, które są już wyświetlane w hello galerii aplikacji usługi Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 78c37c52453c375bf7ccbca6df5c9008be4ce642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Problem podczas konfiguracji hasła logowanie jednokrotne dla aplikacji w galerii Azure AD

W tym artykule pomóc toounderstand hello typowych problemów osób krój podczas konfigurowania **hasło logowania jednokrotnego** przy użyciu aplikacji do galerii Azure AD.

## <a name="credentials-are-filled-in-but-hello-extension-does-not-submit-them"></a>Poświadczenia są wypełniane, ale hello rozszerzenia nie przekazywać

Dzieje się to zwykle logowania zmiana dostawcy aplikacji hello ostatnio strony tooadd pola, zmienić identyfikatora źródłowego użyliśmy hello toodetect pola Nazwa użytkownika i hasło lub zmodyfikować sposób logowania hello wystąpić działa w przypadku ich aplikacji. Na szczęście w wielu przypadkach firmy Microsoft może współpracować z aplikacji dostawców toorapidly Rozwiąż te problemy.

Gdy firma Microsoft ma tooautomatically technologii Wykryj, kiedy te integracji break, ale czasami nie jesteśmy w stanie toofind te prawa, które zadań lub wykonać niektóre problemy czasu toofix. W przypadku powitania po jednej z tych integracji nie działa prawidłowo, prosimy o wyrażenie po otwarciu sprawy pomocy technicznej, a my naprawimy go jak najszybciej.

W toothis dodanie **w przypadku kontaktu z dostawcą tej aplikacji,** **wysyłać je sposób** , firma Microsoft może współpracować z ich toonatively integracji aplikacji z usługą Azure Active Directory. Możesz wysłać hello dostawcy toohello [listę aplikacji w galerii aplikacji usługi Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget je uruchomić.

## <a name="credentials-are-filled-in-and-submitted-but-hello-page-indicates-hello-credentials-are-incorrect"></a>Poświadczenia są wypełnione i przesłane, ale strona hello wskazuje hello poświadczenia są niepoprawne

Ten problem, pierwszego następującego hello wyboru tooresolve:

-   Użytkownik hello najpierw spróbuj użyć zbyt**Zaloguj toohello aplikacji witryny sieci Web bezpośrednio** z hello poświadczenia przechowywane dla nich.

  * Jeśli to zrobić, mieć użytkownika powitania kliknij hello **zaktualizować poświadczenia** przycisk na powitania **kafelka aplikacji** w hello **aplikacje** sekcji hello [aplikacji Dostęp do panelu](https://myapps.microsoft.com/) tooupdate ich toohello najnowszych znane pracy nazwy użytkownika i hasła.

   * Jeśli użytkownik lub innego poświadczenia hello przypisanego administratora dla tego użytkownika, znaleźć hello użytkownika lub grupy aplikacji przypisania przechodząc toohello **użytkownicy i grupy** kartę aplikacji hello, wybierając hello przypisania i Kliknięcie przycisku hello **poświadczenia aktualizacji** przycisku.

-   Jeśli użytkownik hello przypisane własnymi poświadczeniami, mają użytkownika hello **Sprawdź toobe się upewnić, że ich hasła nie wygasł aplikacji hello** , a jeśli tak, **aktualizacja wygasłego hasła** logując się toohello bezpośrednio do aplikacji.

   * Po aktualizacji hasła hello w aplikacji hello żądania hello użytkownika tooclick hello **zaktualizować poświadczenia** przycisk na powitania **kafelka aplikacji** w hello **aplikacji** sekcja hello [panelu dostępu aplikacji](https://myapps.microsoft.com/) tooupdate ich toohello najnowszych znane pracy nazwy użytkownika i hasła.

   * Jeśli użytkownik lub innego poświadczenia hello przypisanego administratora dla tego użytkownika, znaleźć hello użytkownika lub grupy aplikacji przypisania przechodząc toohello **użytkownicy i grupy** kartę aplikacji hello, wybierając hello przypisania i Kliknięcie przycisku hello **poświadczenia aktualizacji** przycisku.

-   Ma rozszerzenie przeglądarki panelu dostępu hello hello użytkownika aktualizacji, wykonując poniższe czynności hello w hello [jak tooinstall hello rozszerzenia przeglądarki panelu dostępu](#how-to-install-the-access-panel-browser-extension) sekcji.

-   Upewnij się, że rozszerzenie przeglądarki panelu dostępu hello jest uruchomiony i włączone w przeglądarce użytkownika.

-   Upewnij się, że użytkownicy nie próbujesz toosign w toohello aplikacji hello panelu dostępu podczas w **incognito, przeglądanie inPrivate lub prywatnej tryb**. rozszerzenie panelu dostępu Hello nie jest obsługiwana w tych trybach.

W przypadku, gdy to nie zadziała, może to być przypadku hello, że nastąpiła zmiana po stronie aplikacji hello, który uległ tymczasowo aplikacji hello integracji z usługą Azure AD. Na przykład to może wystąpić, gdy wprowadzono dostawcy aplikacji hello skrypt na ich strona, która zależy od ręczne vs automatycznie danych wejściowych, co powoduje, że automatyczne integracji, takich jak własnej, toobreak. Na szczęście w wielu przypadkach firmy Microsoft może współpracować z aplikacji dostawców toorapidly Rozwiąż te problemy.

Gdy firma Microsoft ma tooautomatically technologii Wykryj, kiedy te integracji break, ale czasami nie jesteśmy w stanie toofind te prawa, które zadań lub wykonać niektóre problemy czasu toofix. W przypadku powitania po jednej z tych integracji nie działa prawidłowo, prosimy o wyrażenie po otwarciu sprawy pomocy technicznej, a my naprawimy go jak najszybciej.

W toothis dodanie **w przypadku kontaktu z dostawcą tej aplikacji,** **wysyłać je sposób** , firma Microsoft może współpracować z ich toonatively integracji aplikacji z usługą Azure Active Directory. Możesz wysłać hello dostawcy toohello [listę aplikacji w galerii aplikacji usługi Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget je uruchomić.

## <a name="hello-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a>rozszerzenie Hello działa w Chrome, a program Firefox, ale nie w programie Internet Explorer

Istnieją dwa główne przyczyny problemu toothis:

-   W zależności od hello ustawienia zabezpieczeń włączone w programie Internet Explorer, jeśli hello witryny sieci Web nie jest częścią **zaufane**, czasami zablokowane wykonywania dla aplikacji hello naszych skryptu.

  *  tooresolve, poinstruuj użytkowników hello zbyt**Dodaj witrynę sieci Web aplikacji hello** toohello **Zaufane witryny** listy w ich **ustawień zabezpieczeń programu Internet Explorer**. Możesz wysłać toohello Twojego użytkowników [jak tooadd toomy witryn zaufanych witryn listy](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) artykuł, aby uzyskać szczegółowe instrukcje.

-   W rzadkich przypadkach walidacji zabezpieczeń programu Internet Explorer mogą wywoływać tooload strony hello wolniej niż wykonanie hello naszych skryptu.

   * Niestety ta sytuacja może się różnić w zależności od wersji przeglądarki hello, szybkość komputera lub odwiedzi witrynę. W takim przypadku zaleca się z obsługą, możemy naprawić hello integracji dla tej określonej aplikacji.

W toothis dodanie **w przypadku kontaktu z dostawcą tej aplikacji,** **wysyłać je sposób** , firma Microsoft może współpracować z ich toonatively integracji aplikacji z usługą Azure Active Directory. Możesz wysłać hello dostawcy toohello [listę aplikacji w galerii aplikacji usługi Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget je uruchomić.

## <a name="check-if-hello-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a>Sprawdź, czy hello strony logowania aplikacji został ostatnio zmieniony lub wymaga dodatkowego pola

Jeśli strona logowania aplikacji hello zmienił znacząco, czasami powoduje naszych toobreak integracji. Przykładem jest dostawca aplikacji dodaje znak w polu captcha, lub napotyka tootheir uwierzytelnianie wieloskładnikowe. Na szczęście w wielu przypadkach firmy Microsoft może współpracować z aplikacji dostawców toorapidly Rozwiąż te problemy.

Gdy firma Microsoft ma tooautomatically technologii Wykryj, kiedy te integracji break, ale czasami nie jesteśmy w stanie toofind te problemy od razu. W przeciwnym razie potrwać niektórych toofix czasu. W przypadku powitania po jednej z tych integracji nie działa prawidłowo, prosimy o wyrażenie otwieranie sprawy pomocy technicznej, a my naprawimy go jak najszybciej.

W toothis dodanie **w przypadku kontaktu z dostawcą tej aplikacji,** **wysyłać je sposób** , firma Microsoft może współpracować z ich toonatively integracji aplikacji z usługą Azure Active Directory. Możesz wysłać hello dostawcy toohello [listę aplikacji w galerii aplikacji usługi Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget je uruchomić.

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Jak tooinstall hello rozszerzenia przeglądarki panelu dostępu

hello tooinstall rozszerzenia przeglądarki panelu dostępu, wykonaj poniższe kroki hello:

1.  Otwórz hello [panelu dostępu](https://myapps.microsoft.com) w jednym z hello obsługiwane przeglądarki i zaloguj się jako **użytkownika** w usługi Azure AD.

2.  Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w hello panelu dostępu.

3.  Hello monitu pytaniem tooinstall hello oprogramowania, zaznaczyć **Zainstaluj teraz**.

4.  Oparte na przeglądarce można ukierunkowanej toohello łącze. **Dodaj** hello rozszerzenia tooyour przeglądarki.

5.  Jeśli przeglądarka pytanie, wybierz tooeither **włączyć** lub **Zezwalaj** hello rozszerzenia.

6.  Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.

7.  Zaloguj się do hello panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji

Może również pobrać hello rozszerzenia dla programu Chrome, a program Firefox z poniższych linków bezpośrednich hello:

-   [Rozszerzenie panelu dostępu Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Rozszerzenie panelu dostępu Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a>Następne kroki
[Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)

