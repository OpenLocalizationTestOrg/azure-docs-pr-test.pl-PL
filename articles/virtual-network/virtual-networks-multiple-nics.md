---
title: "Maszyna wirtualna (klasyczna) z wieloma kartami sieciowymi przy użyciu programu PowerShell aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i konfigurowanie maszyn wirtualnych z wieloma kartami sieciowymi przy użyciu programu PowerShell."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a>Tworzenie maszyny Wirtualnej (klasyczne) z wieloma kartami sieciowymi
Można tworzyć maszyn wirtualnych (VM) na platformie Azure i dołączyć wiele sieci tooeach interfejsów (NIC) z maszyn wirtualnych. Wiele kart sieciowych są wymagane w przypadku wielu sieci wirtualnych urządzeń, takich jak dostarczania aplikacji i rozwiązań Optymalizacja sieci WAN. Wiele kart sieciowych zapewniają również izolacji ruchu między kart sieciowych.

![Obsługa wielu kart interfejsu Sieciowego dla maszyny Wirtualnej](./media/virtual-networks-multiple-nics/IC757773.png)

rysunek pokazuje Hello maszyny Wirtualnej z trzema kartami sieciowymi, każdy jest połączony tooa innej podsieci.

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać Menedżera zasobów.

* VIP połączonych z Internetem (wdrożenia klasyczne) jest obsługiwany tylko na powitania "domyślne" karty sieciowej. Istnieje tylko jeden adres IP toohello VIP o hello domyślną kartę sieciową.
* W tym czasie wystąpienia poziomu publicznego adresu IP (LPIP) adresy (wdrożenia klasyczne) nie są obsługiwane dla wielu maszyn wirtualnych kart Sieciowych.
* Witaj kolejność kart sieciowych hello z wewnątrz hello maszyny Wirtualnej będzie losowe i można również zmienić między aktualizacjami infrastruktury platformy Azure. Jednak hello adresów IP i hello odpowiedni adres ethernet MAC pozostanie adresy hello takie same. Załóżmy na przykład **Eth1** ma adres IP 10.1.0.100 i adres MAC 00-0D-3A-B0-39-0D; po aktualizacji infrastruktury platformy Azure i uruchom ponownie komputer, którego można można zmienić za**Eth2**, ale hello adresów IP i MAC parowanie zostanie pozostają takie same hello. Jeśli ponowne uruchomienie jest inicjowane przez klienta, pozostaną hello kolejność kart hello takie same.
* Witaj adresów dla każdej karty Sieciowej na każdej maszynie Wirtualnej musi znajdować się w podsieci, wiele kart sieciowych w ramach jednej maszyny Wirtualnej każdego można przypisać adresy znajdujące się w hello tej samej podsieci.
* Hello rozmiar maszyny Wirtualnej określa hello liczbę kart Sieciowych, który można utworzyć maszyny wirtualnej. Odwołanie hello [systemu Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toodetermine artykuły rozmiary maszyny Wirtualnej, jak wiele kart Sieciowych każdego rozmiaru maszyny Wirtualnej obsługuje. 

## <a name="network-security-groups-nsgs"></a>Grupy zabezpieczeń sieci (NSG)
W ramach wdrożenia usługi Resource Manager dowolnej karty interfejsu Sieciowego na maszynie Wirtualnej może być skojarzony z sieciowej grupy zabezpieczeń (NSG), w tym wszystkie karty sieciowe na maszynie Wirtualnej, który ma wiele kart sieciowych włączone. Jeśli karta sieciowa zostanie przypisany adres znajdujący się w podsieci, w którym jest skojarzona z grupy NSG podsieci hello, następnie hello reguły w NSG podsieci hello stosuje się również toothat karty sieciowej. Dodawanie podsieci tooassociating z grup NSG można także skojarzyć karty Sieciowej z grupy NSG.

Jeśli podsieć jest skojarzony z grupy NSG, a karta sieciowa w tej podsieci indywidualnie powiązanego z grupy NSG, hello skojarzone reguły NSG są stosowane w **przepływ kolejności** zgodnie z toohello kierunek ruchu hello przekazywany do lub z Witaj karty Sieciowej:

* **Ruch przychodzący** których obiektem docelowym jest hello karty Sieciowej w pytanie najpierw przechodzi przez hello podsieci, wyzwolenie reguły NSG podsieci hello, przed przekazaniem do hello karty Sieciowej, a następnie wyzwolenie reguły NSG hello karty Sieciowej.
* **Ruch wychodzący** źródłem jest hello karty Sieciowej w przepływa pierwszy na wyjściu z hello karty Sieciowej, wyzwolenie reguły NSG hello karty Sieciowej, przed przechodzącej przez hello podsieci, a następnie wyzwolenie reguły NSG hello podsieci.

Dowiedz się więcej o [grup zabezpieczeń sieci](virtual-networks-nsg.md) i jak są one stosowane na podstawie toosubnets skojarzenia, maszyn wirtualnych i karty sieciowe.

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a>Jak tooConfigure wielu kart interfejsu Sieciowego maszyny Wirtualnej w ramach wdrożenia klasycznego
Poniższe instrukcje Hello umożliwia tworzenie wielu kart Sieciowych maszyny Wirtualnej zawierający 3 kart sieciowych: domyślna karta sieciowa a dwie dodatkowe karty sieciowe. kroki konfiguracji Hello spowoduje utworzenie maszyny Wirtualnej, który zostanie skonfigurowany zgodnie z poniższym fragment pliku konfiguracji usługi toohello:

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


Należy hello następujące wymagania wstępne, przed podjęciem próby poleceń programu PowerShell hello toorun w przykładzie hello.

* Subskrypcja platformy Azure.
* Skonfigurowanej sieci wirtualnej. Zobacz [omówienie sieci wirtualnych](virtual-networks-overview.md) uzyskać więcej informacji o sieci wirtualnych.
* najnowszą wersję programu Azure PowerShell Hello pobrane i zainstalowane. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

toocreate Maszynę wirtualną z wieloma kartami sieciowymi, pełną hello, wykonaj następujące kroki, wprowadzając każde polecenie w ramach jednej sesji programu PowerShell:

1. Wybierz obraz maszyny Wirtualnej z galerii obrazu maszyny Wirtualnej platformy Azure. Należy pamiętać, że obrazy często zmieniana i są dostępne w poszczególnych regionach. Witaj obrazu określonego w poniższym przykładzie hello może zmienić lub może nie być w danym regionie, dlatego należy toospecify hello obrazu należy.

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. Tworzenie konfiguracji maszyny Wirtualnej.

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. Utwórz identyfikator logowania administratora domyślnego hello.

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. Dodawanie dodatkowych konfiguracji maszyny Wirtualnej toohello kart sieciowych.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. Określ hello podsieć lub adres IP dla hello domyślną kartę sieciową.

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. Utwórz hello maszyny Wirtualnej w sieci wirtualnej.

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > Witaj sieci wirtualnej, określone w tym miejscu musi już istnieć (jak wspomniano w hello wymagania wstępne). w poniższym przykładzie Hello określa sieć wirtualną o nazwie **MultiNIC-VNet**.
    >

## <a name="limitations"></a>Ograniczenia
Hello następujące ograniczenia mają zastosowanie w przypadku korzystania z wielu kart sieciowych:

* Maszyny wirtualne z wieloma kartami sieciowymi muszą być tworzone w sieci wirtualnej platformy Azure (sieci wirtualne). Nie można skonfigurować sieci wirtualnej nie maszyn wirtualnych z wieloma kartami sieciowymi.
* Wszystkie maszyny wirtualne w dostępności ustawiony toouse potrzeby wiele kart sieciowych lub jednej karty sieciowej. Nie może być wiele maszyn wirtualnych kart Sieciowych i jednej karty Sieciowej maszyn wirtualnych w zestawie dostępności. Te same zasady mają zastosowanie dla maszyn wirtualnych w usłudze w chmurze. Dla wielu kart interfejsu Sieciowego maszyn wirtualnych, nie są one wymagane toohave hello samą liczbę kart sieciowych, jak długo każdy z nich ma co najmniej dwóch.
* Nie można skonfigurować maszynę Wirtualną z jednej karty Sieciowej z wielu kart sieciowych (i na odwrót) po wdrożeniu, bez usunięcia i ponownego utworzenia go.

## <a name="secondary-nics-access-tooother-subnets"></a>Dodatkowej podsieci tooother dostęp do kart sieciowych
Domyślnie dodatkowej karty sieciowe nie zostanie skonfigurowany dla bramy domyślnej powodu toowhich hello ruchu na powitania dodatkowej karty sieciowe będą ograniczone toobe w hello tej samej podsieci. Jeśli użytkownicy hello tooenable dodatkowej tootalk kart sieciowych spoza własnej podsieci, muszą tooadd wpis w hello tabeli tooconfigure hello bramy routingu jako opisanych poniżej.

> [!NOTE]
> Maszyny wirtualne utworzone przed lipca 2015 może mieć brama domyślna jest skonfigurowana dla wszystkich kart sieciowych. Hello brama domyślna dla dodatkowej kart sieciowych nie zostaną usunięte, dopóki te maszyny wirtualne są ponownie uruchamiane. W systemach operacyjnych, korzystających z hello słabe routingu modelu hosta, takich jak Linux Jeśli hello ruchu przychodzące i wychodzące używane różne karty sieciowe mogą być dzielone łączności z Internetem.
> 

### <a name="configure-windows-vms"></a>Konfigurowanie maszyn wirtualnych systemu Windows
Załóżmy, że ma maszyny Wirtualnej systemu Windows z dwiema kartami sieciowymi w następujący sposób:

* Podstawowy adres IP karty Sieciowej: 192.168.1.4
* Pomocniczego adresu IP karty Sieciowej: 192.168.2.5

Witaj tabelę tras IPv4 dla tej maszyny Wirtualnej będzie wyglądać następująco:

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

Należy zauważyć, że hello trasa domyślna (0.0.0.0) jest tylko dostępne toohello podstawowej karty sieciowej. Nie będą mogli tooaccess zasobów spoza hello podsieć hello dodatkowej karty Sieciowej, jak pokazano poniżej:

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

tooadd trasy domyślne na hello dodatkowej karty Sieciowej, wykonaj poniższe kroki hello:

1. W wierszu polecenia Uruchom polecenie hello poniżej numer indeksu hello tooidentify hello dodatkowej karty Sieciowej:
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. Zwróć uwagę, hello drugi wpis w tabeli hello z indeksem 27 (w tym przykładzie).
3. W wierszu polecenia hello Uruchom hello **dodać trasy** polecenia, jak pokazano poniżej. W tym przykładzie są określanie 192.168.2.1 jako brama domyślna hello hello dodatkowej karty Sieciowej:
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. łączność tootest toohello wiersza polecenia i spróbuj tooping z innej podsieci hello dodatkowej karty Sieciowej jako pokazano int eh przykładzie poniżej:
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. Można również sprawdzić, że Twoje hello toocheck tabeli tras nowo dodany trasy, jak pokazano poniżej:
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a>Konfigurowanie maszyn wirtualnych systemu Linux
Dla maszyn wirtualnych systemu Linux, ponieważ hello domyślne zachowanie używa słabe hosta routingu, zaleca się tym hello dodatkowej karty sieciowe są ograniczone tootraffic przepływów tylko w obrębie hello tej samej podsieci. Jednak w przypadku niektórych scenariuszy żądanie łączność poza hello podsieci, użytkowników, należy włączyć tooensure routingu opartego na zasadach, które hello wejściowych i używa ruch wychodzący hello tej samej karty sieciowej.

## <a name="next-steps"></a>Następne kroki
* Wdrażanie [MultiNIC maszyn wirtualnych, w przypadku aplikacji warstwy 2 w ramach wdrożenia usługi Resource Manager](virtual-network-deploy-multinic-arm-template.md).
* Wdrażanie [MultiNIC maszyn wirtualnych, w przypadku aplikacji warstwy 2 w ramach wdrożenia klasycznego](virtual-network-deploy-multinic-classic-ps.md).

