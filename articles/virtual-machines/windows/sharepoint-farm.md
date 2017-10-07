---
title: "aaaCreate farmy serwerów programu SharePoint na platformie Azure | Dokumentacja firmy Microsoft"
description: "Szybko utworzyć nową farmę programu SharePoint 2013 lub SharePoint 2016 na platformie Azure przy użyciu hello Azure portalu marketplace."
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
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a><span data-ttu-id="6b8b3-103">Tworzenie farmy serwerów programu SharePoint przy użyciu hello Azure portalu marketplace</span><span class="sxs-lookup"><span data-stu-id="6b8b3-103">Create SharePoint server farms using hello Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="6b8b3-104">Farm programu SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="6b8b3-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="6b8b3-105">Microsoft Azure hello portalu Marketplace można szybko utworzyć wstępnie skonfigurowane farm programu SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-105">With hello Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="6b8b3-106">To można zaoszczędzić dużo czasu na potrzeby farmy programu SharePoint podstawowego lub wysokiej dostępności dla środowiska i testowania lub jeśli dokonujesz oceny programu SharePoint Server 2013 jako rozwiązanie współpracy dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="6b8b3-107">Witaj **farmy serwerów programu SharePoint** usunięto element w portalu Azure Marketplace hello hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-107">hello **SharePoint Server Farm** item in hello Azure Marketplace of hello Azure portal has been removed.</span></span> <span data-ttu-id="6b8b3-108">Zastąpiono z hello **farmy SharePoint 2013 nie - HA** i **farmy programu SharePoint 2013 HA** elementów.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-108">It has been replaced with hello **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="6b8b3-109">Hello podstawowego farmy programu SharePoint obejmuje trzy maszyny wirtualne w tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-109">hello basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="6b8b3-111">Uproszczona konfiguracja do tworzenia aplikacji programu SharePoint lub ocenę pierwszego programu SharePoint 2013, można użyć tej konfiguracji farmy.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="6b8b3-112">toocreate hello podstawowe (farmy trzech serwerów) programu SharePoint:</span><span class="sxs-lookup"><span data-stu-id="6b8b3-112">toocreate hello basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="6b8b3-113">Kliknij przycisk [tutaj](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span><span class="sxs-lookup"><span data-stu-id="6b8b3-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="6b8b3-114">Kliknij przycisk **wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="6b8b3-115">Na powitania **farmy SharePoint 2013 nie - HA** okienku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-115">On hello **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="6b8b3-116">Określ ustawienia na powitania kroki hello **tworzenia farmy SharePoint 2013 nie - HA** okienka, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-116">Specify settings on hello steps of hello **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="6b8b3-117">farma programu SharePoint wysokiej dostępności Hello składa się z dziewięciu maszyn wirtualnych w tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-117">hello high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="6b8b3-119">Można użyć tej farmy konfiguracji tootest wyższe klienta obciążeniem, wysoką dostępność hello zewnętrznej witryny programu SharePoint i grup dostępności AlwaysOn programu SQL Server dla farmy programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-119">You can use this farm configuration tootest higher client loads, high availability of hello external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="6b8b3-120">Ta konfiguracja służy także do tworzenia aplikacji programu SharePoint w środowisku o wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="6b8b3-121">farma programu SharePoint toocreate hello wysokiej dostępności (9 serwerów):</span><span class="sxs-lookup"><span data-stu-id="6b8b3-121">toocreate hello high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="6b8b3-122">Kliknij przycisk [tutaj](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span><span class="sxs-lookup"><span data-stu-id="6b8b3-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="6b8b3-123">Kliknij przycisk **wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="6b8b3-124">Na powitania **farmy programu SharePoint 2013 HA** okienku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-124">On hello **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="6b8b3-125">Określ ustawienia na powitania siedmiu kroków hello **tworzenia farmy programu SharePoint 2013 HA** okienka, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-125">Specify settings on hello seven steps of hello **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="6b8b3-126">Nie można utworzyć hello **farmy SharePoint 2013 nie - HA** lub **farmy programu SharePoint 2013 HA** z bezpłatnej wersji próbnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-126">You cannot create hello **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="6b8b3-127">Witaj portalu Azure tworzy oba te farm tylko w chmurze sieci wirtualnej internetowy witrynę internetową.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-127">hello Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="6b8b3-128">Nie jest żadna lokacja lokacja sieci VPN i ExpressRoute połączenia wstecz tooyour organizacji sieć.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-128">There is no site-to-site VPN or ExpressRoute connection back tooyour organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="6b8b3-129">Po hello tworzenia podstawowego lub farmy programu SharePoint wysokiej dostępności przy użyciu hello portalu Azure, nie można określić istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-129">When you create hello basic or high-availability SharePoint farms using hello Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="6b8b3-130">toowork wokół to ograniczenie, Utwórz te farm przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-130">toowork around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="6b8b3-131">Aby uzyskać więcej informacji, zobacz [tworzenie programu SharePoint 2013: tworzenie i testowanie farm przy użyciu programu Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="6b8b3-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="6b8b3-132">Farm programu SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="6b8b3-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="6b8b3-133">Zobacz [w tym artykule](https://technet.microsoft.com/library/mt723354.aspx) dla hello toobuild instrukcje powitania po jednym serwerze programu SharePoint Server 2016 farmy.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for hello instructions toobuild hello following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a><span data-ttu-id="6b8b3-135">Zarządzanie hello farmy programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b8b3-135">Managing hello SharePoint farms</span></span>
<span data-ttu-id="6b8b3-136">Można administrować serwerami hello tych farm za pomocą połączenia pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-136">You can administer hello servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="6b8b3-137">Aby uzyskać więcej informacji, zobacz [Zaloguj się na maszynie wirtualnej toohello](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="6b8b3-137">For more information, see [Log on toohello virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="6b8b3-138">Z lokacji centralnej administracji programu SharePoint hello można skonfigurować Moje witryny, aplikacji programu SharePoint i innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-138">From hello Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="6b8b3-139">Aby uzyskać więcej informacji, zobacz [Konfigurowanie programu SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b8b3-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b8b3-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6b8b3-140">Next steps</span></span>
* <span data-ttu-id="6b8b3-141">Odnajdywanie dodatkowe [konfiguracji programu SharePoint](https://technet.microsoft.com/library/dn635309.aspx) w usług infrastruktury platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6b8b3-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
