---
title: aaaAzure AD Connect w Niemczech Microsoft Cloud
description: "Program Azure AD Connect umożliwia integrowanie katalogów lokalnych z usługą Azure Active Directory. Dzięki temu tooprovide wspólną tożsamością dla usługi Office 365, Azure i aplikacji SaaS zintegrowanych z usługą Azure AD."
keywords: "wprowadzenie tooAzure AD Connect, omówienie usługi Azure AD Connect, co to jest usługa Azure AD Connect, instalowania usługi active directory, Niemczech, czarnym lesie"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a>Program Azure AD Connect w usłudze Microsoft Cloud w Niemczech — publiczna wersja zapoznawcza
## <a name="introduction"></a>Wprowadzenie
Azure AD Connect zapewnia synchronizację między lokalną usługą Active Directory a usługą Azure Active Directory.
Obecnie wiele scenariuszy hello w [Niemcy Microsoft Cloud](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) musi zostać wykonane przez operatora hello. Korzystając z Microsoft Cloud Niemczech, należy pamiętać o następujących hello:

* Witaj następujące adresy URL muszą być otwarte na serwerze proxy dla synchronizacji toooccur pomyślnie:
  
  * *.microsoftonline.de
  * *.windows.net
  * * Listy odwołania certyfikatów
* Po zarejestrowaniu się w katalogu usługi Azure AD tooyour, należy użyć konta w domenie onmicrosoft.de hello.
* Witaj, następujące funkcje są niedostępne:
  * Azure AD Connect Health
  * Automatyczne aktualizacje
 
## <a name="download"></a>Do pobrania
Azure AD Connect można pobrać z bloku Azure AD Connect hello hello portalu.  Użyj instrukcji hello poniżej toolocate hello Azure AD Connect bloku.

### <a name="hello-azure-ad-connect-blade"></a>Hello Azure AD Connect bloku
Po zalogowaniu toohello portalu Azure hello następujące:

1. Przejdź tooBrowse
2. Wybierz pozycję Azure Active Directory
3. Następnie wybierz pozycję Azure AD Connect

Powinny pojawić się następujące hello:

![Blok programu Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

Witaj poniższej tabeli opisano funkcje hello wyświetlane w bloku hello.

| Tytuł | Opis |
| --- | --- |
| STAN SYNCHRONIZACJI |Informuje, czy synchronizacja jest włączona, czy wyłączona. |
| OSTATNIA SYNCHRONIZACJA |Witaj czas ostatniej pomyślnej synchronizacji ukończone. |
| DOMENY FEDERACYJNE |Pokazuje liczbę hello Sfederowanych domen obecnie skonfigurowane. |

## <a name="installation"></a>Instalacja
tooinstall Azure AD Connect, korzystając z dokumentacji hello [tutaj](active-directory-aadconnect.md#install-azure-ad-connect).

## <a name="advanced-features-and-additional-information"></a>Funkcje zaawansowane i dodatkowe informacje
Aby uzyskać dodatkowe informacje i wskazówki dotyczące ustawień niestandardowych lub zaawansowanych konfiguracji, na początek zapoznaj się z artykułem [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).  Ta strona zawiera informacje i linki tooadditional wskazówki.

