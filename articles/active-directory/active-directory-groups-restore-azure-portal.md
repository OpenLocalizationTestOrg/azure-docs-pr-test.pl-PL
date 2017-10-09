---
title: "grupy aaaRestore usunięto usługi Office 365 w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toorestore usuniętej grupie, wyświetlanie dostępnych grup i permamnently usunąć grupę w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="0d880-103">Przywracanie usuniętej grupy usługi Office 365 w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d880-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="0d880-104">Podczas usuwania grupy usługi Office 365 w hello Azure Active Directory (Azure AD), hello usunięta grupa jest zachowane, ale nie są widoczne przez 30 dni od daty usunięcia hello.</span><span class="sxs-lookup"><span data-stu-id="0d880-104">When you delete an Office 365 group in hello Azure Active Directory (Azure AD), hello deleted group is retained but not visible for 30 days from hello deletion date.</span></span> <span data-ttu-id="0d880-105">Jest tak, aby grupa hello i jego zawartość można przywrócić w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="0d880-105">This is so that hello group and its contents can be restored if needed.</span></span> <span data-ttu-id="0d880-106">Ta funkcja jest ograniczone wyłącznie tooOffice 365 grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d880-106">This functionality is restricted exclusively tooOffice 365 groups in Azure AD.</span></span> <span data-ttu-id="0d880-107">Nie jest dostępna dla grup zabezpieczeń i grup dystrybucyjnych.</span><span class="sxs-lookup"><span data-stu-id="0d880-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="0d880-108">Nie używaj `Remove-MsolGroup` ponieważ Przeczyszcza grupy hello trwałe.</span><span class="sxs-lookup"><span data-stu-id="0d880-108">Don't use `Remove-MsolGroup` because it purges hello group permanently.</span></span> <span data-ttu-id="0d880-109">Zawsze używaj `Remove-AzureADMSGroup` grupy toodelete usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="0d880-109">Always use `Remove-AzureADMSGroup` toodelete an O365 group.</span></span> 

<span data-ttu-id="0d880-110">wymagane uprawnienia Hello toorestore grupa może zawierać żadnego z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="0d880-110">hello permissions required toorestore a group can be any of hello following:</span></span>

