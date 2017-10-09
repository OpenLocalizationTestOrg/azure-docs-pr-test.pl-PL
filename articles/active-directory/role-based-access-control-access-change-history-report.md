---
title: "Raportowanie aaaAccess — Azure RBAC | Dokumentacja firmy Microsoft"
description: "Generowanie raportu, że wyświetla wszystkie zmiany w tooyour dostępu do subskrypcji platformy Azure z opartej na rolach kontrola dostępu za pośrednictwem hello w ciągu ostatnich 90 dni."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="89fdf-103">Tworzenie raportu programu access do kontroli dostępu opartej na rolach</span><span class="sxs-lookup"><span data-stu-id="89fdf-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="89fdf-104">Ilekroć ktoś lub go przydziela odwołuje dostęp w ramach subskrypcji, hello zmiany mają być rejestrowane w zdarzeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="89fdf-104">Any time someone grants or revokes access within your subscriptions, hello changes get logged in Azure events.</span></span> <span data-ttu-id="89fdf-105">Można utworzyć toosee raporty historii zmian dostępu do wszystkich zmian dla hello w ciągu ostatnich 90 dni.</span><span class="sxs-lookup"><span data-stu-id="89fdf-105">You can create access change history reports toosee all changes for hello past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="89fdf-106">Tworzenie raportu przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89fdf-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="89fdf-107">toocreate dostępu zmienić historii raportu w programie PowerShell, użyj hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) polecenia.</span><span class="sxs-lookup"><span data-stu-id="89fdf-107">toocreate an access change history report in PowerShell, use hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="89fdf-108">Po wywołaniu tego polecenia, można określić, które właściwości mają wymienionych w tym następujących hello przydziały hello:</span><span class="sxs-lookup"><span data-stu-id="89fdf-108">When you call this command, you can specify which property of hello assignments you want listed, including hello following:</span></span>

| <span data-ttu-id="89fdf-109">Właściwość</span><span class="sxs-lookup"><span data-stu-id="89fdf-109">Property</span></span> | <span data-ttu-id="89fdf-110">Opis</span><span class="sxs-lookup"><span data-stu-id="89fdf-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="89fdf-111">**Akcja**</span><span class="sxs-lookup"><span data-stu-id="89fdf-111">**Action**</span></span> |<span data-ttu-id="89fdf-112">Określa, czy przyznany lub odwołany dostęp</span><span class="sxs-lookup"><span data-stu-id="89fdf-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="89fdf-113">**Obiekt wywołujący**</span><span class="sxs-lookup"><span data-stu-id="89fdf-113">**Caller**</span></span> |<span data-ttu-id="89fdf-114">Zmień właściciela Hello odpowiedzialny za hello dostępu</span><span class="sxs-lookup"><span data-stu-id="89fdf-114">hello owner responsible for hello access change</span></span> |
| <span data-ttu-id="89fdf-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="89fdf-115">**PrincipalId**</span></span> | <span data-ttu-id="89fdf-116">Unikatowy identyfikator Hello hello użytkownika, grupy lub aplikacji, która została przypisana rola hello</span><span class="sxs-lookup"><span data-stu-id="89fdf-116">hello unique identifier of hello user, group, or application that was assigned hello role</span></span> |
| <span data-ttu-id="89fdf-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="89fdf-117">**PrincipalName**</span></span> |<span data-ttu-id="89fdf-118">Nazwa Hello hello użytkownika, grupy lub aplikacji</span><span class="sxs-lookup"><span data-stu-id="89fdf-118">hello name of hello user, group, or application</span></span> |
| <span data-ttu-id="89fdf-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="89fdf-119">**PrincipalType**</span></span> |<span data-ttu-id="89fdf-120">Określa, czy przypisania hello był przeznaczony dla użytkowników, grupy lub aplikacji</span><span class="sxs-lookup"><span data-stu-id="89fdf-120">Whether hello assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="89fdf-121">**Wartość RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="89fdf-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="89fdf-122">Witaj GUID hello roli, który został przyznany lub odwołany</span><span class="sxs-lookup"><span data-stu-id="89fdf-122">hello GUID of hello role that was granted or revoked</span></span> |
| <span data-ttu-id="89fdf-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="89fdf-123">**RoleName**</span></span> |<span data-ttu-id="89fdf-124">Rola Hello, który został przyznany lub odwołany</span><span class="sxs-lookup"><span data-stu-id="89fdf-124">hello role that was granted or revoked</span></span> |
| <span data-ttu-id="89fdf-125">**Zakres**</span><span class="sxs-lookup"><span data-stu-id="89fdf-125">**Scope**</span></span> | <span data-ttu-id="89fdf-126">Unikatowy identyfikator hello subskrypcji, grupy zasobów lub zasobów, które hello przypisania Hello stosuje zbyt</span><span class="sxs-lookup"><span data-stu-id="89fdf-126">hello unique identifier of hello subscription, resource group, or resource that hello assignment applies too</span></span>| 
| <span data-ttu-id="89fdf-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="89fdf-127">**ScopeName**</span></span> |<span data-ttu-id="89fdf-128">Nazwa Hello hello subskrypcji, grupy zasobów lub zasobów</span><span class="sxs-lookup"><span data-stu-id="89fdf-128">hello name of hello subscription, resource group, or resource</span></span> |
| <span data-ttu-id="89fdf-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="89fdf-129">**ScopeType**</span></span> |<span data-ttu-id="89fdf-130">Określa, czy hello przydział został w hello subskrypcji, grupy zasobów lub zasobów zakresu</span><span class="sxs-lookup"><span data-stu-id="89fdf-130">Whether hello assignment was at hello subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="89fdf-131">**Znacznik czasu**</span><span class="sxs-lookup"><span data-stu-id="89fdf-131">**Timestamp**</span></span> |<span data-ttu-id="89fdf-132">Witaj Data i godzina dostęp został zmieniony</span><span class="sxs-lookup"><span data-stu-id="89fdf-132">hello date and time that access was changed</span></span> |

