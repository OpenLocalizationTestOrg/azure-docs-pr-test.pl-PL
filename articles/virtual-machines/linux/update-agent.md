---
title: "Zaktualizuj agenta systemu Linux platformy Azure z usługi GitHub | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zaktualizować agenta systemu Linux platformy Azure dla maszyny Wirtualnej systemu Linux na platformie Azure do najnowszej wersji z usługi GitHub"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: c79e37976a58ae5384b5856e0f7f258a773ef0fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-update-the-azure-linux-agent-on-a-vm"></a><span data-ttu-id="d7859-103">Jak zaktualizować agenta systemu Linux platformy Azure na maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d7859-103">How to update the Azure Linux Agent on a VM</span></span>

<span data-ttu-id="d7859-104">Aby zaktualizować Twojej [agenta systemu Linux Azure](https://github.com/Azure/WALinuxAgent) na Maszynę wirtualną systemu Linux na platformie Azure, trzeba już mieć:</span><span class="sxs-lookup"><span data-stu-id="d7859-104">To update your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="d7859-105">Uruchomionej maszyny Wirtualnej systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d7859-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="d7859-106">Połączenie z tą maszyną Wirtualną z systemem Linux przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="d7859-106">A connection to that Linux VM using SSH.</span></span>

<span data-ttu-id="d7859-107">Należy zawsze sprawdzić, czy pakiet w repozytorium distro Linux najpierw.</span><span class="sxs-lookup"><span data-stu-id="d7859-107">You should always check for a package in the Linux distro repository first.</span></span> <span data-ttu-id="d7859-108">Możliwe jest najnowszą wersję, jednak włączenie funkcji Aktualizacje automatyczne będą upewnij się, że Agent systemu Linux będzie zawsze Pobierz najnowszą aktualizację nie mogą być dostępne pakietu.</span><span class="sxs-lookup"><span data-stu-id="d7859-108">It is possible the package available may not be the latest version, however, enabling autoupdate will ensure the Linux Agent will always get the latest update.</span></span> <span data-ttu-id="d7859-109">Czy ma problemy z instalacją menedżerów pakietu, należy zwrócić pomocy technicznej od dostawcy distro.</span><span class="sxs-lookup"><span data-stu-id="d7859-109">Should you have issues installing from the package managers, you should seek support from the distro vendor.</span></span>

## <a name="updating-the-azure-linux-agent"></a><span data-ttu-id="d7859-110">Aktualizowanie Azure agenta systemu Linux</span><span class="sxs-lookup"><span data-stu-id="d7859-110">Updating the Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="d7859-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d7859-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="d7859-112">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="d7859-113">Pamięć podręczną pakietów aktualizacji</span><span class="sxs-lookup"><span data-stu-id="d7859-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="d7859-114">Zainstaluj najnowszą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-114">Install the latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="d7859-115">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="d7859-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="d7859-116">Najpierw sprawdź, czy jest włączony:</span><span class="sxs-lookup"><span data-stu-id="d7859-116">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="d7859-117">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="d7859-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="d7859-118">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="d7859-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="d7859-119">Aby włączyć uruchamianie:</span><span class="sxs-lookup"><span data-stu-id="d7859-119">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="d7859-120">Uruchom ponownie usługę agenta waagent</span><span class="sxs-lookup"><span data-stu-id="d7859-120">Restart the waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="d7859-121">Uruchom ponownie agenta dla 14.04</span><span class="sxs-lookup"><span data-stu-id="d7859-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="d7859-122">Uruchom ponownie agenta dla 16.04 / 17.04</span><span class="sxs-lookup"><span data-stu-id="d7859-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="d7859-123">Debian</span><span class="sxs-lookup"><span data-stu-id="d7859-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="d7859-124">Debian 7 "Wheezy"</span><span class="sxs-lookup"><span data-stu-id="d7859-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="d7859-125">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="d7859-126">Pamięć podręczną pakietów aktualizacji</span><span class="sxs-lookup"><span data-stu-id="d7859-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="d7859-127">Zainstaluj najnowszą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-127">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="d7859-128">Włącz Aktualizacje automatyczne agenta</span><span class="sxs-lookup"><span data-stu-id="d7859-128">Enable agent auto update</span></span>
<span data-ttu-id="d7859-129">Ta wersja Debian nie ma wersji > = 2.0.16, dlatego aktualizacje automatyczne jest niedostępna dla niego.</span><span class="sxs-lookup"><span data-stu-id="d7859-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="d7859-130">Dane wyjściowe z powyższego polecenia wyświetli, jeśli pakiet jest aktualny.</span><span class="sxs-lookup"><span data-stu-id="d7859-130">The output from the above command will show you if the package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="d7859-131">Debian 8 "Joasia" / Debian 9 "Stretch"</span><span class="sxs-lookup"><span data-stu-id="d7859-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="d7859-132">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="d7859-133">Pamięć podręczną pakietów aktualizacji</span><span class="sxs-lookup"><span data-stu-id="d7859-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="d7859-134">Zainstaluj najnowszą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-134">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="d7859-135">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="d7859-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="d7859-136">Najpierw sprawdź, czy jest włączony:</span><span class="sxs-lookup"><span data-stu-id="d7859-136">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="d7859-137">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="d7859-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="d7859-138">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="d7859-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="d7859-139">Aby włączyć uruchamianie:</span><span class="sxs-lookup"><span data-stu-id="d7859-139">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="d7859-140">Uruchom ponownie usługę agenta waagent</span><span class="sxs-lookup"><span data-stu-id="d7859-140">Restart the waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="d7859-141">RedHat / CentOS</span><span class="sxs-lookup"><span data-stu-id="d7859-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="d7859-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="d7859-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="d7859-143">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="d7859-144">Sprawdzanie dostępności aktualizacji</span><span class="sxs-lookup"><span data-stu-id="d7859-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="d7859-145">Zainstaluj najnowszą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-145">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="d7859-146">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="d7859-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="d7859-147">Najpierw sprawdź, czy jest włączony:</span><span class="sxs-lookup"><span data-stu-id="d7859-147">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="d7859-148">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="d7859-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="d7859-149">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="d7859-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="d7859-150">Aby włączyć uruchamianie:</span><span class="sxs-lookup"><span data-stu-id="d7859-150">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="d7859-151">Uruchom ponownie usługę agenta waagent</span><span class="sxs-lookup"><span data-stu-id="d7859-151">Restart the waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="d7859-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="d7859-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="d7859-153">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="d7859-154">Sprawdzanie dostępności aktualizacji</span><span class="sxs-lookup"><span data-stu-id="d7859-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="d7859-155">Zainstaluj najnowszą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-155">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="d7859-156">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="d7859-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="d7859-157">Najpierw sprawdź, czy jest włączony:</span><span class="sxs-lookup"><span data-stu-id="d7859-157">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="d7859-158">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="d7859-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="d7859-159">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="d7859-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="d7859-160">Aby włączyć uruchamianie:</span><span class="sxs-lookup"><span data-stu-id="d7859-160">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="d7859-161">Uruchom ponownie usługę agenta waagent</span><span class="sxs-lookup"><span data-stu-id="d7859-161">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="d7859-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="d7859-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="d7859-163">SUSE SLES 11 Z DODATKIEM SP4</span><span class="sxs-lookup"><span data-stu-id="d7859-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="d7859-164">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="d7859-165">Sprawdzanie dostępności aktualizacji</span><span class="sxs-lookup"><span data-stu-id="d7859-165">Check available updates</span></span>

<span data-ttu-id="d7859-166">Powyższe dane wyjściowe wyświetli, jeśli pakiet jest aktualny.</span><span class="sxs-lookup"><span data-stu-id="d7859-166">The above output will show you if the package is up to date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="d7859-167">Zainstaluj najnowszą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-167">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="d7859-168">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="d7859-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="d7859-169">Najpierw sprawdź, czy jest włączony:</span><span class="sxs-lookup"><span data-stu-id="d7859-169">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="d7859-170">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="d7859-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="d7859-171">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="d7859-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="d7859-172">Aby włączyć uruchamianie:</span><span class="sxs-lookup"><span data-stu-id="d7859-172">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="d7859-173">Uruchom ponownie usługę agenta waagent</span><span class="sxs-lookup"><span data-stu-id="d7859-173">Restart the waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="d7859-174">SUSE SLES 12 Z DODATKIEM SP2</span><span class="sxs-lookup"><span data-stu-id="d7859-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="d7859-175">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="d7859-176">Sprawdzanie dostępności aktualizacji</span><span class="sxs-lookup"><span data-stu-id="d7859-176">Check available updates</span></span>

<span data-ttu-id="d7859-177">W danych wyjściowych z powyższych spowoduje to wyświetlenie Jeśli pakiet jest maksymalnie daty.</span><span class="sxs-lookup"><span data-stu-id="d7859-177">In the output from the above, this will show you if the package is upto date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="d7859-178">Zainstaluj najnowszą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="d7859-178">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="d7859-179">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="d7859-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="d7859-180">Najpierw sprawdź, czy jest włączony:</span><span class="sxs-lookup"><span data-stu-id="d7859-180">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="d7859-181">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="d7859-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="d7859-182">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="d7859-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="d7859-183">Aby włączyć uruchamianie:</span><span class="sxs-lookup"><span data-stu-id="d7859-183">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="d7859-184">Uruchom ponownie usługę agenta waagent</span><span class="sxs-lookup"><span data-stu-id="d7859-184">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="d7859-185">Oracle 6 i 7</span><span class="sxs-lookup"><span data-stu-id="d7859-185">Oracle 6 and 7</span></span>

<span data-ttu-id="d7859-186">Upewnij się, że dla Oracle Linux `Addons` repozytorium jest włączona.</span><span class="sxs-lookup"><span data-stu-id="d7859-186">For Oracle Linux, make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="d7859-187">Wybierz edytować plik `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) lub `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) i zmień wiersz `enabled=0` do `enabled=1` w obszarze **[ol6_addons]** lub **[ol7_addons]** w tym plik.</span><span class="sxs-lookup"><span data-stu-id="d7859-187">Choose to edit the file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="d7859-188">Następnie Aby zainstalować najnowszą wersję agenta systemu Linux platformy Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="d7859-188">Then, to install the latest version of the Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="d7859-189">Jeśli nie znajdziesz repozytorium dodatek można było łatwo dodać te wiersze na końcu pliku .repo zgodnie z publikowania Oracle Linux:</span><span class="sxs-lookup"><span data-stu-id="d7859-189">If you don't find the add-on repository you can simply add these lines at the end of your .repo file according to your Oracle Linux release:</span></span>

