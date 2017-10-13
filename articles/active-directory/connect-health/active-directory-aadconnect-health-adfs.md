---
title: "Używanie programu Azure AD Connect Health z usługami AD FS | Microsoft Docs"
description: "To jest strona programu Azure AD Connect Health, która informuje, jak monitorować lokalną infrastrukturę usług AD FS."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
editor: curtand
ms.assetid: dc0e53d8-403e-462a-9543-164eaa7dd8b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7946f11d209e6341caa3a11e946fb1596e758277
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="monitor-ad-fs-using-azure-ad-connect-health"></a>Monitorowanie usług AD FS za pomocą programu Azure AD Connect Health
Poniższa dokumentacja dotyczy monitorowania infrastruktury usług AD FS przy użyciu programu Azure AD Connect Health. Aby uzyskać informacje na temat monitorowania programu Azure AD Connect (synchronizacja) za pomocą programu Azure AD Connect Health, zobacz [Używanie programu Azure AD Connect Health w celu synchronizacji](active-directory-aadconnect-health-sync.md). Ponadto, aby uzyskać informacje na temat monitorowania Usług domenowych Active Directory za pomocą programu Azure AD Connect Health, zobacz [Używanie programu Azure AD Connect Health z usługami AD DS](active-directory-aadconnect-health-adds.md).

## <a name="alerts-for-ad-fs"></a>Alerty dla usług AD FS
Sekcja Alerty programu Azure AD Connect Health udostępnia listę aktywnych alertów. Każdy alert zawiera istotne informacje, kroki do rozwiązania problemu i linki do powiązanej dokumentacji.

Kliknij dwukrotnie aktywny lub rozwiązany alert, aby otworzyć nowy blok z dodatkowymi informacjami, krokami, jakie można podjąć, aby rozwiązać alert, oraz linkami do dodatkowej dokumentacji. Można również wyświetlić dane historyczne na temat alertów, które zostały rozwiązane w przeszłości.

![Portal programu Azure AD Connect Health](./media/active-directory-aadconnect-health/alert2.png)

## <a name="usage-analytics-for-ad-fs"></a>Analiza użycia usług AD FS
Analiza użycia programu Azure AD Connect Health analizuje ruch na serwerach federacyjnych związany z uwierzytelnianiem. Kliknij dwukrotnie pole analizy użycia, aby otworzyć blok analizy użycia, który zawiera metryki i grupowania.

