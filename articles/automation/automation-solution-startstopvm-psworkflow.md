---
title: "Uruchamianie i zatrzymywanie maszyn wirtualnych w usłudze Automatyzacja Azure — przepływ pracy programu PowerShell | Dokumentacja firmy Microsoft"
description: "Wersja graficznego elementów runbook, aby uruchomić i zatrzymać klasycznych maszyn wirtualnych w tym scenariuszu usługi Automatyzacja Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Scenariusz automatyzacji Azure — uruchamianie i zatrzymywanie maszyn wirtualnych
Ten scenariusz automatyzacji Azure zawiera elementy runbook, aby uruchomić i zatrzymać klasycznych maszyn wirtualnych.  W tym scenariuszu można użyć dla dowolnego z następujących czynności:  

* Użyj elementów runbook bez żadnych modyfikacji w środowisku.
* Modyfikowanie elementów runbook do wykonania funkcji niestandardowych.  
* Wywoływanie elementów runbook z innego elementu runbook jako część ogólnego rozwiązania.
* Użyj elementów runbook jako samouczki, aby dowiedzieć się pojęcia dotyczące tworzenia elementu runbook.

> [!div class="op_single_selector"]
> * [Element graficzny](automation-solution-startstopvm-graphical.md)
> * [Przepływ pracy programu PowerShell](automation-solution-startstopvm-psworkflow.md)
> 
> 

To jest wersja elementu runbook przepływu pracy programu PowerShell tego scenariusza. Jest również dostępny za pomocą [graficznych elementów runbook](automation-solution-startstopvm-graphical.md).

## <a name="getting-the-scenario"></a>Uzyskiwanie scenariusza
W tym scenariuszu składa się z dwóch elementy runbook przepływu pracy programu PowerShell, które można pobrać z poniższych łączy.  Zobacz [wersji graficznego](automation-solution-startstopvm-graphical.md) tego scenariusza dla łącza do graficznych elementów runbook.

