---
title: "Zapewnianie dostępu do aplikacji kontenera Azure DC/OS | Dokumentacja firmy Microsoft"
description: "Jak włączyć publicznego dostępu do kontenerów DC/OS usługi kontenera platformy Azure."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c9ef5913859cf3a55a2de2107a9304f1d28a4829
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="enable-public-access-to-an-azure-container-service-application"></a><span data-ttu-id="bdb9e-104">Włącz publiczny dostęp do aplikacji usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bdb9e-104">Enable public access to an Azure Container Service application</span></span>
<span data-ttu-id="bdb9e-105">Każdy kontener DC/OS w ACS [puli agenta publicznego](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) automatycznie połączenie z Internetem.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-105">Any DC/OS container in the ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed to the internet.</span></span> <span data-ttu-id="bdb9e-106">Domyślnie porty **80**, **443**, **8080** są otwarte i każdy kontener (publicznych) nasłuchuje na te porty są dostępne.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="bdb9e-107">W tym artykule przedstawiono sposób otwierania więcej portów dla aplikacji w usłudze kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-107">This article shows you how to open more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="bdb9e-108">Otwórz port (portal)</span><span class="sxs-lookup"><span data-stu-id="bdb9e-108">Open a port (portal)</span></span>
<span data-ttu-id="bdb9e-109">Najpierw należy otworzyć port, którego chcemy.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-109">First, we need to open the port we want.</span></span>

