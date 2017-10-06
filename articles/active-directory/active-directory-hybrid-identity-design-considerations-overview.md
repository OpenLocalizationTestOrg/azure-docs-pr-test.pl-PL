---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości - Przegląd | Dokumentacja firmy Microsoft"
description: "Omówienie i Mapa zawartości z przewodnika po zagadnieniach dotyczących projektowania tożsamości hybrydowej"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 100509c4-0b83-4207-90c8-549ba8372cf7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 10aacb04c90abd100eb56d7c44d590946b052f18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations"></a>Zagadnienia dotyczące projektowania tożsamości hybrydowej usługi Azure Active Directory
Konsumenckie urządzeń są rozmnażające Witaj świecie firmy i oprogramowania jako usługa (SaaS) aplikacji działających w chmurze są łatwe tooadopt. W związku z tym zachowaniu kontroli nad dostęp do aplikacji użytkowników wewnętrznych platformach centrów danych i w chmurze może być trudne.  

Firmy Microsoft tożsamościach span lokalnych i chmurze możliwości tworzenia tożsamością jednego użytkownika do uwierzytelniania i autoryzacji zasobów tooall, bez względu na lokalizację. Nazywamy to tożsamość hybrydowa. Istnieją różne opcje projektowania i konfiguracji dla tożsamość hybrydowa korzystania z rozwiązań firmy Microsoft, a w niektórych przypadkach może być trudne toodetermine kombinację najlepiej spełniającą hello potrzeb organizacji. 

Ten przewodnik zagadnienia dotyczące projektowania tożsamości hybrydowego pomoże Ci toounderstand jak toodesign hybrydowego tożsamości, która najlepiej odpowiada hello biznesowych i technologicznych potrzeb organizacji.  Ten przewodnik zawiera szczegóły serii kroków i zadań, czy można wykonać toohelp Projektowanie rozwiązania z tożsamością hybrydową spełniającego specyficzne wymagania danej organizacji. W ramach zadań i kroków hello hello przewodnik przedstawia hello odpowiednich technologii i funkcji toomeet tooorganizations dostępne opcje funkcjonalności i jakości usługi (np. dostępność, skalowalność, wydajność, możliwości zarządzania i bezpieczeństwo) wymagań dotyczących poziomu. 

W szczególności cele przewodnik zagadnienia dotyczące projektu w tożsamości hybrydowego hello są hello tooanswer następujące pytania: 

* Co zrobić pytania I wymagają tooask i odpowiedzi toodrive hybrydowego tożsamości specyficzne dla technologii lub dziedziny problemu czy najlepiej odpowiadają wymaganiom?
* Jaką sekwencję działań należy zakończeniu toodesign rozwiązania z tożsamością hybrydową dla hello technologii lub dziedziny problemu? 
* Jakie hybrydowego tożsamości technologii i opcje konfiguracji są toohelp dostępny me spełnienie moich wymagań? Co to są kompromisy hello jedną z tych opcji, w którym można wybrać hello najlepszym rozwiązaniem dla firmy?

## <a name="who-is-this-guide-intended-for"></a>Kogo jest przeznaczony ten przewodnik?
 CIO, CITO, architektów tożsamości główny, architektów przedsiębiorstwa i architekci systemów informatycznych odpowiedzialni za projektowanie rozwiązania z tożsamością hybrydową dla średnich i dużych organizacji.

## <a name="how-can-this-guide-help-you"></a>Jak może być pomocny ten przewodnik?
Można użyć tego przewodnika toounderstand jak toodesign rozwiązania z tożsamością hybrydową, który jest w stanie toointegrate chmurę na podstawie tożsamości systemu zarządzania z bieżącym lokalnego rozwiązania z tożsamością. 

powitania po grafika przedstawia przykład rozwiązania z tożsamością hybrydową umożliwiający ich bieżącego systemu Windows Server Active Directory rozwiązania, znajdujących się na lokalnym Microsoft Azure Active Directory tooenable użytkowników toouse jednym toointegrate toomanage Administratorzy IT Logowania jednokrotnego (SSO) w aplikacjach znajdujących się w chmurze hello i lokalnych.

