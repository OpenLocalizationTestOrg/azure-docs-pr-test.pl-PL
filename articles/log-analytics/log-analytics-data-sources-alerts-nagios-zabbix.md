---
title: Zbieraj alerty Nagios i Zabbix w OMS Log Analytics | Dokumentacja firmy Microsoft
description: "Nagios i Zabbix są typu open source, narzędzia do monitorowania. Alerty można zbierać z tych narzędzi do analizy dzienników w celu przeanalizowania wraz z alertów z innych źródeł.  W tym artykule opisano sposób konfigurowania agenta pakietu OMS dla systemu Linux zbierać alerty z tych systemów."
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
ms.openlocfilehash: 0b64c32e1031e704d50aab0b38eaea41e27d134b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="22d92-105">Zbieraj alerty z Nagios i Zabbix w Log Analytics z usługą OMS agenta dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="22d92-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="22d92-106">[Nagios](https://www.nagios.org/) i [Zabbix](http://www.zabbix.com/) są typu open source, narzędzia do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="22d92-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="22d92-107">Można zbierać alerty z tych narzędzi do analizy dzienników w celu przeanalizowania wraz z [alertów z innych źródeł](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="22d92-107">You can collect alerts from these tools into Log Analytics in order to analyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="22d92-108">W tym artykule opisano sposób konfigurowania agenta pakietu OMS dla systemu Linux zbierać alerty z tych systemów.</span><span class="sxs-lookup"><span data-stu-id="22d92-108">This article describes how to configure the OMS Agent for Linux to collect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="22d92-109">Konfigurowanie zbierania alertów</span><span class="sxs-lookup"><span data-stu-id="22d92-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="22d92-110">Konfigurowanie zbierania alertów Nagios</span><span class="sxs-lookup"><span data-stu-id="22d92-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="22d92-111">Wykonaj następujące czynności na serwerze Nagios do zbierania alertów.</span><span class="sxs-lookup"><span data-stu-id="22d92-111">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="22d92-112">Przyznaj użytkownikowi **omsagent** dostęp do odczytu do pliku dziennika Nagios (tj. `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="22d92-112">Grant the user **omsagent** read access to the Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="22d92-113">Zakładając, że plik nagios.log jest właścicielem grupy `nagios`, można dodać użytkownika **omsagent** do **nagios** grupy.</span><span class="sxs-lookup"><span data-stu-id="22d92-113">Assuming the nagios.log file is owned by the group `nagios`, you can add the user **omsagent** to the **nagios** group.</span></span> 

    <span data-ttu-id="22d92-114">sudo usermod - -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="22d92-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="22d92-115">Modyfikowanie pliku konfiguracji na (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="22d92-115">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="22d92-116">Upewnij się, że następujące wpisy są obecne i nie komentarze wychodzących:</span><span class="sxs-lookup"><span data-stu-id="22d92-116">Ensure the following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path to point to your nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="22d92-117">Uruchom ponownie demona omsagent</span><span class="sxs-lookup"><span data-stu-id="22d92-117">Restart the omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="22d92-118">Konfigurowanie zbierania alertów Zabbix</span><span class="sxs-lookup"><span data-stu-id="22d92-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="22d92-119">Aby zbierać alerty z serwera Zabbix, należy określić użytkownika i hasło w *zwykły tekst*.</span><span class="sxs-lookup"><span data-stu-id="22d92-119">To collect alerts from a Zabbix server, you need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="22d92-120">Nie jest to idealne rozwiązanie, ale zalecamy, aby utworzyć użytkownika, a następnie udzielić uprawnień, aby monitorować onlu.</span><span class="sxs-lookup"><span data-stu-id="22d92-120">This is not ideal, but we recommend that you create the user and grant permissions to monitor onlu.</span></span>

<span data-ttu-id="22d92-121">Wykonaj następujące czynności na serwerze Nagios do zbierania alertów.</span><span class="sxs-lookup"><span data-stu-id="22d92-121">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="22d92-122">Modyfikowanie pliku konfiguracji na (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="22d92-122">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="22d92-123">Upewnij się, że następujące wpisy są obecne i nie komentarze wychodzących.</span><span class="sxs-lookup"><span data-stu-id="22d92-123">Ensure the following entries are present and not commented out.</span></span>  <span data-ttu-id="22d92-124">Zmień wartości w danym środowisku Zabbix nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="22d92-124">Change the user name and password to values for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="22d92-125">Uruchom ponownie demona omsagent</span><span class="sxs-lookup"><span data-stu-id="22d92-125">Restart the omsagent daemon</span></span>

    <span data-ttu-id="22d92-126">sudo sh /opt/microsoft/omsagent/bin/service_control ponownego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="22d92-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="22d92-127">Rejestruje alertu</span><span class="sxs-lookup"><span data-stu-id="22d92-127">Alert records</span></span>
<span data-ttu-id="22d92-128">Rejestruje alertu można pobrać z Nagios i Zabbix przy użyciu [dziennika wyszukiwania](log-analytics-log-searches.md) w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="22d92-128">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="22d92-129">Rejestruje Nagios Alert</span><span class="sxs-lookup"><span data-stu-id="22d92-129">Nagios Alert records</span></span>

<span data-ttu-id="22d92-130">Alert ma rekordy zebrane przez Nagios **typu** z **alertu** i **SourceSystem** z **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="22d92-130">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="22d92-131">Mają one właściwości w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="22d92-131">They have the properties in the following table.</span></span>

| <span data-ttu-id="22d92-132">Właściwość</span><span class="sxs-lookup"><span data-stu-id="22d92-132">Property</span></span> | <span data-ttu-id="22d92-133">Opis</span><span class="sxs-lookup"><span data-stu-id="22d92-133">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d92-134">Typ</span><span class="sxs-lookup"><span data-stu-id="22d92-134">Type</span></span> |<span data-ttu-id="22d92-135">*Alert*</span><span class="sxs-lookup"><span data-stu-id="22d92-135">*Alert*</span></span> |
| <span data-ttu-id="22d92-136">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="22d92-136">SourceSystem</span></span> |<span data-ttu-id="22d92-137">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="22d92-137">*Nagios*</span></span> |
| <span data-ttu-id="22d92-138">AlertName</span><span class="sxs-lookup"><span data-stu-id="22d92-138">AlertName</span></span> |<span data-ttu-id="22d92-139">Nazwa alertu.</span><span class="sxs-lookup"><span data-stu-id="22d92-139">Name of the alert.</span></span> |
| <span data-ttu-id="22d92-140">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="22d92-140">AlertDescription</span></span> | <span data-ttu-id="22d92-141">Opis alertu.</span><span class="sxs-lookup"><span data-stu-id="22d92-141">Description of the alert.</span></span> |
| <span data-ttu-id="22d92-142">Stan alertu</span><span class="sxs-lookup"><span data-stu-id="22d92-142">AlertState</span></span> | <span data-ttu-id="22d92-143">Stan usługi lub hosta.</span><span class="sxs-lookup"><span data-stu-id="22d92-143">Status of the service or host.</span></span><br><br><span data-ttu-id="22d92-144">OK</span><span class="sxs-lookup"><span data-stu-id="22d92-144">OK</span></span><br><span data-ttu-id="22d92-145">OSTRZEŻENIE</span><span class="sxs-lookup"><span data-stu-id="22d92-145">WARNING</span></span><br><span data-ttu-id="22d92-146">W GÓRĘ</span><span class="sxs-lookup"><span data-stu-id="22d92-146">UP</span></span><br><span data-ttu-id="22d92-147">W DÓŁ</span><span class="sxs-lookup"><span data-stu-id="22d92-147">DOWN</span></span> |
| <span data-ttu-id="22d92-148">Nazwa hosta</span><span class="sxs-lookup"><span data-stu-id="22d92-148">HostName</span></span> | <span data-ttu-id="22d92-149">Nazwa hosta, który utworzony alert.</span><span class="sxs-lookup"><span data-stu-id="22d92-149">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="22d92-150">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="22d92-150">PriorityNumber</span></span> | <span data-ttu-id="22d92-151">Poziom priorytetu alertu.</span><span class="sxs-lookup"><span data-stu-id="22d92-151">Priority level of the alert.</span></span> |
| <span data-ttu-id="22d92-152">StateType</span><span class="sxs-lookup"><span data-stu-id="22d92-152">StateType</span></span> | <span data-ttu-id="22d92-153">Typ stanu alertu.</span><span class="sxs-lookup"><span data-stu-id="22d92-153">The type of state of the alert.</span></span><br><br><span data-ttu-id="22d92-154">SOFT - problem, który nie został zresetowany.</span><span class="sxs-lookup"><span data-stu-id="22d92-154">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="22d92-155">TWARDE — problem, który został zresetowany przez określoną liczbę razy.</span><span class="sxs-lookup"><span data-stu-id="22d92-155">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="22d92-156">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="22d92-156">TimeGenerated</span></span> |<span data-ttu-id="22d92-157">Data i godzina utworzenia alertu.</span><span class="sxs-lookup"><span data-stu-id="22d92-157">Date and time the alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="22d92-158">Rejestruje alertu Zabbix</span><span class="sxs-lookup"><span data-stu-id="22d92-158">Zabbix alert records</span></span>
<span data-ttu-id="22d92-159">Alert ma rekordy zebrane przez Zabbix **typu** z **alertu** i **SourceSystem** z **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="22d92-159">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="22d92-160">Mają one właściwości w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="22d92-160">They have the properties in the following table.</span></span>

| <span data-ttu-id="22d92-161">Właściwość</span><span class="sxs-lookup"><span data-stu-id="22d92-161">Property</span></span> | <span data-ttu-id="22d92-162">Opis</span><span class="sxs-lookup"><span data-stu-id="22d92-162">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d92-163">Typ</span><span class="sxs-lookup"><span data-stu-id="22d92-163">Type</span></span> |<span data-ttu-id="22d92-164">*Alert*</span><span class="sxs-lookup"><span data-stu-id="22d92-164">*Alert*</span></span> |
| <span data-ttu-id="22d92-165">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="22d92-165">SourceSystem</span></span> |<span data-ttu-id="22d92-166">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="22d92-166">*Zabbix*</span></span> |
| <span data-ttu-id="22d92-167">AlertName</span><span class="sxs-lookup"><span data-stu-id="22d92-167">AlertName</span></span> | <span data-ttu-id="22d92-168">Nazwa alertu.</span><span class="sxs-lookup"><span data-stu-id="22d92-168">Name of the alert.</span></span> |
| <span data-ttu-id="22d92-169">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="22d92-169">AlertPriority</span></span> | <span data-ttu-id="22d92-170">Ważność alertu.</span><span class="sxs-lookup"><span data-stu-id="22d92-170">Severity of the alert.</span></span><br><br><span data-ttu-id="22d92-171">nie sklasyfikowane</span><span class="sxs-lookup"><span data-stu-id="22d92-171">not classified</span></span><br><span data-ttu-id="22d92-172">Informacje</span><span class="sxs-lookup"><span data-stu-id="22d92-172">information</span></span><br><span data-ttu-id="22d92-173">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="22d92-173">warning</span></span><br><span data-ttu-id="22d92-174">Średnia</span><span class="sxs-lookup"><span data-stu-id="22d92-174">average</span></span><br><span data-ttu-id="22d92-175">Wysoka</span><span class="sxs-lookup"><span data-stu-id="22d92-175">high</span></span><br><span data-ttu-id="22d92-176">po awarii</span><span class="sxs-lookup"><span data-stu-id="22d92-176">disaster</span></span>  |
| <span data-ttu-id="22d92-177">Stan alertu</span><span class="sxs-lookup"><span data-stu-id="22d92-177">AlertState</span></span> | <span data-ttu-id="22d92-178">Stan alertu.</span><span class="sxs-lookup"><span data-stu-id="22d92-178">State of the alert.</span></span><br><br><span data-ttu-id="22d92-179">0 — stan jest aktualny.</span><span class="sxs-lookup"><span data-stu-id="22d92-179">0 - State is up to date.</span></span><br><span data-ttu-id="22d92-180">1 — stan jest nieznany.</span><span class="sxs-lookup"><span data-stu-id="22d92-180">1 - State is unknown.</span></span>  |
| <span data-ttu-id="22d92-181">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="22d92-181">AlertTypeNumber</span></span> | <span data-ttu-id="22d92-182">Określa, czy alert może wygenerować wiele zdarzeń problem.</span><span class="sxs-lookup"><span data-stu-id="22d92-182">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="22d92-183">0 — stan jest aktualny.</span><span class="sxs-lookup"><span data-stu-id="22d92-183">0 - State is up to date.</span></span><br><span data-ttu-id="22d92-184">1 — stan jest nieznany.</span><span class="sxs-lookup"><span data-stu-id="22d92-184">1 - State is unknown.</span></span>    |
| <span data-ttu-id="22d92-185">Komentarze</span><span class="sxs-lookup"><span data-stu-id="22d92-185">Comments</span></span> | <span data-ttu-id="22d92-186">Dodatkowe uwagi o alercie.</span><span class="sxs-lookup"><span data-stu-id="22d92-186">Additional comments for alert.</span></span> |
| <span data-ttu-id="22d92-187">Nazwa hosta</span><span class="sxs-lookup"><span data-stu-id="22d92-187">HostName</span></span> | <span data-ttu-id="22d92-188">Nazwa hosta, który utworzony alert.</span><span class="sxs-lookup"><span data-stu-id="22d92-188">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="22d92-189">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="22d92-189">PriorityNumber</span></span> | <span data-ttu-id="22d92-190">Wartość wskazująca, ważność alertu.</span><span class="sxs-lookup"><span data-stu-id="22d92-190">Value indicating severity of the alert.</span></span><br><br><span data-ttu-id="22d92-191">0 — nie sklasyfikowane</span><span class="sxs-lookup"><span data-stu-id="22d92-191">0 - not classified</span></span><br><span data-ttu-id="22d92-192">1 — informacje</span><span class="sxs-lookup"><span data-stu-id="22d92-192">1 - information</span></span><br><span data-ttu-id="22d92-193">2 — ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="22d92-193">2 - warning</span></span><br><span data-ttu-id="22d92-194">3 — średnia</span><span class="sxs-lookup"><span data-stu-id="22d92-194">3 - average</span></span><br><span data-ttu-id="22d92-195">4 - Wysoka</span><span class="sxs-lookup"><span data-stu-id="22d92-195">4 - high</span></span><br><span data-ttu-id="22d92-196">5 — po awarii</span><span class="sxs-lookup"><span data-stu-id="22d92-196">5 - disaster</span></span> |
| <span data-ttu-id="22d92-197">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="22d92-197">TimeGenerated</span></span> |<span data-ttu-id="22d92-198">Data i godzina utworzenia alertu.</span><span class="sxs-lookup"><span data-stu-id="22d92-198">Date and time the alert was created.</span></span> |
| <span data-ttu-id="22d92-199">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="22d92-199">TimeLastModified</span></span> |<span data-ttu-id="22d92-200">Data i godzina ostatniej zmiany stanu alertu.</span><span class="sxs-lookup"><span data-stu-id="22d92-200">Date and time the state of the alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="22d92-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22d92-201">Next steps</span></span>
* <span data-ttu-id="22d92-202">Dowiedz się więcej o [alerty](log-analytics-alerts.md) w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="22d92-202">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="22d92-203">Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) analizować dane zebrane ze źródeł danych i rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="22d92-203">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