<span data-ttu-id="d7859-190">W przypadku maszyn wirtualnych Oracle Linux 6:</span><span class="sxs-lookup"><span data-stu-id="d7859-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="d7859-191">Oracle Linux 7 maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="d7859-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="d7859-192">Następnie wpisz:</span><span class="sxs-lookup"><span data-stu-id="d7859-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="d7859-193">Zazwyczaj jest to wszystkie wymagane, ale jeśli jakiegoś powodu musisz zainstalować go z https://github.com bezpośrednio, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="d7859-193">Typically this is all you need, but if for some reason you need to install it from https://github.com directly, use the following steps.</span></span>


## <a name="update-the-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="d7859-194">Zaktualizuj agenta systemu Linux, gdy pakiet agenta, nie istnieje dla dystrybucji</span><span class="sxs-lookup"><span data-stu-id="d7859-194">Update the Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="d7859-195">Zainstaluj wget (istnieją pewne dystrybucjach, który nie należy instalować go domyślnie, takie jak wersje Redhat, CentOS i Oracle Linux 6.4 i 6.5) przez wpisanie `sudo yum install wget` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="d7859-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on the command line.</span></span>

### <a name="1-download-the-latest-version"></a><span data-ttu-id="d7859-196">1. Pobierz najnowszą wersję</span><span class="sxs-lookup"><span data-stu-id="d7859-196">1. Download the latest version</span></span>
<span data-ttu-id="d7859-197">Otwórz [wersji agenta systemu Linux platformy Azure w serwisie GitHub](https://github.com/Azure/WALinuxAgent/releases) strony sieci web, i sprawdź numer najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="d7859-197">Open [the release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out the latest version number.</span></span> <span data-ttu-id="d7859-198">(Można znaleźć wersji bieżącej, wpisując `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="d7859-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="d7859-199">Dla wersji 2.2.x lub później, wpisz:</span><span class="sxs-lookup"><span data-stu-id="d7859-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="d7859-200">Następujący wiersz jest używana wersja 2.2.0 na przykład:</span><span class="sxs-lookup"><span data-stu-id="d7859-200">The following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-the-azure-linux-agent"></a><span data-ttu-id="d7859-201">2. Zainstaluj agenta systemu Linux platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d7859-201">2. Install the Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="d7859-202">Dla wersji 2.2.x, użyj:</span><span class="sxs-lookup"><span data-stu-id="d7859-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="d7859-203">Może być konieczne zainstalowanie pakietu `setuptools` najpierw — zobacz [tutaj](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="d7859-203">You may need to install the package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="d7859-204">Następnie uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="d7859-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="d7859-205">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="d7859-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="d7859-206">Najpierw sprawdź, czy jest włączony:</span><span class="sxs-lookup"><span data-stu-id="d7859-206">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="d7859-207">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="d7859-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="d7859-208">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="d7859-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="d7859-209">Aby włączyć uruchamianie:</span><span class="sxs-lookup"><span data-stu-id="d7859-209">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-the-waagent-service"></a><span data-ttu-id="d7859-210">3. Uruchom ponownie usługę agenta waagent</span><span class="sxs-lookup"><span data-stu-id="d7859-210">3. Restart the waagent service</span></span>
<span data-ttu-id="d7859-211">Dla większości dystrybucjach systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="d7859-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="d7859-212">Ubuntu użyć:</span><span class="sxs-lookup"><span data-stu-id="d7859-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="d7859-213">Dla CoreOS użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="d7859-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-the-azure-linux-agent-version"></a><span data-ttu-id="d7859-214">4. Potwierdzenie wersji agenta systemu Linux platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d7859-214">4. Confirm the Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="d7859-215">Dla CoreOS powyższe polecenie może nie działać.</span><span class="sxs-lookup"><span data-stu-id="d7859-215">For CoreOS, the above command may not work.</span></span>

<span data-ttu-id="d7859-216">Zobaczysz, że wersja agenta systemu Linux platformy Azure został zaktualizowany do nowej wersji.</span><span class="sxs-lookup"><span data-stu-id="d7859-216">You will see that the Azure Linux Agent version has been updated to the new version.</span></span>

<span data-ttu-id="d7859-217">Aby uzyskać więcej informacji na temat agenta systemu Linux platformy Azure, zobacz [README agenta systemu Linux Azure](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="d7859-217">For more information regarding the Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>