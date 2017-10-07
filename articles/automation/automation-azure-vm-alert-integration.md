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
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a>Scenariusz automatyzacji Azure - skorygować alerty maszyny Wirtualnej Azure
Maszyny wirtualne Azure i automatyzacji Azure zostały wydane nową funkcję, umożliwiając tooconfigure elementu runbook usługi Automatyzacja toorun alerty maszyn wirtualnych (VM). Ta nowa funkcja umożliwia tooautomatically przeprowadzanie korekty standardowe w odpowiedzi tooVM alertów, takie jak ponowne uruchamianie lub zatrzymywanie hello maszyny Wirtualnej.

Wcześniej, podczas tworzenia reguły alertu maszyny Wirtualnej można było zbyt[Określ element webhook usługi automatyzacja](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) runbook tooa w kolejności toorun hello runbook przy każdym wyzwoleniu alertu hello. Jednak to wymaga od Ciebie toodo hello pracy tworzenia elementów runbook hello, tworzenia elementu webhook hello hello elementu runbook i następnie kopiowania i wklejania elementu webhook hello podczas tworzenia reguły alertu. Z tej nowej wersji hello procesu jest znacznie łatwiejsze, ponieważ element runbook może bezpośrednio wybrać z listy, podczas tworzenia reguły alertu, można wybrać konto usługi Automatyzacja, którego będzie uruchomić element runbook hello lub łatwo utworzyć konto.

W tym artykule nasz opisano, jak łatwo jest tooset się alert maszyny Wirtualnej platformy Azure i skonfigurować toorun elementu runbook automatyzacji zawsze, gdy wyzwala hello alert. Przykładowe scenariusze obejmują ponowne uruchamianie maszyny Wirtualnej podczas hello użycie pamięci przekroczy próg niektórych powodu tooan aplikacji hello maszyny Wirtualnej z przeciek pamięci ani zatrzymywanie maszyny Wirtualnej, gdy czas użytkownika Procesora hello jest niższy niż 1% dla ostatniej godziny i nie jest używany. Prezentujemy również zasady jak hello automatycznego tworzenia z nazwy głównej usługi w sieci automatyzacji konta upraszcza hello Użyj elementów runbook w programie Azure korygowania alertu.

## <a name="create-an-alert-on-a-vm"></a>Utwórz alert na maszynie Wirtualnej
Wykonaj hello następujące kroki tooconfigure alertu toolaunch element runbook po jego próg zostały spełnione.

> [!NOTE]
> W tej wersji obsługiwany jest tylko maszyny wirtualne w wersji 2 i pomocy technicznej klasycznego maszyn wirtualnych zostaną dodane wkrótce.  
> 
> 

1. Zaloguj się za toohello portalu Azure, a następnie kliknij przycisk **maszyn wirtualnych**.  
2. Wybierz jedną z maszyn wirtualnych.  Witaj bloku pulpitu nawigacyjnego maszyny wirtualnej będą wyświetlane i hello **ustawienia** prawo tooits bloku.  
3. Z hello **ustawienia** bloku, w obszarze hello wybierz sekcji monitorowanie **reguły alertów**.
4. Na powitania **reguły alertów** bloku, kliknij przycisk **Dodaj alert**.

Spowoduje to otwarcie zapasowej hello **dodać regułę alertu** bloku, w którym można skonfigurować warunki hello hello alert i można wybrać jedną z co najmniej jedną z tych opcji: wysyłanie wiadomości e-mail toosomeone, należy użyć dla elementu webhook tooforward hello alert tooanother systemu, i/lub Uruchom element runbook usługi Automatyzacja w odpowiedzi próba tooremediate hello problem.

## <a name="configure-a-runbook"></a>Konfigurowanie elementu runbook
Wybierz tooconfigure toorun elementu runbook, gdy próg alertu hello maszyny Wirtualnej zostanie spełniony, **elementu Runbook automatyzacji**. W hello **skonfigurować runbook** bloku, możesz wybrać hello runbook toorun i hello runbook hello toorun konto usługi Automatyzacja w.

