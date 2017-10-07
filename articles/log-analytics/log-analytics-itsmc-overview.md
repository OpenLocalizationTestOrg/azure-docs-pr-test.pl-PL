---
title: "Łącznik usługi zarządzania w OMS aaaIT | Dokumentacja firmy Microsoft"
description: "Użyj monitora toocentrally łącznika zarządzania usługi IT hello zarządzania elementami pracy Zarządzanie usługami IT — Witaj w OMS i szybkie rozwiązywanie problemów."
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
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="3fb6e-103">Centralne zarządzanie Zarządzanie usługami IT — elementów roboczych za pomocą łącznika zarządzania usługi IT (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="3fb6e-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Symbol łącznika usługi zarządzania IT](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="3fb6e-105">Można użyć hello IT usługi zarządzania łącznika (ITSMC) w monitorze toocentrally analizy dzienników OMS i zarządzania elementami pracy przez Zarządzanie usługami IT — produktów/usług.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-105">You can use hello IT Service Management Connector (ITSMC) in OMS Log Analytics toocentrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="3fb6e-106">Hello IT usługi zarządzania łącznika usług i produktach zarządzania usługi IT (zarządzanie, usługami IT —) integruje się z analizy dzienników OMS.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-106">hello IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="3fb6e-107">rozwiązanie Hello ma dwukierunkową integrację z Zarządzanie usługami IT — produktów/usług, w przypadku, gdy zapewnia hello OMS użytkowników opcji toocreate zdarzenia, alerty lub zdarzenia w rozwiązaniu Zarządzanie usługami IT —.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-107">hello solution has bidirectional integration with ITSM products/services, where it provides hello OMS users an option toocreate incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="3fb6e-108">Łącznik Hello również importuje dane takie jak zdarzenia i żądania zmiany z Zarządzanie usługami IT — rozwiązanie do analizy dzienników OMS.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-108">hello connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="3fb6e-109">Łącznik zarządzania usługi IT możesz:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="3fb6e-110">Centralnie monitorować i zarządzać nimi elementów roboczych dla Zarządzanie usługami IT — produktów/usług używanych w organizacji.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="3fb6e-111">Utwórz Zarządzanie usługami IT — elementów roboczych (na przykład alert, zdarzenie, zdarzenia) w zarządzanie usługami IT — OMS alertów i za pomocą wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="3fb6e-112">Przeczytaj zdarzenia i żądania zmiany z rozwiązania Zarządzanie usługami IT — skorelowany dziennik odpowiednich danych w obszarze roboczym analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="3fb6e-113">Znajdź wszelkie nieoczekiwane i nietypowe zdarzenia i rozwiązać je, nawet przed użytkownikom końcowym hello wywołań i raportuj je toohello pracy działu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-113">Find any unexpected and unusual events and resolve them, even before hello end users call and report them toohello helpdesk.</span></span>
  - <span data-ttu-id="3fb6e-114">Importowanie danych elementów pracy do analizy dzienników i tworzenia raportów kluczowy wskaźnik wydajności.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="3fb6e-115">Korzystanie z tych raportów, możesz zidentyfikować, oceny i działają na kilka istotnych elementów, takich jak oceny złośliwego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="3fb6e-116">Wyświetlić wyselekcjonowanych pulpity nawigacyjne dla lepszy wgląd w zdarzenia, żądań zmiany i wpływ na systemy.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="3fb6e-117">Rozwiązywanie problemów szybciej, korelując z innych rozwiązań do zarządzania w obszarze roboczym analizy dzienników hello.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-117">Troubleshoot faster by correlating with other management solutions in hello Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3fb6e-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3fb6e-118">Prerequisites</span></span>

<span data-ttu-id="3fb6e-119">tooimport hello Zarządzanie usługami IT — elementów pracy do analizy dzienników OMS, hello rozwiązanie wymaga połączenia między hello łącznika zarządzania usługi IT w hello OMS i IT SM hello produktu lub usługi, z których importować hello elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-119">tooimport hello ITSM work items into OMS Log Analytics, hello solution requires a connection between hello IT Service Management Connector in hello OMS and hello IT SM product/service from which you import hello work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="3fb6e-120">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="3fb6e-120">Configuration</span></span>

<span data-ttu-id="3fb6e-121">Dodaj hello obszar roboczy łącznika zarządzania usługi IT rozwiązania tooyour OMS, za pomocą hello procesu opisanego w [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="3fb6e-121">Add hello IT Service Management Connector solution tooyour OMS work space, using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="3fb6e-122">Łącznik zarządzania usługi IT kafelka, jak widać w galerii rozwiązań hello:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-122">IT Service Management Connector tile as you see in hello Solutions gallery:</span></span>

![Łącznik kafelka](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="3fb6e-124">Po pomyślnym dodaniu zobaczysz hello łącznika zarządzania usługi IT w obszarze **OMS** > **ustawienia** > **połączonych źródeł.**</span><span class="sxs-lookup"><span data-stu-id="3fb6e-124">After successful addition, you will see hello IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC połączone](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="3fb6e-126">Domyślnie hello łącznika zarządzania usługi IT odświeża dane połączenia hello raz w co 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-126">By default, hello IT Service Management Connector refreshes hello connection's data once in every 24 hours.</span></span> <span data-ttu-id="3fb6e-127">toorefresh tego połączenia danych natychmiast dla wszystkich edycji lub szablon aktualizacji, które zostaną wprowadzone, kliknij przycisk hello odświeżania wyświetlany przycisk następnej tooyour połączenie.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-127">toorefresh your connection's data instantly for any edits or template updates that you make, click hello refresh button displayed next tooyour connection.</span></span>

 ![Odśwież ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="3fb6e-129">Pakiety administracyjne</span><span class="sxs-lookup"><span data-stu-id="3fb6e-129">Management packs</span></span>
<span data-ttu-id="3fb6e-130">To rozwiązanie nie wymaga żadnych pakietów administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="3fb6e-131">Połączone źródła</span><span class="sxs-lookup"><span data-stu-id="3fb6e-131">Connected sources</span></span>

<span data-ttu-id="3fb6e-132">Witaj następujących produktów/usług Zarządzanie usługami IT — są obsługiwane przez hello łącznika zarządzania usługi IT:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-132">hello following ITSM products/services are supported by hello IT Service Management Connector:</span></span>

- [<span data-ttu-id="3fb6e-133">Program System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="3fb6e-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="3fb6e-134">Usługi ServiceNow</span><span class="sxs-lookup"><span data-stu-id="3fb6e-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="3fb6e-135">Provance</span><span class="sxs-lookup"><span data-stu-id="3fb6e-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="3fb6e-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="3fb6e-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a><span data-ttu-id="3fb6e-137">Za pomocą rozwiązania hello</span><span class="sxs-lookup"><span data-stu-id="3fb6e-137">Using hello solution</span></span>

<span data-ttu-id="3fb6e-138">Po podłączeniu hello OMS IT usługi zarządzania łącznika z usługą Zarządzanie usługami IT — usługi analizy dzienników hello rozpoczyna zbieranie danych hello z Zarządzanie usługami IT — hello połączone produktów/usług.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-138">Once you connect hello OMS IT Service Management Connector with your ITSM service, hello Log Analytics services starts gathering hello data from hello connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="3fb6e-139">Dane importowane przez rozwiązanie łącznika zarządzania usługi IT pojawia się w analizy dziennika jako zdarzenia o nazwie **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="3fb6e-140">Zdarzenie zawiera pole o nazwie **ServiceDeskWorkItemType_s**.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="3fb6e-141">które wykonać jego wartość, jak zdarzenia lub żądania zmiany, w zależności od hello elementu roboczego dane zawarte w hello **ServiceDesk_CL** zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-141">which can take its value as incident, or change request, depending on hello work item data contained in hello **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="3fb6e-142">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="3fb6e-142">Input data</span></span>
<span data-ttu-id="3fb6e-143">Elementy robocze zaimportowane z hello Zarządzanie usługami IT — produktów/usług.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-143">Work items imported from hello ITSM products/services.</span></span>

<span data-ttu-id="3fb6e-144">Witaj następujące informacje znajdują się przykładowe dane zebrane przez łącznik zarządzania usługami INFORMATYCZNYMI hello:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-144">hello following information shows examples of data gathered by hello IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="3fb6e-145">W zależności od hello typu elementu roboczego zaimportowane do analizy dzienników **ServiceDesk_CL** zawiera hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-145">Depending on hello work item type imported into Log Analytics, **ServiceDesk_CL** contains hello following fields:</span></span>

<span data-ttu-id="3fb6e-146">**Element pracy:** **zdarzenia**</span><span class="sxs-lookup"><span data-stu-id="3fb6e-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="3fb6e-147">ServiceDeskWorkItemType_s = "Zdarzenie"</span><span class="sxs-lookup"><span data-stu-id="3fb6e-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="3fb6e-148">**Pola**</span><span class="sxs-lookup"><span data-stu-id="3fb6e-148">**Fields**</span></span>

- <span data-ttu-id="3fb6e-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="3fb6e-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="3fb6e-150">Identyfikator technicznej usługi</span><span class="sxs-lookup"><span data-stu-id="3fb6e-150">Service Desk ID</span></span>
- <span data-ttu-id="3fb6e-151">Stan</span><span class="sxs-lookup"><span data-stu-id="3fb6e-151">State</span></span>
- <span data-ttu-id="3fb6e-152">Pilności</span><span class="sxs-lookup"><span data-stu-id="3fb6e-152">Urgency</span></span>
- <span data-ttu-id="3fb6e-153">Wpływ</span><span class="sxs-lookup"><span data-stu-id="3fb6e-153">Impact</span></span>
- <span data-ttu-id="3fb6e-154">Priorytet</span><span class="sxs-lookup"><span data-stu-id="3fb6e-154">Priority</span></span>
- <span data-ttu-id="3fb6e-155">Eskalacja</span><span class="sxs-lookup"><span data-stu-id="3fb6e-155">Escalation</span></span>
- <span data-ttu-id="3fb6e-156">Utworzone przez</span><span class="sxs-lookup"><span data-stu-id="3fb6e-156">Created By</span></span>
- <span data-ttu-id="3fb6e-157">Rozwiązany przez</span><span class="sxs-lookup"><span data-stu-id="3fb6e-157">Resolved By</span></span>
- <span data-ttu-id="3fb6e-158">Zamknięte przez</span><span class="sxs-lookup"><span data-stu-id="3fb6e-158">Closed By</span></span>
- <span data-ttu-id="3fb6e-159">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="3fb6e-159">Source</span></span>
- <span data-ttu-id="3fb6e-160">Przypisane do</span><span class="sxs-lookup"><span data-stu-id="3fb6e-160">Assigned To</span></span>
- <span data-ttu-id="3fb6e-161">Kategoria</span><span class="sxs-lookup"><span data-stu-id="3fb6e-161">Category</span></span>
- <span data-ttu-id="3fb6e-162">Tytuł</span><span class="sxs-lookup"><span data-stu-id="3fb6e-162">Title</span></span>
- <span data-ttu-id="3fb6e-163">Opis</span><span class="sxs-lookup"><span data-stu-id="3fb6e-163">Description</span></span>
- <span data-ttu-id="3fb6e-164">Data utworzenia</span><span class="sxs-lookup"><span data-stu-id="3fb6e-164">Created Date</span></span>
- <span data-ttu-id="3fb6e-165">Data zamknięcia</span><span class="sxs-lookup"><span data-stu-id="3fb6e-165">Closed Date</span></span>
- <span data-ttu-id="3fb6e-166">Data rozwiązania</span><span class="sxs-lookup"><span data-stu-id="3fb6e-166">Resolved Date</span></span>
- <span data-ttu-id="3fb6e-167">Data ostatniej modyfikacji</span><span class="sxs-lookup"><span data-stu-id="3fb6e-167">Last Modified Date</span></span>
- <span data-ttu-id="3fb6e-168">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="3fb6e-168">Computer</span></span>


<span data-ttu-id="3fb6e-169">**Element pracy:** **żądania zmiany**</span><span class="sxs-lookup"><span data-stu-id="3fb6e-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="3fb6e-170">ServiceDeskWorkItemType_s = "Żądanie zmiany"</span><span class="sxs-lookup"><span data-stu-id="3fb6e-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="3fb6e-171">**Pola**</span><span class="sxs-lookup"><span data-stu-id="3fb6e-171">**Fields**</span></span>
- <span data-ttu-id="3fb6e-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="3fb6e-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="3fb6e-173">Identyfikator technicznej usługi</span><span class="sxs-lookup"><span data-stu-id="3fb6e-173">Service Desk ID</span></span>
- <span data-ttu-id="3fb6e-174">Utworzone przez</span><span class="sxs-lookup"><span data-stu-id="3fb6e-174">Created By</span></span>
- <span data-ttu-id="3fb6e-175">Zamknięte przez</span><span class="sxs-lookup"><span data-stu-id="3fb6e-175">Closed By</span></span>
- <span data-ttu-id="3fb6e-176">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="3fb6e-176">Source</span></span>
- <span data-ttu-id="3fb6e-177">Przypisane do</span><span class="sxs-lookup"><span data-stu-id="3fb6e-177">Assigned To</span></span>
- <span data-ttu-id="3fb6e-178">Tytuł</span><span class="sxs-lookup"><span data-stu-id="3fb6e-178">Title</span></span>
- <span data-ttu-id="3fb6e-179">Typ</span><span class="sxs-lookup"><span data-stu-id="3fb6e-179">Type</span></span>
- <span data-ttu-id="3fb6e-180">Kategoria</span><span class="sxs-lookup"><span data-stu-id="3fb6e-180">Category</span></span>
- <span data-ttu-id="3fb6e-181">Stan</span><span class="sxs-lookup"><span data-stu-id="3fb6e-181">State</span></span>
- <span data-ttu-id="3fb6e-182">Eskalacja</span><span class="sxs-lookup"><span data-stu-id="3fb6e-182">Escalation</span></span>
- <span data-ttu-id="3fb6e-183">Konflikt stanu</span><span class="sxs-lookup"><span data-stu-id="3fb6e-183">Conflict Status</span></span>
- <span data-ttu-id="3fb6e-184">Pilności</span><span class="sxs-lookup"><span data-stu-id="3fb6e-184">Urgency</span></span>
- <span data-ttu-id="3fb6e-185">Priorytet</span><span class="sxs-lookup"><span data-stu-id="3fb6e-185">Priority</span></span>
- <span data-ttu-id="3fb6e-186">Ryzyko</span><span class="sxs-lookup"><span data-stu-id="3fb6e-186">Risk</span></span>
- <span data-ttu-id="3fb6e-187">Wpływ</span><span class="sxs-lookup"><span data-stu-id="3fb6e-187">Impact</span></span>
- <span data-ttu-id="3fb6e-188">Przypisane do</span><span class="sxs-lookup"><span data-stu-id="3fb6e-188">Assigned To</span></span>
- <span data-ttu-id="3fb6e-189">Data utworzenia</span><span class="sxs-lookup"><span data-stu-id="3fb6e-189">Created Date</span></span>
- <span data-ttu-id="3fb6e-190">Data zamknięcia</span><span class="sxs-lookup"><span data-stu-id="3fb6e-190">Closed Date</span></span>
- <span data-ttu-id="3fb6e-191">Data ostatniej modyfikacji</span><span class="sxs-lookup"><span data-stu-id="3fb6e-191">Last Modified Date</span></span>
- <span data-ttu-id="3fb6e-192">Żądana data</span><span class="sxs-lookup"><span data-stu-id="3fb6e-192">Requested Date</span></span>
- <span data-ttu-id="3fb6e-193">Planowana data rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="3fb6e-193">Planned Start Date</span></span>
- <span data-ttu-id="3fb6e-194">Planowana data zakończenia</span><span class="sxs-lookup"><span data-stu-id="3fb6e-194">Planned End Date</span></span>
- <span data-ttu-id="3fb6e-195">Data rozpoczęcia pracy</span><span class="sxs-lookup"><span data-stu-id="3fb6e-195">Work Start Date</span></span>
- <span data-ttu-id="3fb6e-196">Data zakończenia pracy</span><span class="sxs-lookup"><span data-stu-id="3fb6e-196">Work End Date</span></span>
- <span data-ttu-id="3fb6e-197">Opis</span><span class="sxs-lookup"><span data-stu-id="3fb6e-197">Description</span></span>
- <span data-ttu-id="3fb6e-198">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="3fb6e-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="3fb6e-199">Dane wyjściowe dla zdarzenia usługi ServiceNow</span><span class="sxs-lookup"><span data-stu-id="3fb6e-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="3fb6e-200">Pole OMS</span><span class="sxs-lookup"><span data-stu-id="3fb6e-200">OMS field</span></span> | <span data-ttu-id="3fb6e-201">Zarządzanie usługami IT — pola</span><span class="sxs-lookup"><span data-stu-id="3fb6e-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="3fb6e-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-202">ServiceDeskId_s</span></span>| <span data-ttu-id="3fb6e-203">Liczba</span><span class="sxs-lookup"><span data-stu-id="3fb6e-203">Number</span></span> |
| <span data-ttu-id="3fb6e-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-204">IncidentState_s</span></span> | <span data-ttu-id="3fb6e-205">Stan</span><span class="sxs-lookup"><span data-stu-id="3fb6e-205">State</span></span> |
| <span data-ttu-id="3fb6e-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-206">Urgency_s</span></span> |<span data-ttu-id="3fb6e-207">Pilności</span><span class="sxs-lookup"><span data-stu-id="3fb6e-207">Urgency</span></span> |
| <span data-ttu-id="3fb6e-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-208">Impact_s</span></span> |<span data-ttu-id="3fb6e-209">Wpływ</span><span class="sxs-lookup"><span data-stu-id="3fb6e-209">Impact</span></span>|
| <span data-ttu-id="3fb6e-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-210">Priority_s</span></span> | <span data-ttu-id="3fb6e-211">Priorytet</span><span class="sxs-lookup"><span data-stu-id="3fb6e-211">Priority</span></span> |
| <span data-ttu-id="3fb6e-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-212">CreatedBy_s</span></span> | <span data-ttu-id="3fb6e-213">Otwarty przez</span><span class="sxs-lookup"><span data-stu-id="3fb6e-213">Opened by</span></span> |
| <span data-ttu-id="3fb6e-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-214">ResolvedBy_s</span></span> | <span data-ttu-id="3fb6e-215">Rozwiązany przez</span><span class="sxs-lookup"><span data-stu-id="3fb6e-215">Resolved by</span></span>|
| <span data-ttu-id="3fb6e-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-216">ClosedBy_s</span></span>  | <span data-ttu-id="3fb6e-217">Zamknięte przez</span><span class="sxs-lookup"><span data-stu-id="3fb6e-217">Closed by</span></span> |
| <span data-ttu-id="3fb6e-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-218">Source_s</span></span>| <span data-ttu-id="3fb6e-219">Skontaktuj się z typu</span><span class="sxs-lookup"><span data-stu-id="3fb6e-219">Contact type</span></span> |
| <span data-ttu-id="3fb6e-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-220">AssignedTo_s</span></span> | <span data-ttu-id="3fb6e-221">Zbyt przypisany</span><span class="sxs-lookup"><span data-stu-id="3fb6e-221">Assigned too</span></span> |
| <span data-ttu-id="3fb6e-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-222">Category_s</span></span> | <span data-ttu-id="3fb6e-223">Kategoria</span><span class="sxs-lookup"><span data-stu-id="3fb6e-223">Category</span></span> |
| <span data-ttu-id="3fb6e-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-224">Title_s</span></span>|  <span data-ttu-id="3fb6e-225">Krótki opis</span><span class="sxs-lookup"><span data-stu-id="3fb6e-225">Short description</span></span> |
| <span data-ttu-id="3fb6e-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-226">Description_s</span></span>|  <span data-ttu-id="3fb6e-227">Uwagi</span><span class="sxs-lookup"><span data-stu-id="3fb6e-227">Notes</span></span> |
| <span data-ttu-id="3fb6e-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="3fb6e-228">CreatedDate_t</span></span>|  <span data-ttu-id="3fb6e-229">Otwarte</span><span class="sxs-lookup"><span data-stu-id="3fb6e-229">Opened</span></span> |
| <span data-ttu-id="3fb6e-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="3fb6e-230">ClosedDate_t</span></span>| <span data-ttu-id="3fb6e-231">zamknięte</span><span class="sxs-lookup"><span data-stu-id="3fb6e-231">closed</span></span>|
| <span data-ttu-id="3fb6e-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="3fb6e-232">ResolvedDate_t</span></span>|<span data-ttu-id="3fb6e-233">Rozwiązane</span><span class="sxs-lookup"><span data-stu-id="3fb6e-233">Resolved</span></span>|
| <span data-ttu-id="3fb6e-234">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="3fb6e-234">Computer</span></span>  | <span data-ttu-id="3fb6e-235">element konfiguracji</span><span class="sxs-lookup"><span data-stu-id="3fb6e-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="3fb6e-236">Dane wyjściowe dla usługi ServiceNow żądania zmiany</span><span class="sxs-lookup"><span data-stu-id="3fb6e-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="3fb6e-237">Pole OMS</span><span class="sxs-lookup"><span data-stu-id="3fb6e-237">OMS field</span></span> | <span data-ttu-id="3fb6e-238">Zarządzanie usługami IT — pola</span><span class="sxs-lookup"><span data-stu-id="3fb6e-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="3fb6e-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-239">ServiceDeskId_s</span></span>| <span data-ttu-id="3fb6e-240">Liczba</span><span class="sxs-lookup"><span data-stu-id="3fb6e-240">Number</span></span> |
| <span data-ttu-id="3fb6e-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-241">CreatedBy_s</span></span> | <span data-ttu-id="3fb6e-242">Żądanie</span><span class="sxs-lookup"><span data-stu-id="3fb6e-242">Requested by</span></span> |
| <span data-ttu-id="3fb6e-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-243">ClosedBy_s</span></span> | <span data-ttu-id="3fb6e-244">Zamknięte przez</span><span class="sxs-lookup"><span data-stu-id="3fb6e-244">Closed by</span></span> |
| <span data-ttu-id="3fb6e-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-245">AssignedTo_s</span></span> | <span data-ttu-id="3fb6e-246">Zbyt przypisany</span><span class="sxs-lookup"><span data-stu-id="3fb6e-246">Assigned too</span></span> |
| <span data-ttu-id="3fb6e-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-247">Title_s</span></span>|  <span data-ttu-id="3fb6e-248">Krótki opis</span><span class="sxs-lookup"><span data-stu-id="3fb6e-248">Short description</span></span> |
| <span data-ttu-id="3fb6e-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-249">Type_s</span></span>|  <span data-ttu-id="3fb6e-250">Typ</span><span class="sxs-lookup"><span data-stu-id="3fb6e-250">Type</span></span> |
| <span data-ttu-id="3fb6e-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-251">Category_s</span></span>|  <span data-ttu-id="3fb6e-252">Catgory</span><span class="sxs-lookup"><span data-stu-id="3fb6e-252">Catgory</span></span> |
| <span data-ttu-id="3fb6e-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-253">CRState_s</span></span>|  <span data-ttu-id="3fb6e-254">Stan</span><span class="sxs-lookup"><span data-stu-id="3fb6e-254">State</span></span>|
| <span data-ttu-id="3fb6e-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-255">Urgency_s</span></span>|  <span data-ttu-id="3fb6e-256">Pilności</span><span class="sxs-lookup"><span data-stu-id="3fb6e-256">Urgency</span></span> |
| <span data-ttu-id="3fb6e-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-257">Priority_s</span></span>| <span data-ttu-id="3fb6e-258">Priorytet</span><span class="sxs-lookup"><span data-stu-id="3fb6e-258">Priority</span></span>|
| <span data-ttu-id="3fb6e-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-259">Risk_s</span></span>| <span data-ttu-id="3fb6e-260">Ryzyko</span><span class="sxs-lookup"><span data-stu-id="3fb6e-260">Risk</span></span>|
| <span data-ttu-id="3fb6e-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-261">Impact_s</span></span>| <span data-ttu-id="3fb6e-262">Wpływ</span><span class="sxs-lookup"><span data-stu-id="3fb6e-262">Impact</span></span>|
| <span data-ttu-id="3fb6e-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="3fb6e-263">RequestedDate_t</span></span>  | <span data-ttu-id="3fb6e-264">Żądana według daty</span><span class="sxs-lookup"><span data-stu-id="3fb6e-264">Requested by date</span></span> |
| <span data-ttu-id="3fb6e-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="3fb6e-265">ClosedDate_t</span></span> | <span data-ttu-id="3fb6e-266">Data zamknięcia</span><span class="sxs-lookup"><span data-stu-id="3fb6e-266">Closed date</span></span> |
| <span data-ttu-id="3fb6e-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="3fb6e-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="3fb6e-268">Planowana data rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="3fb6e-268">Planned start date</span></span> |
| <span data-ttu-id="3fb6e-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="3fb6e-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="3fb6e-270">Planowana data zakończenia</span><span class="sxs-lookup"><span data-stu-id="3fb6e-270">Planned end date</span></span> |
| <span data-ttu-id="3fb6e-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="3fb6e-271">WorkStartDate_t</span></span>  | <span data-ttu-id="3fb6e-272">Rzeczywista data rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="3fb6e-272">Actual start date</span></span> |
| <span data-ttu-id="3fb6e-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="3fb6e-273">WorkEndDate_t</span></span> | <span data-ttu-id="3fb6e-274">Rzeczywista data zakończenia</span><span class="sxs-lookup"><span data-stu-id="3fb6e-274">Actual end date</span></span>|
| <span data-ttu-id="3fb6e-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="3fb6e-275">Description_s</span></span> | <span data-ttu-id="3fb6e-276">Opis</span><span class="sxs-lookup"><span data-stu-id="3fb6e-276">Description</span></span> |
| <span data-ttu-id="3fb6e-277">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="3fb6e-277">Computer</span></span>  | <span data-ttu-id="3fb6e-278">Element konfiguracji</span><span class="sxs-lookup"><span data-stu-id="3fb6e-278">Configuration Item</span></span> |

<span data-ttu-id="3fb6e-279">**Przykładowy ekran analizy dzienników dla danych Zarządzanie usługami IT —:**</span><span class="sxs-lookup"><span data-stu-id="3fb6e-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Ekran analiza dziennika](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="3fb6e-281">Łącznik zarządzania usługami IT — Integracja z innych rozwiązań pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="3fb6e-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="3fb6e-282">Łącznik zarządzania usługi IT, obecnie obsługuje integrację z hello rozwiązania mapy usługi.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-282">IT Service Management Connector, currently supports integration with hello Service Map solution.</span></span>

<span data-ttu-id="3fb6e-283">Mapa usług automatycznie odnajduje hello składniki aplikacji w systemie Windows i systemów Linux i map hello komunikacji między usługami.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-283">Service Map automatically discovers hello application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="3fb6e-284">Pozwala ona tooview serwerów jako należy wziąć pod uwagę z nich — jako połączonych systemy, które dostarczają usług krytycznych.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-284">It allows you tooview your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="3fb6e-285">Mapy usługi pokazuje połączeń między serwerami, procesów, i portów w dowolnej architekturze połączenia TCP z konfiguracji wymagane inne niż instalacji agenta.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="3fb6e-286">Więcej informacji: [mapy usługi](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="3fb6e-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="3fb6e-287">Z tej integracji można wyświetlać elementy technicznej usług hello utworzone w hello Zarządzanie usługami IT — rozwiązania, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-287">With this integration, you can view hello service desk items created in hello ITSM solutions as shown in hello following example:</span></span>

![<span data-ttu-id="3fb6e-288">Zintegrowane rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="3fb6e-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="3fb6e-289">Tworzenie elementów roboczych Zarządzanie usługami IT — OMS alertów</span><span class="sxs-lookup"><span data-stu-id="3fb6e-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="3fb6e-290">Hello OMS alertów można utworzyć skojarzonych elementów roboczych w źródłach Zarządzanie usługami IT — Witaj połączony.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-290">For hello OMS alerts, you can create associated work items in hello connected ITSM sources.</span></span>  <span data-ttu-id="3fb6e-291">toodo tego hello użyj następującej procedury:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-291">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="3fb6e-292">Z **wyszukiwania dziennika** okna danych tooview zapytania wyszukiwania dziennika jest uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-292">From **Log Search** window, run a log search query tooview data.</span></span> <span data-ttu-id="3fb6e-293">Wyniki zapytania są źródłem powitania dla elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-293">Query results are hello source for work items.</span></span>
2. <span data-ttu-id="3fb6e-294">W **wyszukiwania dziennika**, kliknij przycisk **alertu** tooopen hello **Dodaj regułę alertu** strony.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-294">In **Log Search**, click **Alert** tooopen hello **Add Alert Rule** page.</span></span>

    ![Ekran analiza dziennika](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="3fb6e-296">Na powitania **Dodaj regułę alertu** okna, podaj szczegóły hello wymagane **nazwa**, **ważność**, **zapytania wyszukiwania**, i  **Kryteria alertu** (pomiar Metryka okno czasu).</span><span class="sxs-lookup"><span data-stu-id="3fb6e-296">On hello **Add Alert Rule** window, provide hello required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="3fb6e-297">Wybierz **tak** dla **akcje Zarządzanie usługami IT —**.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="3fb6e-298">Wybierz połączenie Zarządzanie usługami IT — od hello **połączenia wybierz** listy.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-298">Select your ITSM connection from hello **Select Connection** list.</span></span>
6. <span data-ttu-id="3fb6e-299">Podaj szczegóły hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-299">Provide hello details as required.</span></span>
7. <span data-ttu-id="3fb6e-300">toocreate elementu roboczego osobne dla każdego wpisu dziennika z tym hello alertów, wybierz pozycję **utworzyć poszczególnych elementach roboczych dla każdego wpisu dziennika** wyboru.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-300">toocreate a separate work item for each log entry of this alert, select hello **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="3fb6e-301">Lub</span><span class="sxs-lookup"><span data-stu-id="3fb6e-301">Or</span></span>

    <span data-ttu-id="3fb6e-302">Pozostaw to pole wyboru niezaznaczone toocreate tylko jednego elementu roboczego dla dowolnej liczby wpisów dziennika w ramach tego alertu.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-302">leave this checkbox unselected toocreate only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="3fb6e-303">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-303">Click **Save**.</span></span>

<span data-ttu-id="3fb6e-304">Hello OMS alert zostaną utworzone w obszarze **alerty**.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-304">hello OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="3fb6e-305">Witaj pracy odpowiedniego połączenia Zarządzanie usługami IT — elementy są tworzone po spełnieniu warunku hello określony alert.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-305">hello corresponding ITSM connection's work items are created when hello specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="3fb6e-306">Tworzenie elementów roboczych Zarządzanie usługami IT — z dzienników OMS</span><span class="sxs-lookup"><span data-stu-id="3fb6e-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="3fb6e-307">Można utworzyć elementów roboczych w źródłach Zarządzanie usługami IT — Witaj połączone za pomocą wyszukiwania dziennika OMS.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-307">You can create work items in hello connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="3fb6e-308">toodo tego hello użyj następującej procedury:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-308">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="3fb6e-309">Z **wyszukiwania dziennika**, wyszukiwanie danych hello wymagane, wybierz hello szczegółów, a następnie kliknij przycisk **Utwórz element roboczy**.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-309">From **Log Search**,  search hello required data, select hello detail, and click **Create work item**.</span></span>

    <span data-ttu-id="3fb6e-310">Witaj **elementu roboczego Zarządzanie usługami IT — tworzenie** zostanie wyświetlone okno:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-310">hello **Create ITSM Work item** window appears:</span></span>

    ![Ekran analiza dziennika](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="3fb6e-312">Dodaj hello poniższe informacje:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-312">Add hello following details:</span></span>

  - <span data-ttu-id="3fb6e-313">**Tytuł elementu pracy**: tytuł dla elementu roboczego hello.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-313">**Work item Title**: Title for hello work item.</span></span>
  - <span data-ttu-id="3fb6e-314">**Opis elementu roboczego**: opis hello nowego elementu roboczego.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-314">**Work item Description**: Description for hello new work item.</span></span>
  - <span data-ttu-id="3fb6e-315">**Wpływ na komputerze**: Nazwa komputera hello, gdzie te dane dziennika został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-315">**Affected Computer**: Name of hello computer where this log data was found.</span></span>
  - <span data-ttu-id="3fb6e-316">**Wybierz połączenie**: Zarządzanie usługami IT — połączenie, w którym chcesz toocreate tego elementu roboczego.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-316">**Select Connection**:  ITSM connection in which you want toocreate this work item.</span></span>
  - <span data-ttu-id="3fb6e-317">**Element roboczy**: typ elementu roboczego.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="3fb6e-318">toouse istniejącego szablonu elementu pracy zdarzenia, kliknij przycisk **tak** w obszarze **Generuj element pracy oparty na szablonie hello** opcji, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-318">toouse an existing work item template for an incident, click **Yes** under **Generate work item based on hello template** option and then click **Create**.</span></span>

    <span data-ttu-id="3fb6e-319">Lub:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-319">Or,</span></span>

    <span data-ttu-id="3fb6e-320">Kliknij przycisk **nr** Jeśli chcesz tooprovide dostosowanych wartości.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-320">Click **No** if you want tooprovide your customized values.</span></span>

4. <span data-ttu-id="3fb6e-321">Podaj odpowiednie wartości hello w hello **typ**, **wpływ**, **pilność**, **kategorii**, i **podkategorii**  pola tekstowe, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-321">Provide hello appropriate values in hello **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="3fb6e-322">element roboczy Hello zostaną utworzone w hello Zarządzanie usługami IT —, które można również wyświetlić OMS.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-322">hello work item will be created in hello ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="3fb6e-323">Rozwiązywanie problemów z połączeniami Zarządzanie usługami IT — w OMS</span><span class="sxs-lookup"><span data-stu-id="3fb6e-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="3fb6e-324">Jeśli połączenie nie powiedzie się z połączonych źródła interfejsu użytkownika i pobrać hello **błąd podczas zapisywania połączenia** komunikatów, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-324">If connection fails from connected source's UI and you get hello **Error in saving connection** message, do hello following:</span></span>
 - <span data-ttu-id="3fb6e-325">W przypadku połączenia usługi ServiceNow, Cherwell i Provance upewnij się, możesz hello prawidłowo wprowadzić nazwę użytkownika/hasło i klienta identyfikator/klucz tajny klienta dla każdego połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  hello username/password and  client ID/client secret  for each of hello connections.</span></span> <span data-ttu-id="3fb6e-326">Jeśli hello błąd będzie się powtarzał, sprawdź, czy masz wystarczające uprawnienia w hello odpowiednie zarządzanie usługami IT — produktu toomake hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-326">If hello error persists, check if you have sufficient privileges  in hello corresponding ITSM product toomake hello connection.</span></span>
 - <span data-ttu-id="3fb6e-327">W przypadku programu Service Manager, sprawdź, czy aplikacja sieci Web powitania po pomyślnym wdrożeniu i utworzono połączenie hybrydowe.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-327">In case of Service Manager, ensure that hello Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="3fb6e-328">pomyślnie jest nawiązywane połączenie hello tooverify z hello lokalnego programu Service Manager maszyny, odwiedź adres URL aplikacji sieci Web hello zgodnie z opisem w dokumentacji hello dokonywania hello [połączenia hybrydowego](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="3fb6e-328">tooverify hello connection is successfully established with hello on-prem Service Manager machine, visit hello  Web app URL as detailed in hello documentation for making hello [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="3fb6e-329">Jeśli dane z usługi ServiceNow nie jest pierwsze zsynchronizowane w OMS, upewnij się, że to wystąpienie usługi ServiceNow hello nie jest uśpiony.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-329">If data from ServiceNow is not getting synced in OMS, ensure that hello ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="3fb6e-330">Taka sytuacja może chwilę wystąpić w hello wystąpień usługi ServiceNow deweloperów, po bezczynności.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-330">This might sometime happen in hello ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="3fb6e-331">Else, zgłoś problem hello.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-331">Else, report hello issue.</span></span>
3.  <span data-ttu-id="3fb6e-332">Jeśli alerty pobierania uruchomienia z pakietu OMS, ale nie pobierania utworzonych elementów roboczych w zarządzanie usługami IT — produktu lub elementy konfiguracji nie otrzymują toowork utworzone połączone elementy lub wszelkie informacje ogólne, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3fb6e-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked toowork items or for any generic information, do hello following:</span></span>
 -  <span data-ttu-id="3fb6e-333">Rozwiązanie usługi zarządzania łącznika IT w portalu OMS może być używane tooget podsumowanie połączeń/pracy elementów/komputerów itp. Komunikat o błędzie hello w bloku stanu powitania kliknij kolejno zbyt**wyszukiwania dziennika** i wyświetlić hello połączenie, które zawiera błąd hello przy użyciu okna Szczegóły hello w komunikacie o błędzie hello.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-333">IT Service Management Connector solution in OMS portal could be used tooget a summary of connections/work items/computers etc. Click hello error message in hello status blade, navigate too**Log Search** and view hello connection that has hello error by using hello details in hello error message.</span></span>
 - <span data-ttu-id="3fb6e-334">informacje związane z/błędy hello bezpośrednio można wyświetlić w hello **wyszukiwania dziennika** strony *typu = ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-334">you can directly view hello errors/related information in hello **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="3fb6e-335">Rozwiązywanie problemów z wdrażaniem aplikacji sieci Web programu Service Manager</span><span class="sxs-lookup"><span data-stu-id="3fb6e-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="3fb6e-336">W przypadku problemów z wdrożeniem aplikacji sieci web upewnij się, masz wystarczające uprawnienia w subskrypcji hello wymienionych toocreate/wdrażanie zasobów.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in hello subscription mentioned toocreate/deploy resources.</span></span>
2.  <span data-ttu-id="3fb6e-337">Jeśli **odwołania do obiektu nie jest ustawiony tooinstance obiektu** komunikat o błędzie jest wyświetlany podczas uruchamiania hello [skryptu](log-analytics-itsmc-service-manager-script.md) upewnij się, że wprowadzono prawidłowe wartości w obszarze **Konfiguracja użytkownika**sekcji.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-337">If **Object reference not set tooinstance of an object** error message appears while running hello [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="3fb6e-338">Jeśli nie zostanie toocreate przestrzeń nazw przekaźnik magistrali usług, upewnij się, że dostawca zasobów jest zarejestrowane w subskrypcji hello wymagane tego hello.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-338">If you fail toocreate service bus relay namespace, ensure that hello required resource provider is registered in hello subscription.</span></span> <span data-ttu-id="3fb6e-339">Jeśli nie jest zarejestrowany, ręcznie utwórz je z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-339">If not registered, manually create it from hello Azure portal.</span></span> <span data-ttu-id="3fb6e-340">Można również utworzyć go podczas [Tworzenie połączenia hybrydowego hello](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3fb6e-340">You can also create it while [creating hello hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from hello Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="3fb6e-341">Skontaktuj się z nami</span><span class="sxs-lookup"><span data-stu-id="3fb6e-341">Contact us</span></span>

<span data-ttu-id="3fb6e-342">Dla zapytania lub opinie na powitania łącznika zarządzania usługi IT, skontaktuj się z nami pod adresem [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="3fb6e-342">For any queries or feedback on hello IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fb6e-343">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3fb6e-343">Next steps</span></span>
<span data-ttu-id="3fb6e-344">[Dodaj tooIT produktów i usług Zarządzanie usługami IT — usługi zarządzania łącznika](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="3fb6e-344">[Add ITSM products/services tooIT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
