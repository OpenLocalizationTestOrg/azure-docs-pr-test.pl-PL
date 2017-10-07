---
title: "Użytkownik tooconfigure aaaHow Inicjowanie obsługi administracyjnej aplikacji galerii tooan usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Jak można szybko skonfigurować konto użytkownika sformatowanego alokowania i anulowania alokowania tooapplications już na liście hello galerii aplikacji usługi Azure AD"
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
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a>Jak użytkownika tooconfigure inicjowania obsługi usługi Azure AD tooan galerii aplikacji

*Inicjowanie obsługi konta użytkownika* polega hello tworzenie, aktualizowanie i/lub wyłączenie rekordów konta użytkowników w magazynie profil lokalny użytkownika aplikacji. Większość chmury i aplikacji SaaS przechowywać hello role użytkowników i uprawnienia własny magazyn profilu użytkownika lokalnego, a jest obecność takich rekordu użytkownika w lokalnym magazynie *wymagane* dla pojedynczego toowork logowania i dostępu.

W portalu Azure hello, hello **inicjowania obsługi administracyjnej** karta w okienku nawigacji po lewej stronie powitania aplikacji przedsiębiorstwa Wyświetla, jakie tryby inicjowania obsługi administracyjnej są obsługiwane dla danej aplikacji. Może to być jedną z dwóch wartości:

## <a name="configuring-an-application-for-manual-provisioning"></a>Konfigurowanie aplikacji do ręcznego inicjowania obsługi

*Ręczne* inicjowania obsługi administracyjnej oznacza, że należy utworzyć konta użytkownika ręcznie przy użyciu metody hello udostępniane przez danej aplikacji. Może to oznaczać logowania do portalu administracyjnego dla danej aplikacji i dodawanie użytkowników przy użyciu interfejsu użytkownika opartego na sieci web. Lub może być przekazywania arkusz kalkulacyjny zawierający szczegółów konta użytkownika, przy użyciu mechanizmu udostępniane przez tę aplikację. Zapoznaj się dokumentacją hello, pod warunkiem aplikacji hello lub skontaktuj się z pomocą hello aplikacji są dostępne mechanizmy wat toodetermine developer.

Jeśli ręczne jest tylko tryb hello wyświetlany dla danej aplikacji, oznacza to, że nie usługi Azure AD automatycznego inicjowania obsługi administracyjnej łącznik został utworzony dla aplikacji hello jeszcze. Lub oznacza to, że aplikacja hello nie nie obsługi hello użytkownika wymaganego interfejsu API zarządzania po którym toobuild automatycznego inicjowania obsługi administracyjnej łącznika.

Jeśli chcesz obsługę toorequest automatyczne Inicjowanie obsługi administracyjnej dla danej aplikacji, możesz też wypełnić żądania w <http://aka.ms/aadapprequest>.

## <a name="configuring-an-application-for-automatic-provisioning"></a>Konfigurowanie aplikacji do automatycznego inicjowania obsługi

*Automatyczne* oznacza, że usługi Azure AD, inicjowania obsługi administracyjnej łącznik został opracowany dla tej aplikacji. Aby uzyskać więcej informacji na temat hello Azure AD inicjowania obsługi administracyjnej usługi oraz sposób jej działania, zobacz [tooSaaS zautomatyzować Inicjowanie obsługi użytkowników i anulowania zastrzeżenia aplikacji za pomocą usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).

Aby uzyskać więcej informacji na temat sposobu tooprovision konkretnych użytkowników i grup tooan aplikacji, zobacz [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).

Witaj tooenable wymagane kroki rzeczywiste i skonfigurować automatyczne udostępnianie się różnić w zależności od aplikacji hello.

>[!NOTE]
>Należy zacząć od znajdowanie hello samouczek toosetting określonych ustawień się inicjowanie obsługi administracyjnej dla aplikacji, a po tooconfigure te kroki zarówno aplikacja hello, jak i usługi Azure AD toocreate hello połączenia inicjowania obsługi administracyjnej. 
>
>

Samouczki aplikacji można znaleźć w folderze [listy samouczki dotyczące tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

Tooconsider ważne podczas konfigurowania udostępniania można tooreview i skonfigurować mapowanie atrybutów hello i przepływów pracy, definiujące które przepływ właściwości użytkownika (lub grupy) z usługi Azure AD toohello aplikacji. Obejmuje to ustawienie hello "zgodnej właściwości", który można toouniquely używane zidentyfikować a użytkowników/grupy między hello dwa systemy są takie same. Aby uzyskać więcej informacji na ten proces ważne.

## <a name="next-steps"></a>Następne kroki
[Dostosowywanie użytkownika udostępniania mapowań atrybutów dla aplikacji SaaS w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

