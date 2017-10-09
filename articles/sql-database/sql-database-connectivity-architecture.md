---
title: "aaaAzure architektury połączenia bazy danych SQL | Dokumentacja firmy Microsoft"
description: "W tym dokumencie opisano hello Azure SQLDB łączności architektury od Azure lub z poza platformą Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="165d9-103">Architektura połączenia bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="165d9-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="165d9-104">W tym artykule opisano architektury połączenia bazy danych SQL Azure hello oraz wyjaśniono, jak hello różnych składników funkcji toodirect ruchu tooyour wystąpienia bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="165d9-104">This article explains hello Azure SQL Database connectivity architecture and explains how hello different components function toodirect traffic tooyour instance of Azure SQL Database.</span></span> <span data-ttu-id="165d9-105">Te składniki łączności bazy danych SQL Azure funkcji toohello ruchu sieciowego toodirect bazy danych platformy Azure z klientów łączących się w obrębie platformy Azure i klientów łączących się z poza platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="165d9-105">These Azure SQL Database connectivity components function toodirect network traffic toohello Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="165d9-106">Ten artykuł zawiera także jak łączność występuje toochange przykłady skryptów i hello zagadnienia związane z toochanging hello domyślnych łączności.</span><span class="sxs-lookup"><span data-stu-id="165d9-106">This article also provides script samples toochange how connectivity occurs, and hello considerations related toochanging hello default connectivity settings.</span></span> <span data-ttu-id="165d9-107">Jeśli istnieją jakieś pytania po przeczytaniu tego artykułu, skontaktuj się z Dhruv na dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="165d9-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="165d9-108">Architektura łączności</span><span class="sxs-lookup"><span data-stu-id="165d9-108">Connectivity architecture</span></span>

<span data-ttu-id="165d9-109">powitania po diagram zawiera omówienie hello architektury połączenia bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="165d9-109">hello following diagram provides a high-level overview of hello Azure SQL Database connectivity architecture.</span></span> 

