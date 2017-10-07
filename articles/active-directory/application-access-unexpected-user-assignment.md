---
title: "tooapplications użytkowników tooAssign aaaHow | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak użytkownicy zostaną przypisane tooan aplikacji w Twojej dzierżawie"
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
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a>Jak tooassign tooapplications użytkowników

W tym artykule pomocy toounderstand jak użytkownicy zostaną przypisane tooan aplikacji w dzierżawie.

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a>Jak użytkownicy zostaną przypisane tooan aplikacji w usłudze Azure AD?

Dla tooaccess użytkownika aplikacji one należy przypisać tooit w określony sposób. Przypisanie może zostać wykonana przez administratora, delegat biznesowych lub czasami użytkownika hello samodzielnie. Poniżej opisano sposoby hello, które użytkownicy mogą zostać przypisani tooapplications:

1.  Administrator [przypisuje użytkownika](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello aplikacji bezpośrednio

2.  Administrator [przypisuje grupę](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) hello użytkownik jest członkiem toohello aplikacji, w tym:

  * Grupy, która była synchronizowana z lokalnymi

  * Grupy zabezpieczeń statycznych utworzone w chmurze hello

  * A [grupy zabezpieczeń dynamiczne](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) utworzone w chmurze hello

  * Grupy usługi Office 365 utworzone w chmurze hello

  * Witaj [wszyscy użytkownicy](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) grupy

3.  Administrator włączy [samoobsługi dostęp do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow tooadd użytkownika, przy użyciu aplikacji hello [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Dodaj aplikację** funkcji **bez zatwierdzenia biznesowa**

4.  Administrator włączy [samoobsługi dostęp do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow tooadd użytkownika, przy użyciu aplikacji hello [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Dodaj aplikację** funkcji, ale tylko w **i pobieraniu z zestawu wybranych osób zatwierdzających biznesowa**

5.  Administrator włączy [Samoobsługowe zarządzanie grupami](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin użytkownika grupy aplikacji przypisany zbyt**bez zatwierdzenia biznesowa**

6.  Administrator włączy [Samoobsługowe zarządzanie grupami](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin użytkownika grupę, której aplikacja jest przypisany do, ale tylko **o pobieraniu z zestawu wybranych osób zatwierdzających biznesowa**

7.  Administrator przypisuje tooa licencji użytkownika bezpośrednio do pierwszej strony aplikacji, tak samo, jak [Microsoft Office 365](http://products.office.com/)

8.  Przypisuje administratora grupy tooa licencji, która hello użytkownika jest członkiem tooa pierwszej aplikacji firm, takich jak [Microsoft Office 365](http://products.office.com/)

9.  [Administrator wyrazi na to zgody aplikacji tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe używane przez wszystkich użytkowników, a następnie użytkownik loguje się toohello aplikacji

10. Użytkownik [zgadza aplikacji tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) się po zarejestrowaniu się w aplikacji toohello

## <a name="next-steps"></a>Następne kroki
[Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory](active-directory-enable-sso-scenario.md)
