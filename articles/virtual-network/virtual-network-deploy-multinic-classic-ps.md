---
title: "Maszyna wirtualna (klasyczna) z wieloma kartami sieciowymi — programu Azure PowerShell aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate maszyna wirtualna (klasyczna) z wieloma kartami sieciowymi przy użyciu programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a>Tworzenie maszyny Wirtualnej (klasyczne) z wieloma kartami sieciowymi przy użyciu programu PowerShell

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Można tworzyć maszyn wirtualnych (VM) na platformie Azure i dołączyć wiele sieci tooeach interfejsów (NIC) z maszyn wirtualnych. Wiele kart sieciowych włączać rozdzielenie typów ruchu sieciowego między kart sieciowych. Na przykład jedna karta sieciowa może komunikować się z hello Internet, podczas gdy inny komunikuje się tylko z wewnętrznych zasobów nie podłączone toohello Internet. Program Hello możliwości tooseparate ruch sieciowy między wieloma kartami jest wymagany dla wielu urządzeń wirtualnych sieci, takich jak dostarczania aplikacji i rozwiązań Optymalizacja sieci WAN.

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Dowiedz się, jak tooperform te czynności przy użyciu hello [modelu wdrażania usługi Resource Manager](virtual-network-deploy-multinic-arm-ps.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Witaj następujące kroki Użyj grupy zasobów o nazwie *IaaSStory* hello serwerów sieci WEB oraz grupę zasobów o nazwie *IaaSStory zaplecza* dla serwerów hello bazy danych.

## <a name="prerequisites"></a>Wymagania wstępne

Przed utworzeniem hello serwerów bazy danych, należy toocreate hello *IaaSStory* grupy zasobów z wszystkie niezbędne zasoby hello w tym scenariuszu. toocreate tych zasobów, pełny hello kroki, które należy wykonać. Tworzenie sieci wirtualnej, wykonując następujące kroki hello hello [utworzyć sieć wirtualną](virtual-networks-create-vnet-classic-netcfg-ps.md) artykułu.

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>Tworzenie hello zaplecza maszyn wirtualnych
Hello zaplecza maszyny wirtualne są zależne od utworzenia hello hello następujące zasoby:

* **Podsieci wewnętrznej bazy danych**. serwery bazy danych Hello będą częścią osobnej podsieci ruchu toosegregate. Poniższy skrypt Hello oczekuje tooexist tej podsieci w sieci wirtualnej o nazwie *WTestVnet*.
* **Konto magazynu dla dysków z danymi**. W celu poprawy wydajności hello dysków z danymi na serwerach bazy danych hello użyje półprzewodnikowych (SSD) dysku technologii, która wymaga konta magazynu w warstwie premium. Upewnij się, że hello wdrożyć magazyn w warstwie premium toosupport lokalizacji platformy Azure.
* **Zestaw dostępności**. Wszystkie serwery baz danych zostanie dodany zestaw dostępności pojedynczego tooa, tooensure co najmniej jeden z maszyn wirtualnych hello jest uruchomiona podczas konserwacji.

### <a name="step-1---start-your-script"></a>Krok 1 — Uruchom skrypt
Możesz pobrać hello używane pełne skrypt programu PowerShell [tutaj](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1). Wykonaj kroki hello poniżej toochange hello skryptu toowork w danym środowisku.

1. Zmień hello wartości zmiennych hello poniżej oparte na istniejącej grupie zasobów wdrożone powyżej w [wymagania wstępne](#Prerequisites).

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. Zmień hello wartości zmiennych hello poniżej na podstawie wartości hello ma toouse wdrożenia wewnętrznej bazy danych.

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Krok 2 — Tworzenie niezbędne zasoby dla maszyn wirtualnych
Należy toocreate konta dla dysków z danymi hello nową usługę w chmurze i magazynu dla wszystkich maszyn wirtualnych. Należy również toospecify obrazu, a konto administratora lokalnego na powitania maszyn wirtualnych. ukończenie tych zasobów, toocreate hello następujące kroki:

1. Utwórz nową usługę w chmurze.

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. Utwórz nowe konto magazynu premium.

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. Ustaw konto magazynu hello utworzone powyżej jako hello bieżącego konta magazynu dla Twojej subskrypcji.

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. Wybierz obraz powitania maszyny Wirtualnej.

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. Ustaw poświadczenia konta administratora lokalnego hello.

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a>Krok 3 — Tworzenie maszyn wirtualnych
Należy toouse toocreate pętli, jak wiele maszyn wirtualnych, a tworzenie hello niezbędne karty sieciowe i maszyn wirtualnych w pętli hello. toocreate hello kart sieciowych i maszyn wirtualnych, należy wykonać hello następujące kroki.

1. Uruchom `for` hello toorepeat pętli polecenia toocreate Maszynę wirtualną i dwie karty sieciowe, jak tyle razy, na podstawie hello wartości hello `$numberOfVMs` zmiennej.

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. Utwórz `VMConfig` obiektu określenie hello obrazu, rozmiar i zbiór dostępności dla hello maszyny Wirtualnej.

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. Zainicjuj obsługę hello maszyny Wirtualnej jako Maszynę wirtualną systemu Windows.

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. Ustaw domyślny hello karty Sieciowej i przypisz mu statyczny adres IP.

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. Dodawanie drugiej karty Sieciowej dla każdej maszyny Wirtualnej.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. Tworzenie dysków toodata dla każdej maszyny Wirtualnej.

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. Utwórz każdej maszyny Wirtualnej, a koniec hello pętli.

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a>Krok 4 — uruchamianie skryptu hello
Pobrane i zmienić hello skryptu na podstawie Twoich potrzeb, runt on skryptu bazy toocreate hello wewnętrznej bazy danych maszyn wirtualnych z wieloma kartami sieciowymi.

1. Zapisz skrypt i uruchom go z hello **PowerShell** wiersza polecenia lub **PowerShell ISE**. Zobaczysz hello początkowej danych wyjściowych, jak pokazano poniżej.

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. Wypełnij informacje hello potrzebne hello poświadczeń monit i kliknij przycisk **OK**. zwracany jest Hello danych wyjściowych poniżej.

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
