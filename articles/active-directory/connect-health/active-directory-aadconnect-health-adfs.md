---
title: "aaaUsing Azure AD Connect Health z usługami AD FS | Dokumentacja firmy Microsoft"
description: "Jak to hello Azure AD Connect Health strony toomonitor lokalnej infrastruktury usług AD FS."
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
ms.openlocfilehash: 0cd26e8762be65e09d22e1f113e5165c4f131715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-ad-fs-using-azure-ad-connect-health"></a>Monitorowanie usług AD FS za pomocą programu Azure AD Connect Health
Witaj następujących dokumentacji jest szczególne toomonitoring infrastruktury usług AD FS z usługi Azure AD Connect Health. Aby uzyskać informacje na temat monitorowania programu Azure AD Connect (synchronizacja) za pomocą programu Azure AD Connect Health, zobacz [Używanie programu Azure AD Connect Health w celu synchronizacji](active-directory-aadconnect-health-sync.md). Ponadto, aby uzyskać informacje na temat monitorowania Usług domenowych Active Directory za pomocą programu Azure AD Connect Health, zobacz [Używanie programu Azure AD Connect Health z usługami AD DS](active-directory-aadconnect-health-adds.md).

## <a name="alerts-for-ad-fs"></a>Alerty dla usług AD FS
Hello Azure AD Connect alerty kondycji zawiera hello listę aktywnych alertów. Każdy alert zawiera istotne informacje, kroki rozwiązania i dokumentacji toorelated łącza.

Możesz kliknąć dwukrotnie aktywny lub rozwiązany alertu, tooopen nowy blok z dodatkowymi informacjami, kroki można wykonać tooresolve hello alertu i dokumentacji toorelevant łącza. Można również wyświetlić dane historyczne na temat alertów, które zostały rozwiązane w przeszłości hello.

![Portal programu Azure AD Connect Health](./media/active-directory-aadconnect-health/alert2.png)

## <a name="usage-analytics-for-ad-fs"></a>Analiza użycia usług AD FS
Azure AD Connect Health analizy użycia analizuje hello ruchu uwierzytelniania serwerów federacyjnych. Dwukrotne kliknięcie pola analizy użycia hello, bloku analizy użycia hello tooopen, który zawiera kilka metryki i grupowania.

