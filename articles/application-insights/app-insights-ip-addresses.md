---
title: "Adresy IP używane przez usługę Application Insights | Dokumentacja firmy Microsoft"
description: "Wyjątki zapory serwera wymagane przez usługę Application Insights"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 8/11/2017
ms.author: bwren
ms.openlocfilehash: 3bb076c63223fc1567c6b7b25c1a513bbc81ed58
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="00833-103">Adresy IP używane przez usługę Application Insights</span><span class="sxs-lookup"><span data-stu-id="00833-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="00833-104">[Azure Application Insights](app-insights-overview.md) usługa używa liczba adresów IP.</span><span class="sxs-lookup"><span data-stu-id="00833-104">The [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="00833-105">Może być konieczne, jeśli aplikacja, która monitorowanych znajduje się za zaporą informacje tych adresów.</span><span class="sxs-lookup"><span data-stu-id="00833-105">You might need to know these addresses if the app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="00833-106">Mimo że te adresy są statyczne, istnieje możliwość, że musimy zmienić je od czasu do czasu.</span><span class="sxs-lookup"><span data-stu-id="00833-106">Although these addresses are static, it's possible that we will need to change them from time to time.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="00833-107">Porty wychodzące</span><span class="sxs-lookup"><span data-stu-id="00833-107">Outgoing ports</span></span>
<span data-ttu-id="00833-108">Należy otworzyć niektóre wychodzących porty zapory serwera umożliwia zestaw SDK usługi Application Insights lub Monitor stanu wysyłania danych do portalu:</span><span class="sxs-lookup"><span data-stu-id="00833-108">You need to open some outgoing ports in your server's firewall to allow the Application Insights SDK and/or Status Monitor to send data to the portal:</span></span>

