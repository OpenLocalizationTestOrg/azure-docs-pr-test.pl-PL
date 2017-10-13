---
title: "Co to jest usługa Azure Active Directory?"
description: "Użyj usługi Azure Active Directory można rozszerzyć Twoje istniejące tożsamości lokalnych do chmury lub usługi Azure AD zintegrowane aplikacje."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.assetid: 498820c4-9ebe-42be-bda2-ecf38cc514ca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.custom: it-pro
ms.openlocfilehash: b6746afd508832afbd54153851b6f2ae404af147
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-azure-active-directory"></a>Co to jest usługa Azure Active Directory?
Azure Active Directory (Azure AD) jest wielodostępne firmy Microsoft, chmurze Usługa zarządzania katalogami i tożsamościami. Usługi Azure AD łączy podstawowych usług katalogowych, Zarządzanie zaawansowane tożsamości i zarządzania dostępem do aplikacji. Usługi Azure AD oferuje rozbudowane, opartych na standardach platforma, która umożliwia deweloperom tworzenie kontroli dostępu do aplikacji, na podstawie scentralizowanych zasad i reguł. 

Dla administratorów IT, usługa Azure AD zapewnia ekonomiczny, łatwy w użyciu rozwiązanie do udostępnienia pracownikom i partnerom biznesowym rejestracji jednokrotnej (SSO) [tysięcy chmury aplikacji SaaS](active-directory-saas-tutorial-list.md) , takich jak usługi Office 365, witryny Salesforce.com, DropBox i Concur.

Dla deweloperów aplikacji usługi Azure AD pozwala skupić się na tworzeniu aplikacji, dzięki czemu szybkie i proste do integracji z światowej klasy rozwiązania do zarządzania tożsamościami używane przez miliony organizacji na całym świecie.

Usługi Azure AD zawiera również pełny zestaw możliwości zarządzania tożsamościami, takich jak uwierzytelnianie wieloskładnikowe, rejestracji urządzenia, zarządzanie hasłami samoobsługi, Samoobsługowe zarządzanie grupami, uprzywilejowane konto zarządzania, kontroli dostępu opartej na rolach , monitorowania użycia aplikacji, sformatowanego Inspekcja i monitorowanie zabezpieczeń i alertów. Te możliwości mogą aplikacji bezpiecznego oparte na chmurze, usprawnić procesów IT, zmniejszyć koszty i pozwalają zagwarantować, że są spełnione cele zgodność z zasadami firmowymi.

Ponadto z dokładnie [cztery kliknięć](./connect/active-directory-aadconnect-get-started-express.md), usługi Azure AD można zintegrować z istniejącego systemu Windows Server Active Directory, zapewniając organizacji umożliwia wykorzystanie istniejącej lokalnej inwestycji tożsamości, aby zarządzać dostępem do chmurową aplikacji SaaS.

W przypadku usługi Office 365, Azure lub usługi Dynamics CRM Online klienta może nie Pamiętaj, że korzystasz już z usługi Azure AD. Każdemu dzierżawcy usługi Office 365, Azure i usługi Dynamics CRM jest rzeczywiście już dzierżawa usługi Azure AD. Zawsze, gdy ma się, że możesz rozpocząć korzystanie z tej dzierżawy do zarządzania dostęp do tysięcy inne aplikacje w chmurze Azure AD integruje się z!

![Stos programu Azure AD Connect](./media/active-directory-whatis/Azure_Active_Directory.png)

## <a name="how-reliable-is-azure-ad"></a>Jak niezawodnych jest Azure AD?
Podczas projektowania wielodostępne, rozproszona geograficznie o wysokiej dostępności usługi Azure AD oznacza, że mogą polegać na nim do najważniejszych potrzeb biznesowych. Kończy centrów danych 28 na świecie z automatycznego trybu failover, konieczne będzie wygodnie wiedząc, że usługi Azure AD jest wysoce niezawodne i że nawet jeśli Centrum danych ulegnie awarii, kopie danych katalogu są na żywo w co najmniej dwóch więcej regionalnie rozproszone danych w centrach i dostępny dla natychmiastowy dostęp.

Aby uzyskać więcej informacji, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/).

## <a name="choose-an-edition"></a>Wybierz edition
Wszystkie usługi biznesowe w witrynie Microsoft Online zależą od usługi Azure Active Directory (Azure AD) do logowania i musi innych tożsamości. Jeśli subskrybujesz usług firm Online firmy Microsoft (na przykład usługi Office 365 lub Microsoft Azure), możesz uzyskać usługi Azure AD dostęp do wszystkich funkcji wolne. Z usługi Azure Active Directory bezpłatnej wersji można zarządzać użytkownikami i grupami, synchronizować z lokalnymi katalogami, Pobierz rejestracji jednokrotnej na platformie Azure, Office 365 i tysiące popularnych aplikacji SaaS, takich jak Salesforce, produktu Workday, Concur, DocuSign, Google Aplikacje, okno usługi ServiceNow, Dropbox i więcej. 

Aby ulepszyć usługi Azure Active Directory, możesz dodać płatnych funkcji przy użyciu wersji usługi Azure Active Directory — wersja podstawowa, Premium P1 i Premium P2. Usługi Azure Active Directory płatnej wersje są zbudowane na podstawie istniejącego katalogu bezpłatne, zapewnia enterprise możliwości klasy spanning samoobsługi, rozszerzone monitorowanie, zabezpieczenia raportowania usługi Multi-Factor Authentication (MFA) i bezpieczny dostęp do sieci pracowników mobilnych.

