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
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="31250-104">Konfigurowanie protokołu DHCPv6 dla maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="31250-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="31250-105">Niektóre obrazy maszyny wirtualnej systemu Linux hello w hello Azure Marketplace nie mają DHCPv6 konfiguracja domyślna.</span><span class="sxs-lookup"><span data-stu-id="31250-105">Some of hello Linux virtual machine images in hello Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="31250-106">toosupport IPv6 i DHCPv6 muszą być skonfigurowane w w dystrybucji systemu operacyjnego Linux hello, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="31250-106">toosupport IPv6, DHCPv6 must be configured in within hello Linux OS distribution that you are using.</span></span> <span data-ttu-id="31250-107">Różne dystrybucje systemu Linux mają różne sposoby konfigurowania protokołu DHCPv6, ponieważ korzystają z różnych pakietów.</span><span class="sxs-lookup"><span data-stu-id="31250-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="31250-108">Ostatnie SUSE Linux i CoreOS obrazów w portalu Azure Marketplace hello zostały wstępnie skonfigurowany z użyciem protokołu DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="31250-108">Recent SUSE Linux and CoreOS images in hello Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="31250-109">Korzystając z tych obrazów są wymagane nie dodatkowe zmiany.</span><span class="sxs-lookup"><span data-stu-id="31250-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="31250-110">W tym dokumencie opisano sposób tooenable DHCPv6 tak, aby maszyny wirtualnej systemu Linux uzyskuje adres IPv6.</span><span class="sxs-lookup"><span data-stu-id="31250-110">This document describes how tooenable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="31250-111">Nieprawidłowo edycję plików konfiguracyjnych sieci może spowodować możesz toolose sieci dostępu tooyour maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="31250-111">Improperly editing network configuration files can cause you toolose network access tooyour VM.</span></span> <span data-ttu-id="31250-112">Zaleca się przetestowanie zmiany konfiguracji w systemach nieprodukcyjnych.</span><span class="sxs-lookup"><span data-stu-id="31250-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="31250-113">Witaj instrukcje w tym artykule zostały przetestowane na powitania najnowsze wersje hello Linux obrazów w hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="31250-113">hello instructions in this article have been tested on hello latest versions of hello Linux images in hello Azure Marketplace.</span></span> <span data-ttu-id="31250-114">Zapoznaj się dokumentacją hello konkretnej wersji systemu Linux bardziej szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="31250-114">Consult hello documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="31250-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="31250-115">Ubuntu</span></span>

1. <span data-ttu-id="31250-116">Edytuj plik hello `/etc/dhcp/dhclient6.conf` i Dodaj powitania po wierszu:</span><span class="sxs-lookup"><span data-stu-id="31250-116">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="31250-117">Edytuj hello konfigurację sieci dla interfejsu eth0 hello z hello następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="31250-117">Edit hello network configuration for hello eth0 interface with hello following configuration:</span></span>

   * <span data-ttu-id="31250-118">Na **Ubuntu 12.04 i 14.04**, Edytuj plik hello`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="31250-118">On **Ubuntu 12.04 and 14.04**, edit hello file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="31250-119">Na **Ubuntu 16.04**, Edytuj plik hello`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="31250-119">On **Ubuntu 16.04**, edit hello file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="31250-120">Odnów adres IPv6:</span><span class="sxs-lookup"><span data-stu-id="31250-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="31250-121">Debian</span><span class="sxs-lookup"><span data-stu-id="31250-121">Debian</span></span>

1. <span data-ttu-id="31250-122">Edytuj plik hello `/etc/dhcp/dhclient6.conf` i Dodaj powitania po wierszu:</span><span class="sxs-lookup"><span data-stu-id="31250-122">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="31250-123">Edytuj plik hello `/etc/network/interfaces` i Dodaj hello następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="31250-123">Edit hello file `/etc/network/interfaces` and add hello following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="31250-124">Odnów adres IPv6:</span><span class="sxs-lookup"><span data-stu-id="31250-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="31250-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="31250-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="31250-126">Edytuj plik hello `/etc/sysconfig/network` i Dodaj hello następującego parametru:</span><span class="sxs-lookup"><span data-stu-id="31250-126">Edit hello file `/etc/sysconfig/network` and add hello following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="31250-127">Edytuj plik hello `/etc/sysconfig/network-scripts/ifcfg-eth0` i Dodaj hello następujące dwa parametry:</span><span class="sxs-lookup"><span data-stu-id="31250-127">Edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="31250-128">Odnów adres IPv6:</span><span class="sxs-lookup"><span data-stu-id="31250-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="31250-129">SLES 11 & openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="31250-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="31250-130">Ostatnie SLES i openSUSE obrazów na platformie Azure zostały wstępnie skonfigurowany z użyciem protokołu DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="31250-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="31250-131">Korzystając z tych obrazów są wymagane nie dodatkowe zmiany.</span><span class="sxs-lookup"><span data-stu-id="31250-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="31250-132">Jeśli masz maszyny Wirtualnej na podstawie obrazu SUSE starszych lub niestandardowego, należy użyć hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="31250-132">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="31250-133">Zainstaluj hello `dhcp-client` pakietu, w razie potrzeby:</span><span class="sxs-lookup"><span data-stu-id="31250-133">Install hello `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="31250-134">Edytuj plik hello `/etc/sysconfig/network/ifcfg-eth0` i Dodaj hello następującego parametru:</span><span class="sxs-lookup"><span data-stu-id="31250-134">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and add hello following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="31250-135">Odnów adres hello IPv6:</span><span class="sxs-lookup"><span data-stu-id="31250-135">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="31250-136">SLES 12 i openSUSE przestępnego</span><span class="sxs-lookup"><span data-stu-id="31250-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="31250-137">Ostatnie SLES i openSUSE obrazów na platformie Azure zostały wstępnie skonfigurowany z użyciem protokołu DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="31250-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="31250-138">Korzystając z tych obrazów są wymagane nie dodatkowe zmiany.</span><span class="sxs-lookup"><span data-stu-id="31250-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="31250-139">Jeśli masz maszyny Wirtualnej na podstawie obrazu SUSE starszych lub niestandardowego, należy użyć hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="31250-139">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="31250-140">Edytuj plik hello `/etc/sysconfig/network/ifcfg-eth0` i Zastąp ten parametr</span><span class="sxs-lookup"><span data-stu-id="31250-140">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="31250-141">z hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="31250-141">with hello following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="31250-142">Dodaj hello zbyt następującego parametru`/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="31250-142">Add hello following parameter too`/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="31250-143">Odnów adres hello IPv6:</span><span class="sxs-lookup"><span data-stu-id="31250-143">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="31250-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="31250-144">CoreOS</span></span>

<span data-ttu-id="31250-145">Ostatnie obrazy CoreOS na platformie Azure zostały wstępnie skonfigurowany z użyciem protokołu DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="31250-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="31250-146">Korzystając z tych obrazów są wymagane nie dodatkowe zmiany.</span><span class="sxs-lookup"><span data-stu-id="31250-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="31250-147">Jeśli masz maszyny Wirtualnej na podstawie obrazu CoreOS starszych lub niestandardowego, należy użyć hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="31250-147">If you have a VM based on an older or custom CoreOS image, use hello following steps:</span></span>

1. <span data-ttu-id="31250-148">Edytuj plik hello`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="31250-148">Edit hello file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="31250-149">Odnów adres hello IPv6:</span><span class="sxs-lookup"><span data-stu-id="31250-149">Renew hello IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