> [!NOTE]
> Aby móc korzystać z analizy użycia dla usług AD FS, należy się upewnić, że inspekcja usług AD FS jest włączona. Aby uzyskać więcej informacji, zobacz [Włączanie inspekcji dla usług AD FS](active-directory-aadconnect-health-agent-install.md#enable-auditing-for-ad-fs).
>
>

![Portal programu Azure AD Connect Health](./media/active-directory-aadconnect-health/report1.png)

Aby wybrać dodatkowe metryki, określić zakres czasu lub zmienić grupowanie, kliknij prawym przyciskiem myszy wykres analizy użycia i wybierz pozycję Edytuj wykres. Następnie możesz określić zakres czasu, wybrać inne metryki oraz zmienić grupowanie. Za pomocą odpowiednich parametrów funkcji „grupuj według” opisanych w poniższej sekcji możesz zobaczyć rozkład ruchu uwierzytelniania w oparciu o różne „metryki” i pogrupować wszystkie metryki.

**Metryka: Łączna liczba żądań** — łączna liczba żądań przetworzonych przez serwery usług AD FS.

|Grupuj według | Co oznacza grupowanie i dlaczego jest przydatne? |
| --- | --- |
| Wszyscy | Pokazuje łączną liczbę żądań przetworzonych przez wszystkie serwery usług AD FS.|
| Aplikacja | Grupuj wszystkie żądania na podstawie docelowej jednostki zależnej. To grupowanie przydaje się, aby sprawdzić, która aplikacja ma największy procentowy udział w całkowitym ruchu sieciowym. |
|  Serwer |Grupuje wszystkie żądania na podstawie serwera, który przetwarzał żądanie. Dzięki takiemu grupowaniu można sprawdzić rozkład obciążenia dla całego ruchu sieciowego.
| Urządzenia dołączone w miejscu pracy |Grupuje wszystkie te żądania, które pochodzą z urządzeń dołączonych w miejscu pracy (znane). Dzięki takiemu grupowaniu można sprawdzić, czy do Twoich zasobów uzyskują dostęp urządzenia nieznane dla infrastruktury do obsługi tożsamości. |
|  Metoda uwierzytelniania | Grupuje wszystkie żądania na podstawie metody uwierzytelniania użytej podczas uwierzytelniania. Dzięki takiemu grupowaniu można się dowiedzieć, jaka metoda uwierzytelniania jest najczęściej używana podczas uwierzytelniania. Możliwe są następujące metody uwierzytelniania <ol> <li>Zintegrowane uwierzytelnianie systemu Windows (system Windows)</li> <li>Uwierzytelnianie oparte na formularzach (Formularze)</li> <li>Logowanie jednokrotne (SSO, Single Sign On)</li> <li>Uwierzytelnianie w oparciu o certyfikat standardu X509 (Certyfikat)</li> <br>Jeśli serwery federacyjne otrzymają żądanie przez plik cookie SSO, żądanie jest traktowane jako SSO (logowanie jednokrotne). W takim przypadku, jeśli plik cookie jest ważny, użytkownik nie jest proszony o dostarczenie poświadczeń i od razu uzyskuje dostęp do aplikacji. To zachowanie ma miejsce często, gdy ma się wiele jednostek zależnych chronionych przez serwery federacyjne. |
| Lokalizacja sieciowa | Grupuje wszystkie żądania na podstawie lokalizacji sieciowej użytkownika. Może to być zarówno sieć intranet, jak i ekstranet. Dzięki takiemu grupowaniu można sprawdzić, jaki procent ruchu sieciowego pochodzi z intranetu, a jaki z ekstranetu. |


**Metryka: Łączna liczba żądań zakończonych niepowodzeniem** — łączna liczba żądań zakończonych niepowodzeniem przetworzonych przez usługę federacyjną. (Ta metryka jest dostępna tylko w usługach AD FS dla systemu Windows Server 2012 R2)

|Grupuj według | Co oznacza grupowanie i dlaczego jest przydatne? |
| --- | --- |
| Typ błędu | Wyświetla liczbę błędów na podstawie wcześniej zdefiniowanych typów błędów. Takie grupowanie umożliwia zapoznanie się z najczęściej popełnianymi typami błędów. <ul><li>Nieprawidłowa nazwa użytkownika lub hasło: Błędy spowodowane nieprawidłową nazwą użytkownika lub nieprawidłowym hasłem.</li> <li>„Zablokowany ekstranet”: Niepowodzenia spowodowane żądaniami otrzymanymi od użytkownika, któremu został zablokowany dostęp do sieci ekstranet. </li><li> „Hasło nieaktualne”: Niepowodzenia spowodowane logowaniem się użytkowników przy użyciu nieaktualnych haseł.</li><li>„Konto wyłączone”: Niepowodzenia spowodowane logowaniem się użytkowników przy użyciu wyłączonych kont.</li><li>„Uwierzytelnianie urządzenia”: Niepowodzenia spowodowane nieudanymi uwierzytelnieniami użytkowników przy użyciu uwierzytelniania urządzenia.</li><li>„Uwierzytelnianie certyfikatu użytkownika”: Niepowodzenia wynikające z nieudanych uwierzytelnień użytkowników z powodu nieprawidłowego certyfikatu.</li><li>„MFA”: Niepowodzenia wynikające z nieudanych uwierzytelnień użytkowników przy użyciu usługi Multi Factor Authentication.</li><li>„Inne poświadczenia”: „Autoryzacja wystawiania”: Niepowodzenia spowodowane błędami autoryzacji.</li><li>„Delegowanie wystawiania”: Niepowodzenia spowodowane błędami delegowania wystawiania.</li><li>„Akceptacja tokenu”: Niepowodzenia spowodowane odrzuceniem przez usługi AD FS tokenu od innego dostawcy tożsamości.</li><li>„Protokół”: Niepowodzenie z powodu błędów protokołu.</li><li>„Nieznane”: Wszystkie inne rodzaje niepowodzeń. Wszystkie inne niepowodzenia, które nie mieszczą się w zdefiniowanych kategoriach.</li> |
| Serwer | Grupuje błędy według serwera. Dzięki takiemu grupowaniu można sprawdzić, jak wygląda rozkład błędów między serwerami. Nierównomierny rozkład może oznaczać uszkodzenie serwera. |
| Lokalizacja sieciowa | Grupuje błędy na podstawie lokalizacji sieciowej żądań (intranet lub ekstranet). Dzięki takiemu grupowaniu można sprawdzić typy żądań, które kończą się niepowodzeniem. |
|  Aplikacja | Grupuje niepowodzenia na podstawie aplikacji docelowej (jednostki zależnej). Dzięki takiemu grupowaniu można sprawdzić, która aplikacja docelowa ma do czynienia z największą liczbą błędów. |

**Metryka: Liczba użytkowników** — średnia liczba unikatowych użytkowników aktywnie uwierzytelnianych za pomocą usług AD FS.

|Grupuj według | Co oznacza grupowanie i dlaczego jest przydatne? |
| --- | --- |
|Wszyscy |Ta metryka zapewnia liczenie średniej liczby użytkowników korzystających z usługi federacyjnej w wybranym przedziale czasu. Użytkownicy nie są zgrupowani. <br>Średnia zależy od wybranego przedziału czasu. |
| Aplikacja |Grupuje średnią liczbę użytkowników na podstawie aplikacji docelowej (jednostki zależnej). Dzięki takiemu grupowaniu można sprawdzić, ilu użytkowników korzysta z danej aplikacji. |

## <a name="performance-monitoring-for-ad-fs"></a>Monitorowanie wydajności dla usług AD FS
Funkcja monitorowania wydajności w programie Azure AD Connect Health udostępnia informacje o metrykach. Wybranie pola Monitorowanie powoduje otwarcie nowego bloku ze szczegółowymi informacjami o metrykach.

![Portal programu Azure AD Connect Health](./media/active-directory-aadconnect-health/perf1.png)

Po wybraniu opcji Filtrowanie u góry bloku można przeprowadzać filtrowanie według serwera, aby uzyskać informacje o poszczególnych metrykach serwera. Aby zmienić metrykę, kliknij prawym przyciskiem myszy wykres monitorowania pod blokiem monitorowania i wybierz pozycję Edytuj wykres (lub wybierz przycisk Edytuj wykres). W nowo otwartym bloku możesz wybrać dodatkowe metryki z listy rozwijanej i określić zakres czasu w celu wyświetlenia danych wydajności.

## <a name="reports-for-ad-fs"></a>Raporty dotyczące usług AD FS
Program Azure AD Connect Health udostępnia raporty o aktywności i wydajności usług AD FS. Raporty te umożliwiają administratorom wgląd w działania na serwerach usług AD FS.

### <a name="top-50-users-with-failed-usernamepassword-logins"></a>50 użytkowników z największą liczbą nieudanych logowań z powodu błędnej nazwy użytkownika lub błędnego hasła
Typowe przyczyny niepowodzenia żądania uwierzytelnienia na serwerze usług AD FS to żądanie z nieprawidłowymi poświadczeniami, czyli z nieprawidłową nazwą użytkownika lub nieprawidłowym hasłem. Zwykle jest to spowodowane przez użycie złożonych haseł, zapomnienie haseł lub literówki.

Jednak istnieją inne przyczyny nieoczekiwanej liczby żądań obsługiwanych przez serwery usług AD FS, takie jak: wygaśnięcie poświadczeń użytkownika przechowywanych w pamięci podręcznej aplikacji lub próba zalogowania się do konta przez złośliwego użytkownika przy użyciu serii dobrze znanych haseł. Te dwa przykłady są potencjalnymi przyczynami wzrostu liczby żądań.

Program Azure AD Connect Health dla usług AD FS dostarcza raport dotyczący 50 użytkowników z największą liczbą nieudanych prób logowania z powodu wpisania nieprawidłowej nazwy użytkownika lub nieprawidłowego hasła. Ten raport jest uzyskiwany przez przetwarzanie zdarzeń inspekcji generowanych przez wszystkie serwery usług AD FS w farmach.

![Portal programu Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report1a.png)

Ten raport daje łatwy dostęp do następujących informacji:

* Łączna liczba nieudanych żądań z błędną nazwą użytkownika lub błędnym hasłem w ciągu ostatnich 30 dni.
* Średnia dzienna liczba użytkowników, którzy popełnili błędy podczas logowania się w wyniku podania nieprawidłowej nazwy użytkownika lub nieprawidłowego hasła.

Kliknięcie tej części przenosi do głównego bloku raportu z dodatkowymi informacjami. Ten blok zawiera wykres z informacjami o trendach, który ułatwia ustalenie linii bazowej dotyczącej żądań z nieprawidłową nazwą użytkownika lub hasłem. Zawiera również listę 50 użytkowników o największej liczbie nieudanych prób.

Wykres udostępnia następujące informacje:

* Łączna liczba nieudanych logowań w ciągu jednego dnia z powodu podania nieprawidłowej nazwy użytkownika lub nieprawidłowego hasła.
* Łączna liczba unikatowych użytkowników w ciągu jednego dnia, którym nie udało się zalogować.
* Adres IP klienta dla ostatniego żądania

![Portal programu Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report3a.png)

Raport zawiera następujące informacje:

| Element raportu | Opis |
| --- | --- |
| Identyfikator użytkownika |Wyświetla użyty identyfikator użytkownika. Jest to wartość wpisana przez użytkownika, co w niektórych przypadkach powoduje użycie nieprawidłowego identyfikatora użytkownika. |
| Nieudane próby |Pokazuje łączną liczbę nieudanych prób dla konkretnego identyfikatora użytkownika. Tabela jest sortowana według największej liczby nieudanych prób w kolejności malejącej. |
| Ostatnia nieudana próba |Wyświetla sygnaturę czasową momentu, w którym wystąpiła ostatnia awaria. |
| Adres IP ostatniej nieudanej próby |Wyświetla adres IP klienta dla ostatniego złego żądania. |

> [!NOTE]
> Ten raport jest aktualizowany automatycznie co dwie godziny o nowe informacje, które pojawiły się w tym czasie. W rezultacie próby logowania z ostatnich dwóch godzin mogą nie zostać zawarte w raporcie.
>
>

## <a name="related-links"></a>Powiązane linki
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalowanie agenta programu Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operacje w programie Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Używanie programu Azure AD Connect Health w celu synchronizacji](active-directory-aadconnect-health-sync.md)
* [Używanie programu Azure AD Connect Health z usługami AD DS](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health — często zadawane pytania](active-directory-aadconnect-health-faq.md)
* [Historia wersji programu Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)