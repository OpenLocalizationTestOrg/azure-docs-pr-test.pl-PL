---
title: "Program Azure AD Connect w usłudze Microsoft Cloud w Niemczech"
description: "Program Azure AD Connect umożliwia integrowanie katalogów lokalnych z usługą Azure Active Directory. Dzięki temu można posługiwać się wspólną tożsamością dla usługi Office 365, platformy Azure i aplikacji SaaS zintegrowanych z usługą Azure AD."
keywords: "wprowadzenie do programu Azure AD Connect, omówienie programu Azure AD Connect, co to jest program Azure AD Connect, instalowanie usługi Active Directory, Niemcy, Black Forest"
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
ms.openlocfilehash: 4c55b116c0dc080ae316caca873a7b693caa793b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a>Program Azure AD Connect w usłudze Microsoft Cloud w Niemczech — publiczna wersja zapoznawcza
## <a name="introduction"></a>Wprowadzenie
Azure AD Connect zapewnia synchronizację między lokalną usługą Active Directory a usługą Azure Active Directory.
Obecnie wiele scenariuszy w usłudze [Microsoft Cloud w Niemczech](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) musi być wykonywanych przez operatora. Korzystając z usługi Microsoft Cloud w Niemczech, należy pamiętać o następujących kwestiach:

* Następujące adresy URL muszą zostać otwarte na serwerze proxy, aby synchronizacja zakończyła się pomyślnie:
  
  * *.microsoftonline.de
  * *.windows.net
  * * Listy odwołania certyfikatów
* Po zalogowaniu do katalogu usługi Azure AD należy używać konta w domenie onmicrosoft.de.
* Następujące funkcje nie są dostępne:
  * Azure AD Connect Health
  * Automatyczne aktualizacje
 
## <a name="download"></a>Do pobrania
Usługę Azure AD Connect można pobrać z bloku programu Azure AD Connect w portalu.  Znajdź blok programu Azure AD Connect, korzystając z poniższych instrukcji.

### <a name="the-azure-ad-connect-blade"></a>Blok programu Azure AD Connect
Po zalogowaniu się do witryny Azure Portal wykonaj następujące czynności:

1. Przejdź do pozycji Przeglądaj
2. Wybierz pozycję Azure Active Directory
3. Następnie wybierz pozycję Azure AD Connect

Powinien zostać wyświetlony następujący ekran:

![Blok programu Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

W poniższej tabeli opisano funkcje wyświetlane w bloku.

| Tytuł | Opis |
| --- | --- |
| STAN SYNCHRONIZACJI |Informuje, czy synchronizacja jest włączona, czy wyłączona. |
| OSTATNIA SYNCHRONIZACJA |Godzina zakończenia ostatniej pomyślnej synchronizacji. |
| DOMENY FEDERACYJNE |Wyświetla liczbę obecnie skonfigurowanych domen federacyjnych. |

## <a name="installation"></a>Instalacja
Możesz zainstalować program Azure AD Connect, korzystając z dokumentacji znajdującej się [tutaj](active-directory-aadconnect.md#install-azure-ad-connect).

## <a name="advanced-features-and-additional-information"></a>Funkcje zaawansowane i dodatkowe informacje
Aby uzyskać dodatkowe informacje i wskazówki dotyczące ustawień niestandardowych lub zaawansowanych konfiguracji, na początek zapoznaj się z artykułem [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).  Ta strona zawiera informacje i linki do dodatkowych wskazówek.

