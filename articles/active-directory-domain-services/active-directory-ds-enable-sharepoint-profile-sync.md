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
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="6d4af-103">Konfigurowanie synchronizacji profilu domeny zarządzanej toosupport programu SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="6d4af-103">Configure a managed domain toosupport profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="6d4af-104">Serwer programu SharePoint obejmuje usługi profilu użytkownika, który służy do synchronizacji profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6d4af-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="6d4af-105">tooset się hello usługi profilu użytkownika, odpowiednie uprawnienia muszą toobe przyznane domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6d4af-105">tooset up hello User Profile Service, appropriate permissions need toobe granted on an Active Directory domain.</span></span> <span data-ttu-id="6d4af-106">Aby uzyskać więcej informacji, zobacz [uprawnienia usług domenowych w usłudze Active Directory synchronizacji profilów w programie SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d4af-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="6d4af-107">W tym artykule opisano, jak można skonfigurować usługi domenowe Azure AD domen zarządzanych toodeploy hello synchronizacji profilu użytkownika z programem SharePoint Server usługę.</span><span class="sxs-lookup"><span data-stu-id="6d4af-107">This article explains how you can configure Azure AD Domain Services managed domains toodeploy hello SharePoint Server User Profile Sync service.</span></span>

## <a name="hello-aad-dc-service-accounts-group"></a><span data-ttu-id="6d4af-108">Grupa "Konta usługi kontrolera domeny usługi AAD" Hello</span><span class="sxs-lookup"><span data-stu-id="6d4af-108">hello 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="6d4af-109">Grupy zabezpieczeń o nazwie "**konta usługi kontrolera domeny usługi AAD**" znajduje się w jednostce organizacyjnej "Użytkowników" hello na domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="6d4af-109">A security group called '**AAD DC Service Accounts**' is available within hello 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="6d4af-110">Można wyświetlić tej grupy w hello **użytkownicy usługi Active Directory i komputery** przystawka programu MMC w domenie zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="6d4af-110">You can see this group in hello **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![Grupa zabezpieczeń konta usługi kontrolera domeny usługi AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="6d4af-112">Członkowie tej grupy zabezpieczeń są delegowanego hello następujące uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="6d4af-112">Members of this security group are delegated hello following privileges:</span></span>
- <span data-ttu-id="6d4af-113">uprawnienie "Replikować zmiany katalogu" Hello hello głównego elementu DSE z hello zarządzane domeny.</span><span class="sxs-lookup"><span data-stu-id="6d4af-113">hello 'Replicate Directory Changes' privilege on hello root DSE of hello managed domain.</span></span>
- <span data-ttu-id="6d4af-114">Witaj 'Replikować zmiany katalogu' uprawnień w kontekście nazewnictwa konfiguracji hello (cn = kontenera konfiguracji) hello zarządzane domeny.</span><span class="sxs-lookup"><span data-stu-id="6d4af-114">hello 'Replicate Directory Changes' privilege on hello Configuration naming context (cn=configuration container) of hello managed domain.</span></span>

<span data-ttu-id="6d4af-115">Ta grupa zabezpieczeń jest również członkiem grupy wbudowane hello **dostęp zgodny z systemami starszymi niż Windows 2000**.</span><span class="sxs-lookup"><span data-stu-id="6d4af-115">This security group is also a member of hello built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![Grupa zabezpieczeń konta usługi kontrolera domeny usługi AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a><span data-ttu-id="6d4af-117">Włącz toosupport Twojego domeny zarządzanej synchronizacja profilu użytkownika programu SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="6d4af-117">Enable your managed domain toosupport SharePoint Server user profile sync</span></span>
<span data-ttu-id="6d4af-118">Można dodać hello konto usługi używane przez toohello synchronizacji profilu użytkownika programu SharePoint **konta usługi kontrolera domeny usługi AAD** grupy.</span><span class="sxs-lookup"><span data-stu-id="6d4af-118">You can add hello service account used for SharePoint user profile synchronization toohello **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="6d4af-119">W związku z tym konto synchronizacji hello pobiera odpowiednie uprawnienia tooreplicate zmiany toohello katalogu.</span><span class="sxs-lookup"><span data-stu-id="6d4af-119">As a result, hello synchronization account gets adequate privileges tooreplicate changes toohello directory.</span></span> <span data-ttu-id="6d4af-120">Ten krok konfiguracji umożliwia toowork synchronizacji profilu użytkownika programu SharePoint Server poprawnie.</span><span class="sxs-lookup"><span data-stu-id="6d4af-120">This configuration step enables SharePoint Server user profile sync toowork correctly.</span></span>

![Konta usługi AAD kontrolera domeny — dodawanie członków](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Konta usługi AAD kontrolera domeny — dodawanie członków](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="6d4af-123">Powiązana zawartość</span><span class="sxs-lookup"><span data-stu-id="6d4af-123">Related Content</span></span>
* [<span data-ttu-id="6d4af-124">Dokumentacja techniczna - uprawnienia Grant usług domenowych Active Directory synchronizacji profilów w programie SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="6d4af-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
