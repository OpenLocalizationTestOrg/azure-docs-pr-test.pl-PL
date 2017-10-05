---
title: "Rozwiązywanie problemów z łącznością między maszynami wirtualnymi Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązywać problemy z łącznością między maszynami wirtualnymi Azure."
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
ms.openlocfilehash: fd0f25c07cb3f385d3e8480ce1e33dec1ae0a214
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Rozwiązywanie problemów z łącznością między maszynami wirtualnymi Azure

Mogą wystąpić problemy z łącznością między maszynami wirtualnymi Azure. Ten artykuł zawiera kroki rozwiązywania problemów, aby rozwiązać ten problem. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Objaw

Maszyny Wirtualnej platformy Azure nie może połączyć się innej maszyny Wirtualnej platformy Azure.

## <a name="troubleshooting-guidance"></a>Wskazówki dotyczące rozwiązywania problemów 

1. [Sprawdź, jeśli karta sieciowa jest błędnie skonfigurowane](#step-1-check-if-nic-is-misconfigured)
2. [Sprawdź, czy ruch sieciowy jest blokowany przez NSG lub przez](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Sprawdź, czy ruch sieciowy jest blokowany przez zaporę maszyny Wirtualnej](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Sprawdź, czy maszyna wirtualna aplikacji lub usługi nasłuchuje na porcie](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Sprawdź, czy przyczyną problemu jest SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Sprawdź, czy ruch jest blokowany przez listy kontroli dostępu dla klasycznego maszyny Wirtualnej](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Sprawdź, czy punkt końcowy jest tworzony dla klasycznego maszyny Wirtualnej](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [Nie można nawiązać połączenia z udziału sieciowego maszyny Wirtualnej](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Łączność między sieciami wirtualnymi](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Kroki rozwiązywania problemów

Wykonaj następujące kroki, aby rozwiązać problem. Sprawdź, czy problem został rozwiązany po każdym kroku. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Krok 1: Sprawdź, jeśli karta sieciowa jest błędnie skonfigurowane

Postępuj zgodnie z [sposób resetowania interfejsu sieciowego dla maszyny Wirtualnej systemu Windows Azure](../virtual-machines/windows/reset-network-interface.md). 

Jeśli ten problem występuje po zmodyfikowaniu interfejsu sieciowego (NIC), wykonaj następujące kroki:

**Karta sieciowa Mulit maszyny wirtualne**

1. Dodaj kartę sieciową.
2. Rozwiąż problemy w zły karty Sieciowej lub usunąć zły karty sieciowej.  Następnie readd karty sieciowej.

Aby uzyskać więcej informacji, zobacz [interfejsów sieciowych, aby dodać lub usunąć z maszyny wirtualnej](virtual-network-network-interface-vm.md).

**Wirtualna karta sieciowa na jednym** 

- [Wdrożenie maszyny Wirtualnej z systemem Windows](../virtual-machines/windows/redeploy-to-new-node.md)
- [Wdrożenie maszyny Wirtualnej systemu Linux](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Krok 2: Sprawdź, czy ruch sieciowy jest blokowany przez NSG lub przez

Korzystanie z [Sprawdź przepływ IP obserwatora sieciowego](../network-watcher/network-watcher-ip-flow-verify-overview.md) i [rejestrowania przepływu NSG](../network-watcher/network-watcher-nsg-flow-logging-overview.md) do ustalenia, czy istnieje grupa zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, która jest zakłócać przepływ ruchu.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Krok 3: Sprawdź, czy ruch sieciowy jest blokowany przez zaporę maszyny Wirtualnej

Wyłącz zaporę, a następnie sprawdź wynik. Jeśli ten problem zostanie rozwiązany, sprawdź poprawność ustawień zapory, a następnie ponownie włącz.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-the-port"></a>Krok 4: Sprawdź, czy maszyna wirtualna aplikacji lub usługi nasłuchuje na porcie

Można użyć jednej z następujących metod do sprawdzenia, czy aplikacja wirtualna lub usługa nasłuchuje na porcie

- Uruchom następujące polecenia, aby sprawdzić, czy serwer nasłuchuje na tym porcie.

**Maszyna wirtualna z systemem Windows**

    netstat –ano

**Maszyna wirtualna z systemem Linux**

    netstat -l

- Uruchom **Telnet** polecenia na maszynie Wirtualnej do samej siebie, aby przetestować portu. Jeśli test ma wynik negatywny, aplikacja lub usługa nie skonfigurowano nasłuchiwanie na porcie.

### <a name="step-5-check-whether-the-problem-is-caused-by-snat"></a>Krok 5: Sprawdź, czy przyczyną problemu jest SNAT

W niektórych scenariuszach maszyna wirtualna znajduje się za rozwiązania równoważenia obciążenia, które ma zależności zasobów poza platformą Azure. W tych scenariuszach występują sporadyczne problemy z połączeniem, problem może być spowodowane [wyczerpania portu SNAT](../load-balancer/load-balancer-outbound-connections.md). Aby rozwiązać ten problem, Utwórz dla każdej maszyny Wirtualnej związanej z modułem równoważenia obciążenia i zabezpieczyć za pomocą NSG lub listy ACL adresu VIP (lub ILPIP klasycznego). 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm"></a>Krok 6: Sprawdź, czy ruch jest blokowany przez listy kontroli dostępu dla klasycznego maszyny Wirtualnej

Listy ACL zapewnia możliwość selektywnego akceptowanie lub odrzucanie ruchu dla punktu końcowego maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [Zarządzanie listy ACL punktu końcowego](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-the-endpoint-is-created-for-the-classic-vm"></a>Krok 7: Sprawdź, czy punkt końcowy jest tworzony dla klasycznego maszyny Wirtualnej

Wszystkie maszyny wirtualne utworzone na platformie Azure przy użyciu klasycznego modelu wdrażania można automatycznie komunikują się za pośrednictwem kanału między maszynami wirtualnymi w tej samej usługi w chmurze lub sieci wirtualnej sieci prywatnej. Jednak komputery w innych sieciach wirtualnych wymagają punktów końcowych, aby skierować ruch sieciowy przychodzący do maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [sposobu konfigurowania punktów końcowych](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-to-connect-to-a-vm-network-share"></a>Krok 8: Nie można nawiązać połączenia z udziału sieciowego maszyny Wirtualnej

Jeśli nie można nawiązać połączenia z udziału sieciowego maszyny Wirtualnej, problem może wpływać niedostępny kart sieciowych w maszynie Wirtualnej. Aby usunąć niedostępny kart sieciowych, zobacz [sposób usuwania niedostępny kart sieciowych](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>Krok 9: Łączności między sieciami wirtualnymi

Korzystanie z [Sprawdź przepływ IP obserwatora sieciowego](../network-watcher/network-watcher-ip-flow-verify-overview.md) i [rejestrowania przepływu NSG](../network-watcher/network-watcher-nsg-flow-logging-overview.md) do ustalenia, czy istnieje grupa zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, która jest zakłócać przepływ ruchu. Można również sprawdzić poprawności konfiguracji sieci wirtualnej między [tutaj](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) uzyskać szybkie rozwiązanie problemu.