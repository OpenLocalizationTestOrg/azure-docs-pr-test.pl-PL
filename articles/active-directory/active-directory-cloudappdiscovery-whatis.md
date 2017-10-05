---
title: "Znajdowanie aplikacji w chmurze niezarządzane z usługi Cloud App Discovery | Dokumentacja firmy Microsoft"
description: "Zawiera informacje o znajdowanie aplikacji i zarządzanie nimi z Cloud App Discovery, jakie są zalety i jak działa."
services: active-directory
keywords: "Usługa cloud app discovery, zarządzanie aplikacjami"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6284ff5bac8edbc19561d0916adef153526dfbe3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a>Znajdowanie niezarządzanych aplikacji w chmurze z usługi Cloud App Discovery
## <a name="overview"></a>Omówienie
W przedsiębiorstwach nowoczesnego działu IT często nie są znane wszystkich aplikacji korzystających z członków organizacji ich w pracy w chmurze. To proste zobaczyć, dlaczego Administratorzy byłyby problemów dotyczących nieautoryzowanego dostępu do danych firmowych, wycieku danych i inne zagrożenia dla bezpieczeństwa. To Brak świadomości ułatwia tworzenie planu zajmowanie się te zagrożenia bezpieczeństwa wydawać się czasochłonnym zadaniem.

Usługa cloud App Discovery jest funkcją Premium usługi Azure Active Directory (AD), który umożliwia odnalezienie aplikacji w chmurze używane przez osoby z Twojej organizacji.

**Usługa Cloud App Discovery można:**

* Znajdź używane aplikacje w chmurze i pomiar wykorzystanie przez liczbę użytkowników, ilości ruchu lub liczbę żądań sieci web do aplikacji.
* Określenie użytkowników, którzy korzystają z aplikacji.
* Eksportowanie danych do analizy w trybie offline.
* Przenoszenie tych aplikacji pod kontrolą IT i Włącz funkcji logowania jednokrotnego do zarządzania użytkownikami.

## <a name="how-it-works"></a>Jak to działa
1. Aplikacja użycia agenci są zainstalowani na komputerach użytkowników.
2. Informacje o użyciu aplikacji przechwycone przez agentów są wysyłane za pośrednictwem kanału bezpieczne, zaszyfrowane do usługi odnajdywania aplikacji w chmurze.
3. Usługa Cloud App Discovery ocenia dane i generuje raporty.

![Diagram odnajdywania aplikacji w chmurze](./media/active-directory-cloudappdiscovery/cad01.png)

Aby rozpocząć pracę z usługi Cloud App Discovery, zobacz [pobierania uruchomiona z Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)

## <a name="related-articles"></a>Pokrewne artykuły:
* [Cloud App Discovery zabezpieczeń i zagadnienia dotyczące ochrony prywatności](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [Przewodnik wdrażania zasad grupy odnajdywania aplikacji chmury](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [Przewodnik wdrażania programu System Center cloud App odnajdywania](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [Ustawienia funkcji cloud Discovery aplikacji rejestru dotyczące serwerów Proxy z portami niestandardowe](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [Wykaz cloud App Discovery agenta zmian](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [Usługa cloud App Discovery — często zadawane pytania](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)

