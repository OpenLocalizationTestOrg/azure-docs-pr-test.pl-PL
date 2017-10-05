---
title: "Rozwiązywanie problemów z licencji dla grupy w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Sposób identyfikacji i rozwiązywania problemów przypisania licencji podczas korzystania z usługi Azure Active Directory na podstawie grupy licencji"
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
ms.openlocfilehash: bfa951a897c9b383072c0d29c9a4266c163fe753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>Identyfikowanie i rozwiązywanie problemów przypisania licencji dla grupy w usłudze Azure Active Directory

Na podstawie grupy Licencjonowanie w usłudze Azure Active Directory (Azure AD) wprowadza pojęcia użytkowników w stanie błędu licencjonowania. W tym artykule opisano możemy uzasadnienie, dlaczego użytkownicy mogą wystąpić w tym stanie.

Po przypisaniu licencji bezpośrednio do poszczególnych użytkowników bez użycia na podstawie grupy licencjonowania operacji przypisania może zakończyć się niepowodzeniem. Na przykład podczas wykonywania polecenia cmdlet programu PowerShell `Set-MsolUserLicense` na koncie użytkownika, polecenie cmdlet może się nie powieść z kilku powodów związanych z logiki biznesowej. Na przykład może być niewystarczającą liczbę licencji lub konflikt między dwa pakiety usług, których nie można przypisać w tym samym czasie. Problem jest natychmiast raportowane do Ciebie.

Podczas korzystania z na podstawie grupy licencji, mogą wystąpić błędy tego samego, ale wystąpią w tle, gdy usługi Azure AD jest przypisywaniu licencji. Z tego powodu błędy nie komunikowane użytkownikowi bezpośrednio. Zamiast tego są rejestrowane na obiekt użytkownika i następnie zgłoszone za pośrednictwem portalu administracyjnego. Zauważ, że oryginalnego zamiaru licencji użytkownika nigdy nie zostaną utracone, który jest rejestrowany w stanie błędu w przyszłości badania i rozwiązywania.

## <a name="how-to-find-license-assignment-errors"></a>Jak znaleźć błędy przypisania licencji

1. Aby znaleźć użytkowników w stan błędu w określonej grupie, otwórz blok dla grupy. W obszarze **licencji**, będą wyświetlane, gdy wszyscy użytkownicy w stanie błędu powiadomienie.

