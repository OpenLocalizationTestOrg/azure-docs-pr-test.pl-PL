---
title: "Jak przypisać użytkowników do aplikacji | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak użytkownicy zostaną przypisane do aplikacji w Twojej dzierżawie"
services: active-directory
documentationcenter: 
author: ajamess
manager: mtillman
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 6681131f24dd36ccc5881d50f3efdf9806b15c58
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="how-to-assign-users-to-applications"></a>Jak przypisać użytkowników do aplikacji

Ten artykuł ułatwia zrozumienie, jak użytkownicy zostaną przypisane do aplikacji w dzierżawie.

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a>Jak użytkownicy zostaną przypisane do aplikacji w usłudze Azure AD?

Aby użytkownik mógł uzyskać dostęp do aplikacji ich należy przypisać do niej w określony sposób. Przypisanie może zostać wykonana przez administratora, delegata biznesowych lub czasami użytkownik samodzielnie. Poniżej opisano sposoby, które użytkownicy mogą zostać przypisani do aplikacji:

1.  Administrator [przypisuje użytkownika](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) bezpośrednio w aplikacji

2.  Administrator [przypisuje grupę](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) czy użytkownik jest członkiem do aplikacji, w tym:

  * Grupy, która była synchronizowana z lokalnymi

  * Grupy zabezpieczeń statycznych utworzone w chmurze

  * A [grupy zabezpieczeń dynamiczne](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) utworzone w chmurze

  * Grupy usługi Office 365 utworzone w chmurze

  * [Wszyscy użytkownicy](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) grupy

3.  Administrator włączy [samoobsługi dostęp do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) Aby zezwolić użytkownikowi na dodawanie aplikacji przy użyciu [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Dodaj aplikację** funkcji **bez zatwierdzenia biznesowa**

4.  Administrator włączy [samoobsługi dostęp do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) Aby zezwolić użytkownikowi na dodawanie aplikacji przy użyciu [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Dodaj aplikację** funkcji, ale tylko w**i pobieraniu z zestawu wybranych osób zatwierdzających biznesowa**

5.  Administrator włączy [Samoobsługowe zarządzanie grupami](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) zezwolić użytkownikowi do dołączenia do grupy aplikacji przypisany do **bez zatwierdzenia biznesowa**

6.  Administrator włączy [Samoobsługowe zarządzanie grupami](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) zezwolić użytkownikowi do dołączenia do grupy, która aplikacja jest przypisany do, ale tylko **o pobieraniu z zestawu wybranych osób zatwierdzających biznesowa**

7.  Administrator powoduje przypisanie licencji użytkownika bezpośrednio do pierwszej aplikacji firm, takie jak [Microsoft Office 365](http://products.office.com/)

8.  Administrator przypisuje licencję do grupy czy użytkownik jest członkiem do pierwszej strony aplikacji, tak samo, jak [Microsoft Office 365](http://products.office.com/)

9.  [Administratora zgadza się na aplikacji](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) mają być używane przez wszystkich użytkowników, a następnie użytkownik loguje się do aplikacji

10. Użytkownik [zgadza się na aplikacji](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) się logując się do aplikacji

## <a name="next-steps"></a>Następne kroki
[Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory](active-directory-enable-sso-scenario.md)
