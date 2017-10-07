---
title: "aaaConfigure prywatnych adresów IP dla maszyn wirtualnych (klasyczne) - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure prywatnych adresów IP maszyn wirtualnych (klasyczne) za pomocą hello Azure interfejsu wiersza polecenia (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a>Konfigurowanie prywatnych adresów IP dla maszyny wirtualnej (klasyczne) przy użyciu hello Azure CLI w wersji 1.0

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

W tym artykule omówiono hello klasycznego modelu wdrażania. Możesz również [Zarządzanie statycznego prywatnego adresu IP w modelu wdrażania usługi Resource Manager hello](virtual-networks-static-private-ip-arm-cli.md).

Poniższe polecenia interfejsu wiersza polecenia Azure próbki Hello oczekiwać środowisku niezłożonym już utworzone. Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, najpierw utworzyć środowisko testowe hello opisane w [utworzyć sieć wirtualną](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Jak toospecify statycznych prywatnych adresów IP podczas tworzenia maszyny Wirtualnej
toocreate nowej maszyny Wirtualnej o nazwie *DNS01* w nową usługę w chmurze o nazwie *TestService* oparte na powyższym scenariuszu hello, wykonaj następujące kroki:

1. Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.
2. Uruchom hello **tworzenia usługi azure** poleceń usługi w chmurze hello toocreate.
   
        azure service create TestService --location uscentral
   
    Oczekiwane dane wyjściowe:
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. Uruchom hello **azure tworzenie maszyny wirtualnej** polecenia toocreate hello maszyny Wirtualnej. Zwróć uwagę, wartość hello statycznego prywatnego adresu IP. Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    Oczekiwane dane wyjściowe:
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * **-l (lub --location)**. Region platformy Azure, w której zostanie utworzona hello maszyny Wirtualnej. W naszym scenariuszu jest to *centralus*.
   * **-n (lub nazwę maszyny wirtualnej —)**. Nazwa hello toobe maszyny Wirtualnej utworzone.
   * **-w (lub--wirtualnej nazwy sieciowej)**. Nazwa hello sieci wirtualnej, w której zostanie utworzona hello maszyny Wirtualnej. 
   * **-S (lub--static ip)**. Statycznego prywatnego adresu IP dla hello maszyny Wirtualnej.
   * **TestService**. Nazwa usługi w chmurze hello której zostanie utworzona hello maszyny Wirtualnej.
   * **bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**. Obraz używany hello toocreate maszyny Wirtualnej.
   * **adminuser**. Administrator lokalny hello maszyny Wirtualnej systemu Windows.
   * **AdminP@ssw0rd**. Hasło administratora lokalnego dla maszyny Wirtualnej systemu Windows hello.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Jak tooretrieve statycznych prywatnych adresów IP informacji dla maszyny Wirtualnej
tooview hello statycznego prywatnego adresu IP adres dla hello maszyny Wirtualnej utworzone za pomocą skryptu hello powyżej, uruchom następujące polecenie z wiersza polecenia platformy Azure hello i sprawdź wartość hello *StaticIP sieci*:

    azure vm static-ip show DNS01

Oczekiwane dane wyjściowe:

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Jak tooremove statycznych prywatnych adresów IP z maszyny Wirtualnej
tooremove hello statycznego prywatnego adresu IP dodane toohello maszyny Wirtualnej w skrypcie hello powyżej hello uruchom następujące polecenie z wiersza polecenia platformy Azure:

    azure vm static-ip remove DNS01

Oczekiwane dane wyjściowe:

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a>Jak tooadd statycznego prywatnego tooan IP istniejącej maszyny Wirtualnej
tooadd statycznego prywatnego adresu IP adres toohello maszyny Wirtualnej utworzonej przy użyciu skryptu hello powyżej runt następujące polecenie:

    azure vm static-ip set DNS01 192.168.1.101

Oczekiwane dane wyjściowe:

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zastrzeżone publicznego adresu IP](virtual-networks-reserved-public-ip.md) adresów.
* Dowiedz się więcej o [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresów.
* Zapoznaj się hello [zastrzeżonego adresu IP interfejsów API REST](https://msdn.microsoft.com/library/azure/dn722420.aspx).

