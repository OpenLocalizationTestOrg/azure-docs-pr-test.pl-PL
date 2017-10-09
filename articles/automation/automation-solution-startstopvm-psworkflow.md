---
title: "aaaStarting i zatrzymywanie maszyn wirtualnych w usłudze Automatyzacja Azure — przepływ pracy programu PowerShell | Dokumentacja firmy Microsoft"
description: "Wersja graficznego elementów runbook toostart i Zatrzymaj klasycznych maszyn wirtualnych w tym scenariuszu usługi Automatyzacja Azure."
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
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Scenariusz automatyzacji Azure — uruchamianie i zatrzymywanie maszyn wirtualnych
Ten scenariusz automatyzacji Azure zawiera elementy runbook toostart i Zatrzymaj klasycznych maszyn wirtualnych.  Dla każdego z następujących hello można użyć tego scenariusza:  

* Używanie elementów runbook hello bez żadnych modyfikacji, we własnym środowisku.
* Zmodyfikuj hello elementów runbook tooperform dostosować funkcjonalność.  
* Wywołaj hello elementów runbook z innego elementu runbook jako część ogólnego rozwiązania.
* Używanie elementów runbook hello jako elementu runbook toolearn samouczki tworzenia pojęcia.

> [!div class="op_single_selector"]
> * [Element graficzny](automation-solution-startstopvm-graphical.md)
> * [Przepływ pracy programu PowerShell](automation-solution-startstopvm-psworkflow.md)
> 
> 

Jest to hello wersji elementu runbook przepływu pracy programu PowerShell tego scenariusza. Jest również dostępny za pomocą [graficznych elementów runbook](automation-solution-startstopvm-graphical.md).

## <a name="getting-hello-scenario"></a>Pobieranie hello scenariusza
Ten scenariusz zawiera dwa elementy runbook przepływu pracy programu PowerShell, które można pobrać z następującego łącza hello.  Zobacz hello [wersji graficznego](automation-solution-startstopvm-graphical.md) tego scenariusza dla łącza toohello graficznych elementów runbook.

