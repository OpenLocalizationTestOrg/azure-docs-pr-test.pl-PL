---
title: "problemy z łącznością aaaTroubleshooting między maszynami wirtualnymi Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooTroubleshoot hello występują problemy z łącznością między maszynami wirtualnymi Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Rozwiązywanie problemów z łącznością między maszynami wirtualnymi Azure

Mogą wystąpić problemy z łącznością między maszynami wirtualnymi Azure. Ten artykuł zawiera toohelp kroki rozwiązywania problemów możesz rozwiązać ten problem. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Objaw

Maszyny Wirtualnej platformy Azure nie może połączyć tooanother maszyny Wirtualnej platformy Azure.

## <a name="troubleshooting-guidance"></a>Wskazówki dotyczące rozwiązywania problemów 

1. [Sprawdź, jeśli karta sieciowa jest błędnie skonfigurowane](#step-1-check-if-nic-is-misconfigured)
2. [Sprawdź, czy ruch sieciowy jest blokowany przez NSG lub przez](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Sprawdź, czy ruch sieciowy jest blokowany przez zaporę maszyny Wirtualnej](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Sprawdź, czy maszyna wirtualna aplikacji lub usługi nasłuchuje na porcie hello](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Sprawdź, czy przyczyną problemu hello jest SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Sprawdź, czy ruch jest blokowany przez listy kontroli dostępu dla hello klasyczne maszyny Wirtualnej](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Sprawdź czy punkt końcowy hello jest tworzone dla hello klasyczne maszyny Wirtualnej](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [Udział sieciowy maszyny Wirtualnej tooa tooconnect](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Łączność między sieciami wirtualnymi](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Kroki rozwiązywania problemów

Wykonaj te kroki tootroubleshoot hello problem. Sprawdź, czy hello problem zostanie rozwiązany po każdym kroku. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Krok 1: Sprawdź, jeśli karta sieciowa jest błędnie skonfigurowane

Postępuj zgodnie z [jak tooreset interfejsu sieciowego dla maszyny Wirtualnej systemu Windows Azure](../virtual-machines/windows/reset-network-interface.md). 

Jeśli wystąpi problem powitania po zmodyfikowaniu hello interfejsu sieciowego (NIC), wykonaj następujące kroki:

**Karta sieciowa Mulit maszyny wirtualne**

1. Dodaj kartę sieciową.
2. Rozwiąż problemy hello w hello zły karty Sieciowej lub usuwanie nieprawidłowych karty sieciowej.  Następnie readd hello karty sieciowej.

Aby uzyskać więcej informacji, zobacz [tooor interfejsów sieciowych Add usunięcia z maszyn wirtualnych](virtual-network-network-interface-vm.md).

**Wirtualna karta sieciowa na jednym** 

- [Wdrożenie maszyny Wirtualnej z systemem Windows](../virtual-machines/windows/redeploy-to-new-node.md)
- [Wdrożenie maszyny Wirtualnej systemu Linux](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Krok 2: Sprawdź, czy ruch sieciowy jest blokowany przez NSG lub przez

Korzystanie z [Sprawdź przepływ IP obserwatora sieciowego](../network-watcher/network-watcher-ip-flow-verify-overview.md) i [rejestrowania przepływu NSG](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify, jeśli istnieje grupa zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, która jest zakłócać przepływ ruchu.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Krok 3: Sprawdź, czy ruch sieciowy jest blokowany przez zaporę maszyny Wirtualnej

Wyłącz hello zapory, a następnie hello wyniku testu. Jeśli hello problem zostanie rozwiązany, sprawdź poprawność ustawień hello w zaporze hello i ponownie włącz.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a>Krok 4: Sprawdź, czy maszyna wirtualna aplikacji lub usługi nasłuchuje na porcie hello

Można użyć jednej z hello następujące metody toocheck, czy aplikacja wirtualna lub usługa nasłuchuje na porcie hello

- Uruchom następujące polecenia toocheck czy hello server nasłuchuje na tym porcie hello.

**Maszyna wirtualna z systemem Windows**

    netstat –ano

**Maszyna wirtualna z systemem Linux**

    netstat -l

- Uruchom hello **Telnet** na powitania port hello tootest tooitself maszyny Wirtualnej. Jeśli hello test zakończy się niepowodzeniem, aplikacja lub usługa nie jest skonfigurowany toolisten na porcie hello.

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a>Krok 5: Sprawdź, czy przyczyną problemu hello jest SNAT

W niektórych scenariuszach hello maszyny Wirtualnej znajduje się za rozwiązania równoważenia obciążenia, które ma zależności zasobów poza platformą Azure. W tych scenariuszach występują sporadyczne problemy z połączeniem, hello przyczyną problemu może być [wyczerpania portu SNAT](../load-balancer/load-balancer-outbound-connections.md). tooresolve hello problem, Utwórz VIP (lub ILPIP klasycznego) dla każdej maszyny Wirtualnej, która jest za usługą równoważenia obciążenia hello i zabezpieczyć za pomocą NSG lub listy ACL. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a>Krok 6: Sprawdź czy ruch jest blokowany przez listy kontroli dostępu dla tekst hello klasyczne maszyny Wirtualnej

Listy ACL zapewnia hello możliwości tooselectively zezwolenia lub odmowy ruchu dla punktu końcowego maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [Zarządzaj hello listy ACL punktu końcowego](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a>Krok 7: Sprawdź czy punkt końcowy hello jest tworzone dla tekst hello klasyczne maszyny Wirtualnej

Wszystkie maszyny wirtualne utworzone na platformie Azure przy użyciu hello klasycznego modelu wdrażania może komunikować się automatycznie kanałem sieci prywatnej innym maszynom wirtualnym w hello się, że takie same w chmurze, usługi lub wirtualnych sieci. Jednak komputery w innych sieciach wirtualnych wymagają punkty końcowe toodirect hello ruchu przychodzącego ruchu tooa maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [jak tooset się punkty końcowe](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a>Krok 8: Udział sieciowy maszyny Wirtualnej tooa tooconnect

W przypadku udziału sieciowego maszyny Wirtualnej tooa tooconnect hello problemu może być spowodowane niedostępny karty sieciowe w hello maszyny Wirtualnej. toodelete hello niedostępny kart sieciowych, zobacz [jak toodelete hello niedostępny kart sieciowych](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>Krok 9: Łączności między sieciami wirtualnymi

Korzystanie z [Sprawdź przepływ IP obserwatora sieciowego](../network-watcher/network-watcher-ip-flow-verify-overview.md) i [rejestrowania przepływu NSG](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify, jeśli istnieje grupa zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, która jest zakłócać przepływ ruchu. Można również sprawdzić poprawności konfiguracji sieci wirtualnej między [tutaj](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.