> [!NOTE]
> Do cenników tych wersji, zobacz [Azure Active Directory cennik](https://azure.microsoft.com/pricing/details/active-directory/). Azure Active Directory Premium P1 Premium P2 i Azure Active Directory — wersja podstawowa nie są obecnie obsługiwane w Chinach. Skontaktuj się z nami na Azure Active Directory Forum Aby uzyskać więcej informacji.
>

* **Azure Active Directory — wersja podstawowa** -przeznaczone dla pracowników zadań musi najpierw chmury, ta wersja zawiera chmury aplikacji na dostęp i samoobsługi rozwiązań do zarządzania tożsamościami. W ramach wersji Podstawowa usługi Azure Active Directory uzyskujesz dostęp do funkcji zwiększających produktywność oraz redukujących koszty, takich jak zarządzanie dostępem opartym na grupach, samoobsługowe resetowanie haseł do aplikacji w chmurze oraz serwer proxy aplikacji usługi Azure Active Directory (na potrzeby publikowania lokalnych aplikacji sieci Web przy użyciu usługi Azure Active Directory), z którymi powiązana jest umowa SLA na poziomie przedsiębiorstwa gwarantująca brak awarii przez 99,9% czasu.
* **Azure Active Directory Premium P1** — mające na celu zwiększenie możliwości dostępnych dla organizacji mających więcej wymagających wymagania w zakresie zarządzania tożsamościami i dostępem, Azure Active Directory — wersja Premium dodaje tożsamości przedsiębiorstw bogate możliwości zarządzania i Umożliwia użytkownikom hybrydowego bezproblemowo uzyskiwać dostęp do lokalnych i możliwości w chmurze. Ta wersja oferuje wszystko, czego potrzebujesz dla informacyjnych procesów roboczych oraz administratorów tożsamości w środowiskach hybrydowych na potrzeby funkcji uzyskiwania dostępu do aplikacji, samoobsługowego zarządzania tożsamościami i dostępem, ochrony tożsamości i bezpieczeństwa w chmurze. Obsługuje zaawansowane administracji i delegowanie zasobów, takich jak grupami dynamicznymi i Samoobsługowe zarządzanie grupami. Zawiera program Microsoft Identity Manager (lokalne tożsamości i dostępu do zarządzania pakiet), a zapewnia chmury możliwości zapisu włączania rozwiązań, takich jak samoobsługowego resetowania haseł dla użytkowników lokalnych.
* **Azure Active Directory Premium P2** -zaprojektowany z zaawansowaną ochronę dla wszystkich użytkowników i administratorów, to nową ofertę zawiera wszystkie funkcje w Azure AD Premium P1, a także naszych nowe Identity Protection i tożsamościami uprzywilejowanymi Zarządzanie. Azure Active Directory Identity Protection wykorzystuje miliardów sygnałów w celu zapewnienia ryzyka warunkowego dostępu do aplikacji i najważniejsze dane firmy. Możemy też pomóc chronić kont uprzywilejowanych z usługi Azure Active Directory Privileged Identity Management, więc można wyszukiwać i zarządzać nimi ograniczyć i monitorować administratorów oraz ich dostępu do zasobów i zapewnić dostęp w czasie, gdy jest wymagane.  

> [!NOTE]
> Wiele możliwości usługi Azure Active Directory są dostępne wersje "płatności zgodnie z rzeczywistym użyciem":
>
> * Active Directory B2C to rozwiązanie zarządzania tożsamościami i dostępem dla aplikacji dla użytkownika. Aby uzyskać więcej informacji, zobacz [Azure Active Directory B2C](https://azure.microsoft.com/documentation/services/active-directory-b2c/)
> * Usługa Azure Multi-Factor Authentication może służyć za pośrednictwem dla użytkownika lub dla dostawców uwierzytelniania. Aby uzyskać więcej informacji, zobacz [co to jest uwierzytelnianie wieloskładnikowe Azure?](../multi-factor-authentication/multi-factor-authentication.md)
>

## <a name="how-can-i-get-started"></a>Jak można rozpocząć pracę?

**Jeśli administrator IT:**

* [Wypróbuj](https://azure.microsoft.com/trial/get-started-active-directory/) — można utworzyć konto bezpłatnej 30-dniowej wersji próbnej dzisiaj i wdrożyć pierwsze rozwiązanie chmury w obszarze 5 minut, za pomocą tego łącza

* Odczyt [wprowadzenie do korzystania z usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) dla dzierżawy i uruchomić szybkie porady i wskazówki dotyczące konfigurowania usługi Azure AD

**Jeśli jesteś deweloperem:**
 
* Zapoznaj się z naszym [przewodnik dla deweloperów](active-directory-developers-guide.md) do usługi Azure Active Directory

* [Rozpocznij okres próbny](https://azure.microsoft.com/trial/get-started-active-directory/) — obecnie utworzyć konto bezpłatnej 30-dniowej wersji próbnej i rozpocząć Integrowanie aplikacji z usługą Azure AD

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o podstawowe informacje na temat zarządzania tożsamościami i dostępem platformy Azure](https://docs.microsoft.com/azure/active-directory/identity-fundamentals)
