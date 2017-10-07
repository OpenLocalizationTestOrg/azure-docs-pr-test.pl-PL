---
title: "aaaOverview Oracle sytuacji odzyskiwania po awarii w środowisku platformy Azure | Dokumentacja firmy Microsoft"
description: "Scenariusza odzyskiwania po awarii dla bazy danych Oracle 12c w środowisku platformy Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a>Odzyskiwanie po awarii dla bazy danych programu Oracle Database 12c w środowisku platformy Azure

## <a name="assumptions"></a>Wartości domyślne

- Należy dobrze poznać zasady środowiska platformy Azure i Oracle Data Guard projektu.


## <a name="goals"></a>Cele
- Projektowanie topologii hello i konfiguracji, które spełniają wymagania odzyskiwanie po awarii.

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a>Scenariusz 1: Lokacji głównej i odzyskiwania po awarii lokacji na platformie Azure

Klient ma Oracle bazy danych Ustaw hello lokacji głównej. Lokacja A DR znajduje się w innym regionie. powitania klienta używa Oracle Data Guard Szybkie odzyskiwanie między tymi lokacjami. lokacja główna Hello ma również pomocniczej bazy danych raportowania i innych celów. 

### <a name="topology"></a>Topologia

Poniżej przedstawiono podsumowanie hello Azure Instalatora:

- Dwie witryny (lokacji głównej i lokacji odzyskiwania po awarii)
- Dwie sieci wirtualne
- Dwóch baz danych Oracle Data Guard (podstawowe i stan gotowości)
- Dwóch baz danych Oracle Golden bramy lub Data Guard (tylko w lokacji głównej)
- Dwie usługi aplikacji, podstawowego i jeden w lokacji hello DR
- *Zestawu dostępności* używany dla usługi bazy danych i aplikacji w lokacji głównej hello
- Jeden jumpbox w każdej lokacji, która ogranicza sieci prywatnej toohello dostępu i zezwala na logowanie przez administratora
- Jumpbox, usługa aplikacji, bazy danych i Brama sieci VPN w różnych podsieciach
- Grupa NSG wymuszone w aplikacji i podsieci bazy danych

![Zrzut ekranu przedstawiający stronę topologii hello DR](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a>Scenariusz 2: Lokalne lokacji głównej i lokacji odzyskiwania po awarii na platformie Azure

Klient ma Konfiguracja bazy danych Oracle lokalnymi (lokacji głównej). Lokacja A DR jest na platformie Azure. Oracle Data Guard służy do szybkiego odzyskania między tymi lokacjami. lokacja główna Hello ma również pomocniczej bazy danych raportowania i innych celów. 

Istnieją dwa podejścia do tej instalacji.

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a>Podejście 1: Bezpośrednich połączeń między lokalną i platformą Azure, wymagających otwartych portów TCP w zaporze hello 

Nie zaleca się bezpośredniego połączenia, ponieważ udostępniają toohello porty TCP hello poza world.

#### <a name="topology"></a>Topologia

Poniżej znajduje się podsumowanie hello Azure Instalatora:

- Jeden odzyskiwania po awarii lokacji 
- Jedną sieć wirtualną
- Co baza danych Oracle przy użyciu funkcji Guard danych (aktywny)
- Usługa jedną aplikację w witrynie hello DR
- Jumpbox jeden, co ogranicza sieci prywatnej toohello dostępu i zezwala na logowanie przez administratora
- Jumpbox, usługa aplikacji, bazy danych i Brama sieci VPN w różnych podsieciach
- Grupa NSG wymuszone w aplikacji i podsieci bazy danych
- Tooallow/reguły NSG ruchu przychodzącego dla portu TCP 1521 (lub portu zdefiniowane przez użytkownika)
- Grupa NSG reguły/toorestrict tylko hello adresy adresów IP/sieci wirtualnej hello tooaccess lokalnymi (baza danych lub aplikacji)

![Zrzut ekranu przedstawiający stronę topologii hello DR](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a>Podejście 2: VPN lokacja lokacja
Sieć VPN lokacja lokacja jest lepszym rozwiązaniem. Aby uzyskać więcej informacji na temat konfigurowania sieci VPN, zobacz [tworzenie sieci wirtualnej za pomocą połączenia sieci VPN typu lokacja-lokacja za pomocą interfejsu wiersza polecenia](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).

#### <a name="topology"></a>Topologia

Poniżej znajduje się podsumowanie hello Azure Instalatora:

- Jeden odzyskiwania po awarii lokacji 
- Jedną sieć wirtualną 
- Co baza danych Oracle przy użyciu funkcji Guard danych (aktywny)
- Usługa jedną aplikację w witrynie hello DR
- Jumpbox jeden, co ogranicza sieci prywatnej toohello dostępu i zezwala na logowanie przez administratora
- Jumpbox, usługa aplikacji, bazy danych i Brama sieci VPN są w różnych podsieciach
- Grupa NSG wymuszone w aplikacji i podsieci bazy danych
- Połączenia sieci VPN lokacja lokacja między lokalną i platformą Azure

![Zrzut ekranu przedstawiający stronę topologii hello DR](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a>Dodatkowe materiały

- [Projektowania i implementacji bazy danych programu Oracle na platformie Azure](oracle-design.md)
- [Skonfiguruj Oracle Data Guard](configure-oracle-dataguard.md)
- [Konfigurowanie bramy Golden Oracle](configure-oracle-golden-gate.md)
- [Oracle kopii zapasowych i odzyskiwania](oracle-backup-recovery.md)


## <a name="next-steps"></a>Następne kroki

- [Samouczek: Tworzenie maszyn wirtualnych wysokiej dostępności](../../linux/create-cli-complete.md)
- [Eksploruj przykłady Azure CLI wdrożenia maszyny Wirtualnej](../../linux/cli-samples.md)
