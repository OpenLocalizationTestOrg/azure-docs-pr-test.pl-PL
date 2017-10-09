---
title: "aaaResolve problemów licencji dla grupy w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooidentify i rozwiąż licencji przypisania problemy podczas korzystania z usługi Azure Active Directory na podstawie grupy licencji"
services: active-directory
keywords: "Licencjonowanie usługi Azure AD"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ec9c74214a9e246f21fcf767b0bbd586ae702445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>Identyfikowanie i rozwiązywanie problemów przypisania licencji dla grupy w usłudze Azure Active Directory

Na podstawie grupy Licencjonowanie w usłudze Azure Active Directory (Azure AD) wprowadzono pojęcie hello użytkowników w stanie błędu licencjonowania. W tym artykule firma Microsoft wyjaśnienia przyczyn hello, dlaczego użytkownicy mogą wystąpić w tym stanie.

Po przypisaniu licencji bezpośrednio tooindividual użytkowników bez użycia na podstawie grupy licencji, operacja przypisania hello może zakończyć się niepowodzeniem. Na przykład podczas wykonywania polecenia cmdlet programu PowerShell hello `Set-MsolUserLicense` na koncie użytkownika, polecenia cmdlet hello może się nie powieść z kilku powodów, które są powiązane toobusiness logiki. Na przykład może być niewystarczającą liczbę licencji lub konflikt między dwa pakiety usług, których nie można przypisać na powitania sam czas. Witaj problem jest natychmiast zgłoszony kopii tooyou.

Podczas korzystania z oparte na grupach licencjonowania, hello, które mogą wystąpić błędy w tej samej, ale się tak zdarzyć w tle hello hello usługi Azure AD jest przypisywania licencji. Z tego powodu hello błędy nie może być przekazane tooyou natychmiast. Zamiast tego są rejestrowane na powitania obiektu użytkownika i następnie zgłoszone za pośrednictwem portalu administracyjnego hello. Należy pamiętać, że hello oryginalnego konwersji toolicense hello użytkownika nigdy nie zostaną utracone, ale jest rejestrowany w stanie błędu w przyszłości badania i rozwiązywania.

## <a name="how-toofind-license-assignment-errors"></a>Jak toofind licencji błędy przypisania

1. Użytkownicy toofind stanu błędu w określonej grupie, otwórz hello bloku hello grupy. W obszarze **licencji**, będą wyświetlane, gdy wszyscy użytkownicy w stanie błędu powiadomienie.

