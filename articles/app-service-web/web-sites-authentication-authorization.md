---
title: "aaaAuthenticate z lokalnej usługi Active Directory w aplikacji Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o różnych opcjach hello aplikacji biznesowych — w usłudze Azure App Service tooauthenticate z lokalną usługą Active Directory"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: dde6b7e6-bf6a-4fa5-8390-3a18155d21bd
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: 65bf25aaa0447fbbea7c754db55842d57e70757e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a>Uwierzytelniania za pomocą lokalnej usługi Active Directory w aplikacji Azure
W tym artykule opisano sposób tooauthenticate z lokalnej usługi Active Directory (AD) w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md). Aplikację Azure znajduje się w chmurze hello, ale istnieją sposoby tooauthenticate lokalnych użytkowników usługi AD bezpieczne. 

## <a name="authenticate-through-azure-active-directory"></a>Uwierzytelnianie za pomocą usługi Azure Active Directory
Dzierżawy usługi Azure Active Directory może być directory synchronizowane z lokalnej usługi AD. Takie podejście umożliwia użytkownikom AD dostęp do aplikacji z hello internet i Uwierzytelnij się przy użyciu poświadczeń lokalnych. Ponadto usługi Azure App Service udostępnia [gotowe rozwiązanie dla tej metody](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Za pomocą kilku kliknięć przycisku można włączyć uwierzytelnianie z dzierżawą zsynchronizowany katalog dla aplikacji platformy Azure. Takie podejście charakteryzuje się hello następujące korzyści:

* Nie wymaga żadnych kod uwierzytelniania w aplikacji. Zezwolić czy usługi aplikacji hello uwierzytelniania i poświęcić czas na dostarczanie funkcji w aplikacji.
* [Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx) umożliwia dostęp do danych toodirectory z aplikacji Azure.
* Umożliwia logowanie Jednokrotne za[wszystkich aplikacji obsługiwanych przez usługę Azure Active Directory](/marketplace/active-directory/), w tym usługi Office 365, Dynamics CRM Online, Microsoft Intune i tysiące aplikacji w chmurze firmy Microsoft. 
* Azure Active Directory obsługuje kontroli dostępu opartej na rolach. Można używać wzorca hello [Authorize(Roles="X")] przy minimalnych zmianach tooyour kodu.

toosee toowrite aplikacji Azure — biznesowych, który jest uwierzytelniany w usłudze Azure Active Directory, zobacz temat [tworzenie aplikacji Azure — biznesowych przy użyciu uwierzytelniania usługi Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md).

## <a name="authenticate-through-an-on-premises-sts"></a>Uwierzytelnianie za pośrednictwem lokalnej usługi STS
Jeśli masz bezpiecznego tokenu usługi lokalnej (STS) jak Active Directory Federation Services (AD FS), można użyć uwierzytelniania toofederate dla aplikacji platformy Azure. Ta metoda jest najbardziej, gdy zasady firmy zabrania AD dane przechowywane na platformie Azure. Zwróć jednak uwagę hello następujące czynności:

* Topologia usługi STS musi być wdrożone w infrastrukturze lokalnej, działanie kosztów i zarządzania.
* Tylko Administratorzy usług AD FS można skonfigurować [jednostki uzależnionej strony zaufania oraz reguły oświadczeń](http://technet.microsoft.com/library/dd807108.aspx), które mogą ograniczyć opcje hello dewelopera. Na powitania drugiej strony, jest możliwe toomanage i dostosować [oświadczeń](http://technet.microsoft.com/library/ee913571.aspx) na podstawie określonych aplikacji.
* Dostęp do lokalnych tooon oddzielnym rozwiązaniu przez zaporę firmowej hello wymaga danymi usługi AD.

toosee toowrite — biznesowych aplikacji Azure, który przeprowadza uwierzytelnianie z lokalnej usługi STS, zobacz temat [tworzenie aplikacji Azure — biznesowych uwierzytelniania usług AD FS](web-sites-dotnet-lob-application-adfs.md).

