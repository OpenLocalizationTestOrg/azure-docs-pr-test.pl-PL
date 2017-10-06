---
title: "Azure AD Connect: Przekazywanego uwierzytelniania - preview uaktualniania agentów uwierzytelniania | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooupgrade konfiguracji uwierzytelniania przekazywanego usługi Azure Active Directory (Azure AD)."
services: active-directory
keywords: "Azure AD Connect przekazywanego uwierzytelniania, instalacji usługi Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 1695326b182278944e9f1584da72b18862b6ef27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a>Usługi Azure Active Directory przekazywanego uwierzytelniania: Agenci uwierzytelniania uaktualnienia wersji zapoznawczej

## <a name="overview"></a>Omówienie

W tym artykule jest przeznaczona dla klientów przy użyciu usługi Azure AD przekazywanego uwierzytelniania za pomocą podglądu. Firma Microsoft hello niedawno uaktualniony (i rebranded) oprogramowanie agenta uwierzytelniania. Należy too_manually_ uaktualnienia Podgląd uwierzytelniania agentów zainstalowanych na serwerach lokalnych. Ręczne uaktualnienie jest tylko Akcja jednorazowa. Wszystkie przyszłe aktualizacje automatyczne są tooAuthentication agentów. Hello tooupgrade przyczyny są następujące:

- wersji zapoznawczych Hello agentów uwierzytelniania nie będą otrzymywać żadnych dalszych zabezpieczeń lub poprawki.
-   Nie można zainstalować wersji zapoznawczych Hello uwierzytelniania agentów na dodatkowych serwerach wysokiej dostępności.

## <a name="check-versions-of-your-authentication-agents"></a>Sprawdź wersje agentów uwierzytelniania

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a>Krok 1: Sprawdź, których zainstalowano agentów uwierzytelniania

Wykonaj te kroki toocheck zainstalowaną agentów uwierzytelniania:

1. Zaloguj się toohello [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) z hello poświadczenia administratora globalnego dla dzierżawy.
2. Wybierz **usługi Azure Active Directory** na powitania nawigacji po lewej stronie.
3. Wybierz **programu Azure AD Connect**. 
4. Wybierz **uwierzytelniania przekazywanego**. Ten blok Wyświetla listę serwerów hello, w których zainstalowano agentów uwierzytelniania.

