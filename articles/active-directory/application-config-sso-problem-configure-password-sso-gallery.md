---
title: "Problem podczas konfiguracji hasła logowanie jednokrotne dla aplikacji w galerii Azure AD | Dokumentacja firmy Microsoft"
description: "Zrozumienie kroju osób typowe problemy podczas konfigurowania haseł logowanie jednokrotne dla aplikacji, które są już wyświetlane w galerii aplikacji usługi Azure AD"
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
ms.openlocfilehash: 58d29996a922fac6d295e753ba5d66d32e745a57
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Problem podczas konfiguracji hasła logowanie jednokrotne dla aplikacji w galerii Azure AD

Ten artykuł ułatwia zrozumienie kroju osób typowe problemy podczas konfigurowania **hasło logowania jednokrotnego** przy użyciu aplikacji do galerii Azure AD.

## <a name="credentials-are-filled-in-but-the-extension-does-not-submit-them"></a>Poświadczenia są wypełniane, ale rozszerzenie nie przekazywać

Zazwyczaj dzieje się tak, jeśli zmieniła się z dostawcą aplikacji ich strona logowania ostatnio Aby dodać pole, zmień identyfikator źródłowego się, że użyliśmy wykryć pola Nazwa użytkownika i hasło lub zmodyfikować sposób logowania wystąpić działa w przypadku ich aplikacji. Na szczęście w wielu przypadkach firmy Microsoft może współpracować z dostawcami aplikacji w celu szybkiego rozwiązywania tych problemów.

Gdy firma Microsoft udostępnia technologie, aby automatycznie Wykryj, kiedy te integracji break, ale czasami nie możemy znaleźć od razu te problemy lub ich zająć trochę czasu, aby rozwiązać problem. W przypadku, gdy jeden z tych integracji nie działa prawidłowo, prosimy o wyrażenie po otwarciu sprawy pomocy technicznej, a my naprawimy go jak najszybciej.

Oprócz tego **w przypadku kontaktu z dostawcą tej aplikacji,** **wysyłać je sposób** , firma Microsoft może pracować z nimi natywnie integracja aplikacji z usługą Azure Active Directory. Możesz wysłać z dostawcą, aby [listę aplikacji w galerii aplikacji usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) do ich pracy.

## <a name="credentials-are-filled-in-and-submitted-but-the-page-indicates-the-credentials-are-incorrect"></a>Poświadczenia są wypełnione i przesłane, ale strona wskazuje, że poświadczenia są nieprawidłowe

Aby rozwiązać ten problem, sprawdź najpierw następujące czynności:

