---
title: "Zarządzanie dziennikami przepływu grupy zabezpieczeń sieci z obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona opisano sposób zarządzania dziennikami przepływu sieciowej grupy zabezpieczeń w obserwatora sieciowego Azure"
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
ms.openlocfilehash: 41cb5ffab9bd3a3bed75ffdb6a7383ca1690f810
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-group-flow-logs-in-the-azure-portal"></a><span data-ttu-id="8fc04-103">Zarządzanie dziennikami przepływu grupy zabezpieczeń sieci w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8fc04-103">Manage network security group flow logs in the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8fc04-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8fc04-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="8fc04-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8fc04-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="8fc04-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="8fc04-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="8fc04-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="8fc04-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="8fc04-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="8fc04-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="8fc04-109">Dzienniki przepływu grupy zabezpieczeń sieci są funkcją obserwatora sieciowego, który umożliwia wyświetlenie informacji o przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="8fc04-109">Network security group flow logs are a feature of Network Watcher that enables you to view information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="8fc04-110">Te dzienniki przepływu są zapisywane w formacie JSON i zawierają istotne informacje, w tym:</span><span class="sxs-lookup"><span data-stu-id="8fc04-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="8fc04-111">Wychodzące i przychodzące przepływem na podstawie reguł.</span><span class="sxs-lookup"><span data-stu-id="8fc04-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="8fc04-112">Karta sieciowa, która dotyczy przepływu.</span><span class="sxs-lookup"><span data-stu-id="8fc04-112">The NIC that the flow applies to.</span></span>
- <span data-ttu-id="8fc04-113">5-elementowej informacje o przepływie (źródłowego i docelowego adresu IP, portu źródłowego i docelowego, protokół).</span><span class="sxs-lookup"><span data-stu-id="8fc04-113">5-tuple information about the flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="8fc04-114">Informacja, czy dozwolony lub odrzucany ruchu.</span><span class="sxs-lookup"><span data-stu-id="8fc04-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8fc04-115">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="8fc04-115">Before you begin</span></span>

