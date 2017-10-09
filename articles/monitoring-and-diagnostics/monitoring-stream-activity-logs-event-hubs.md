---
title: "aaaStream hello dziennika aktywności platformy Azure tooEvent koncentratory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toostream hello tooEvent dziennika aktywności platformy Azure koncentratorów."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a><span data-ttu-id="8151a-103">Strumienia tooEvent dziennika aktywności platformy Azure hello koncentratory</span><span class="sxs-lookup"><span data-stu-id="8151a-103">Stream hello Azure Activity Log tooEvent Hubs</span></span>
<span data-ttu-id="8151a-104">Witaj [ **dziennika aktywności platformy Azure** ](monitoring-overview-activity-logs.md) mogą być przesyłane strumieniowo w niemal w czasie rzeczywistym tooany aplikacji przy użyciu wbudowanych opcji "Eksportuj" hello, w portalu hello lub przez włączenie hello identyfikator reguły magistrali usług w profilu dziennika za pomocą hello Polecenia cmdlet programu PowerShell systemu Azure lub Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8151a-104">hello [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time tooany application using hello built-in “Export” option in hello portal, or by enabling hello Service Bus Rule Id in a Log Profile via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a><span data-ttu-id="8151a-105">Co można zrobić z hello dziennika aktywności i usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8151a-105">What you can do with hello Activity Log and Event Hubs</span></span>
<span data-ttu-id="8151a-106">Poniżej przedstawiono kilka sposobów może używać hello przesyłania strumieniowego dla hello dziennik aktywności możliwości:</span><span class="sxs-lookup"><span data-stu-id="8151a-106">Here are just a few ways you might use hello streaming capability for hello Activity Log:</span></span>

