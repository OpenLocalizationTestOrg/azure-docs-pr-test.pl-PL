---
title: "Przywracanie usuniętej grupy usługi Office 365 w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Przywracanie usuniętej grupie, wyświetlanie dostępnych grup i usuwanie permamnently grupy w usłudze Azure Active Directory"
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
ms.openlocfilehash: 32d36ae96797a59bb47bf782ab038f21f231f046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="8e307-103">Przywracanie usuniętej grupy usługi Office 365 w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e307-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="8e307-104">Podczas usuwania grupy usługi Office 365 w usłudze Azure Active Directory (Azure AD), usuwana grupa jest zachowane, ale nie są widoczne przez 30 dni od daty usunięcia.</span><span class="sxs-lookup"><span data-stu-id="8e307-104">When you delete an Office 365 group in the Azure Active Directory (Azure AD), the deleted group is retained but not visible for 30 days from the deletion date.</span></span> <span data-ttu-id="8e307-105">Jest tak, aby nazwa grupy i jego zawartość można przywrócić w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="8e307-105">This is so that the group and its contents can be restored if needed.</span></span> <span data-ttu-id="8e307-106">Ta funkcja jest ograniczone wyłącznie do grup usługi Office 365 w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e307-106">This functionality is restricted exclusively to Office 365 groups in Azure AD.</span></span> <span data-ttu-id="8e307-107">Nie jest dostępna dla grup zabezpieczeń i grup dystrybucyjnych.</span><span class="sxs-lookup"><span data-stu-id="8e307-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="8e307-108">Nie używaj `Remove-MsolGroup` ponieważ Przeczyszcza grupy trwałe.</span><span class="sxs-lookup"><span data-stu-id="8e307-108">Don't use `Remove-MsolGroup` because it purges the group permanently.</span></span> <span data-ttu-id="8e307-109">Zawsze używaj `Remove-AzureADMSGroup` można usunąć grupy usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="8e307-109">Always use `Remove-AzureADMSGroup` to delete an O365 group.</span></span> 

<span data-ttu-id="8e307-110">Uprawnień wymaganych do przywrócenia grupy może być jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="8e307-110">The permissions required to restore a group can be any of the following:</span></span>