![Powiadomienie o błędzie grupy](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. Kliknij przycisk hello powiadomień tooopen listę wszystkich użytkowników. Możesz kliknąć każdy użytkownik indywidualnie toosee więcej szczegółowych informacji.

![Grupy, listę użytkowników w stan błędu](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. toofind wszystkich grup, które zawierają co najmniej jeden błąd, na powitania **usługi Azure Active Directory** wybierz bloku **licencji** , a następnie **omówienie**. Pole informacje jest wyświetlane, gdy niektóre grupy wymagają Twojej uwagi.

![Przegląd informacji na temat grup w stan błędu](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. Polecenie toosee pole hello listę wszystkich grup z błędami. Możesz kliknąć każdej grupy, aby uzyskać więcej informacji.

![Przegląd, lista grup błędów](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


Poniżej znajduje się opis każdego potencjalne tooresolve sposób problemu i hello go.

## <a name="not-enough-licenses"></a>Za mało licencji

**Problem:** nie ma wystarczającej liczby dostępnych licencji dla jednego z hello produktów, które jest określone w grupie hello. Należy tooeither Kup więcej licencji produktu hello, lub zwolnij na nim nieużywanych licencji z innym użytkownikom lub grupom.

toosee liczby licencji są dostępne, należy przejść za**usługi Azure Active Directory** > **licencji** > **wszystkie produkty**.

toosee zużywają licencji, którzy użytkownicy i grupy kliknij produkt. W obszarze **licencjonowani użytkownicy**, zobaczysz wszyscy użytkownicy, którzy właśnie przypisane bezpośrednio lub za pośrednictwem jednej lub kilku grup licencji. W obszarze **licencjonowane grup**, zobaczysz wszystkich grup, które mają przypisane produktu.

**Środowiska PowerShell:** poleceń cmdlet programu PowerShell, zgłoś ten błąd jako _CountViolation_.

## <a name="conflicting-service-plans"></a>Plany usługi powodujące konflikt

**Problem:** jeden hello produktów, które jest określone w grupie hello zawiera planu usług, który powoduje konflikt z innego planu usług, który jest już przypisany toohello użytkownika za pośrednictwem innego produktu. Niektóre plany usługi są skonfigurowane w taki sposób, że ich nie można przypisać toohello tego samego użytkownika innego planu pokrewne usługi.

Należy wziąć pod uwagę hello poniższy przykład. Użytkownik ma licencję dla Office 365 Enterprise **E1** przypisany bezpośrednio, za pomocą wszystkich planów hello włączone. Witaj użytkownik został dodany tooa grupy, która ma hello Office 365 Enterprise **E3** tooit produktu przypisany. Ten produkt zawiera plany usługi, które nie może nakładać się z planami hello uwzględniona w E1, więc przypisanie licencji grupy hello zakończy się niepowodzeniem z hello błąd "Powodujące konflikt planów usługi". W tym przykładzie są hello powodujące konflikt planów usług:

-   Usługi SharePoint Online (Planowanie 2) powoduje konflikt z usługą SharePoint Online (Planowanie 1).
-   Exchange Online (Planowanie 2) powoduje konflikt z usługą Exchange Online (Planowanie 1).

toosolve tej konflikt należy toodisable tych dwóch planów licencji na powitania E1 to jest użytkownik toohello bezpośrednio przypisane. Lub wymagają przypisania licencji całej grupy hello toomodify i wyłączyć plany hello hello E3 licencji. Alternatywnie możesz tooremove hello E1 licencji użytkownika hello Jeśli nadmiarowego w kontekście hello hello E3 licencji.

Witaj decyzję o jak licencje produktu powodujące konflikt tooresolve zawsze należy toohello administratora. Usługi Azure AD nie automatycznie rozwiązać konflikty licencji.

**Środowiska PowerShell:** poleceń cmdlet programu PowerShell, zgłoś ten błąd jako _MutuallyExclusiveViolation_.

## <a name="other-products-depend-on-this-license"></a>Inne produkty są zależne od tej licencji

**Problem:** jeden hello produktów, które jest określone w grupie hello zawiera plan usługi, która musi być włączona dla innego planu usług, w innego produktu, aby funkcja. Ten błąd występuje, gdy podstawowy plan usługi tooremove hello próbuje usługi Azure AD. Na przykład może to nastąpić w wyniku użytkownika hello usuwanych z grupy hello.

toosolve ten problem, należy toomake się, że plan wymagane hello jest ciągle przypisany toousers za pomocą innej metody, lub czy hello zależne usługi zostały wyłączone dla tych użytkowników. Po tym można prawidłowo Usuń hello grupy licencji z tych użytkowników.

**Środowiska PowerShell:** poleceń cmdlet programu PowerShell, zgłoś ten błąd jako _DependencyViolation_.

## <a name="usage-location-isnt-allowed"></a>Lokalizacja użytkowania nie jest dozwolona

**Problem:** pewnych usług firmy Microsoft nie są dostępne we wszystkich lokalizacjach z powodu lokalnych przepisów eksportowych. Przed przypisaniem licencji użytkownika tooa masz właściwość "Lokalizacji użytkowania" hello toospecify hello użytkownika. Można to zrobić w obszarze hello **użytkownika** > **profilu** > **ustawienia** części hello portalu Azure.

Jeśli usługi Azure AD próbuje tooassign użytkownika tooa licencji grupy, których lokalizacji użytkowania nie jest obsługiwany, spowoduje niepowodzenie i zarejestrować ten błąd na powitania użytkownika.

toosolve ten problem, Usuń użytkowników z nieobsługiwanych lokalizacji z grupy hello licencji. Alternatywnie Jeśli hello wartości w bieżącej lokalizacji użycie nie reprezentować lokalizacji użytkownika rzeczywiste hello, można je zmodyfikować tak, aby licencje hello są poprawnie przypisać identyfikatory potwierdzenia następnym (jeśli jest obsługiwana w nowej lokalizacji hello).

**Środowiska PowerShell:** poleceń cmdlet programu PowerShell, zgłoś ten błąd jako _ProhibitedInUsageLocationViolation_.

> [!NOTE]
> Usługi Azure AD przypisuje grupę licencji, wszyscy użytkownicy bez użycia lokalizacji określonej dziedziczyły hello lokalizację katalogu hello. Zalecane Administratorzy ustawienie hello odpowiednie użycie wartości lokalizacji dla użytkowników przed użyciem toocomply licencjonowania na podstawie grupy z lokalnych przepisów eksportowych.

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>Co się stanie, gdy jest kilku licencji produktu grupy?

Można przypisać więcej niż jednej grupy tooa licencji produktu. Na przykład można przypisać Office 365 Enterprise E3 i Enterprise Mobility + Security tooa grupy tooeasily włączyć wszystkie dołączone usługi dla użytkowników.

Usługi Azure AD prób tooassign wszystkie licencje, które są określone w hello grupy tooeach użytkownika. Jeśli usługi Azure AD nie można przypisać jedną hello produktów z powodu problemów logiki biznesowej (na przykład, jeśli nie ma wystarczającą liczbę licencji dla wszystkich lub jeśli występują konflikty z innymi usługami, które są włączone na powitania użytkownika), nie będzie przypisać hello inne licencje w grupie hello albo.

Będziesz w stanie toosee hello, użytkowników, którzy nie można przypisać tooget nie powiodło się i wyboru produktów, które mają zostać wpłynie to na.

## <a name="license-assignment-fails-silently-for-a-user-due-tooduplicate-proxy-addresses-in-exchange-online"></a>Przypisanie licencji nie powiedzie się dyskretnie użytkownika powodu tooduplicate adresów serwerów proxy w usłudze Exchange Online

Jeśli używasz usługi Exchange Online, niektórzy użytkownicy w Twojej dzierżawie może być niepoprawnie skonfigurowana z hello tę samą wartość adres serwera proxy. Gdy na podstawie grupy licencjonowania podejmie próbę tooassign toosuch licencji użytkownika, zakończy się niepowodzeniem i nie będą rejestrować błąd (w przeciwieństwie do w hello innych błędów opisanych powyżej) — jest to ograniczenie w wersji preview hello tej funkcji i zamierzamy tooaddress go przed  *Ogólnie*.

> [!TIP]
> Jeśli zauważysz, że niektórym użytkownikom nie otrzymały licencji i nie było błędu zarejestrowanych dla tych użytkowników, najpierw sprawdź, czy mają one adres serwera proxy zduplikowane.
> Można to zrobić, wykonując następujące polecenia cmdlet programu PowerShell dla usługi Exchange Online hello:
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [W tym artykule](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) zawiera szczegółowe informacje o tym problemie, łącznie z informacjami na [jak tooExchange tooconnect Online przy użyciu zdalnego programu PowerShell](https://technet.microsoft.com/library/jj984289.aspx).

Po proxy rozwiązywać problemy zostały rozwiązane hello wpływ na użytkowników, należy upewnić się, że licencji tooforce przetwarzania na powitania grupy toomake się, że licencji można zastosować teraz ponownie.

## <a name="how-do-you-force-license-processing-in-a-group-tooresolve-errors"></a>Jak wymusić przetwarzania błędów tooresolve grupę licencji?

W zależności od jakie kroki zostały wykonane błędy tooresolve, może być konieczne toomanually przetwarzania wyzwalacz stanu użytkownika hello tooupdate grupy.

Na przykład jeśli niektóre licencje zwalniane przez usunięcie przypisań licencji bezpośrednio od użytkowników, musisz przetwarzania tootrigger grup, których wcześniej nie powiodła się licencji toofully wszyscy członkowie użytkownika. Otwórz toodo, który znaleźć bloku grupy hello, **licencji**i wybierz hello **ponownie przetworzyć** przycisk hello w pasku narzędzi.

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat innych scenariuszy zarządzania licencji za pomocą grup, zobacz następujące hello:

* [Przypisywanie licencji tooa grupy w usłudze Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Co to jest oparte na grupach Licencjonowanie w usłudze Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Jak osoba toomigrate — licencjonowani użytkownicy toogroup na podstawie Licencjonowanie w usłudze Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Usługa Azure Active Directory na podstawie grupy licencjonowania dodatkowe scenariusze](active-directory-licensing-group-advanced.md)