<span data-ttu-id="8fc04-116">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć wystąpienia obserwatora sieciowego](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="8fc04-116">This scenario assumes you have already followed the steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="8fc04-117">Scenariusz założono również, czy masz grupy zasobów z prawidłową maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="8fc04-117">The scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="8fc04-118">Zarejestruj dostawcę usługi Insights</span><span class="sxs-lookup"><span data-stu-id="8fc04-118">Register Insights provider</span></span>

<span data-ttu-id="8fc04-119">Przepływ rejestrowanie działało poprawnie **elemencie Microsoft.Insights** dostawcy musi być zarejestrowana.</span><span class="sxs-lookup"><span data-stu-id="8fc04-119">For flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="8fc04-120">Aby zarejestrować dostawcę, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8fc04-120">To register the provider, take the following steps:</span></span> 

1. <span data-ttu-id="8fc04-121">Przejdź do **subskrypcje**, a następnie wybierz subskrypcję, dla której chcesz włączyć dzienniki przepływu.</span><span class="sxs-lookup"><span data-stu-id="8fc04-121">Go to **Subscriptions**, and then select the subscription for which you want to enable flow logs.</span></span> 
2. <span data-ttu-id="8fc04-122">Na **subskrypcji** bloku, wybierz opcję **dostawców zasobów**.</span><span class="sxs-lookup"><span data-stu-id="8fc04-122">On the **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="8fc04-123">Spójrz na listę dostawców i upewnij się, że **elemencie microsoft.insights** dostawca został zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="8fc04-123">Look at the list of providers, and verify that the **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="8fc04-124">Jeśli nie, następnie wybierz **zarejestrować**.</span><span class="sxs-lookup"><span data-stu-id="8fc04-124">If not, then select **Register**.</span></span>

![Widok dostawców][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="8fc04-126">Włączanie dzienników przepływu</span><span class="sxs-lookup"><span data-stu-id="8fc04-126">Enable flow logs</span></span>

<span data-ttu-id="8fc04-127">Następujące kroki umożliwiają włączenie przepływu dzienniki w lokacji sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="8fc04-127">These steps take you through the process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="8fc04-128">Krok 1</span><span class="sxs-lookup"><span data-stu-id="8fc04-128">Step 1</span></span>

<span data-ttu-id="8fc04-129">Przejdź do wystąpienia obserwatora sieciowego, a następnie wybierz **przepływ NSG rejestruje**.</span><span class="sxs-lookup"><span data-stu-id="8fc04-129">Go to a Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Przegląd dzienników przepływu][1]

### <a name="step-2"></a><span data-ttu-id="8fc04-131">Krok 2</span><span class="sxs-lookup"><span data-stu-id="8fc04-131">Step 2</span></span>

<span data-ttu-id="8fc04-132">Wybierz grupy zabezpieczeń sieci z listy.</span><span class="sxs-lookup"><span data-stu-id="8fc04-132">Select a network security group from the list.</span></span>

![Przegląd dzienników przepływu][2]

### <a name="step-3"></a><span data-ttu-id="8fc04-134">Krok 3</span><span class="sxs-lookup"><span data-stu-id="8fc04-134">Step 3</span></span> 

<span data-ttu-id="8fc04-135">Na **ustawień dzienników przepływu** bloku, Ustaw stan na **na**, a następnie skonfiguruj konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="8fc04-135">On the **Flow logs settings** blade, set the status to **On**, and then configure a storage account.</span></span>  <span data-ttu-id="8fc04-136">Gdy wszystko będzie gotowe, wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="8fc04-136">When you're done, select **OK**.</span></span> <span data-ttu-id="8fc04-137">Następnie wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="8fc04-137">Then select **Save**.</span></span>

![Przegląd dzienników przepływu][3]

## <a name="download-flow-logs"></a><span data-ttu-id="8fc04-139">Pobierz dzienniki przepływu</span><span class="sxs-lookup"><span data-stu-id="8fc04-139">Download flow logs</span></span>

<span data-ttu-id="8fc04-140">Przepływ dzienniki są zapisywane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="8fc04-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="8fc04-141">Pobierz dzienniki przepływu, aby je wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="8fc04-141">Download your flow logs to view them.</span></span>

### <a name="step-1"></a><span data-ttu-id="8fc04-142">Krok 1</span><span class="sxs-lookup"><span data-stu-id="8fc04-142">Step 1</span></span>

<span data-ttu-id="8fc04-143">Aby pobrać dzienniki przepływu, wybierz **dzienniki przepływu można pobrać z kont magazynu skonfigurowanych**.</span><span class="sxs-lookup"><span data-stu-id="8fc04-143">To download flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="8fc04-144">Ten krok przejście do widoku konto magazynu, na którym można wybrać dzienniki, które można pobrać.</span><span class="sxs-lookup"><span data-stu-id="8fc04-144">This step takes you to a storage account view where you can choose which logs to download.</span></span>

![Przepływ ustawień dzienników][4]

### <a name="step-2"></a><span data-ttu-id="8fc04-146">Krok 2</span><span class="sxs-lookup"><span data-stu-id="8fc04-146">Step 2</span></span>

<span data-ttu-id="8fc04-147">Przejdź do konta magazynu poprawne.</span><span class="sxs-lookup"><span data-stu-id="8fc04-147">Go to the correct storage account.</span></span> <span data-ttu-id="8fc04-148">Następnie wybierz **kontenery** > **insights — dziennik networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="8fc04-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Przepływ ustawień dzienników][5]

### <a name="step-3"></a><span data-ttu-id="8fc04-150">Krok 3</span><span class="sxs-lookup"><span data-stu-id="8fc04-150">Step 3</span></span>

<span data-ttu-id="8fc04-151">Przejdź do lokalizacji pliku dziennika przepływu, zaznacz go, a następnie wybierz **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="8fc04-151">Go to the location of the flow log, select it, and then select **Download**.</span></span>

![Przepływ ustawień dzienników][6]

<span data-ttu-id="8fc04-153">Informacje o strukturze dziennika, odwiedź stronę [Omówienie dziennika przepływu grupy zabezpieczeń sieci](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8fc04-153">For information about the structure of the log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fc04-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8fc04-154">Next steps</span></span>

<span data-ttu-id="8fc04-155">Dowiedz się, jak [wizualizacji dzienników przepływu grupy NSG z usługą Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="8fc04-155">Learn how to [visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
