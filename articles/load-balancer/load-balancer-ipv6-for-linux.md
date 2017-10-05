---
title: "Konfigurowanie protokołu DHCPv6 dla maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft"
description: "Jak skonfigurować DHCPv6 dla maszyn wirtualnych systemu Linux."
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
ms.openlocfilehash: 5c591e7f1838c86ca74caea9dd3a5e8f874fd8a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="1906d-104">Konfigurowanie protokołu DHCPv6 dla maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="1906d-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="1906d-105">Niektóre obrazy maszyny wirtualnej systemu Linux w portalu Azure Marketplace nie mają domyślnie skonfigurowany tak, protokołu DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="1906d-105">Some of the Linux virtual machine images in the Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="1906d-106">Aby obsługiwać protokół IPv6, DHCPv6 muszą być skonfigurowane w w dystrybucji systemu operacyjnego Linux, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="1906d-106">To support IPv6, DHCPv6 must be configured in within the Linux OS distribution that you are using.</span></span> <span data-ttu-id="1906d-107">Różne dystrybucje systemu Linux mają różne sposoby konfigurowania protokołu DHCPv6, ponieważ korzystają z różnych pakietów.</span><span class="sxs-lookup"><span data-stu-id="1906d-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="1906d-108">Ostatnie SUSE Linux i CoreOS obrazów w portalu Azure Marketplace zostały wstępnie skonfigurowany z użyciem protokołu DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="1906d-108">Recent SUSE Linux and CoreOS images in the Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="1906d-109">Korzystając z tych obrazów są wymagane nie dodatkowe zmiany.</span><span class="sxs-lookup"><span data-stu-id="1906d-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="1906d-110">Ten dokument zawiera opis sposobu zapewniają DHCPv6, dzięki czemu maszyny wirtualnej systemu Linux uzyskuje adres IPv6.</span><span class="sxs-lookup"><span data-stu-id="1906d-110">This document describes how to enable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="1906d-111">Nieprawidłowo edycję plików konfiguracyjnych sieci może spowodować utratę dostępu do sieci do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1906d-111">Improperly editing network configuration files can cause you to lose network access to your VM.</span></span> <span data-ttu-id="1906d-112">Zaleca się przetestowanie zmiany konfiguracji w systemach nieprodukcyjnych.</span><span class="sxs-lookup"><span data-stu-id="1906d-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="1906d-113">Instrukcje w tym artykule zostały przetestowane na najnowsze wersje obrazów systemu Linux w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1906d-113">The instructions in this article have been tested on the latest versions of the Linux images in the Azure Marketplace.</span></span> <span data-ttu-id="1906d-114">Dokumentacja konkretnej wersji systemu Linux bardziej szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="1906d-114">Consult the documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="1906d-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1906d-115">Ubuntu</span></span>

1. <span data-ttu-id="1906d-116">Edytuj plik `/etc/dhcp/dhclient6.conf` i Dodaj następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="1906d-116">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="1906d-117">Zmień konfigurację sieci dla interfejsu eth0 przy użyciu następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="1906d-117">Edit the network configuration for the eth0 interface with the following configuration:</span></span>

   * <span data-ttu-id="1906d-118">Na **Ubuntu 12.04 i 14.04**, przeprowadź edycję pliku`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="1906d-118">On **Ubuntu 12.04 and 14.04**, edit the file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="1906d-119">Na **Ubuntu 16.04**, przeprowadź edycję pliku`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="1906d-119">On **Ubuntu 16.04**, edit the file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="1906d-120">Odnów adres IPv6:</span><span class="sxs-lookup"><span data-stu-id="1906d-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="1906d-121">Debian</span><span class="sxs-lookup"><span data-stu-id="1906d-121">Debian</span></span>

