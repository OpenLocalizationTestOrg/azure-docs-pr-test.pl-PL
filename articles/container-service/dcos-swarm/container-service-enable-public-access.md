---
title: "aaaEnable dostępu tooAzure DC/OS kontenera aplikacji | Dokumentacja firmy Microsoft"
description: "Jak tooenable publiczny dostęp do kontenerów tooDC/OS usługi kontenera platformy Azure."
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
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a><span data-ttu-id="a445a-104">Włączenie aplikacji usługi kontenera platformy Azure tooan dostępu publicznego</span><span class="sxs-lookup"><span data-stu-id="a445a-104">Enable public access tooan Azure Container Service application</span></span>
<span data-ttu-id="a445a-105">Każdy kontener DC/OS w hello ACS [puli agenta publicznego](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) jest automatycznie narażonych toohello internet.</span><span class="sxs-lookup"><span data-stu-id="a445a-105">Any DC/OS container in hello ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed toohello internet.</span></span> <span data-ttu-id="a445a-106">Domyślnie porty **80**, **443**, **8080** są otwarte i każdy kontener (publicznych) nasłuchuje na te porty są dostępne.</span><span class="sxs-lookup"><span data-stu-id="a445a-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="a445a-107">W tym artykule opisano, jak tooopen więcej portów dla aplikacji w usłudze kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a445a-107">This article shows you how tooopen more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="a445a-108">Otwórz port (portal)</span><span class="sxs-lookup"><span data-stu-id="a445a-108">Open a port (portal)</span></span>
<span data-ttu-id="a445a-109">Najpierw należy tooopen hello portu, którą chcemy udostępnić.</span><span class="sxs-lookup"><span data-stu-id="a445a-109">First, we need tooopen hello port we want.</span></span>

