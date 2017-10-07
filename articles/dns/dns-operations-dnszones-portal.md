---
title: "aaaManage DNS strefy w usłudze Azure DNS - portalu Azure | Dokumentacja firmy Microsoft"
description: "Można zarządzać za pomocą portalu Azure hello stref DNS. W tym artykule opisano sposób tooupdate, usunąć i utworzyć strefy DNS w usłudze Azure DNS"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a><span data-ttu-id="e2dc9-104">Jak toomanage strefy DNS w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e2dc9-104">How toomanage DNS Zones in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e2dc9-105">Portal</span><span class="sxs-lookup"><span data-stu-id="e2dc9-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="e2dc9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2dc9-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="e2dc9-107">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e2dc9-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="e2dc9-108">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e2dc9-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="e2dc9-109">W tym artykule opisano, jak toomanage serwery DNS strefy za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-109">This article shows you how toomanage your DNS zones by using hello Azure portal.</span></span> <span data-ttu-id="e2dc9-110">Można również zarządzać stref DNS przy użyciu wieloplatformowych hello [interfejsu wiersza polecenia Azure](dns-operations-dnszones-cli.md) lub hello Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="e2dc9-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="e2dc9-111">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="e2dc9-111">Create a DNS zone</span></span>

1. <span data-ttu-id="e2dc9-112">Zaloguj się toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e2dc9-112">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="e2dc9-113">W menu centralnym hello, kliknij polecenie, a następnie kliknij przycisk **nowy > Sieć >** , a następnie kliknij przycisk **strefy DNS** bloku strefy DNS Utwórz hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-113">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Strefa DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="e2dc9-115">Na powitania **strefy DNS Utwórz** bloku wprowadź hello następujące wartości, a następnie kliknij przycisk **Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="e2dc9-115">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="e2dc9-116">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="e2dc9-116">**Setting**</span></span> | <span data-ttu-id="e2dc9-117">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="e2dc9-117">**Value**</span></span> | <span data-ttu-id="e2dc9-118">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="e2dc9-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="e2dc9-119">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="e2dc9-119">**Name**</span></span>|<span data-ttu-id="e2dc9-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="e2dc9-120">contoso.com</span></span>|<span data-ttu-id="e2dc9-121">Nazwa Hello hello strefy DNS</span><span class="sxs-lookup"><span data-stu-id="e2dc9-121">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="e2dc9-122">**Subskrypcja**</span><span class="sxs-lookup"><span data-stu-id="e2dc9-122">**Subscription**</span></span>|<span data-ttu-id="e2dc9-123">[Twoja subskrypcja]</span><span class="sxs-lookup"><span data-stu-id="e2dc9-123">[Your subscription]</span></span>|<span data-ttu-id="e2dc9-124">Wybierz strefę DNS subskrypcji toocreate hello w.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-124">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="e2dc9-125">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="e2dc9-125">**Resource group**</span></span>|<span data-ttu-id="e2dc9-126">**Utwórz nową:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="e2dc9-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="e2dc9-127">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-127">Create a resource group.</span></span> <span data-ttu-id="e2dc9-128">Nazwa grupy zasobów Hello musi być unikatowa w ramach subskrypcji hello, wybranych.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-128">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="e2dc9-129">więcej informacji na temat grup zasobów, przeczytaj hello toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artykuł z omówieniem.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-129">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="e2dc9-130">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="e2dc9-130">**Location**</span></span>|<span data-ttu-id="e2dc9-131">Zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="e2dc9-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="e2dc9-132">Grupa zasobów Hello odwołuje się lokalizacji toohello hello grupy zasobów, a nie ma wpływu na powitania strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-132">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="e2dc9-133">Lokalizacja strefy DNS Hello jest zawsze "globalne" i nie jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-133">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="e2dc9-134">Lista stref DNS</span><span class="sxs-lookup"><span data-stu-id="e2dc9-134">List DNS zones</span></span>

<span data-ttu-id="e2dc9-135">W portalu Azure hello kolejno zbyt**więcej usług** > **sieci** > **stref DNS**.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-135">In hello Azure portal, navigate too**More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="e2dc9-136">Każdej strefy DNS jest jest własnych zasobów, informacje, takie jak liczba zestawów rekordów i serwery nazw są widoczne w tym widoku.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="e2dc9-137">Kolumna Hello **serwery nazw** nie występuje w hello widok domyślny, tooadd kliknij **kolumn**, wybierz pozycję **serwery nazw** i kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-137">hello column **NAME SERVERS** is not in hello default view, tooadd it click **Columns**, select **Name servers** and click **Done**.</span></span>

![Lista stref DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="e2dc9-139">Usuń strefę DNS</span><span class="sxs-lookup"><span data-stu-id="e2dc9-139">Delete a DNS zone</span></span>

<span data-ttu-id="e2dc9-140">Przejdź tooa strefy DNS w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-140">Navigate tooa DNS zone in hello portal.</span></span> <span data-ttu-id="e2dc9-141">Na powitania **strefy DNS** bloku, kliknij przycisk **Usuń strefę**.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-141">On hello **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="e2dc9-142">Jesteś zostanie wyświetlony monit o tooconfirm są pożądane strefy DNS hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-142">You are prompted tooconfirm you are wanting toodelete hello DNS zone.</span></span> <span data-ttu-id="e2dc9-143">Usunięcie strefy DNS powoduje usunięcie wszystkich rekordów hello, które są zawarte w strefie hello.</span><span class="sxs-lookup"><span data-stu-id="e2dc9-143">Deleting a DNS zone also deletes all hello records that are contained in hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2dc9-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e2dc9-144">Next steps</span></span>

<span data-ttu-id="e2dc9-145">Dowiedz się, jak toowork strefy DNS i rekordy odwiedzając [wprowadzenie do usługi Azure DNS przy użyciu portalu Azure hello](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e2dc9-145">Learn how toowork with your DNS Zone and records by visiting [Get started with Azure DNS using hello Azure portal](dns-getstarted-portal.md).</span></span>
