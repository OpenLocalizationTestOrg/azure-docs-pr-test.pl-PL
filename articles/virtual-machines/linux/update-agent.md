---
title: "Witaj aaaUpdate agenta systemu Linux platformy Azure z usługi GitHub | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupdate agenta systemu Linux platformy Azure dla maszyny Wirtualnej systemu Linux w najnowszej wersji Azure toohello z usługi GitHub"
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
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a><span data-ttu-id="cac69-103">Jak tooupdate hello Azure agenta systemu Linux na maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cac69-103">How tooupdate hello Azure Linux Agent on a VM</span></span>

<span data-ttu-id="cac69-104">tooupdate Twojego [agenta systemu Linux Azure](https://github.com/Azure/WALinuxAgent) na Maszynę wirtualną systemu Linux na platformie Azure, należy wcześniej:</span><span class="sxs-lookup"><span data-stu-id="cac69-104">tooupdate your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="cac69-105">Uruchomionej maszyny Wirtualnej systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cac69-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="cac69-106">Toothat połączenia maszyny Wirtualnej systemu Linux przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="cac69-106">A connection toothat Linux VM using SSH.</span></span>

<span data-ttu-id="cac69-107">Należy zawsze sprawdzić, czy pakiet w repozytorium distro Linux hello najpierw.</span><span class="sxs-lookup"><span data-stu-id="cac69-107">You should always check for a package in hello Linux distro repository first.</span></span> <span data-ttu-id="cac69-108">Możliwe jest dostępny pakiet hello nie może być hello najnowszej wersji, jednak włączenie autoupdate zapewnia hello agenta systemu Linux będzie zawsze uzyskać hello najnowszej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="cac69-108">It is possible hello package available may not be hello latest version, however, enabling autoupdate will ensure hello Linux Agent will always get hello latest update.</span></span> <span data-ttu-id="cac69-109">Czy ma problemy z instalacją hello menedżerów pakietu, należy zwrócić wsparciu hello distro dostawcy.</span><span class="sxs-lookup"><span data-stu-id="cac69-109">Should you have issues installing from hello package managers, you should seek support from hello distro vendor.</span></span>

## <a name="updating-hello-azure-linux-agent"></a><span data-ttu-id="cac69-110">Aktualizowanie hello Azure agenta systemu Linux</span><span class="sxs-lookup"><span data-stu-id="cac69-110">Updating hello Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="cac69-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cac69-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="cac69-112">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="cac69-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="cac69-113">Pamięć podręczną pakietów aktualizacji</span><span class="sxs-lookup"><span data-stu-id="cac69-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="cac69-114">Zainstaluj najnowszą wersję pakietu hello</span><span class="sxs-lookup"><span data-stu-id="cac69-114">Install hello latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="cac69-115">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="cac69-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="cac69-116">Najpierw należy sprawdzić toosee, jeśli jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-116">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="cac69-117">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="cac69-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="cac69-118">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="cac69-119">tooenable Uruchom:</span><span class="sxs-lookup"><span data-stu-id="cac69-119">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="cac69-120">Uruchom ponownie usługę agenta waagent hello</span><span class="sxs-lookup"><span data-stu-id="cac69-120">Restart hello waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="cac69-121">Uruchom ponownie agenta dla 14.04</span><span class="sxs-lookup"><span data-stu-id="cac69-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="cac69-122">Uruchom ponownie agenta dla 16.04 / 17.04</span><span class="sxs-lookup"><span data-stu-id="cac69-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="cac69-123">Debian</span><span class="sxs-lookup"><span data-stu-id="cac69-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="cac69-124">Debian 7 "Wheezy"</span><span class="sxs-lookup"><span data-stu-id="cac69-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="cac69-125">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="cac69-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="cac69-126">Pamięć podręczną pakietów aktualizacji</span><span class="sxs-lookup"><span data-stu-id="cac69-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="cac69-127">Zainstaluj najnowszą wersję pakietu hello</span><span class="sxs-lookup"><span data-stu-id="cac69-127">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="cac69-128">Włącz Aktualizacje automatyczne agenta</span><span class="sxs-lookup"><span data-stu-id="cac69-128">Enable agent auto update</span></span>
<span data-ttu-id="cac69-129">Ta wersja Debian nie ma wersji > = 2.0.16, dlatego aktualizacje automatyczne jest niedostępna dla niego.</span><span class="sxs-lookup"><span data-stu-id="cac69-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="cac69-130">dane wyjściowe Hello hello powyżej polecenie wyświetli, jeśli pakietów hello jest aktualny.</span><span class="sxs-lookup"><span data-stu-id="cac69-130">hello output from hello above command will show you if hello package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="cac69-131">Debian 8 "Joasia" / Debian 9 "Stretch"</span><span class="sxs-lookup"><span data-stu-id="cac69-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="cac69-132">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="cac69-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="cac69-133">Pamięć podręczną pakietów aktualizacji</span><span class="sxs-lookup"><span data-stu-id="cac69-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="cac69-134">Zainstaluj najnowszą wersję pakietu hello</span><span class="sxs-lookup"><span data-stu-id="cac69-134">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="cac69-135">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="cac69-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="cac69-136">Najpierw należy sprawdzić toosee, jeśli jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-136">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="cac69-137">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="cac69-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="cac69-138">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="cac69-139">tooenable Uruchom:</span><span class="sxs-lookup"><span data-stu-id="cac69-139">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="cac69-140">Uruchom ponownie usługę agenta waagent hello</span><span class="sxs-lookup"><span data-stu-id="cac69-140">Restart hello waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="cac69-141">RedHat / CentOS</span><span class="sxs-lookup"><span data-stu-id="cac69-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="cac69-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="cac69-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="cac69-143">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="cac69-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="cac69-144">Sprawdzanie dostępności aktualizacji</span><span class="sxs-lookup"><span data-stu-id="cac69-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="cac69-145">Zainstaluj najnowszą wersję pakietu hello</span><span class="sxs-lookup"><span data-stu-id="cac69-145">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="cac69-146">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="cac69-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="cac69-147">Najpierw należy sprawdzić toosee, jeśli jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-147">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="cac69-148">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="cac69-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="cac69-149">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="cac69-150">tooenable Uruchom:</span><span class="sxs-lookup"><span data-stu-id="cac69-150">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="cac69-151">Uruchom ponownie usługę agenta waagent hello</span><span class="sxs-lookup"><span data-stu-id="cac69-151">Restart hello waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="cac69-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="cac69-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="cac69-153">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="cac69-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="cac69-154">Sprawdzanie dostępności aktualizacji</span><span class="sxs-lookup"><span data-stu-id="cac69-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="cac69-155">Zainstaluj najnowszą wersję pakietu hello</span><span class="sxs-lookup"><span data-stu-id="cac69-155">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="cac69-156">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="cac69-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="cac69-157">Najpierw należy sprawdzić toosee, jeśli jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-157">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="cac69-158">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="cac69-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="cac69-159">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="cac69-160">tooenable Uruchom:</span><span class="sxs-lookup"><span data-stu-id="cac69-160">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="cac69-161">Uruchom ponownie usługę agenta waagent hello</span><span class="sxs-lookup"><span data-stu-id="cac69-161">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="cac69-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="cac69-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="cac69-163">SUSE SLES 11 Z DODATKIEM SP4</span><span class="sxs-lookup"><span data-stu-id="cac69-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="cac69-164">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="cac69-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="cac69-165">Sprawdzanie dostępności aktualizacji</span><span class="sxs-lookup"><span data-stu-id="cac69-165">Check available updates</span></span>

<span data-ttu-id="cac69-166">Hello powyżej dane wyjściowe wyświetli, jeśli pakiet hello działa toodate.</span><span class="sxs-lookup"><span data-stu-id="cac69-166">hello above output will show you if hello package is up toodate.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="cac69-167">Zainstaluj najnowszą wersję pakietu hello</span><span class="sxs-lookup"><span data-stu-id="cac69-167">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="cac69-168">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="cac69-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="cac69-169">Najpierw należy sprawdzić toosee, jeśli jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-169">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="cac69-170">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="cac69-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="cac69-171">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="cac69-172">tooenable Uruchom:</span><span class="sxs-lookup"><span data-stu-id="cac69-172">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="cac69-173">Uruchom ponownie usługę agenta waagent hello</span><span class="sxs-lookup"><span data-stu-id="cac69-173">Restart hello waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="cac69-174">SUSE SLES 12 Z DODATKIEM SP2</span><span class="sxs-lookup"><span data-stu-id="cac69-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="cac69-175">Sprawdź bieżącą wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="cac69-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="cac69-176">Sprawdzanie dostępności aktualizacji</span><span class="sxs-lookup"><span data-stu-id="cac69-176">Check available updates</span></span>

<span data-ttu-id="cac69-177">W danych wyjściowych hello z hello powyżej spowoduje to wyświetlenie Jeśli pakietów hello jest maksymalnie daty.</span><span class="sxs-lookup"><span data-stu-id="cac69-177">In hello output from hello above, this will show you if hello package is upto date.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="cac69-178">Zainstaluj najnowszą wersję pakietu hello</span><span class="sxs-lookup"><span data-stu-id="cac69-178">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="cac69-179">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="cac69-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="cac69-180">Najpierw należy sprawdzić toosee, jeśli jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-180">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="cac69-181">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="cac69-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="cac69-182">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="cac69-183">tooenable Uruchom:</span><span class="sxs-lookup"><span data-stu-id="cac69-183">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="cac69-184">Uruchom ponownie usługę agenta waagent hello</span><span class="sxs-lookup"><span data-stu-id="cac69-184">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="cac69-185">Oracle 6 i 7</span><span class="sxs-lookup"><span data-stu-id="cac69-185">Oracle 6 and 7</span></span>

<span data-ttu-id="cac69-186">Oracle Linux, upewnij się, że hello `Addons` repozytorium jest włączona.</span><span class="sxs-lookup"><span data-stu-id="cac69-186">For Oracle Linux, make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="cac69-187">Wybierz plik hello tooedit `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) lub `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) i zmień wiersz hello `enabled=0` za`enabled=1` w obszarze **[ol6_addons]** lub **[ol7_addons]** w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="cac69-187">Choose tooedit hello file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="cac69-188">Następnie tooinstall hello najnowszą wersję hello Azure agenta systemu Linux, wpisz:</span><span class="sxs-lookup"><span data-stu-id="cac69-188">Then, tooinstall hello latest version of hello Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="cac69-189">Jeśli nie znajdziesz hello dodatek repozytorium można po prostu dodać te wiersze na końcu pliku .repo zgodnie z wersji Oracle Linux tooyour hello:</span><span class="sxs-lookup"><span data-stu-id="cac69-189">If you don't find hello add-on repository you can simply add these lines at hello end of your .repo file according tooyour Oracle Linux release:</span></span>

