---
title: "aaaPreview usługi Office 365 grupuje ważności w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooset się wygaśnięcia dla usługi Office 365 grup w usłudze Azure Active Directory (wersja zapoznawcza)"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="99998-103">Skonfiguruj wygaśnięcia grup usługi Office 365 (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="99998-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="99998-104">Możesz teraz zarządzać hello cyklem życia grup usługi Office 365, ustawiając wygaśnięcia w wybranych grupach usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="99998-104">You can now manage hello lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="99998-105">Po ustawieniu tej wygaśnięcia właścicieli tych grup są zadawane toorenew ich grup, jeśli nadal potrzebujesz hello grup.</span><span class="sxs-lookup"><span data-stu-id="99998-105">Once this expiration is set, owners of those groups are asked toorenew their groups if they still need hello groups.</span></span> <span data-ttu-id="99998-106">Wszystkie grupy usługi Office 365, która nie zostanie odnowiony zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="99998-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="99998-107">W ciągu 30 dni można przywrócić żadnej grupy usługi Office 365, który został usunięty przez właścicieli grupy hello lub hello administratora.</span><span class="sxs-lookup"><span data-stu-id="99998-107">Any Office 365 group that was deleted can be restored within 30 days by hello group owners or hello administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="99998-108">Można ustawić wygaśnięcie tylko grup usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="99998-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="99998-109">Ustawianie ważności dla grup usługi Office 365 wymaga przypisania licencji usługi Azure AD Premium do</span><span class="sxs-lookup"><span data-stu-id="99998-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="99998-110">Witaj, administrator konfiguruje ustawienia wygaśnięcia hello hello dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="99998-110">hello administrator who configures hello expiration settings for hello tenant</span></span>
>   - <span data-ttu-id="99998-111">Wszyscy członkowie grupy hello wybrana dla tego ustawienia</span><span class="sxs-lookup"><span data-stu-id="99998-111">All members of hello groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="99998-112">Ustawienia okresu ważności grup usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="99998-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="99998-113">Otwórz hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym w dzierżawie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99998-113">Open hello [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="99998-114">Otwórz usługę Azure AD, wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="99998-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="99998-115">Wybierz **ustawienia grupy** , a następnie wybierz **wygaśnięcia** ustawienia wygaśnięcia hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="99998-115">Select **Group settings** and then select **Expiration** tooopen hello expiration settings.</span></span>
  
  ![Blok wygaśnięcia](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="99998-117">Na powitania **wygaśnięcia** bloku, można wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="99998-117">On hello **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="99998-118">Ustaw okres istnienia grupy hello w dniach.</span><span class="sxs-lookup"><span data-stu-id="99998-118">Set hello group lifetime in days.</span></span> <span data-ttu-id="99998-119">Można wybrać jedną z hello ustawienia wartości lub wartości niestandardowych (powinien być 31 dni lub więcej).</span><span class="sxs-lookup"><span data-stu-id="99998-119">You could select one of hello preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="99998-120">Określ adres e-mail, w którym mają być wysyłane powiadomienia hello odnowienia i wygaśnięcia po grupie nie ma ono właściciela.</span><span class="sxs-lookup"><span data-stu-id="99998-120">Specify an email address where hello renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="99998-121">Wybierz grupy, które usługi Office 365 wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="99998-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="99998-122">Można włączyć wygaśnięcia dla **wszystkie** grup usługi Office 365, możesz wybrać spośród grup hello usługi Office 365 lub wybrać **Brak** wyłączyć wygaśnięcia dla wszystkich grup.</span><span class="sxs-lookup"><span data-stu-id="99998-122">You can enable expiration for **All** Office 365 groups, you can select from among hello Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="99998-123">Zapisz ustawienia, gdy wszystko będzie gotowe, wybierając **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="99998-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="99998-124">Aby uzyskać instrukcje dotyczące sposobu toodownload i zainstaluj hello wygaśnięcia tooconfigure modułu PowerShell firmy Microsoft dla grup usługi Office 365 za pomocą programu PowerShell, zobacz [Azure V2 PowerShell moduł usługi Active Directory - publicznej wersji zapoznawczej 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="99998-124">For instructions on how toodownload and install hello Microsoft PowerShell module tooconfigure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="99998-125">Powiadomienia e-mail, taką jak są wysyłane właścicieli grupy usługi Office 365 toohello 30 dni, 15 dni i 1 dzień przed tooexpiration hello grupy.</span><span class="sxs-lookup"><span data-stu-id="99998-125">Email notifications such as this one are sent toohello Office 365 group owners 30 days, 15 days, and 1 day prior tooexpiration of hello group.</span></span>

![Powiadomienia e-mail o wygaśnięciu](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="99998-127">Właściciel grupy Hello można wybrać **grupy odnawiania** toorenew hello grupy usługi Office 365 lub wybrać **Przejdź toogroup** członków hello toosee i inne szczegółowe informacje o hello grupy.</span><span class="sxs-lookup"><span data-stu-id="99998-127">hello group owner can then select **Renew group** toorenew hello Office 365 group, or can select **Go toogroup** toosee hello members and other details about hello group.</span></span>

<span data-ttu-id="99998-128">Po wygaśnięciu grupy jeden dzień po dacie wygaśnięcia hello jest usunąć hello grupy.</span><span class="sxs-lookup"><span data-stu-id="99998-128">When a group expires, hello group is deleted one day after hello expiration date.</span></span> <span data-ttu-id="99998-129">Powiadomienie e-mail, taką jak są wysyłane właścicieli grupy usługi Office 365 toohello informująca o wygaśnięciu hello i kolejne usunięcie ich z grupy usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="99998-129">An email notification such as this one is sent toohello Office 365 group owners informing them about hello expiration and subsequent deletion of their Office 365 group.</span></span>

![Powiadomienie e-mail usunięcia grupy](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="99998-131">Witaj grupy można przywrócić, wybierając **grupy przywracania** lub za pomocą poleceń cmdlet programu PowerShell, zgodnie z opisem w [przywracanie usuniętych usługi Office 365 grupy w usłudze Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-groups-Restore-Azure-Portal).</span><span class="sxs-lookup"><span data-stu-id="99998-131">hello group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="99998-132">Jeśli grupa hello, które są przywracane zawiera dokumentów, witryn programu SharePoint lub inne obiekty trwałe, może upłynąć too24 godziny toofully przywracania hello grupy i jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="99998-132">If hello group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up too24 hours toofully restore hello group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="99998-133">Podczas wdrażania ustawień wygasania hello, może być niektórych grup, które są starsze niż hello okna wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="99998-133">When deploying hello expiration settings, there might be some groups that are older than hello expiration window.</span></span> <span data-ttu-id="99998-134">Te grupy nie są można natychmiast usunąć, ale są too30 dni do wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="99998-134">These groups are not be immediately deleted, but are set too30 days until expiration.</span></span> <span data-ttu-id="99998-135">Hello pierwszy odnawiania powiadomienia e-mail jest wysyłane w ciągu dnia.</span><span class="sxs-lookup"><span data-stu-id="99998-135">hello first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="99998-136">Na przykład, A grupa została utworzona 400 dni temu i hello wygaśnięcia interwał jest ustawiany too180 dni.</span><span class="sxs-lookup"><span data-stu-id="99998-136">For example, Group A was created 400 days ago, and hello expiration interval is set too180 days.</span></span> <span data-ttu-id="99998-137">Podczas stosowania ustawień wygasania, A grupy ma 30 dni przed usunięciem, chyba że właściciela hello odnawia go.</span><span class="sxs-lookup"><span data-stu-id="99998-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless hello owner renews it.</span></span>
> * <span data-ttu-id="99998-138">Gdy dynamiczna grupa jest usuwane i przywrócić, jest to traktowane jako nową grupę i ponownie wypełnione zgodnie z reguły toohello.</span><span class="sxs-lookup"><span data-stu-id="99998-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according toohello rule.</span></span> <span data-ttu-id="99998-139">Ten proces może potrwać too24 godzin.</span><span class="sxs-lookup"><span data-stu-id="99998-139">This process might take up too24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99998-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="99998-140">Next steps</span></span>
<span data-ttu-id="99998-141">Te artykuły zawierają dodatkowe informacje o grup usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99998-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="99998-142">Zobacz istniejących grup</span><span class="sxs-lookup"><span data-stu-id="99998-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="99998-143">Zarządzanie ustawieniami grupy</span><span class="sxs-lookup"><span data-stu-id="99998-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="99998-144">Elementy członkowskie grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="99998-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="99998-145">Zarządzanie członkostwami grup</span><span class="sxs-lookup"><span data-stu-id="99998-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="99998-146">Dynamiczne reguły dla użytkowników w grupie zarządzania</span><span class="sxs-lookup"><span data-stu-id="99998-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
