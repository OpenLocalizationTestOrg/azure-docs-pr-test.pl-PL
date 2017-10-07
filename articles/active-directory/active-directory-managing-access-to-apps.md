---
title: "aaaManaging tooapps dostępu za pomocą usługi Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak Azure Active Directory umożliwia organizacjom toospecify hello aplikacji toowhich każdy użytkownik ma dostęp."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: b0829f18-9e57-4107-925d-5f0457d81671
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: b9461b7a1cc8913cd8fb4a4ce0778afe03274935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-access-tooapps"></a>Zarządzanie tooapps dostępu
Zarządzanie dostępem trwającą, użycia oceny i raportowania nadal toobe żądanie po aplikacji jest zintegrowany system obsługi tożsamości organizacji. W wielu przypadkach administratorzy IT lub pomocą techniczną ma tootake trwającą aktywną rolę w zarządzaniu aplikacjami tooyour dostępu. Czasami przypisania jest wykonywane przez zespół IT ogólne lub działów. Często decyzja przypisania hello jest zamierzone toobe toohello delegowanego firm podejmującą, wymaganie zatwierdzenia przed IT sprawia, że hello przypisania.  Inne organizacje inwestycji w Integracja z istniejącą automatycznych tożsamościami i dostępem system zarządzania, takich jak kontrola dostępu oparta na rolach (RBAC) lub kontroli dostępu na podstawie atrybutu (ABAC). Zarówno hello integracji i rozwoju reguły zwykle toobe specjalistyczne i kosztowne. Monitorowania i raportowania w obu podejścia do zarządzania jest inwestycji oddzielne, kosztowne i skomplikowane.

## <a name="how-does-azure-active-directory-help"></a>Jak pomaga usługi Azure Active Directory?
 Azure AD obsługuje szeroką gamę access management dla skonfigurowanych aplikacji, włączanie tooeasily organizacji osiągnięcie zasad odpowiednich uprawnień dostępu powitania od przypisania automatycznego, opartych na atrybutach (scenariusze ABAC lub RBAC) za pośrednictwem przedstawicielstwa i tym Zarządzanie administratorami. Z usługą Azure AD można łatwo uzyskać złożone zasady łączenie wielu modeli zarządzania dla jednej aplikacji i może nawet ponownego użycia zasad zarządzania w aplikacjach z hello tej samej grupy odbiorców.

* [Dodawanie nowych lub istniejących aplikacji](active-directory-sso-integrate-saas-apps.md)

 Przypisanie aplikacji usługi Azure AD koncentruje się na dwóch trybów przypisania głównej:

* **Przypisanie poszczególnych** administratora z uprawnieniami administratora globalnego katalogu można wybrać poszczególnych kont użytkowników i przyznano im dostęp do aplikacji toohello.
* **Przypisanie oparte na grupach (płatnej tylko usługi Azure AD)** administratora z uprawnieniami administratora globalnego katalogu można przypisać grupie aplikacji toohello. Dostęp do określonych użytkowników wynika, czy są oni członkami grupy hello w czasie hello próbują tooaccess hello aplikacji. Innymi słowy administrator może efektywnie utworzyć regułę przypisania, podając "wszelkie bieżący element członkowski hello przypisane grupie ma dostęp toohello aplikacji". Użycie tej opcji przypisania, Administratorzy mogą korzystać z tych opcji zarządzania grupami usługi Azure AD, w tym [opartych na atrybutach grup dynamicznych](active-directory-accessmanagement-manage-groups.md), grup systemu zewnętrznego (na przykład w infrastrukturze lokalnej usługi Active Directory lub pracy), lub zarządzana przez administratora lub zarządzane eksploatacyjnych niezależne grup. Pojedynczej grupy można łatwo przypisać aplikacje toomultiple zapewnienie, że aplikacje przypisania koligacji mogą współużytkować reguły przypisania zmniejszenie hello ogólną złożoność zarządzania. Należy pamiętać, że grup zagnieżdżonych członkostwa nie są obsługiwane dla tooapplications przypisywania na podstawie grupy w tej chwili.

Korzystanie z tych trybów dwóch przypisania, Administratorzy można osiągnąć wszystkie przypisania pożądane podejścia do zarządzania.

Z usługą Azure AD użycia i przydział raportowania jest w pełni zintegrowana, umożliwiające administratorom tooeasily raportu na stan przypisania, błędy przydziału i użycia nawet.