| <span data-ttu-id="00833-109">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="00833-109">Purpose</span></span> | <span data-ttu-id="00833-110">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="00833-110">URL</span></span> | <span data-ttu-id="00833-111">Adres IP</span><span class="sxs-lookup"><span data-stu-id="00833-111">IP</span></span> | <span data-ttu-id="00833-112">Porty</span><span class="sxs-lookup"><span data-stu-id="00833-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00833-113">Telemetria</span><span class="sxs-lookup"><span data-stu-id="00833-113">Telemetry</span></span> |<span data-ttu-id="00833-114">DC.Services.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="00833-115">DC.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="00833-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="00833-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="00833-116">40.114.241.141</span></span><br/><span data-ttu-id="00833-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="00833-117">104.45.136.42</span></span><br/><span data-ttu-id="00833-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="00833-118">40.84.189.107</span></span><br/><span data-ttu-id="00833-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="00833-119">168.63.242.221</span></span><br/><span data-ttu-id="00833-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="00833-120">52.167.221.184</span></span><br/><span data-ttu-id="00833-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="00833-121">52.169.64.244</span></span> |<span data-ttu-id="00833-122">443</span><span class="sxs-lookup"><span data-stu-id="00833-122">443</span></span> |
| <span data-ttu-id="00833-123">Metryki strumień na żywo</span><span class="sxs-lookup"><span data-stu-id="00833-123">Live Metrics Stream</span></span> |<span data-ttu-id="00833-124">RT.Services.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="00833-125">RT.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="00833-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="00833-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="00833-126">23.96.28.38</span></span><br/><span data-ttu-id="00833-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="00833-127">13.92.40.198</span></span> |<span data-ttu-id="00833-128">443</span><span class="sxs-lookup"><span data-stu-id="00833-128">443</span></span> |
| <span data-ttu-id="00833-129">Wewnętrzny Telemetrii</span><span class="sxs-lookup"><span data-stu-id="00833-129">Internal Telemetry</span></span> |<span data-ttu-id="00833-130">BREEZE.aimon.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="00833-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="00833-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="00833-131">52.161.11.71</span></span> |<span data-ttu-id="00833-132">443</span><span class="sxs-lookup"><span data-stu-id="00833-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="00833-133">Monitor stanu</span><span class="sxs-lookup"><span data-stu-id="00833-133">Status Monitor</span></span>
<span data-ttu-id="00833-134">Stan monitora konfiguracji — potrzebne tylko podczas wprowadzania zmian.</span><span class="sxs-lookup"><span data-stu-id="00833-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="00833-135">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="00833-135">Purpose</span></span> | <span data-ttu-id="00833-136">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="00833-136">URL</span></span> | <span data-ttu-id="00833-137">Adres IP</span><span class="sxs-lookup"><span data-stu-id="00833-137">IP</span></span> | <span data-ttu-id="00833-138">Porty</span><span class="sxs-lookup"><span data-stu-id="00833-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00833-139">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="00833-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="00833-140">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="00833-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="00833-141">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="00833-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="00833-142">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="00833-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="00833-143">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="00833-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="00833-144">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="00833-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="00833-145">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="00833-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="00833-146">Instalacja</span><span class="sxs-lookup"><span data-stu-id="00833-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="00833-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="00833-147">HockeyApp</span></span>
| <span data-ttu-id="00833-148">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="00833-148">Purpose</span></span> | <span data-ttu-id="00833-149">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="00833-149">URL</span></span> | <span data-ttu-id="00833-150">Adres IP</span><span class="sxs-lookup"><span data-stu-id="00833-150">IP</span></span> | <span data-ttu-id="00833-151">Porty</span><span class="sxs-lookup"><span data-stu-id="00833-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00833-152">Dane dotyczące awarii</span><span class="sxs-lookup"><span data-stu-id="00833-152">Crash data</span></span> |<span data-ttu-id="00833-153">GATE.hockeyapp.NET</span><span class="sxs-lookup"><span data-stu-id="00833-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="00833-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="00833-154">104.45.136.42</span></span> |<span data-ttu-id="00833-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="00833-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="00833-156">Testy dostępności</span><span class="sxs-lookup"><span data-stu-id="00833-156">Availability tests</span></span>
<span data-ttu-id="00833-157">Jest to lista adresów, z którego [testów sieci web dostępności](app-insights-monitor-web-app-availability.md) są uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="00833-157">This is the list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="00833-158">Jeśli chcesz uruchamiać testy sieci web w aplikacji, ale serwer sieci web jest ograniczone do określonych klientów obsługujących, będzie mieć umożliwić ruch przychodzący z naszych dostępności serwerów testu.</span><span class="sxs-lookup"><span data-stu-id="00833-158">If you want to run web tests on your app, but your web server is restricted to serving specific clients, then you will have to permit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="00833-159">Otwórz porty 80 (http) i 443 (https) dla ruchu przychodzącego z tych adresów (adresy IP są grupowane według lokalizacji):</span><span class="sxs-lookup"><span data-stu-id="00833-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a><span data-ttu-id="00833-160">Interfejs API dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="00833-160">Data access API</span></span>
| <span data-ttu-id="00833-161">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="00833-161">Purpose</span></span> | <span data-ttu-id="00833-162">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="00833-162">URI</span></span> | <span data-ttu-id="00833-163">Adres IP</span><span class="sxs-lookup"><span data-stu-id="00833-163">IP</span></span> | <span data-ttu-id="00833-164">Porty</span><span class="sxs-lookup"><span data-stu-id="00833-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00833-165">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="00833-165">API</span></span> |<span data-ttu-id="00833-166">API.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="00833-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="00833-167">api1.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="00833-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="00833-168">api2.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="00833-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="00833-169">api3.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="00833-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="00833-170">api4.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="00833-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="00833-171">api5.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="00833-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="00833-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="00833-172">13.82.26.252</span></span><br/><span data-ttu-id="00833-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="00833-173">40.76.213.73</span></span> |<span data-ttu-id="00833-174">80,443</span><span class="sxs-lookup"><span data-stu-id="00833-174">80,443</span></span> |
| <span data-ttu-id="00833-175">Dokumentacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="00833-175">API docs</span></span> |<span data-ttu-id="00833-176">dev.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="00833-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="00833-177">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="00833-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="00833-178">dev.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="00833-179">www.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="00833-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="00833-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="00833-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="00833-181">www.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="00833-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="00833-182">13.82.24.149</span></span><br/><span data-ttu-id="00833-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="00833-183">40.114.82.10</span></span> |<span data-ttu-id="00833-184">80,443</span><span class="sxs-lookup"><span data-stu-id="00833-184">80,443</span></span> |
| <span data-ttu-id="00833-185">Wewnętrzny interfejsu API</span><span class="sxs-lookup"><span data-stu-id="00833-185">Internal API</span></span> |<span data-ttu-id="00833-186">aigs.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="00833-187">aigs1.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="00833-188">aigs2.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="00833-189">aigs3.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="00833-190">aigs4.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="00833-191">aigs5.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="00833-192">aigs6.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="00833-193">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-193">dynamic</span></span>|<span data-ttu-id="00833-194">443</span><span class="sxs-lookup"><span data-stu-id="00833-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="00833-195">Application Insights analityka</span><span class="sxs-lookup"><span data-stu-id="00833-195">Application Insights Analytics</span></span>

