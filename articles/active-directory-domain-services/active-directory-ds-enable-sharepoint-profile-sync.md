---
title: "Azure Active Directory Domain Services: Włączanie obsługi usługi profilu użytkownika programu SharePoint | Dokumentacja firmy Microsoft"
description: "Konfigurowanie synchronizacji profilu toosupport domen zarządzanych usług domenowych Azure Active Directory dla programu SharePoint Server"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a>Konfigurowanie synchronizacji profilu domeny zarządzanej toosupport programu SharePoint Server
Serwer programu SharePoint obejmuje usługi profilu użytkownika, który służy do synchronizacji profilu użytkownika. tooset się hello usługi profilu użytkownika, odpowiednie uprawnienia muszą toobe przyznane domeny usługi Active Directory. Aby uzyskać więcej informacji, zobacz [uprawnienia usług domenowych w usłudze Active Directory synchronizacji profilów w programie SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).

W tym artykule opisano, jak można skonfigurować usługi domenowe Azure AD domen zarządzanych toodeploy hello synchronizacji profilu użytkownika z programem SharePoint Server usługę.

## <a name="hello-aad-dc-service-accounts-group"></a>Grupa "Konta usługi kontrolera domeny usługi AAD" Hello
Grupy zabezpieczeń o nazwie "**konta usługi kontrolera domeny usługi AAD**" znajduje się w jednostce organizacyjnej "Użytkowników" hello na domeny zarządzanej. Można wyświetlić tej grupy w hello **użytkownicy usługi Active Directory i komputery** przystawka programu MMC w domenie zarządzanej.

![Grupa zabezpieczeń konta usługi kontrolera domeny usługi AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

Członkowie tej grupy zabezpieczeń są delegowanego hello następujące uprawnienia:
- uprawnienie "Replikować zmiany katalogu" Hello hello głównego elementu DSE z hello zarządzane domeny.
- Witaj 'Replikować zmiany katalogu' uprawnień w kontekście nazewnictwa konfiguracji hello (cn = kontenera konfiguracji) hello zarządzane domeny.

Ta grupa zabezpieczeń jest również członkiem grupy wbudowane hello **dostęp zgodny z systemami starszymi niż Windows 2000**.

![Grupa zabezpieczeń konta usługi kontrolera domeny usługi AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a>Włącz toosupport Twojego domeny zarządzanej synchronizacja profilu użytkownika programu SharePoint Server
Można dodać hello konto usługi używane przez toohello synchronizacji profilu użytkownika programu SharePoint **konta usługi kontrolera domeny usługi AAD** grupy. W związku z tym konto synchronizacji hello pobiera odpowiednie uprawnienia tooreplicate zmiany toohello katalogu. Ten krok konfiguracji umożliwia toowork synchronizacji profilu użytkownika programu SharePoint Server poprawnie.

![Konta usługi AAD kontrolera domeny — dodawanie członków](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Konta usługi AAD kontrolera domeny — dodawanie członków](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a>Powiązana zawartość
* [Dokumentacja techniczna - uprawnienia Grant usług domenowych Active Directory synchronizacji profilów w programie SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx)
