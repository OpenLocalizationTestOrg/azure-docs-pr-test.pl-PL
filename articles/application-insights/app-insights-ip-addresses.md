---
title: "adresy aaaIP używane przez usługi Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 2c101b8da2ba9594fbff607f4f7551cda80c3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="b2639-103">Adresy IP używane przez usługę Application Insights</span><span class="sxs-lookup"><span data-stu-id="b2639-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="b2639-104">Witaj [Azure Application Insights](app-insights-overview.md) usługa używa liczba adresów IP.</span><span class="sxs-lookup"><span data-stu-id="b2639-104">hello [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="b2639-105">Może być potrzebny tooknow te adresy są monitorowania aplikacji hello znajduje się za zaporą.</span><span class="sxs-lookup"><span data-stu-id="b2639-105">You might need tooknow these addresses if hello app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="b2639-106">Mimo że te adresy są statyczne, jest to możliwe, że są wymagane toochange je z tootime czasu.</span><span class="sxs-lookup"><span data-stu-id="b2639-106">Although these addresses are static, it's possible that we will need toochange them from time tootime.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="b2639-107">Porty wychodzące</span><span class="sxs-lookup"><span data-stu-id="b2639-107">Outgoing ports</span></span>
<span data-ttu-id="b2639-108">Należy tooopen niektórych portów wychodzących w hello tooallow zapory serwera zestawu SDK usługi Application Insights i/lub Monitor stanu toosend danych toohello portalu:</span><span class="sxs-lookup"><span data-stu-id="b2639-108">You need tooopen some outgoing ports in your server's firewall tooallow hello Application Insights SDK and/or Status Monitor toosend data toohello portal:</span></span>

| <span data-ttu-id="b2639-109">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="b2639-109">Purpose</span></span> | <span data-ttu-id="b2639-110">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="b2639-110">URL</span></span> | <span data-ttu-id="b2639-111">Adres IP</span><span class="sxs-lookup"><span data-stu-id="b2639-111">IP</span></span> | <span data-ttu-id="b2639-112">Porty</span><span class="sxs-lookup"><span data-stu-id="b2639-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2639-113">Telemetria</span><span class="sxs-lookup"><span data-stu-id="b2639-113">Telemetry</span></span> |<span data-ttu-id="b2639-114">DC.Services.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="b2639-115">DC.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="b2639-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="b2639-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="b2639-116">40.114.241.141</span></span><br/><span data-ttu-id="b2639-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="b2639-117">104.45.136.42</span></span><br/><span data-ttu-id="b2639-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="b2639-118">40.84.189.107</span></span><br/><span data-ttu-id="b2639-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="b2639-119">168.63.242.221</span></span><br/><span data-ttu-id="b2639-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="b2639-120">52.167.221.184</span></span><br/><span data-ttu-id="b2639-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="b2639-121">52.169.64.244</span></span> |<span data-ttu-id="b2639-122">443</span><span class="sxs-lookup"><span data-stu-id="b2639-122">443</span></span> |
| <span data-ttu-id="b2639-123">Metryki strumień na żywo</span><span class="sxs-lookup"><span data-stu-id="b2639-123">Live Metrics Stream</span></span> |<span data-ttu-id="b2639-124">RT.Services.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="b2639-125">RT.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="b2639-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="b2639-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="b2639-126">23.96.28.38</span></span><br/><span data-ttu-id="b2639-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="b2639-127">13.92.40.198</span></span> |<span data-ttu-id="b2639-128">443</span><span class="sxs-lookup"><span data-stu-id="b2639-128">443</span></span> |
| <span data-ttu-id="b2639-129">Wewnętrzny Telemetrii</span><span class="sxs-lookup"><span data-stu-id="b2639-129">Internal Telemetry</span></span> |<span data-ttu-id="b2639-130">BREEZE.aimon.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="b2639-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="b2639-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="b2639-131">52.161.11.71</span></span> |<span data-ttu-id="b2639-132">443</span><span class="sxs-lookup"><span data-stu-id="b2639-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="b2639-133">Monitor stanu</span><span class="sxs-lookup"><span data-stu-id="b2639-133">Status Monitor</span></span>
<span data-ttu-id="b2639-134">Stan monitora konfiguracji — potrzebne tylko podczas wprowadzania zmian.</span><span class="sxs-lookup"><span data-stu-id="b2639-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="b2639-135">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="b2639-135">Purpose</span></span> | <span data-ttu-id="b2639-136">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="b2639-136">URL</span></span> | <span data-ttu-id="b2639-137">Adres IP</span><span class="sxs-lookup"><span data-stu-id="b2639-137">IP</span></span> | <span data-ttu-id="b2639-138">Porty</span><span class="sxs-lookup"><span data-stu-id="b2639-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2639-139">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="b2639-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="b2639-140">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="b2639-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="b2639-141">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="b2639-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="b2639-142">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="b2639-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="b2639-143">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="b2639-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="b2639-144">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="b2639-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="b2639-145">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="b2639-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="b2639-146">Instalacja</span><span class="sxs-lookup"><span data-stu-id="b2639-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="b2639-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="b2639-147">HockeyApp</span></span>
| <span data-ttu-id="b2639-148">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="b2639-148">Purpose</span></span> | <span data-ttu-id="b2639-149">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="b2639-149">URL</span></span> | <span data-ttu-id="b2639-150">Adres IP</span><span class="sxs-lookup"><span data-stu-id="b2639-150">IP</span></span> | <span data-ttu-id="b2639-151">Porty</span><span class="sxs-lookup"><span data-stu-id="b2639-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2639-152">Dane dotyczące awarii</span><span class="sxs-lookup"><span data-stu-id="b2639-152">Crash data</span></span> |<span data-ttu-id="b2639-153">GATE.hockeyapp.NET</span><span class="sxs-lookup"><span data-stu-id="b2639-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="b2639-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="b2639-154">104.45.136.42</span></span> |<span data-ttu-id="b2639-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="b2639-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="b2639-156">Testy dostępności</span><span class="sxs-lookup"><span data-stu-id="b2639-156">Availability tests</span></span>
<span data-ttu-id="b2639-157">To jest lista hello adresów, z którego [testów sieci web dostępności](app-insights-monitor-web-app-availability.md) są uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="b2639-157">This is hello list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="b2639-158">Jeśli chcesz toorun testy sieci web w aplikacji, ale serwer sieci web jest ograniczone tooserving określonych klientów, konieczne będzie toopermit ruch przychodzący z naszych serwerów testu dostępności, a następnie.</span><span class="sxs-lookup"><span data-stu-id="b2639-158">If you want toorun web tests on your app, but your web server is restricted tooserving specific clients, then you will have toopermit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="b2639-159">Otwórz porty 80 (http) i 443 (https) dla ruchu przychodzącego z tych adresów (adresy IP są grupowane według lokalizacji):</span><span class="sxs-lookup"><span data-stu-id="b2639-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

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

## <a name="data-access-api"></a><span data-ttu-id="b2639-160">Interfejs API dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="b2639-160">Data access API</span></span>
| <span data-ttu-id="b2639-161">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="b2639-161">Purpose</span></span> | <span data-ttu-id="b2639-162">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="b2639-162">URI</span></span> | <span data-ttu-id="b2639-163">Adres IP</span><span class="sxs-lookup"><span data-stu-id="b2639-163">IP</span></span> | <span data-ttu-id="b2639-164">Porty</span><span class="sxs-lookup"><span data-stu-id="b2639-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2639-165">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="b2639-165">API</span></span> |<span data-ttu-id="b2639-166">API.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="b2639-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="b2639-167">api1.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="b2639-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="b2639-168">api2.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="b2639-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="b2639-169">api3.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="b2639-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="b2639-170">api4.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="b2639-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="b2639-171">api5.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="b2639-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="b2639-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="b2639-172">13.82.26.252</span></span><br/><span data-ttu-id="b2639-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="b2639-173">40.76.213.73</span></span> |<span data-ttu-id="b2639-174">80,443</span><span class="sxs-lookup"><span data-stu-id="b2639-174">80,443</span></span> |
| <span data-ttu-id="b2639-175">Dokumentacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="b2639-175">API docs</span></span> |<span data-ttu-id="b2639-176">dev.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="b2639-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="b2639-177">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="b2639-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="b2639-178">dev.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="b2639-179">www.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="b2639-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="b2639-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="b2639-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="b2639-181">www.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="b2639-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="b2639-182">13.82.24.149</span></span><br/><span data-ttu-id="b2639-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="b2639-183">40.114.82.10</span></span> |<span data-ttu-id="b2639-184">80,443</span><span class="sxs-lookup"><span data-stu-id="b2639-184">80,443</span></span> |
| <span data-ttu-id="b2639-185">Wewnętrzny interfejsu API</span><span class="sxs-lookup"><span data-stu-id="b2639-185">Internal API</span></span> |<span data-ttu-id="b2639-186">aigs.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="b2639-187">aigs1.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="b2639-188">aigs2.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="b2639-189">aigs3.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="b2639-190">aigs4.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="b2639-191">aigs5.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="b2639-192">aigs6.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="b2639-193">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-193">dynamic</span></span>|<span data-ttu-id="b2639-194">443</span><span class="sxs-lookup"><span data-stu-id="b2639-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="b2639-195">Application Insights analityka</span><span class="sxs-lookup"><span data-stu-id="b2639-195">Application Insights Analytics</span></span>

| <span data-ttu-id="b2639-196">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="b2639-196">Purpose</span></span> | <span data-ttu-id="b2639-197">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="b2639-197">URI</span></span> | <span data-ttu-id="b2639-198">Adres IP</span><span class="sxs-lookup"><span data-stu-id="b2639-198">IP</span></span> | <span data-ttu-id="b2639-199">Porty</span><span class="sxs-lookup"><span data-stu-id="b2639-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2639-200">Portal analityka</span><span class="sxs-lookup"><span data-stu-id="b2639-200">Analytics Portal</span></span> | <span data-ttu-id="b2639-201">Analytics.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="b2639-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="b2639-202">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-202">dynamic</span></span> | <span data-ttu-id="b2639-203">80,443</span><span class="sxs-lookup"><span data-stu-id="b2639-203">80,443</span></span> |
| <span data-ttu-id="b2639-204">CDN</span><span class="sxs-lookup"><span data-stu-id="b2639-204">CDN</span></span> | <span data-ttu-id="b2639-205">applicationanalytics.azureedge.NET</span><span class="sxs-lookup"><span data-stu-id="b2639-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="b2639-206">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-206">dynamic</span></span> | <span data-ttu-id="b2639-207">80,443</span><span class="sxs-lookup"><span data-stu-id="b2639-207">80,443</span></span> |
| <span data-ttu-id="b2639-208">Nośnik CDN</span><span class="sxs-lookup"><span data-stu-id="b2639-208">Media CDN</span></span> | <span data-ttu-id="b2639-209">applicationanalyticsmedia.azureedge.NET</span><span class="sxs-lookup"><span data-stu-id="b2639-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="b2639-210">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-210">dynamic</span></span> | <span data-ttu-id="b2639-211">80,443</span><span class="sxs-lookup"><span data-stu-id="b2639-211">80,443</span></span> |

<span data-ttu-id="b2639-212">Uwaga: *. applicationinsights.io domeny należy do zespołu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b2639-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="b2639-213">Usługa Application Insights rozszerzenie portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b2639-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="b2639-214">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="b2639-214">Purpose</span></span> | <span data-ttu-id="b2639-215">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="b2639-215">URI</span></span> | <span data-ttu-id="b2639-216">Adres IP</span><span class="sxs-lookup"><span data-stu-id="b2639-216">IP</span></span> | <span data-ttu-id="b2639-217">Porty</span><span class="sxs-lookup"><span data-stu-id="b2639-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2639-218">Rozszerzenie usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="b2639-218">Application Insights Extension</span></span> | <span data-ttu-id="b2639-219">stamp2.App.insightsportal.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="b2639-220">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-220">dynamic</span></span> | <span data-ttu-id="b2639-221">80,443</span><span class="sxs-lookup"><span data-stu-id="b2639-221">80,443</span></span> |
| <span data-ttu-id="b2639-222">Rozszerzenie usługi Application Insights CDN</span><span class="sxs-lookup"><span data-stu-id="b2639-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="b2639-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="b2639-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="b2639-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="b2639-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="b2639-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="b2639-226">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-226">dynamic</span></span> | <span data-ttu-id="b2639-227">80,443</span><span class="sxs-lookup"><span data-stu-id="b2639-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="b2639-228">Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="b2639-228">Application Insights SDKs</span></span>

| <span data-ttu-id="b2639-229">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="b2639-229">Purpose</span></span> | <span data-ttu-id="b2639-230">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="b2639-230">URI</span></span> | <span data-ttu-id="b2639-231">Adres IP</span><span class="sxs-lookup"><span data-stu-id="b2639-231">IP</span></span> | <span data-ttu-id="b2639-232">Porty</span><span class="sxs-lookup"><span data-stu-id="b2639-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2639-233">Zestaw SDK aplikacji Insights JS CDN</span><span class="sxs-lookup"><span data-stu-id="b2639-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="b2639-234">az416426.Vo.msecnd.NET</span><span class="sxs-lookup"><span data-stu-id="b2639-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="b2639-235">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-235">dynamic</span></span> | <span data-ttu-id="b2639-236">80,443</span><span class="sxs-lookup"><span data-stu-id="b2639-236">80,443</span></span> |
| <span data-ttu-id="b2639-237">Application Insights Java SDK</span><span class="sxs-lookup"><span data-stu-id="b2639-237">Application Insights Java SDK</span></span> | <span data-ttu-id="b2639-238">aijavasdk.blob.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="b2639-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="b2639-239">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-239">dynamic</span></span> | <span data-ttu-id="b2639-240">80,443</span><span class="sxs-lookup"><span data-stu-id="b2639-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="b2639-241">Profiler</span><span class="sxs-lookup"><span data-stu-id="b2639-241">Profiler</span></span>

| <span data-ttu-id="b2639-242">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="b2639-242">Purpose</span></span> | <span data-ttu-id="b2639-243">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="b2639-243">URI</span></span> | <span data-ttu-id="b2639-244">Adres IP</span><span class="sxs-lookup"><span data-stu-id="b2639-244">IP</span></span> | <span data-ttu-id="b2639-245">Porty</span><span class="sxs-lookup"><span data-stu-id="b2639-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2639-246">Agent</span><span class="sxs-lookup"><span data-stu-id="b2639-246">Agent</span></span> | <span data-ttu-id="b2639-247">Agent.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="b2639-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="b2639-248">*. agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="b2639-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="b2639-249">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-249">dynamic</span></span> | <span data-ttu-id="b2639-250">443</span><span class="sxs-lookup"><span data-stu-id="b2639-250">443</span></span>
| <span data-ttu-id="b2639-251">Portal</span><span class="sxs-lookup"><span data-stu-id="b2639-251">Portal</span></span> | <span data-ttu-id="b2639-252">Gateway.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="b2639-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="b2639-253">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-253">dynamic</span></span> | <span data-ttu-id="b2639-254">443</span><span class="sxs-lookup"><span data-stu-id="b2639-254">443</span></span>
| <span data-ttu-id="b2639-255">Magazyn</span><span class="sxs-lookup"><span data-stu-id="b2639-255">Storage</span></span> | <span data-ttu-id="b2639-256">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="b2639-256">*.core.windows.net</span></span> | <span data-ttu-id="b2639-257">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-257">dynamic</span></span> | <span data-ttu-id="b2639-258">443</span><span class="sxs-lookup"><span data-stu-id="b2639-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="b2639-259">Debuger migawek</span><span class="sxs-lookup"><span data-stu-id="b2639-259">Snapshot Debugger</span></span>

| <span data-ttu-id="b2639-260">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="b2639-260">Purpose</span></span> | <span data-ttu-id="b2639-261">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="b2639-261">URI</span></span> | <span data-ttu-id="b2639-262">Adres IP</span><span class="sxs-lookup"><span data-stu-id="b2639-262">IP</span></span> | <span data-ttu-id="b2639-263">Porty</span><span class="sxs-lookup"><span data-stu-id="b2639-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2639-264">Agent</span><span class="sxs-lookup"><span data-stu-id="b2639-264">Agent</span></span> | <span data-ttu-id="b2639-265">PPE.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="b2639-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="b2639-266">*. ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="b2639-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="b2639-267">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-267">dynamic</span></span> | <span data-ttu-id="b2639-268">443</span><span class="sxs-lookup"><span data-stu-id="b2639-268">443</span></span>
| <span data-ttu-id="b2639-269">Portal</span><span class="sxs-lookup"><span data-stu-id="b2639-269">Portal</span></span> | <span data-ttu-id="b2639-270">PPE.Gateway.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="b2639-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="b2639-271">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-271">dynamic</span></span> | <span data-ttu-id="b2639-272">443</span><span class="sxs-lookup"><span data-stu-id="b2639-272">443</span></span>
| <span data-ttu-id="b2639-273">Magazyn</span><span class="sxs-lookup"><span data-stu-id="b2639-273">Storage</span></span> | <span data-ttu-id="b2639-274">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="b2639-274">*.core.windows.net</span></span> | <span data-ttu-id="b2639-275">dynamiczne</span><span class="sxs-lookup"><span data-stu-id="b2639-275">dynamic</span></span> | <span data-ttu-id="b2639-276">443</span><span class="sxs-lookup"><span data-stu-id="b2639-276">443</span></span>
