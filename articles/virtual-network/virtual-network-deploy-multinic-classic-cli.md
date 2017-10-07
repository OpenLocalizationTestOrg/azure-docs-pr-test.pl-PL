---
title: Maszyna wirtualna (klasyczna) z wieloma kartami sieciowymi - Azure CLI 1.0 aaaCreate | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate maszyna wirtualna (klasyczna) z wieloma kartami sieciowymi przy użyciu hello Azure interfejsu wiersza polecenia (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a>Tworzenie maszyny Wirtualnej (klasyczne) z wieloma kartami sieciowymi przy użyciu hello Azure CLI w wersji 1.0

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Można tworzyć maszyn wirtualnych (VM) na platformie Azure i dołączyć wiele sieci tooeach interfejsów (NIC) z maszyn wirtualnych. Wiele kart sieciowych włączać rozdzielenie typów ruchu sieciowego między kart sieciowych. Na przykład jedna karta sieciowa może komunikować się z hello Internet, podczas gdy inny komunikuje się tylko z wewnętrznych zasobów nie podłączone toohello Internet. Program Hello możliwości tooseparate ruch sieciowy między wieloma kartami jest wymagany dla wielu urządzeń wirtualnych sieci, takich jak dostarczania aplikacji i rozwiązań Optymalizacja sieci WAN.

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Dowiedz się, jak tooperform te czynności przy użyciu hello [modelu wdrażania usługi Resource Manager](virtual-network-deploy-multinic-arm-cli.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Witaj następujące kroki Użyj grupy zasobów o nazwie *IaaSStory* hello serwerów sieci WEB oraz grupę zasobów o nazwie *IaaSStory zaplecza* dla serwerów hello bazy danych.

## <a name="prerequisites"></a>Wymagania wstępne
Przed utworzeniem hello serwerów bazy danych, należy toocreate hello *IaaSStory* grupy zasobów z wszystkie niezbędne zasoby hello w tym scenariuszu. toocreate tych zasobów, pełny hello kroki, które należy wykonać. Tworzenie sieci wirtualnej, wykonując następujące kroki hello hello [utworzyć sieć wirtualną](virtual-networks-create-vnet-classic-cli.md) artykułu.

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a>Wdrażanie zaplecza hello maszyny wirtualne
Hello zaplecza maszyny wirtualne są zależne od utworzenia hello hello następujące zasoby:

* **Konto magazynu dla dysków z danymi**. W celu poprawy wydajności hello dysków z danymi na serwerach bazy danych hello użyje półprzewodnikowych (SSD) dysku technologii, która wymaga konta magazynu w warstwie premium. Upewnij się, że hello wdrożyć magazyn w warstwie premium toosupport lokalizacji platformy Azure.
* **Karty sieciowe**. Każda maszyna wirtualna będzie mieć dwie karty sieciowe, jeden dla dostępu do bazy danych, a drugi do zarządzania.
* **Zestaw dostępności**. Wszystkie serwery baz danych zostanie dodany zestaw dostępności pojedynczego tooa, tooensure co najmniej jeden z maszyn wirtualnych hello jest uruchomiona podczas konserwacji.

### <a name="step-1---start-your-script"></a>Krok 1 — Uruchom skrypt
Możesz pobrać hello pełna bash skryptu używanego [tutaj](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh). Wykonaj następujące kroki toochange hello skryptu toowork w danym środowisku hello:

1. Zmień hello wartości zmiennych hello poniżej oparte na istniejącej grupie zasobów wdrożone powyżej w [wymagania wstępne](#Prerequisites).

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. Zmień hello wartości zmiennych hello poniżej na podstawie wartości hello ma toouse wdrożenia wewnętrznej bazy danych.

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Krok 2 — Tworzenie niezbędne zasoby dla maszyn wirtualnych
1. Utwórz nową usługę chmury dla wszystkich maszyn wirtualnych wewnętrznej bazy danych. Użycie hello powiadomienia hello `$backendCSName` zmiennej dla hello Nazwa grupy zasobów, i `$location` dla hello region platformy Azure.

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. Utwórz konto magazynu w warstwie premium dla hello systemu operacyjnego i toobe dysków danych używany przez Twoje maszyn wirtualnych.

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a>Krok 3 — Tworzenie maszyn wirtualnych z wieloma kartami sieciowymi
1. Uruchom toocreate pętli wielu maszyn wirtualnych, oparte na powitania `numberOfVMs` zmiennych.

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. Dla każdej maszyny Wirtualnej Określ nazwę hello i adres IP każdego Witaj dwie karty sieciowe.

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. Utwórz hello maszyny Wirtualnej. Zwróć uwagę, użycie hello hello `--nic-config` parametr zawierający listę wszystkich kart sieciowych podsieci, adresów IP i nazwy.

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. Dla każdej maszyny Wirtualnej należy utworzyć dwa dyski danych.

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a>Krok 4 — uruchamianie skryptu hello
Pobrane i zmienić hello skryptu na podstawie Twoich potrzeb, ponownie uruchom hello skryptu toocreate hello końcowy maszyn wirtualnych bazy danych z wieloma kartami sieciowymi.

1. Zapisz skrypt i uruchom go z Twojego **Bash** terminala. Zobaczysz hello początkowej danych wyjściowych, jak pokazano poniżej.

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. Po kilku minutach zakończy się wykonanie hello i zostanie wyświetlony rest hello hello danych wyjściowych, jak pokazano poniżej.

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