| <span data-ttu-id="00833-196">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="00833-196">Purpose</span></span> | <span data-ttu-id="00833-197">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="00833-197">URI</span></span> | <span data-ttu-id="00833-198">Adres IP</span><span class="sxs-lookup"><span data-stu-id="00833-198">IP</span></span> | <span data-ttu-id="00833-199">Porty</span><span class="sxs-lookup"><span data-stu-id="00833-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00833-200">Portal analityka</span><span class="sxs-lookup"><span data-stu-id="00833-200">Analytics Portal</span></span> | <span data-ttu-id="00833-201">Analytics.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="00833-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="00833-202">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-202">dynamic</span></span> | <span data-ttu-id="00833-203">80,443</span><span class="sxs-lookup"><span data-stu-id="00833-203">80,443</span></span> |
| <span data-ttu-id="00833-204">CDN</span><span class="sxs-lookup"><span data-stu-id="00833-204">CDN</span></span> | <span data-ttu-id="00833-205">applicationanalytics.azureedge.NET</span><span class="sxs-lookup"><span data-stu-id="00833-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="00833-206">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-206">dynamic</span></span> | <span data-ttu-id="00833-207">80,443</span><span class="sxs-lookup"><span data-stu-id="00833-207">80,443</span></span> |
| <span data-ttu-id="00833-208">Nośnik CDN</span><span class="sxs-lookup"><span data-stu-id="00833-208">Media CDN</span></span> | <span data-ttu-id="00833-209">applicationanalyticsmedia.azureedge.NET</span><span class="sxs-lookup"><span data-stu-id="00833-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="00833-210">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-210">dynamic</span></span> | <span data-ttu-id="00833-211">80,443</span><span class="sxs-lookup"><span data-stu-id="00833-211">80,443</span></span> |

<span data-ttu-id="00833-212">Uwaga: *. applicationinsights.io domeny należy do zespołu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="00833-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="00833-213">Usługa Application Insights rozszerzenie portalu Azure</span><span class="sxs-lookup"><span data-stu-id="00833-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="00833-214">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="00833-214">Purpose</span></span> | <span data-ttu-id="00833-215">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="00833-215">URI</span></span> | <span data-ttu-id="00833-216">Adres IP</span><span class="sxs-lookup"><span data-stu-id="00833-216">IP</span></span> | <span data-ttu-id="00833-217">Porty</span><span class="sxs-lookup"><span data-stu-id="00833-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00833-218">Rozszerzenie usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="00833-218">Application Insights Extension</span></span> | <span data-ttu-id="00833-219">stamp2.App.insightsportal.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="00833-220">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-220">dynamic</span></span> | <span data-ttu-id="00833-221">80,443</span><span class="sxs-lookup"><span data-stu-id="00833-221">80,443</span></span> |
| <span data-ttu-id="00833-222">Rozszerzenie usługi Application Insights CDN</span><span class="sxs-lookup"><span data-stu-id="00833-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="00833-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="00833-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="00833-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="00833-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="00833-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="00833-226">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-226">dynamic</span></span> | <span data-ttu-id="00833-227">80,443</span><span class="sxs-lookup"><span data-stu-id="00833-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="00833-228">Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="00833-228">Application Insights SDKs</span></span>

