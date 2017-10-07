---
title: "AAA wystąpił nieoczekiwany błąd podczas wykonywania aplikacji tooan zgody | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono błędów, które mogą wystąpić w trakcie procesu hello zgodę tooan aplikacji i co można zrobić o nich"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: dfee35f3a10e3cc4313109cedd972499452320f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-error-when-performing-consent-tooan-application"></a>Wystąpił nieoczekiwany błąd podczas wykonywania zgody tooan aplikacji

W tym artykule omówiono błędów, które mogą wystąpić w trakcie procesu hello zgodę tooan aplikacji. Jeśli jesteś rozwiązywanie nieoczekiwany zgody monity nie zawiera komunikaty o błędach, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).

Wiele aplikacji, które integrują się z usługą Azure Active Directory wymaga uprawnienia tooaccess innych zasobów w kolejności toofunction. Jeśli te zasoby są również zintegrowane z usługą Azure Active Directory, tooaccess uprawnień, ich jest często żądana za pomocą wspólnego hello zgoda framework. 

Powoduje to monit o zgodę będzie wyświetlany, którego działanie ma zazwyczaj miejsce powitania po raz pierwszy aplikacja jest używana, ale może również wystąpić w kolejnych za pomocą aplikacji hello.

Określone warunki musi mieć wartość true dla uprawnienia toohello tooconsent użytkownika, który wymaga aplikacji. Jeśli te warunki nie są spełnione, mogą wystąpić różne błędy. Należą do nich:

## <a name="requesting-not-authorized-permissions-error"></a>Błąd uprawnień nie Autoryzowano żądania
* **AADSTS90093:** &lt;clientAppDisplayName&gt; żąda jedno lub więcej uprawnień, które nie są autoryzowane toogrant. Skontaktuj się z administratorem, który można wyrazić zgodę toothis aplikacji w Twoim imieniu.

Ten błąd występuje, gdy użytkownik, który nie jest administratorem firmy próbuje toouse aplikacji, która żąda uprawnienia, których może udzielić tylko administrator. Ten błąd można rozwiązać przez administratora udzielanie dostępu toohello aplikacji w imieniu swojej organizacji.

## <a name="policy-prevents-granting-permissions-error"></a>Zasady uniemożliwiają udzielanie uprawnień błąd
* **AADSTS90093:** administrator &lt;tenantDisplayName&gt; ustawił zasadę, która uniemożliwia udzielanie &lt;Nazwa aplikacji&gt; hello żąda uprawnień. Skontaktuj się z administratorem &lt;tenantDisplayName&gt;, który można przyznać uprawnień toothis aplikacji w Twoim imieniu.

Ten błąd występuje, gdy administrator firmy wyłącza możliwość hello tooapplications tooconsent użytkowników, a następnie użytkownik bez uprawnień administratora próbuje toouse aplikację, która wymaga zgody. Ten błąd można rozwiązać przez administratora udzielanie dostępu toohello aplikacji w imieniu swojej organizacji.

## <a name="intermittent-problem-error"></a>Problem tymczasowy błąd
* **AADSTS90090:** prawdopodobnie wystąpił problem tymczasowy rejestrowania uprawnienia hello podjęto zbyt toogrant&lt;clientAppDisplayName&gt;. Spróbuj ponownie później.

Ten błąd wskazuje, że wystąpił problem po stronie usługi tymczasowymi. Można go rozwiązać przez podejmowanie próby tooconsent toohello ponownie aplikację.

## <a name="resource-not-available-error"></a>Zasób nie jest dostępny błąd
* **AADSTS65005:** aplikacji hello &lt;clientAppDisplayName&gt; wymagane uprawnienia tooaccess zasobu &lt;resourceAppDisplayName&gt; jest niedostępny. 

Skontaktuj się z deweloperem aplikacji hello.

##  <a name="resource-not-available-in-tenant-error"></a>Zasób nie jest dostępna w błąd dzierżawy
* **AADSTS65005:** &lt;clientAppDisplayName&gt; żąda dostępu do zasobów tooa &lt;resourceAppDisplayName&gt; które nie są dostępne w Twojej organizacji &lt; tenantDisplayName&gt;. 

Upewnij się, że ten zasób jest dostępny, lub skontaktuj się z administratorem &lt;tenantDisplayName&gt;.

## <a name="permissions-mismatch-error"></a>Błąd niezgodności uprawnień
* **AADSTS65005:** aplikacji hello żądany zasób tooaccess zgody &lt;resourceAppDisplayName&gt;. To żądanie nie powiodło się, ponieważ nie jest zgodny, jak aplikacja hello zostało wstępnie skonfigurowane podczas rejestracji aplikacji. Skontaktuj się z hello aplikacji vendor.* *

Wszystkie błędy występują, jeśli aplikacja hello użytkownik próbuje toois tooconsent żąda uprawnienia tooaccess aplikacji zasobów, której nie można znaleźć w katalogu organizacji hello (dzierżawcy). Taka sytuacja może wystąpić z kilku powodów:

-   Deweloper aplikacji Hello klienta ma ich stosowania nieprawidłowo skonfigurowane, powodowania toorequest dostępu tooan nieprawidłowy zasób. W takim przypadku Deweloper aplikacji hello należy zaktualizować konfigurację hello powitania klienta aplikacji tooresolve ten problem.

-   Nazwy głównej usługi reprezentujący hello docelowego zasobu aplikacji nie istnieje w organizacji hello lub istniał w przeszłości hello, ale została usunięta. Ten problem, nazwy głównej usługi hello zasobów aplikacji musi być udostępnione w organizacji hello tak powitania klienta aplikacji można zażądać uprawnień tooit tooresolve. Może to wystąpić w różne sposoby, w zależności od typu hello aplikacji, w tym:

    -   Uzyskiwanie subskrypcji dla aplikacji zasobów hello (Firma Microsoft opublikowała aplikacji)

    -   Zgodę toohello zasobów aplikacji

    -   Udzielanie uprawnień aplikacji hello za pośrednictwem hello portalu Azure

    -   Dodawanie aplikacji hello z hello galerii aplikacji usługi Azure AD

## <a name="next-steps"></a>Następne kroki 

[Aplikacje, uprawnienia i zgody w usłudze Azure Active Directory (punkt końcowy v1)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[Zakresy, uprawnienia i zgody w hello Azure Active Directory (punktu końcowego v2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