> [!NOTE]
> toouse analizy użycia z usługami AD FS, pamiętaj, że inspekcja usług AD FS jest włączona. Aby uzyskać więcej informacji, zobacz [Włączanie inspekcji dla usług AD FS](active-directory-aadconnect-health-agent-install.md#enable-auditing-for-ad-fs).
>
>

![Portal programu Azure AD Connect Health](./media/active-directory-aadconnect-health/report1.png)

tooselect dodatkowe metryki, określić zakres czasu lub toochange hello grupowanie, kliknij prawym przyciskiem myszy wykres analizy użycia hello i wybierz pozycję Edytuj wykres. Następnie można określić zakres czasu hello, wybierz inną metryki i zmień hello grupowania. Można wyświetlić hello rozkład ruchu uwierzytelniania hello w oparciu o różne "metryki" i pogrupować wszystkie metryki przy użyciu parametrów odpowiednich "Grupuj według" opisanych w hello następujących sekcji:

**Metryka: Łączna liczba żądań** — łączna liczba żądań przetworzonych przez serwery usług AD FS.

|Grupuj według | Co oznacza określenie hello grupowanie i dlaczego jest przydatne? |
| --- | --- |
| Wszystkie | Pokazuje hello liczba całkowita liczba żądań przetwarzanych przez wszystkie serwery usług AD FS.|
| Aplikacja | Grupy hello całkowita liczba żądań oparte na powitania docelową uzależnioną. Ta metoda grupowania jest przydatna toounderstand, która aplikacja odbiera wartość procentową hello całkowitym ruchu. |
|  Serwer |Grupy hello całkowita liczba żądań oparte na powitania serwera, który przetwarzał żądanie hello. To grupowanie jest przydatne toounderstand rozkład obciążenia hello hello całkowitym ruchu.
| Urządzenia dołączone w miejscu pracy |Grupy hello całkowita liczba żądań według tego, czy są przesyłanych z urządzeń, które są dołączone do miejsca pracy (znane). Ta metoda grupowania jest przydatna toounderstand, jeśli zasoby są dostępne przy użyciu urządzenia, które są nieznane toohello infrastruktury tożsamości. |
|  Metoda uwierzytelniania | Grupy hello całkowita liczba żądań na podstawie metody uwierzytelniania hello używany do uwierzytelniania. Ta metoda grupowania jest przydatna toounderstand hello metoda uwierzytelniania jest najczęściej używana do uwierzytelniania. Poniżej przedstawiono metody uwierzytelniania można hello <ol> <li>Zintegrowane uwierzytelnianie systemu Windows (system Windows)</li> <li>Uwierzytelnianie oparte na formularzach (Formularze)</li> <li>Logowanie jednokrotne (SSO, Single Sign On)</li> <li>Uwierzytelnianie w oparciu o certyfikat standardu X509 (Certyfikat)</li> <br>Jeśli serwery federacyjne hello otrzymają hello żądania o plik Cookie logowania jednokrotnego, to żądanie jest traktowane jako SSO (logowanie jednokrotne). W takich przypadkach jeśli hello plik cookie jest prawidłowy, hello użytkownik nie jest proszony tooprovide poświadczenia i pobiera aplikację toohello bezproblemowy dostęp. To zachowanie jest wspólne, jeśli masz wiele jednostek zależnych chronionych przez serwery federacyjne hello. |
| Lokalizacja sieciowa | Grupy hello całkowita liczba żądań na podstawie lokalizacji sieciowej hello hello użytkownika. Może to być zarówno sieć intranet, jak i ekstranet. Ta metoda grupowania jest przydatna tooknow, jaki procent ruchu hello pochodzi z hello intranet lub ekstranet. |


**Metryki: Łączna nie powiodło się żądanie** -hello łączna liczba żądań przetwarzanych przez usługę federacyjną hello nie powiodło się. (Ta metryka jest dostępna tylko w usługach AD FS dla systemu Windows Server 2012 R2)

|Grupuj według | Co oznacza określenie hello grupowanie i dlaczego jest przydatne? |
| --- | --- |
| Typ błędu | Pokazuje hello liczbę błędów w oparciu wcześniej zdefiniowanych typów błędów. Ta metoda grupowania jest przydatna toounderstand hello typowych błędów. <ul><li>Nieprawidłowa nazwa użytkownika lub hasło: błędy powodu tooincorrect nazwa użytkownika lub hasło.</li> <li>"Blokowanie ekstranetu w usługach": niepowodzenia powodu toohello żądania otrzymane od użytkownika, które zostało zablokowane z ekstranetu </li><li> "Hasło nieaktualne": niepowodzenia powodu toousers logującym się przy użyciu nieaktualnych haseł.</li><li>"Konto wyłączone": niepowodzenia powodu toousers rejestrowanie przy użyciu wyłączonych kont.</li><li>"Uwierzytelnianie urządzenia": niepowodzenia powodu tooauthenticate niepowodzenie toousers przy użyciu uwierzytelniania urządzenia.</li><li>"Uwierzytelnianie certyfikatu użytkownika": niepowodzenia powodu tooauthenticate toousers się niepowodzeniem z powodu nieprawidłowego certyfikatu.</li><li>"MFA": niepowodzenia powodu tooauthenticate niepowodzenie toouser przy użyciu usługi Multi-Factor Authentication.</li><li>"Inne poświadczenia": "Autoryzacja wystawiania": niepowodzenia powodu tooauthorization błędów.</li><li>"Delegowanie wystawiania": niepowodzenia powodu tooissuance błędami delegowania.</li><li>"Akceptacja tokenu": niepowodzenia powodu odrzucenia tooADFS hello tokenu od dostawcy tożsamości innych firm.</li><li>"Protokół": niepowodzenia powodu tooprotocol błędy.</li><li>„Nieznane”: Wszystkie inne rodzaje niepowodzeń. Inne błędy, które nie pasują do hello zdefiniowanych kategorii.</li> |
| Serwer | Grupy hello błędy oparte na powitania serwera. Ta metoda grupowania jest przydatna toounderstand hello błąd dystrybucji na serwerach. Nierównomierny rozkład może oznaczać uszkodzenie serwera. |
| Lokalizacja sieciowa | Grupy hello błędów na podstawie lokalizacji sieciowej hello hello żądań (intranet lub ekstranet). Ta metoda grupowania jest przydatna toounderstand hello typ żądań, które kończą się niepowodzeniem. |
|  Aplikacja | Grupy hello błędów na podstawie aplikacji hello docelowe (jednostki zależnej). Ta metoda grupowania jest przydatna toounderstand, która aplikacja docelowa ma do czynienia z największą liczbą błędów. |

**Metryka: Liczba użytkowników** — średnia liczba unikatowych użytkowników aktywnie uwierzytelnianych za pomocą usług AD FS.

|Grupuj według | Co oznacza określenie hello grupowanie i dlaczego jest przydatne? |
| --- | --- |
|Wszystkie |Ta metryka zapewnia liczenie średniej liczby użytkowników przy użyciu usługi federacyjnej hello w hello wybranym przedziale czasu. Witaj, użytkownicy nie są zgrupowani. <br>Średnia Hello zależy od wybranego przedziału czasu hello. |
| Aplikacja |Średnia liczba hello grup użytkowników oparte na powitania przeznaczone dla aplikacji (jednostki uzależnionej). Ta metoda grupowania jest przydatna toounderstand ilu użytkowników korzysta z danej aplikacji. |

## <a name="performance-monitoring-for-ad-fs"></a>Monitorowanie wydajności dla usług AD FS
Funkcja monitorowania wydajności w programie Azure AD Connect Health udostępnia informacje o metrykach. Po zaznaczeniu pola monitorowanie hello, zostanie otwarty nowy blok z szczegółowe informacje na temat hello metryki.

![Portal programu Azure AD Connect Health](./media/active-directory-aadconnect-health/perf1.png)

Wybranie opcji filtrowania hello u góry bloku hello hello można filtrować według toosee serwera poszczególnych metrykach serwera. Metryka toochange, kliknij prawym przyciskiem myszy na powitania monitorowanie wykres w obszarze monitorowania bloku hello i wybierz Edytuj wykres (lub hello wybierz przycisk Edytuj wykres). Z hello nowy blok otwartym możesz wybrać dodatkowe metryki z listy rozwijanej hello i określ zakres czasu w celu wyświetlania danych o wydajności hello.

## <a name="reports-for-ad-fs"></a>Raporty dotyczące usług AD FS
Program Azure AD Connect Health udostępnia raporty o aktywności i wydajności usług AD FS. Raporty te umożliwiają administratorom wgląd w działania na serwerach usług AD FS.

### <a name="top-50-users-with-failed-usernamepassword-logins"></a>50 użytkowników z największą liczbą nieudanych logowań z powodu błędnej nazwy użytkownika lub błędnego hasła
Jednym z hello typowe przyczyny niepowodzenia żądania uwierzytelnienia na serwerze usług AD FS jest żądanie z nieprawidłowymi poświadczeniami, czyli nieprawidłową nazwę użytkownika lub hasło. Zwykle odbywa się toousers toocomplex hasła, zapomniane hasła lub literówki.

Ale są też inne przyczyny, które mogą skutkować nieoczekiwaną liczbę żądań obsługiwanych przez serwery usług AD FS, takie jak: aplikacja, która wygaśnie pamięci podręcznych poświadczeń użytkownika i poświadczeń hello lub złośliwy użytkownik próbujący toosign do konta z serii dobrze znane hasła. Te dwa przykłady są prawidłowe przyczyn, które może spowodować wzrost tooa w żądaniach.

Azure AD Connect Health dla usług AD FS dostarcza raport dotyczący 50 pierwszych użytkownikom nieudanych prób logowania powodu tooinvalid nazwa użytkownika lub hasło. Ten raport jest to osiągane przez przetwarzanie zdarzeń inspekcji hello generowanych przez wszystkie serwery hello usług AD FS w farmach hello

![Portal programu Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report1a.png)

W tym raporcie są toohello łatwy dostęp następujące informacje:

* Całkowita liczba nieudanych żądań z nieprawidłową nazwę użytkownika/hasło hello ostatnich 30 dni
* Średnia dzienna liczba użytkowników, którzy popełnili błędy podczas logowania się w wyniku podania nieprawidłowej nazwy użytkownika lub nieprawidłowego hasła.

Kliknięcie tej części przyjmuje toohello głównego bloku raportu z dodatkowymi informacjami. Ten blok zawiera wykres z analizy trendów informacji toohelp nakreślić linię bazową żądań z nieprawidłową nazwą użytkownika lub hasło. Ponadto zapewnia hello listę top 50 użytkowników z hello liczby nieudanych prób.

Wykres Hello udostępnia hello następujących informacji:

* Witaj łączna liczba nieudanych logowań powodu tooa zły nazwy użytkownika i hasła na podstawie ciągu jednego dnia.
* Witaj łączną liczbę unikatowych użytkowników, którym nie udało się na podstawie ciągu jednego dnia.
* Adres IP klienta dla ostatniego żądania

![Portal programu Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report3a.png)

Raport Hello zawiera hello następujących informacji:

| Element raportu | Opis |
| --- | --- |
| Identyfikator użytkownika |Pokazuje hello identyfikator użytkownika, który został użyty. Ta wartość jest jakie hello użytkownika wpisany, co jest hello błędnego Identyfikatora użytkownika używane w niektórych przypadkach. |
| Nieudane próby |Pokazuje hello łączną liczbę nieudanych prób dostępu dla tego konkretnego identyfikatora użytkownika. Witaj tabela jest sortowana według hello najbardziej liczba nieudanych prób w kolejności malejącej. |
| Ostatnia nieudana próba |Zawiera sygnaturę czasową powitania po ostatniej awarii hello. |
| Adres IP ostatniej nieudanej próby |Zawiera adres IP klienta hello z hello najnowsze nieprawidłowe żądanie. |

> [!NOTE]
> Ten raport jest aktualizowany automatycznie co dwie godziny z hello nowe informacje zebrane w tym czasie. W związku z tym Witaj dwie godziny ostatniej próby logowania mogą nie zostać zawarte w raporcie hello.
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