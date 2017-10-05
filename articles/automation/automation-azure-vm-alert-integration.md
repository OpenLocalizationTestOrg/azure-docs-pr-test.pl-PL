---
title: " Korygowanie alerty Azure maszyny Wirtualnej z elementami Runbook automatyzacji | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób integracji alerty maszyny wirtualnej platformy Azure z elementu runbook usługi Automatyzacja Azure i automatyczne rozwiązywanie problemów"
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
ms.openlocfilehash: 738959b8e1ee5da989bb996d1ce8148cbf912781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="869a3-103">Scenariusz automatyzacji Azure - skorygować alerty maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="869a3-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="869a3-104">Maszyny wirtualne Azure i automatyzacji Azure zostały wydane nowa funkcja umożliwia konfigurowanie alertów maszyn wirtualnych (VM) do uruchamiania elementów runbook automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="869a3-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you to configure Virtual Machine (VM) alerts to run Automation runbooks.</span></span> <span data-ttu-id="869a3-105">Ta nowa funkcja umożliwia automatycznie przeprowadzić korektę standardowe w odpowiedzi na alerty maszyny Wirtualnej, takie jak ponowne uruchomienie lub zatrzymanie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="869a3-105">This new capability allows you to automatically perform standard remediation in response to VM alerts, like restarting or stopping the VM.</span></span>

<span data-ttu-id="869a3-106">Wcześniej, podczas tworzenia reguły alertu maszyny Wirtualnej można było [Określ element webhook usługi automatyzacja](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) do elementu runbook, aby można było uruchomić element runbook, przy każdym wyzwoleniu alertu.</span><span class="sxs-lookup"><span data-stu-id="869a3-106">Previously, during VM alert rule creation you were able to [specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) to a runbook in order to run the runbook whenever the alert triggered.</span></span> <span data-ttu-id="869a3-107">Jednak to wymagane do pracy z tworzenia elementu runbook, tworzenia elementu webhook dla elementu runbook, kopiowanie i wklejanie elementu webhook podczas tworzenia reguły alertu.</span><span class="sxs-lookup"><span data-stu-id="869a3-107">However, this required you to do the work of creating the runbook, creating the webhook for the runbook, and then copying and pasting the webhook during alert rule creation.</span></span> <span data-ttu-id="869a3-108">W tej nowej wersji proces jest znacznie łatwiejsze, ponieważ element runbook może bezpośrednio wybrać z listy, podczas tworzenia reguły alertu, można wybrać konto usługi Automatyzacja, którego będzie uruchomić element runbook lub łatwo utworzyć konto.</span><span class="sxs-lookup"><span data-stu-id="869a3-108">With this new release, the process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run the runbook or easily create an account.</span></span>

