---
title: "tooResource aaaMigrate Manager przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono hello obsługiwane platformy migracji zasobów IaaS, takich jak maszynach wirtualnych (VM), sieci wirtualnych (sieci wirtualne) oraz kont magazynu z klasycznym tooAzure Resource Manager (ARM) za pomocą poleceń programu PowerShell systemu Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a>Migracja zasobów IaaS z klasycznym tooAzure Resource Manager przy użyciu programu Azure PowerShell
Te kroki pokazują, jak toouse programu Azure PowerShell poleceń toomigrate infrastruktura jako usługa (IaaS) zasoby z modelu wdrażania usługi Azure Resource Manager toohello hello wdrażania klasycznego modelu.

Należy również przeprowadzić migrację zasobów za pomocą hello [interfejsu wiersza polecenia platformy Azure (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).

* Aby uzyskać podstawowe informacje dotyczące obsługiwanych scenariuszy migracji, zobacz [obsługiwane platformy migracji zasobów IaaS z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-overview.md).
* Aby uzyskać szczegółowe wskazówki i Przewodnik migracji, zobacz [techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).
* [Przegląd najbardziej typowych błędów migracji](migration-classic-resource-manager-errors.md)

<br>
Poniżej przedstawiono kolejność hello tooidentify schemat blokowy, w którym kroki należy wykonać podczas procesu migracji toobe

![Zrzut ekranu pokazujący hello kroków migracji](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a>Krok 1: Planowanie migracji
Poniżej przedstawiono kilka najlepsze rozwiązania, które firma Microsoft zaleca jako ocenić migracji zasobów IaaS z klasycznym tooResource Menedżera:

* Zapoznaj się z artykułem hello [obsługiwane i nieobsługiwane funkcje i konfiguracje](migration-classic-resource-manager-overview.md). Jeśli masz maszyn wirtualnych, które używają nieobsługiwane konfiguracje i funkcje, firma Microsoft zaleca, poczekaj toobe obsługi funkcji/Konfiguracja hello anonsowania. Jeśli zgodnie z potrzebami, Usuń tej funkcji lub przenieść poza migracji tooenable tej konfiguracji.
* Jeśli mają automatyczny skrypty, które obecnie wdrażanie infrastruktury i aplikacji, spróbuj toocreate podobnych konfiguracji testu przy użyciu tych skryptów do migracji. Można też skonfigurować próbkę środowiskami przy użyciu hello portalu Azure.

> [!IMPORTANT]
> Migracji z klasycznym tooResource Menedżera bramy aplikacji nie są obecnie obsługiwane. toomigrate klasycznej sieci wirtualnej z bramy aplikacji usunąć bramę hello przed uruchomieniem operacji Prepare toomove hello sieci. Po zakończeniu migracji hello ponownie hello bramy w usłudze Azure Resource Manager.
>
>Łączenie obwody tooExpressRoute w innej subskrypcji bram usługi ExpressRoute nie może być migrowane automatycznie. W takiej sytuacji należy usunąć bramę usługi ExpressRoute hello, migrację sieci wirtualnej hello i Utwórz ponownie hello bramy. Zobacz [ExpressRoute migracji obwody i skojarzone sieci wirtualne od modelu wdrażania Menedżera zasobów klasycznych toohello hello](../../expressroute/expressroute-migration-classic-resource-manager.md) Aby uzyskać więcej informacji.
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a>Krok 2: Zainstaluj najnowszą wersję hello programu Azure PowerShell
Istnieją dwa główne opcje tooinstall programu Azure PowerShell: [galerii programu PowerShell](https://www.powershellgallery.com/profiles/azure-sdk/) lub [Instalatora platformy sieci Web (WebPI)](http://aka.ms/webpi-azps). WebPI odbiera comiesięcznych aktualizacji. Galerii programu PowerShell odbiera aktualizacje w sposób ciągły. W tym artykule jest oparta na program Azure PowerShell w wersji 2.1.0.

Aby uzyskać instrukcje instalacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a>Krok 3: Upewnij się, że jesteś administratorem subskrypcji hello w portalu Azure
tooperform tej migracji, musi zostać dodany jako współadministrator subskrypcji hello w hello [portalu Azure](https://portal.azure.com).

1. Zaloguj się na powitania [portalu Azure](https://portal.azure.com).
2. W menu Centrum hello wybierz **subskrypcji**. Jeśli nie widzisz, wybierz **więcej usług**.
3. Znajdź hello subskrypcji odpowiedni wpis, a następnie przyjrzeć się hello **Moje roli** pola. Dla administratora współpracującego, hello wartość powinna być _administrator konta_.

Jeśli nie jest możliwe tooadd współadministratorem, następnie skontaktuj się z administratorem usługi ani współadministratorem tooget subskrypcji hello dodane przez użytkownika.   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a>Krok 4: Ustaw subskrypcji i zaloguj do migracji
Najpierw należy uruchomić wiersz programu PowerShell. W przypadku migracji należy tooset Twojego środowiska dla obu classic i Menedżera zasobów.

Zaloguj się konta tooyour hello modelu Resource Manager.

```powershell
    Login-AzureRmAccount
```

Uzyskiwanie hello dostępnych subskrypcji przy użyciu hello następujące polecenie:

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

Ustaw subskrypcji platformy Azure dla hello bieżącej sesji. W tym przykładzie ustawia domyślną nazwę subskrypcji hello zbyt**moją subskrypcję Azure**. Zamień nazwę subskrypcji przykład hello własne.

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> Rejestracja jest jednorazowe krok, ale należy to robić raz przed próbą wykonania migracji. Bez rejestrowania, zobacz temat hello następujący komunikat o błędzie:
>
> *Element BadRequest: Subskrypcja nie jest zarejestrowana do migracji.*
>
>

Rejestracja dostawcy zasobów migracji hello za pomocą następującego polecenia hello:

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Poczekaj pięć minut hello toofinish rejestracji. Stan hello zatwierdzenia hello można sprawdzić za pomocą następującego polecenia hello:

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Upewnij się, że jest RegistrationState `Registered` przed kontynuowaniem.

Teraz Zaloguj się na koncie tooyour hello klasycznego modelu.

```powershell
    Add-AzureAccount
```

Uzyskiwanie hello dostępnych subskrypcji przy użyciu hello następujące polecenie:

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

Ustaw subskrypcji platformy Azure dla hello bieżącej sesji. W tym przykładzie subskrypcji domyślne hello zbyt**moją subskrypcję Azure**. Zamień nazwę subskrypcji przykład hello własne.

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Krok 5: Upewnij się, że masz wystarczająco dużo rdzeni maszyny wirtualnej Azure Resource Manager w hello region platformy Azure dla bieżącego wdrożenia lub sieci Wirtualnej
Możesz użyć hello następującego środowiska PowerShell polecenie toocheck hello bieżąca liczba rdzeni, do których masz usługi Azure Resource Manager. toolearn więcej informacji na temat przydziały core, zobacz [limity i hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).

W tym przykładzie służy do sprawdzania dostępności hello hello **zachodnie stany USA** regionu. Zamień nazwę regionu przykład hello własne.

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a>Krok 6: Uruchamianie poleceń toomigrate zasobów IaaS
> [!NOTE]
> Wszystkie operacje hello opisane w tym miejscu są idempotentności. Jeśli masz problem niż nieobsługiwanej funkcji lub błąd konfiguracji, zalecamy możesz ponowić próbę hello przygotowanie, przerwania lub przekazania operacji. Platforma Hello próbuje hello akcję ponownie.
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a>Krok 6.1: Opcja 1 — migracji maszyn wirtualnych w usłudze w chmurze (nie w sieci wirtualnej)
Pobranie listy hello usługi w chmurze przy użyciu hello następujące polecenie, a następnie usługa w chmurze hello pobrania, które mają toomigrate. Jeśli hello maszyn wirtualnych w usłudze w chmurze hello znajdują się w sieci wirtualnej lub mają one role sieci web lub procesu roboczego, hello polecenie zwróci komunikat o błędzie.

```powershell
    Get-AzureService | ft Servicename
```

Pobierz hello Nazwa wdrożenia dla usługi w chmurze hello. W tym przykładzie nazwa usługi hello jest **Moje usługi**. Nazwa usługi przykład hello należy zastąpić nazwę usługi.

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

Przygotuj maszyny wirtualne hello hello w usłudze w chmurze do migracji. Masz dwie opcje toochoose z.

* **Opcja 1. Migrowanie hello maszyn wirtualnych tooa utworzone platformy sieci wirtualnej**

    Po pierwsze sprawdzanie poprawności w przypadku migrowania usługi w chmurze hello za pomocą następującego polecenia hello:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    Witaj poprzednie polecenie wyświetla wszystkie ostrzeżenia i błędy, które blokują migracji. Jeśli weryfikacja zakończy się pomyślnie, a następnie można przenieść na toohello **Prepare** krok:

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* **Opcja 2. Migrowanie tooan istniejącej sieci wirtualnej w modelu wdrażania usługi Resource Manager hello**

    W tym przykładzie zestawy hello Nazwa grupy zasobów zbyt**myResourceGroup**, zbyt hello wirtualnej nazwy sieciowej**myVirtualNetwork** i hello nazwy podsieci za**mySubNet**. Zamień nazwy hello w przykładzie hello hello nazw własnych zasobów.

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    Po pierwsze sprawdzanie poprawności w przypadku migrowania hello sieci wirtualnej przy użyciu hello następujące polecenie:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    Witaj poprzednie polecenie wyświetla wszystkie ostrzeżenia i błędy, które blokują migracji. Jeśli weryfikacja zakończy się pomyślnie, można przejść z powitania po kroku:

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

Po hello operacji Prepare powiedzie się przy użyciu jednej z hello poprzedzających opcji, należy zbadać stanu migracji hello hello maszyn wirtualnych. Upewnij się, że są one hello `Prepared` stanu.

W tym przykładzie zestawy hello nazwę maszyny Wirtualnej za**myVM**. Zastąp nazwę przykład hello nazwę maszyny Wirtualnej.

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

Sprawdź konfigurację hello hello przygotowany zasobów przy użyciu programu PowerShell lub hello portalu Azure. Jeśli nie jest jeszcze gotowa do migracji i ma toogo toohello wstecz poprzedni stan, użyj hello następujące polecenie:

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

Jeśli hello przygotowane Konfiguracja wygląda dobrze, możesz przejść do przodu i zatwierdzić hello zasobów za pomocą następującego polecenia hello:

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a>Krok 6.1: Opcja 2 — migracji maszyn wirtualnych w sieci wirtualnej

maszyny wirtualne toomigrate w sieci wirtualnej, migracja hello sieci wirtualnej. maszyny wirtualne Hello automatycznie migracji z hello sieci wirtualnej. Pobranie hello sieci wirtualnej, które mają toomigrate.
> [!NOTE]
> [Przeprowadź migrację jednej maszyny wirtualnej klasycznego](migrate-single-classic-to-resource-manager.md) przez utworzenie nowej maszyny wirtualnej usługi Resource Manager z dyskami zarządzane przy użyciu hello plików (systemu operacyjnego i danych) wirtualnego dysku twardego hello maszyny wirtualnej.
<br>

> [!NOTE]
> Nazwa sieci wirtualnej Hello mogą się różnić od co przedstawiono na powitania nowego portalu. Witaj nowego portalu Azure Wyświetla hello nazwę jako `[vnet-name]` , ale nazwa rzeczywista sieci wirtualnej hello jest typu `Group [resource-group-name] [vnet-name]`. Przed migracją wyszukiwania hello rzeczywiste wirtualnej nazwy sieciowej przy użyciu polecenia hello `Get-AzureVnetSite | Select -Property Name` lub wyświetlania w hello starego portalu Azure. 

W tym przykładzie zestawy hello wirtualnej nazwy sieciowej zbyt**myVnet**. Zamień nazwę sieci wirtualnej przykład hello własne.

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> Jeśli sieć wirtualna hello zawiera sieci web lub roli proces roboczy lub maszyn wirtualnych z nieobsługiwaną konfiguracją, otrzymasz komunikat o błędzie weryfikacji.
>
>

Po pierwsze sprawdzanie poprawności w przypadku migrowania hello sieci wirtualnej przy użyciu następującego polecenia hello:

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

Witaj poprzednie polecenie wyświetla wszystkie ostrzeżenia i błędy, które blokują migracji. Jeśli weryfikacja zakończy się pomyślnie, można przejść z powitania po kroku:

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

Sprawdź konfigurację hello hello przygotowany maszyn wirtualnych przy użyciu programu Azure PowerShell lub hello portalu Azure. Jeśli nie jest jeszcze gotowa do migracji i ma toogo toohello wstecz poprzedni stan, użyj hello następujące polecenie:

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

Jeśli hello przygotowane Konfiguracja wygląda dobrze, możesz przejść do przodu i zatwierdzić hello zasobów za pomocą następującego polecenia hello:

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a>Krok 6.2 migracji konta magazynu
Po zakończeniu migracji maszyn wirtualnych hello, zaleca się migrowanie hello kont magazynu.

Przed przeprowadzeniem migracji konta magazynu hello, należy wykonać przed wymagań wstępnych:

* **Migrowanie klasycznych maszyn wirtualnych, których dyski są przechowywane na koncie magazynu hello**

    Poprzedzających polecenie zwraca RoleName i DiskName właściwości wszystkich dysków maszyny Wirtualnej z klasycznym hello hello konta magazynu. RoleName jest nazwa hello hello toowhich maszynę wirtualną, której jest dołączona dysku. Jeśli poprzedzających polecenie zwraca dysków upewnij się, że toowhich maszyny wirtualne są dołączone dyski te są migrowane przed migracją hello konta magazynu.
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* **Usuń przechowywane na koncie magazynu hello niedołączonej klasycznego dysków maszyny Wirtualnej**

    Find niedołączonej klasycznego dysków maszyny Wirtualnej w magazynie hello konta przy użyciu następujących poleceń:

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    Jeśli powyżej polecenie zwraca dysków Usuń te dyski za pomocą następujących poleceń:

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* **Usuń maszyny Wirtualnej obrazy przechowywane na koncie magazynu hello**

    Poprzedzających polecenie zwraca wszystkie obrazy maszyny Wirtualnej hello dysku systemu operacyjnego przechowywanego w hello konta magazynu.
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     Poprzedzających polecenie zwraca wszystkie obrazy maszyny Wirtualnej hello z dyskami danych przechowywane na koncie magazynu hello.
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    Usuń wszystkie obrazy maszyny Wirtualnej hello zwrócony przez powyżej poleceń przy użyciu poprzedniego polecenia:
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

Sprawdzanie poprawności każdego konta magazynu dla migracji za pomocą hello następujące polecenia. W tym przykładzie nazwa konta magazynu hello jest **Mojekontomagazynu**. Zamień hello Przykładowa nazwa hello nazwę konta magazynu.

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

Następnym krokiem jest tooPrepare hello konto magazynu na potrzeby migracji

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

Sprawdź konfigurację hello hello przygotowane konta magazynu przy użyciu programu Azure PowerShell lub hello portalu Azure. Jeśli nie jest jeszcze gotowa do migracji i ma toogo toohello wstecz poprzedni stan, użyj hello następujące polecenie:

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

Jeśli hello przygotowane Konfiguracja wygląda dobrze, możesz przejść do przodu i zatwierdzić hello zasobów za pomocą następującego polecenia hello:

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a>Następne kroki
* [Omówienie migracji zasobów IaaS z klasycznym tooAzure Resource Manager obsługiwane platformy](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Planowanie migracji zasobów IaaS z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Użyj interfejsu wiersza polecenia toomigrate IaaS zasobów z klasycznym tooAzure Resource Manager](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Narzędzia z migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów społeczności](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Przegląd najbardziej typowych błędów migracji](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Hello przeglądu najczęściej zadawane pytania dotyczące migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
