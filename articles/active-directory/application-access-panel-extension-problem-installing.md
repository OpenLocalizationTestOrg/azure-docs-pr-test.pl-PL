---
title: "Instalowanie rozszerzenia przeglądarki panelu dostępu do aplikacji hello aaaProblem | Dokumentacja firmy Microsoft"
description: "Jak toofix typowych błędów napotkanych podczas instalowania rozszerzenia przeglądarki panelu dostępu hello"
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
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a>Problem podczas instalowania rozszerzenia przeglądarki panelu dostępu do aplikacji hello

Witaj Panel dostępu jest oparte na sieci web portalu, co pozwoli na użytkownika mającego służbowe konto w usłudze Azure Active Directory (Azure AD) tooview, a następnie uruchom aplikacje oparte na chmurze administrator hello Azure AD udzielił im dostępu do. Użytkownik, który ma wersje usługi Azure AD umożliwia także grupami samoobsługi i funkcje zarządzania aplikacjami za pośrednictwem hello panelu dostępu. Witaj Panel dostępu jest oddzielony od hello portalu Azure i nie wymaga toohave użytkownicy subskrypcji platformy Azure.

toouse opartego na hasłach rejestracji jednokrotnej (SSO) w hello Panel dostępu, hello rozszerzenia Panelu dostępu należy zainstalować w przeglądarce użytkownika hello. To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Spełnia wymagania dotyczące przeglądarki dla hello panelu dostępu

Witaj panelu dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS. toouse opartego na hasłach rejestracji jednokrotnej (SSO) w hello Panel dostępu, hello rozszerzenia Panelu dostępu należy zainstalować w przeglądarce użytkownika hello. To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.

Logowanie Jednokrotne opartego na hasłach można przeglądarki hello przez użytkownika końcowego:

-   Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy

-   Krawędź w systemie Windows 10 Anniversary Edition lub nowszy 

-   Chrome — W systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych

-   Firefox 26.0 lub później — w systemie Windows XP z dodatkiem SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Jak tooinstall hello rozszerzenia przeglądarki panelu dostępu

hello tooinstall rozszerzenia przeglądarki panelu dostępu, wykonaj poniższe kroki hello:

1.  Otwórz hello [panelu dostępu](https://myapps.microsoft.com) w jednym z hello obsługiwane przeglądarki i zaloguj się jako **użytkownika** w usługi Azure AD.

2.  Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w hello panelu dostępu.

3.  Hello monitu pytaniem tooinstall hello oprogramowania, zaznaczyć **Zainstaluj teraz**.

4.  Oparte na przeglądarce można ukierunkowanej toohello łącze. **Dodaj** hello rozszerzenia tooyour przeglądarki.

5.  Jeśli przeglądarka pytanie, wybierz tooeither **włączyć** lub **Zezwalaj** hello rozszerzenia.

6.  Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.

7.  Zaloguj się do hello panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji

Może również pobrać hello rozszerzenia dla programu Chrome i krawędzi, z poniższe linki bezpośrednie hello:

-   [Rozszerzenie panelu dostępu Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Rozszerzenie panelu dostępu krawędzi](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Konfigurowanie zasad grupy dla programu Internet Explorer

Możesz skonfigurować zasady grupy, które pozwalają tooremotely instalacji hello panelu dostępu rozszerzenie programu Internet Explorer na komputerach użytkowników.

wymagania wstępne Hello obejmują:

-   Po skonfigurowaniu [usług domenowych w usłudze Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), i mieć przyłączone do domeny tooyour maszyny użytkowników.

-   Musi mieć hello "Edytuj ustawienia" uprawnień tooedit hello obiektu zasad grupy (GPO). Domyślnie to uprawnienie mają członkowie hello następujących grup zabezpieczeń: Administratorzy domeny, Administratorzy przedsiębiorstwa oraz Twórcy-właściciele zasad grupy. [Dowiedz się więcej](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Czynności opisane w samouczku hello [jak tooDeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy](active-directory-saas-ie-group-policy.md) instrukcje krok po kroku dotyczące sposobu tooconfigure hello zasad grupy i wdróż je toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Rozwiązywanie problemów z hello panelu dostępu w programie Internet Explorer

Wykonaj hello [rozwiązywanie hello rozszerzenia Panel dostępu dla programu Internet Explorer](active-directory-saas-ie-troubleshooting.md) przewodnik dostępu narzędzia diagnostycznego i instrukcje krok po kroku dotyczące konfigurowania hello rozszerzenia dla programu Internet Explorer.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Jeśli te kroki rozwiązywania problemów nie rozwiąże problemu hello

Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:

-   Identyfikator błędu korelacji

-   Nazwa UPN (adres e-mail użytkownika)

-   Dla identyfikatora dzierżawcy

-   Typ przeglądarki

-   Strefa czasowa i przedziału czasu/czasu podczas błąd występuje

-   Ślady fiddler

## <a name="next-steps"></a>Następne kroki
[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