1. <span data-ttu-id="1906d-122">Edytuj plik `/etc/dhcp/dhclient6.conf` i Dodaj następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="1906d-122">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="1906d-123">Edytuj plik `/etc/network/interfaces` i dodaj następującą konfigurację:</span><span class="sxs-lookup"><span data-stu-id="1906d-123">Edit the file `/etc/network/interfaces` and add the following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="1906d-124">Odnów adres IPv6:</span><span class="sxs-lookup"><span data-stu-id="1906d-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="1906d-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="1906d-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="1906d-126">Edytuj plik `/etc/sysconfig/network` i Dodaj następujący parametr:</span><span class="sxs-lookup"><span data-stu-id="1906d-126">Edit the file `/etc/sysconfig/network` and add the following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="1906d-127">Edytuj plik `/etc/sysconfig/network-scripts/ifcfg-eth0` i dodaj następujące dwa parametry:</span><span class="sxs-lookup"><span data-stu-id="1906d-127">Edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="1906d-128">Odnów adres IPv6:</span><span class="sxs-lookup"><span data-stu-id="1906d-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="1906d-129">SLES 11 & openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="1906d-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="1906d-130">Ostatnie SLES i openSUSE obrazów na platformie Azure zostały wstępnie skonfigurowany z użyciem protokołu DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="1906d-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="1906d-131">Korzystając z tych obrazów są wymagane nie dodatkowe zmiany.</span><span class="sxs-lookup"><span data-stu-id="1906d-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="1906d-132">Jeśli masz maszyny Wirtualnej na podstawie obrazu SUSE starszych lub niestandardowego, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1906d-132">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="1906d-133">Zainstaluj `dhcp-client` pakietu, w razie potrzeby:</span><span class="sxs-lookup"><span data-stu-id="1906d-133">Install the `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="1906d-134">Edytuj plik `/etc/sysconfig/network/ifcfg-eth0` i Dodaj następujący parametr:</span><span class="sxs-lookup"><span data-stu-id="1906d-134">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and add the following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="1906d-135">Odnów adres IPv6:</span><span class="sxs-lookup"><span data-stu-id="1906d-135">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="1906d-136">SLES 12 i openSUSE przestępnego</span><span class="sxs-lookup"><span data-stu-id="1906d-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="1906d-137">Ostatnie SLES i openSUSE obrazów na platformie Azure zostały wstępnie skonfigurowany z użyciem protokołu DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="1906d-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="1906d-138">Korzystając z tych obrazów są wymagane nie dodatkowe zmiany.</span><span class="sxs-lookup"><span data-stu-id="1906d-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="1906d-139">Jeśli masz maszyny Wirtualnej na podstawie obrazu SUSE starszych lub niestandardowego, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1906d-139">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="1906d-140">Edytuj plik `/etc/sysconfig/network/ifcfg-eth0` i Zastąp ten parametr</span><span class="sxs-lookup"><span data-stu-id="1906d-140">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="1906d-141">przy użyciu następującej wartości:</span><span class="sxs-lookup"><span data-stu-id="1906d-141">with the following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="1906d-142">Dodaj następujący parametr do `/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="1906d-142">Add the following parameter to `/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="1906d-143">Odnów adres IPv6:</span><span class="sxs-lookup"><span data-stu-id="1906d-143">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="1906d-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="1906d-144">CoreOS</span></span>

<span data-ttu-id="1906d-145">Ostatnie obrazy CoreOS na platformie Azure zostały wstępnie skonfigurowany z użyciem protokołu DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="1906d-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="1906d-146">Korzystając z tych obrazów są wymagane nie dodatkowe zmiany.</span><span class="sxs-lookup"><span data-stu-id="1906d-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="1906d-147">Jeśli masz maszyny Wirtualnej na podstawie obrazu CoreOS starszych lub niestandardowego, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1906d-147">If you have a VM based on an older or custom CoreOS image, use the following steps:</span></span>

1. <span data-ttu-id="1906d-148">Przeprowadź edycję pliku`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="1906d-148">Edit the file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="1906d-149">Odnów adres IPv6:</span><span class="sxs-lookup"><span data-stu-id="1906d-149">Renew the IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