<span data-ttu-id="8e307-111">Rola</span><span class="sxs-lookup"><span data-stu-id="8e307-111">Role</span></span>  | <span data-ttu-id="8e307-112">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="8e307-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="8e307-113">Administrator firmy, pomocy partnera Tier2 i Administratorzy usługi InTune</span><span class="sxs-lookup"><span data-stu-id="8e307-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="8e307-114">Można przywrócić wszystkie usunięte grupy usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="8e307-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="8e307-115">Administrator konta użytkownika i Tier1 partnera pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="8e307-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="8e307-116">Można przywrócić wszystkie usunięte grupy usługi Office 365 z wyjątkiem tych, przypisane do roli administratora firmy</span><span class="sxs-lookup"><span data-stu-id="8e307-116">Can restore any deleted Office 365 group except those assigned to the Company Administrator role</span></span> 
<span data-ttu-id="8e307-117">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="8e307-117">User</span></span> | <span data-ttu-id="8e307-118">Można przywrócić wszystkie usuniętej grupy usługi Office 365, które są jego własnością</span><span class="sxs-lookup"><span data-stu-id="8e307-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-the-deleted-office-365-groups-that-are-available-to-restore"></a><span data-ttu-id="8e307-119">Wyświetlanie usuniętych grup usługi Office 365, które są dostępne do przywrócenia</span><span class="sxs-lookup"><span data-stu-id="8e307-119">View the deleted Office 365 groups that are available to restore</span></span>
<span data-ttu-id="8e307-120">Następujące polecenia cmdlet umożliwia wyświetlanie usuniętych grup, aby sprawdzić, czy co najmniej te, które są zainteresowani nie jeszcze zostały trwale usunięte.</span><span class="sxs-lookup"><span data-stu-id="8e307-120">The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="8e307-121">Te polecenia cmdlet są częścią [modułu Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="8e307-121">These cmdlets are part of the [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="8e307-122">Więcej informacji na temat tego modułu można znaleźć w [Azure Active Directory programu PowerShell w wersji 2](/powershell/azure/install-adv2?view=azureadps-2.0) artykułu.</span><span class="sxs-lookup"><span data-stu-id="8e307-122">More information about this module can be found in the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="8e307-123">Uruchom następujące polecenie cmdlet, aby wyświetlić wszystkich usuniętych grup usługi Office 365 w dzierżawie, które są nadal dostępne do przywrócenia.</span><span class="sxs-lookup"><span data-stu-id="8e307-123">Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="8e307-124">Jeśli znasz identyfikator obiektu określonej grupy (, możesz pobrać go z polecenia cmdlet w kroku 1) uruchom następujące polecenie cmdlet, aby sprawdzić, czy określone usuniętej grupy nie jeszcze trwale usunięto.</span><span class="sxs-lookup"><span data-stu-id="8e307-124">Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-to-restore-your-deleted-office-365-group"></a><span data-ttu-id="8e307-125">Przywracanie usuniętych grupy usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="8e307-125">How to restore your deleted Office 365 group</span></span>
<span data-ttu-id="8e307-126">Po upewnieniu się, że grupa jest nadal dostępne do przywrócenia, przywracanie usuniętej grupy z jedną z następujących czynności.</span><span class="sxs-lookup"><span data-stu-id="8e307-126">Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps.</span></span> <span data-ttu-id="8e307-127">Jeśli grupa zawiera dokumenty, SP witryn lub inne obiekty trwałe, może potrwać do 24 godzin pełni przywrócić grupy i jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="8e307-127">If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.</span></span>

1.  <span data-ttu-id="8e307-128">Uruchom następujące polecenie cmdlet, aby przywrócić grupy i jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="8e307-128">Run the following cmdlet to restore the group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="8e307-129">Można też uruchomić następujące polecenie cmdlet na stałe usunąć do usuniętej grupy.</span><span class="sxs-lookup"><span data-stu-id="8e307-129">Alternatively, the following cmdlet can be run to permanently remove the deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="8e307-130">Skąd wiadomo, to pracy?</span><span class="sxs-lookup"><span data-stu-id="8e307-130">How do you know this worked?</span></span>
<span data-ttu-id="8e307-131">Aby sprawdzić, czy został pomyślnie przywrócił grupy usługi Office 365, uruchom `Get-AzureADGroup –ObjectId <objectId>` polecenia cmdlet, aby wyświetlić informacje o grupie.</span><span class="sxs-lookup"><span data-stu-id="8e307-131">To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group.</span></span> <span data-ttu-id="8e307-132">Po przywróceniu jest ukończone żądania:</span><span class="sxs-lookup"><span data-stu-id="8e307-132">After the restore request is completed:</span></span>
- <span data-ttu-id="8e307-133">Grupa pojawi się na lewym pasku nawigacyjnym na serwerze Exchange</span><span class="sxs-lookup"><span data-stu-id="8e307-133">The group will appear in the Left nav bar on Exchange</span></span>
- <span data-ttu-id="8e307-134">Plan dla tej grupy będą wyświetlane w planowania</span><span class="sxs-lookup"><span data-stu-id="8e307-134">The plan for the group will appear in Planner</span></span>
- <span data-ttu-id="8e307-135">Witryny programu Sharepoint i wszystkie ich zawartość będzie dostępna</span><span class="sxs-lookup"><span data-stu-id="8e307-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="8e307-136">Grupy jest możliwy za pomocą dowolnego punkty końcowe programu Exchange i innych obciążeń usługi Office 365, które obsługują grup usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="8e307-136">The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="8e307-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8e307-137">Next steps</span></span>
<span data-ttu-id="8e307-138">Te artykuły zawierają dodatkowe informacje o grupach usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e307-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="8e307-139">Zobacz istniejących grup</span><span class="sxs-lookup"><span data-stu-id="8e307-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="8e307-140">Zarządzanie ustawieniami grupy</span><span class="sxs-lookup"><span data-stu-id="8e307-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="8e307-141">Elementy członkowskie grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="8e307-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="8e307-142">Zarządzanie członkostwami grup</span><span class="sxs-lookup"><span data-stu-id="8e307-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="8e307-143">Dynamiczne reguły dla użytkowników w grupie zarządzania</span><span class="sxs-lookup"><span data-stu-id="8e307-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