| <span data-ttu-id="00833-229">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="00833-229">Purpose</span></span> | <span data-ttu-id="00833-230">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="00833-230">URI</span></span> | <span data-ttu-id="00833-231">Adres IP</span><span class="sxs-lookup"><span data-stu-id="00833-231">IP</span></span> | <span data-ttu-id="00833-232">Porty</span><span class="sxs-lookup"><span data-stu-id="00833-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00833-233">Zestaw SDK aplikacji Insights JS CDN</span><span class="sxs-lookup"><span data-stu-id="00833-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="00833-234">az416426.Vo.msecnd.NET</span><span class="sxs-lookup"><span data-stu-id="00833-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="00833-235">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-235">dynamic</span></span> | <span data-ttu-id="00833-236">80,443</span><span class="sxs-lookup"><span data-stu-id="00833-236">80,443</span></span> |
| <span data-ttu-id="00833-237">Application Insights Java SDK</span><span class="sxs-lookup"><span data-stu-id="00833-237">Application Insights Java SDK</span></span> | <span data-ttu-id="00833-238">aijavasdk.blob.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="00833-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="00833-239">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-239">dynamic</span></span> | <span data-ttu-id="00833-240">80,443</span><span class="sxs-lookup"><span data-stu-id="00833-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="00833-241">Profiler</span><span class="sxs-lookup"><span data-stu-id="00833-241">Profiler</span></span>

| <span data-ttu-id="00833-242">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="00833-242">Purpose</span></span> | <span data-ttu-id="00833-243">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="00833-243">URI</span></span> | <span data-ttu-id="00833-244">Adres IP</span><span class="sxs-lookup"><span data-stu-id="00833-244">IP</span></span> | <span data-ttu-id="00833-245">Porty</span><span class="sxs-lookup"><span data-stu-id="00833-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00833-246">Agent</span><span class="sxs-lookup"><span data-stu-id="00833-246">Agent</span></span> | <span data-ttu-id="00833-247">Agent.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="00833-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="00833-248">*. agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="00833-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="00833-249">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-249">dynamic</span></span> | <span data-ttu-id="00833-250">443</span><span class="sxs-lookup"><span data-stu-id="00833-250">443</span></span>
| <span data-ttu-id="00833-251">Portal</span><span class="sxs-lookup"><span data-stu-id="00833-251">Portal</span></span> | <span data-ttu-id="00833-252">Gateway.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="00833-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="00833-253">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-253">dynamic</span></span> | <span data-ttu-id="00833-254">443</span><span class="sxs-lookup"><span data-stu-id="00833-254">443</span></span>
| <span data-ttu-id="00833-255">Magazyn</span><span class="sxs-lookup"><span data-stu-id="00833-255">Storage</span></span> | <span data-ttu-id="00833-256">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="00833-256">*.core.windows.net</span></span> | <span data-ttu-id="00833-257">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-257">dynamic</span></span> | <span data-ttu-id="00833-258">443</span><span class="sxs-lookup"><span data-stu-id="00833-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="00833-259">Debuger migawek</span><span class="sxs-lookup"><span data-stu-id="00833-259">Snapshot Debugger</span></span>

| <span data-ttu-id="00833-260">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="00833-260">Purpose</span></span> | <span data-ttu-id="00833-261">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="00833-261">URI</span></span> | <span data-ttu-id="00833-262">Adres IP</span><span class="sxs-lookup"><span data-stu-id="00833-262">IP</span></span> | <span data-ttu-id="00833-263">Porty</span><span class="sxs-lookup"><span data-stu-id="00833-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00833-264">Agent</span><span class="sxs-lookup"><span data-stu-id="00833-264">Agent</span></span> | <span data-ttu-id="00833-265">PPE.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="00833-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="00833-266">*. ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="00833-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="00833-267">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-267">dynamic</span></span> | <span data-ttu-id="00833-268">443</span><span class="sxs-lookup"><span data-stu-id="00833-268">443</span></span>
| <span data-ttu-id="00833-269">Portal</span><span class="sxs-lookup"><span data-stu-id="00833-269">Portal</span></span> | <span data-ttu-id="00833-270">PPE.Gateway.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="00833-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="00833-271">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-271">dynamic</span></span> | <span data-ttu-id="00833-272">443</span><span class="sxs-lookup"><span data-stu-id="00833-272">443</span></span>
| <span data-ttu-id="00833-273">Magazyn</span><span class="sxs-lookup"><span data-stu-id="00833-273">Storage</span></span> | <span data-ttu-id="00833-274">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="00833-274">*.core.windows.net</span></span> | <span data-ttu-id="00833-275">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="00833-275">dynamic</span></span> | <span data-ttu-id="00833-276">443</span><span class="sxs-lookup"><span data-stu-id="00833-276">443</span></span>