![Przegląd architektury](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="165d9-111">Witaj poniższych krokach opisano sposób połączenie jest ustalonych tooan bazy danych Azure SQL za pośrednictwem hello bazy danych SQL Azure oprogramowania do równoważenia obciążenia (Programowego) i hello bramy bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="165d9-111">hello following steps describe how a connection is established tooan Azure SQL database through hello Azure SQL Database software load-balancer (SLB) and hello Azure SQL Database gateway.</span></span>

- <span data-ttu-id="165d9-112">Klienci w obrębie platformy Azure lub na zewnątrz Azure łączyć toohello Programowego, który ma publicznego adresu IP i nasłuchuje na porcie 1433.</span><span class="sxs-lookup"><span data-stu-id="165d9-112">Clients within Azure or outside of Azure connect toohello SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="165d9-113">Witaj Programowego kieruje ruch toohello bazy danych SQL Azure bramy.</span><span class="sxs-lookup"><span data-stu-id="165d9-113">hello SLB directs traffic toohello Azure SQL Database gateway.</span></span>
- <span data-ttu-id="165d9-114">Brama Hello przekierowuje hello ruchu toohello poprawne serwera proxy w oprogramowaniu pośredniczącym.</span><span class="sxs-lookup"><span data-stu-id="165d9-114">hello gateway redirects hello traffic toohello correct proxy middleware.</span></span>
- <span data-ttu-id="165d9-115">oprogramowanie pośredniczące serwera proxy Hello przekierowuje hello ruchu toohello odpowiednie bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="165d9-115">hello proxy middleware redirects hello traffic toohello appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="165d9-116">Każdy z tych składników został rozesłany odmowa wbudowanych w sieci hello i warstwy aplikacji hello protection service (DDoS).</span><span class="sxs-lookup"><span data-stu-id="165d9-116">Each of these components has distributed denial of service (DDoS) protection built-in at hello network and hello app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="165d9-117">Łączność między w obrębie platformy Azure</span><span class="sxs-lookup"><span data-stu-id="165d9-117">Connectivity from within Azure</span></span>

<span data-ttu-id="165d9-118">Jeśli nawiązujesz w obrębie platformy Azure połączenia mają zasady połączenia **przekierowania** domyślnie.</span><span class="sxs-lookup"><span data-stu-id="165d9-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="165d9-119">Zasady **przekierowania** oznacza, że połączenia bazy danych Azure SQL ustalonych toohello po sesji TCP hello powitania klienta sesji, a następnie przekierowanie oprogramowania pośredniczącego serwera proxy toohello z zmiany toohello docelowego wirtualnego adresu IP z który hello bazy danych SQL Azure bramy toothat oprogramowania pośredniczącego serwera proxy hello.</span><span class="sxs-lookup"><span data-stu-id="165d9-119">A policy of **Redirect** means that connections after hello TCP session is established toohello Azure SQL database, hello client session is then redirected toohello proxy middleware with a change toohello destination virtual IP from that of hello Azure SQL Database gateway toothat of hello proxy middleware.</span></span> <span data-ttu-id="165d9-120">Następnie wszystkie kolejne pakiety przepływać bezpośrednio za pomocą oprogramowania pośredniczącego serwera proxy hello, pomijanie hello bramy bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="165d9-120">Thereafter, all subsequent packets flow directly via hello proxy middleware, bypassing hello Azure SQL Database gateway.</span></span> <span data-ttu-id="165d9-121">powitania po diagram ilustruje tego przepływu ruchu.</span><span class="sxs-lookup"><span data-stu-id="165d9-121">hello following diagram illustrates this traffic flow.</span></span>

![Przegląd architektury](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="165d9-123">Łączność z poza platformą Azure</span><span class="sxs-lookup"><span data-stu-id="165d9-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="165d9-124">Jeśli łączysz się z zewnętrznej platformy Azure, połączenia mają zasady połączenia **Proxy** domyślnie.</span><span class="sxs-lookup"><span data-stu-id="165d9-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="165d9-125">Zasady **Proxy** oznacza, że ustanowieniu sesji TCP hello za pośrednictwem bramy bazy danych SQL Azure hello i wszystkie kolejne pakiety przepływu za pośrednictwem hello bramy.</span><span class="sxs-lookup"><span data-stu-id="165d9-125">A policy of **Proxy** means that hello TCP session is established via hello Azure SQL Database gateway and all subsequent packets flow via hello gateway.</span></span> <span data-ttu-id="165d9-126">powitania po diagram ilustruje tego przepływu ruchu.</span><span class="sxs-lookup"><span data-stu-id="165d9-126">hello following diagram illustrates this traffic flow.</span></span>

![Przegląd architektury](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="165d9-128">Adresy IP bramy bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="165d9-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="165d9-129">tooconnect tooan bazy danych Azure SQL z lokalnych zasobów, należy tooallow wychodzącego ruchu toohello bazy danych SQL Azure bramy w Twoim regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="165d9-129">tooconnect tooan Azure SQL database from on-premises resources, you need tooallow outbound network traffic toohello Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="165d9-130">Połączenia postępować tylko za pośrednictwem bramy hello podczas nawiązywania połączenia w trybie serwera Proxy, który jest domyślnym hello, podczas nawiązywania połączenia z zasobami lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="165d9-130">Your connections only go via hello gateway when connecting in Proxy mode, which is hello default when connecting from on-premises resources.</span></span>

<span data-ttu-id="165d9-131">Witaj w następującej tabeli przedstawiono hello głównych i dodatkowych adresów IP hello bramy bazy danych SQL Azure dla wszystkich obszarów danych.</span><span class="sxs-lookup"><span data-stu-id="165d9-131">hello following table lists hello primary and secondary IPs of hello Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="165d9-132">W pewnych regionach istnieją dwa adresy IP.</span><span class="sxs-lookup"><span data-stu-id="165d9-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="165d9-133">W tych regionów hello podstawowy adres IP jest hello bieżącego adresu IP bramy hello i hello drugiego adresu IP jest adresem IP trybu failover.</span><span class="sxs-lookup"><span data-stu-id="165d9-133">In these regions, hello primary IP address is hello current IP address of hello gateway and hello second IP address is a failover IP address.</span></span> <span data-ttu-id="165d9-134">adres trybu failover Hello jest toowhich adres hello firma Microsoft może przenieść Twojej tookeep hello usługi dostępność serwera wysokiej.</span><span class="sxs-lookup"><span data-stu-id="165d9-134">hello failover address is hello address toowhich we might move your server tookeep hello service availability high.</span></span> <span data-ttu-id="165d9-135">Dla tych regionów firma Microsoft zaleca Zezwalaj wychodzących tooboth hello adresy IP.</span><span class="sxs-lookup"><span data-stu-id="165d9-135">For these regions, we recommend that you allow outbound tooboth hello IP addresses.</span></span> <span data-ttu-id="165d9-136">Witaj drugiego adresu IP jest własnością firmy Microsoft i nie będzie nasłuchiwać na wszystkich usług, dopóki nie zostanie aktywowany przez połączenia tooaccept bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="165d9-136">hello second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database tooaccept connections.</span></span>

| <span data-ttu-id="165d9-137">Nazwa regionu</span><span class="sxs-lookup"><span data-stu-id="165d9-137">Region Name</span></span> | <span data-ttu-id="165d9-138">Podstawowy adres IP</span><span class="sxs-lookup"><span data-stu-id="165d9-138">Primary IP address</span></span> | <span data-ttu-id="165d9-139">Pomocniczy adres IP</span><span class="sxs-lookup"><span data-stu-id="165d9-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="165d9-140">Australia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="165d9-140">Australia East</span></span> | <span data-ttu-id="165d9-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="165d9-141">191.238.66.109</span></span> | <span data-ttu-id="165d9-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="165d9-142">13.75.149.87</span></span> |
| <span data-ttu-id="165d9-143">Australia Południowo-Wschodnia</span><span class="sxs-lookup"><span data-stu-id="165d9-143">Australia South East</span></span> | <span data-ttu-id="165d9-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="165d9-144">191.239.192.109</span></span> | <span data-ttu-id="165d9-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="165d9-145">13.73.109.251</span></span> |
| <span data-ttu-id="165d9-146">Brazylia Południowa</span><span class="sxs-lookup"><span data-stu-id="165d9-146">Brazil South</span></span> | <span data-ttu-id="165d9-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="165d9-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="165d9-148">Kanada Środkowa</span><span class="sxs-lookup"><span data-stu-id="165d9-148">Canada Central</span></span> | <span data-ttu-id="165d9-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="165d9-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="165d9-150">Kanada Wschodnia</span><span class="sxs-lookup"><span data-stu-id="165d9-150">Canada East</span></span> | <span data-ttu-id="165d9-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="165d9-151">40.86.226.166</span></span> | |
| <span data-ttu-id="165d9-152">Środkowe stany USA</span><span class="sxs-lookup"><span data-stu-id="165d9-152">Central US</span></span> | <span data-ttu-id="165d9-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="165d9-153">23.99.160.139</span></span> | <span data-ttu-id="165d9-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="165d9-154">13.67.215.62</span></span> |
| <span data-ttu-id="165d9-155">Azja Wschodnia</span><span class="sxs-lookup"><span data-stu-id="165d9-155">East Asia</span></span> | <span data-ttu-id="165d9-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="165d9-156">191.234.2.139</span></span> | <span data-ttu-id="165d9-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="165d9-157">52.175.33.150</span></span> |
| <span data-ttu-id="165d9-158">Wschodnie stany USA 1</span><span class="sxs-lookup"><span data-stu-id="165d9-158">East US 1</span></span> | <span data-ttu-id="165d9-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="165d9-159">191.238.6.43</span></span> | <span data-ttu-id="165d9-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="165d9-160">40.121.158.30</span></span> |
| <span data-ttu-id="165d9-161">Wschodnie stany USA 2</span><span class="sxs-lookup"><span data-stu-id="165d9-161">East US 2</span></span> | <span data-ttu-id="165d9-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="165d9-162">191.239.224.107</span></span> | <span data-ttu-id="165d9-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="165d9-163">40.79.84.180</span></span> |
| <span data-ttu-id="165d9-164">Indie Środkowe</span><span class="sxs-lookup"><span data-stu-id="165d9-164">India Central</span></span> | <span data-ttu-id="165d9-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="165d9-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="165d9-166">Indie Południowe</span><span class="sxs-lookup"><span data-stu-id="165d9-166">India South</span></span> | <span data-ttu-id="165d9-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="165d9-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="165d9-168">Indie Zachodnie</span><span class="sxs-lookup"><span data-stu-id="165d9-168">India West</span></span> | <span data-ttu-id="165d9-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="165d9-169">104.211.160.80</span></span> | |
| <span data-ttu-id="165d9-170">Japonia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="165d9-170">Japan East</span></span> | <span data-ttu-id="165d9-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="165d9-171">191.237.240.43</span></span> | <span data-ttu-id="165d9-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="165d9-172">13.78.61.196</span></span> |
| <span data-ttu-id="165d9-173">Japonia Zachodnia</span><span class="sxs-lookup"><span data-stu-id="165d9-173">Japan West</span></span> | <span data-ttu-id="165d9-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="165d9-174">191.238.68.11</span></span> | <span data-ttu-id="165d9-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="165d9-175">104.214.148.156</span></span> |
| <span data-ttu-id="165d9-176">Korea Środkowa</span><span class="sxs-lookup"><span data-stu-id="165d9-176">Korea Central</span></span> | <span data-ttu-id="165d9-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="165d9-177">52.231.32.42</span></span> | |
| <span data-ttu-id="165d9-178">Korea Południowa</span><span class="sxs-lookup"><span data-stu-id="165d9-178">Korea South</span></span> | <span data-ttu-id="165d9-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="165d9-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="165d9-180">Środkowo-północne stany USA</span><span class="sxs-lookup"><span data-stu-id="165d9-180">North Central US</span></span> | <span data-ttu-id="165d9-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="165d9-181">23.98.55.75</span></span> | <span data-ttu-id="165d9-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="165d9-182">23.96.178.199</span></span> |
| <span data-ttu-id="165d9-183">Europa Północna</span><span class="sxs-lookup"><span data-stu-id="165d9-183">North Europe</span></span> | <span data-ttu-id="165d9-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="165d9-184">191.235.193.75</span></span> | <span data-ttu-id="165d9-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="165d9-185">40.113.93.91</span></span> |
| <span data-ttu-id="165d9-186">Środkowo-południowe stany USA</span><span class="sxs-lookup"><span data-stu-id="165d9-186">South Central US</span></span> | <span data-ttu-id="165d9-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="165d9-187">23.98.162.75</span></span> | <span data-ttu-id="165d9-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="165d9-188">13.66.62.124</span></span> |
| <span data-ttu-id="165d9-189">Azja Południowo-Wschodnia</span><span class="sxs-lookup"><span data-stu-id="165d9-189">South East Asia</span></span> | <span data-ttu-id="165d9-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="165d9-190">23.100.117.95</span></span> | <span data-ttu-id="165d9-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="165d9-191">104.43.15.0</span></span> |
| <span data-ttu-id="165d9-192">Północne Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="165d9-192">UK North</span></span> | <span data-ttu-id="165d9-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="165d9-193">13.87.97.210</span></span> | |
| <span data-ttu-id="165d9-194">Wielka Brytania Południowa 1</span><span class="sxs-lookup"><span data-stu-id="165d9-194">UK South 1</span></span> | <span data-ttu-id="165d9-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="165d9-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="165d9-196">Południowe Zjednoczone Królestwo 2</span><span class="sxs-lookup"><span data-stu-id="165d9-196">UK South 2</span></span> | <span data-ttu-id="165d9-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="165d9-197">13.87.34.7</span></span> | |
| <span data-ttu-id="165d9-198">Zachodnie Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="165d9-198">UK West</span></span> | <span data-ttu-id="165d9-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="165d9-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="165d9-200">Środkowo-zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="165d9-200">West Central US</span></span> | <span data-ttu-id="165d9-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="165d9-201">13.78.145.25</span></span> | |
| <span data-ttu-id="165d9-202">Europa Zachodnia</span><span class="sxs-lookup"><span data-stu-id="165d9-202">West Europe</span></span> | <span data-ttu-id="165d9-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="165d9-203">191.237.232.75</span></span> | <span data-ttu-id="165d9-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="165d9-204">40.68.37.158</span></span> |
| <span data-ttu-id="165d9-205">Zachodnie stany USA 1</span><span class="sxs-lookup"><span data-stu-id="165d9-205">West US 1</span></span> | <span data-ttu-id="165d9-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="165d9-206">23.99.34.75</span></span> | <span data-ttu-id="165d9-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="165d9-207">104.42.238.205</span></span> |
| <span data-ttu-id="165d9-208">Zachodnie stany USA 2</span><span class="sxs-lookup"><span data-stu-id="165d9-208">West US 2</span></span> | <span data-ttu-id="165d9-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="165d9-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="165d9-210">Zmień zasady połączenia bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="165d9-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="165d9-211">Witaj toochange zasady połączenia bazy danych SQL Azure dla serwera bazy danych SQL Azure, użyj hello [interfejsu API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="165d9-211">toochange hello Azure SQL Database connection policy for an Azure SQL Database server, use hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="165d9-212">Jeśli zasady połączenia ustawiono zbyt**Proxy**, wszystkich sieci przepływu pakietów za pośrednictwem hello bramy bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="165d9-212">If your connection policy is set too**Proxy**, all network packets flow via hello Azure SQL Database gateway.</span></span> <span data-ttu-id="165d9-213">Dla tego ustawienia należy IP bramy tooallow wychodzących tooonly hello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="165d9-213">For this setting, you need tooallow outbound tooonly hello Azure SQL Database gateway IP.</span></span> <span data-ttu-id="165d9-214">Przy użyciu ustawienie **Proxy** ma opóźnienia więcej niż ustawienie **przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="165d9-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="165d9-215">Jeśli to ustawienie zasad połączenia **przekierowania**, wszystkich pakietów sieciowych bezpośrednio przepływ toohello proxy oprogramowania pośredniczącego.</span><span class="sxs-lookup"><span data-stu-id="165d9-215">If your connection policy is setting **Redirect**, all network packets flow directly toohello middleware proxy.</span></span> <span data-ttu-id="165d9-216">Dla tego ustawienia należy tooallow toomultiple wychodzących adresów IP.</span><span class="sxs-lookup"><span data-stu-id="165d9-216">For this setting, you need tooallow outbound toomultiple IPs.</span></span> 

## <a name="script-toochange-connection-settings"></a><span data-ttu-id="165d9-217">Ustawienia połączenia toochange skryptu</span><span class="sxs-lookup"><span data-stu-id="165d9-217">Script toochange connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="165d9-218">Ten skrypt wymaga hello [modułu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="165d9-218">This script requires hello [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="165d9-219">Witaj następującego skryptu programu PowerShell pokazuje, jak toochange hello zasad połączenia.</span><span class="sxs-lookup"><span data-stu-id="165d9-219">hello following PowerShell script shows how toochange hello connection policy.</span></span>

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="165d9-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="165d9-220">Next steps</span></span>

- <span data-ttu-id="165d9-221">Informacje dotyczące sposobu toochange hello zasady połączenia bazy danych SQL Azure dla serwera bazy danych SQL Azure znajdują się w temacie [Create lub zasada połączenia serwera aktualizacji przy użyciu hello interfejsu API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="165d9-221">For information on how toochange hello Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="165d9-222">Uzyskać informacji dotyczących zachowania połączenia bazy danych SQL Azure dla klientów używających ADO.NET 4.5 lub nowszej wersji, zobacz [porty inne niż 1433 dla ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="165d9-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="165d9-223">Informacje ogólne programowanie ogólne aplikacji, zobacz [Omówienie projektowania aplikacji bazy danych SQL](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="165d9-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
