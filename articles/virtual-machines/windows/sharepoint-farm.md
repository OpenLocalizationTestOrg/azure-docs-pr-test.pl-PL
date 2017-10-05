---
title: "Tworzenie farmy serwerów programu SharePoint na platformie Azure | Dokumentacja firmy Microsoft"
description: "Szybko utworzyć nową farmę programu SharePoint 2013 lub SharePoint 2016 na platformie Azure przy użyciu witrynę portalu Azure marketplace."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 00648ee35962b22fb7eeceaa6d9df7305c801abf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-sharepoint-server-farms-using-the-azure-portal-marketplace"></a><span data-ttu-id="271d7-103">Tworzenie farmy serwerów programu SharePoint przy użyciu witrynę portalu Azure marketplace</span><span class="sxs-lookup"><span data-stu-id="271d7-103">Create SharePoint server farms using the Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="271d7-104">Farm programu SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="271d7-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="271d7-105">Microsoft Azure Marketplace portalu można szybko utworzyć wstępnie skonfigurowane farm programu SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="271d7-105">With the Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="271d7-106">To można zaoszczędzić dużo czasu na potrzeby farmy programu SharePoint podstawowego lub wysokiej dostępności dla środowiska i testowania lub jeśli dokonujesz oceny programu SharePoint Server 2013 jako rozwiązanie współpracy dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="271d7-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="271d7-107">**Farmy serwerów programu SharePoint** usunięto element w portalu Azure Marketplace w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="271d7-107">The **SharePoint Server Farm** item in the Azure Marketplace of the Azure portal has been removed.</span></span> <span data-ttu-id="271d7-108">Zostało zastąpione przez **farmy SharePoint 2013 nie - HA** i **farmy programu SharePoint 2013 HA** elementów.</span><span class="sxs-lookup"><span data-stu-id="271d7-108">It has been replaced with the **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="271d7-109">Podstawowe farmy programu SharePoint obejmuje trzy maszyny wirtualne w tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="271d7-109">The basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="271d7-111">Uproszczona konfiguracja do tworzenia aplikacji programu SharePoint lub ocenę pierwszego programu SharePoint 2013, można użyć tej konfiguracji farmy.</span><span class="sxs-lookup"><span data-stu-id="271d7-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="271d7-112">Aby utworzyć podstawowy farmy programu SharePoint (trzech serwerów):</span><span class="sxs-lookup"><span data-stu-id="271d7-112">To create the basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="271d7-113">Kliknij przycisk [tutaj](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span><span class="sxs-lookup"><span data-stu-id="271d7-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="271d7-114">Kliknij przycisk **wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="271d7-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="271d7-115">Na **farmy SharePoint 2013 nie - HA** okienku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="271d7-115">On the **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="271d7-116">Określ ustawienia na kroki **tworzenia farmy SharePoint 2013 nie - HA** okienka, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="271d7-116">Specify settings on the steps of the **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="271d7-117">Farma programu SharePoint wysokiej dostępności składa się z dziewięciu maszyn wirtualnych w tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="271d7-117">The high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="271d7-119">Tej konfiguracji farmy służy do testowania wyższej klienta obciążenia, wysoką dostępność zewnętrznej witryny programu SharePoint i grup dostępności AlwaysOn programu SQL Server dla farmy programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="271d7-119">You can use this farm configuration to test higher client loads, high availability of the external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="271d7-120">Ta konfiguracja służy także do tworzenia aplikacji programu SharePoint w środowisku o wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="271d7-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="271d7-121">Aby utworzyć farmę programu SharePoint (serwerze 9) wysokiej dostępności:</span><span class="sxs-lookup"><span data-stu-id="271d7-121">To create the high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="271d7-122">Kliknij przycisk [tutaj](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span><span class="sxs-lookup"><span data-stu-id="271d7-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="271d7-123">Kliknij przycisk **wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="271d7-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="271d7-124">Na **farmy programu SharePoint 2013 HA** okienku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="271d7-124">On the **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="271d7-125">Określ ustawienia na siedem kroków **tworzenia farmy programu SharePoint 2013 HA** okienka, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="271d7-125">Specify settings on the seven steps of the **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="271d7-126">Nie można utworzyć **farmy SharePoint 2013 nie - HA** lub **farmy programu SharePoint 2013 HA** z bezpłatnej wersji próbnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="271d7-126">You cannot create the **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="271d7-127">Azure portal tworzy oba te farm tylko w chmurze sieci wirtualnej internetowy witrynę internetową.</span><span class="sxs-lookup"><span data-stu-id="271d7-127">The Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="271d7-128">Brak połączenia lokacja lokacja sieci VPN i ExpressRoute do sieci organizacji.</span><span class="sxs-lookup"><span data-stu-id="271d7-128">There is no site-to-site VPN or ExpressRoute connection back to your organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="271d7-129">Podczas tworzenia podstawowego lub farmy programu SharePoint wysokiej dostępności przy użyciu portalu Azure, nie można określić istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="271d7-129">When you create the basic or high-availability SharePoint farms using the Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="271d7-130">Aby obejść to ograniczenie, Utwórz te farm przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="271d7-130">To work around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="271d7-131">Aby uzyskać więcej informacji, zobacz [tworzenie programu SharePoint 2013: tworzenie i testowanie farm przy użyciu programu Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="271d7-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="271d7-132">Farm programu SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="271d7-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="271d7-133">Zobacz [w tym artykule](https://technet.microsoft.com/library/mt723354.aspx) instrukcje dotyczące kompilacji następujące farmy programu SharePoint Server 2016 pojedynczego serwera.</span><span class="sxs-lookup"><span data-stu-id="271d7-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for the instructions to build the following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-the-sharepoint-farms"></a><span data-ttu-id="271d7-135">Zarządzanie farmy programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="271d7-135">Managing the SharePoint farms</span></span>
<span data-ttu-id="271d7-136">Serwery te farm za pomocą połączenia pulpitu zdalnego można administrować.</span><span class="sxs-lookup"><span data-stu-id="271d7-136">You can administer the servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="271d7-137">Aby uzyskać więcej informacji, zobacz [Zaloguj się do maszyny wirtualnej](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="271d7-137">For more information, see [Log on to the virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="271d7-138">Z lokacji centralnej administracji programu SharePoint można skonfigurować Moje witryny, aplikacji programu SharePoint i innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="271d7-138">From the Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="271d7-139">Aby uzyskać więcej informacji, zobacz [Konfigurowanie programu SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="271d7-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="271d7-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="271d7-140">Next steps</span></span>
* <span data-ttu-id="271d7-141">Odnajdywanie dodatkowe [konfiguracji programu SharePoint](https://technet.microsoft.com/library/dn635309.aspx) w usług infrastruktury platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="271d7-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
