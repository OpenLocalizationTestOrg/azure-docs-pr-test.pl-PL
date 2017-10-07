---
title: "AAA\"skorygować alerty Azure maszyny Wirtualnej z elementami Runbook automatyzacji | Dokumentacja firmy Microsoft\""
description: "W tym artykule pokazano, jak alerty toointegrate maszyny wirtualnej platformy Azure z elementu runbook usługi Automatyzacja Azure i automatyczne rozwiązywanie problemów"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="22962-103">Scenariusz automatyzacji Azure - skorygować alerty maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="22962-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="22962-104">Maszyny wirtualne Azure i automatyzacji Azure zostały wydane nową funkcję, umożliwiając tooconfigure elementu runbook usługi Automatyzacja toorun alerty maszyn wirtualnych (VM).</span><span class="sxs-lookup"><span data-stu-id="22962-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you tooconfigure Virtual Machine (VM) alerts toorun Automation runbooks.</span></span> <span data-ttu-id="22962-105">Ta nowa funkcja umożliwia tooautomatically przeprowadzanie korekty standardowe w odpowiedzi tooVM alertów, takie jak ponowne uruchamianie lub zatrzymywanie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22962-105">This new capability allows you tooautomatically perform standard remediation in response tooVM alerts, like restarting or stopping hello VM.</span></span>

