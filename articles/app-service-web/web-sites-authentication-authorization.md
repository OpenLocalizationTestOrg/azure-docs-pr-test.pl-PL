---
title: "Uwierzytelniania za pomocą lokalnej usługi Active Directory w aplikacji Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o różnych opcji dla aplikacji biznesowych — w usłudze aplikacji Azure do uwierzytelniania za pomocą lokalnej usługi Active Directory"
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
ms.openlocfilehash: a68bcd7040498515a6e35a87ee6e6940a84506d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a>Uwierzytelniania za pomocą lokalnej usługi Active Directory w aplikacji Azure
W tym artykule przedstawiono sposób uwierzytelniania za pomocą lokalnej usługi Active Directory (AD) w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md). Aplikacja Azure jest hostowana w chmurze, ale istnieją sposoby uwierzytelniania lokalnych użytkowników usługi AD bezpiecznie. 

## <a name="authenticate-through-azure-active-directory"></a>Uwierzytelnianie za pomocą usługi Azure Active Directory
Dzierżawy usługi Azure Active Directory może być directory synchronizowane z lokalnej usługi AD. Takie podejście umożliwia użytkownikom AD dostęp do aplikacji z Internetu i uwierzytelniania przy użyciu poświadczeń lokalnych. Ponadto usługi Azure App Service udostępnia [gotowe rozwiązanie dla tej metody](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Za pomocą kilku kliknięć przycisku można włączyć uwierzytelnianie z dzierżawą zsynchronizowany katalog dla aplikacji platformy Azure. Takie podejście ma następujące zalety:

* Nie wymaga żadnych kod uwierzytelniania w aplikacji. Zezwala aplikacji usługi, czy uwierzytelnianie i poświęcić czas na dostarczanie funkcji w aplikacji.
* [Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx) umożliwia dostęp do katalogu danych z aplikacji Azure.
* Umożliwia logowanie Jednokrotne [wszystkich aplikacji obsługiwanych przez usługę Azure Active Directory](/marketplace/active-directory/), w tym usługi Office 365, Dynamics CRM Online, Microsoft Intune i tysiące aplikacji w chmurze firmy Microsoft. 
* Azure Active Directory obsługuje kontroli dostępu opartej na rolach. Korzystając wzorca [Authorize(Roles="X")] przy minimalnych zmianach w kodzie.

Aby zobaczyć, jak napisać aplikację Azure-biznesowych, która jest uwierzytelniany w usłudze Azure Active Directory, zobacz [tworzenie aplikacji Azure — biznesowych przy użyciu uwierzytelniania usługi Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md).

## <a name="authenticate-through-an-on-premises-sts"></a>Uwierzytelnianie za pośrednictwem lokalnej usługi STS
Jeśli masz bezpiecznego tokenu usługi lokalnej (STS) jak Active Directory Federation Services (AD FS), można go używać, aby Federację uwierzytelniania dla aplikacji platformy Azure. Ta metoda jest najbardziej, gdy zasady firmy zabrania AD dane przechowywane na platformie Azure. Jednak należy uwzględnić następujące informacje:

* Topologia usługi STS musi być wdrożone w infrastrukturze lokalnej, działanie kosztów i zarządzania.
* Tylko Administratorzy usług AD FS można skonfigurować [jednostki uzależnionej strony zaufania oraz reguły oświadczeń](http://technet.microsoft.com/library/dd807108.aspx), które mogą ograniczyć opcje dewelopera. Z drugiej strony, istnieje możliwość zarządzania i dostosować [oświadczeń](http://technet.microsoft.com/library/ee913571.aspx) na podstawie określonych aplikacji.
* Dostęp do lokalnych danych AD wymaga oddzielnym rozwiązaniu przez zaporę firmowej.

Aby zobaczyć, jak napisać biznesowych z aplikacji Azure, który przeprowadza uwierzytelnianie z lokalnej usługi STS, zobacz [tworzenie aplikacji Azure — biznesowych uwierzytelniania usług AD FS](web-sites-dotnet-lob-application-adfs.md).

