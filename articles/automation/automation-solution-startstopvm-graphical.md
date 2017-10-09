---
title: Wykres aaaStarting i zatrzymywanie maszyn wirtualnych - | Dokumentacja firmy Microsoft
description: "Wersja przepływu pracy programu PowerShell elementów runbook toostart i Zatrzymaj klasycznych maszyn wirtualnych w tym scenariuszu usługi Automatyzacja Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 62d93170-ca3d-42ef-ac1d-6d50b61ac87d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 5add8d8cf35ea2e89a570744755ac7db0a6feb07
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

To jest wersja graficznym elementem runbook hello tego scenariusza. Jest również dostępny za pomocą [elementach runbook przepływu pracy programu PowerShell](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-hello-scenario"></a>Pobieranie hello scenariusza
W tym scenariuszu składa się z dwóch Witaj dwie graficznych elementów runbook, które mogą pobierać z następujących łączy.  Zobacz hello [przepływu pracy programu PowerShell w wersji](automation-solution-startstopvm-psworkflow.md) tego scenariusza dla łącza toohello elementach runbook przepływu pracy programu PowerShell.

| Element Runbook | Link | Typ | Opis |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Start Azure VM klasycznego graficznym elementem Runbook](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Graficzna |Uruchamia wszystkie klasycznych maszyn wirtualnych w subskrypcji platformy Azure lub wszystkich maszyn wirtualnych o nazwie określonej usługi. |
| StopAzureClassicVM |[Zatrzymaj Azure VM klasycznego graficznym elementem Runbook](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Graficzna |Powoduje zatrzymanie wszystkich maszyn wirtualnych w konto usługi Automatyzacja lub wszystkich maszyn wirtualnych o nazwie określonej usługi. |

## <a name="installing-and-configuring-hello-scenario"></a>Instalowanie i konfigurowanie hello scenariusza
### <a name="1-install-hello-runbooks"></a>1. Zainstaluj hello elementów runbook
Po pobraniu hello elementów runbook, można je zaimportować przy użyciu procedury hello w [procedury graficznym elementem runbook](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-hello-description-and-requirements"></a>2. Przejrzyj opis hello i wymagania
elementy runbook Hello obejmują działania o nazwie **odczytu mnie** zawierającą opis i wymagane zasoby.  Informacje te można wyświetlić, wybierając hello **odczytu mnie** działania, a następnie hello **skrypt przepływu pracy** parametru.  Można także uzyskać hello tych samych informacji z tego artykułu.

### <a name="3-configure-assets"></a>3. Konfigurowanie zasobów
elementy runbook Hello wymagają hello następujące zasoby, które należy utworzyć i umieścić odpowiednie wartości.  nazwy Hello są domyślne.  Można użyć zasoby o różnych nazwach określenia nazwy w hello [parametrów wejściowych](#using-the-runbooks) podczas uruchamiania elementu runbook hello.

| Typ zasobu | Domyślna nazwa | Opis |
|:--- |:--- |:--- |:--- |
| [Poświadczenia](automation-credentials.md) |AzureCredential |Zawiera poświadczenia dla konta, które ma urząd toostart i zatrzymanie maszyny wirtualnej w hello subskrypcji platformy Azure. |
| [Zmienna](automation-variables.md) |AzureSubscriptionId |Zawiera identyfikator subskrypcji hello subskrypcji platformy Azure. |

## <a name="using-hello-scenario"></a>Przy użyciu hello scenariusza
### <a name="parameters"></a>Parametry
Witaj elementy runbook każdej mają następujące hello [parametrów wejściowych](automation-starting-a-runbook.md#runbook-parameters).  Należy podać wartości parametrów obowiązkowych i opcjonalnie można podać wartości innych parametrów w zależności od wymagań.

| Parametr | Typ | Obowiązkowy | Opis |
|:--- |:--- |:--- |:--- |
| ServiceName |Ciąg |Nie |Jeśli podano wartość, wszystkich maszyn wirtualnych o tej nazwie Usługa jest uruchomiona lub zatrzymana.  Jeśli wartość nie zostanie podana, klasycznych maszyn wirtualnych w hello subskrypcji platformy Azure jest uruchomiona lub zatrzymana. |
| AzureSubscriptionIdAssetName |Ciąg |Nie |Zawiera nazwę hello hello [zasób zmiennej](#installing-and-configuring-the-scenario) zawierający identyfikator subskrypcji hello subskrypcji platformy Azure.  Jeśli nie określisz wartości, *AzureSubscriptionId* jest używany. |
| AzureCredentialAssetName |Ciąg |Nie |Zawiera nazwę hello hello [zasób poświadczeń](#installing-and-configuring-the-scenario) zawierający poświadczenia hello hello toouse elementu runbook.  Jeśli nie określisz wartości, *AzureCredential* jest używany. |

### <a name="starting-hello-runbooks"></a>Uruchamianie hello elementów runbook
Można użyć dowolnego z metody hello w [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md) toostart albo hello elementów runbook, w tym artykule.

następujące przykładowe polecenia Hello używa toorun środowiska Windows PowerShell **StartAzureClassicVM** toostart wszystkich maszyn wirtualnych o nazwie usługi hello *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Dane wyjściowe
elementy runbook Hello będzie [output komunikat](automation-runbook-output-and-messages.md) dla każdej maszyny wirtualnej, wskazując czy hello uruchomienia lub zatrzymania instrukcji zostało pomyślnie przesłane.  Określony ciąg hello dane wyjściowe toodetermine hello wyników dla każdego elementu runbook można wyszukać.  ciągi danych wyjściowych Hello są wyświetlane w hello w poniższej tabeli.

| Element Runbook | Warunek | Komunikat |
|:--- |:--- |:--- |
| StartAzureClassicVM |Maszyna wirtualna jest już uruchomiona. |MyVM jest już uruchomiony. |
| StartAzureClassicVM |Żądanie uruchomienia maszyny wirtualnej utworzone pomyślnie |MyVM została uruchomiona. |
| StartAzureClassicVM |Żądanie uruchomienia maszyny wirtualnej nie powiodło się. |Toostart MyVM nie powiodło się |
| StopAzureClassicVM |Maszyna wirtualna jest już uruchomiona. |MyVM jest już zatrzymana. |
| StopAzureClassicVM |Żądanie uruchomienia maszyny wirtualnej utworzone pomyślnie |MyVM została uruchomiona. |
| StopAzureClassicVM |Żądanie uruchomienia maszyny wirtualnej nie powiodło się. |Toostart MyVM nie powiodło się |

Poniżej znajduje się obraz przy użyciu hello **StartAzureClassicVM** jako [podrzędnego elementu runbook](automation-child-runbooks.md) w graficznym przykładowego elementu runbook.  Używa łączy warunkowych hello hello w poniższej tabeli.

| Link | Kryteria |
|:--- |:--- |
| Powodzenie łącza |$ActivityOutput [StartAzureClassicVM] — takie jak "\* została uruchomiona" |
| Błąd łącza |$ActivityOutput [StartAzureClassicVM]-notlike "\* została uruchomiona" |

![Przykład podrzędny element runbook](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>Szczegółowy podział
Poniżej znajduje się szczegółowy podział hello elementów runbook, w tym scenariuszu.  Informacje te można wykorzystać tooeither dostosować hello elementów runbook lub po prostu toolearn ich do tworzenia własnych scenariuszy automatyzacji.

### <a name="authentication"></a>Authentication
![Authentication](media/automation-solution-startstopvm/graphical-authentication.png)

Witaj runbook rozpoczyna się od działań tooset hello [poświadczenia](automation-credentials.md) i subskrypcji Azure, która będzie służyć do reszty hello hello elementu runbook.

Witaj pierwsze dwa działania **Uzyskaj identyfikator subskrypcji** i **uzyskać poświadczenia usługi Azure**, pobrać hello [zasoby](#installing-the-runbook) używanych przez hello następne dwa działania.  Te działania bezpośrednio można określić hello zasoby, ale muszą hello nazwy zasobów.  Ponieważ firma Microsoft umożliwia toospecify użytkownika hello tych nazw w hello [parametrów wejściowych](#using-the-runbooks), potrzebujemy tych działań tooretrieve hello zasobów o nazwie określonej przez parametr wejściowy.

**Dodaj-AzureAccount** zestawy hello poświadczenia, które będą używane do reszty hello hello elementu runbook.  zasób poświadczeń Hello pobierającej z **uzyskać poświadczenia Azure** musi mieć dostęp toostart i zatrzymanie maszyny wirtualnej w hello subskrypcji platformy Azure.  Witaj subskrypcji, która jest używana jest wybierany przez **AzureSubscription wybierz** hello subskrypcji o Id, który używa z **Uzyskaj identyfikator subskrypcji**.

### <a name="get-virtual-machines"></a>Pobierz maszyny wirtualne
![Pobierz maszyny wirtualne](media/automation-solution-startstopvm/graphical-getvms.png)

Witaj runbook wymaga toodetermine maszyn wirtualnych go będzie działać z i określa, czy są one już uruchomiona, lub zatrzymane (w zależności od elementu runbook hello).   Jeden z dwóch działań pobierze hello maszyn wirtualnych.  **Pobierz maszyny wirtualne w usłudze** zostanie uruchomiony, gdy hello *ServiceName* parametru wejściowego dla elementu runbook hello zawiera nieprawidłową wartość.  **Pobierz wszystkie maszyny wirtualne** zostanie uruchomiony, gdy hello *ServiceName* parametru wejściowego dla elementu runbook hello nie zawiera wartości.  Istotą takiej logiki jest wykonywane przez hello łączy warunkowych przed każdym działaniu.

Witaj korzystają zarówno działania **Get-AzureVM** polecenia cmdlet.  **Pobierz wszystkie maszyny wirtualne** hello używa **ListAllVMs** ustawiony parametr tooreturn wszystkich maszyn wirtualnych.  **Pobierz maszyny wirtualne w usłudze** hello używa **GetVMByServiceAndVMName** parametru zestawu oraz udostępnia hello **ServiceName** parametru wejściowego dla hello **ServiceName**parametru.  

### <a name="merge-vms"></a>Scal maszyny wirtualne
![Scal maszyny wirtualne](media/automation-solution-startstopvm/graphical-mergevms.png)

Hello **scalania maszyn wirtualnych** działanie jest wymagane tooprovide wejściowych zbyt**Start AzureVM** co wymaga hello nazwy i nazwy usługi hello toostart wirtualne.  Czy dane wejściowe może pochodzić z jednej **pobrania wszystkich maszyn wirtualnych** lub **uzyskać maszyn wirtualnych w usłudze**, ale **Start AzureVM** można określić tylko jedno działanie dla jej danych wejściowych.   

Scenariusz Hello jest toocreate **scalania maszyn wirtualnych** uruchamia hello **Write-Output** polecenia cmdlet.  Witaj **InputObject** parametr dla tego polecenia cmdlet jest wyrażenie programu PowerShell, które łączy dane wejściowe hello hello poprzednich dwóch działań.  Tylko jeden z tych działań zostanie uruchomiony tylko jeden zestaw danych wyjściowych jest oczekiwany.  **Początek AzureVM** za pomocą tego raportu można jego parametrów wejściowych.

### <a name="startstop-virtual-machines"></a>Uruchamianie/zatrzymywanie maszyn wirtualnych
![Uruchom maszyny wirtualne](media/automation-solution-startstopvm/graphical-startvm.png) ![Zatrzymanie maszyny wirtualne](media/automation-solution-startstopvm/graphical-stopvm.png)

W zależności od hello runbook działania dalej hello podejmować toostart lub zatrzymać hello runbook za pomocą **Start AzureVM** lub **Stop-AzureVM**.  Ponieważ działania hello jest poprzedzony link potoku, uruchomi on raz dla każdego obiektu zwróconego z **scalania maszyn wirtualnych**.  Witaj łącze jest warunkowego, aby hello działania zostanie uruchomiony tylko wtedy, jeśli hello *RunningState* hello maszyny wirtualnej jest *zatrzymane* dla **Start AzureVM** i  *Rozpoczęto* dla **Stop-AzureVM**. Jeśli ten warunek nie jest spełniony, następnie **powiadomić już uruchomiona** lub **powiadomić już zatrzymana** jest uruchomienie toosend komunikat przy użyciu **Write-Output**.

### <a name="send-output"></a>Wyślij dane wyjściowe
![Powiadom Start maszyny wirtualne](media/automation-solution-startstopvm/graphical-notifystart.png) ![Powiadom zatrzymania maszyny wirtualne](media/automation-solution-startstopvm/graphical-notifystop.png)

Ostatnim krokiem hello runbook Hello jest dane wyjściowe toosend czy hello start lub pomyślnie przesłano żądanie zatrzymania dla każdej maszyny wirtualnej. Brak oddzielnej **Write-Output** działanie dla każdego z nich, i określić, które toorun jednego z łączami warunkowymi.  **Powiadom uruchomiona maszyna wirtualna** lub **powiadomić zatrzymana maszyna wirtualna** zostanie wykonany, jeżeli *OperationStatus* jest *zakończyło się pomyślnie*.  Jeśli *OperationStatus* jest następnie wszelkie inne wartości **tooStart powiadomienia nie powiodło się** lub **tooStop powiadomienia nie powiodło się** jest uruchamiany.

## <a name="next-steps"></a>Następne kroki
* [Graficzny tworzenia w programie usługi Automatyzacja Azure](automation-graphical-authoring-intro.md)
* [Podrzędne elementy runbook automatyzacji Azure](automation-child-runbooks.md)
* [Element Runbook danych wyjściowych i komunikatów w usłudze Automatyzacja Azure](automation-runbook-output-and-messages.md)