<span data-ttu-id="22962-106">Wcześniej, podczas tworzenia reguły alertu maszyny Wirtualnej można było zbyt[Określ element webhook usługi automatyzacja](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) runbook tooa w kolejności toorun hello runbook przy każdym wyzwoleniu alertu hello.</span><span class="sxs-lookup"><span data-stu-id="22962-106">Previously, during VM alert rule creation you were able too[specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook in order toorun hello runbook whenever hello alert triggered.</span></span> <span data-ttu-id="22962-107">Jednak to wymaga od Ciebie toodo hello pracy tworzenia elementów runbook hello, tworzenia elementu webhook hello hello elementu runbook i następnie kopiowania i wklejania elementu webhook hello podczas tworzenia reguły alertu.</span><span class="sxs-lookup"><span data-stu-id="22962-107">However, this required you toodo hello work of creating hello runbook, creating hello webhook for hello runbook, and then copying and pasting hello webhook during alert rule creation.</span></span> <span data-ttu-id="22962-108">Z tej nowej wersji hello procesu jest znacznie łatwiejsze, ponieważ element runbook może bezpośrednio wybrać z listy, podczas tworzenia reguły alertu, można wybrać konto usługi Automatyzacja, którego będzie uruchomić element runbook hello lub łatwo utworzyć konto.</span><span class="sxs-lookup"><span data-stu-id="22962-108">With this new release, hello process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run hello runbook or easily create an account.</span></span>

<span data-ttu-id="22962-109">W tym artykule nasz opisano, jak łatwo jest tooset się alert maszyny Wirtualnej platformy Azure i skonfigurować toorun elementu runbook automatyzacji zawsze, gdy wyzwala hello alert.</span><span class="sxs-lookup"><span data-stu-id="22962-109">In this article, we will show you how easy it is tooset up an Azure VM alert and configure an Automation runbook toorun whenever hello alert triggers.</span></span> <span data-ttu-id="22962-110">Przykładowe scenariusze obejmują ponowne uruchamianie maszyny Wirtualnej podczas hello użycie pamięci przekroczy próg niektórych powodu tooan aplikacji hello maszyny Wirtualnej z przeciek pamięci ani zatrzymywanie maszyny Wirtualnej, gdy czas użytkownika Procesora hello jest niższy niż 1% dla ostatniej godziny i nie jest używany.</span><span class="sxs-lookup"><span data-stu-id="22962-110">Example scenarios include restarting a VM when hello memory usage exceeds some threshold due tooan application on hello VM with a memory leak, or stopping a VM when hello CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="22962-111">Prezentujemy również zasady jak hello automatycznego tworzenia z nazwy głównej usługi w sieci automatyzacji konta upraszcza hello Użyj elementów runbook w programie Azure korygowania alertu.</span><span class="sxs-lookup"><span data-stu-id="22962-111">We’ll also explain how hello automated creation of a service principal in your Automation account simplifies hello use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="22962-112">Utwórz alert na maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="22962-112">Create an alert on a VM</span></span>
<span data-ttu-id="22962-113">Wykonaj hello następujące kroki tooconfigure alertu toolaunch element runbook po jego próg zostały spełnione.</span><span class="sxs-lookup"><span data-stu-id="22962-113">Perform hello following steps tooconfigure an alert toolaunch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="22962-114">W tej wersji obsługiwany jest tylko maszyny wirtualne w wersji 2 i pomocy technicznej klasycznego maszyn wirtualnych zostaną dodane wkrótce.</span><span class="sxs-lookup"><span data-stu-id="22962-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="22962-115">Zaloguj się za toohello portalu Azure, a następnie kliknij przycisk **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="22962-115">Log in toohello Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="22962-116">Wybierz jedną z maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="22962-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="22962-117">Witaj bloku pulpitu nawigacyjnego maszyny wirtualnej będą wyświetlane i hello **ustawienia** prawo tooits bloku.</span><span class="sxs-lookup"><span data-stu-id="22962-117">hello virtual machine dashboard blade will appear and hello **Settings** blade tooits right.</span></span>  
3. <span data-ttu-id="22962-118">Z hello **ustawienia** bloku, w obszarze hello wybierz sekcji monitorowanie **reguły alertów**.</span><span class="sxs-lookup"><span data-stu-id="22962-118">From hello **Settings** blade, under hello Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="22962-119">Na powitania **reguły alertów** bloku, kliknij przycisk **Dodaj alert**.</span><span class="sxs-lookup"><span data-stu-id="22962-119">On hello **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="22962-120">Spowoduje to otwarcie zapasowej hello **dodać regułę alertu** bloku, w którym można skonfigurować warunki hello hello alert i można wybrać jedną z co najmniej jedną z tych opcji: wysyłanie wiadomości e-mail toosomeone, należy użyć dla elementu webhook tooforward hello alert tooanother systemu, i/lub Uruchom element runbook usługi Automatyzacja w odpowiedzi próba tooremediate hello problem.</span><span class="sxs-lookup"><span data-stu-id="22962-120">This opens up hello **Add an alert rule** blade, where you can configure hello conditions for hello alert and choose among one or all of these options: send email toosomeone, use a webhook tooforward hello alert tooanother system, and/or run an Automation runbook in response attempt tooremediate hello issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="22962-121">Konfigurowanie elementu runbook</span><span class="sxs-lookup"><span data-stu-id="22962-121">Configure a runbook</span></span>
<span data-ttu-id="22962-122">Wybierz tooconfigure toorun elementu runbook, gdy próg alertu hello maszyny Wirtualnej zostanie spełniony, **elementu Runbook automatyzacji**.</span><span class="sxs-lookup"><span data-stu-id="22962-122">tooconfigure a runbook toorun when hello VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="22962-123">W hello **skonfigurować runbook** bloku, możesz wybrać hello runbook toorun i hello runbook hello toorun konto usługi Automatyzacja w.</span><span class="sxs-lookup"><span data-stu-id="22962-123">In hello **Configure runbook** blade, you can select hello runbook toorun and hello Automation account toorun hello runbook in.</span></span>

![Skonfiguruj element runbook usługi Automatyzacja i Utwórz nowe konto automatyzacji](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="22962-125">W tej wersji są dostępne trzy elementy runbook, które zapewnia usługi hello — ponowne uruchomienie maszyny Wirtualnej, Zatrzymaj maszyny Wirtualnej lub usunąć maszyny Wirtualnej (Usuń go).</span><span class="sxs-lookup"><span data-stu-id="22962-125">For this release you can choose from three runbooks that hello service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="22962-126">Witaj tooselect możliwości inne elementy runbook lub jeden z własnych elementów runbook będą dostępne w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="22962-126">hello ability tooselect other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Elementy Runbook toochoose z](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="22962-128">Po wybraniu jednej z trzech hello dostępne elementy runbook, hello **konto automatyzacji** prawdopodobnie listy rozwijanej i wybrać obiekt automatyzacji konta hello runbook będzie uruchamiany jako.</span><span class="sxs-lookup"><span data-stu-id="22962-128">After you select one of hello three available runbooks, hello **Automation account** drop-down list appears and you can select an automation account hello runbook will run as.</span></span> <span data-ttu-id="22962-129">Elementy Runbook muszą toorun w kontekście hello [konto automatyzacji](automation-security-overview.md) w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22962-129">Runbooks need toorun in hello context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="22962-130">Można wybrać konto usługi Automatyzacja już utworzone, czy masz utworzone nowe konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="22962-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="22962-131">Witaj elementów runbook, które znajdują się uwierzytelnić tooAzure przy użyciu nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="22962-131">hello runbooks that are provided authenticate tooAzure using a service principal.</span></span> <span data-ttu-id="22962-132">Jeśli w jednym z istniejących kont automatyzacji elementu runbook hello toorun, automatycznie utworzymy hello usługi głównej dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="22962-132">If you choose toorun hello runbook in one of your existing Automation accounts, we will automatically create hello service principal for you.</span></span> <span data-ttu-id="22962-133">Jeśli wybierzesz toocreate nowe konto usługi Automatyzacja, następnie automatycznie utworzymy hello konta i nazwę główną usługi hello.</span><span class="sxs-lookup"><span data-stu-id="22962-133">If you choose toocreate a new Automation account, then we will automatically create hello account and hello service principal.</span></span> <span data-ttu-id="22962-134">W obu przypadkach dwa zasoby zostanie utworzony również w hello konto automatyzacji — zasób certyfikatu o nazwie **AzureRunAsCertificate** i zasób połączenia o nazwie **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="22962-134">In both cases, two assets will also be created in hello Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="22962-135">elementy runbook Hello użyje **AzureRunAsConnection** tooauthenticate z platformy Azure, w kolejności tooperform hello zarządzania akcji przed hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22962-135">hello runbooks will use **AzureRunAsConnection** tooauthenticate with Azure in order tooperform hello management action against hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="22962-136">nazwy głównej usługi Hello jest tworzony w zakresie subskrypcji hello i przypisano rolę współautora hello.</span><span class="sxs-lookup"><span data-stu-id="22962-136">hello service principal is created in hello subscription scope and is assigned hello Contributor role.</span></span> <span data-ttu-id="22962-137">Ta rola jest wymagana, aby hello konta toohave uprawnienia toorun automatyzacji elementów runbook toomanage maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22962-137">This role is required in order for hello account toohave permission toorun Automation runbooks toomanage Azure VMs.</span></span>  <span data-ttu-id="22962-138">Tworzenie Hello Automaton konta i/lub nazwy głównej usługi jest zdarzenia jednorazowego.</span><span class="sxs-lookup"><span data-stu-id="22962-138">hello creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="22962-139">Po ich utworzeniu można użyć tego elementów runbook toorun konta dla innych alertów maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22962-139">Once they are created, you can use that account toorun runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="22962-140">Po kliknięciu **OK** hello alert jest skonfigurowany i w przypadku wybrania hello opcja toocreate nowe konto automatyzacji jest tworzony wraz z hello nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="22962-140">When you click **OK** hello alert is configured and if you selected hello option toocreate a new Automation account, it is created along with hello service principal.</span></span>  <span data-ttu-id="22962-141">Może to zająć kilka sekund toocomplete.</span><span class="sxs-lookup"><span data-stu-id="22962-141">This can take a few seconds toocomplete.</span></span>  

![Element Runbook jest skonfigurowany](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="22962-143">Po zakończeniu konfiguracji hello zobaczysz hello nazwa elementu runbook hello są wyświetlane w hello **dodać regułę alertu** bloku.</span><span class="sxs-lookup"><span data-stu-id="22962-143">After hello configuration is completed you will see hello name of hello runbook appear in hello **Add an alert rule** blade.</span></span>

![Element Runbook jest skonfigurowany](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="22962-145">Kliknij przycisk **OK** w hello **dodać regułę alertu** bloku i hello reguły alertu zostanie utworzona i aktywowane, jeśli maszyna wirtualna hello jest w stanie uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="22962-145">Click **OK** in hello **Add an alert rule** blade and hello alert rule will be created and activate if hello virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="22962-146">Włącz lub wyłącz elementu runbook</span><span class="sxs-lookup"><span data-stu-id="22962-146">Enable or disable a runbook</span></span>
<span data-ttu-id="22962-147">Bez usuwania konfiguracji elementu runbook hello je wyłączyć elementu runbook skonfigurowane dla alertu.</span><span class="sxs-lookup"><span data-stu-id="22962-147">If you have a runbook configured for an alert, you can disable it without removing hello runbook configuration.</span></span> <span data-ttu-id="22962-148">Pozwala tookeep hello alertów uruchomiona i może testowania niektórych reguł alertów hello i później ponownie włączyć hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="22962-148">This allows you tookeep hello alert running and perhaps test some of hello alert rules and then later re-enable hello runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="22962-149">Tworzenie elementu runbook, który współpracuje z Azure alertu</span><span class="sxs-lookup"><span data-stu-id="22962-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="22962-150">Po wybraniu elementu runbook w ramach platformy Azure reguły alertu hello elementu runbook musi toohave logikę w nim toomanage hello dane alertów przekazywany tooit.</span><span class="sxs-lookup"><span data-stu-id="22962-150">When you choose a runbook as part of an Azure alert rule, hello runbook needs toohave logic in it toomanage hello alert data that is passed tooit.</span></span>  <span data-ttu-id="22962-151">Jeśli element runbook jest skonfigurowany w regule alertu, elementu webhook jest tworzona dla elementu runbook hello; tego elementu webhook jest używane toostart hello runbook każdej czasu hello alertu wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="22962-151">When a runbook is configured in an alert rule, a webhook is created for hello runbook; that webhook is then used toostart hello runbook each time hello alert triggers.</span></span>  <span data-ttu-id="22962-152">Witaj rzeczywiste wywołanie toostart hello runbook jest adres URL elementu webhook toohello żądania HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="22962-152">hello actual call toostart hello runbook is an HTTP POST request toohello webhook URL.</span></span> <span data-ttu-id="22962-153">Witaj treści żądania POST hello zawiera sformatowane JSON obiekt, który zawiera przydatne właściwości powiązanych toohello alert.</span><span class="sxs-lookup"><span data-stu-id="22962-153">hello body of hello POST request contains a JSON-formated object that contains useful properties related toohello alert.</span></span>  <span data-ttu-id="22962-154">Jak widać poniżej, dane alertów hello zawiera szczegóły, takie jak identyfikator subskrypcji, grupy zasobów o nazwie resourceName i typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="22962-154">As you can see below, hello alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="22962-155">Przykład danych alertu</span><span class="sxs-lookup"><span data-stu-id="22962-155">Example of Alert data</span></span>
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

<span data-ttu-id="22962-156">Odebrania hello usługi elementu webhook usługi Automatyzacja hello HTTP POST wyodrębnia dane alertów hello i przekazuje je toohello runbook parametr wejściowy hello WebhookData elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="22962-156">When hello Automation webhook service receives hello HTTP POST it extracts hello alert data and passes it toohello runbook in hello WebhookData runbook input parameter.</span></span>  <span data-ttu-id="22962-157">Poniżej przedstawiono przykładowy element runbook, pokazujący sposób toouse hello parametru WebhookData i wyodrębniania danych alertów hello i korzystać z niego hello toomanage zasobów platformy Azure, która wyzwoliła hello alert.</span><span class="sxs-lookup"><span data-stu-id="22962-157">Below is a sample runbook that shows how toouse hello WebhookData parameter and extract hello alert data and use it toomanage hello Azure resource that triggered hello alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="22962-158">Przykładowy element runbook</span><span class="sxs-lookup"><span data-stu-id="22962-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="22962-159">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="22962-159">Summary</span></span>
<span data-ttu-id="22962-160">Podczas konfigurowania alertu na maszynie Wirtualnej platformy Azure, masz teraz hello tooeasily możliwości konfigurowania automatyzacji runbook tooautomatically wykonania akcji korygowania podczas wyzwala hello alertu.</span><span class="sxs-lookup"><span data-stu-id="22962-160">When you configure an alert on an Azure VM, you now have hello ability tooeasily configure an Automation runbook tooautomatically perform remediation action when hello alert triggers.</span></span> <span data-ttu-id="22962-161">W tej wersji możesz wybrać spośród elementów runbook toorestart, Zatrzymaj, lub usuń Maszynę wirtualną w zależności od danego scenariusza alertu.</span><span class="sxs-lookup"><span data-stu-id="22962-161">For this release, you can choose from runbooks toorestart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="22962-162">Jest to początek tylko hello włączenie scenariuszy, w którym kontrolować akcje hello (powiadomienia, rozwiązywania problemów, korygowania), które zostaną wykonane automatycznie po wyzwala alert.</span><span class="sxs-lookup"><span data-stu-id="22962-162">This is just hello beginning of enabling scenarios where you control hello actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22962-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22962-163">Next Steps</span></span>
* <span data-ttu-id="22962-164">tooget wprowadzenie do graficznych elementów runbook, zobacz [Mój pierwszy graficznym elementem runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="22962-164">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="22962-165">tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="22962-165">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="22962-166">Zobacz toolearn więcej informacji na temat typów elementów runbook, ich zalety i ograniczenia, [typy elementu runbook usługi Automatyzacja Azure](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="22962-166">toolearn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