<span data-ttu-id="cac69-190">W przypadku maszyn wirtualnych Oracle Linux 6:</span><span class="sxs-lookup"><span data-stu-id="cac69-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="cac69-191">Oracle Linux 7 maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="cac69-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="cac69-192">Następnie wpisz:</span><span class="sxs-lookup"><span data-stu-id="cac69-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="cac69-193">Zazwyczaj jest wymagany, ale z jakiegoś powodu potrzebne tooinstall z https://github.com bezpośrednio, użyj hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="cac69-193">Typically this is all you need, but if for some reason you need tooinstall it from https://github.com directly, use hello following steps.</span></span>


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="cac69-194">Zaktualizuj hello agenta systemu Linux, gdy pakiet agenta, nie istnieje dla dystrybucji</span><span class="sxs-lookup"><span data-stu-id="cac69-194">Update hello Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="cac69-195">Zainstaluj wget (istnieją pewne dystrybucjach, który nie należy instalować go domyślnie, takie jak wersje Redhat, CentOS i Oracle Linux 6.4 i 6.5) przez wpisanie `sudo yum install wget` hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="cac69-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on hello command line.</span></span>

### <a name="1-download-hello-latest-version"></a><span data-ttu-id="cac69-196">1. Pobieranie najnowszej wersji hello</span><span class="sxs-lookup"><span data-stu-id="cac69-196">1. Download hello latest version</span></span>
<span data-ttu-id="cac69-197">Otwórz [hello wersji agenta systemu Linux platformy Azure w serwisie GitHub](https://github.com/Azure/WALinuxAgent/releases) strony sieci web, i sprawdź numer hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="cac69-197">Open [hello release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out hello latest version number.</span></span> <span data-ttu-id="cac69-198">(Można znaleźć wersji bieżącej, wpisując `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="cac69-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="cac69-199">Dla wersji 2.2.x lub później, wpisz:</span><span class="sxs-lookup"><span data-stu-id="cac69-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="cac69-200">Witaj następujący wiersz jest używana wersja 2.2.0 na przykład:</span><span class="sxs-lookup"><span data-stu-id="cac69-200">hello following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a><span data-ttu-id="cac69-201">2. Zainstaluj hello Azure agenta systemu Linux</span><span class="sxs-lookup"><span data-stu-id="cac69-201">2. Install hello Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="cac69-202">Dla wersji 2.2.x, użyj:</span><span class="sxs-lookup"><span data-stu-id="cac69-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="cac69-203">Może być konieczne pakietu hello tooinstall `setuptools` najpierw — zobacz [tutaj](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="cac69-203">You may need tooinstall hello package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="cac69-204">Następnie uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="cac69-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="cac69-205">Upewnij się, że jest włączone automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="cac69-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="cac69-206">Najpierw należy sprawdzić toosee, jeśli jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-206">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="cac69-207">Znajdź "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="cac69-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="cac69-208">Jeśli to pole wyboru jest wyświetlane, jest włączona:</span><span class="sxs-lookup"><span data-stu-id="cac69-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="cac69-209">tooenable Uruchom:</span><span class="sxs-lookup"><span data-stu-id="cac69-209">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a><span data-ttu-id="cac69-210">3. Uruchom ponownie usługę agenta waagent hello</span><span class="sxs-lookup"><span data-stu-id="cac69-210">3. Restart hello waagent service</span></span>
<span data-ttu-id="cac69-211">Dla większości dystrybucjach systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="cac69-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="cac69-212">Ubuntu użyć:</span><span class="sxs-lookup"><span data-stu-id="cac69-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="cac69-213">Dla CoreOS użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="cac69-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a><span data-ttu-id="cac69-214">4. Potwierdzenie hello wersji agenta systemu Linux platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cac69-214">4. Confirm hello Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="cac69-215">Dla CoreOS hello powyżej polecenie może nie działać.</span><span class="sxs-lookup"><span data-stu-id="cac69-215">For CoreOS, hello above command may not work.</span></span>

<span data-ttu-id="cac69-216">Pojawi się, że tego hello agenta systemu Linux Azure wersji został zaktualizowany toohello nowej wersji.</span><span class="sxs-lookup"><span data-stu-id="cac69-216">You will see that hello Azure Linux Agent version has been updated toohello new version.</span></span>

<span data-ttu-id="cac69-217">Aby uzyskać więcej informacji dotyczących hello agenta systemu Linux platformy Azure, zobacz [README agenta systemu Linux Azure](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="cac69-217">For more information regarding hello Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>