![Centrum administracyjne usługi Active Directory platformy Azure — blok przekazywanego uwierzytelniania](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

### <a name="step-2-check-hello-versions-of-your-authentication-agents"></a>Krok 2: Sprawdź hello wersje agentów uwierzytelniania

toocheck hello wersje agentów uwierzytelniania, na każdym serwerze, które zostały zidentyfikowane w hello poprzedzających krok, wykonaj następujące instrukcje:

1. Przejdź za**Panel sterowania -> programy -> programy i funkcje** na powitania serwera lokalnego.
2. Jeśli istnieje wpis dotyczący "**agenta programu Microsoft Azure AD Connect uwierzytelniania**", nie potrzebujesz tootake żadnych działań na tym serwerze.
3. Jeśli istnieje wpis dotyczący "**łącznika serwera Proxy w aplikacji pakietu Microsoft Azure AD**", wersji 1.5.132.0 lub wcześniej, należy toomanually uaktualniania na tym serwerze.

![Wersja zapoznawcza Agent uwierzytelniania](./media/active-directory-aadconnect-pass-through-authentication/pta6.png)

## <a name="best-practices-toofollow-before-starting-hello-upgrade"></a>Najlepszych praktyk toofollow przed rozpoczęciem powitalne uaktualnienia

Przed rozpoczęciem uaktualniania upewnij się, że masz następujące elementy w miejscu hello:

1. **Tworzenie konta administratora globalnego tylko w chmurze**: nie uaktualniaj bez konieczności tylko w chmurze toouse konta administratora globalnego w nagłych wypadkach, gdzie agentów uwierzytelniania przekazywanego nie działa prawidłowo. Dowiedz się więcej o [dodanie konta administratora globalnego tylko w chmurze](../active-directory-users-create-azure-portal.md). Wykonanie tego kroku jest krytyczna i zapewnia, że należy przed zablokowaniem dzierżawy.
2.  **Zapewni to wysoką dostępność**: Jeśli wcześniej nie ukończone, należy zainstalować autonomiczny drugi Agent uwierzytelniania tooprovide wysoka dostępność dla żądań logowania, za pomocą tych [instrukcje](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="upgrading-hello-authentication-agent-on-your-azure-ad-connect-server"></a>Uaktualnianie hello Agent uwierzytelniania na serwerze programu Azure AD Connect

Azure AD Connect należy uaktualnić przed uaktualnieniem hello Agent uwierzytelniania na powitania tym samym serwerze. Na serwerze podstawowym i przemieszczania serwery usługi Azure AD Connect, wykonaj następujące kroki:

1. **Uaktualnij Azure AD Connect**: po tym [artykułu](./active-directory-aadconnect-upgrade-previous-version.md) i uaktualniania wersji programu toohello najnowsze usługi Azure AD Connect.
2. **Odinstaluj wersję zapoznawczą hello hello Agent uwierzytelniania**: Pobierz [ten skrypt programu PowerShell](https://aka.ms/rmpreviewagent) i uruchom go jako Administrator na powitania serwera.
3. **Pobieranie najnowszej wersji hello hello Agent uwierzytelniania (wersje 1.5.193.0 lub nowszym)**: Zaloguj toohello [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) przy użyciu poświadczeń administratora globalnego Twojej dzierżawy. Wybierz **usługi Azure Active Directory -> Azure AD Connect -> uwierzytelniania przekazywanego -> agent pobierania**. Zaakceptuj postanowienia hello usługi, a następnie Pobierz najnowszą wersję hello hello Agent uwierzytelniania.
4. **Zainstaluj najnowszą wersję hello Agent uwierzytelniania hello**: hello uruchomienia pliku wykonywalnego pobranego w kroku 3. Podaj poświadczenia administratora globalnego Twojej dzierżawy, po wyświetleniu monitu.
5. **Sprawdź zainstalowano najnowszą wersję tego hello**: jak pokazano wcześniej, przejdź zbyt**Panel sterowania -> programy -> programy i funkcje** i sprawdź, czy istnieje wpis dotyczący "**Microsoft Azure AD Connect Agent uwierzytelniania**".

>[!NOTE]
>Jeśli wybierzesz bloku uwierzytelniania przekazywanego hello na powitania [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) po zakończeniu hello w poprzednich krokach, zobaczysz dwa wpisy uwierzytelniania agenta na serwer - jeden wpis przedstawiający hello Agent uwierzytelniania jako **Active** i inne, hello **nieaktywne**. Jest to _Oczekiwano_. Witaj **nieaktywne** wpis jest automatycznie usunięte po upływie kilku dni.

## <a name="upgrading-hello-authentication-agent-on-other-servers"></a>Uaktualnianie hello Agent uwierzytelniania na innych serwerach

Wykonaj te kroki tooupgrade uwierzytelniania agentów na innych serwerach (gdzie Azure AD Connect nie jest zainstalowany):

1. **Odinstaluj wersję zapoznawczą hello hello Agent uwierzytelniania**: Pobierz [ten skrypt programu PowerShell](https://aka.ms/rmpreviewagent) i uruchom go jako Administrator na powitania serwera.
2. **Pobieranie najnowszej wersji hello hello Agent uwierzytelniania (wersje 1.5.193.0 lub nowszym)**: Zaloguj toohello [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) przy użyciu poświadczeń administratora globalnego Twojej dzierżawy. Wybierz **usługi Azure Active Directory -> Azure AD Connect -> uwierzytelniania przekazywanego -> agent pobierania**. Zaakceptuj postanowienia hello usługi i pobieranie hello najnowszej wersji.
3. **Zainstaluj najnowszą wersję hello Agent uwierzytelniania hello**: hello uruchomienia pliku wykonywalnego pobranego w kroku 2. Podaj poświadczenia administratora globalnego Twojej dzierżawy, po wyświetleniu monitu.
4. **Sprawdź zainstalowano najnowszą wersję tego hello**: jak pokazano wcześniej, przejdź zbyt**Panel sterowania -> programy -> programy i funkcje** i sprawdź, czy istnieje wpis o nazwie **Microsoft Azure AD Connect Agent uwierzytelniania**.

>[!NOTE]
>Jeśli wybierzesz bloku uwierzytelniania przekazywanego hello na powitania [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) po zakończeniu hello w poprzednich krokach, zobaczysz dwa wpisy uwierzytelniania agenta na serwer - jeden wpis przedstawiający hello Agent uwierzytelniania jako **Active** i inne, hello **nieaktywne**. Jest to _Oczekiwano_. Witaj **nieaktywne** wpis jest automatycznie usunięte po upływie kilku dni.

## <a name="next-steps"></a>Następne kroki
- [**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.
