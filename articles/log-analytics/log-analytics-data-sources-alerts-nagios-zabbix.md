---
title: alerty Nagios i Zabbix aaaCollect w OMS Log Analytics | Dokumentacja firmy Microsoft
description: "Nagios i Zabbix są typu open source, narzędzia do monitorowania. Można zebrać alertów z tych narzędzi do analizy dzienników w kolejności tooanalyze je wraz z alertów z innych źródeł.  W tym artykule opisano, jak tooconfigure hello Agent pakietu OMS dla systemu Linux toocollect alerty z tych systemów."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="854fe-105">Zbieraj alerty z Nagios i Zabbix w Log Analytics z usługą OMS agenta dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="854fe-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="854fe-106">[Nagios](https://www.nagios.org/) i [Zabbix](http://www.zabbix.com/) są typu open source, narzędzia do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="854fe-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="854fe-107">Można zebrać alertów z tych narzędzi do analizy dzienników w kolejności tooanalyze je wraz z [alertów z innych źródeł](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="854fe-107">You can collect alerts from these tools into Log Analytics in order tooanalyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="854fe-108">W tym artykule opisano, jak tooconfigure hello Agent pakietu OMS dla systemu Linux toocollect alerty z tych systemów.</span><span class="sxs-lookup"><span data-stu-id="854fe-108">This article describes how tooconfigure hello OMS Agent for Linux toocollect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="854fe-109">Konfigurowanie zbierania alertów</span><span class="sxs-lookup"><span data-stu-id="854fe-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="854fe-110">Konfigurowanie zbierania alertów Nagios</span><span class="sxs-lookup"><span data-stu-id="854fe-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="854fe-111">Wykonaj następujące kroki na alerty toocollect serwera Nagios hello hello.</span><span class="sxs-lookup"><span data-stu-id="854fe-111">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="854fe-112">Udziel hello użytkownika **omsagent** pliku dziennika Nagios toohello dostęp do odczytu (tj. `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="854fe-112">Grant hello user **omsagent** read access toohello Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="854fe-113">Zakładając, że plik nagios.log hello jest własnością grupy hello `nagios`, można dodać użytkownika hello **omsagent** toohello **nagios** grupy.</span><span class="sxs-lookup"><span data-stu-id="854fe-113">Assuming hello nagios.log file is owned by hello group `nagios`, you can add hello user **omsagent** toohello **nagios** group.</span></span> 

    <span data-ttu-id="854fe-114">sudo usermod - -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="854fe-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="854fe-115">Modyfikowanie pliku konfiguracji hello w (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="854fe-115">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="854fe-116">Upewnij się, że hello następujące wpisy są obecne i nie komentarze wychodzących:</span><span class="sxs-lookup"><span data-stu-id="854fe-116">Ensure hello following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="854fe-117">Uruchom ponownie demon omsagent hello</span><span class="sxs-lookup"><span data-stu-id="854fe-117">Restart hello omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="854fe-118">Konfigurowanie zbierania alertów Zabbix</span><span class="sxs-lookup"><span data-stu-id="854fe-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="854fe-119">toocollect alertów z serwera Zabbix, należy toospecify użytkownika i hasło w *zwykły tekst*.</span><span class="sxs-lookup"><span data-stu-id="854fe-119">toocollect alerts from a Zabbix server, you need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="854fe-120">Nie jest to idealne rozwiązanie, ale zaleca się utworzenie użytkownika hello i przyznać uprawnienia toomonitor onlu.</span><span class="sxs-lookup"><span data-stu-id="854fe-120">This is not ideal, but we recommend that you create hello user and grant permissions toomonitor onlu.</span></span>

<span data-ttu-id="854fe-121">Wykonaj następujące kroki na alerty toocollect serwera Nagios hello hello.</span><span class="sxs-lookup"><span data-stu-id="854fe-121">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="854fe-122">Modyfikowanie pliku konfiguracji hello w (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="854fe-122">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="854fe-123">Upewnij się, że hello następujące wpisy są obecne i nie komentarze wychodzących.  Zmień hello toovalues nazwę i hasło użytkownika w danym środowisku Zabbix.</span><span class="sxs-lookup"><span data-stu-id="854fe-123">Ensure hello following entries are present and not commented out.  Change hello user name and password toovalues for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="854fe-124">Uruchom ponownie demon omsagent hello</span><span class="sxs-lookup"><span data-stu-id="854fe-124">Restart hello omsagent daemon</span></span>

    <span data-ttu-id="854fe-125">sudo sh /opt/microsoft/omsagent/bin/service_control ponownego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="854fe-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="854fe-126">Rejestruje alertu</span><span class="sxs-lookup"><span data-stu-id="854fe-126">Alert records</span></span>
<span data-ttu-id="854fe-127">Rejestruje alertu można pobrać z Nagios i Zabbix przy użyciu [dziennika wyszukiwania](log-analytics-log-searches.md) w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="854fe-127">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="854fe-128">Rejestruje Nagios Alert</span><span class="sxs-lookup"><span data-stu-id="854fe-128">Nagios Alert records</span></span>

<span data-ttu-id="854fe-129">Alert ma rekordy zebrane przez Nagios **typu** z **alertu** i **SourceSystem** z **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="854fe-129">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="854fe-130">Mają one właściwości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="854fe-130">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="854fe-131">Właściwość</span><span class="sxs-lookup"><span data-stu-id="854fe-131">Property</span></span> | <span data-ttu-id="854fe-132">Opis</span><span class="sxs-lookup"><span data-stu-id="854fe-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="854fe-133">Typ</span><span class="sxs-lookup"><span data-stu-id="854fe-133">Type</span></span> |<span data-ttu-id="854fe-134">*Alert*</span><span class="sxs-lookup"><span data-stu-id="854fe-134">*Alert*</span></span> |
| <span data-ttu-id="854fe-135">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="854fe-135">SourceSystem</span></span> |<span data-ttu-id="854fe-136">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="854fe-136">*Nagios*</span></span> |
| <span data-ttu-id="854fe-137">AlertName</span><span class="sxs-lookup"><span data-stu-id="854fe-137">AlertName</span></span> |<span data-ttu-id="854fe-138">Nazwa alertu hello.</span><span class="sxs-lookup"><span data-stu-id="854fe-138">Name of hello alert.</span></span> |
| <span data-ttu-id="854fe-139">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="854fe-139">AlertDescription</span></span> | <span data-ttu-id="854fe-140">Opis alertu hello.</span><span class="sxs-lookup"><span data-stu-id="854fe-140">Description of hello alert.</span></span> |
| <span data-ttu-id="854fe-141">Stan alertu</span><span class="sxs-lookup"><span data-stu-id="854fe-141">AlertState</span></span> | <span data-ttu-id="854fe-142">Stan usługi hello lub hosta.</span><span class="sxs-lookup"><span data-stu-id="854fe-142">Status of hello service or host.</span></span><br><br><span data-ttu-id="854fe-143">OK</span><span class="sxs-lookup"><span data-stu-id="854fe-143">OK</span></span><br><span data-ttu-id="854fe-144">OSTRZEŻENIE</span><span class="sxs-lookup"><span data-stu-id="854fe-144">WARNING</span></span><br><span data-ttu-id="854fe-145">W GÓRĘ</span><span class="sxs-lookup"><span data-stu-id="854fe-145">UP</span></span><br><span data-ttu-id="854fe-146">W DÓŁ</span><span class="sxs-lookup"><span data-stu-id="854fe-146">DOWN</span></span> |
| <span data-ttu-id="854fe-147">Nazwa hosta</span><span class="sxs-lookup"><span data-stu-id="854fe-147">HostName</span></span> | <span data-ttu-id="854fe-148">Nazwa hosta hello, utworzony hello alert.</span><span class="sxs-lookup"><span data-stu-id="854fe-148">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="854fe-149">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="854fe-149">PriorityNumber</span></span> | <span data-ttu-id="854fe-150">Poziom priorytetu hello alertu.</span><span class="sxs-lookup"><span data-stu-id="854fe-150">Priority level of hello alert.</span></span> |
| <span data-ttu-id="854fe-151">StateType</span><span class="sxs-lookup"><span data-stu-id="854fe-151">StateType</span></span> | <span data-ttu-id="854fe-152">Typ Hello stanu hello alertu.</span><span class="sxs-lookup"><span data-stu-id="854fe-152">hello type of state of hello alert.</span></span><br><br><span data-ttu-id="854fe-153">SOFT - problem, który nie został zresetowany.</span><span class="sxs-lookup"><span data-stu-id="854fe-153">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="854fe-154">TWARDE — problem, który został zresetowany przez określoną liczbę razy.</span><span class="sxs-lookup"><span data-stu-id="854fe-154">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="854fe-155">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="854fe-155">TimeGenerated</span></span> |<span data-ttu-id="854fe-156">Data i godzina hello alert został utworzony.</span><span class="sxs-lookup"><span data-stu-id="854fe-156">Date and time hello alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="854fe-157">Rejestruje alertu Zabbix</span><span class="sxs-lookup"><span data-stu-id="854fe-157">Zabbix alert records</span></span>
<span data-ttu-id="854fe-158">Alert ma rekordy zebrane przez Zabbix **typu** z **alertu** i **SourceSystem** z **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="854fe-158">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="854fe-159">Mają one właściwości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="854fe-159">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="854fe-160">Właściwość</span><span class="sxs-lookup"><span data-stu-id="854fe-160">Property</span></span> | <span data-ttu-id="854fe-161">Opis</span><span class="sxs-lookup"><span data-stu-id="854fe-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="854fe-162">Typ</span><span class="sxs-lookup"><span data-stu-id="854fe-162">Type</span></span> |<span data-ttu-id="854fe-163">*Alert*</span><span class="sxs-lookup"><span data-stu-id="854fe-163">*Alert*</span></span> |
| <span data-ttu-id="854fe-164">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="854fe-164">SourceSystem</span></span> |<span data-ttu-id="854fe-165">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="854fe-165">*Zabbix*</span></span> |
| <span data-ttu-id="854fe-166">AlertName</span><span class="sxs-lookup"><span data-stu-id="854fe-166">AlertName</span></span> | <span data-ttu-id="854fe-167">Nazwa alertu hello.</span><span class="sxs-lookup"><span data-stu-id="854fe-167">Name of hello alert.</span></span> |
| <span data-ttu-id="854fe-168">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="854fe-168">AlertPriority</span></span> | <span data-ttu-id="854fe-169">Ważność alertu hello.</span><span class="sxs-lookup"><span data-stu-id="854fe-169">Severity of hello alert.</span></span><br><br><span data-ttu-id="854fe-170">nie sklasyfikowane</span><span class="sxs-lookup"><span data-stu-id="854fe-170">not classified</span></span><br><span data-ttu-id="854fe-171">Informacje</span><span class="sxs-lookup"><span data-stu-id="854fe-171">information</span></span><br><span data-ttu-id="854fe-172">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="854fe-172">warning</span></span><br><span data-ttu-id="854fe-173">Średnia</span><span class="sxs-lookup"><span data-stu-id="854fe-173">average</span></span><br><span data-ttu-id="854fe-174">Wysoka</span><span class="sxs-lookup"><span data-stu-id="854fe-174">high</span></span><br><span data-ttu-id="854fe-175">po awarii</span><span class="sxs-lookup"><span data-stu-id="854fe-175">disaster</span></span>  |
| <span data-ttu-id="854fe-176">Stan alertu</span><span class="sxs-lookup"><span data-stu-id="854fe-176">AlertState</span></span> | <span data-ttu-id="854fe-177">Stan alertu hello.</span><span class="sxs-lookup"><span data-stu-id="854fe-177">State of hello alert.</span></span><br><br><span data-ttu-id="854fe-178">0 — stan działa toodate.</span><span class="sxs-lookup"><span data-stu-id="854fe-178">0 - State is up toodate.</span></span><br><span data-ttu-id="854fe-179">1 — stan jest nieznany.</span><span class="sxs-lookup"><span data-stu-id="854fe-179">1 - State is unknown.</span></span>  |
| <span data-ttu-id="854fe-180">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="854fe-180">AlertTypeNumber</span></span> | <span data-ttu-id="854fe-181">Określa, czy alert może wygenerować wiele zdarzeń problem.</span><span class="sxs-lookup"><span data-stu-id="854fe-181">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="854fe-182">0 — stan działa toodate.</span><span class="sxs-lookup"><span data-stu-id="854fe-182">0 - State is up toodate.</span></span><br><span data-ttu-id="854fe-183">1 — stan jest nieznany.</span><span class="sxs-lookup"><span data-stu-id="854fe-183">1 - State is unknown.</span></span>    |
| <span data-ttu-id="854fe-184">Komentarze</span><span class="sxs-lookup"><span data-stu-id="854fe-184">Comments</span></span> | <span data-ttu-id="854fe-185">Dodatkowe uwagi o alercie.</span><span class="sxs-lookup"><span data-stu-id="854fe-185">Additional comments for alert.</span></span> |
| <span data-ttu-id="854fe-186">Nazwa hosta</span><span class="sxs-lookup"><span data-stu-id="854fe-186">HostName</span></span> | <span data-ttu-id="854fe-187">Nazwa hosta hello, utworzony hello alert.</span><span class="sxs-lookup"><span data-stu-id="854fe-187">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="854fe-188">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="854fe-188">PriorityNumber</span></span> | <span data-ttu-id="854fe-189">Wartość wskazująca, ważność alertu hello.</span><span class="sxs-lookup"><span data-stu-id="854fe-189">Value indicating severity of hello alert.</span></span><br><br><span data-ttu-id="854fe-190">0 — nie sklasyfikowane</span><span class="sxs-lookup"><span data-stu-id="854fe-190">0 - not classified</span></span><br><span data-ttu-id="854fe-191">1 — informacje</span><span class="sxs-lookup"><span data-stu-id="854fe-191">1 - information</span></span><br><span data-ttu-id="854fe-192">2 — ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="854fe-192">2 - warning</span></span><br><span data-ttu-id="854fe-193">3 — średnia</span><span class="sxs-lookup"><span data-stu-id="854fe-193">3 - average</span></span><br><span data-ttu-id="854fe-194">4 - Wysoka</span><span class="sxs-lookup"><span data-stu-id="854fe-194">4 - high</span></span><br><span data-ttu-id="854fe-195">5 — po awarii</span><span class="sxs-lookup"><span data-stu-id="854fe-195">5 - disaster</span></span> |
| <span data-ttu-id="854fe-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="854fe-196">TimeGenerated</span></span> |<span data-ttu-id="854fe-197">Data i godzina hello alert został utworzony.</span><span class="sxs-lookup"><span data-stu-id="854fe-197">Date and time hello alert was created.</span></span> |
| <span data-ttu-id="854fe-198">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="854fe-198">TimeLastModified</span></span> |<span data-ttu-id="854fe-199">Data i godzina stan hello hello alert został ostatnio zmieniony.</span><span class="sxs-lookup"><span data-stu-id="854fe-199">Date and time hello state of hello alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="854fe-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="854fe-200">Next steps</span></span>
* <span data-ttu-id="854fe-201">Dowiedz się więcej o [alerty](log-analytics-alerts.md) w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="854fe-201">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="854fe-202">Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="854fe-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
