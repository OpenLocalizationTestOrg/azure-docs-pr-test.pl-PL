---
title: "IT usługi łącznika zarządzania w OMS | Dokumentacja firmy Microsoft"
description: "Użyj łącznika zarządzania usługi IT, aby centralnie monitorować i zarządzać nimi elementy robocze Zarządzanie usługami IT — w OMS i szybkie rozwiązywanie problemów."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 54974ef06efdae69ddbfa12b1ba9278b48b113d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="888b0-103">Centralne zarządzanie Zarządzanie usługami IT — elementów roboczych za pomocą łącznika zarządzania usługi IT (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="888b0-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Symbol łącznika usługi zarządzania IT](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="888b0-105">Łącznik zarządzania usługi IT (ITSMC) OMS Log Analytics umożliwia centralnie monitorować i zarządzać nimi elementy robocze między Zarządzanie usługami IT — produktów/usług.</span><span class="sxs-lookup"><span data-stu-id="888b0-105">You can use the IT Service Management Connector (ITSMC) in OMS Log Analytics to centrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="888b0-106">Łącznik zarządzania usługi IT istniejących zarządzania usługi IT (zarządzanie, usługami IT —) produkty i usługi integruje się z analizy dzienników OMS.</span><span class="sxs-lookup"><span data-stu-id="888b0-106">The IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="888b0-107">Rozwiązanie ma dwukierunkową integrację z Zarządzanie usługami IT — produktów/usług, których zapewnia użytkownikom OMS opcję, aby utworzyć zdarzenia i alerty lub zdarzenia w rozwiązaniu Zarządzanie usługami IT —.</span><span class="sxs-lookup"><span data-stu-id="888b0-107">The solution has bidirectional integration with ITSM products/services, where it provides the OMS users an option to create incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="888b0-108">Łącznik również importuje dane takie jak zdarzenia i żądania zmiany z Zarządzanie usługami IT — rozwiązanie do analizy dzienników OMS.</span><span class="sxs-lookup"><span data-stu-id="888b0-108">The connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="888b0-109">Łącznik zarządzania usługi IT możesz:</span><span class="sxs-lookup"><span data-stu-id="888b0-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="888b0-110">Centralnie monitorować i zarządzać nimi elementów roboczych dla Zarządzanie usługami IT — produktów/usług używanych w organizacji.</span><span class="sxs-lookup"><span data-stu-id="888b0-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="888b0-111">Utwórz Zarządzanie usługami IT — elementów roboczych (na przykład alert, zdarzenie, zdarzenia) w zarządzanie usługami IT — OMS alertów i za pomocą wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="888b0-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="888b0-112">Przeczytaj zdarzenia i żądania zmiany z rozwiązania Zarządzanie usługami IT — skorelowany dziennik odpowiednich danych w obszarze roboczym analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="888b0-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="888b0-113">Znajdź wszelkie nieoczekiwane i nietypowe zdarzenia i rozwiąż je, nawet przed użytkowników końcowych wywołań i raportuj je do działu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="888b0-113">Find any unexpected and unusual events and resolve them, even before the end users call and report them to the helpdesk.</span></span>
  - <span data-ttu-id="888b0-114">Importowanie danych elementów pracy do analizy dzienników i tworzenia raportów kluczowy wskaźnik wydajności.</span><span class="sxs-lookup"><span data-stu-id="888b0-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="888b0-115">Korzystanie z tych raportów, możesz zidentyfikować, oceny i działają na kilka istotnych elementów, takich jak oceny złośliwego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="888b0-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="888b0-116">Wyświetlić wyselekcjonowanych pulpity nawigacyjne dla lepszy wgląd w zdarzenia, żądań zmiany i wpływ na systemy.</span><span class="sxs-lookup"><span data-stu-id="888b0-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="888b0-117">Rozwiązywanie problemów szybciej, korelując z innych rozwiązań do zarządzania w obszarze roboczym analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="888b0-117">Troubleshoot faster by correlating with other management solutions in the Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="888b0-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="888b0-118">Prerequisites</span></span>

<span data-ttu-id="888b0-119">Aby zaimportować elementy robocze Zarządzanie usługami IT — do analizy dzienników OMS, rozwiązanie wymaga połączenia między łącznika zarządzania usługi IT w OMS i IT SM produktu lub usługi z którego importowania elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="888b0-119">To import the ITSM work items into OMS Log Analytics, the solution requires a connection between the IT Service Management Connector in the OMS and the IT SM product/service from which you import the work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="888b0-120">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="888b0-120">Configuration</span></span>

<span data-ttu-id="888b0-121">Dodaj rozwiązanie IT usługi zarządzania łącznika do obszaru roboczego OMS zastosowanie procesu opisanego w [rozwiązań dodać analizy dzienników z galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="888b0-121">Add the IT Service Management Connector solution to your OMS work space, using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="888b0-122">Łącznik zarządzania usługi IT kafelka, jak widać w galerii rozwiązań:</span><span class="sxs-lookup"><span data-stu-id="888b0-122">IT Service Management Connector tile as you see in the Solutions gallery:</span></span>

![Łącznik kafelka](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="888b0-124">Po pomyślnym dodaniu zobaczysz łącznika zarządzania usługi IT w obszarze **OMS** > **ustawienia** > **połączonych źródeł.**</span><span class="sxs-lookup"><span data-stu-id="888b0-124">After successful addition, you will see the IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC połączone](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="888b0-126">Domyślnie łącznika zarządzania usługi IT odświeża dane połączenia raz w co 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="888b0-126">By default, the IT Service Management Connector refreshes the connection's data once in every 24 hours.</span></span> <span data-ttu-id="888b0-127">Aby odświeżyć tego połączenia danych natychmiast dla wszystkich edycji lub szablonu aktualizacje, które zostaną wprowadzone, kliknij przycisk Odśwież wyświetlana obok połączenia.</span><span class="sxs-lookup"><span data-stu-id="888b0-127">To refresh your connection's data instantly for any edits or template updates that you make, click the refresh button displayed next to your connection.</span></span>

 ![Odśwież ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="888b0-129">Pakiety administracyjne</span><span class="sxs-lookup"><span data-stu-id="888b0-129">Management packs</span></span>
<span data-ttu-id="888b0-130">To rozwiązanie nie wymaga żadnych pakietów administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="888b0-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="888b0-131">Połączone źródła</span><span class="sxs-lookup"><span data-stu-id="888b0-131">Connected sources</span></span>

<span data-ttu-id="888b0-132">Następujące produkty Zarządzanie usługami IT — / usługi są obsługiwane przez łącznik zarządzania usługi IT:</span><span class="sxs-lookup"><span data-stu-id="888b0-132">The following ITSM products/services are supported by the IT Service Management Connector:</span></span>

- [<span data-ttu-id="888b0-133">Program System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="888b0-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="888b0-134">Usługi ServiceNow</span><span class="sxs-lookup"><span data-stu-id="888b0-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="888b0-135">Provance</span><span class="sxs-lookup"><span data-stu-id="888b0-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="888b0-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="888b0-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-the-solution"></a><span data-ttu-id="888b0-137">Użycie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="888b0-137">Using the solution</span></span>

<span data-ttu-id="888b0-138">Po podłączeniu łącznika zarządzania OMS IT usługi z usługą Zarządzanie usługami IT — usługi analizy dzienników rozpoczyna zbieranie danych z połączonych Zarządzanie usługami IT — produktów/usług.</span><span class="sxs-lookup"><span data-stu-id="888b0-138">Once you connect the OMS IT Service Management Connector with your ITSM service, the Log Analytics services starts gathering the data from the connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="888b0-139">Dane importowane przez rozwiązanie łącznika zarządzania usługi IT pojawia się w analizy dziennika jako zdarzenia o nazwie **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="888b0-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="888b0-140">Zdarzenie zawiera pole o nazwie **ServiceDeskWorkItemType_s**.</span><span class="sxs-lookup"><span data-stu-id="888b0-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="888b0-141">które wykonać jego wartość jako zdarzenie lub żądanie, w zależności od danych elementów pracy znajdujących się na zmiany **ServiceDesk_CL** zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="888b0-141">which can take its value as incident, or change request, depending on the work item data contained in the **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="888b0-142">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="888b0-142">Input data</span></span>
<span data-ttu-id="888b0-143">Elementy pracy zaimportowane z Zarządzanie usługami IT — produktów/usług.</span><span class="sxs-lookup"><span data-stu-id="888b0-143">Work items imported from the ITSM products/services.</span></span>

<span data-ttu-id="888b0-144">Poniższe informacje przedstawiono przykładowe dane zebrane przez łącznik zarządzania usługami IT:</span><span class="sxs-lookup"><span data-stu-id="888b0-144">The following information shows examples of data gathered by the IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="888b0-145">W zależności od typu elementu roboczego zaimportowane do analizy dzienników **ServiceDesk_CL** zawiera następujące pola:</span><span class="sxs-lookup"><span data-stu-id="888b0-145">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span></span>

<span data-ttu-id="888b0-146">**Element pracy:** **zdarzenia**</span><span class="sxs-lookup"><span data-stu-id="888b0-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="888b0-147">ServiceDeskWorkItemType_s = "Zdarzenie"</span><span class="sxs-lookup"><span data-stu-id="888b0-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="888b0-148">**Pola**</span><span class="sxs-lookup"><span data-stu-id="888b0-148">**Fields**</span></span>

- <span data-ttu-id="888b0-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="888b0-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="888b0-150">Identyfikator technicznej usługi</span><span class="sxs-lookup"><span data-stu-id="888b0-150">Service Desk ID</span></span>
- <span data-ttu-id="888b0-151">Stan</span><span class="sxs-lookup"><span data-stu-id="888b0-151">State</span></span>
- <span data-ttu-id="888b0-152">Pilności</span><span class="sxs-lookup"><span data-stu-id="888b0-152">Urgency</span></span>
- <span data-ttu-id="888b0-153">Wpływ</span><span class="sxs-lookup"><span data-stu-id="888b0-153">Impact</span></span>
- <span data-ttu-id="888b0-154">Priorytet</span><span class="sxs-lookup"><span data-stu-id="888b0-154">Priority</span></span>
- <span data-ttu-id="888b0-155">Eskalacja</span><span class="sxs-lookup"><span data-stu-id="888b0-155">Escalation</span></span>
- <span data-ttu-id="888b0-156">Utworzone przez</span><span class="sxs-lookup"><span data-stu-id="888b0-156">Created By</span></span>
- <span data-ttu-id="888b0-157">Rozwiązany przez</span><span class="sxs-lookup"><span data-stu-id="888b0-157">Resolved By</span></span>
- <span data-ttu-id="888b0-158">Zamknięte przez</span><span class="sxs-lookup"><span data-stu-id="888b0-158">Closed By</span></span>
- <span data-ttu-id="888b0-159">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="888b0-159">Source</span></span>
- <span data-ttu-id="888b0-160">Przypisane do</span><span class="sxs-lookup"><span data-stu-id="888b0-160">Assigned To</span></span>
- <span data-ttu-id="888b0-161">Kategoria</span><span class="sxs-lookup"><span data-stu-id="888b0-161">Category</span></span>
- <span data-ttu-id="888b0-162">Tytuł</span><span class="sxs-lookup"><span data-stu-id="888b0-162">Title</span></span>
- <span data-ttu-id="888b0-163">Opis</span><span class="sxs-lookup"><span data-stu-id="888b0-163">Description</span></span>
- <span data-ttu-id="888b0-164">Data utworzenia</span><span class="sxs-lookup"><span data-stu-id="888b0-164">Created Date</span></span>
- <span data-ttu-id="888b0-165">Data zamknięcia</span><span class="sxs-lookup"><span data-stu-id="888b0-165">Closed Date</span></span>
- <span data-ttu-id="888b0-166">Data rozwiązania</span><span class="sxs-lookup"><span data-stu-id="888b0-166">Resolved Date</span></span>
- <span data-ttu-id="888b0-167">Data ostatniej modyfikacji</span><span class="sxs-lookup"><span data-stu-id="888b0-167">Last Modified Date</span></span>
- <span data-ttu-id="888b0-168">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="888b0-168">Computer</span></span>


<span data-ttu-id="888b0-169">**Element pracy:** **żądania zmiany**</span><span class="sxs-lookup"><span data-stu-id="888b0-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="888b0-170">ServiceDeskWorkItemType_s = "Żądanie zmiany"</span><span class="sxs-lookup"><span data-stu-id="888b0-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="888b0-171">**Pola**</span><span class="sxs-lookup"><span data-stu-id="888b0-171">**Fields**</span></span>
- <span data-ttu-id="888b0-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="888b0-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="888b0-173">Identyfikator technicznej usługi</span><span class="sxs-lookup"><span data-stu-id="888b0-173">Service Desk ID</span></span>
- <span data-ttu-id="888b0-174">Utworzone przez</span><span class="sxs-lookup"><span data-stu-id="888b0-174">Created By</span></span>
- <span data-ttu-id="888b0-175">Zamknięte przez</span><span class="sxs-lookup"><span data-stu-id="888b0-175">Closed By</span></span>
- <span data-ttu-id="888b0-176">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="888b0-176">Source</span></span>
- <span data-ttu-id="888b0-177">Przypisane do</span><span class="sxs-lookup"><span data-stu-id="888b0-177">Assigned To</span></span>
- <span data-ttu-id="888b0-178">Tytuł</span><span class="sxs-lookup"><span data-stu-id="888b0-178">Title</span></span>
- <span data-ttu-id="888b0-179">Typ</span><span class="sxs-lookup"><span data-stu-id="888b0-179">Type</span></span>
- <span data-ttu-id="888b0-180">Kategoria</span><span class="sxs-lookup"><span data-stu-id="888b0-180">Category</span></span>
- <span data-ttu-id="888b0-181">Stan</span><span class="sxs-lookup"><span data-stu-id="888b0-181">State</span></span>
- <span data-ttu-id="888b0-182">Eskalacja</span><span class="sxs-lookup"><span data-stu-id="888b0-182">Escalation</span></span>
- <span data-ttu-id="888b0-183">Konflikt stanu</span><span class="sxs-lookup"><span data-stu-id="888b0-183">Conflict Status</span></span>
- <span data-ttu-id="888b0-184">Pilności</span><span class="sxs-lookup"><span data-stu-id="888b0-184">Urgency</span></span>
- <span data-ttu-id="888b0-185">Priorytet</span><span class="sxs-lookup"><span data-stu-id="888b0-185">Priority</span></span>
- <span data-ttu-id="888b0-186">Ryzyko</span><span class="sxs-lookup"><span data-stu-id="888b0-186">Risk</span></span>
- <span data-ttu-id="888b0-187">Wpływ</span><span class="sxs-lookup"><span data-stu-id="888b0-187">Impact</span></span>
- <span data-ttu-id="888b0-188">Przypisane do</span><span class="sxs-lookup"><span data-stu-id="888b0-188">Assigned To</span></span>
- <span data-ttu-id="888b0-189">Data utworzenia</span><span class="sxs-lookup"><span data-stu-id="888b0-189">Created Date</span></span>
- <span data-ttu-id="888b0-190">Data zamknięcia</span><span class="sxs-lookup"><span data-stu-id="888b0-190">Closed Date</span></span>
- <span data-ttu-id="888b0-191">Data ostatniej modyfikacji</span><span class="sxs-lookup"><span data-stu-id="888b0-191">Last Modified Date</span></span>
- <span data-ttu-id="888b0-192">Żądana data</span><span class="sxs-lookup"><span data-stu-id="888b0-192">Requested Date</span></span>
- <span data-ttu-id="888b0-193">Planowana data rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="888b0-193">Planned Start Date</span></span>
- <span data-ttu-id="888b0-194">Planowana data zakończenia</span><span class="sxs-lookup"><span data-stu-id="888b0-194">Planned End Date</span></span>
- <span data-ttu-id="888b0-195">Data rozpoczęcia pracy</span><span class="sxs-lookup"><span data-stu-id="888b0-195">Work Start Date</span></span>
- <span data-ttu-id="888b0-196">Data zakończenia pracy</span><span class="sxs-lookup"><span data-stu-id="888b0-196">Work End Date</span></span>
- <span data-ttu-id="888b0-197">Opis</span><span class="sxs-lookup"><span data-stu-id="888b0-197">Description</span></span>
- <span data-ttu-id="888b0-198">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="888b0-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="888b0-199">Dane wyjściowe dla zdarzenia usługi ServiceNow</span><span class="sxs-lookup"><span data-stu-id="888b0-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="888b0-200">Pole OMS</span><span class="sxs-lookup"><span data-stu-id="888b0-200">OMS field</span></span> | <span data-ttu-id="888b0-201">Zarządzanie usługami IT — pola</span><span class="sxs-lookup"><span data-stu-id="888b0-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="888b0-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="888b0-202">ServiceDeskId_s</span></span>| <span data-ttu-id="888b0-203">Numer</span><span class="sxs-lookup"><span data-stu-id="888b0-203">Number</span></span> |
| <span data-ttu-id="888b0-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="888b0-204">IncidentState_s</span></span> | <span data-ttu-id="888b0-205">Stan</span><span class="sxs-lookup"><span data-stu-id="888b0-205">State</span></span> |
| <span data-ttu-id="888b0-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="888b0-206">Urgency_s</span></span> |<span data-ttu-id="888b0-207">Pilności</span><span class="sxs-lookup"><span data-stu-id="888b0-207">Urgency</span></span> |
| <span data-ttu-id="888b0-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="888b0-208">Impact_s</span></span> |<span data-ttu-id="888b0-209">Wpływ</span><span class="sxs-lookup"><span data-stu-id="888b0-209">Impact</span></span>|
| <span data-ttu-id="888b0-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="888b0-210">Priority_s</span></span> | <span data-ttu-id="888b0-211">Priorytet</span><span class="sxs-lookup"><span data-stu-id="888b0-211">Priority</span></span> |
| <span data-ttu-id="888b0-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="888b0-212">CreatedBy_s</span></span> | <span data-ttu-id="888b0-213">Otwarty przez</span><span class="sxs-lookup"><span data-stu-id="888b0-213">Opened by</span></span> |
| <span data-ttu-id="888b0-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="888b0-214">ResolvedBy_s</span></span> | <span data-ttu-id="888b0-215">Rozwiązany przez</span><span class="sxs-lookup"><span data-stu-id="888b0-215">Resolved by</span></span>|
| <span data-ttu-id="888b0-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="888b0-216">ClosedBy_s</span></span>  | <span data-ttu-id="888b0-217">Zamknięte przez</span><span class="sxs-lookup"><span data-stu-id="888b0-217">Closed by</span></span> |
| <span data-ttu-id="888b0-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="888b0-218">Source_s</span></span>| <span data-ttu-id="888b0-219">Skontaktuj się z typu</span><span class="sxs-lookup"><span data-stu-id="888b0-219">Contact type</span></span> |
| <span data-ttu-id="888b0-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="888b0-220">AssignedTo_s</span></span> | <span data-ttu-id="888b0-221">Przypisane do</span><span class="sxs-lookup"><span data-stu-id="888b0-221">Assigned to</span></span>  |
| <span data-ttu-id="888b0-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="888b0-222">Category_s</span></span> | <span data-ttu-id="888b0-223">Kategoria</span><span class="sxs-lookup"><span data-stu-id="888b0-223">Category</span></span> |
| <span data-ttu-id="888b0-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="888b0-224">Title_s</span></span>|  <span data-ttu-id="888b0-225">Krótki opis</span><span class="sxs-lookup"><span data-stu-id="888b0-225">Short description</span></span> |
| <span data-ttu-id="888b0-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="888b0-226">Description_s</span></span>|  <span data-ttu-id="888b0-227">Uwagi</span><span class="sxs-lookup"><span data-stu-id="888b0-227">Notes</span></span> |
| <span data-ttu-id="888b0-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="888b0-228">CreatedDate_t</span></span>|  <span data-ttu-id="888b0-229">Otwarte</span><span class="sxs-lookup"><span data-stu-id="888b0-229">Opened</span></span> |
| <span data-ttu-id="888b0-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="888b0-230">ClosedDate_t</span></span>| <span data-ttu-id="888b0-231">zamknięte</span><span class="sxs-lookup"><span data-stu-id="888b0-231">closed</span></span>|
| <span data-ttu-id="888b0-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="888b0-232">ResolvedDate_t</span></span>|<span data-ttu-id="888b0-233">Rozwiązane</span><span class="sxs-lookup"><span data-stu-id="888b0-233">Resolved</span></span>|
| <span data-ttu-id="888b0-234">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="888b0-234">Computer</span></span>  | <span data-ttu-id="888b0-235">element konfiguracji</span><span class="sxs-lookup"><span data-stu-id="888b0-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="888b0-236">Dane wyjściowe dla usługi ServiceNow żądania zmiany</span><span class="sxs-lookup"><span data-stu-id="888b0-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="888b0-237">Pole OMS</span><span class="sxs-lookup"><span data-stu-id="888b0-237">OMS field</span></span> | <span data-ttu-id="888b0-238">Zarządzanie usługami IT — pola</span><span class="sxs-lookup"><span data-stu-id="888b0-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="888b0-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="888b0-239">ServiceDeskId_s</span></span>| <span data-ttu-id="888b0-240">Numer</span><span class="sxs-lookup"><span data-stu-id="888b0-240">Number</span></span> |
| <span data-ttu-id="888b0-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="888b0-241">CreatedBy_s</span></span> | <span data-ttu-id="888b0-242">Żądanie</span><span class="sxs-lookup"><span data-stu-id="888b0-242">Requested by</span></span> |
| <span data-ttu-id="888b0-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="888b0-243">ClosedBy_s</span></span> | <span data-ttu-id="888b0-244">Zamknięte przez</span><span class="sxs-lookup"><span data-stu-id="888b0-244">Closed by</span></span> |
| <span data-ttu-id="888b0-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="888b0-245">AssignedTo_s</span></span> | <span data-ttu-id="888b0-246">Przypisane do</span><span class="sxs-lookup"><span data-stu-id="888b0-246">Assigned to</span></span>  |
| <span data-ttu-id="888b0-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="888b0-247">Title_s</span></span>|  <span data-ttu-id="888b0-248">Krótki opis</span><span class="sxs-lookup"><span data-stu-id="888b0-248">Short description</span></span> |
| <span data-ttu-id="888b0-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="888b0-249">Type_s</span></span>|  <span data-ttu-id="888b0-250">Typ</span><span class="sxs-lookup"><span data-stu-id="888b0-250">Type</span></span> |
| <span data-ttu-id="888b0-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="888b0-251">Category_s</span></span>|  <span data-ttu-id="888b0-252">Catgory</span><span class="sxs-lookup"><span data-stu-id="888b0-252">Catgory</span></span> |
| <span data-ttu-id="888b0-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="888b0-253">CRState_s</span></span>|  <span data-ttu-id="888b0-254">Stan</span><span class="sxs-lookup"><span data-stu-id="888b0-254">State</span></span>|
| <span data-ttu-id="888b0-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="888b0-255">Urgency_s</span></span>|  <span data-ttu-id="888b0-256">Pilności</span><span class="sxs-lookup"><span data-stu-id="888b0-256">Urgency</span></span> |
| <span data-ttu-id="888b0-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="888b0-257">Priority_s</span></span>| <span data-ttu-id="888b0-258">Priorytet</span><span class="sxs-lookup"><span data-stu-id="888b0-258">Priority</span></span>|
| <span data-ttu-id="888b0-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="888b0-259">Risk_s</span></span>| <span data-ttu-id="888b0-260">Ryzyko</span><span class="sxs-lookup"><span data-stu-id="888b0-260">Risk</span></span>|
| <span data-ttu-id="888b0-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="888b0-261">Impact_s</span></span>| <span data-ttu-id="888b0-262">Wpływ</span><span class="sxs-lookup"><span data-stu-id="888b0-262">Impact</span></span>|
| <span data-ttu-id="888b0-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="888b0-263">RequestedDate_t</span></span>  | <span data-ttu-id="888b0-264">Żądana według daty</span><span class="sxs-lookup"><span data-stu-id="888b0-264">Requested by date</span></span> |
| <span data-ttu-id="888b0-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="888b0-265">ClosedDate_t</span></span> | <span data-ttu-id="888b0-266">Data zamknięcia</span><span class="sxs-lookup"><span data-stu-id="888b0-266">Closed date</span></span> |
| <span data-ttu-id="888b0-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="888b0-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="888b0-268">Planowana data rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="888b0-268">Planned start date</span></span> |
| <span data-ttu-id="888b0-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="888b0-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="888b0-270">Planowana data zakończenia</span><span class="sxs-lookup"><span data-stu-id="888b0-270">Planned end date</span></span> |
| <span data-ttu-id="888b0-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="888b0-271">WorkStartDate_t</span></span>  | <span data-ttu-id="888b0-272">Rzeczywista data rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="888b0-272">Actual start date</span></span> |
| <span data-ttu-id="888b0-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="888b0-273">WorkEndDate_t</span></span> | <span data-ttu-id="888b0-274">Rzeczywista data zakończenia</span><span class="sxs-lookup"><span data-stu-id="888b0-274">Actual end date</span></span>|
| <span data-ttu-id="888b0-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="888b0-275">Description_s</span></span> | <span data-ttu-id="888b0-276">Opis</span><span class="sxs-lookup"><span data-stu-id="888b0-276">Description</span></span> |
| <span data-ttu-id="888b0-277">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="888b0-277">Computer</span></span>  | <span data-ttu-id="888b0-278">Element konfiguracji</span><span class="sxs-lookup"><span data-stu-id="888b0-278">Configuration Item</span></span> |

<span data-ttu-id="888b0-279">**Przykładowy ekran analizy dzienników dla danych Zarządzanie usługami IT —:**</span><span class="sxs-lookup"><span data-stu-id="888b0-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Ekran analiza dziennika](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="888b0-281">Łącznik zarządzania usługami IT — Integracja z innych rozwiązań pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="888b0-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="888b0-282">Łącznik zarządzania usługi IT, obecnie obsługuje integrację z rozwiązaniem mapy usługi.</span><span class="sxs-lookup"><span data-stu-id="888b0-282">IT Service Management Connector, currently supports integration with the Service Map solution.</span></span>

<span data-ttu-id="888b0-283">Mapa usług automatycznie wykrywa składniki aplikacji w systemach Windows i Linux i mapuje komunikacji między usługami.</span><span class="sxs-lookup"><span data-stu-id="888b0-283">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="888b0-284">Umożliwia ona przeglądać serwery jako traktować ich — jako połączonych systemy, które dostarczają usług krytycznych.</span><span class="sxs-lookup"><span data-stu-id="888b0-284">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="888b0-285">Mapy usługi pokazuje połączeń między serwerami, procesów, i portów w dowolnej architekturze połączenia TCP z konfiguracji wymagane inne niż instalacji agenta.</span><span class="sxs-lookup"><span data-stu-id="888b0-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="888b0-286">Więcej informacji: [mapy usługi](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="888b0-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="888b0-287">Dzięki tej integracji można wyświetlić elementy technicznej usług utworzone w rozwiązaniach Zarządzanie usługami IT —, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="888b0-287">With this integration, you can view the service desk items created in the ITSM solutions as shown in the following example:</span></span>

![<span data-ttu-id="888b0-288">Zintegrowane rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="888b0-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="888b0-289">Tworzenie elementów roboczych Zarządzanie usługami IT — OMS alertów</span><span class="sxs-lookup"><span data-stu-id="888b0-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="888b0-290">Dla alertów OMS w połączonych źródeł Zarządzanie usługami IT — można utworzyć skojarzonych elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="888b0-290">For the OMS alerts, you can create associated work items in the connected ITSM sources.</span></span>  <span data-ttu-id="888b0-291">Aby to zrobić, użyj następującej procedury:</span><span class="sxs-lookup"><span data-stu-id="888b0-291">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="888b0-292">Z **wyszukiwania dziennika** okna, uruchom zapytania wyszukiwania dziennika, aby wyświetlić dane.</span><span class="sxs-lookup"><span data-stu-id="888b0-292">From **Log Search** window, run a log search query to view data.</span></span> <span data-ttu-id="888b0-293">Wyniki zapytania są źródłem dla elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="888b0-293">Query results are the source for work items.</span></span>
2. <span data-ttu-id="888b0-294">W **wyszukiwania dziennika**, kliknij przycisk **alertu** otworzyć **Dodaj regułę alertu** strony.</span><span class="sxs-lookup"><span data-stu-id="888b0-294">In **Log Search**, click **Alert** to open the **Add Alert Rule** page.</span></span>

    ![Ekran analiza dziennika](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="888b0-296">Na **Dodaj regułę alertu** okna, podaj wymagane szczegóły dotyczące **nazwa**, **ważność**, **zapytania wyszukiwania**, i **alertu kryteria** (pomiar Metryka okno czasu).</span><span class="sxs-lookup"><span data-stu-id="888b0-296">On the **Add Alert Rule** window, provide the required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="888b0-297">Wybierz **tak** dla **akcje Zarządzanie usługami IT —**.</span><span class="sxs-lookup"><span data-stu-id="888b0-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="888b0-298">Wybierz połączenie Zarządzanie usługami IT — od **połączenia wybierz** listy.</span><span class="sxs-lookup"><span data-stu-id="888b0-298">Select your ITSM connection from the **Select Connection** list.</span></span>
6. <span data-ttu-id="888b0-299">Podaj szczegóły zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="888b0-299">Provide the details as required.</span></span>
7. <span data-ttu-id="888b0-300">Aby utworzyć element roboczy osobne dla każdego wpisu dziennika tego alertu, wybierz **utworzyć poszczególnych elementach roboczych dla każdego wpisu dziennika** wyboru.</span><span class="sxs-lookup"><span data-stu-id="888b0-300">To create a separate work item for each log entry of this alert, select the **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="888b0-301">Lub</span><span class="sxs-lookup"><span data-stu-id="888b0-301">Or</span></span>

    <span data-ttu-id="888b0-302">Pozostaw to pole wyboru niezaznaczone można utworzyć tylko jeden element roboczy dla dowolnej liczby wpisów dziennika w ramach tego alertu.</span><span class="sxs-lookup"><span data-stu-id="888b0-302">leave this checkbox unselected to create only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="888b0-303">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="888b0-303">Click **Save**.</span></span>

<span data-ttu-id="888b0-304">OMS alert zostaną utworzone w obszarze **alerty**.</span><span class="sxs-lookup"><span data-stu-id="888b0-304">The OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="888b0-305">Zarządzanie usługami IT — połączenie odpowiednich elementów roboczych są tworzone po spełnieniu warunku określony alert.</span><span class="sxs-lookup"><span data-stu-id="888b0-305">The corresponding ITSM connection's work items are created when the specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="888b0-306">Tworzenie elementów roboczych Zarządzanie usługami IT — z dzienników OMS</span><span class="sxs-lookup"><span data-stu-id="888b0-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="888b0-307">Elementy robocze w połączonych źródeł Zarządzanie usługami IT — można utworzyć za pomocą wyszukiwania dziennika OMS.</span><span class="sxs-lookup"><span data-stu-id="888b0-307">You can create work items in the connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="888b0-308">Aby to zrobić, użyj następującej procedury:</span><span class="sxs-lookup"><span data-stu-id="888b0-308">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="888b0-309">Z **wyszukiwania dziennika**, wyszukaj wymagane dane, wybierz szczegóły, a następnie kliknij przycisk **Utwórz element roboczy**.</span><span class="sxs-lookup"><span data-stu-id="888b0-309">From **Log Search**,  search the required data, select the detail, and click **Create work item**.</span></span>

    <span data-ttu-id="888b0-310">**Elementu roboczego Zarządzanie usługami IT — tworzenie** zostanie wyświetlone okno:</span><span class="sxs-lookup"><span data-stu-id="888b0-310">The **Create ITSM Work item** window appears:</span></span>

    ![Ekran analiza dziennika](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="888b0-312">Dodaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="888b0-312">Add the following details:</span></span>

  - <span data-ttu-id="888b0-313">**Tytuł elementu pracy**: tytuł dla elementu roboczego.</span><span class="sxs-lookup"><span data-stu-id="888b0-313">**Work item Title**: Title for the work item.</span></span>
  - <span data-ttu-id="888b0-314">**Opis elementu roboczego**: opis nowego elementu roboczego.</span><span class="sxs-lookup"><span data-stu-id="888b0-314">**Work item Description**: Description for the new work item.</span></span>
  - <span data-ttu-id="888b0-315">**Wpływ na komputerze**: Nazwa komputera, na którym zostało znalezione te dane dziennika.</span><span class="sxs-lookup"><span data-stu-id="888b0-315">**Affected Computer**: Name of the computer where this log data was found.</span></span>
  - <span data-ttu-id="888b0-316">**Wybierz połączenie**: Zarządzanie usługami IT — połączenie, w którym chcesz utworzyć ten element roboczy.</span><span class="sxs-lookup"><span data-stu-id="888b0-316">**Select Connection**:  ITSM connection in which you want to create this work item.</span></span>
  - <span data-ttu-id="888b0-317">**Element roboczy**: typ elementu roboczego.</span><span class="sxs-lookup"><span data-stu-id="888b0-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="888b0-318">Aby korzystać z istniejących szablonów elementów pracy zdarzenia, kliknij przycisk **tak** w obszarze **Generuj element pracy oparty na szablonie** opcji, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="888b0-318">To use an existing work item template for an incident, click **Yes** under **Generate work item based on the template** option and then click **Create**.</span></span>

    <span data-ttu-id="888b0-319">Lub:</span><span class="sxs-lookup"><span data-stu-id="888b0-319">Or,</span></span>

    <span data-ttu-id="888b0-320">Kliknij przycisk **nr** Jeśli chcesz podać dostosowanych wartości.</span><span class="sxs-lookup"><span data-stu-id="888b0-320">Click **No** if you want to provide your customized values.</span></span>

4. <span data-ttu-id="888b0-321">Podaj odpowiednie wartości w **typ**, **wpływ**, **pilność**, **kategorii**, i **podkategorii** pola tekstowe, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="888b0-321">Provide the appropriate values in the **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="888b0-322">Element pracy zostanie utworzony w zarządzanie usługami IT —, które można również wyświetlić OMS.</span><span class="sxs-lookup"><span data-stu-id="888b0-322">The work item will be created in the ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="888b0-323">Rozwiązywanie problemów z połączeniami Zarządzanie usługami IT — w OMS</span><span class="sxs-lookup"><span data-stu-id="888b0-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="888b0-324">Jeśli połączenie nie powiedzie się z poziomu interfejsu użytkownika połączenia źródła i możesz uzyskać **błąd podczas zapisywania połączenia** wiadomości, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="888b0-324">If connection fails from connected source's UI and you get the **Error in saving connection** message, do the following:</span></span>
 - <span data-ttu-id="888b0-325">W przypadku połączenia usługi ServiceNow, Cherwell i Provance upewnij się, że poprawnie wprowadzono hasła identyfikator/klienta nazwy użytkownika i hasła i klienta dla każdego połączenia.</span><span class="sxs-lookup"><span data-stu-id="888b0-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  the username/password and  client ID/client secret  for each of the connections.</span></span> <span data-ttu-id="888b0-326">Jeśli błąd będzie się powtarzać, sprawdź, czy masz wystarczające uprawnienia w produktu Zarządzanie usługami IT — do nawiązania połączenia.</span><span class="sxs-lookup"><span data-stu-id="888b0-326">If the error persists, check if you have sufficient privileges  in the corresponding ITSM product to make the connection.</span></span>
 - <span data-ttu-id="888b0-327">W przypadku programu Service Manager upewnij się, że aplikacji sieci Web zostanie pomyślnie wdrożona i utworzono połączenie hybrydowe.</span><span class="sxs-lookup"><span data-stu-id="888b0-327">In case of Service Manager, ensure that the Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="888b0-328">Aby sprawdzić pomyślnym nawiązaniu połączenia z komputera lokalnego programu Service Manager, odwiedź adres URL aplikacji sieci Web zgodnie z opisem w dokumentacji dotyczącej wprowadzania [połączenia hybrydowego](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="888b0-328">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="888b0-329">Jeśli dane z usługi ServiceNow nie jest pierwsze zsynchronizowane w OMS, upewnij się, że usługi ServiceNow, wystąpienie nie jest uśpiony.</span><span class="sxs-lookup"><span data-stu-id="888b0-329">If data from ServiceNow is not getting synced in OMS, ensure that the ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="888b0-330">Może to nastąpić pewnego czasu w wystąpieniach deweloperów usługi ServiceNow, po bezczynności.</span><span class="sxs-lookup"><span data-stu-id="888b0-330">This might sometime happen in the ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="888b0-331">W przeciwnym wypadku zgłosić problem.</span><span class="sxs-lookup"><span data-stu-id="888b0-331">Else, report the issue.</span></span>
3.  <span data-ttu-id="888b0-332">Jeśli alerty pobierania uruchomienia z pakietu OMS, ale elementy robocze nie są pobierania utworzone w zarządzanie usługami IT — elementy produktu lub konfiguracja nie otrzymują utworzone/połączone z elementów roboczych lub informacje o ogólnym, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="888b0-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked to work items or for any generic information, do the following:</span></span>
 -  <span data-ttu-id="888b0-333">Rozwiązanie usługi zarządzania łącznika IT w portalu OMS może posłużyć do uzyskać podsumowanie połączeń/pracy elementów/komputerów itp. Kliknij komunikat o błędzie w bloku stanu, przejdź do **wyszukiwania dziennika** i wyświetlić połączenia, które zawiera błąd przy użyciu szczegóły komunikatu o błędzie.</span><span class="sxs-lookup"><span data-stu-id="888b0-333">IT Service Management Connector solution in OMS portal could be used to get a summary of connections/work items/computers etc. Click the error message in the status blade, navigate to **Log Search** and view the connection that has the error by using the details in the error message.</span></span>
 - <span data-ttu-id="888b0-334">bezpośrednio można wyświetlić informacje związane z/błędy w **wyszukiwania dziennika** strony *typu = ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="888b0-334">you can directly view the errors/related information in the **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="888b0-335">Rozwiązywanie problemów z wdrażaniem aplikacji sieci Web programu Service Manager</span><span class="sxs-lookup"><span data-stu-id="888b0-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="888b0-336">W przypadku problemów z wdrożeniem aplikacji sieci web upewnij się, że masz wystarczające uprawnienia w wymienionych do tworzenia/wdrożenie zasobów subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="888b0-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span></span>
2.  <span data-ttu-id="888b0-337">Jeśli **obiekt odwołanie nie jest ustawione na wystąpienie obiektu** komunikat o błędzie pojawia się podczas pracy [skryptu](log-analytics-itsmc-service-manager-script.md) upewnij się, że wprowadzono prawidłowe wartości w obszarze **Konfiguracja użytkownika** sekcja.</span><span class="sxs-lookup"><span data-stu-id="888b0-337">If **Object reference not set to instance of an object** error message appears while running the [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="888b0-338">Nie można utworzyć przestrzeń nazw przekaźnik magistrali usług, upewnij się, że dostawca wymagany zasób jest zarejestrowany w subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="888b0-338">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span></span> <span data-ttu-id="888b0-339">Jeśli nie jest zarejestrowany, ręcznie utworzyć go w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="888b0-339">If not registered, manually create it from the Azure portal.</span></span> <span data-ttu-id="888b0-340">Można również utworzyć go podczas [Tworzenie połączenia hybrydowego](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="888b0-340">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="888b0-341">Skontaktuj się z nami</span><span class="sxs-lookup"><span data-stu-id="888b0-341">Contact us</span></span>

<span data-ttu-id="888b0-342">Dla zapytania lub opinii na temat łącznika zarządzania usługi IT, skontaktuj się z nami pod adresem [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="888b0-342">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="888b0-343">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="888b0-343">Next steps</span></span>
<span data-ttu-id="888b0-344">[Dodaj do łącznika zarządzania usługi IT zarządzanie usługami IT — produktów/usług](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="888b0-344">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
