---
title: "wersje usługi MFA aaaAzure oraz zużycie plany | Dokumentacja firmy Microsoft"
description: "Informacje o powitania klienta uwierzytelniania wieloskładnikowego i hello różnych metod i wersje dostępne. Szczegółowe informacje dotyczące każdego planu zużycie"
keywords: 
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: kgremban
ms.openlocfilehash: 4914747e435531b9f950356d23aa386f3d9585d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-azure-multi-factor-authentication"></a>Jak tooget uwierzytelnianie wieloskładnikowe Azure

Po przejściu do tooprotecting Twojego konta, weryfikację dwuetapową powinna być standardowe całej organizacji. Ta funkcja jest szczególnie ważne w przypadku konta z uprawnieniami administracyjnymi, które mają uprzywilejowany dostęp tooresources. Z tego powodu firma Microsoft oferuje tooOffice funkcji weryfikacji dwuetapowej podstawowe 365 i Azure Administratorzy. Funkcje hello tooupgrade dla administratorów, lub rozszerzyć rest toohello weryfikacji dwuetapowej użytkowników, możesz kupić Azure Multi-Factor Authentication. 

W tym artykule omówiono wyjaśniono hello różnicę między wersjami hello oferowane tooadministrators i hello pełną wersję usługi Azure MFA i określa, które funkcje są dostępne w każdym. Jeśli wszystko jest gotowe toodeploy hello ukończyć oferty usługi Azure MFA, hello nowsze opcje implementacji obejmuje sekcje i jak Microsoft oblicza zużycia.

