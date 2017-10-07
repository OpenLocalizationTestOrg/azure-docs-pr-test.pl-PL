---
title: aaaConfiguring DHCPv6 dla maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: Jak tooconfigure DHCPv6 dla maszyn wirtualnych systemu Linux.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "Protokół IPv6, usługi równoważenia obciążenia azure, podwójnego stosu, publiczny adres ip, natywnego protokołu ipv6, mobile, iot"
ms.assetid: b32719b6-00e8-4cd0-ba7f-e60e8146084b
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: abd5a98c3496b189946f59bab1d9c20dcd0aa2c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a>Konfigurowanie protokołu DHCPv6 dla maszyn wirtualnych systemu Linux

Niektóre obrazy maszyny wirtualnej systemu Linux hello w hello Azure Marketplace nie mają DHCPv6 konfiguracja domyślna. toosupport IPv6 i DHCPv6 muszą być skonfigurowane w w dystrybucji systemu operacyjnego Linux hello, którego używasz. Różne dystrybucje systemu Linux mają różne sposoby konfigurowania protokołu DHCPv6, ponieważ korzystają z różnych pakietów.

> [!NOTE]
> Ostatnie SUSE Linux i CoreOS obrazów w portalu Azure Marketplace hello zostały wstępnie skonfigurowany z użyciem protokołu DHCPv6. Korzystając z tych obrazów są wymagane nie dodatkowe zmiany.

W tym dokumencie opisano sposób tooenable DHCPv6 tak, aby maszyny wirtualnej systemu Linux uzyskuje adres IPv6.

> [!WARNING]
> Nieprawidłowo edycję plików konfiguracyjnych sieci może spowodować możesz toolose sieci dostępu tooyour maszyny Wirtualnej. Zaleca się przetestowanie zmiany konfiguracji w systemach nieprodukcyjnych. Witaj instrukcje w tym artykule zostały przetestowane na powitania najnowsze wersje hello Linux obrazów w hello Azure Marketplace. Zapoznaj się dokumentacją hello konkretnej wersji systemu Linux bardziej szczegółowe informacje.

## <a name="ubuntu"></a>Ubuntu

1. Edytuj plik hello `/etc/dhcp/dhclient6.conf` i Dodaj powitania po wierszu:

        timeout 10;

2. Edytuj hello konfigurację sieci dla interfejsu eth0 hello z hello następującej konfiguracji:

   * Na **Ubuntu 12.04 i 14.04**, Edytuj plik hello`/etc/network/interfaces.d/eth0.cfg`
   * Na **Ubuntu 16.04**, Edytuj plik hello`/etc/network/interfaces.d/50-cloud-init.cfg`

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Odnów adres IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a>Debian

1. Edytuj plik hello `/etc/dhcp/dhclient6.conf` i Dodaj powitania po wierszu:

        timeout 10;

2. Edytuj plik hello `/etc/network/interfaces` i Dodaj hello następującej konfiguracji:

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Odnów adres IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a>RHEL / CentOS / Oracle Linux

1. Edytuj plik hello `/etc/sysconfig/network` i Dodaj hello następującego parametru:

        NETWORKING_IPV6=yes

2. Edytuj plik hello `/etc/sysconfig/network-scripts/ifcfg-eth0` i Dodaj hello następujące dwa parametry:

        IPV6INIT=yes
        DHCPV6C=yes

3. Odnów adres IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a>SLES 11 & openSUSE 13

Ostatnie SLES i openSUSE obrazów na platformie Azure zostały wstępnie skonfigurowany z użyciem protokołu DHCPv6. Korzystając z tych obrazów są wymagane nie dodatkowe zmiany. Jeśli masz maszyny Wirtualnej na podstawie obrazu SUSE starszych lub niestandardowego, należy użyć hello następujące kroki:

1. Zainstaluj hello `dhcp-client` pakietu, w razie potrzeby:

    ```bash
    sudo zypper install dhcp-client
    ```

2. Edytuj plik hello `/etc/sysconfig/network/ifcfg-eth0` i Dodaj hello następującego parametru:

        DHCLIENT6_MODE='managed'

3. Odnów adres hello IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a>SLES 12 i openSUSE przestępnego

Ostatnie SLES i openSUSE obrazów na platformie Azure zostały wstępnie skonfigurowany z użyciem protokołu DHCPv6. Korzystając z tych obrazów są wymagane nie dodatkowe zmiany. Jeśli masz maszyny Wirtualnej na podstawie obrazu SUSE starszych lub niestandardowego, należy użyć hello następujące kroki:

1. Edytuj plik hello `/etc/sysconfig/network/ifcfg-eth0` i Zastąp ten parametr

        #BOOTPROTO='dhcp4'

    z hello następujące wartości:

        BOOTPROTO='dhcp'

2. Dodaj hello zbyt następującego parametru`/etc/sysconfig/network/ifcfg-eth0`:

        DHCLIENT6_MODE='managed'

3. Odnów adres hello IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a>CoreOS

Ostatnie obrazy CoreOS na platformie Azure zostały wstępnie skonfigurowany z użyciem protokołu DHCPv6. Korzystając z tych obrazów są wymagane nie dodatkowe zmiany. Jeśli masz maszyny Wirtualnej na podstawie obrazu CoreOS starszych lub niestandardowego, należy użyć hello następujące kroki:

1. Edytuj plik hello`/etc/systemd/network/10_dhcp.network`

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. Odnów adres hello IPv6:

    ```bash
    sudo systemctl restart systemd-networkd
    ```