![Skonfiguruj element runbook usługi Automatyzacja i Utwórz nowe konto automatyzacji](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> W tej wersji są dostępne trzy elementy runbook, które zapewnia usługi hello — ponowne uruchomienie maszyny Wirtualnej, Zatrzymaj maszyny Wirtualnej lub usunąć maszyny Wirtualnej (Usuń go).  Witaj tooselect możliwości inne elementy runbook lub jeden z własnych elementów runbook będą dostępne w przyszłej wersji.
> 
> 

![Elementy Runbook toochoose z](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

Po wybraniu jednej z trzech hello dostępne elementy runbook, hello **konto automatyzacji** prawdopodobnie listy rozwijanej i wybrać obiekt automatyzacji konta hello runbook będzie uruchamiany jako. Elementy Runbook muszą toorun w kontekście hello [konto automatyzacji](automation-security-overview.md) w Twojej subskrypcji platformy Azure. Można wybrać konto usługi Automatyzacja już utworzone, czy masz utworzone nowe konto automatyzacji.

Witaj elementów runbook, które znajdują się uwierzytelnić tooAzure przy użyciu nazwy głównej usługi. Jeśli w jednym z istniejących kont automatyzacji elementu runbook hello toorun, automatycznie utworzymy hello usługi głównej dla Ciebie. Jeśli wybierzesz toocreate nowe konto usługi Automatyzacja, następnie automatycznie utworzymy hello konta i nazwę główną usługi hello. W obu przypadkach dwa zasoby zostanie utworzony również w hello konto automatyzacji — zasób certyfikatu o nazwie **AzureRunAsCertificate** i zasób połączenia o nazwie **AzureRunAsConnection**. elementy runbook Hello użyje **AzureRunAsConnection** tooauthenticate z platformy Azure, w kolejności tooperform hello zarządzania akcji przed hello maszyny Wirtualnej.

> [!NOTE]
> nazwy głównej usługi Hello jest tworzony w zakresie subskrypcji hello i przypisano rolę współautora hello. Ta rola jest wymagana, aby hello konta toohave uprawnienia toorun automatyzacji elementów runbook toomanage maszynach wirtualnych platformy Azure.  Tworzenie Hello Automaton konta i/lub nazwy głównej usługi jest zdarzenia jednorazowego. Po ich utworzeniu można użyć tego elementów runbook toorun konta dla innych alertów maszyny Wirtualnej platformy Azure.
> 
> 

Po kliknięciu **OK** hello alert jest skonfigurowany i w przypadku wybrania hello opcja toocreate nowe konto automatyzacji jest tworzony wraz z hello nazwy głównej usługi.  Może to zająć kilka sekund toocomplete.  

![Element Runbook jest skonfigurowany](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

Po zakończeniu konfiguracji hello zobaczysz hello nazwa elementu runbook hello są wyświetlane w hello **dodać regułę alertu** bloku.

![Element Runbook jest skonfigurowany](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

Kliknij przycisk **OK** w hello **dodać regułę alertu** bloku i hello reguły alertu zostanie utworzona i aktywowane, jeśli maszyna wirtualna hello jest w stanie uruchomienia.

### <a name="enable-or-disable-a-runbook"></a>Włącz lub wyłącz elementu runbook
Bez usuwania konfiguracji elementu runbook hello je wyłączyć elementu runbook skonfigurowane dla alertu. Pozwala tookeep hello alertów uruchomiona i może testowania niektórych reguł alertów hello i później ponownie włączyć hello elementu runbook.

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a>Tworzenie elementu runbook, który współpracuje z Azure alertu
Po wybraniu elementu runbook w ramach platformy Azure reguły alertu hello elementu runbook musi toohave logikę w nim toomanage hello dane alertów przekazywany tooit.  Jeśli element runbook jest skonfigurowany w regule alertu, elementu webhook jest tworzona dla elementu runbook hello; tego elementu webhook jest używane toostart hello runbook każdej czasu hello alertu wyzwalaczy.  Witaj rzeczywiste wywołanie toostart hello runbook jest adres URL elementu webhook toohello żądania HTTP POST. Witaj treści żądania POST hello zawiera sformatowane JSON obiekt, który zawiera przydatne właściwości powiązanych toohello alert.  Jak widać poniżej, dane alertów hello zawiera szczegóły, takie jak identyfikator subskrypcji, grupy zasobów o nazwie resourceName i typu zasobu.

### <a name="example-of-alert-data"></a>Przykład danych alertu
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

Odebrania hello usługi elementu webhook usługi Automatyzacja hello HTTP POST wyodrębnia dane alertów hello i przekazuje je toohello runbook parametr wejściowy hello WebhookData elementu runbook.  Poniżej przedstawiono przykładowy element runbook, pokazujący sposób toouse hello parametru WebhookData i wyodrębniania danych alertów hello i korzystać z niego hello toomanage zasobów platformy Azure, która wyzwoliła hello alert.

### <a name="example-runbook"></a>Przykładowy element runbook
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

## <a name="summary"></a>Podsumowanie
Podczas konfigurowania alertu na maszynie Wirtualnej platformy Azure, masz teraz hello tooeasily możliwości konfigurowania automatyzacji runbook tooautomatically wykonania akcji korygowania podczas wyzwala hello alertu. W tej wersji możesz wybrać spośród elementów runbook toorestart, Zatrzymaj, lub usuń Maszynę wirtualną w zależności od danego scenariusza alertu. Jest to początek tylko hello włączenie scenariuszy, w którym kontrolować akcje hello (powiadomienia, rozwiązywania problemów, korygowania), które zostaną wykonane automatycznie po wyzwala alert.

## <a name="next-steps"></a>Następne kroki
* tooget wprowadzenie do graficznych elementów runbook, zobacz [Mój pierwszy graficznym elementem runbook](automation-first-runbook-graphical.md)
* tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md)
* Zobacz toolearn więcej informacji na temat typów elementów runbook, ich zalety i ograniczenia, [typy elementu runbook usługi Automatyzacja Azure](automation-runbook-types.md)