>[!IMPORTANT]
>W tym artykule jest przeznaczona toobe toohelp przewodniku, należy zrozumieć hello toobuy różne sposoby Azure Multi-Factor Authentication. Aby uzyskać szczegółowe informacje o cenach i rozliczeń, powinni zawsze zapoznać toohello [uwierzytelnianie wieloskładnikowe, na stronie dotyczącej cen](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

## <a name="available-versions-of-azure-multi-factor-authentication"></a>Dostępne wersje usługi Azure Multi-Factor Authentication

Witaj poniższej tabeli opisano różnice hello trzy wersje usługi Multi-Factor Authentication:

| Wersja | Opis |
| --- | --- |
| Usługa Multi-Factor Authentication dla usługi Office 365 |Ta wersja działa wyłącznie z aplikacjami usługi Office 365 i jest zarządzany z portalu usługi Office 365 hello. Administratorzy mogą [zabezpieczenia zasobów usługi Office 365 w trakcie weryfikacji dwuetapowej](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6). Ta wersja jest częścią subskrypcji usługi Office 365. |
| Uwierzytelnianie wieloskładnikowe dla administratorów usługi Azure | Administratorzy globalni dzierżawców Azure można włączyć weryfikację dwuetapową dla konta administratora globalnego bez ponoszenia dodatkowych kosztów.|
| Azure Multi-Factor Authentication | Często określonego tooas wersja "pełnej" hello, uwierzytelnianie wieloskładnikowe Azure udostępnia hello najszerszym zestaw funkcji. Zapewnia dodatkowe opcje konfiguracji za pośrednictwem hello [klasycznego portalu Azure](https://manage.windowsazure.com), zaawansowane raportowanie i obsługuje szeroką gamę lokalnych i aplikacji w chmurze. Uwierzytelnianie wieloskładnikowe platformy Azure znajduje się w usłudze Azure Active Directory Premium (planów P1 i P2) i Enterprise Mobility + Security (planów E3 i E5) i może być wdrożony albo [w chmurze hello lub lokalnie](multi-factor-authentication-get-started.md). |

## <a name="feature-comparison-of-versions"></a>Porównanie funkcji wersji
Witaj Poniższa tabela zawiera listę funkcji hello, które są dostępne w hello różnych wersji usługi Azure Multi-Factor Authentication.

> [!NOTE]
> Ta tabela porównawcza omówiono hello funkcje, które są częścią każdej wersji usługi Multi-Factor Authentication. Jeśli masz pełne usługi Azure Multi-Factor Authentication hello, niektóre funkcje mogą być dostępne w zależności od tego, czy używasz [MFA w chmurze hello lub MFA lokalnymi](multi-factor-authentication-get-started.md).


| Funkcja | Usługa Multi-Factor Authentication dla usługi Office 365 | Uwierzytelnianie wieloskładnikowe dla administratorów usługi Azure | Azure Multi-Factor Authentication |
| --- |:---:|:---:|:---:|
| Ochrona kont administratorów za pomocą usługi MFA |● |● (tylko dla konta administratora globalnego) |● |
| Aplikacji mobilnej jako czynnika |● |● |● |
| Połączenie telefoniczne jako czynnika |● |● |● |
| SMS jako czynnika |● |● |● |
| Hasła aplikacji dla klientów, które nie obsługują uwierzytelniania Wieloskładnikowego |● |● |● |
| Administrator kontrolę nad metody weryfikacji |● |● |● |
| Tryb numeru PIN | | |● |
| Alert dotyczący wykrycia oszustwa | | |● |
| Raporty usługi MFA | | |● |
| Jednorazowe obejście | | |● |
| Niestandardowe powitania dla połączeń telefonicznych | | |● |
| Identyfikator wywołującego niestandardowych dla połączeń telefonicznych | | |● |
| Zaufane adresy IP | | |● |
| Pamiętanie uwierzytelniania MFA w przypadku zaufanych urządzeń |● |● |● |
| Zestaw MFA SDK | | |● (dostawca wymaga uwierzytelniania wieloskładnikowego i subskrypcji pełnej Azure) |
| Usługi MFA dla aplikacji lokalnych | | |● |

## <a name="how-tooget-azure-multi-factor-authentication"></a>Jak tooget uwierzytelnianie wieloskładnikowe Azure
Jeśli chcesz pełnej funkcjonalności hello oferowanych przez usługi Azure Multi-Factor Authentication, dostępnych jest kilka opcji:

### <a name="option-1---mfa-licenses"></a>Opcja 1 — licencji usługi MFA

Zakupu licencji Azure Multi-Factor Authentication i przypisać je tooyour użytkowników w usłudze Azure Active Directory. 

Jeśli używasz tej opcji, należy utworzyć dostawcę usługi Azure Multi-Factor Authentication tylko wtedy, gdy należy również tooprovide weryfikacji dwuetapowej dla niektórych użytkowników, które nie mają licencji. W przeciwnym razie należy może zostać użyta, dwa razy.

### <a name="option-2---bundled-licenses-that-include-mfa"></a>Opcja 2 — powiązane licencji, które obejmują usługi MFA

Zakupu licencji, które obejmują usługi Azure Multi-Factor Authentication, takich jak Azure Active Directory Premium (P1 lub P2) lub pakietu Enterprise Mobility + Security (E3 lub E5) i przypisać je tooyour użytkowników w usłudze Azure Active Directory. 

Jeśli używasz tej opcji, należy utworzyć dostawcę usługi Azure Multi-Factor Authentication tylko wtedy, gdy należy również tooprovide weryfikacji dwuetapowej dla niektórych użytkowników, które nie mają licencji. W przeciwnym razie należy może zostać użyta, dwa razy. 

### <a name="option-3---mfa-consumption-based-model"></a>Opcja 3 - MFA na podstawie zużycia modelu

Utwórz dostawcę usługi Azure Multi-Factor Authentication w ramach subskrypcji platformy Azure. Azure MFA dostawcy są zasobów platformy Azure, które są rozliczane przed Twoje umowy Enterprise Agreement, Azure zobowiązań pieniężnych lub karty kredytowej, takie jak innych zasobów platformy Azure. Tych dostawców można tworzyć tylko w pełnej Azure subskrypcji, innymi subskrypcji platformy Azure, które mają 0 $ limit wydatków. Ograniczone subskrypcje są tworzone podczas aktywacji licencji, podobnie jak w opcjach 1 i 2. 

Podczas korzystania z dostawcy usługi Azure Multi-Factor Authentication, istnieją dwa modele użycia dostępne, które są rozliczane za pośrednictwem subskrypcji platformy Azure:  

1. **Dla każdego użytkownika** — w przypadku przedsiębiorstw, które mają tooenable weryfikacji dwuetapowej dla stałej liczby pracowników, którzy regularnie muszą uwierzytelniania. Rozliczeń dla poszczególnych użytkowników jest oparta na powitania liczbę użytkowników, włączone dla usługi MFA w dzierżawie usługi Azure AD i/lub z serwera usługi Azure MFA. Jeśli użytkownicy są włączone dla usługi MFA w obu usługi Azure AD i serwera usługi Azure MFA i synchronizacji domeny (Azure AD Connect) jest włączona, a następnie możemy liczba hello większy zestaw użytkowników. Jeśli synchronizacja domeny nie jest włączona, a następnie możemy liczba hello sumę wszystkich użytkowników włączone dla usługi MFA w usłudze Azure AD i serwera usługi Azure MFA. Są naliczane proporcjonalnie i podać toohello Commerce systemu codziennie. 

  > [!NOTE]
  > Przykład rozliczeń 1: 5000 użytkowników włączone dla usługi MFA dzisiaj. Hello systemu MFA dzieli ten numer 31, a użytkownicy 161.29 raportów dla danego dnia. Jutro 15 większą liczbę użytkowników, należy włączyć tak hello systemu MFA raporty 161.77 użytkowników do danego dnia. Hello końca cyklu rozliczeniowego hello tooaround 5000 sumuje hello łącznej liczby użytkowników, rozliczane względem subskrypcji platformy Azure. 
  >
  > Przykład rozliczeń 2: masz kombinację użytkowników z licencjami i użytkowników bez, więc toomake dostawcy usługi Azure MFA dla poszczególnych użytkowników, zapasowej hello różnicy. Brak 4500 pakietu Enterprise Mobility + licencji zabezpieczeń w swojej dzierżawy, ale 5000 użytkownikami włączone dla usługi MFA. Subskrypcji platformy Azure jest rozliczany 500 użytkownikom, obliczone proporcjonalnie i codziennie zgłoszone jako 16.13 użytkowników. 

2. **Każde uwierzytelnianie** — w przypadku przedsiębiorstw, które mają tooenable weryfikacji dwuetapowej dla dużej grupy użytkowników, którzy rzadko potrzebują uwierzytelniania. Karta opiera się na powitania liczbę żądań weryfikacji dwuetapowej odebranych przez hello usługi w chmurze Azure MFA, niezależnie od tego, czy te weryfikacji powiedzie się lub nie są dozwolone. Ta karta pojawia się w instrukcji użycia platformy Azure w pakietach 10 uwierzytelnienia, a codziennie jest zgłoszony toohello Commerce systemu. 

  > [!NOTE]
  > Przykład rozliczeń 3: obecnie hello usługi Azure MFA Odebrano 3,105 żądania weryfikacji dwuetapowej. Twoja subskrypcja platformy Azure jest on rozliczany 310.5 pakietów uwierzytelniania. 

Jest ważne toonote może mieć licencji usługi Azure MFA, ale nadal uzyskać rozliczane na podstawie zużycia konfiguracji. Jeśli konfigurujesz dostawcę dla uwierzytelniania usługi Azure MFA rozliczenie jest przeprowadzane przy każdym żądaniu weryfikacji dwuetapowej, nawet te, które wykonywane przez użytkowników, którzy mają licencje. Jeśli należy skonfigurować dostawcę dla poszczególnych użytkowników usługi Azure MFA w domenie, która nie jest połączony tooyour dzierżawy usługi Azure AD, nawet jeśli użytkownicy mają licencje na usługę Azure AD są rozliczane każdego włączonego użytkownika. 

## <a name="next-steps"></a>Następne kroki

- Aby uzyskać więcej informacje o cenach, zobacz [cennik usługi Azure MFA](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

- Wybierz czy toodeploy usługi Azure MFA [w chmurze hello lub lokalnie](multi-factor-authentication-get-started.md)
