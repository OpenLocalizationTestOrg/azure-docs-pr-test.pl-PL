---
title: "Azure Active Directory Domain Services: Włączanie obsługi usługi profilu użytkownika programu SharePoint | Dokumentacja firmy Microsoft"
description: "Konfigurowanie domen zarządzanych usług domenowych Azure Active Directory w celu obsługi synchronizacji profilu programu SharePoint Server"
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
ms.openlocfilehash: c3c923b5c9cd652f0c5b0ec98c1cda740f180122
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-managed-domain-to-support-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="515ae-103">Konfigurowanie domeny zarządzanej w celu obsługi synchronizacji profilu programu SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="515ae-103">Configure a managed domain to support profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="515ae-104">Serwer programu SharePoint obejmuje usługi profilu użytkownika, który służy do synchronizacji profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="515ae-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="515ae-105">Aby skonfigurować usługi profilu użytkownika, odpowiednie uprawnienia muszą być przyznane domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="515ae-105">To set up the User Profile Service, appropriate permissions need to be granted on an Active Directory domain.</span></span> <span data-ttu-id="515ae-106">Aby uzyskać więcej informacji, zobacz [uprawnienia usług domenowych w usłudze Active Directory synchronizacji profilów w programie SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="515ae-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="515ae-107">W tym artykule opisano, jak można skonfigurować usługi domenowe Azure AD domen zarządzanych w celu wdrożenia usługi synchronizacji profilu użytkownika z programem SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="515ae-107">This article explains how you can configure Azure AD Domain Services managed domains to deploy the SharePoint Server User Profile Sync service.</span></span>

## <a name="the-aad-dc-service-accounts-group"></a><span data-ttu-id="515ae-108">Grupa "Konta usługi kontrolera domeny usługi AAD"</span><span class="sxs-lookup"><span data-stu-id="515ae-108">The 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="515ae-109">Grupy zabezpieczeń o nazwie "**konta usługi kontrolera domeny usługi AAD**" znajduje się w jednostce organizacyjnej 'Użytkownicy' domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="515ae-109">A security group called '**AAD DC Service Accounts**' is available within the 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="515ae-110">Można wyświetlić tej grupy w **użytkownicy usługi Active Directory i komputery** przystawka programu MMC w domenie zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="515ae-110">You can see this group in the **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![Grupa zabezpieczeń konta usługi kontrolera domeny usługi AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="515ae-112">Delegowane są członkami tej grupy zabezpieczeń następujące uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="515ae-112">Members of this security group are delegated the following privileges:</span></span>
- <span data-ttu-id="515ae-113">Uprawnienie "Replikować zmiany katalogu" na komputerze głównego elementu DSE domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="515ae-113">The 'Replicate Directory Changes' privilege on the root DSE of the managed domain.</span></span>
- <span data-ttu-id="515ae-114">Uprawnienie 'Replikować zmiany katalogu' w kontekście nazewnictwa konfiguracji (cn = kontenera konfiguracji) do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="515ae-114">The 'Replicate Directory Changes' privilege on the Configuration naming context (cn=configuration container) of the managed domain.</span></span>

<span data-ttu-id="515ae-115">Ta grupa zabezpieczeń jest również członkiem grupy wbudowane **dostęp zgodny z systemami starszymi niż Windows 2000**.</span><span class="sxs-lookup"><span data-stu-id="515ae-115">This security group is also a member of the built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![Grupa zabezpieczeń konta usługi kontrolera domeny usługi AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-to-support-sharepoint-server-user-profile-sync"></a><span data-ttu-id="515ae-117">Włącz domeny zarządzanej do obsługi synchronizacji profilu użytkownika programu SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="515ae-117">Enable your managed domain to support SharePoint Server user profile sync</span></span>
<span data-ttu-id="515ae-118">Można dodać konto usługi używane do synchronizacji profilu użytkownika programu SharePoint do **konta usługi kontrolera domeny usługi AAD** grupy.</span><span class="sxs-lookup"><span data-stu-id="515ae-118">You can add the service account used for SharePoint user profile synchronization to the **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="515ae-119">W związku z tym konta synchronizacji pobiera odpowiednie uprawnienia, aby replikować zmiany do katalogu.</span><span class="sxs-lookup"><span data-stu-id="515ae-119">As a result, the synchronization account gets adequate privileges to replicate changes to the directory.</span></span> <span data-ttu-id="515ae-120">Ten krok konfiguracji powoduje włączenie synchronizacji profilu użytkownika programu SharePoint Server działała prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="515ae-120">This configuration step enables SharePoint Server user profile sync to work correctly.</span></span>

![Konta usługi AAD kontrolera domeny — dodawanie członków](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Konta usługi AAD kontrolera domeny — dodawanie członków](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="515ae-123">Powiązana zawartość</span><span class="sxs-lookup"><span data-stu-id="515ae-123">Related Content</span></span>
* [<span data-ttu-id="515ae-124">Dokumentacja techniczna - uprawnienia Grant usług domenowych Active Directory synchronizacji profilów w programie SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="515ae-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