* <span data-ttu-id="8151a-107">**Strumienia systemów firm toothird rejestrowania i dane telemetryczne** — wraz z upływem czasu przesyłania strumieniowego usługi Event Hubs ma zostać toopipe mechanizmu hello dziennik aktywności w innych rozwiązań Siem a dziennika rozwiązań analitycznych.</span><span class="sxs-lookup"><span data-stu-id="8151a-107">**Stream toothird-party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="8151a-108">**Tworzenie niestandardowych telemetrii i rejestrowanie platformy** — Jeśli masz już platformy telemetrii niestandardowej lub są po prostu pomyśleć o budynku jedną hello skalowalnej publikowania / subskrypcji rodzaj usługi Event Hubs umożliwia tooflexibly pozyskiwania hello Dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="8151a-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest hello activity log.</span></span> [<span data-ttu-id="8151a-109">Zobacz Dan Rosanova przewodnik toousing centra zdarzeń w skali globalnej platformy telemetrii w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="8151a-109">See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a><span data-ttu-id="8151a-110">Przesyłania strumieniowego hello dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="8151a-110">Enable streaming of hello Activity Log</span></span>
<span data-ttu-id="8151a-111">Umożliwiają przesyłanie strumieniowe hello dziennik aktywności programowo lub za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="8151a-111">You can enable streaming of hello Activity Log either programmatically or via hello portal.</span></span> <span data-ttu-id="8151a-112">W obu przypadkach wybierz Namespace magistrali usługi i zasady dostępu współdzielonego dla tej przestrzeni nazw i Centrum zdarzeń jest tworzony w tej przestrzeni nazw, po wystąpieniu zdarzenia dziennika aktywności nowe pierwszy hello.</span><span class="sxs-lookup"><span data-stu-id="8151a-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when hello first new Activity Log event occurs.</span></span> <span data-ttu-id="8151a-113">Jeśli nie masz Namespace magistrali usług, należy najpierw toocreate jeden.</span><span class="sxs-lookup"><span data-stu-id="8151a-113">If you do not have a Service Bus Namespace, you first need toocreate one.</span></span> <span data-ttu-id="8151a-114">Jeśli wcześniej zostały strumieniowo toothis zdarzenia dziennika aktywności Namespace magistrali usług, hello Centrum zdarzeń, która została wcześniej utworzona zostanie ono użyte ponownie.</span><span class="sxs-lookup"><span data-stu-id="8151a-114">If you have previously streamed Activity Log events toothis Service Bus Namespace, hello Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="8151a-115">zasady dostępu Hello udostępnionych definiuje hello uprawnienia hello mechanizm przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="8151a-115">hello shared access policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="8151a-116">Obecnie wymaga przesyłania strumieniowego usługi Event Hubs tooan **Zarządzaj**, **wysyłania**, i **nasłuchiwania** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="8151a-116">Today, streaming tooan Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="8151a-117">Można utworzyć lub zmodyfikować zasady dostępu Namespace magistrali usług udostępnionych w portalu klasycznym hello karcie "Konfiguruj" hello dla Twojego Namespace magistrali usługi.</span><span class="sxs-lookup"><span data-stu-id="8151a-117">You can create or modify Service Bus Namespace shared access policies in hello classic portal under hello “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="8151a-118">tooupdate hello dziennik aktywności dziennika profilu tooinclude przesyłania strumieniowego, użytkownik hello wprowadzeniu zmiany hello musi mieć uprawnienie ListKey hello w tej regule autoryzacji magistrali usługi.</span><span class="sxs-lookup"><span data-stu-id="8151a-118">tooupdate hello Activity Log log profile tooinclude streaming, hello user making hello change must have hello ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="8151a-119">Witaj bus lub event hub przestrzeni nazw usługi nie ma toobe w hello tej samej subskrypcji co subskrypcji hello emitowanie dzienniki tak długo, jak hello użytkownik, który konfiguruje ustawienia hello ma odpowiednie RBAC dostępu tooboth subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8151a-119">hello service bus or event hub namespace does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="8151a-120">Za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8151a-120">Via Azure portal</span></span>
1. <span data-ttu-id="8151a-121">Przejdź toohello **dziennik aktywności** przy użyciu hello menu na powitania po lewej stronie portalu hello bloku.</span><span class="sxs-lookup"><span data-stu-id="8151a-121">Navigate toohello **Activity Log** blade using hello menu on hello left side of hello portal.</span></span>
   
    ![Przejdź tooActivity dziennika w portalu](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="8151a-123">Kliknij przycisk hello **wyeksportować** u góry hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="8151a-123">Click hello **Export** button at hello top of hello blade.</span></span>
   
    ![Przycisk Eksportuj w portalu](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="8151a-125">W wyświetlonym bloku hello można wybrać hello regionów, dla których chcesz toostream zdarzenia i hello usługi magistrali Namespace, w którym chcesz toobe Centrum zdarzeń utworzonych dla przesyłania strumieniowego te zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8151a-125">In hello blade that appears, you can select hello regions for which you would like toostream events and hello Service Bus Namespace in which you would like an Event Hub toobe created for streaming these events.</span></span>
   
    ![Eksport dziennika aktywności bloku](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="8151a-127">Kliknij przycisk **zapisać** toosave te ustawienia.</span><span class="sxs-lookup"><span data-stu-id="8151a-127">Click **Save** toosave these settings.</span></span> <span data-ttu-id="8151a-128">Ustawienia Hello są natychmiast być zastosowane tooyour subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8151a-128">hello settings are immediately be applied tooyour subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="8151a-129">Za pomocą poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="8151a-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="8151a-130">Jeśli istnieje już profil dziennika, należy najpierw tooremove tego profilu.</span><span class="sxs-lookup"><span data-stu-id="8151a-130">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="8151a-131">Użyj `Get-AzureRmLogProfile` tooidentify, jeśli istnieje już profil dziennika</span><span class="sxs-lookup"><span data-stu-id="8151a-131">Use `Get-AzureRmLogProfile` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="8151a-132">Jeśli tak, użyj `Remove-AzureRmLogProfile` tooremove go.</span><span class="sxs-lookup"><span data-stu-id="8151a-132">If so, use `Remove-AzureRmLogProfile` tooremove it.</span></span>
3. <span data-ttu-id="8151a-133">Użyj `Set-AzureRmLogProfile` toocreate profil:</span><span class="sxs-lookup"><span data-stu-id="8151a-133">Use `Set-AzureRmLogProfile` toocreate a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="8151a-134">Hello identyfikator reguły magistrali usług to ciąg w formacie: {identyfikator zasobu magistrali usługi} /authorizationrules/ {nazwa klucza}, np.</span><span class="sxs-lookup"><span data-stu-id="8151a-134">hello Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="8151a-135">Za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8151a-135">Via Azure CLI</span></span>
<span data-ttu-id="8151a-136">Jeśli istnieje już profil dziennika, należy najpierw tooremove tego profilu.</span><span class="sxs-lookup"><span data-stu-id="8151a-136">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="8151a-137">Użyj `azure insights logprofile list` tooidentify, jeśli istnieje już profil dziennika</span><span class="sxs-lookup"><span data-stu-id="8151a-137">Use `azure insights logprofile list` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="8151a-138">Jeśli tak, użyj `azure insights logprofile delete` tooremove go.</span><span class="sxs-lookup"><span data-stu-id="8151a-138">If so, use `azure insights logprofile delete` tooremove it.</span></span>
3. <span data-ttu-id="8151a-139">Użyj `azure insights logprofile add` toocreate profil:</span><span class="sxs-lookup"><span data-stu-id="8151a-139">Use `azure insights logprofile add` toocreate a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="8151a-140">Hello identyfikator reguły magistrali usług to ciąg w formacie: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="8151a-140">hello Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="8151a-141">Jak korzystać z hello danych dziennika z usługi Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="8151a-141">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="8151a-142">[Schemat Hello hello dziennik aktywności jest dostępnych tutaj](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="8151a-142">[hello schema for hello Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="8151a-143">Każde wydarzenie jest w tablicy obiektów blob JSON o nazwie "rekordy."</span><span class="sxs-lookup"><span data-stu-id="8151a-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="8151a-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8151a-144">Next Steps</span></span>
* [<span data-ttu-id="8151a-145">Archiwum hello konta magazynu tooa dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="8151a-145">Archive hello Activity Log tooa storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="8151a-146">Omówienie hello odczytu hello dziennika aktywności platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8151a-146">Read hello overview of hello Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="8151a-147">Konfigurowanie alertu na podstawie zdarzenia dziennika aktywności</span><span class="sxs-lookup"><span data-stu-id="8151a-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