| Element Runbook | Link | Typ | Opis |
|:--- |:--- |:--- |:--- |
| Start AzureVMs |[Uruchom maszyny wirtualne platformy Azure Classic](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |Przepływ pracy programu PowerShell |Uruchamia wszystkie klasycznych maszyn wirtualnych w Azure subscriptionor wszystkich maszyn wirtualnych o nazwie określonej usługi. |
| Stop-AzureVMs |[Zatrzymaj Azure klasycznych maszyn wirtualnych](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |Przepływ pracy programu PowerShell |Powoduje zatrzymanie wszystkich maszyn wirtualnych w konto usługi Automatyzacja lub wszystkich maszyn wirtualnych o nazwie określonej usługi. |

## <a name="installing-and-configuring-the-scenario"></a>Instalowanie i konfigurowanie scenariusza
### <a name="1-install-the-runbooks"></a>1. Zainstaluj elementy runbook
Po pobraniu elementy runbook, można zaimportować je za pomocą procedury w [importowanie elementu Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).

### <a name="2-review-the-description-and-requirements"></a>2. Przejrzyj opis i wymagania
Elementy runbook zawierają tekst pomocy komentarze, który zawiera opis i wymagane zasoby.  Można także uzyskać te same informacje z tego artykułu.

### <a name="3-configure-assets"></a>3. Konfigurowanie zasobów
Elementy runbook wymagają następujące zasoby, które należy utworzyć i umieścić odpowiednie wartości.

| Typ zasobu | Nazwa zasobu | Opis |
|:--- |:--- |:--- |:--- |
| Poświadczenie |AzureCredential |Zawiera poświadczenia dla konta, które ma uprawnienia do uruchamiania i zatrzymywania maszyn wirtualnych w subskrypcji platformy Azure.  Alternatywnie można określić innego zasobu poświadczeń w **poświadczeń** parametr **Add-AzureAccount** działania. |
| Zmienna |AzureSubscriptionId |Zawiera identyfikator subskrypcji z subskrypcją platformy Azure. |

## <a name="using-the-scenario"></a>Przy użyciu tego scenariusza
### <a name="parameters"></a>Parametry
Elementy runbook każdy ma następujące parametry.  Należy podać wartości parametrów obowiązkowych i opcjonalnie można podać wartości innych parametrów w zależności od wymagań.

| Parametr | Typ | Obowiązkowy | Opis |
|:--- |:--- |:--- |:--- |
| ServiceName |Ciąg |Nie |Jeśli podano wartość, wszystkich maszyn wirtualnych o tej nazwie Usługa jest uruchomiona lub zatrzymana.  Jeśli wartość nie zostanie podana, klasycznych maszyn wirtualnych w subskrypcji platformy Azure jest uruchomiona lub zatrzymana. |
| AzureSubscriptionIdAssetName |Ciąg |Nie |Zawiera nazwę [zasób zmiennej](#installing-and-configuring-the-scenario) zawierający identyfikator subskrypcji z subskrypcją platformy Azure.  Jeśli nie określisz wartości, *AzureSubscriptionId* jest używany. |
| AzureCredentialAssetName |Ciąg |Nie |Zawiera nazwę [zasób poświadczeń](#installing-and-configuring-the-scenario) zawierający poświadczenia dla elementu runbook do użycia.  Jeśli nie określisz wartości, *AzureCredential* jest używany. |

### <a name="starting-the-runbooks"></a>Uruchamianie elementów runbook
Można użyć dowolnej z metod w [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md) uruchomić jeden z elementów runbook w tym scenariuszu.

Następujące przykładowe polecenia używa środowiska Windows PowerShell do uruchamiania **StartAzureVMs** na uruchomienie wszystkich maszyn wirtualnych przy użyciu nazwy usługi *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>Dane wyjściowe
Elementy runbook będą [output komunikat](automation-runbook-output-and-messages.md) dla każdej maszyny wirtualnej, wskazującą, czy instrukcję uruchomienia lub zatrzymania zostało pomyślnie przesłane.  Określony ciąg w danych wyjściowych, aby ustalić wyniku dla każdego elementu runbook można wyszukać.  W poniższej tabeli wymieniono ciągi danych wyjściowych.

| Element Runbook | Warunek | Komunikat |
|:--- |:--- |:--- |
| Start AzureVMs |Maszyna wirtualna jest już uruchomiona. |MyVM jest już uruchomiony. |
| Start AzureVMs |Żądanie uruchomienia maszyny wirtualnej utworzone pomyślnie |MyVM została uruchomiona. |
| Start AzureVMs |Żądanie uruchomienia maszyny wirtualnej nie powiodło się. |Nie można uruchomić MyVM |
| Stop-AzureVMs |Maszyna wirtualna jest już zatrzymana. |MyVM jest już zatrzymana. |
| Stop-AzureVMs |Zatrzymaj żądanie pomyślnie przesłano maszyny wirtualnej |MyVM została zatrzymana. |
| Stop-AzureVMs |Żądanie zatrzymania maszyny wirtualnej nie powiodło się |Nie można zatrzymać MyVM |

Na przykład poniższy fragment kodu z elementu runbook podejmowana jest próba uruchomienia wszystkich maszyn wirtualnych przy użyciu nazwy usługi *MyServiceName*.  Jeśli jedna z błędów żądań start, może zostać pobrany akcje błędu.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a>Szczegółowy podział
Poniżej znajduje się szczegółowy podział elementów runbook w tym scenariuszu.  Te informacje można użyć do dostosowania elementy runbook albo też dowiedzieć się od nich używanych do tworzenia własnych scenariuszy automatyzacji.

### <a name="parameters"></a>Parametry
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

Przepływ pracy rozpoczyna się od wartości dla pobrania [parametrów wejściowych](#using-the-scenario).  Jeśli nie podano nazwy zasobów są używane domyślne nazwy.

### <a name="output"></a>Dane wyjściowe
    # Returns strings with status messages
    [OutputType([String])]

Ten wiersz deklaruje, że dane wyjściowe element runbook będzie ciąg.  To nie jest wymagana, ale jest najlepszym rozwiązaniem w przypadku gdy element runbook zostanie użyty jako [podrzędnego elementu runbook](automation-child-runbooks.md) tak, aby nadrzędny element runbook będzie wiedzieć, oczekiwany typ danych wyjściowych.

### <a name="authentication"></a>Authentication
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

Następnej linii zestaw [poświadczenia](automation-credentials.md) i subskrypcji platformy Azure, który będzie używany w pozostałej części elementu runbook.
Najpierw używamy **Get-AutomationPSCredential** można pobrać zawartości, który przechowuje poświadczenia z dostępem do uruchamiania i zatrzymywania maszyn wirtualnych w subskrypcji platformy Azure. **Dodaj-AzureAccount** następnie używa tego zasobu można ustawić poświadczenia.  Dane wyjściowe jest przypisany do zmiennej zastępczego, dzięki czemu nie jest zawarte w danych wyjściowych elementu runbook.  

Zasób zmiennej z subskrypcją identyfikator następnie są pobierane z **Get-AutomationVariable** i subskrypcji ustawiony za pomocą **AzureSubscription wybierz**.

### <a name="get-vms"></a>Pobierz maszyny wirtualne
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-AzureVM** służy do pobierania element runbook będzie działać z maszyn wirtualnych.  Jeśli wartość jest podana w **ServiceName** wejściowych zmiennej, a następnie są pobierane tylko maszyn wirtualnych o tej nazwie usługi.  Jeśli **ServiceName** jest pusta, a następnie są pobierane wszystkie maszyny wirtualne.

### <a name="startstop-virtual-machines-and-send-output"></a>Uruchamiania/zatrzymywania maszyn wirtualnych i Wyślij dane wyjściowe
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

Następnym krokiem wierszy za pomocą każdej maszyny wirtualnej.  Pierwszy **PowerState** maszyny wirtualnej jest sprawdzane w celu sprawdzenia, jeśli jest już uruchomiona lub zatrzymana, w zależności od elementu runbook.  Jeśli jest już w stanie docelowej, do danych wyjściowych i zakończenia elementu runbook jest wysyłany komunikat.  Jeśli nie, następnie **Start AzureVM** lub **Stop AzureVM** służy próbę rozpocząć lub zatrzymać maszynę wirtualną w wyniku żądania przechowywane do zmiennej.  Komunikat jest następnie wysyłana do wyjściowego określenie, czy żądanie, aby uruchomić lub zatrzymać zostało pomyślnie przesłane.

## <a name="next-steps"></a>Następne kroki
* Aby dowiedzieć się więcej o pracy z podrzędnych elementów runbook, zobacz [podrzędnych elementów runbook automatyzacji Azure](automation-child-runbooks.md)
* Aby dowiedzieć się więcej o komunikaty wyjściowe podczas wykonywania elementu runbook i rejestrowanie do rozwiązywania problemów, zobacz [Runbook dane wyjściowe i komunikaty w automatyzacji Azure](automation-runbook-output-and-messages.md)