1. <span data-ttu-id="bdb9e-110">Zaloguj się do portalu.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-110">Log in to the portal.</span></span>
2. <span data-ttu-id="bdb9e-111">Znajdź wdrożonej usługi kontenera platformy Azure do grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-111">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="bdb9e-112">Wybierz usługę równoważenia obciążenia agenta (nosi podobny do **XXXX-agent-lb-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="bdb9e-112">Select the agent load balancer (which is named similar to **XXXX-agent-lb-XXXX**).</span></span>
   
    ![Moduł równoważenia obciążenia usługi kontenera platformy Azure](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="bdb9e-114">Kliknij przycisk **sondy** , a następnie **dodać**.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-114">Click **Probes** and then **Add**.</span></span>
   
    ![Sondy modułu równoważenia obciążenia usługi kontenera platformy Azure](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="bdb9e-116">Wypełnij formularz sondowania, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-116">Fill out the probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="bdb9e-117">Pole</span><span class="sxs-lookup"><span data-stu-id="bdb9e-117">Field</span></span> | <span data-ttu-id="bdb9e-118">Opis</span><span class="sxs-lookup"><span data-stu-id="bdb9e-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="bdb9e-119">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bdb9e-119">Name</span></span> |<span data-ttu-id="bdb9e-120">Opisowa nazwa sondy.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-120">A descriptive name of the probe.</span></span> |
   | <span data-ttu-id="bdb9e-121">Port</span><span class="sxs-lookup"><span data-stu-id="bdb9e-121">Port</span></span> |<span data-ttu-id="bdb9e-122">Port kontenera do testowania.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-122">The port of the container to test.</span></span> |
   | <span data-ttu-id="bdb9e-123">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="bdb9e-123">Path</span></span> |<span data-ttu-id="bdb9e-124">(Podczas w trybie HTTP) Ścieżka względna witryny sieci Web do sondowania.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-124">(When in HTTP mode) The relative website path to probe.</span></span> <span data-ttu-id="bdb9e-125">Protokół HTTPS nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="bdb9e-126">Interwał</span><span class="sxs-lookup"><span data-stu-id="bdb9e-126">Interval</span></span> |<span data-ttu-id="bdb9e-127">Ilość czasu między sondowania prób w sekundach.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-127">The amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="bdb9e-128">Próg złej kondycji</span><span class="sxs-lookup"><span data-stu-id="bdb9e-128">Unhealthy threshold</span></span> |<span data-ttu-id="bdb9e-129">Liczba kolejnych sondowania prób przed uwzględnieniu kontenera złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-129">Number of consecutive probe attempts before considering the container unhealthy.</span></span> |
6. <span data-ttu-id="bdb9e-130">W właściwości usługi równoważenia obciążenia agenta, kliknij przycisk **reguły równoważenia obciążenia** , a następnie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-130">Back at the properties of the agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Reguły modułu równoważenia obciążenia usługi kontenera platformy Azure](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="bdb9e-132">Wypełnij formularz usługi równoważenia obciążenia, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-132">Fill out the load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="bdb9e-133">Pole</span><span class="sxs-lookup"><span data-stu-id="bdb9e-133">Field</span></span> | <span data-ttu-id="bdb9e-134">Opis</span><span class="sxs-lookup"><span data-stu-id="bdb9e-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="bdb9e-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bdb9e-135">Name</span></span> |<span data-ttu-id="bdb9e-136">Opisowa nazwa usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-136">A descriptive name of the load balancer.</span></span> |
   | <span data-ttu-id="bdb9e-137">Port</span><span class="sxs-lookup"><span data-stu-id="bdb9e-137">Port</span></span> |<span data-ttu-id="bdb9e-138">Port publiczny przychodzących.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-138">The public incoming port.</span></span> |
   | <span data-ttu-id="bdb9e-139">Port zaplecza</span><span class="sxs-lookup"><span data-stu-id="bdb9e-139">Backend port</span></span> |<span data-ttu-id="bdb9e-140">Port wewnętrzny publicznego kontenera, aby kierować ruchem do.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-140">The internal-public port of the container to route traffic to.</span></span> |
   | <span data-ttu-id="bdb9e-141">Puli wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="bdb9e-141">Backend pool</span></span> |<span data-ttu-id="bdb9e-142">Kontenery w tej puli będzie docelowej dla tej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-142">The containers in this pool will be the target for this load balancer.</span></span> |
   | <span data-ttu-id="bdb9e-143">Sondy</span><span class="sxs-lookup"><span data-stu-id="bdb9e-143">Probe</span></span> |<span data-ttu-id="bdb9e-144">Sonda używany do określenia, czy element docelowy w **puli zaplecza** jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-144">The probe used to determine if a target in the **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="bdb9e-145">Trwałość sesji</span><span class="sxs-lookup"><span data-stu-id="bdb9e-145">Session persistence</span></span> |<span data-ttu-id="bdb9e-146">Określa sposób obsługi ruchu w kliencie na czas trwania sesji.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-146">Determines how traffic from a client should be handled for the duration of the session.</span></span><br><br><span data-ttu-id="bdb9e-147">**Brak**: kolejne żądania z tego samego klienta mogą być obsługiwane przez wszystkie kontenera.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-147">**None**: Successive requests from the same client can be handled by any container.</span></span><br><span data-ttu-id="bdb9e-148">**Klient IP**: kolejne żądania z tego samego adresu IP klienta są obsługiwane przez tego samego kontenera.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-148">**Client IP**: Successive requests from the same client IP are handled by the same container.</span></span><br><span data-ttu-id="bdb9e-149">**Klient IP i protokół**: kolejne żądania z tej samej kombinacji adresu IP i Protokół klienta są obsługiwane przez tego samego kontenera.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-149">**Client IP and protocol**: Successive requests from the same client IP and protocol combination are handled by the same container.</span></span> |
   | <span data-ttu-id="bdb9e-150">Limit czasu bezczynności</span><span class="sxs-lookup"><span data-stu-id="bdb9e-150">Idle timeout</span></span> |<span data-ttu-id="bdb9e-151">(Tylko TCP) W minutach czas przechowywania klienta TCP/HTTP Otwórz bez polegania na *keep-alive* wiadomości.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-151">(TCP only) In minutes, the time to keep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="bdb9e-152">Dodawanie reguły zabezpieczeń (portal)</span><span class="sxs-lookup"><span data-stu-id="bdb9e-152">Add a security rule (portal)</span></span>
<span data-ttu-id="bdb9e-153">Następnie należy dodać regułę zabezpieczeń, który przekierowuje ruch z naszych otwarty port przez zaporę.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-153">Next, we need to add a security rule that routes traffic from our opened port through the firewall.</span></span>

1. <span data-ttu-id="bdb9e-154">Zaloguj się do portalu.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-154">Log in to the portal.</span></span>
2. <span data-ttu-id="bdb9e-155">Znajdź wdrożonej usługi kontenera platformy Azure do grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-155">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="bdb9e-156">Wybierz **publicznego** agenta sieciowej grupy zabezpieczeń (nosi podobny do **XXXX-agent publicznego nsg-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="bdb9e-156">Select the **public** agent network security group (which is named similar to **XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Grupy zabezpieczeń sieci usługi kontenera platformy Azure](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="bdb9e-158">Wybierz **reguły zabezpieczeń dla ruchu przychodzącego** , a następnie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Reguły grupy zabezpieczeń sieci usługi kontenera platformy Azure](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="bdb9e-160">Wypełnianie reguły zapory, aby umożliwić port publiczny i kliknij pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-160">Fill out the firewall rule to allow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="bdb9e-161">Pole</span><span class="sxs-lookup"><span data-stu-id="bdb9e-161">Field</span></span> | <span data-ttu-id="bdb9e-162">Opis</span><span class="sxs-lookup"><span data-stu-id="bdb9e-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="bdb9e-163">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bdb9e-163">Name</span></span> |<span data-ttu-id="bdb9e-164">Opisowa nazwa reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-164">A descriptive name of the firewall rule.</span></span> |
   | <span data-ttu-id="bdb9e-165">Priorytet</span><span class="sxs-lookup"><span data-stu-id="bdb9e-165">Priority</span></span> |<span data-ttu-id="bdb9e-166">Ranga priorytet reguły.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-166">Priority rank for the rule.</span></span> <span data-ttu-id="bdb9e-167">Im mniejsza liczba wyższy priorytet.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-167">The lower the number the higher the priority.</span></span> |
   | <span data-ttu-id="bdb9e-168">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="bdb9e-168">Source</span></span> |<span data-ttu-id="bdb9e-169">Ogranicz przychodzące zakres adresów IP, aby być dozwolony lub odrzucany przez tę regułę.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-169">Restrict the incoming IP address range to be allowed or denied by this rule.</span></span> <span data-ttu-id="bdb9e-170">Użyj **żadnych** aby nie określać ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-170">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="bdb9e-171">Usługa</span><span class="sxs-lookup"><span data-stu-id="bdb9e-171">Service</span></span> |<span data-ttu-id="bdb9e-172">Wybierz zestaw wstępnie zdefiniowanych usług, których dotyczy ta zasada zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="bdb9e-173">W przeciwnym razie użyj **niestandardowy** do tworzenia własnych.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-173">Otherwise use **Custom** to create your own.</span></span> |
   | <span data-ttu-id="bdb9e-174">Protokół</span><span class="sxs-lookup"><span data-stu-id="bdb9e-174">Protocol</span></span> |<span data-ttu-id="bdb9e-175">Ograniczanie ruchu na podstawie **TCP** lub **UDP**.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="bdb9e-176">Użyj **żadnych** aby nie określać ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-176">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="bdb9e-177">Zakres portów</span><span class="sxs-lookup"><span data-stu-id="bdb9e-177">Port range</span></span> |<span data-ttu-id="bdb9e-178">Gdy **usługi** jest **niestandardowe**, określa zakres portów, które ma wpływ ta reguła.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-178">When **Service** is **Custom**, specifies the range of ports that this rule affects.</span></span> <span data-ttu-id="bdb9e-179">Można użyć jednego portu, takich jak **80**, lub zakres, takich jak **1024 1500**.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="bdb9e-180">Akcja</span><span class="sxs-lookup"><span data-stu-id="bdb9e-180">Action</span></span> |<span data-ttu-id="bdb9e-181">Zezwalaj lub Odmów ruchu, który spełnia kryteria.</span><span class="sxs-lookup"><span data-stu-id="bdb9e-181">Allow or deny traffic that meets the criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bdb9e-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bdb9e-182">Next steps</span></span>
<span data-ttu-id="bdb9e-183">Dowiedz się więcej na temat różnic między [publiczne i prywatne agentów DC/OS](container-service-dcos-agents.md).</span><span class="sxs-lookup"><span data-stu-id="bdb9e-183">Learn about the difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="bdb9e-184">Przeczytaj więcej informacji na temat [Zarządzanie kontenerów DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="bdb9e-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

