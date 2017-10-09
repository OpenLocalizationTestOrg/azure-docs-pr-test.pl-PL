---
title: "Dzienniki przepływu grupy zabezpieczeń sieci aaaManage z obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono sposób rejestrowania toomanage przepływu sieciowej grupy zabezpieczeń w obserwatora sieciowego Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a><span data-ttu-id="8a997-103">Zarządzanie dziennikami przepływu grupy zabezpieczeń sieci w portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="8a997-103">Manage network security group flow logs in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8a997-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8a997-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="8a997-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a997-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="8a997-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="8a997-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="8a997-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="8a997-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="8a997-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="8a997-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="8a997-109">Dzienniki przepływu grupy zabezpieczeń sieci są funkcją obserwatora sieciowego, umożliwiający tooview informacji na temat przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="8a997-109">Network security group flow logs are a feature of Network Watcher that enables you tooview information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="8a997-110">Te dzienniki przepływu są zapisywane w formacie JSON i zawierają istotne informacje, w tym:</span><span class="sxs-lookup"><span data-stu-id="8a997-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="8a997-111">Wychodzące i przychodzące przepływem na podstawie reguł.</span><span class="sxs-lookup"><span data-stu-id="8a997-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="8a997-112">dotyczy Hello hello przepływ karty interfejsu Sieciowego.</span><span class="sxs-lookup"><span data-stu-id="8a997-112">hello NIC that hello flow applies to.</span></span>
- <span data-ttu-id="8a997-113">5-elementowej informacje o przepływu hello (źródłowego i docelowego adresu IP, portu źródłowego i docelowego, protokół).</span><span class="sxs-lookup"><span data-stu-id="8a997-113">5-tuple information about hello flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="8a997-114">Informacja, czy dozwolony lub odrzucany ruchu.</span><span class="sxs-lookup"><span data-stu-id="8a997-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8a997-115">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="8a997-115">Before you begin</span></span>