-   Użytkownik pierwszej próby **Zaloguj się do witryny sieci Web aplikacji bezpośrednio** przy użyciu poświadczeń przechowywanych dla nich.

  * To zrobić, wybrać użytkownika, kliknij przycisk **zaktualizować poświadczenia** znajdującego się na **kafelka aplikacji** w **aplikacje** sekcji [panelu dostępu aplikacji](https://myapps.microsoft.com/) ich aktualizacji do najnowszej znane pracy nazwy użytkownika i hasła.

   * Jeśli użytkownik lub inny administrator przypisane poświadczenia dla tego użytkownika, znaleźć użytkownika lub grupy aplikacji przydziału, przechodząc do **użytkownicy i grupy** aplikacji, wybierając przypisania i klikając pozycję **poświadczenia aktualizacji** przycisku.

-   Jeśli użytkownik jest przypisany własnymi poświadczeniami, ma użytkownika **wyboru należy upewnić się, że ich hasła nie wygasł w aplikacji** , a jeśli tak, **aktualizacja wygasłego hasła** logując się do aplikacji bezpośrednio.

   * Po zaktualizowaniu hasło aplikacji żądania użytkownika do kliknięcia **zaktualizować poświadczenia** znajdującego się na **kafelka aplikacji** w **aplikacje** sekcji [panelu dostępu aplikacji](https://myapps.microsoft.com/) ich aktualizacji do najnowszej znane pracy nazwy użytkownika i hasła.

   * Jeśli użytkownik lub inny administrator przypisane poświadczenia dla tego użytkownika, znaleźć użytkownika lub grupy aplikacji przydziału, przechodząc do **użytkownicy i grupy** aplikacji, wybierając przypisania i klikając pozycję **poświadczenia aktualizacji** przycisku.

-   Użytkownik powinien zaktualizować rozszerzenia przeglądarki panel dostępu, wykonując poniższe kroki w [jak zainstalować rozszerzenie przeglądarki panelu dostępu](#how-to-install-the-access-panel-browser-extension) sekcji.

-   Upewnij się, że rozszerzenie przeglądarki panel dostępu jest uruchomiony i włączone w przeglądarce użytkownika.

-   Upewnij się, że użytkownicy nie próbuje zalogować się do aplikacji w panelu dostępu podczas w **incognito, przeglądanie inPrivate lub prywatnej tryb**. Rozszerzenie panelu dostępu nie jest obsługiwana w tych trybach.

W przypadku, gdy to nie zadziała, może to być to zostało zmienione na stronie aplikacji, który uległ tymczasowo integracji aplikacji z usługą Azure AD. Na przykład to może wystąpić, gdy wprowadza się z dostawcą aplikacji w danych wejściowych, co powoduje, że automatyczne integracji, takich jak własnej, aby przerwać automatycznie skrypt na ich strona, która zależy od ręczne vs. Na szczęście w wielu przypadkach firmy Microsoft może współpracować z dostawcami aplikacji w celu szybkiego rozwiązywania tych problemów.

Gdy firma Microsoft udostępnia technologie, aby automatycznie Wykryj, kiedy te integracji break, ale czasami nie możemy znaleźć od razu te problemy lub ich zająć trochę czasu, aby rozwiązać problem. W przypadku, gdy jeden z tych integracji nie działa prawidłowo, prosimy o wyrażenie po otwarciu sprawy pomocy technicznej, a my naprawimy go jak najszybciej.

Oprócz tego **w przypadku kontaktu z dostawcą tej aplikacji,** **wysyłać je sposób** , firma Microsoft może pracować z nimi natywnie integracja aplikacji z usługą Azure Active Directory. Możesz wysłać z dostawcą, aby [listę aplikacji w galerii aplikacji usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) do ich pracy.

## <a name="the-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a>Rozszerzenie działania w Chrome, a program Firefox, ale nie w programie Internet Explorer

Istnieją dwa główne przyczyny tego problemu:

-   W zależności od ustawienia zabezpieczeń włączone w programie Internet Explorer, jeśli witryna sieci Web nie jest częścią **zaufane**, czasami naszych skryptu zablokować dostęp do wykonywania dla aplikacji.

  *  Aby rozwiązać ten problem, poinstruuj użytkowników, aby **Dodaj witrynę sieci Web aplikacji** do **Zaufane witryny** listy w ich **ustawień zabezpieczeń programu Internet Explorer**. Możesz wysłać użytkownikom [sposób dodawania witryny do listy zaufanych witryn](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) artykuł, aby uzyskać szczegółowe instrukcje.

-   W rzadkich przypadkach walidacji zabezpieczeń programu Internet Explorer mogą wywoływać stronę, aby załadować wolniej niż wykonanie naszych skryptu.

   * Niestety ta sytuacja zależy od wersji przeglądarki, szybkość komputera lub odwiedzi witrynę. W takim przypadku zaleca się z obsługą, możemy naprawić integracji dla tej określonej aplikacji.

Oprócz tego **w przypadku kontaktu z dostawcą tej aplikacji,** **wysyłać je sposób** , firma Microsoft może pracować z nimi natywnie integracja aplikacji z usługą Azure Active Directory. Możesz wysłać z dostawcą, aby [listę aplikacji w galerii aplikacji usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) do ich pracy.

## <a name="check-if-the-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a>Sprawdź, czy strona logowania aplikacji został ostatnio zmieniony lub wymaga dodatkowego pola

Jeśli strona logowania aplikacji zmienił znacząco, czasami powoduje naszych integracji przerwanie. Przykładem jest dostawca aplikacji dodaje znak w polu, captcha lub uwierzytelnianie wieloskładnikowe się swoimi doświadczeniami. Na szczęście w wielu przypadkach firmy Microsoft może współpracować z dostawcami aplikacji w celu szybkiego rozwiązywania tych problemów.

Gdy firma Microsoft udostępnia technologie, aby automatycznie Wykryj, kiedy te integracji break, ale czasami nie możemy znaleźć od razu te problemy. W przeciwnym razie one zająć trochę czasu, aby rozwiązać problem. W przypadku, gdy jeden z tych integracji nie działa prawidłowo, prosimy o wyrażenie otwieranie sprawy pomocy technicznej, a my naprawimy go jak najszybciej.

Oprócz tego **w przypadku kontaktu z dostawcą tej aplikacji,** **wysyłać je sposób** , firma Microsoft może pracować z nimi natywnie integracja aplikacji z usługą Azure Active Directory. Możesz wysłać z dostawcą, aby [listę aplikacji w galerii aplikacji usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) do ich pracy.

## <a name="how-to-install-the-access-panel-browser-extension"></a>Jak zainstalować rozszerzenie przeglądarki panelu dostępu

Aby zainstalować rozszerzenie przeglądarki panelu dostępu, wykonaj następujące czynności:

1.  Otwórz [panelu dostępu](https://myapps.microsoft.com) w jednym z obsługiwanych przeglądarkach i zaloguj się jako **użytkownika** w usługi Azure AD.

2.  Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w panelu dostępu.

3.  W oknie komunikatu z pytaniem do zainstalowania oprogramowania, zaznaczyć **Zainstaluj teraz**.

4.  Oparte na przeglądarce być kierowane do łącza pobierania. **Dodaj** rozszerzenia do przeglądarki.

5.  Jeśli przeglądarka pytanie, wybierz albo **włączyć** lub **Zezwalaj** rozszerzenia.

6.  Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.

7.  Zaloguj się do panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji

Może również pobrać rozszerzenia dla programu Chrome, a program Firefox z bezpośrednich łączy poniżej:

-   [Rozszerzenie panelu dostępu Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Rozszerzenie panelu dostępu Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a>Następne kroki
[Podaj logowanie jednokrotne do aplikacji przy użyciu serwera Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)