| Element Runbook | Link | Typ | Opis |
|:--- |:--- |:--- |:--- |
| Start AzureVMs |[Uruchom maszyny wirtualne platformy Azure Classic](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |Przepływ pracy programu PowerShell |Uruchamia wszystkie klasycznych maszyn wirtualnych w Azure subscriptionor wszystkich maszyn wirtualnych o nazwie określonej usługi. |
| Stop-AzureVMs |[Zatrzymaj Azure klasycznych maszyn wirtualnych](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |Przepływ pracy programu PowerShell |Powoduje zatrzymanie wszystkich maszyn wirtualnych w konto usługi Automatyzacja lub wszystkich maszyn wirtualnych o nazwie określonej usługi. |

## <a name="installing-and-configuring-hello-scenario"></a>Instalowanie i konfigurowanie hello scenariusza
### <a name="1-install-hello-runbooks"></a>1. Zainstaluj hello elementów runbook
Po pobraniu hello elementów runbook, można je zaimportować przy użyciu procedury hello w [importowanie elementu Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).

### <a name="2-review-hello-description-and-requirements"></a>2. Przejrzyj opis hello i wymagania
elementy runbook Hello obejmują tekst pomocy komentarze, który zawiera opis i wymagane zasoby.  Można także uzyskać hello tych samych informacji z tego artykułu.

### <a name="3-configure-assets"></a>3. Konfigurowanie zasobów
elementy runbook Hello wymagają hello następujące zasoby, które należy utworzyć i umieścić odpowiednie wartości.

| Typ zasobu | Nazwa zasobu | Opis |
|:--- |:--- |:--- |:--- |
| Poświadczenie |AzureCredential |Zawiera poświadczenia dla konta, które ma urząd toostart i zatrzymanie maszyny wirtualnej w hello subskrypcji platformy Azure.  Alternatywnie można określić innego zasobu poświadczeń w hello **poświadczeń** parametru hello **Add-AzureAccount** działania. |
| Zmienna |AzureSubscriptionId |Zawiera identyfikator subskrypcji hello subskrypcji platformy Azure. |

## <a name="using-hello-scenario"></a>Przy użyciu hello scenariusza
### <a name="parameters"></a>Parametry
Witaj runbook mają hello następujące parametry.  Należy podać wartości parametrów obowiązkowych i opcjonalnie można podać wartości innych parametrów w zależności od wymagań.

| Parametr | Typ | Obowiązkowy | Opis |
|:--- |:--- |:--- |:--- |
| ServiceName |Ciąg |Nie |Jeśli podano wartość, wszystkich maszyn wirtualnych o tej nazwie Usługa jest uruchomiona lub zatrzymana.  Jeśli wartość nie zostanie podana, klasycznych maszyn wirtualnych w hello subskrypcji platformy Azure jest uruchomiona lub zatrzymana. |
| AzureSubscriptionIdAssetName |Ciąg |Nie |Zawiera nazwę hello hello [zasób zmiennej](#installing-and-configuring-the-scenario) zawierający identyfikator subskrypcji hello subskrypcji platformy Azure.  Jeśli nie określisz wartości, *AzureSubscriptionId* jest używany. |
| AzureCredentialAssetName |Ciąg |Nie |Zawiera nazwę hello hello [zasób poświadczeń](#installing-and-configuring-the-scenario) zawierający poświadczenia hello hello toouse elementu runbook.  Jeśli nie określisz wartości, *AzureCredential* jest używany. |

### <a name="starting-hello-runbooks"></a>Uruchamianie hello elementów runbook
Można użyć dowolnego z metody hello w [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md) toostart albo hello elementów runbook, w tym scenariuszu.

następujące przykładowe polecenia Hello używa toorun środowiska Windows PowerShell **StartAzureVMs** toostart wszystkich maszyn wirtualnych o nazwie usługi hello *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>Dane wyjściowe
elementy runbook Hello będzie [output komunikat](automation-runbook-output-and-messages.md) dla każdej maszyny wirtualnej, wskazując czy hello uruchomienia lub zatrzymania instrukcji zostało pomyślnie przesłane.  Określony ciąg hello dane wyjściowe toodetermine hello wyników dla każdego elementu runbook można wyszukać.  ciągi danych wyjściowych Hello są wyświetlane w hello w poniższej tabeli.

| Element Runbook | Warunek | Komunikat |
|:--- |:--- |:--- |
| Start AzureVMs |Maszyna wirtualna jest już uruchomiona. |MyVM jest już uruchomiony. |
| Start AzureVMs |Żądanie uruchomienia maszyny wirtualnej utworzone pomyślnie |MyVM została uruchomiona. |
| Start AzureVMs |Żądanie uruchomienia maszyny wirtualnej nie powiodło się. |Toostart MyVM nie powiodło się |
| Stop-AzureVMs |Maszyna wirtualna jest już zatrzymana. |MyVM jest już zatrzymana. |
| Stop-AzureVMs |Zatrzymaj żądanie pomyślnie przesłano maszyny wirtualnej |MyVM została zatrzymana. |
| Stop-AzureVMs |Żądanie zatrzymania maszyny wirtualnej nie powiodło się |Toostop MyVM nie powiodło się |

Na przykład hello następującego fragmentu kodu z elementu runbook prób toostart wszystkich maszyn wirtualnych o nazwie usługi hello *MyServiceName*.  Jeśli hello początkowym Niepowodzenie żądania, może zostać pobrany akcje błędu.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a>Szczegółowy podział
Poniżej znajduje się szczegółowy podział hello elementów runbook, w tym scenariuszu.  Informacje te można wykorzystać tooeither dostosować hello elementów runbook lub po prostu toolearn ich do tworzenia własnych scenariuszy automatyzacji.

### <a name="parameters"></a>Parametry
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

Witaj przepływ pracy uruchamiany przez pobieranie hello wartości dla hello [parametrów wejściowych](#using-the-scenario).  Jeśli nie podano nazwy zasobów hello są używane domyślne nazwy.

### <a name="output"></a>Dane wyjściowe
    # Returns strings with status messages
    [OutputType([String])]

Ten wiersz deklaruje, że hello hello runbook będą zwracać ciąg.  To nie jest wymagana, ale jest najlepszym rozwiązaniem w przypadku gdy hello runbook jest używany jako [podrzędnego elementu runbook](automation-child-runbooks.md) tak, aby nadrzędny element runbook będzie wiadomo, dane wyjściowe hello wpisz tooexpect.

### <a name="authentication"></a>Authentication
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

Następne wiersze Hello ustawić hello [poświadczenia](automation-credentials.md) i subskrypcji Azure, która będzie służyć do reszty hello hello elementu runbook.
Najpierw używamy **Get-AutomationPSCredential** tooget hello zawartości, który przechowuje poświadczenia hello z dostępem do toostart i zatrzymywanie maszyn wirtualnych w hello subskrypcji platformy Azure. **Dodaj-AzureAccount** następnie używa tego poświadczenia hello tooset zasobów.  dane wyjściowe Hello zostanie przypisana zmienna fikcyjny tooa, dzięki czemu nie jest zawarte w danych wyjściowych elementu runbook hello.  

zasób zmiennej Hello z subskrypcją hello identyfikator następnie są pobierane z **Get-AutomationVariable** i ustawić o subskrypcji hello **AzureSubscription wybierz**.

### <a name="get-vms"></a>Pobierz maszyny wirtualne
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-AzureVM** jest tooretrieve używanych maszyn wirtualnych hello hello element runbook będzie współpracować.  Jeśli wartość jest podana w hello **ServiceName** dane wejściowe są pobierane w zmiennej, a następnie tylko maszyny wirtualne hello o tej nazwie usługi.  Jeśli **ServiceName** jest pusta, a następnie są pobierane wszystkie maszyny wirtualne.

### <a name="startstop-virtual-machines-and-send-output"></a>Uruchamiania/zatrzymywania maszyn wirtualnych i Wyślij dane wyjściowe
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

Witaj następnego kroku wierszy za pomocą każdej maszyny wirtualnej.  Najpierw hello **PowerState** hello maszyny wirtualnej jest zaznaczone toosee Jeśli już jest uruchomiona lub zatrzymana, w zależności od hello elementu runbook.  Jeśli jest już w stanie docelowym hello, wiadomość jest wysyłana toooutput i hello zakończenia elementu runbook.  Jeśli nie, następnie **Start AzureVM** lub **Stop AzureVM** jest używane tooattempt toostart lub zatrzymania hello maszyny wirtualnej z wynikiem hello zmiennej przechowywanej tooa żądania hello.  Komunikat jest następnie wysyłana określenie toooutput czy toostart żądania hello lub Zatrzymaj zostało pomyślnie przesłane.

## <a name="next-steps"></a>Następne kroki
* toolearn więcej informacji na temat pracy z podrzędnych elementów runbook, zobacz [podrzędnych elementów runbook automatyzacji Azure](automation-child-runbooks.md)
* więcej informacji o toolearn output komunikaty podczas wykonywania elementu runbook i rejestrowanie toohelp Rozwiązywanie problemów z, zobacz [Runbook dane wyjściowe i komunikaty w automatyzacji Azure](automation-runbook-output-and-messages.md)

