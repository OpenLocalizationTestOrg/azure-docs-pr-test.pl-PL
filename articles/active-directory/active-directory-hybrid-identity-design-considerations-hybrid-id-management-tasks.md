---
title: "tożsamość hybrydowa usługi Active Directory aaaAzure zagadnienia dotyczące projektowania - Określ zadań zarządzania tożsamości hybrydowej | Dokumentacja firmy Microsoft"
description: "Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza hello określonych warunków, można wybrać podczas uwierzytelniania użytkownika hello i przed zezwoleniem na dostęp toohello aplikacji. Gdy te warunki są spełnione, użytkownik hello uwierzytelniony i dozwolone dostępu toohello aplikacji."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 65f80aea-0426-4072-83e1-faf5b76df034
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: d3c0e9b23f43127b3d8e0b3a4e8f03d4bc148c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-hybrid-identity-lifecycle"></a>Plan cyklu życia tożsamości hybrydowej
Tożsamość jest jednym z podstaw hello enterprise mobility i stosowania strategii dostępu. Czy logujesz się na urządzeniu przenośnym tooyour lub aplikacji SaaS, tożsamości jest hello toogaining klucza dostępu tooeverything. Na najwyższym poziomie rozwiązania do zarządzania tożsamościami obejmuje połączenie i synchronizacja między repozytoriami tożsamości, co obejmuje automatyzacji i scentralizowany hello proces inicjowania obsługi administracyjnej zasobów. rozwiązania z tożsamością Hello powinien być scentralizowane tożsamości w ramach lokalnej i w chmurze i również użyć jakiegoś tożsamości federacyjnych toomaintain scentralizowane uwierzytelnianie i bezpiecznie udziału i współpracować z użytkowników zewnętrznych i firm. Zasoby należeć do zakresu od systemów operacyjnych i aplikacji toopeople w lub powiązane z organizacji. Struktura organizacyjna może być zmieniony tooaccommodate hello inicjowania obsługi zasad i procedur.

Toohave tożsamości rozwiązanie dostosowane tooempower użytkowników przez zapewnienie im z ważne jest również samoobsługi napotyka tookeep ich wydajność. Rozwiązania tożsamości jest bardziej niezawodną metodą, jeśli umożliwia logowanie jednokrotne użytkowników we wszystkich zasobów hello potrzebują dostępu administratorów na wszystkich poziomach standardowych procedur można użyć do zarządzania poświadczeniami użytkownika. Niektóre poziomy administracyjnej można zredukować lub usunięte, w zależności od szerokości hello hello inicjowania obsługi administracyjnej rozwiązania do zarządzania. Ponadto można bezpiecznie rozpowszechniać możliwości administrowania ręcznie lub automatycznie, między różnymi organizacjami. Na przykład administrator domeny może obsługiwać tylko osoby hello oraz zasoby w tej domenie. Tego użytkownika mogą wykonywać zadania administracyjne i inicjowania obsługi administracyjnej, ale jest nie Autoryzowano toodo zadania konfiguracji, takich jak tworzenie przepływów pracy.

## <a name="determine-hybrid-identity-management-tasks"></a>Określić zadań zarządzania tożsamości hybrydowej
Przesyłanie zadań administracyjnych w organizacji zwiększa dokładność hello i efektywności administracji i zwiększa hello Równoważenie obciążenia hello organizacji. Poniżej przedstawiono przestawień hello, definiujące tożsamości niezawodny system zarządzania.

 ![](./media/hybrid-id-design-considerations/Identity_management_considerations.png)

zadania zarządzania tożsamości hybrydowej toodefine, należy poznać niektóre istotne cechy hello organizacji, która zostanie przyjęty tożsamość hybrydowa. Jest ważne toounderstand hello bieżącego repozytoriów używane dla tożsamości źródeł. Znając te podstawowe elementy, konieczne będzie hello podstawowych wymagań i na podstawie należy tooask bardziej szczegółowe pytania który doprowadzi tooa lepszego projektowania decyzji rozwiązania tożsamości.  

Podczas definiowania tych wymagań, upewnij się, że hello co najmniej następujące odpowiedzi na pytania

* Opcje inicjowania obsługi: 
  
  * Rozwiązania z tożsamością hybrydową hello obsługuje niezawodny konta dostępu do zarządzania i inicjowania obsługi administracyjnej systemu?
  * W jaki sposób użytkowników, grup i haseł mają toobe zarządzane?
  * Zarządzanie cyklem życia tożsamości hello jest elastyczny? 
    * Jak długo zawieszenie konta aktualizacji hasła podąża?
* Zarządzanie licencjami: 
  
  * Wykonuje hello hybrydowe rozwiązanie uchwytów licencji Zarządzanie tożsamościami?
    * Jeśli tak, jakie funkcje są dostępne?
* Wykonuje hello rozwiązania dojście licencji na podstawie grupy zarządzania? 
  
      - Jeśli tak, czy jest możliwe tooassign tooit grupy zabezpieczeń? 
       - Jeśli tak, katalogiem w chmurze hello automatycznie przypisze licencji tooall hello członkami grupy hello? 
        - Co się stanie, jeśli użytkownik jest następnie dodane do lub usunięte z grupy hello, zostaną licencji automatycznie przypisane lub usunięte odpowiednio? 
* Integracja z innych dostawców tożsamości innych firm:
* To rozwiązanie hybrydowe można zintegrować z tożsamości innych firm dostawców tooimplement rejestracji jednokrotnej?
* Jest to możliwe toounify wszystkie hello dostawców tożsamości innego systemu spójnych tożsamości?
* Jeśli tak, jak i które są one i jakie funkcje są dostępne?

## <a name="synchronization-management"></a>Zarządzanie synchronizacji
Jednym z celów hello identity manager w stanie toobring toobe hello wszystkich dostawców tożsamości i przechowywać zsynchronizowane. Zachowaj dane hello synchronizowane oparte na dostawcy tożsamości wzorca autorytatywnych. W scenariuszu hybrydowym tożsamości, z modelem zarządzania zsynchronizowane wszystkich tożsamości użytkowników i urządzeń w lokalnym serwerze zarządzania i zsynchronizować hello konta i, opcjonalnie, chmury toohello hasła. Witaj użytkownik wprowadza hello tego samego hasła lokalnie jak użytkownik w chmurze hello i na logowanie, hasło hello jest weryfikowany przez hello rozwiązania z tożsamością. Ten model korzysta z narzędzia synchronizacji katalogów.

![](./media/hybrid-id-design-considerations/Directory_synchronization.png)Synchronizacja hello tooproper projektowania rozwiązania z tożsamością hybrydową upewnij się, odpowiedzi na tym hello następujące pytania: •, jakie są dostępne dla rozwiązania z tożsamością hybrydową hello rozwiązania synchronizacji hello?
• Co to są hello logowania jednokrotnego możliwości są dostępne?
•, Jakie są opcje hello Federację tożsamości między B2B i B2C?

## <a name="next-steps"></a>Następne kroki
[Określić strategii wdrażania zarządzania tożsamości hybrydowej](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)

## <a name="see-also"></a>Zobacz też
[Omówienie zagadnień dotyczących projektowania](active-directory-hybrid-identity-design-considerations-overview.md)

