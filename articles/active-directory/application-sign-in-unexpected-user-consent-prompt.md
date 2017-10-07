---
title: "monit o zgodę aaaUnexpected przy logowaniu się w aplikacji tooan | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot, gdy użytkownik zobaczy monit o zgodę aplikacja jest zintegrowana z usługą Azure AD, która nie oczekiwano"
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
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a>Monit o zgodę nieoczekiwany przy logowaniu się w aplikacji tooan

Wiele aplikacji, które integrują się z usługą Azure Active Directory wymaga uprawnień toovarious zasobów w kolejności toorun. Jeśli te zasoby są również zintegrowane z usługą Azure Active Directory, wymagany jest ich za pomocą usługi Azure AD hello tooaccess uprawnienia zgoda framework. 

Powoduje to monit o zgodę pokazywane powitania po raz pierwszy jest używana w aplikacji, która często jest to jednorazowa operacja. 

## <a name="scenarios-in-which-users-see-consent-prompts"></a>Scenariusze, w których użytkownicy widzą zgody monitów

Dodatkowe monity można oczekiwać w różnych scenariuszach:

* zestaw uprawnień wymaganych przez aplikację hello Hello zostały zmienione.

* Hello użytkownika, który pierwotnie zgodę toohello aplikacji nie jest administratorem, a teraz różnych (użytkownika niebędącego administratorem) korzysta z aplikacji hello powitania po raz pierwszy.

* Witaj użytkownika, który pierwotnie zgodę toohello aplikacji zostało administrator, ale nie wyrazili zgody w imieniu hello całej organizacji.

* Aplikacja Hello używa [zgody przyrostowych i dynamicznych](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest dodatkowe uprawnienia po początkowym udzielono zgody. Jest to często używane, gdy funkcje opcjonalne dodatkowe aplikacji wymaga uprawnień niż wymagany do obsługi funkcji linii bazowej.

* Zgody został odwołany po początkowym pozwolenia.

* Deweloper Hello skonfigurował toorequire aplikacji hello monit o zgodę za każdym razem, gdy jest używany (Uwaga: to nie jest najlepszym rozwiązaniem).

## <a name="next-steps"></a>Następne kroki

-   [Aplikacje, uprawnienia i zgody w usłudze Azure Active Directory (punkt końcowy 1.0)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [Zakresy, uprawnienia i zgody w hello Azure Active Directory (punktu końcowego v2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