<span data-ttu-id="0d880-111">Rola</span><span class="sxs-lookup"><span data-stu-id="0d880-111">Role</span></span>  | <span data-ttu-id="0d880-112">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="0d880-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="0d880-113">Administrator firmy, pomocy partnera Tier2 i Administratorzy usługi InTune</span><span class="sxs-lookup"><span data-stu-id="0d880-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="0d880-114">Można przywrócić wszystkie usunięte grupy usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="0d880-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="0d880-115">Administrator konta użytkownika i Tier1 partnera pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="0d880-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="0d880-116">Można przywrócić wszystkie usuniętej grupy usługi Office 365, z wyjątkiem tych toohello przypisanej roli Administrator firmy</span><span class="sxs-lookup"><span data-stu-id="0d880-116">Can restore any deleted Office 365 group except those assigned toohello Company Administrator role</span></span> 
<span data-ttu-id="0d880-117">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="0d880-117">User</span></span> | <span data-ttu-id="0d880-118">Można przywrócić wszystkie usuniętej grupy usługi Office 365, które są jego własnością</span><span class="sxs-lookup"><span data-stu-id="0d880-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a><span data-ttu-id="0d880-119">Widok hello usunięte grup usługi Office 365, które są dostępne toorestore</span><span class="sxs-lookup"><span data-stu-id="0d880-119">View hello deleted Office 365 groups that are available toorestore</span></span>
<span data-ttu-id="0d880-120">Hello następującego polecenia cmdlet mogą być używane tooview hello usunięte grup tooverify, który hello jedną lub te, które interesują Cię nie jeszcze zostały trwale usunięte.</span><span class="sxs-lookup"><span data-stu-id="0d880-120">hello following cmdlets can be used tooview hello deleted groups tooverify that hello one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="0d880-121">Te polecenia cmdlet są częścią hello [modułu Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="0d880-121">These cmdlets are part of hello [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="0d880-122">Więcej informacji na temat tego modułu można znaleźć w hello [Azure Active Directory programu PowerShell w wersji 2](/powershell/azure/install-adv2?view=azureadps-2.0) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0d880-122">More information about this module can be found in hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="0d880-123">Uruchom następujące polecenia cmdlet toodisplay usunięte grup usługi Office 365 w dzierżawie, które są nadal dostępne toorestore hello.</span><span class="sxs-lookup"><span data-stu-id="0d880-123">Run hello following cmdlet toodisplay all deleted Office 365 groups in your tenant that are still available toorestore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="0d880-124">Jeśli znasz objectID hello określonej grupy (i pobrać go ze strony hello polecenie cmdlet w kroku 1), uruchom hello tooverify polecenia cmdlet, które hello określonej grupy usunięte po nie jeszcze trwale usunięto.</span><span class="sxs-lookup"><span data-stu-id="0d880-124">Alternately, if you know hello objectID of a specific group (and you can get it from hello cmdlet in step 1), run hello following cmdlet tooverify that hello specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a><span data-ttu-id="0d880-125">Jak toorestore Twojego usuniętej grupy usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="0d880-125">How toorestore your deleted Office 365 group</span></span>
<span data-ttu-id="0d880-126">Po upewnieniu się, że grupa ta hello jest nadal dostępny toorestore hello przywracania usunął grupę z jednym hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="0d880-126">Once you have verified that hello group is still available toorestore, restore hello deleted group with one of hello following steps.</span></span> <span data-ttu-id="0d880-127">Jeśli grupa hello zawiera dokumenty, SP witryn lub inne obiekty trwałe, grupy i jego zawartość może potrwać nawet too24 godziny toofully przywracania.</span><span class="sxs-lookup"><span data-stu-id="0d880-127">If hello group contains documents, SP sites, or other persistent objects, it might take up too24 hours toofully restore a group and its contents.</span></span>

1.  <span data-ttu-id="0d880-128">Uruchom hello następujące polecenia cmdlet toorestore hello grupy i jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="0d880-128">Run hello following cmdlet toorestore hello group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="0d880-129">Alternatywnie hello następującego polecenia cmdlet można uruchomić toopermanently Usuń hello usunąć grupę.</span><span class="sxs-lookup"><span data-stu-id="0d880-129">Alternatively, hello following cmdlet can be run toopermanently remove hello deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="0d880-130">Skąd wiadomo, to pracy?</span><span class="sxs-lookup"><span data-stu-id="0d880-130">How do you know this worked?</span></span>
<span data-ttu-id="0d880-131">tooverify zostały pomyślnie przywrócił grupy usługi Office 365, uruchom hello `Get-AzureADGroup –ObjectId <objectId>` polecenia cmdlet toodisplay informacji o grupie hello.</span><span class="sxs-lookup"><span data-stu-id="0d880-131">tooverify that you’ve successfully restored an Office 365 group, run hello `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay information about hello group.</span></span> <span data-ttu-id="0d880-132">Po przywróceniu hello jest ukończone żądania:</span><span class="sxs-lookup"><span data-stu-id="0d880-132">After hello restore request is completed:</span></span>
- <span data-ttu-id="0d880-133">grupy Hello pojawią się w pasku nawigacyjnym po lewej stronie powitania na serwerze Exchange</span><span class="sxs-lookup"><span data-stu-id="0d880-133">hello group will appear in hello Left nav bar on Exchange</span></span>
- <span data-ttu-id="0d880-134">Planowanie Hello hello grupy będą wyświetlane w planowania</span><span class="sxs-lookup"><span data-stu-id="0d880-134">hello plan for hello group will appear in Planner</span></span>
- <span data-ttu-id="0d880-135">Witryny programu Sharepoint i wszystkie ich zawartość będzie dostępna</span><span class="sxs-lookup"><span data-stu-id="0d880-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="0d880-136">Hello grupy jest możliwy za pomocą dowolnego hello punktów końcowych z programu Exchange i innych obciążeń usługi Office 365, które obsługują grup usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="0d880-136">hello group can be accessed from any of hello Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="0d880-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0d880-137">Next steps</span></span>
<span data-ttu-id="0d880-138">Te artykuły zawierają dodatkowe informacje o grupach usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0d880-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="0d880-139">Zobacz istniejących grup</span><span class="sxs-lookup"><span data-stu-id="0d880-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="0d880-140">Zarządzanie ustawieniami grupy</span><span class="sxs-lookup"><span data-stu-id="0d880-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="0d880-141">Elementy członkowskie grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="0d880-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="0d880-142">Zarządzanie członkostwami grup</span><span class="sxs-lookup"><span data-stu-id="0d880-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="0d880-143">Dynamiczne reguły dla użytkowników w grupie zarządzania</span><span class="sxs-lookup"><span data-stu-id="0d880-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