<span data-ttu-id="869a3-109">W tym artykule pokazano, jak łatwo jest aby ustawić alert maszyny Wirtualnej platformy Azure i skonfigurować element runbook usługi Automatyzacja do uruchamiania w przypadku wyzwala alert.</span><span class="sxs-lookup"><span data-stu-id="869a3-109">In this article, we will show you how easy it is to set up an Azure VM alert and configure an Automation runbook to run whenever the alert triggers.</span></span> <span data-ttu-id="869a3-110">Przykładowe scenariusze obejmują ponowne uruchomienie maszyny Wirtualnej, gdy użycie pamięci przekroczy próg niektóre z powodu aplikacji na maszynie Wirtualnej o przeciek pamięci ani zatrzymywanie maszyny Wirtualnej, gdy czas użytkownika procesora CPU było poniżej 1% ostatniej godziny i nie jest używany.</span><span class="sxs-lookup"><span data-stu-id="869a3-110">Example scenarios include restarting a VM when the memory usage exceeds some threshold due to an application on the VM with a memory leak, or stopping a VM when the CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="869a3-111">Prezentujemy również zasady sposób automatycznego tworzenia usługi podmiotu zabezpieczeń na Twoim koncie automatyzacji upraszcza korzystanie z elementów runbook w programie Azure korygowania alertu.</span><span class="sxs-lookup"><span data-stu-id="869a3-111">We’ll also explain how the automated creation of a service principal in your Automation account simplifies the use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="869a3-112">Utwórz alert na maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="869a3-112">Create an alert on a VM</span></span>
<span data-ttu-id="869a3-113">Wykonaj poniższe kroki, aby skonfigurować alert, aby uruchomić element runbook po jego próg zostały spełnione.</span><span class="sxs-lookup"><span data-stu-id="869a3-113">Perform the following steps to configure an alert to launch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="869a3-114">W tej wersji obsługiwany jest tylko maszyny wirtualne w wersji 2 i pomocy technicznej klasycznego maszyn wirtualnych zostaną dodane wkrótce.</span><span class="sxs-lookup"><span data-stu-id="869a3-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="869a3-115">Zaloguj się do portalu Azure, a następnie kliknij przycisk **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="869a3-115">Log in to the Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="869a3-116">Wybierz jedną z maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="869a3-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="869a3-117">Zostanie wyświetlony pulpit nawigacyjny bloku maszyny wirtualnej i **ustawienia** bloku, aby po jego prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="869a3-117">The virtual machine dashboard blade will appear and the **Settings** blade to its right.</span></span>  
3. <span data-ttu-id="869a3-118">Z **ustawienia** bloku, w obszarze Wybieranie sekcji monitorowanie **reguły alertów**.</span><span class="sxs-lookup"><span data-stu-id="869a3-118">From the **Settings** blade, under the Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="869a3-119">Na **reguły alertów** bloku, kliknij przycisk **Dodaj alert**.</span><span class="sxs-lookup"><span data-stu-id="869a3-119">On the **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="869a3-120">Spowoduje to otwarcie **dodać regułę alertu** bloku, w którym można skonfigurować warunki alertu i wyboru spośród jedno lub wszystkie z następujących opcji: Wyślij wiadomość e-mail do osoby, należy użyć elementu webhook do przesyłania dalej alertów do innego systemu i/lub uruchom Element runbook automatyzacji w odpowiedzi próbę rozwiązania problemu.</span><span class="sxs-lookup"><span data-stu-id="869a3-120">This opens up the **Add an alert rule** blade, where you can configure the conditions for the alert and choose among one or all of these options: send email to someone, use a webhook to forward the alert to another system, and/or run an Automation runbook in response attempt to remediate the issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="869a3-121">Konfigurowanie elementu runbook</span><span class="sxs-lookup"><span data-stu-id="869a3-121">Configure a runbook</span></span>
<span data-ttu-id="869a3-122">Aby skonfigurować element runbook uruchamiany, gdy próg alertu maszyny Wirtualnej jest spełniony, wybierz **elementu Runbook automatyzacji**.</span><span class="sxs-lookup"><span data-stu-id="869a3-122">To configure a runbook to run when the VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="869a3-123">W **skonfigurować runbook** bloku, możesz wybrać na uruchomienie elementu runbook i konta automatyzacji, aby uruchomić element runbook.</span><span class="sxs-lookup"><span data-stu-id="869a3-123">In the **Configure runbook** blade, you can select the runbook to run and the Automation account to run the runbook in.</span></span>

