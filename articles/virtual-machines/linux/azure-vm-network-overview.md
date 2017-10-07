---
title: aaaAzure i opis sieci maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: "Przegląd sieci platformy Azure i maszyny Wirtualnej systemu Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: b5420e35-0463-4456-9803-6142db150f2e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: c3de2dc583c62160e10c0e97e96fef49b9eaffbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-network-overview"></a>Omówienie sieci maszyny Wirtualnej systemu Linux i Azure
## <a name="virtual-networks"></a>Sieci wirtualne
Sieć wirtualna platformy Azure (VNet) to reprezentacja sieci w chmurze hello. Jest logiczną izolacją hello subskrypcji tooyour chmury Azure w wersji dedykowanej. Można w pełni kontrolować bloki adresów IP hello, ustawienia DNS, zasady zabezpieczeń i tabele tras w ramach tej sieci. Można również podzielić sieć na podsieci i uruchom maszyny wirtualne Azure IaaS (VM) i/lub usługi w chmurze (wystąpienia roli PaaS). Ponadto można połączyć hello sieci wirtualnej tooyour sieci lokalnej przy użyciu jednej z opcji łączności hello dostępnej na platformie Azure. W zasadzie można rozwinąć tooAzure Twojej sieci, zachowując pełną kontrolę nad blokami adresów IP i hello zaletą przez platformę Azure skalowalność przedsiębiorstwa.

* [Omówienie sieci wirtualnej](../../virtual-network/virtual-networks-overview.md)

toocreate sieć wirtualną przy użyciu hello interfejsu wiersza polecenia Azure, przejdź tutaj toofollow hello krokach związanych z.

* [Jak toocreate sieci wirtualnej przy użyciu hello wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a>Grupy zabezpieczeń sieci
Grupy zabezpieczeń sieci (NSG) zawiera listę reguł listy kontroli dostępu (ACL), które akceptować lub odrzucać ruch sieciowy tooyour wystąpień maszyn wirtualnych w sieci wirtualnej. Grupy NSG można kojarzyć z podsieciami lub poszczególnymi wystąpieniami maszyn wirtualnych w danej podsieci. Gdy grupa NSG jest skojarzona z podsiecią, reguły listy ACL hello zastosować wystąpień maszyn wirtualnych hello tooall w tej podsieci. Ponadto ruch tooan poszczególnych maszyn wirtualnych można ograniczyć jeszcze bardziej przez skojarzenie grupy NSG bezpośrednio toothat maszyny Wirtualnej.

* [Co to jest sieciowa grupa zabezpieczeń?](../../virtual-network/virtual-networks-nsg.md)
* [Jak grupy NSG toocreate w hello wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a>Trasy definiowane przez użytkownika
Po dodaniu maszynach wirtualnych (VM) tooa sieć wirtualną (VNet) na platformie Azure można zauważyć maszyn wirtualnych hello automatycznie są możliwe toocommunicate ze sobą za pośrednictwem sieci hello. Nie trzeba toospecify bramy, nawet jeśli hello maszyn wirtualnych znajdują się w różnych podsieciach. Witaj dotyczy to także komunikacji z toohello maszyn wirtualnych hello publicznego Internetu i sieci lokalnej tooyour nawet gdy połączenie hybrydowe z platformy Azure tooyour własnych centrum danych jest obecny.

* [Co to są trasy zdefiniowane przez użytkownika i przekazywanie adresów IP?](../../virtual-network/virtual-networks-udr-overview.md)
* [Utwórz przez w hello wiersza polecenia platformy Azure](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-tooyour-linux-vm"></a>Kojarzenie tooyour nazwa FQDN maszyny Wirtualnej systemu Linux
Podczas tworzenia maszyny wirtualnej (VM) w portalu Azure hello przy użyciu modelu wdrażania usługi Resource Manager hello, publiczny adres IP zasobów dla maszyny wirtualnej hello jest tworzony automatycznie. Możesz użyć tego adresu IP adres tooremotely dostępu hello maszyny Wirtualnej. Mimo że hello portal nie tworzy pełną nazwę domeny lub nazwę FQDN, domyślnie, możesz dodać kategorię, po utworzeniu hello maszyny Wirtualnej.

* [Utwórz w pełni kwalifikowaną nazwę domeny w hello portalu Azure](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a>Interfejsy sieciowe
Interfejsu sieciowego (NIC) jest hello połączenia między maszyn wirtualnych (VM) i hello bazowy oprogramowania sieci. W tym artykule opisano nowy interfejs sieciowy jest i sposobie ich użycia w modelu wdrażania usługi Azure Resource Manager hello.

* [Interfejsy sieci wirtualnej](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a>Wirtualne karty sieciowe i etykietowanie DNS
Serwer należy toobe trwałe, że ten serwer jest traktowane jako bydła i będzie działo i często wdrożone, można toouse DNS etykietowania na nazwę karty Sieciowej toopersist hello na powitania sieci Wirtualnej.  Z przewodnika po hello umożliwią skonfigurowanie trwale nazwanego kartę Sieciową ze statycznym adresem IP.

* [Utwórz pełną środowiska systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a>Bramy sieci wirtualnej
Brama sieci wirtualnej służy toosend ruchu sieciowego między sieciami wirtualnymi platformy Azure i lokalizacji lokalnej, a także między sieciami wirtualnymi w obrębie platformy Azure (VNet-VNet). Podczas konfigurowania bramy VPN Gateway należy utworzyć i skonfigurować bramę sieci wirtualnej oraz połączenie bramy sieci wirtualnej.

* [VPN Gateway — informacje](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a>Wewnętrzne Równoważenie obciążenia
Usługa Azure Load Balancer to moduł równoważenia obciążenia w warstwie 4 (TCP, UDP). Hello modułu równoważenia obciążenia zapewnia wysoką dostępność, przekazując przychodzący ruch między wystąpienie usługi działa prawidłowo usług w chmurze lub maszyn wirtualnych w zestawie usługi równoważenia obciążenia. Usługa Azure Load Balancer może także prezentować te usługi na wielu portach i/lub wielu adresach IP.

* [Tworzenie wewnętrznego modułu równoważenia obciążenia przy użyciu hello wiersza polecenia platformy Azure](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