![](./media/hybrid-id-design-considerations/hybridID-example.png)

Witaj powyżej ilustracji jest przykładem rozwiązania z tożsamością hybrydową wykorzystujący chmury usług toointegrate z funkcjami lokalnymi w kolejności tooprovide proces uwierzytelniania użytkownika końcowego toohello pojedynczego środowisko i toofacilitate IT zarządzanie te zasoby. Chociaż może to być bardzo typowy scenariusz, projektowania tożsamości hybrydowej każda organizacja jest prawdopodobnie toobe inne niż przykład Witaj przedstawione na rysunku 1 z powodu toodifferent wymagania. 

Ten przewodnik zawiera serię kroków i zadań, czy można wykonać toodesign rozwiązania z tożsamością hybrydową spełniającego specyficzne wymagania danej organizacji. Poniższe kroki i zadania, hello przewodnik przedstawia informacje o liczbie hello odpowiednich technologii i funkcji w całym hello opcje dotyczące poziomu jakości funkcjonalności i usługi toomeet tooyou dostępne dla Twojej organizacji.

**Założenia**: użytkownik ma pewne doświadczenie z systemu Windows Server, usług domenowych w usłudze Active Directory i Azure Active Directory. W tym dokumencie przyjęto założenie, że użytkownik chce się dowiedzieć, jak te rozwiązania mogą spełnić potrzeby biznesowe samodzielnie lub w rozwiązaniu zintegrowanym.

## <a name="design-considerations-overview"></a>Omówienie zagadnień dotyczących projektowania
Ten dokument zawiera zestaw kroków i zadań, czy można wykonać toodesign hybrydowego tożsamości, która najlepiej odpowiada wymaganiom. Witaj kroki są prezentowane w uporządkowanej kolejności. Zagadnienia dotyczące projektowania, które użytkownik pozna w kolejnych krokach może wymagać toochange decyzji podjętych we wcześniejszych krokach, jednak powodu tooconflicting decyzji projektowych. Każdy podejmowana jest tooalert możesz toopotential konfliktami projektowymi hello dokumentu. 

Pojawią się na powitania projekt najlepiej spełniający wymagania dopiero po wykonaniu kroków tyle razy, ile to konieczne tooincorporate hello wszystkich zagadnień hello w dokumencie hello. 

| Faza tożsamości hybrydowej | Lista tematów |
| --- | --- |
| Określenie wymagań dotyczących tożsamości |[Określanie potrzeb biznesowych](active-directory-hybrid-identity-design-considerations-business-needs.md)<br> [Określenie wymagań synchronizacji katalogu](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)<br> [Określić wymagania dotyczące uwierzytelniania wieloskładnikowego](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)<br> [Definiowanie strategii wdrażania tożsamości hybrydowej](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md) |
| Planowanie wzmocnienia bezpieczeństwa danych za pośrednictwem rozwiązania silnej tożsamości |[Określenie wymagań dotyczących ochrony danych](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md) <br> [Określenie wymagań dotyczących zarządzania zawartością](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)<br> [Określenie wymagań dotyczących kontroli dostępu](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)<br> [Określenie wymagań dotyczących odpowiedzi na zdarzenia](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) <br> [Definiowanie strategii ochrony danych](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) |
| Plan cyklu życia tożsamości hybrydowej |[Określić zadań zarządzania tożsamości hybrydowej](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) <br> [Zarządzanie synchronizacji](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)<br> [Określić strategii wdrażania zarządzania tożsamości hybrydowej](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md) |

## <a name="download-this-guide"></a>Pobierz w tym przewodniku
Można pobrać wersję pdf hello zagadnienia dotyczące projektowania tożsamości hybrydowej przewodnika z hello [galerii Technet](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288). 