<span data-ttu-id="8a997-116">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć wystąpienia obserwatora sieciowego](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="8a997-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="8a997-117">Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="8a997-117">hello scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="8a997-118">Zarejestruj dostawcę usługi Insights</span><span class="sxs-lookup"><span data-stu-id="8a997-118">Register Insights provider</span></span>

<span data-ttu-id="8a997-119">Przepływ hello pomyślnie, rejestrowanie toowork **elemencie Microsoft.Insights** dostawcy musi być zarejestrowana.</span><span class="sxs-lookup"><span data-stu-id="8a997-119">For flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="8a997-120">Dostawca hello tooregister, hello wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8a997-120">tooregister hello provider, take hello following steps:</span></span> 

1. <span data-ttu-id="8a997-121">Przejdź za**subskrypcje**, a następnie wybierz hello subskrypcji, dla której ma zostać tooenable przepływu dzienników.</span><span class="sxs-lookup"><span data-stu-id="8a997-121">Go too**Subscriptions**, and then select hello subscription for which you want tooenable flow logs.</span></span> 
2. <span data-ttu-id="8a997-122">Na powitania **subskrypcji** bloku, wybierz opcję **dostawców zasobów**.</span><span class="sxs-lookup"><span data-stu-id="8a997-122">On hello **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="8a997-123">Spójrz na hello listy dostawców i sprawdź, że hello **elemencie microsoft.insights** dostawca został zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="8a997-123">Look at hello list of providers, and verify that hello **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="8a997-124">Jeśli nie, następnie wybierz **zarejestrować**.</span><span class="sxs-lookup"><span data-stu-id="8a997-124">If not, then select **Register**.</span></span>

![Widok dostawców][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="8a997-126">Włączanie dzienników przepływu</span><span class="sxs-lookup"><span data-stu-id="8a997-126">Enable flow logs</span></span>

<span data-ttu-id="8a997-127">Te kroki przejście hello proces włączania przepływu dzienniki w lokacji sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="8a997-127">These steps take you through hello process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="8a997-128">Krok 1</span><span class="sxs-lookup"><span data-stu-id="8a997-128">Step 1</span></span>

<span data-ttu-id="8a997-129">Przejdź do wystąpienia obserwatora sieciowego tooa, a następnie wybierz **przepływ NSG rejestruje**.</span><span class="sxs-lookup"><span data-stu-id="8a997-129">Go tooa Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Przegląd dzienników przepływu][1]

### <a name="step-2"></a><span data-ttu-id="8a997-131">Krok 2</span><span class="sxs-lookup"><span data-stu-id="8a997-131">Step 2</span></span>

<span data-ttu-id="8a997-132">Wybierz grupy zabezpieczeń sieci z listy hello.</span><span class="sxs-lookup"><span data-stu-id="8a997-132">Select a network security group from hello list.</span></span>

![Przegląd dzienników przepływu][2]

### <a name="step-3"></a><span data-ttu-id="8a997-134">Krok 3</span><span class="sxs-lookup"><span data-stu-id="8a997-134">Step 3</span></span> 

<span data-ttu-id="8a997-135">Na powitania **ustawień dzienników przepływu** bloku, Ustaw stan hello zbyt**na**, a następnie skonfiguruj konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="8a997-135">On hello **Flow logs settings** blade, set hello status too**On**, and then configure a storage account.</span></span>  <span data-ttu-id="8a997-136">Gdy wszystko będzie gotowe, wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="8a997-136">When you're done, select **OK**.</span></span> <span data-ttu-id="8a997-137">Następnie wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="8a997-137">Then select **Save**.</span></span>

![Przegląd dzienników przepływu][3]

## <a name="download-flow-logs"></a><span data-ttu-id="8a997-139">Pobierz dzienniki przepływu</span><span class="sxs-lookup"><span data-stu-id="8a997-139">Download flow logs</span></span>

<span data-ttu-id="8a997-140">Przepływ dzienniki są zapisywane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="8a997-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="8a997-141">Pobieranie Twojej tooview dzienniki przepływu je.</span><span class="sxs-lookup"><span data-stu-id="8a997-141">Download your flow logs tooview them.</span></span>

### <a name="step-1"></a><span data-ttu-id="8a997-142">Krok 1</span><span class="sxs-lookup"><span data-stu-id="8a997-142">Step 1</span></span>

<span data-ttu-id="8a997-143">toodownload przepływ dzienników, wybierz **dzienniki przepływu można pobrać z kont magazynu skonfigurowanych**.</span><span class="sxs-lookup"><span data-stu-id="8a997-143">toodownload flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="8a997-144">Ten krok umożliwia przejście widoku konto magazynu tooa którego można określić, które toodownload dzienniki.</span><span class="sxs-lookup"><span data-stu-id="8a997-144">This step takes you tooa storage account view where you can choose which logs toodownload.</span></span>

![Przepływ ustawień dzienników][4]

### <a name="step-2"></a><span data-ttu-id="8a997-146">Krok 2</span><span class="sxs-lookup"><span data-stu-id="8a997-146">Step 2</span></span>

<span data-ttu-id="8a997-147">Przejdź do konta magazynu poprawne toohello.</span><span class="sxs-lookup"><span data-stu-id="8a997-147">Go toohello correct storage account.</span></span> <span data-ttu-id="8a997-148">Następnie wybierz **kontenery** > **insights — dziennik networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="8a997-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Przepływ ustawień dzienników][5]

### <a name="step-3"></a><span data-ttu-id="8a997-150">Krok 3</span><span class="sxs-lookup"><span data-stu-id="8a997-150">Step 3</span></span>

<span data-ttu-id="8a997-151">Przejdź do lokalizacji toohello hello przepływu dziennika, zaznacz go, a następnie wybierz **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="8a997-151">Go toohello location of hello flow log, select it, and then select **Download**.</span></span>

![Przepływ ustawień dzienników][6]

<span data-ttu-id="8a997-153">Informacji o strukturze hello hello dziennika można znaleźć [Omówienie dziennika przepływu grupy zabezpieczeń sieci](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a997-153">For information about hello structure of hello log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a997-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8a997-154">Next steps</span></span>

<span data-ttu-id="8a997-155">Dowiedz się, jak za[wizualizacji dzienników przepływu grupy NSG z usługą Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="8a997-155">Learn how too[visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