<span data-ttu-id="89fdf-133">To polecenie przykładowe są wyświetlane wszystkie zmiany dostępu w hello subskrypcji na potrzeby hello ostatnich siedmiu dni:</span><span class="sxs-lookup"><span data-stu-id="89fdf-133">This example command lists all access changes in hello subscription for hello past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog — zrzut ekranu](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="89fdf-135">Tworzenie raportu z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="89fdf-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="89fdf-136">toocreate raportu historii zmian dostępu w hello Azure interfejsu wiersza polecenia (CLI), użyj hello `azure role assignment changelog list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="89fdf-136">toocreate an access change history report in hello Azure command-line interface (CLI), use hello `azure role assignment changelog list` command.</span></span>

## <a name="export-tooa-spreadsheet"></a><span data-ttu-id="89fdf-137">Arkusz kalkulacyjny tooa eksportu</span><span class="sxs-lookup"><span data-stu-id="89fdf-137">Export tooa spreadsheet</span></span>
<span data-ttu-id="89fdf-138">toosave hello raportu lub manipulować danymi hello, Eksport hello dostępu zmiany w pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="89fdf-138">toosave hello report, or manipulate hello data, export hello access changes into a .csv file.</span></span> <span data-ttu-id="89fdf-139">Następnie można wyświetlić raport hello w arkuszu kalkulacyjnym do przeglądu.</span><span class="sxs-lookup"><span data-stu-id="89fdf-139">You can then view hello report in a spreadsheet for review.</span></span>

![Wykaz zmian wyświetlane jako arkusz kalkulacyjny — zrzut ekranu](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="89fdf-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89fdf-141">Next steps</span></span>
* <span data-ttu-id="89fdf-142">Praca z [niestandardowych ról w Azure RBAC](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="89fdf-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="89fdf-143">Dowiedz się, jak toomanage [Azure RBAC przy użyciu programu powershell](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="89fdf-143">Learn how toomanage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