1. <span data-ttu-id="a445a-110">Zaloguj się w portalu toohello.</span><span class="sxs-lookup"><span data-stu-id="a445a-110">Log in toohello portal.</span></span>
2. <span data-ttu-id="a445a-111">Znajdź grupę zasobów hello, która została wdrożona hello usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a445a-111">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="a445a-112">Wybierz moduł równoważenia obciążenia agenta hello (który nosi nazwę podobne zbyt**XXXX-agent-lb-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="a445a-112">Select hello agent load balancer (which is named similar too**XXXX-agent-lb-XXXX**).</span></span>
   
    ![Moduł równoważenia obciążenia usługi kontenera platformy Azure](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="a445a-114">Kliknij przycisk **sondy** , a następnie **dodać**.</span><span class="sxs-lookup"><span data-stu-id="a445a-114">Click **Probes** and then **Add**.</span></span>
   
    ![Sondy modułu równoważenia obciążenia usługi kontenera platformy Azure](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="a445a-116">Wypełnij formularz sondowania hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a445a-116">Fill out hello probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="a445a-117">Pole</span><span class="sxs-lookup"><span data-stu-id="a445a-117">Field</span></span> | <span data-ttu-id="a445a-118">Opis</span><span class="sxs-lookup"><span data-stu-id="a445a-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="a445a-119">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a445a-119">Name</span></span> |<span data-ttu-id="a445a-120">Nazwa opisowa hello sondowania.</span><span class="sxs-lookup"><span data-stu-id="a445a-120">A descriptive name of hello probe.</span></span> |
   | <span data-ttu-id="a445a-121">Port</span><span class="sxs-lookup"><span data-stu-id="a445a-121">Port</span></span> |<span data-ttu-id="a445a-122">port Hello hello tootest kontenera.</span><span class="sxs-lookup"><span data-stu-id="a445a-122">hello port of hello container tootest.</span></span> |
   | <span data-ttu-id="a445a-123">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="a445a-123">Path</span></span> |<span data-ttu-id="a445a-124">(Podczas w trybie HTTP) hello tooprobe ścieżki względnej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a445a-124">(When in HTTP mode) hello relative website path tooprobe.</span></span> <span data-ttu-id="a445a-125">Protokół HTTPS nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a445a-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="a445a-126">Interwał</span><span class="sxs-lookup"><span data-stu-id="a445a-126">Interval</span></span> |<span data-ttu-id="a445a-127">próbuje Hello ilość czasu między sondowania, w sekundach.</span><span class="sxs-lookup"><span data-stu-id="a445a-127">hello amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="a445a-128">Próg złej kondycji</span><span class="sxs-lookup"><span data-stu-id="a445a-128">Unhealthy threshold</span></span> |<span data-ttu-id="a445a-129">Liczba kolejnych sondowania prób przed uwzględnieniu kontenera hello złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="a445a-129">Number of consecutive probe attempts before considering hello container unhealthy.</span></span> |
6. <span data-ttu-id="a445a-130">W hello właściwości usługi równoważenia obciążenia agenta hello, kliknij przycisk **reguły równoważenia obciążenia** , a następnie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a445a-130">Back at hello properties of hello agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Reguły modułu równoważenia obciążenia usługi kontenera platformy Azure](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="a445a-132">Wypełnij formularz usługi równoważenia obciążenia hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a445a-132">Fill out hello load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="a445a-133">Pole</span><span class="sxs-lookup"><span data-stu-id="a445a-133">Field</span></span> | <span data-ttu-id="a445a-134">Opis</span><span class="sxs-lookup"><span data-stu-id="a445a-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="a445a-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a445a-135">Name</span></span> |<span data-ttu-id="a445a-136">Nazwa opisowa hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="a445a-136">A descriptive name of hello load balancer.</span></span> |
   | <span data-ttu-id="a445a-137">Port</span><span class="sxs-lookup"><span data-stu-id="a445a-137">Port</span></span> |<span data-ttu-id="a445a-138">port publiczny przychodzące Hello.</span><span class="sxs-lookup"><span data-stu-id="a445a-138">hello public incoming port.</span></span> |
   | <span data-ttu-id="a445a-139">Port zaplecza</span><span class="sxs-lookup"><span data-stu-id="a445a-139">Backend port</span></span> |<span data-ttu-id="a445a-140">port wewnętrzny publicznego Hello hello kontenera tooroute ruchu do.</span><span class="sxs-lookup"><span data-stu-id="a445a-140">hello internal-public port of hello container tooroute traffic to.</span></span> |
   | <span data-ttu-id="a445a-141">Puli wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="a445a-141">Backend pool</span></span> |<span data-ttu-id="a445a-142">kontenery Hello w tej puli będzie hello docelowej dla tej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="a445a-142">hello containers in this pool will be hello target for this load balancer.</span></span> |
   | <span data-ttu-id="a445a-143">Sondy</span><span class="sxs-lookup"><span data-stu-id="a445a-143">Probe</span></span> |<span data-ttu-id="a445a-144">Witaj toodetermine sondowania używany, jeśli obiektem docelowym hello **puli zaplecza** jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="a445a-144">hello probe used toodetermine if a target in hello **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="a445a-145">Trwałość sesji</span><span class="sxs-lookup"><span data-stu-id="a445a-145">Session persistence</span></span> |<span data-ttu-id="a445a-146">Określa sposób obsługi ruchu w kliencie na czas trwania hello hello sesji.</span><span class="sxs-lookup"><span data-stu-id="a445a-146">Determines how traffic from a client should be handled for hello duration of hello session.</span></span><br><br><span data-ttu-id="a445a-147">**Brak**: kolejne żądania z tego samego klienta mogą być obsługiwane przez każdy kontener hello.</span><span class="sxs-lookup"><span data-stu-id="a445a-147">**None**: Successive requests from hello same client can be handled by any container.</span></span><br><span data-ttu-id="a445a-148">**Klient IP**: kolejne żądania z tego samego adresu IP klienta są obsługiwane przez hello hello tego samego kontenera.</span><span class="sxs-lookup"><span data-stu-id="a445a-148">**Client IP**: Successive requests from hello same client IP are handled by hello same container.</span></span><br><span data-ttu-id="a445a-149">**Klient IP i protokół**: kolejne żądania z samej kombinacji adresu IP i Protokół klienta są obsługiwane przez hello hello tego samego kontenera.</span><span class="sxs-lookup"><span data-stu-id="a445a-149">**Client IP and protocol**: Successive requests from hello same client IP and protocol combination are handled by hello same container.</span></span> |
   | <span data-ttu-id="a445a-150">Limit czasu bezczynności</span><span class="sxs-lookup"><span data-stu-id="a445a-150">Idle timeout</span></span> |<span data-ttu-id="a445a-151">(Tylko TCP) (W minutach) hello tookeep czasu klienta TCP/HTTP otwarty bez polegania na *keep-alive* wiadomości.</span><span class="sxs-lookup"><span data-stu-id="a445a-151">(TCP only) In minutes, hello time tookeep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="a445a-152">Dodawanie reguły zabezpieczeń (portal)</span><span class="sxs-lookup"><span data-stu-id="a445a-152">Add a security rule (portal)</span></span>
<span data-ttu-id="a445a-153">Następnie muszą tooadd regułę zabezpieczeń, który przekierowuje ruch z naszych otwarty port przez zaporę Windows hello.</span><span class="sxs-lookup"><span data-stu-id="a445a-153">Next, we need tooadd a security rule that routes traffic from our opened port through hello firewall.</span></span>

1. <span data-ttu-id="a445a-154">Zaloguj się w portalu toohello.</span><span class="sxs-lookup"><span data-stu-id="a445a-154">Log in toohello portal.</span></span>
2. <span data-ttu-id="a445a-155">Znajdź grupę zasobów hello, która została wdrożona hello usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a445a-155">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="a445a-156">Wybierz hello **publicznego** agenta sieciowej grupy zabezpieczeń (który nosi nazwę podobne zbyt**XXXX-agent publicznego nsg-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="a445a-156">Select hello **public** agent network security group (which is named similar too**XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Grupy zabezpieczeń sieci usługi kontenera platformy Azure](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="a445a-158">Wybierz **reguły zabezpieczeń dla ruchu przychodzącego** , a następnie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a445a-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Reguły grupy zabezpieczeń sieci usługi kontenera platformy Azure](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="a445a-160">Wypełnianie tooallow reguły zapory hello port publiczny i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a445a-160">Fill out hello firewall rule tooallow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="a445a-161">Pole</span><span class="sxs-lookup"><span data-stu-id="a445a-161">Field</span></span> | <span data-ttu-id="a445a-162">Opis</span><span class="sxs-lookup"><span data-stu-id="a445a-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="a445a-163">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a445a-163">Name</span></span> |<span data-ttu-id="a445a-164">Nazwę opisową hello reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="a445a-164">A descriptive name of hello firewall rule.</span></span> |
   | <span data-ttu-id="a445a-165">Priorytet</span><span class="sxs-lookup"><span data-stu-id="a445a-165">Priority</span></span> |<span data-ttu-id="a445a-166">Priorytet rangę hello reguły.</span><span class="sxs-lookup"><span data-stu-id="a445a-166">Priority rank for hello rule.</span></span> <span data-ttu-id="a445a-167">Witaj niższe hello numer hello wyższy hello priorytet.</span><span class="sxs-lookup"><span data-stu-id="a445a-167">hello lower hello number hello higher hello priority.</span></span> |
   | <span data-ttu-id="a445a-168">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="a445a-168">Source</span></span> |<span data-ttu-id="a445a-169">Ogranicz hello przychodzące IP adres zakresu toobe dozwolony lub odrzucany przez tę regułę.</span><span class="sxs-lookup"><span data-stu-id="a445a-169">Restrict hello incoming IP address range toobe allowed or denied by this rule.</span></span> <span data-ttu-id="a445a-170">Użyj **żadnych** toonot określ ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="a445a-170">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="a445a-171">Usługa</span><span class="sxs-lookup"><span data-stu-id="a445a-171">Service</span></span> |<span data-ttu-id="a445a-172">Wybierz zestaw wstępnie zdefiniowanych usług, których dotyczy ta zasada zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a445a-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="a445a-173">W przeciwnym razie użyj **niestandardowy** toocreate własne.</span><span class="sxs-lookup"><span data-stu-id="a445a-173">Otherwise use **Custom** toocreate your own.</span></span> |
   | <span data-ttu-id="a445a-174">Protokół</span><span class="sxs-lookup"><span data-stu-id="a445a-174">Protocol</span></span> |<span data-ttu-id="a445a-175">Ograniczanie ruchu na podstawie **TCP** lub **UDP**.</span><span class="sxs-lookup"><span data-stu-id="a445a-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="a445a-176">Użyj **żadnych** toonot określ ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="a445a-176">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="a445a-177">Zakres portów</span><span class="sxs-lookup"><span data-stu-id="a445a-177">Port range</span></span> |<span data-ttu-id="a445a-178">Gdy **usługi** jest **niestandardowe**, określa hello zakres portów, które ma wpływ ta reguła.</span><span class="sxs-lookup"><span data-stu-id="a445a-178">When **Service** is **Custom**, specifies hello range of ports that this rule affects.</span></span> <span data-ttu-id="a445a-179">Można użyć jednego portu, takich jak **80**, lub zakres, takich jak **1024 1500**.</span><span class="sxs-lookup"><span data-stu-id="a445a-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="a445a-180">Akcja</span><span class="sxs-lookup"><span data-stu-id="a445a-180">Action</span></span> |<span data-ttu-id="a445a-181">Zezwalaj lub Odmów ruchu, który spełnia kryteria hello.</span><span class="sxs-lookup"><span data-stu-id="a445a-181">Allow or deny traffic that meets hello criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a445a-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a445a-182">Next steps</span></span>
<span data-ttu-id="a445a-183">Dowiedz się więcej o hello różnica między [publiczne i prywatne agentów DC/OS](container-service-dcos-agents.md).</span><span class="sxs-lookup"><span data-stu-id="a445a-183">Learn about hello difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="a445a-184">Przeczytaj więcej informacji na temat [Zarządzanie kontenerów DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="a445a-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