![Powiadomienie o błędzie grupy](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. Kliknij powiadomienie, aby otworzyć listę wszystkich użytkowników. Możesz kliknąć dla poszczególnych użytkowników, indywidualnie, aby zobaczyć więcej szczegółów.

![Grupy, listę użytkowników w stan błędu](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. Aby znaleźć wszystkie grupy, które zawierają co najmniej jeden błąd, na **usługi Azure Active Directory** wybierz bloku **licencji** , a następnie **omówienie**. Pole informacje jest wyświetlane, gdy niektóre grupy wymagają Twojej uwagi.

![Przegląd informacji na temat grup w stan błędu](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. Kliknij pole, aby wyświetlić listę wszystkich grup z błędami. Możesz kliknąć każdej grupy, aby uzyskać więcej informacji.

![Przegląd, lista grup błędów](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


Poniżej znajduje się opis każdego potencjalny problem i sposobu rozwiązania go.

## <a name="not-enough-licenses"></a>Za mało licencji

**Problem:** nie ma wystarczającej liczby dostępnych licencji na jeden z nich, które jest określone w grupie. Musisz kupić więcej licencji produktu albo zwolnić nieużywanych licencji z innym użytkownikom lub grupom.

Aby sprawdzić, ile licencji są dostępne, przejdź do **usługi Azure Active Directory** > **licencji** > **wszystkie produkty**.

Aby zobaczyć, którzy użytkownicy i grupy zużywają licencji, kliknij produktu. W obszarze **licencjonowani użytkownicy**, zobaczysz wszyscy użytkownicy, którzy właśnie przypisane bezpośrednio lub za pośrednictwem jednej lub kilku grup licencji. W obszarze **licencjonowane grup**, zobaczysz wszystkich grup, które mają przypisane produktu.

**Środowiska PowerShell:** poleceń cmdlet programu PowerShell, zgłoś ten błąd jako _CountViolation_.

## <a name="conflicting-service-plans"></a>Plany usługi powodujące konflikt

**Problem:** zawiera jeden z nich, które jest określone w grupie usługi plan, który powoduje konflikt z innego planu usługi, która jest już przypisana do użytkownika za pośrednictwem innego produktu. Niektóre plany usługi są skonfigurowane w taki sposób, aby nie można przypisać do tego samego użytkownika innego planu pokrewne usługi.

Rozważmy następujący przykład. Użytkownik ma licencję dla Office 365 Enterprise **E1** przypisane bezpośrednio, wszystkie plany włączone. Użytkownik został dodany do grupy, która ma Office 365 Enterprise **E3** produktu przypisane do niej. Ten produkt zawiera plany usługi, które nie może nakładać się z planami uwzględniona w E1, więc przypisania licencji grupy zakończy się niepowodzeniem z powodu błędu "Powodujące konflikt planów usługi". W tym przykładzie są sprzeczne planów usług:

-   Usługi SharePoint Online (Planowanie 2) powoduje konflikt z usługą SharePoint Online (Planowanie 1).
-   Exchange Online (Planowanie 2) powoduje konflikt z usługą Exchange Online (Planowanie 1).

Aby rozwiązać ten konflikt, należy wyłączyć te dwa plany na licencji E1, która jest bezpośrednio przypisane do użytkownika. Lub, należy zmodyfikować przypisanie licencji całej grupy i wyłączyć plany licencji E3. Alternatywnie można zdecydować usunąć licencji E1 od użytkownika, jeśli jest nadmiarowy w kontekście licencji E3.

Decyzja o tym, jak rozwiązać konflikt licencje produktów zawsze należy do administratora. Usługi Azure AD nie automatycznie rozwiązać konflikty licencji.

**Środowiska PowerShell:** poleceń cmdlet programu PowerShell, zgłoś ten błąd jako _MutuallyExclusiveViolation_.

## <a name="other-products-depend-on-this-license"></a>Inne produkty są zależne od tej licencji

**Problem:** zawiera jeden z nich, które jest określone w grupie planu usług, który musi być włączona dla innego planu usług, w innego produktu, aby funkcja. Ten błąd występuje, gdy próbuje usunąć podstawowego planu obsługi usługi Azure AD. Na przykład może to nastąpić w wyniku użytkownika zostanie usunięte z grupy.

Aby rozwiązać ten problem, należy się upewnić, że wymagany plan jest ciągle przypisany do użytkowników za pomocą innej metody, lub czy zależne usługi zostały wyłączone dla tych użytkowników. Po tym prawidłowo można usunąć grupy licencji od tych użytkowników.

**Środowiska PowerShell:** poleceń cmdlet programu PowerShell, zgłoś ten błąd jako _DependencyViolation_.

## <a name="usage-location-isnt-allowed"></a>Lokalizacja użytkowania nie jest dozwolona

**Problem:** pewnych usług firmy Microsoft nie są dostępne we wszystkich lokalizacjach z powodu lokalnych przepisów eksportowych. Przed można przypisać licencję do użytkownika, należy określić właściwość "Lokalizacji użytkowania" dla użytkownika. Można to zrobić w obszarze **użytkownika** > **profilu** > **ustawienia** sekcji w portalu Azure.

Jeśli usługi Azure AD spróbuje przypisać licencję grupy użytkowników, których lokalizacji użytkowania nie jest obsługiwany, spowoduje niepowodzenie i zarejestrować ten błąd użytkownika.

Aby rozwiązać ten problem, należy usunąć użytkowników z nieobsługiwanych lokalizacji z licencjonowanym grupy. Alternatywnie Jeśli bieżące wartości użycia w lokalizacji nie reprezentować lokalizacji rzeczywistego użytkownika, można je zmodyfikować, dzięki czemu licencji są poprawnie przypisać następnym (jeśli jest obsługiwana w nowej lokalizacji).

**Środowiska PowerShell:** poleceń cmdlet programu PowerShell, zgłoś ten błąd jako _ProhibitedInUsageLocationViolation_.

> [!NOTE]
> Gdy usługi Azure AD przypisuje grupę licencji, wszyscy użytkownicy bez użycia lokalizacji określonej dziedziczą lokalizację katalogu. Zalecane Administratorzy ustawienie odpowiednie użycie wartości lokalizacji dla użytkowników przed użyciem na podstawie grupy licencji w celu zapewnienia przestrzegania lokalnych przepisów eksportowych.

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>Co się stanie, gdy jest kilku licencji produktu grupy?

Do grupy można przypisać kilku licencji produktu. Na przykład Office 365 Enterprise E3 i Enterprise Mobility + Security można przypisać do grupy, aby łatwo włączyć wszystkie dołączone usługi dla użytkowników.

Usługi Azure AD próbuje przypisać wszystkie licencje, które są określone w grupie do poszczególnych użytkowników. Jeśli usługi Azure AD nie można przypisać jeden z nich z powodu problemów logiki biznesowej (na przykład, jeśli nie ma wystarczającą liczbę licencji dla wszystkich lub jeśli występują konflikty z innymi usługami, które są włączone dla użytkownika), jego nie albo przypisać innych licencji w grupie.

Będzie możliwe będzie wyświetlenie użytkowników, którzy nie zostaną przypisane nie powiodło się i sprawdzić, które produkty wpłynęła to.

## <a name="license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online"></a>Przypisanie licencji nie powiedzie się dyskretnie dla użytkownika z powodu proxy zduplikowanych adresów w usłudze Exchange Online

Jeśli używasz usługi Exchange Online, niektórzy użytkownicy w Twojej dzierżawie mogą być niepoprawnie konfigurowani z tą samą wartością adresu serwera proxy. Gdy na podstawie grupy licencji spróbuje przypisać licencję do tych użytkowników, zakończy się niepowodzeniem i nie będą rejestrować błąd (w przeciwieństwie do w innych przypadkach błąd opisane powyżej) — jest to ograniczenie w wersji preview tej funkcji i zamierzamy adresów go przed *ogólnej dostępności*.

> [!TIP]
> Jeśli zauważysz, że niektórym użytkownikom nie otrzymały licencji i nie było błędu zarejestrowanych dla tych użytkowników, najpierw sprawdź, czy mają one adres serwera proxy zduplikowane.
> Można to zrobić, wykonując następujące polecenia cmdlet programu PowerShell dla usługi Exchange Online:
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [W tym artykule](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) zawiera szczegółowe informacje o tym problemie, łącznie z informacjami na [łączenie z usługą Exchange Online przy użyciu zdalnego programu PowerShell](https://technet.microsoft.com/library/jj984289.aspx).

Po problemy adres serwera proxy zostały rozwiązane określonych użytkowników, upewnij się wymusić licencji przetwarzania grupy upewnij się, że licencji można zastosować teraz ponownie.

## <a name="how-do-you-force-license-processing-in-a-group-to-resolve-errors"></a>Jak wymusić przetwarzania licencji w grupie, aby naprawić błędy?

W zależności od tego, jakie kroki zostały wykonane w celu rozwiązania błędów może być konieczne ręcznie uruchomić przetwarzania grupy, aby zaktualizować stan użytkownika.

Na przykład niektóre licencje zwalniane przez usunięcie przypisań licencji bezpośrednio od użytkowników, należy wyzwolenia przetwarzania grup, które wcześniej nie pełni licencji wszystkich członków użytkownika. W tym celu Znajdź bloku grupy, otwórz **licencji**i wybierz **ponownie przetworzyć** przycisku w pasku narzędzi.

## <a name="next-steps"></a>Następne kroki

Aby dowiedzieć się więcej na temat innych scenariuszy zarządzania licencji za pomocą grup, zobacz następujące tematy:

* [Przypisywanie licencji do grupy w usłudze Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Co to jest oparte na grupach Licencjonowanie w usłudze Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Jak przeprowadzić migrację poszczególnych licencjonowanych użytkowników do licencjonowania oparte na grupach w usłudze Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Usługa Azure Active Directory na podstawie grupy licencjonowania dodatkowe scenariusze](active-directory-licensing-group-advanced.md)