## <a name="complex-application-assignment-with-azure-ad"></a>Przypisanie złożonych aplikacji z usługą Azure AD
Należy wziąć pod uwagę aplikacji, takie jak Salesforce. W wielu organizacjach Salesforce jest używany głównie przez organizacje hello sprzedaży i marketingu. Często członkowie zespołu marketingu hello ma wysoce uprzywilejowane tooSalesforce dostępu, gdy członkowie zespołu sprzedaży hello mają ograniczony dostęp do. W wielu przypadkach szerokie populacji pracowników przetwarzających informacje mieć ograniczony dostęp toohello aplikacji. Wyjątki reguł toothese skomplikować kwestii. Często jest hello prawa poszczególnych hello marketing lub sprzedaży kierowniczej zespoły toogrant dostępu użytkowników lub zmienić ich ról niezależnie od zasady ogólne.

Z usługą Azure AD można wstępnie skonfigurowane dla rejestracji jednokrotnej (SSO) i automatyczne Inicjowanie obsługi aplikacji, takich jak Salesforce. Po skonfigurowaniu aplikacji hello Administrator może potrwać hello Akcja jednorazowa toocreate i przypisz hello odpowiednich grup. W tym przykładzie administrator może wykonać następujące przydziały hello:

* [Grupami dynamicznymi](active-directory-accessmanagement-manage-groups.md) może być tooautomatically zdefiniowanych reprezentować wszystkie elementy członkowskie hello sprzedaży i marketingu zespołami za pomocą atrybutów, takich jak dział lub roli:
  
  * Wszyscy członkowie grupy marketing będzie mieć przypisaną rolę "marketing" toohello w usłudze Salesforce
  * Wszystkie elementy członkowskie sprzedaży zespołu grup może zostać przypisana rola "sprzedaż" toohello w usłudze Salesforce. Dalsze dopracowanie można użyć wielu grup, które reprezentują regionalnych zespoły przypisane role Salesforce toodifferent.
* mechanizm wyjątków hello tooenable, grupę samoobsługi mógł zostać utworzony dla każdej roli. Na przykład grupę "Salesforce marketingu wyjątek" hello można utworzyć jako grupa samoobsługi. Grupa Hello może być przypisana rola marketing Salesforce toohello i hello marketing kadry kierowniczej mogą być dokonywane właścicieli. Członkowie kadry kierowniczej marketing hello można dodać lub usunąć użytkowników, ustawić zasady sprzężenia, lub nawet zatwierdzenia lub odmowy toojoin żądań poszczególnych użytkowników. Jest to obsługiwane przez środowisko odpowiednie procesu roboczego informacje, które nie wymagają specjalistyczne szkolenie właścicieli lub elementy członkowskie.

W takim przypadku wszystkich użytkowników przypisanych będzie automatycznie aprowizowanego tooSalesforce, ponieważ są one grupy dodane toodifferent, ich przypisania roli będzie aktualizowany w usłudze Salesforce. Użytkownicy będą toodiscover może być i uzyskiwać dostęp do usług Salesforce, za pomocą panelu dostępu aplikacji Microsoft hello, klientom sieci web pakietu Office, lub nawet przechodząc tootheir organizacyjnej strony logowania usługi Salesforce. Administratorzy będą mogli tooeasily widoku użycia i przydział stan za pomocą raportów usługi Azure AD.

Administratorzy mogą stosować [dostępu warunkowego dla usługi Azure AD](active-directory-conditional-access.md) tooset zasady dostępu dla określonych ról. Zasady te mogą obejmować, czy dostęp jest dozwolony poza hello środowiska firmy, a nawet usługi Multi-Factor Authentication lub dostęp tooachieve wymagania dotyczące urządzeń w przypadku różnych.

## <a name="how-can-i-get-started"></a>Jak można rozpocząć pracę?
Pierwszy, jeśli nie używasz już usługi Azure AD i administratora IT:

* [Wypróbuj](https://azure.microsoft.com/trial/get-started-active-directory/) — można Załóż bezpłatne 30-dniowej wersji próbnej już dzisiaj i wdrażania rozwiązania pierwsze chmury w obszarze 5 minut, za pomocą tego łącza

Azure AD funkcje, które umożliwiają udostępnianie konta:

* [Przypisanie do grupy](active-directory-accessmanagement-self-service-group-management.md)
* Dodawanie aplikacji tooAzure AD
* Wprowadzenie do przypisania
* Przypisanie aplikacji — często zadawane pytania
* [Raporty pulpitu nawigacyjnego użycia aplikacji](active-directory-passwords-get-insights.md)

## <a name="where-can-i-learn-more"></a>Gdzie można dowiedzieć się więcej?
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Ochrona aplikacji przy użyciu dostępu warunkowego](active-directory-conditional-access.md)
* [Zarządzanie grupami samoobsługi/SSAA](active-directory-accessmanagement-self-service-group-management.md)

