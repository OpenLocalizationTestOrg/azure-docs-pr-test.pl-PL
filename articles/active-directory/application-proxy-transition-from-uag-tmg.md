---
title: aaaUpgrade tooAzure AD serwera Proxy aplikacji | Dokumentacja firmy Microsoft
description: "Wybierz, jakie rozwiązanie do serwera proxy jest najlepsze w przypadku uaktualniania z programu Microsoft Forefront lub Unified bramy dostępu."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7dc2633140b384e25792470dadbb7f3fa7992a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="compare-remote-access-solutions"></a>Porównanie rozwiązań dostępu zdalnego

Azure Active Directory serwera Proxy aplikacji jest jednym z dwóch rozwiązań dostępu zdalnego, które firma Microsoft oferuje. Witaj innych jest Proxy aplikacji sieci Web, hello lokalnej wersji. Te dwa rozwiązania Zastąp starsze produkty, które oferowane przez firmy Microsoft: Microsoft Forefront Threat Management bramy (TMG) i Unified Access Gateway (UAG). Użyj tego artykułu toounderstand porównanie tych rozwiązań cztery tooeach innych. Dla osób, które nadal przy użyciu hello przestarzałe TMG lub UAG rozwiązań, użyj tego planu toohelp artykułu tooone Twojego migracji z serwera Proxy aplikacji hello. 


## <a name="feature-comparison"></a>Porównanie funkcji

Użyj tej tabeli toounderstand porównanie tooeach innych Threat Management Gateway (TMG), Unified Access Gateway (UAG), serwer Proxy aplikacji sieci Web (WAP) i serwera Proxy aplikacji usługi Azure AD (AP).

| Funkcja | TMG | UAG | WAP | Interfejs API |
| ------- | --- | --- | --- | --- |
| Uwierzytelnianie certyfikatu | Tak | Tak | - | - |
| Selektywnie publikować aplikacje przeglądarki | Tak | Tak | Tak | Tak |
| Wstępnego uwierzytelniania i pojedynczego logowania jednokrotnego | Tak | Tak | Tak | Tak | 
| Warstwy 2/3 zapory | Tak | Tak | - | - |
| Funkcje serwera proxy do przodu | Tak | - | - | - |
| Funkcje sieci VPN | Tak | Tak | - | - |
| Obsługa protokołu sformatowanego | - | Tak | Tak, jeśli uruchomiony za pośrednictwem protokołu HTTP | Tak, jeśli uruchomiony za pośrednictwem protokołu HTTP lub za pośrednictwem bramy usług pulpitu zdalnego |
| Służy jako serwer proxy usług AD FS | - | Tak | Tak | - |
| Jednego portalu dostępu do aplikacji | - | Tak | - | Tak |
| Tłumaczenie łącze treści odpowiedzi | Tak | Tak | - | Tak | 
| Uwierzytelnianie za pomocą nagłówków | - | Tak | - | Tak, z PingAccess | 
| Zabezpieczenia w skali chmury | - | - | - | Tak | 
| Dostęp warunkowy | - | Tak | - | Tak |
| Brak składników w hello strefą zdemilitaryzowaną (DMZ) | - | - | - | Tak |
| Nie połączenia przychodzące | - | - | - | Tak |

W przypadku większości scenariuszy zalecamy aplikacji usługi Azure AD jako nowoczesnego rozwiązania hello. Serwer Proxy aplikacji sieci Web jest tylko preferowane w scenariuszach wymagających serwera proxy usług AD FS i nie można używać niestandardowych domen w usłudze Azure Active Directory. 

Serwera Proxy aplikacji usługi Azure AD oferują unikatowe korzyści, kiedy porównaniu toosimilar produktów, w tym:

- Rozszerzanie zasobów lokalnych tooon usługi Azure AD
   - Skali chmury zabezpieczenia i ochrona
   - Funkcje, takie jak dostęp warunkowy i usługa Multi-Factor Authentication są łatwe tooenable
- Nie componenet w strefą zdemilitaryzowaną hello
- Nie połączenia przychodzące wymagane
- Panel jedno dostępu użytkownikom można przejść toofor wszystkich aplikacji, włącznie z usługi Office 365, Azure AD zintegrowanych aplikacji SaaS i lokalnej sieci web aplikacji. 


## <a name="next-steps"></a>Następne kroki

- [Korzystanie z aplikacji lokalnej tooon bezpieczny dostęp zdalny tooprovide aplikacji usługi Azure AD](active-directory-application-proxy-get-started.md)
- [Przejście z programu Forefront TMG i UAG tooApplication Proxy](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/).