![Skonfiguruj element runbook usługi Automatyzacja i Utwórz nowe konto automatyzacji](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="869a3-125">W tej wersji są dostępne trzy elementy runbook, które udostępnia usługę — ponowne uruchomienie maszyny Wirtualnej, Zatrzymaj maszyny Wirtualnej lub usunąć maszyny Wirtualnej (Usuń go).</span><span class="sxs-lookup"><span data-stu-id="869a3-125">For this release you can choose from three runbooks that the service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="869a3-126">Wybierz inne elementy runbook lub jeden z własnych elementów runbook możliwości będą dostępne w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="869a3-126">The ability to select other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Wybierz spośród elementów Runbook](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="869a3-128">Po wybraniu jednej z trzech dostępnych elementów runbook **konto automatyzacji** prawdopodobnie listy rozwijanej i można wybrać element runbook będzie uruchamiany jako konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="869a3-128">After you select one of the three available runbooks, the **Automation account** drop-down list appears and you can select an automation account the runbook will run as.</span></span> <span data-ttu-id="869a3-129">Elementy Runbook muszą działać w kontekście [konto automatyzacji](automation-security-overview.md) w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="869a3-129">Runbooks need to run in the context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="869a3-130">Można wybrać konto usługi Automatyzacja już utworzone, czy masz utworzone nowe konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="869a3-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="869a3-131">Elementy runbook, które znajdują się uwierzytelnić się na platformie Azure przy użyciu nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="869a3-131">The runbooks that are provided authenticate to Azure using a service principal.</span></span> <span data-ttu-id="869a3-132">Jeśli chcesz uruchomić element runbook w jednym z istniejących kont automatyzacji automatycznie utworzymy usługę podmiotu zabezpieczeń dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="869a3-132">If you choose to run the runbook in one of your existing Automation accounts, we will automatically create the service principal for you.</span></span> <span data-ttu-id="869a3-133">Jeśli użytkownik chce utworzyć nowe konto usługi Automatyzacja, następnie zostanie automatycznie utworzony konta i nazwę główną usługi.</span><span class="sxs-lookup"><span data-stu-id="869a3-133">If you choose to create a new Automation account, then we will automatically create the account and the service principal.</span></span> <span data-ttu-id="869a3-134">W obu przypadkach dwa zasoby zostanie utworzony również w ramach konta usługi Automatyzacja — zasób certyfikatu o nazwie **AzureRunAsCertificate** i zasób połączenia o nazwie **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="869a3-134">In both cases, two assets will also be created in the Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="869a3-135">Elementy runbook użyje **AzureRunAsConnection** do uwierzytelniania w usłudze Azure w celu wykonania akcji zarządzania dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="869a3-135">The runbooks will use **AzureRunAsConnection** to authenticate with Azure in order to perform the management action against the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="869a3-136">Nazwy głównej usługi jest tworzony w zakresie subskrypcji i przypisany do roli współautora.</span><span class="sxs-lookup"><span data-stu-id="869a3-136">The service principal is created in the subscription scope and is assigned the Contributor role.</span></span> <span data-ttu-id="869a3-137">Ta rola jest wymagana w celu zarządzania maszynami wirtualnymi platformy Azure dla konta, aby mieć uprawnienia do uruchamiania elementów runbook automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="869a3-137">This role is required in order for the account to have permission to run Automation runbooks to manage Azure VMs.</span></span>  <span data-ttu-id="869a3-138">Tworzenie konta Automaton i/lub nazwy głównej usługi jest zdarzenia jednorazowego.</span><span class="sxs-lookup"><span data-stu-id="869a3-138">The creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="869a3-139">Po ich utworzeniu można użyć tego konta do uruchamiania elementów runbook dla innych alertów maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="869a3-139">Once they are created, you can use that account to run runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="869a3-140">Po kliknięciu **OK** alert został skonfigurowany, a jeśli wybrano opcję, aby utworzyć nowe konto automatyzacji jest tworzony wraz z nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="869a3-140">When you click **OK** the alert is configured and if you selected the option to create a new Automation account, it is created along with the service principal.</span></span>  <span data-ttu-id="869a3-141">Może to zająć kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="869a3-141">This can take a few seconds to complete.</span></span>  

![Element Runbook jest skonfigurowany](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="869a3-143">Po zakończeniu konfiguracji zobaczysz nazwa elementu runbook są wyświetlane w **dodać regułę alertu** bloku.</span><span class="sxs-lookup"><span data-stu-id="869a3-143">After the configuration is completed you will see the name of the runbook appear in the **Add an alert rule** blade.</span></span>

![Element Runbook jest skonfigurowany](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="869a3-145">Kliknij przycisk **OK** w **dodać regułę alertu** bloku regułę alertu zostanie utworzona i aktywowane, jeśli maszyna wirtualna jest w stanie uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="869a3-145">Click **OK** in the **Add an alert rule** blade and the alert rule will be created and activate if the virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="869a3-146">Włącz lub wyłącz elementu runbook</span><span class="sxs-lookup"><span data-stu-id="869a3-146">Enable or disable a runbook</span></span>
<span data-ttu-id="869a3-147">Jeśli element runbook skonfigurowane dla alertu, można ją wyłączyć, bez usuwania konfiguracji elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="869a3-147">If you have a runbook configured for an alert, you can disable it without removing the runbook configuration.</span></span> <span data-ttu-id="869a3-148">Dzięki temu można zachować alertów uruchomiona i może testowania niektórych reguł alertów i później ponownie włączyć element runbook.</span><span class="sxs-lookup"><span data-stu-id="869a3-148">This allows you to keep the alert running and perhaps test some of the alert rules and then later re-enable the runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="869a3-149">Tworzenie elementu runbook, który współpracuje z Azure alertu</span><span class="sxs-lookup"><span data-stu-id="869a3-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="869a3-150">Po wybraniu elementu runbook regułę alertu Azure w ramach elementu runbook musi mieć logikę w nim zarządzać przekazywane do niego dane alertu.</span><span class="sxs-lookup"><span data-stu-id="869a3-150">When you choose a runbook as part of an Azure alert rule, the runbook needs to have logic in it to manage the alert data that is passed to it.</span></span>  <span data-ttu-id="869a3-151">Jeśli element runbook jest skonfigurowany w regule alertu, elementu webhook jest tworzona dla elementu runbook; tego elementu webhook jest następnie używany do uruchamiania elementu runbook zawsze wyzwala alert.</span><span class="sxs-lookup"><span data-stu-id="869a3-151">When a runbook is configured in an alert rule, a webhook is created for the runbook; that webhook is then used to start the runbook each time the alert triggers.</span></span>  <span data-ttu-id="869a3-152">To rzeczywiste wywołanie do uruchamiania elementu runbook jest żądanie HTTP POST na adres URL elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="869a3-152">The actual call to start the runbook is an HTTP POST request to the webhook URL.</span></span> <span data-ttu-id="869a3-153">Treść żądania POST zawiera sformatowane JSON obiekt, który zawiera przydatne właściwości powiązane z danym alertem.</span><span class="sxs-lookup"><span data-stu-id="869a3-153">The body of the POST request contains a JSON-formated object that contains useful properties related to the alert.</span></span>  <span data-ttu-id="869a3-154">Jak widać poniżej, dane alertu zawiera szczegółowe informacje, takie jak identyfikator subskrypcji, grupy zasobów o nazwie resourceName i typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="869a3-154">As you can see below, the alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="869a3-155">Przykład danych alertu</span><span class="sxs-lookup"><span data-stu-id="869a3-155">Example of Alert data</span></span>
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

<span data-ttu-id="869a3-156">Odebrania usługi elementu webhook usługi Automatyzacja HTTP POST wyodrębnia dane alertów i przekazuje je do elementu runbook w parametrze wejściowym WebhookData elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="869a3-156">When the Automation webhook service receives the HTTP POST it extracts the alert data and passes it to the runbook in the WebhookData runbook input parameter.</span></span>  <span data-ttu-id="869a3-157">Poniżej przedstawiono przykładowy element runbook, który pokazuje, jak parametr WebhookData i wyodrębniania danych alertów i przy jego użyciu zarządzać zasobów platformy Azure, która wyzwoliła alert.</span><span class="sxs-lookup"><span data-stu-id="869a3-157">Below is a sample runbook that shows how to use the WebhookData parameter and extract the alert data and use it to manage the Azure resource that triggered the alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="869a3-158">Przykładowy element runbook</span><span class="sxs-lookup"><span data-stu-id="869a3-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response to an Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get the data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that the alert status is 'Activated' (alert condition went from false to true)
    # and not 'Resolved' (alert condition went from true to false)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get the info needed to identify the VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is the expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate to Azure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in the Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart the VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # The alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant to be started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="869a3-159">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="869a3-159">Summary</span></span>
<span data-ttu-id="869a3-160">Podczas konfigurowania alertu na maszynie Wirtualnej platformy Azure, masz teraz łatwo skonfigurować element runbook usługi Automatyzacja, aby automatyczne wykonywanie akcji korygowania, gdy wyzwala alert.</span><span class="sxs-lookup"><span data-stu-id="869a3-160">When you configure an alert on an Azure VM, you now have the ability to easily configure an Automation runbook to automatically perform remediation action when the alert triggers.</span></span> <span data-ttu-id="869a3-161">W tej wersji można z poziomu elementów runbook można ponownie uruchomić, zatrzymać lub usunąć Maszynę wirtualną w zależności od danego scenariusza alertu.</span><span class="sxs-lookup"><span data-stu-id="869a3-161">For this release, you can choose from runbooks to restart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="869a3-162">Jest to tylko początek włączania scenariuszy, w którym kontrolować akcje, które zostaną wykonane automatycznie po wyzwala alert (powiadomienia, rozwiązywania problemów, korygowania).</span><span class="sxs-lookup"><span data-stu-id="869a3-162">This is just the beginning of enabling scenarios where you control the actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="869a3-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="869a3-163">Next Steps</span></span>
* <span data-ttu-id="869a3-164">Aby rozpocząć pracę z graficznymi elementami Runbook, zobacz artykuł [My first graphical runbook](automation-first-runbook-graphical.md) (Mój pierwszy graficzny element Runbook).</span><span class="sxs-lookup"><span data-stu-id="869a3-164">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="869a3-165">Aby rozpocząć pracę z elementami Runbook przepływu pracy programu PowerShell, zobacz artykuł [My first PowerShell workflow runbook](automation-first-runbook-textual.md) (Mój pierwszy element Runbook przepływu pracy programu PowerShell).</span><span class="sxs-lookup"><span data-stu-id="869a3-165">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="869a3-166">Aby dowiedzieć się więcej na temat typów elementów Runbook, ich zalet i ograniczeń, zobacz artykuł [Azure Automation runbook types](automation-runbook-types.md) (Typy elementów Runbook usługi Azure Automation).</span><span class="sxs-lookup"><span data-stu-id="869a3-166">To learn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

